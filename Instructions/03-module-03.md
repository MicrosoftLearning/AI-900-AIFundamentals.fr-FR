---
lab:
  title: Explorer Vision par ordinateur
---

# Explorer Vision par ordinateur

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

Le service cognitif *Vision par ordinateur* utilise des modèles Machine Learning préformés pour analyser des images et extraire des informations à leur sujet.

Par exemple, supposons que la société de commerce de détail fictive *Northwind Traders* ait décidé d’établir un « Magasin intelligent » que des services d’intelligence artificielle surveillent afin d’identifier les clients nécessitant une assistance, et de guider les employés qui leur viennent en aide. Le service Vision par ordinateur permet d’analyser les images prises par les caméras du magasin pour fournir des descriptions explicites de ce qu’elles montrent.

Dans le cadre de ce labo, vous allez utiliser une application en ligne de commande simple afin de voir à l’œuvre le service Vision par ordinateur. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## Créer une ressource *Azure AI services*

Vous pouvez utiliser le service Vision par ordinateur en créant une ressource **Vision par ordinateur** ou **Azure AI services**.

Si ce n’est déjà fait, créez une ressource **Azure AI services** dans votre abonnement Azure.

1. Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Cliquez sur le bouton **&#65291;Créer une ressource** et recherchez *Cognitive Services*. Sélectionnez **Créer** un plan **Cognitive Services**. Vous accédez à une page pour créer une ressource Azure AI services. Configurez-la avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez ou créez un groupe de ressources portant un nom unique*.
    - **Région** : *choisissez une région disponible*.
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : Standard S0
    - **En cochant cette case, j’ai reconnu que j’ai lu et compris tous les termes ci-dessous** : sélectionné.

1. Examinez et créez la ressource, puis attendez la fin du déploiement. Accédez ensuite à la ressource déployée.

1. Affichez la page **Clés et points de terminaison** de votre ressource Azure AI services. Vous aurez besoin du point de terminaison et des clés pour vous connecter à partir d’applications clientes.

## Exécuter Cloud Shell

Pour tester les fonctionnalités du service Vision par ordinateur, nous allons utiliser une simple application en ligne de commande s’exécutant dans le service Cloud Shell sur Azure.

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail.

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/analyze-images-computer-vision-service/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/analyze-images-computer-vision-service/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes sélectionné en haut à gauche du volet du service Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/analyze-images-computer-vision-service/powershell-portal-guide-3.png)

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/analyze-images-computer-vision-service/powershell-prompt.png)

## Configurer et exécuter une application cliente

Maintenant que vous disposez d’un environnement Cloud Shell, vous pouvez exécuter une application simple qui utilise le service Vision par ordinateur pour analyser une image.

1. Dans l’interpréteur de commandes, entrez la commande suivante pour télécharger l’exemple d’application et l’enregistrer dans un dossier nommé ai-900.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    > **Conseil** Si vous avez déjà utilisé cette commande dans un autre labo pour cloner le dépôt *ai-900*, vous pouvez ignorer cette étape.

1. Les fichiers sont téléchargés dans un dossier nommé **ai-900**. À présent, nous souhaitons voir tous les fichiers de votre stockage Cloud Shell et les utiliser. Tapez la commande suivante dans l’interpréteur de commandes :

    ```PowerShell
    code .
    ```

    Notez que cela a pour effet d’ouvrir un éditeur tel que celui présenté dans l’illustration ci-dessous :

    ![L’éditeur de code.](media/analyze-images-computer-vision-service/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **analyze-image.ps1**. Ce fichier contient du code qui utilise le service Vision par ordinateur pour analyser une image, comme illustré ici :

    ![Éditeur contenant du code pour analyser une image](media/analyze-images-computer-vision-service/analyze-image-code.png)

1. Ne vous souciez pas trop du code. Ce qui importe, c’est qu’il a besoin de l’URL du point de terminaison, ainsi que de l’une ou l’autre des clés de votre ressource Cognitive Services. Copiez celles-ci à partir de la page **Clés et points de terminaison** de votre ressource dans le portail Azure, et collez-les dans l’éditeur de code, en remplaçant respectivement les valeurs d’espace réservé **YOUR_KEY** et **YOUR_ENDPOINT**.

    > **Conseil** Vous devrez peut-être vous servir de la barre de séparation pour ajuster la zone d’écran quand vous utilisez les volets **Clés et point de terminaison** et **Éditeur**.

    Une fois les valeurs de clé et de point de terminaison collées, les deux premières lignes de code devraient ressembler à ceci :

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications.

    L’exemple d’application cliente utilisera votre service Vision par ordinateur pour analyser l’image suivante prise par une caméra dans le magasin de Northwind Traders :

    ![Image d’un parent utilisant une caméra de téléphone portable pour prendre une photo d’un enfant dans un magasin](media/analyze-images-computer-vision-service/store-camera-1.jpg)

1. Dans le volet PowerShell, entrez les commandes suivantes pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./analyze-image.ps1 store-camera-1.jpg
    ```

1. Examinez les résultats de l’analyse d’image, à savoir :
    - légende suggérée décrivant l’image ;
    - liste des objets identifiés dans l’image ;
    - liste d’« étiquettes » pertinentes pour l’image.

1. Essayons maintenant avec une autre image :

    ![Image d’une personne munie d’un panier d’achat dans un supermarché](media/analyze-images-computer-vision-service/store-camera-2.jpg)

    Pour analyser la deuxième image, entrez la commande suivante :

    ```PowerShell
    ./analyze-image.ps1 store-camera-2.jpg
    ```

1. Examinez les résultats de l’analyse pour la deuxième image.

1. Essayons avec une image supplémentaire :

    ![Image d’une personne munie d’un caddie](media/analyze-images-computer-vision-service/store-camera-3.jpg)

    Pour analyser la troisième image, entrez la commande suivante :

    ```PowerShell
    ./analyze-image.ps1 store-camera-3.jpg
    ```

1. Examinez les résultats de l’analyse pour la troisième image.

## En savoir plus

Cette application simple ne montre que quelques fonctionnalités du service Vision par ordinateur. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [Vision par ordinateur](https://azure.microsoft.com/products/ai-services?activetab=pivot:visiontab).
