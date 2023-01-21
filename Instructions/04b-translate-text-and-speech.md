---
lab:
  title: Explorer la traduction
---

# <a name="explore-translation"></a>Explorer la traduction

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

L’une des forces motrices qui ont permis à la civilisation humaine de se développer est sa capacité à communiquer. La communication est au cœur de la plupart des activités humaines.

L’intelligence artificielle (IA) peut simplifier la communication en traduisant un discours écrit ou verbal dans différentes langues, ce qui contribue à éliminer les obstacles à la communication entre les pays et les cultures.

Pour tester les fonctionnalités du service Traducteur, nous allons utiliser une simple application de ligne de commande s’exécutant dans le service Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## <a name="create-a-cognitive-services-resource"></a>Créer une ressource *Cognitive Services*

Vous pouvez utiliser le service Traducteur en créant une ressource **Traducteur** ou **Cognitive Services** .

Si ce n’est déjà fait, créez une ressource **Cognitive Services** dans votre abonnement Azure.

1. Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Sélectionnez le bouton **&#65291;Créer une ressource**, recherchez *Cognitive Services*, puis créez une ressource **Cognitive Services** avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez ou créez un groupe de ressources portant un nom unique*.
    - **Région** : *choisissez une région disponible*.
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : Standard S0
    - **En cochant cette case, j’ai reconnu que j’ai lu et compris tous les termes ci-dessous** : sélectionné.

1. Examinez et créez la ressource, puis attendez la fin du déploiement. Accédez ensuite à la ressource déployée.

1. Affichez la page **Clés et point de terminaison** de votre ressource Cognitive Services. Vous aurez besoin des clés et de l’emplacement pour vous connecter à partir d’applications clientes.

### <a name="get-the-key-and-location-for-your-cognitive-services-resource"></a>Obtenir la clé et l’emplacement de votre ressource Cognitive Services

1. Attendez la fin du déploiement. Accédez ensuite à votre ressource Cognitive Services, puis, dans la page **Vue d’ensemble**, cliquez sur le lien pour gérer les clés du service. Vous aurez besoin de l’emplacement et des clés pour vous connecter à votre ressource Cognitive Services à partir d’applications clientes.

1. Affichez la page **Clés et point de terminaison** de votre ressource. Vous aurez besoin de **l’emplacement ou la région** et de la **clé** pour vous connecter à partir d’applications clientes.

> **Remarque** Pour utiliser le service Translator, vous n’avez pas besoin du point de terminaison Cognitive Services. Un point de terminaison global dédié au service Traducteur est fourni. 

## <a name="run-cloud-shell"></a>Exécuter Cloud Shell

Pour tester les fonctionnalités du service Traduction, nous allons utiliser une simple application en ligne de commande s’exécutant dans le service Cloud Shell sur Azure. 

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail.

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/translate-text-and-speech/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/translate-text-and-speech/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes indiqué en haut à gauche du volet Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant. 

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/translate-text-and-speech/powershell-portal-guide-3.png) 

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/translate-text-and-speech/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>Configurer et exécuter une application cliente

À présent que vous disposez d’un modèle personnalisé, vous pouvez exécuter une simple application cliente utilisant le service Traduction.

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

    ![L’éditeur de code.](media/translate-text-and-speech/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **translator.ps1**. Ce fichier contient du code utilisant le service Traducteur :

    ![Éditeur contenant du code pour utiliser le service Traducteur](media/translate-text-and-speech/translate-code.png)

1. Ne vous souciez pas trop des détails du code. Ce qui importe, c’est qu’il a besoin de la région ou de l’emplacement, ainsi que de l’une ou l’autre des clés de votre ressource Cognitive Services. Copiez celles-ci à partir de la page **Clés et points de terminaison** de votre ressource dans le portail Azure, puis collez-les dans l’éditeur de code, en remplaçant respectivement les valeurs d’espace réservé **YOUR_KEY** et **YOUR_LOCATION**.

    Une fois les valeurs de clé et d’emplacement collées, les premières lignes de code devraient ressembler à ceci :

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."
    $location="somelocation"
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**.

    L’exemple d’application cliente va utiliser le service Traducteur pour accomplir quelques tâches :
    - traduire le texte anglais en français, italien et chinois ;
    - traduire et convertir l’audio anglais en texte français.

    Utilisez le lecteur vidéo ci-dessous pour entendre le son d’entrée que l’application va traiter :

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWORN0" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>


    > **Remarque** Une application réelle peut accepter l’entrée provenant d’un microphone et envoyer la réponse à un orateur. Toutefois, dans cet exemple simple, nous allons utiliser une entrée préenregistrée dans un fichier audio.

1. Dans le volet sur service Cloud Shell, entrez la commande suivante pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./translator.ps1
    ```

1. Passez en revue la sortie. Avez-vous vu la traduction du texte anglais en français, italien et chinois ?  Avez-vous vu l’audio anglais « hello » traduit et converti en texte français ?

## <a name="learn-more"></a>En savoir plus

Cette application simple ne montre que quelques fonctionnalités du service Traducteur. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page Traducteur](https://docs.microsoft.com/azure/cognitive-services/translator/translator-overview).