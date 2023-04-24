---
lab:
  title: Explorer la classification d’images
  module: Module 3 - Computer Vision
---

# <a name="explore-image-classification"></a>Explorer la classification d’images

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

Le service cognitif *Vision par ordinateur* fournit des modèles prédéfinis utiles pour travailler avec les images, mais vous devrez souvent former votre propre modèle pour la vision par ordinateur. Par exemple, supposons que la société de vente au détail Northwind Traders souhaite créer un système de caisse automatisé qui identifie les articles d’épicerie que les clients veulent acheter sur la base d’une image prise par une caméra à la caisse. Pour ce faire, vous devrez former un modèle de classification capable de classer les images pour identifier l’article acheté.

Dans Azure, vous pouvez utiliser le service cognitif ***Custom Vision*** pour former un modèle de classification d’images à partir d’images existantes. Il existe deux éléments pour créer une solution de classification d’images. Tout d’abord, vous devez former un modèle pour reconnaître des classes différentes à l’aide d’images existantes. Ensuite, lorsque le modèle est formé, vous devez le publier en tant que service qui peut être consommé par des applications.

Pour tester les fonctionnalités du service Custom Vision, nous allons utiliser une simple application en ligne de commande s’exécutant dans le service Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## <a name="create-a-cognitive-services-resource"></a>Créer une ressource *Cognitive Services*

Vous pouvez utiliser le service Custom Vision en créant une ressource **Custom Vision** ou **Cognitive Services** .

>**Remarque** Toutes les ressources ne sont pas disponibles dans toutes les régions. Que la ressource à créer soit une ressource Custom Vision ou Cognitive Services, seules les ressources créées dans [certaines régions](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services) peuvent être utilisées pour accéder aux services Custom Vision. Par souci de simplicité, une région est présélectionnée pour vous dans les instructions de configuration ci-dessous.

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

1. Téléchargez et extrayez les images de formation à partir de https://aka.ms/fruit-images. Ces images sont fournies dans un dossier compressé, qui, lorsqu’il est extrait, contient des sous-dossiers appelés **apple**, **banana** et **orange**.

