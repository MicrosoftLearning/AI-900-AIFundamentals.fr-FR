---
lab:
  title: Explorer la détection d’objet
---

# <a name="explore-object-detection"></a>Explorer la détection d’objet

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

La *détection d’objet* est une forme de vision informatique dans laquelle un modèle Machine Learning est formé pour classer des instances d’objet individuelles dans une image et indiquer un *rectangle englobant* qui marque son emplacement. Vous pouvez considérer cela comme une progression de la *classification d’images* (dans laquelle le modèle répond à la question « De quoi est-ce une image ? ») pour créer des solutions où nous pouvons demander au modèle « Quels objets sont sur cette image, et où ? ».

Par exemple, une épicerie peut utiliser un modèle de détection d’objet pour mettre en œuvre un système de caisse automatisé qui scanne un tapis roulant à l’aide d’une caméra et peut identifier des articles spécifiques sans avoir à placer chaque article sur le tapis et à le scanner individuellement.

Le service cognitif **Custom Vision** dans Microsoft Azure fournit une solution basée sur le cloud pour la création et la publication de modèles de détection d’objet personnalisés. Dans Azure, vous pouvez utiliser le service Custom Vision pour former un modèle de classification d’images à partir d’images existantes. Il existe deux éléments pour créer une solution de classification d’images. Tout d’abord, vous devez former un modèle pour reconnaître des classes différentes à l’aide d’images existantes. Ensuite, lorsque le modèle est formé, vous devez le publier en tant que service qui peut être consommé par des applications.

Pour tester les fonctionnalités du service Custom Vision afin de détecter des objets dans des images, nous allons utiliser une simple application en ligne de commande s’exécutant dans le service Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## <a name="create-a-cognitive-services-resource"></a>Créer une ressource *Cognitive Services*

Vous pouvez utiliser le service Custom Vision en créant une ressource **Custom Vision** ou **Cognitive Services** .

> **Remarque** Toutes les ressources ne sont pas disponibles dans toutes les régions. Que la ressource à créer soit une ressource Custom Vision ou Cognitive Services, seules les ressources créées dans [certaines régions](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services) peuvent être utilisées pour accéder aux services Custom Vision. Par souci de simplicité, une région est présélectionnée pour vous dans les instructions de configuration ci-dessous.

Créez une ressource **Cognitive Services** dans votre abonnement Azure.

1. Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Cliquez sur le bouton **&#65291;Créer une ressource**, recherchez *Cognitive Services*, puis créez une ressource **Cognitive Services** avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez ou créez un groupe de ressources portant un nom unique*.
    - **Région** : USA Est
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : Standard S0
    - **En cochant cette case, j’ai reconnu que j’ai lu et compris tous les termes ci-dessous** : sélectionné.

1. Examinez et créez la ressource, puis attendez la fin du déploiement. Accédez ensuite à la ressource déployée.

1. Affichez la page **Clés et point de terminaison** de votre ressource Cognitive Services. Vous aurez besoin du point de terminaison et des clés pour vous connecter à partir d’applications clientes.

## <a name="create-a-custom-vision-project"></a>Créer un projet Custom Vision

Pour former un modèle de détection d’objets, vous devez créer un projet Custom Vision basé sur votre ressource de formation. Pour ce faire, vous allez utiliser le portail Custom Vision.

