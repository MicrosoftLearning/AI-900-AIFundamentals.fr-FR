---
lab:
  title: Explorer la reconnaissance de formulaire
---

# <a name="explore-form-recognition"></a>Explorer la reconnaissance de formulaire

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

Dans le champ Intelligence artificielle (IA) du service Vision par ordinateur, la reconnaissance optique de caractères (OCR) est couramment utilisée pour lire des documents imprimés ou manuscrits. Souvent, le texte est simplement extrait des documents dans un format utilisable à des fins d’analyse ou de traitement ultérieurs.

Un scénario d’OCR plus avancé consiste à extraire des informations de formulaires tels que des bons de commande ou des factures, avec une compréhension sémantique de ce que représentent les champs du formulaire. Le service **Form Recognizer** est spécifiquement conçu pour ce type de problème d’IA.

Il utilise des modèles Machine Learning formés pour extraire du texte d’images de factures, reçus et autres documents. Si d’autres modèles de vision par ordinateur peuvent capturer du texte, le service Form Recognizer capture également la structure du texte, par exemple, des paires clé-valeur et des informations contenues dans des tables. De cette façon, au lieu de devoir taper manuellement les entrées d’un formulaire dans une base de données, vous pouvez capturer automatiquement les relations entre des éléments de texte du fichier d’origine. 

Pour tester les fonctionnalités du service Form Recognizer, nous allons utiliser une simple application de ligne de commande s’exécutant dans le service Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## <a name="create-a-cognitive-services-resource"></a>Créer une ressource *Cognitive Services*

Vous pouvez utiliser le service Form Recognizer en créant une ressource **Form Recognizer** ou **Cognitive Services** .

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

## <a name="run-cloud-shell"></a>Exécuter Cloud Shell

Pour tester les fonctionnalités du service Form Recognizer, nous allons utiliser une simple application de ligne de commande s’exécutant dans le service Cloud Shell sur Azure. 

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail. 

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/analyze-receipts/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/analyze-receipts/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes sélectionné en haut à gauche du volet du service Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/analyze-receipts/powershell-portal-guide-3.png) 

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/analyze-receipts/powershell-prompt.png) 

## <a name="configure-and-run-a-client-application"></a>Configurer et exécuter une application cliente

À présent que vous disposez d’un modèle personnalisé, vous pouvez exécuter une simple application cliente utilisant le service Form Recognizer.

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

    ![L’éditeur de code.](media/analyze-receipts/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **form-recognizer.ps1**. Ce fichier contient du code qui utilise le service Form Recognizer pour analyser les champs d’un reçu, comme illustré ici :

    ![Éditeur contenant du code pour analyser les champs d’un reçu.](media/analyze-receipts/recognize-receipt-code.png)

1. Ne vous souciez pas trop des détails du code. Ce qui importe, c’est qu’il a besoin de l’URL du point de terminaison, ainsi que de l’une ou l’autre des clés de votre ressource Cognitive Services. Copiez celles-ci à partir de la page **Clés et points de terminaison** de votre ressource dans le portail Azure, et collez-les dans l’éditeur de code, en remplaçant respectivement les valeurs d’espace réservé **YOUR_KEY** et **YOUR_ENDPOINT**.

    > **Conseil** Vous devrez peut-être vous servir de la barre de séparation pour ajuster la zone d’écran quand vous utilisez les volets **Clés et point de terminaison** et **Éditeur**.

    Une fois les valeurs de clé et de point de terminaison collées, les deux premières lignes de code devraient ressembler à ceci :

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**. À présent que vous avez configuré la clé et le point de terminaison, vous pouvez utiliser votre ressource pour analyser les champs d’un reçu. Dans ce cas, vous allez utiliser le modèle intégré du service Form Recognizer afin d’analyser un reçu pour la société fictive de vente au détail Northwind Traders.

    L’exemple d’application cliente analyse l’image suivante :

    ![Image d’un reçu.](media/analyze-receipts/receipt.jpg)

1. Dans le volet PowerShell, entrez les commandes suivantes pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./form-recognizer.ps1
    ```

1. Examinez les résultats retournés. Vérifiez que le service Form Recognizer est capable d’interpréter les données figurant dans le formulaire, d’identifier correctement les adresse et numéro de téléphone du marchand, les date et heure de transaction, ainsi que les lignes, les sous-totaux, les taxes et les montants totaux.

## <a name="learn-more"></a>En savoir plus

Cette application simple ne montre que quelques fonctionnalités de Form Recognizer du service Vision par ordinateur. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page Form Recognizer](https://docs.microsoft.com/azure/applied-ai-services/form-recognizer/overview).
