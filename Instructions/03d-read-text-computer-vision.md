---
lab:
  title: Explorer la reconnaissance optique de caractères
---

# Explorer la reconnaissance optique de caractères

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

L’un des défis courants en matière de vision par ordinateur consiste à détecter et interpréter le texte contenu dans une image. Ce type de traitement est souvent appelé *reconnaissance optique de caractères* (OCR). L’API Read de Microsoft permet d’accéder aux fonctionnalités d’OCR. 

Pour tester les fonctionnalités de l’API Read, nous allons utiliser une simple application en ligne de commande qui s’exécute dans Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## Utiliser le service Vision par ordinateur pour lire du texte dans une image

Le service cognitif **Vision par ordinateur** prend en charge les tâches d’OCR, à savoir :

- Une API **Read** optimisée pour les documents plus volumineux. Cette API est utilisée de manière asynchrone et peut être utilisée pour du texte tant imprimé que manuscrit.

## Créer une ressource *Cognitive Services*

Vous pouvez utiliser le service Vision par ordinateur en créant une ressource **Vision par ordinateur** ou **Cognitive Services** .

Si ce n’est déjà fait, créez une ressource **Cognitive Services** dans votre abonnement Azure.

1. Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Cliquez sur le bouton **&#65291;Créer une ressource**, recherchez *Cognitive Services*, puis créez une ressource **Cognitive Services** avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez ou créez un groupe de ressources portant un nom unique*.
    - **Région** : *choisissez une région disponible*.
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : Standard S0
    - **En cochant cette case, j’ai reconnu que j’ai lu et compris tous les termes ci-dessous** : sélectionné.

1. Examinez et créez la ressource, puis attendez la fin du déploiement. Accédez ensuite à la ressource déployée.

1. Affichez la page **Clés et point de terminaison** de votre ressource Cognitive Services. Vous aurez besoin du point de terminaison et des clés pour vous connecter à partir d’applications clientes.

## Exécuter Cloud Shell

Pour tester les fonctionnalités du service Custom Vision, nous allons utiliser une simple application en ligne de commande s’exécutant dans le service Cloud Shell sur Azure.

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail. 

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/read-text-computer-vision/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/read-text-computer-vision/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes sélectionné en haut à gauche du volet du service Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/read-text-computer-vision/powershell-portal-guide-3.png) 

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/read-text-computer-vision/powershell-prompt.png) 

## Configurer et exécuter une application cliente

À présent que vous disposez d’un modèle personnalisé, vous pouvez exécuter une simple application cliente utilisant le service OCR.

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

    ![L’éditeur de code.](media/read-text-computer-vision/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **ocr.ps1**. Ce fichier contient du code qui utilise le service Vision par ordinateur pour détecter et analyser du texte dans une image, comme illustré ici :

    ![Éditeur contenant du code pour analyser du texte figurant dans des images.](media/read-text-computer-vision/ocr-code.png)

1. Ne vous souciez pas trop des détails du code. Ce qui importe, c’est qu’il a besoin de l’URL du point de terminaison, ainsi que de l’une ou l’autre des clés de votre ressource Cognitive Services. Copiez celles-ci à partir de la page **Clés et points de terminaison** de votre ressource dans le portail Azure, et collez-les dans l’éditeur de code, en remplaçant respectivement les valeurs d’espace réservé **YOUR_KEY** et **YOUR_ENDPOINT**.

    > **Conseil** Vous devrez peut-être vous servir de la barre de séparation pour ajuster la zone d’écran quand vous utilisez les volets **Clés et point de terminaison** et **Éditeur**.

    Une fois les valeurs de clé et de point de terminaison collées, les deux premières lignes de code devraient ressembler à ceci :

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**. Maintenant que vous avez configuré la clé et le point de terminaison, vous pouvez utiliser votre ressource Cognitive Services pour extraire le texte d’une image.

    Utilisons l’API **Read**. Dans ce cas, vous disposez d’une image publicitaire pour la société fictive de vente au détail Northwind Traders, qui comprend du texte.

    L’exemple d’application cliente analyse l’image suivante :

    ![Image d’une publication pour le supermarché Northwind Traders.](media/read-text-computer-vision/advert.jpg)

1. Dans le volet PowerShell, entrez les commandes suivantes pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./ocr.ps1 advert.jpg
    ```

1. Passez en revue les détails trouvés dans l’image. Le texte trouvé dans l’image est organisé dans une structure hiérarchique de régions, de lignes et de mots, et le code les lit pour extraire les résultats.

    Notez que l’emplacement d’un texte est indiqué par les coordonnées du point supérieur gauche, associées à la largeur et la hauteur d’un *cadre englobant*, comme illustré ici :

    ![Image du texte dans l’image détourée](media/read-text-computer-vision/lab-05-bounding-boxes.png)

1. Essayons maintenant avec une autre image :

    ![Image d’une lettre dactylographiée.](media/read-text-computer-vision/letter.jpg)

    Pour analyser la deuxième image, entrez la commande suivante :

    ```PowerShell
    ./ocr.ps1 letter.jpg
    ```

1. Examinez les résultats de l’analyse pour la deuxième image. Elle doit également retourner le texte et les cadres englobants du texte.

## En savoir plus

Cette application simple ne montre que quelques fonctionnalités d’OCR du service Vision par ordinateur. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page OCR](https://docs.microsoft.com/azure/cognitive-services/computer-vision/overview-ocr).
