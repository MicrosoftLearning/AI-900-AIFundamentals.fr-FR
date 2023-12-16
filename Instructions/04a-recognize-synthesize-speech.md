---
lab:
  title: Explorer la reconnaissance vocale/synthèse vocale
---

# Explorer la reconnaissance vocale/synthèse vocale

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

Pour créer un logiciel capable d’interpréter la parole audible et de réagir de manière appropriée, vous pouvez utiliser le service cognitif **Azure AI Speech**, qui offre un moyen simple de transcrire la langue parlée en texte et vice versa.

Supposons, par exemple, que vous souhaitiez créer un appareil intelligent qui peut répondre oralement à des questions orales, par exemple « Quelle heure est-il ? ». La réponse doit être l’heure locale.

Pour tester les fonctionnalités du service Speech, nous allons utiliser une simple application de ligne de commande s’exécutant dans le service Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## Créer une ressource *Azure AI services*

Vous pouvez utiliser le service Speech en créant une ressource **Speech** ou **Azure AI services**.

Si ce n’est déjà fait, créez une ressource **Azure AI services** dans votre abonnement Azure.

1. Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Cliquez sur le bouton **&#65291;Créer une ressource** et recherchez *Azure AI services*. Sélectionnez **créer** un plan **Azure AI services**. Vous accédez à une page pour créer une ressource Azure AI services. Configurez-la avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez ou créez un groupe de ressources portant un nom unique*.
    - **Région** : *choisissez une région disponible*.
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : Standard S0
    - **En cochant cette case, j’ai reconnu que j’ai lu et compris tous les termes ci-dessous** : sélectionné.

1. Examinez et créez la ressource.

### Obtenez la Clé et l’Emplacement de votre ressource Azure AI services

1. Attendez la fin du déploiement. Accédez ensuite à votre ressource Azure AI services, puis, dans la page **Vue d’ensemble**, cliquez sur le lien pour gérer les clés du service. Vous aurez besoin du point de terminaison et des clés pour vous connecter à votre ressource Azure AI services à partir d’applications clientes.

1. Affichez la page **Clés et point de terminaison** de votre ressource. Vous aurez besoin de **l’emplacement ou la région** et de la **clé** pour vous connecter à partir d’applications clientes.

## Exécuter Cloud Shell

Pour tester les fonctionnalités du service Speech, nous allons utiliser une simple application de ligne de commande s’exécutant dans le service Cloud Shell sur Azure.

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail.

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/recognize-synthesize-speech/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/recognize-synthesize-speech/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes sélectionné en haut à gauche du volet du service Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/recognize-synthesize-speech/powershell-portal-guide-3.png)

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/recognize-synthesize-speech/powershell-prompt.png)

## Configurer et exécuter une application cliente

À présent que vous disposez d’un modèle personnalisé, vous pouvez exécuter une simple application cliente utilisant le service Speech.

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

    ![L’éditeur de code.](media/recognize-synthesize-speech/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **speaking-clock.ps1**. Ce fichier contient du code qui utilise le service de reconnaissance vocale pour reconnaître et synthétiser la parole :

    ![Éditeur contenant du code pour utiliser le service Speech](media/recognize-synthesize-speech/speaking-clock-code.png)

1. Ne vous souciez pas trop des détails du code. Ce qui est important, c’est qu’il a besoin de la région ou de l’emplacement, ainsi que de l’une ou l’autre des clés de votre ressource Azure AI services. Copiez celles-ci à partir de la page **Clés et points de terminaison** de votre ressource dans le portail Azure, et collez-les dans l’éditeur de code, en remplaçant respectivement les valeurs d’espace réservé **YOUR_KEY** et **YOUR_LOCATION**.

    > **Conseil** Vous devrez peut-être vous servir de la barre de séparation pour ajuster la zone d’écran quand vous utilisez les volets **Clés et point de terminaison** et **Éditeur**.

    Une fois les valeurs de clé et de région/emplacement collées, les premières lignes de code devraient ressembler à ceci :

    ```PowerShell
    $key = "1a2b3c4d5e6f7g8h9i0j...."
    $region="somelocation"
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**.

    L’exemple d’application cliente utilise votre service vocal pour transcrire les entrées vocales, et synthétise une réponse orale appropriée. Une application réelle peut accepter l’entrée d’un microphone et envoyer la réponse à un orateur mais, dans cet exemple simple, nous allons utiliser une entrée pré-enregistrée dans un fichier et enregistrer la réponse dans un autre.

    Utilisez le lecteur vidéo ci-dessous pour entendre le son d’entrée que l’application va traiter :

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWMAvi" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>

1. Dans le volet PowerShell, entrez la commande suivante pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./speaking-clock.ps1
    ```

1. Passez en revue la sortie, qui aurait normalement reconnu le texte « Quelle heure est-il ? » et enregistré une réponse appropriée dans un fichier nommé *output.wav*.

    Utilisez le lecteur vidéo suivant pour entendre la sortie parlée générée par l’application :

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWMSIU" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>

## En savoir plus

Cette application simple ne montre que quelques fonctionnalités du service Speech. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page Speech](https://azure.microsoft.com/services/cognitive-services/speech-services/).