1. Dans un autre onglet de navigateur, ouvrez le portail Custom Vision à l’adresse [https://customvision.ai](https://customvision.ai?azure-portal=true). Si vous y êtes invité, connectez-vous en utilisant le compte Microsoft associé à votre abonnement Azure et acceptez les conditions de service.

1. Dans le portail Custom Vision, créez un nouveau projet avec les paramètres suivants :

    - **Nom** : Caisse de l’épicerie
    - **Description** : Classification d’images pour les articles
    - **Ressource**: *La ressource Custom Vision que vous avez créée précédemment*
    - **Types de projets** : Classification
    - **Types de classification** : multiclasse (une seule étiquette par image)
    - **Domaines** : Nourriture

1. Cliquez sur **Ajouter des images**, puis sélectionnez tous les fichiers du dossier **apple** que vous avez extraits. Téléchargez ensuite les fichiers image en spécifiant la balise *apple*, comme suit :

    ![Charger apple avec la balise apple](media/create-image-classification-system/upload-apples.jpg)

1. Répétez l’étape précédente pour charger les images dans le dossier **banana** avec la balise *banana* et les images du dossier **orange** avec la balise *orange*.

1. Explorez les images que vous avez chargées dans le projet Custom Vision. Il doit y avoir 15 images de chaque classe, comme suit :

    ![Images avec balises de fruits : 15 apples, 15 bananas et 15 oranges](media/create-image-classification-system/fruit.jpg)

1. Dans le projet Custom Vision, au-dessus des images, cliquez sur **Former** pour former un modèle de classification à l’aide des images avec balises. Sélectionnez l’option **Entraînement rapide**, puis attendez la fin de l’itération de formation (cette opération peut prendre une minute).

1. Une fois la formation de l’itération de modèle terminée, examinez les métriques de performance *Précision*, *Rappel* et *AP* : elles mesurent la précision de la prédiction du modèle de classification et doivent toutes être élevées.

## <a name="test-the-model"></a>Tester le modèle

Avant de publier cette itération du modèle pour que les applications puissent l’utiliser, vous devez la tester.

1. Au-dessus des métriques de performances, cliquez sur **Test rapide**.

1. Dans la zone **URL de l’image**, entrez `https://aka.ms/apple-image`, puis cliquez sur &#10132;

1. Vérifiez les prédictions retournées par votre modèle. Le score de probabilité pour *apple* devrait être le plus élevé, comme ceci :

    ![Une image avec une prédiction de classe apple](media/create-image-classification-system/test-apple.jpg)

1. Fermez la fenêtre **Test rapide**.

## <a name="publish-the-image-classification-model"></a>Publier le modèle de classification d’images

Vous êtes maintenant prêt à publier votre modèle formé et à l’utiliser à partir d’une application cliente.

1. Cliquez sur **&#128504; Publier** pour publier le modèle formé avec les paramètres suivants :
    - **Nom du modèle** : épiceries
    - **Ressource de prédiction** : *la ressource de prédiction que vous avez créée précédemment*.

1. Après la publication, cliquez sur l’*URL de prédiction* (&#127760;) pour afficher les informations requises afin d’utiliser le modèle publié. Plus tard, vous aurez besoin de l’URL et des valeurs Prediction-Key appropriées pour obtenir une prédiction à partir d’une URL d’image. Aussi, gardez cette boîte de dialogue ouverte et poursuivez avec la tâche suivante. 

## <a name="run-cloud-shell"></a>Exécuter Cloud Shell

Pour tester les fonctionnalités du service Custom Vision, nous allons utiliser une simple application en ligne de commande s’exécutant dans le service Cloud Shell sur Azure.

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail. 

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/create-image-classification-system/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    [![Créez le stockage en cliquant sur Confirmer.](media/create-image-classification-system/powershell-portal-guide-2.png)](media/create-image-classification-system/powershell-portal-guide-2.png#lightbox)

1. Assurez-vous que le type d’interpréteur de commandes sélectionné en haut à gauche du volet du service Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/create-image-classification-system/powershell-portal-guide-3.png)

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/create-image-classification-system/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>Configurer et exécuter une application cliente

Maintenant que vous disposez d’un environnement Cloud Shell, vous pouvez exécuter une application simple qui utilise le service Custom Vision pour analyser une image.

1. Dans l’interpréteur de commandes, entrez la commande suivante pour télécharger l’exemple d’application et l’enregistrer dans un dossier nommé ai-900. 

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**Conseil** Si vous avez déjà utilisé cette commande dans un autre labo pour cloner le dépôt *ai-900*, vous pouvez ignorer cette étape.

1. Les fichiers sont téléchargés dans un dossier nommé **ai-900**. À présent, nous souhaitons voir tous les fichiers de votre stockage Cloud Shell et les utiliser. Tapez la commande suivante dans l’interpréteur de commandes :

    ```PowerShell
    code .
    ```

    Notez que cela a pour effet d’ouvrir un éditeur tel que celui présenté dans l’illustration ci-dessous : 

    ![L’éditeur de code.](media/create-image-classification-system/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **classify-image.ps1**. Ce fichier contient du code qui utilise le modèle Custom Vision pour analyser une image, comme illustré ici :

     ![Éditeur contenant du code pour classifier une image](media/create-image-classification-system/classify-image-code.png)

1. Ne vous inquiétez pas trop pour les détails du code, mais sachez qu’il a besoin de l’URL et de la clé de prédiction pour votre modèle Custom Vision lors de l’utilisation d’une URL d’image. 

   Récupérez l’*URL de prédiction* dans la boîte de dialogue de votre projet Custom vision. 

   >**Remarque** N’oubliez pas que vous avez examiné l’*URL de prédiction* après la publication du modèle de classification d’images. Pour trouver l’*URL de prédiction*, accédez à l’onglet **Performances** dans votre projet, puis cliquez sur **URL de prédiction** (si l’écran est compressé, vous ne verrez peut-être qu’une icône de globe). Une boîte de dialogue s’affiche. Copiez l’URL pour **Si vous avez une URL d’image**. Collez-la dans l’éditeur de code, en remplaçant **YOUR_PREDICTION_URL**.

    À l’aide de la même boîte de dialogue, obtenez la *clé de prédiction*. Copiez la clé de prédiction affichée après *Set Prediction-Key Header to*. Collez-la dans l’éditeur de code, en remplaçant la valeur d’espace réservé **YOUR_PREDICTION_KEY**.

    ![Capture d’écran de l’URL de prédiction.](media/create-image-classification-system/find-prediction-url.png)

    Après avoir collé les valeurs d’URL de prédiction et de clé de prédiction, les deux premières lignes du code doivent ressembler à ceci :

    ```PowerShell
    $predictionUrl="https..."
    $predictionKey ="1a2b3c4d5e6f7g8h9i0j...."
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**.

    Vous allez utiliser l’exemple d’application cliente pour classer plusieurs images dans la catégorie apple, banana ou orange.

1. Nous allons classer cette image :

    ![Image d’une pomme](media/create-image-classification-system/fruit-1.jpg)

    Dans le volet PowerShell, entrez les commandes suivantes pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./classify-image.ps1 1
    ```

1. Passez en revue la prédiction, qui doit être **apple**.

1. Essayons maintenant avec une autre image :

    ![Image d’une banane](media/create-image-classification-system/fruit-2.jpg)

    Exécutez cette commande :

    ```PowerShell
    ./classify-image.ps1 2
    ```

1. Vérifiez que le modèle classe cette image en tant que **banana**.

1. Enfin, essayons la troisième image de test :

    ![Image d’une orange](media/create-image-classification-system/fruit-3.jpg)

    Exécutez cette commande :

    ```PowerShell
    ./classify-image.ps1 3
    ```

1. Vérifiez que le modèle classe cette image en **orange**.

## <a name="learn-more"></a>En savoir plus

Cette application simple ne montre que quelques fonctionnalités du service Custom Vision. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page Custom Vision](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).