1. Dans un nouvel onglet de navigateur, ouvrez le portail Custom Vision à l’adresse [https://customvision.ai](https://customvision.ai?azure-portal=true) et connectez-vous avec le compte Microsoft associé à votre abonnement Azure.

1. Créez un nouveau projet avec les paramètres suivants :
    - **Nom** : Détection d’épicerie
    - **Description** : Détection d’articles d’épicerie.
    - **Ressource** : *La ressource que vous avez créée précédemment*
    - **Types de projets** : Détection d’objets
    - **Domaines** : Général

1. Attendez que le projet soit créé et ouvert dans le navigateur.

## <a name="add-and-tag-images"></a>Ajouter et baliser des images

Pour former un modèle de détection d’objets, vous devez télécharger des images qui contiennent les classes que vous souhaitez que le modèle identifie, et les marquer pour qu’elles indiquent des zones englobantes pour chaque instance d’objet.

1. Téléchargez et extrayez les images de formation à partir de https://aka.ms/fruit-objects. Le dossier extrait contient une collection d’images de fruits.

1. Dans le portail Custom Vision [https://customvision.ai](https://customvision.ai?azure-portal=true), assurez-vous que vous travaillez dans votre projet de détection d’objet _Détection d’épicerie_. Sélectionnez ensuite **Ajouter des images** et chargez toutes les images du dossier extrait.

    ![Chargez les images téléchargées en cliquant sur Ajouter des images.](media/create-object-detection-solution/fruit-upload.jpg)

1. Une fois les images téléchargées, sélectionnez la première pour l’ouvrir.

1. Maintenez la souris sur un objet dans l’image jusqu’à ce qu’une zone détectée automatiquement soit affichée comme l’image ci-dessous. Sélectionnez ensuite l’objet et, si nécessaire, redimensionnez la région pour l’entourer.

    ![Région par défaut d’un objet](media/create-object-detection-solution/object-region.jpg)

    Vous pouvez aussi simplement faire glisser le curseur autour de l’objet pour créer une région.

1. Lorsque la région entoure l’objet, ajoutez une nouvelle balise avec le type d’objet approprié (*apple*, *banana* ou *orange*) comme indiqué ici :

    ![Objet balisé dans une image](media/create-object-detection-solution/object-tag.jpg)

1. Sélectionnez et marquez chaque autre objet dans l’image, en redimensionnant les régions et en ajoutant de nouvelles balises selon les besoins.

    ![Deux objets avec des balises dans une image](media/create-object-detection-solution/object-tags.jpg)

1. Utilisez le lien **>** situé à droite pour accéder à l’image suivante et baliser ses objets. Il vous suffit ensuite de continuer à travailler sur la totalité de la collection d’images, en marquant chaque pomme, banane et orange.

1. Lorsque vous avez terminé de marquer la dernière image, fermez l’éditeur **Détails de l’image** et, dans la page **Images de formation**, sous **Balises**, sélectionnez **Avec balise** pour afficher toutes vos images avec balises :

    ![Images avec balise dans un projet](media/create-object-detection-solution/tagged-images.jpg)

## <a name="train-and-test-a-model"></a>Formation et test d’un modèle

Maintenant que vous avez balisé les images de votre projet, vous pouvez former un modèle.

1. Dans le projet Custom Vision, cliquez sur **Former** pour former un modèle de détection d’objets à l’aide des images balisées. Sélectionnez l’option **Entraînement rapide**.

1. Attendez la fin de la formation (10 minutes environ), puis passez en revue les métriques de performances de *Précision*, de *Rappel* et de *mAP* : ces métriques mesurent la qualité de la prédiction du modèle de détection d’objet et doivent toutes être élevées.

1. En haut à droite de la page, cliquez sur **Test rapide**, puis dans la zone **URL de l’image**, entrez `https://aka.ms/apple-orange` et affichez la prédiction générée. Fermez ensuite la fenêtre **Test rapide**.

## <a name="publish-the-object-detection-model"></a>Publier le modèle de détection d’objet

Vous êtes maintenant prêt à publier votre modèle formé et à l’utiliser à partir d’une application cliente.

1. Cliquez sur **&#128504; Publier** pour publier le modèle formé avec les paramètres suivants :
    - **Nom du modèle** : détecter-produire
    - **Ressource de prédiction** : *ressource que vous avez créée*.

1. Après la publication, cliquez sur l’*URL de prédiction* (&#127760;) pour afficher les informations requises afin d’utiliser le modèle publié. Plus tard, vous aurez besoin de l’URL et des valeurs Prediction-Key appropriées pour obtenir une prédiction à partir d’une URL d’image. Aussi, gardez cette boîte de dialogue ouverte et poursuivez avec la tâche suivante.

## <a name="run-cloud-shell"></a>Exécuter Cloud Shell

Pour tester les fonctionnalités du service Custom Vision, nous allons utiliser une simple application en ligne de commande s’exécutant dans le service Cloud Shell sur Azure.

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail. 

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/create-object-detection-solution/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/create-object-detection-solution/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes indiqué en haut à gauche du volet Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/create-object-detection-solution/powershell-portal-guide-3.png) 

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/create-object-detection-solution/powershell-prompt.png) 

## <a name="configure-and-run-a-client-application"></a>Configurer et exécuter une application cliente

Maintenant que vous disposez d’un modèle personnalisé, vous pouvez exécuter une application cliente simple qui utilise le service Custom Vision pour détecter des objets dans une image.

1. Dans l’interpréteur de commandes, entrez la commande suivante pour télécharger l’exemple d’application et l’enregistrer dans un dossier nommé ai-900.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**Remarque** Si vous avez déjà utilisé cette commande dans un autre labo pour cloner le dépôt *ai-900*, vous pouvez ignorer cette étape.

1. Les fichiers sont téléchargés dans un dossier nommé **ai-900**. À présent, nous souhaitons voir tous les fichiers de votre stockage Cloud Shell et les utiliser. Tapez la commande suivante dans l’interpréteur de commandes :

    ```PowerShell
    code .
    ```

    Notez que cela a pour effet d’ouvrir un éditeur tel que celui présenté dans l’illustration ci-dessous : 

    ![L’éditeur de code.](media/create-object-detection-solution/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **detect-objects.ps1**. Ce fichier contient du code qui utilise le service Custom Vision pour détecter des objets une image, comme illustré ici :

    ![Éditeur contenant du code pour détecter les articles dans une image](media/create-object-detection-solution/detect-image-code.png)

1. Ne vous inquiétez pas trop pour les détails du code, mais sachez qu’il a besoin de l’URL et de la clé de prédiction pour votre modèle Custom Vision lors de l’utilisation d’une URL d’image. 

    Récupérez l’*URL de prédiction* dans la boîte de dialogue de votre projet Custom vision. 

    >**Remarque** N’oubliez pas que vous avez examiné l’*URL de prédiction* après la publication du modèle de classification d’images. Pour trouver l’*URL de prédiction*, accédez à l’onglet **Performances** dans votre projet, puis cliquez sur **URL de prédiction** (si l’écran est compressé, vous ne verrez peut-être qu’une icône de globe). Une boîte de dialogue s’ouvre. Copiez l’URL pour **Si vous avez une URL d’image**. Collez-la dans l’éditeur de code, en remplaçant **YOUR_PREDICTION_URL**. 

    À l’aide de la même boîte de dialogue, obtenez la *clé de prédiction*. Copiez la clé de prédiction affichée après *Set Prediction-Key Header to*. Collez-la dans l’éditeur de code, en remplaçant la valeur d’espace réservé **YOUR_PREDICTION_KEY**. 

    ![Capture d’écran de l’URL de prédiction.](media/create-object-detection-solution/find-prediction-url.png)

    Après avoir collé les valeurs d’URL de prédiction et de clé de prédiction, les deux premières lignes du code doivent ressembler à ceci :

    ```PowerShell
    $predictionUrl="https..."
    $predictionKey ="1a2b3c4d5e6f7g8h9i0j...."
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**.

    Vous allez utiliser l’exemple d’application cliente pour détecter des objets dans cette image :

    ![Image d’un fruit](media/create-object-detection-solution/produce.jpg)

1. Dans le volet PowerShell, entrez la commande suivante pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./detect-objects.ps1 
    ```

1. Passez en revue la prédiction, qui doit correspondre à *apple orange banana*.

## <a name="learn-more"></a>En savoir plus

Cette application simple ne montre que quelques fonctionnalités du service Custom Vision. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page Custom Vision](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).
