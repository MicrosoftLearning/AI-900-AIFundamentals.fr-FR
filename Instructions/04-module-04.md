---
lab:
  title: Explorer l’analyse de texte
---

# Explorer l’analyse de texte

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

Le traitement en langage naturel (NLP) est une branche de l’intelligence artificielle (IA) qui traite du langage écrit et parlé. Vous pouvez l’utiliser pour créer des solutions qui extraient la signification sémantique du texte ou du discours, ou qui formulent des réponses pertinentes en langage naturel.

La solution Microsoft *Azure AI services* inclut les fonctionnalités d’analyse de texte du service *Language* , offrant des capacités de NLP prêtes à l’emploi, dont l’identification d’expressions clés dans un texte et la classification de texte en fonction du sentiment.

Supposons, par exemple, que l’organisation fictive *Margie’s Travel* encourage ses clients à formuler des avis sur des hôtels. Vous pourriez utiliser le service Language pour résumer les avis en extrayant des expressions clés, discriminer les avis positifs et négatifs ou analyser le texte des avis pour y détecter des mentions d’entités connues telles que des emplacements ou des personnes.

Pour tester les fonctionnalités du service Language, nous allons utiliser une simple application de ligne de commande s’exécutant dans le service Cloud Shell. Les mêmes principes et fonctionnalités s’appliquent aux solutions réelles, telles que des sites web ou applications téléphoniques.

## Créer une ressource *Azure AI services*

Vous pouvez utiliser le service Language en créant une ressource **Language** ou **Azure AI services**.

Si ce n’est déjà fait, créez une ressource **Azure AI services** dans votre abonnement Azure.

1. Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Cliquez sur le bouton **&#65291;Créer une ressource** et recherchez *Azure AI Services*. Sélectionnez **créer** un plan **Azure AI services**. Vous accédez à une page pour créer une ressource Azure AI services. Configurez-la avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez ou créez un groupe de ressources portant un nom unique*.
    - **Région** : *choisissez une région disponible*.
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : Standard S0
    - **En cochant cette case, j’ai reconnu que j’ai lu et compris tous les termes ci-dessous** : sélectionné.

1. Examinez et créez la ressource.

### Obtenir la clé et le point de terminaison de votre ressource Azure AI services

1. Attendez la fin du déploiement. Accédez ensuite à votre ressource Azure AI services puis, dans la page **Vue d’ensemble**, sélectionnez le lien pour gérer les clés du service. Vous aurez besoin du point de terminaison et des clés pour vous connecter à votre ressource Azure AI services à partir d’applications clientes.

1. Affichez la page **Clés et point de terminaison** de votre ressource. Vous aurez besoin de la **clé** et du **point de terminaison** pour vous connecter à partir d’applications clientes.

## Exécuter Cloud Shell

Pour tester les fonctionnalités d’analyse de texte du service Language, nous allons utiliser une simple application de ligne de commande s’exécutant dans le service Cloud Shell sur Azure.

1. Dans le portail Azure, sélectionnez le bouton **[>_]** (*Cloud Shell*) en haut de la page, à droite de la zone de recherche. Cela a pour effet d’ouvrir un volet de Cloud Shell au bas du portail.

    ![Démarrez le service Cloud Shell en cliquant sur l’icône située à droite de la zone de recherche en haut.](media/analyze-text-language-service/powershell-portal-guide-1.png)

1. Lorsque vous ouvrez le service Cloud Shell première fois, il se peut que vous soyez invité à choisir le type d’interpréteur de commandes que vous souhaitez utiliser (*Bash* ou *PowerShell*). Sélectionnez **PowerShell**. Si vous ne voyez pas cette option, ignorez l’étape.  

1. Si vous êtes invité à créer un stockage pour votre service Cloud Shell, assurez-vous que votre abonnement est spécifié, puis sélectionnez **Créer un stockage**. Patientez ensuite environ une minute jusqu’à ce que le stockage soit créé.

    ![Créez le stockage en cliquant sur Confirmer.](media/analyze-text-language-service/powershell-portal-guide-2.png)

1. Assurez-vous que le type d’interpréteur de commandes indiqué en haut à gauche du volet Cloud Shell est *PowerShell*. S’il s’agit de *Bash*, basculez vers *PowerShell* à l’aide du menu déroulant.

    ![Comment trouver le menu déroulant à gauche pour basculer vers PowerShell](media/analyze-text-language-service/powershell-portal-guide-3.png)

1. Attendez que PowerShell démarre. Vous devriez voir l’écran suivant s’afficher dans le portail Azure :  

    ![Attendez que PowerShell démarre.](media/analyze-text-language-service/powershell-prompt.png)

## Configurer et exécuter une application cliente

À présent que vous disposez d’un modèle personnalisé, vous pouvez exécuter une simple application cliente utilisant le service Language.

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

    ![L’éditeur de code.](media/analyze-text-language-service/powershell-portal-guide-4.png)

