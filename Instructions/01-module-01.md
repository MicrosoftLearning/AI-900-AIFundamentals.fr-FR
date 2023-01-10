---
lab:
  title: Explorer les services cognitifs
---

# <a name="explore-cognitive-services"></a>Explorer les services cognitifs

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

Azure Cognitive Services encapsule des fonctionnalités IA courantes qui peuvent être catégorisées en quatre groupes principaux : la vision, la reconnaissance vocale/synthèse vocale, le langage et la décision. Dans cet exercice, vous allez examiner l’un des services de décision pour avoir une idée générale du provisionnement et de l’utilisation d’une ressource Cognitive Services dans une application logicielle.

La ressource Cognitive Services que vous allez explorer dans cet exercice est le *Détecteur d’anomalies*. Le Détecteur d’anomalies permet d’analyser les valeurs des données au fil du temps, et de détecter toutes les valeurs inhabituelles susceptibles d’indiquer un problème ou de nécessiter une investigation plus approfondie. Par exemple, un capteur dans une installation de stockage avec contrôle de la température peut effectuer un monitoring de la température toutes les minutes et journaliser les valeurs mesurées. Vous pouvez utiliser le service Détecteur d’anomalies pour analyser les valeurs de température journalisées, et marquer celles qui se situent considérablement en dehors de la plage normale des températures attendues.

Pour tester les fonctionnalités du service Détection d'anomalie, nous allons utiliser une application de ligne de commande simple s’exécutant dans Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

> **Remarque** L’objectif de cet exercice est d’avoir une idée générale de la façon dont les services Cognitive Services sont provisionnés et utilisés. Le Détecteur d’anomalies est utilisé à titre d’exemple, mais vous n’êtes pas censé acquérir une connaissance complète de la détection d’anomalie dans cet exercice !

## <a name="create-an-anomaly-detector-resource"></a>Créer une ressource *Détecteur d'anomalies*

Commençons par créer une ressource **Détecteur d’anomalies** dans votre abonnement Azure :

1. Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Cliquez sur le bouton **&#65291;Créer une ressource**, recherchez *Détecteur d'anomalies*, puis créez une ressource **Détecteur d'anomalies** avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez un groupe de ressources ou créez-en un nouveau*.
    - **Région** : *choisissez une région disponible*.
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : F0 gratuit

1. Examinez et créez la ressource. Attendez la fin du déploiement, puis accédez à la ressource déployée.

1. Affichez la page **Clés et point de terminaison** de votre ressource Détecteur d'anomalies. Vous aurez besoin du point de terminaison et des clés pour vous connecter à partir d’applications clientes.

## <a name="run-cloud-shell"></a>Exécuter Cloud Shell

Pour tester les fonctionnalités du service Détecteur d'anomalies, nous allons utiliser une application de ligne de commande simple s’exécutant dans Cloud Shell sur Azure.

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail.

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/anomaly-detector/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/anomaly-detector/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes indiqué en haut à gauche du volet Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/anomaly-detector/powershell-portal-guide-3.png)

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/anomaly-detector/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>Configurer et exécuter une application cliente

Maintenant que vous disposez d’un environnement Cloud Shell, vous pouvez exécuter une application simple qui utilise le service Détecteur d’anomalies pour analyser des données.

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

    ![L’éditeur de code.](media/anomaly-detector/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **detect-anomalies.ps1**. Ce fichier contient du code qui utilise le service Détection d'anomalie, comme illustré ici :

    ![Éditeur contenant du code pour détecter les anomalies](media/anomaly-detector/detect-anomalies-code.png)

1. Ne vous souciez pas trop des détails du code. Ce qui importe, c’est qu’il a besoin de l’URL du point de terminaison, ainsi que de l’une ou l’autre des clés de votre ressource Détecteur d'anomalies. Copiez celles-ci à partir de la page **Clés et points de terminaison** de votre ressource (qui doit toujours se trouver dans la partie supérieure du navigateur), et collez-les dans l’éditeur de code, en remplaçant les valeurs d’espace réservé **YOUR_KEY** et **YOUR_ENDPOINT**, respectivement.

    > **Conseil** Vous devrez peut-être vous servir de la barre de séparation pour ajuster la zone d’écran quand vous utilisez les volets **Clés et point de terminaison** et **Éditeur**.

    Une fois les valeurs de clé et de point de terminaison collées, les deux premières lignes de code devraient ressembler à ceci :

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**.

    Encore une fois, la détection d’anomalie est une technique d’intelligence artificielle utilisée pour déterminer si les valeurs d’une série sont comprises dans les paramètres attendus. L’exemple d’application cliente utilise votre service Détecteur d'anomalies pour analyser un fichier contenant une série de valeurs de date/heure et numériques. L’application doit renvoyer des résultats indiquant, à chaque point de temps, si la valeur numérique se situe dans les paramètres attendus.

1. Dans le volet PowerShell, entrez les commandes suivantes pour exécuter le code :

    ```PowerShell
    cd ai-900
    .\detect-anomalies.ps1
    ```

1. Examinez les résultats, en notant que la dernière colonne dans les résultats est **True** ou **False** pour indiquer si la valeur enregistrée à chaque date/heure est considérée comme une anomalie ou non. Pensez à la façon dont nous pourrions utiliser ces informations dans une situation réelle. Quelle action l’application pourrait-elle déclencher si les valeurs sont celles de la température du réfrigérateur ou de la pression sanguine et que des anomalies sont détectées ?  

## <a name="learn-more"></a>En savoir plus

Cette application simple ne montre que quelques fonctionnalités du service Détecteur d'anomalies. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page Détecteur d'anomalies](https://azure.microsoft.com/services/cognitive-services/anomaly-detector/).

## <a name="clean-up"></a>Nettoyage

Il est judicieux, à la fin d’un projet, de déterminer si vous avez encore besoin des ressources que vous avez créées. Les ressources laissées en cours d’exécution peuvent vous coûter de l’argent. 

Si vous passez à d’autres modules d’Azure AI - Notions fondamentales, vous pouvez conserver vos ressources pour les utiliser dans d’autres labos.

Si vous avez fini votre apprentissage, vous pouvez supprimer le groupe de ressources ou les ressources individuelles de votre abonnement Azure :

1. Dans le [portail Azure](https://portal.azure.com/), dans la page **Groupes de ressources**, ouvrez le groupe de ressources que vous avez spécifié lors de la création de votre ressource.

2. Cliquez sur **Supprimer le groupe de ressources**, tapez le nom du groupe de ressources pour confirmer que vous souhaitez le supprimer, puis sélectionnez **Supprimer**. Vous pouvez également choisir de supprimer des ressources individuelles en sélectionnant la ou les ressources, en cliquant sur les trois points pour voir plus d’options, puis en cliquant sur **Supprimer**.