1. Dans le volet **Fichiers** à gauche, développez **ai-900**, puis sélectionnez **analyze-text.ps1**. Ce fichier contient du code utilisant le service Language :

    ![Éditeur contenant du code pour utiliser le service Language](media/analyze-text-language-service/analyze-text-code.png)

1. Ne vous souciez pas trop des détails du code. Dans le Portail Azure, accédez à votre ressource Azure AI services. Sélectionnez ensuite la page **Clés et points de terminaison** dans le volet de gauche. Copiez la clé et le point de terminaison à partir de la page et collez-les dans l’éditeur de code, en remplaçant respectivement les valeurs d’espace réservé **YOUR_KEY** et **YOUR_ENDPOINT**.

    > **Conseil** Vous devrez peut-être vous servir de la barre de séparation pour ajuster la zone d’écran quand vous utilisez les volets **Clés et point de terminaison** et **Éditeur**.

    ![Recherchez l’onglet Clé et point de terminaison dans le volet gauche de votre ressource Azure AI services.](media/analyze-text-language-service/key-endpoint-support.png)

    Une fois les valeurs de clé et de point de terminaison remplacées, les premières lignes de code devraient ressembler à ceci :

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."
    $endpoint="https..."
    ```

1. En haut à droite du volet de l’éditeur, utilisez le bouton **...** pour ouvrir le menu, puis sélectionnez **Enregistrer** pour enregistrer vos modifications. Rouvrez ensuite le menu, puis sélectionnez **Fermer l’éditeur**.

    L’exemple d’application cliente utilisera le service Language de Azure AI services pour détecter la langue, extraire les expressions clés, déterminer le sentiment et extraire des entités connues pour les avis.

1. Dans le Cloud Shell, entrez la commande suivante pour exécuter le code :

    ```PowerShell
    cd ai-900
    ./analyze-text.ps1 review1.txt
    ```

    Vous allez réviser ce texte :

    >Good Hotel and staff The Royal Hotel, London, UK 3/2/2018 Clean rooms, good service, great location near Buckingham Palace and Westminster Abbey, and so on. We thoroughly enjoyed our stay. The courtyard is very peaceful and we went to a restaurant which is part of the same group and is Indian ( West coast so plenty of fish) with a Michelin Star. We had the taster menu which was fabulous. The rooms were very well appointed with a kitchen, lounge, bedroom and enormous bathroom. Thoroughly recommended.

1. Passez en revue la sortie.

1. Dans le volet PowerShell, entrez la commande suivante pour exécuter le code :

    ```PowerShell
    ./analyze-text.ps1 review2.txt
    ```

    Vous allez réviser ce texte :

    >Hôtel vieillissant avec un service médiocre. The Royal Hotel, Londres, Royaume-Uni 06/05/2018. Il s’agit d’un vieil hôtel (existe depuis les années 50) dont le mobilier des chambres n’est plus au goût du jour : il est démodé et doit être changé. The internet didn't work and had to come to one of their office rooms to check in for my flight home. The website says it's close to the British Museum, but it's too far to walk.

1. Passez en revue la sortie.

1. Dans le volet PowerShell, entrez la commande suivante pour exécuter le code :

    ```PowerShell
    ./analyze-text.ps1 review3.txt
    ```

    Vous allez réviser ce texte :

    >Good location and helpful staff, but on a busy road.
    The Lombard Hotel, San Francisco, USA 8/16/2018 We stayed here in August after reading reviews. We were very pleased with location, just behind Chestnut Street, a cosmopolitan and trendy area with plenty of restaurants to choose from. The Marina district was lovely to wander through, very interesting houses. Make sure to walk to the San Francisco Museum of Fine Arts and the Marina to get a good view of Golden Gate bridge and the city. On a bus route and easy to get into centre. Rooms were clean with plenty of room and staff were friendly and helpful. The only down side was the noise from Lombard Street so ask to have a room furthest away from traffic noise.

1. Passez en revue la sortie.

1. Dans le volet PowerShell, entrez la commande suivante pour exécuter le code :

    ```PowerShell
    ./analyze-text.ps1 review4.txt
    ```

    Vous allez réviser ce texte :

    >Very noisy and rooms are tiny The Lombard Hotel, San Francisco, USA 9/5/2018 Hotel is located on Lombard street which is a very busy SIX lane street directly off the Golden Gate Bridge. Traffic from early morning until late at night especially on weekends. Noise would not be so bad if rooms were better insulated but they are not. Had to put cotton balls in my ears to be able to sleep--was too tired to enjoy the city the next day. Rooms are TINY. I picked the room because it had two queen size beds--but the room barely had space to fit them. With family of four in the room it was tight. With all that said, rooms are clean and they've made an effort to update them. The hotel is in Marina district with lots of good places to eat, within walking distance to Presidio. May be good hotel for young stay-up-late adults on a budget

1. Passez en revue la sortie.

## En savoir plus

Cette application simple ne montre que quelques fonctionnalités du service Language. Pour en savoir plus sur ce que ce service est capable de faire, consultez la [page sur le service Language](https://azure.microsoft.com/services/cognitive-services/language-service/).
