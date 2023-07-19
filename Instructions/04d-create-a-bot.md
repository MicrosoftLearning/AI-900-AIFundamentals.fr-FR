---
lab:
  title: Explorer les réponses aux questions
---

# Explorer les réponses aux questions

> **Remarque** Pour suivre ce labo, vous avez besoin d’un [abonnement Azure](https://azure.microsoft.com/free?azure-portal=true) dans lequel vous disposez d’un accès administratif.

Pour des scénarios de service clientèle, il est courant de créer un bot capable d’interpréter les questions fréquemment posées et d’y répondre via une fenêtre de conversation de site web, une adresse e-mail ou une interface vocale. L’interface de bot sous-jacente est une base de connaissances de questions et réponses appropriées dans laquelle le bot peut rechercher des réponses appropriées.

## Créer une base de connaissances de réponses aux questions personnalisées

La fonctionnalité de réponses aux questions personnalisées de Language Service vous permet de créer rapidement une base de connaissances, soit en entrant des paires question/réponse, soit à partir d’un document ou d’une page web existants. Il peut ensuite utiliser des fonctionnalités de traitement en langage naturel intégrées pour interpréter les questions et rechercher des réponses appropriées.

1. Ouvrez le portail Azure sur [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.

1. Cliquez sur le bouton **&#65291;Créer une ressource**, recherchez *Service Language*, créez une ressource du **service Language** avec les paramètres suivants, puis cliquez sur **Continuer pour créer votre ressource** : **Sélectionner des fonctionnalités supplémentaires**
    - **Fonctionnalités par défaut** : *conservez les fonctionnalités par défaut*.
    - **Fonctionnalités personnalisées** : *sélectionnez les réponses aux questions personnalisées*.

    ![Création d’une ressource du service Language avec activation des réponses aux questions personnalisées.](media/create-a-bot/create-language-service-resource.png)

1. Dans la page **Créer une ressource Language**, spécifiez les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez un groupe de ressources ou créez-en un nouveau*.
    - **Nom** : *nom unique de votre ressource Language*.
    - **Niveau tarifaire** : S (1 000 appels par minute)
    - **Région de recherche Azure** : *n’importe quelle localisation disponible*.
    - **Niveau tarifaire Recherche Azure** : Gratuit F (3 index) - (*Si ce niveau n’est pas disponible, sélectionnez Standard S (50 index)* )
    - **En cochant cette case, je certifie que j’ai vérifié et reconnu les termes dans l’avis sur l’IA responsable** : *sélectionné*.

    > **Remarque** Si vous avez déjà provisionné une ressource **Recherche cognitive Azure** de niveau gratuit, votre quota ne vous permettra peut-être pas d’en créer une autre. Dans ce cas, sélectionnez un autre niveau que **Gratuit F**.

1. Cliquez sur **Vérifier et créer**, puis sur **Créer**. Attendez la fin du déploiement de Language Service qui prendra en charge votre base de connaissances de réponses aux questions personnalisées.

1. Sous un nouvel onglet de navigateur, ouvrez le portail Language Studio sur [https://language.azure.com](https://language.azure.com?azure-portal=true) et connectez-vous avec le compte Microsoft associé à votre abonnement Azure.

1. Si vous êtes invité à choisir une ressource de langue, sélectionnez les paramètres suivants :
    - **Annuaire Azure** : annuaire Azure contenant votre abonnement.
    - **Abonnement Azure** : Votre abonnement Azure.
    - **Ressource de langue** : Ressource de langue que vous avez créée précédemment.

1. Si vous n’êtes ***pas*** invité à choisir une ressource de langue, c’est peut-être parce que vous avez plusieurs ressources de langue dans votre abonnement, auquel cas :
    1. Dans la barre en haut de la page, cliquez sur le bouton **Paramètres (&#9881;)**.
    2. Dans la page **Paramètres**, affichez l’onglet **Ressources**.
    3. Sélectionnez la ressource de langue que vous venez de créer, puis cliquez sur **Changer de ressource**.
    4. En haut de la page, cliquez sur **Language Studio** pour revenir à la page d’accueil de Language Studio.

1. En haut du portail Language Studio, dans le menu **Créer**, sélectionnez **Réponses aux questions personnalisées**.

1. Dans la page **Choisissez le paramètre de langue pour la ressource *votre ressource***, sélectionnez **Je souhaite sélectionner la langue quand je crée un projet dans cette ressource**, puis cliquez sur **Suivant**.

1. Dans la page **Entrer les informations de base**, entrez les détails suivants et cliquez sur **Suivant** :
    - **Ressource de langue** : *Choisissez votre ressource de langue*.  
    - **Ressource de recherche Azure** : *Choisissez votre ressource de recherche Azure*.
    - **Nom** : MargiesTravel
    - **Description** : Base de connaissances simple
    - **Langue source** : Anglais
    - **Réponse par défaut quand aucune réponse n’est retournée** : Aucune réponse trouvée

1. Dans la page **Vérifier et terminer**, cliquez sur **Créer un projet**.

1. Vous êtes alors dirigé vers la page **Gérer les sources**. Cliquez sur **&#65291;Ajouter une source** et sélectionnez **URL**.

1. Dans la zone **Ajouter des URL**, cliquez sur **+ Ajouter une URL**. Tapez ce qui suit, puis sélectionnez **Tout ajouter** :
    - **Nom de l’URL** : MargiesKB
    - **URL** : `https://raw.githubusercontent.com/MicrosoftLearning/AI-900-AIFundamentals/main/data/qna/margies_faq.docx`
    - **Classifier la structure des fichiers** : *détection automatique* 

## Modifier la base de connaissances

Votre base de connaissances est basée sur les détails du document FAQ et sur certaines réponses prédéfinies. Vous pouvez ajouter des paires question-réponse personnalisées pour compléter ces informations.

1. Cliquez sur **Modifier la base de connaissances** dans le volet de gauche. Ensuite, cliquez sur **+ Ajouter une paire de questions**.

1. Dans la zone **Questions**, tapez `Hello`, puis cliquez sur **Envoyer les modifications**.

1. Cliquez sur **+ Ajouter une autre expression**, tapez `Hi`, puis cliquez sur **Envoyer les modifications**.

1. Dans la zone **Réponses et invites**, tapez `Hello`. Gardez la **Source** : Éditorial.

1. Cliquez sur **Envoyer**. Puis, en haut de la page, cliquez sur **Enregistrer les modifications**. Il se peut que vous deviez modifier la taille de votre fenêtre pour voir le bouton.

## Entraîner et tester la base de connaissances

Maintenant que vous avez une base de connaissances, vous pouvez la tester.

1. En haut de la page, cliquez sur **Tester** pour tester votre base de connaissances.

1. Dans la partie inférieure du volet de test, entrez le message *Bonjour*. La réponse retournée devrait être **Hello**.

1. Dans la partie inférieure du volet de test, entrez le message *Je veux réserver un vol*. Une réponse appropriée du FAQ devrait être retournée.

    > **Remarque** La réponse comprend une *réponse brève* ainsi qu’un *passage de réponse* plus détaillé. Le passage de réponse affiche le texte complet figurant dans le document de FAQ pour la question correspondante la plus proche, tandis que la réponse brève est extraite intelligemment du passage. Vous pouvez contrôler si la version courte vient de la réponse à l’aide de la case à cocher **Afficher la réponse courte** en haut du volet de test.

1. Essayez une autre question, par exemple *Comment annuler une réservation ?*

1. Lorsque vous avez fini de tester la base de connaissances, cliquez sur **Tester** pour fermer le volet de test.

## Créer un bot pour la base de connaissances

La base de connaissances fournit un service principal que les applications clientes peuvent utiliser pour répondre aux questions via une sorte d’interface utilisateur. Généralement, ces applications clientes sont des bots. Pour mettre la base de connaissances à la disposition d’un bot, vous devez la publier en tant que service accessible via HTTP. Vous pouvez ensuite utiliser l’Azure Bot Service pour créer et héberger un bot utilisant la base de connaissances pour répondre aux questions des utilisateurs.

1. À gauche de la page Langue Studio, cliquez sur **Déployer la base de connaissances**.

1. En haut de la page, cliquez sur **Déployer**. Une boîte de dialogue va vous demander si vous voulez déployer le projet. Sélectionnez **Déployer**.

1. Une fois le service déployé, cliquez sur **Créer un bot**. Cela a pour effet d’ouvrir le portail Azure dans un nouvel onglet de navigateur pour vous permettre de créer un bot d’application web dans votre abonnement Azure.

1. Dans le portail Azure, créez un bot d’application web. (Vous pouvez voir un message d’avertissement demandant de vérifier si la source du modèle est fiable. Vous n’avez pas besoin d’effectuer une action pour ce message.) Continuez en mettant à jour les paramètres suivants :

    - **Détails du projet**
        - **Abonnement** : *votre abonnement Azure*
        - **Groupe de ressources** : *groupe de ressources contenant votre ressource linguistique*
    - **Détails de l’instance**
        - **Emplacement du groupe de ressources** : *le même emplacement que votre service de langage*.
    - **Azure Bot**
        - **Descripteur du bot** : *nom unique de votre bot* (*prérempli*)
    - **Choisir votre niveau tarifaire**
        - **Niveau tarifaire** : Gratuit (F0) (Il peut être nécessaire de sélectionner *Changer de plan*)
    - **ID d’application Microsoft**
        - **Type de création** : *sélectionnez Créer une identité managée affectée par l’utilisateur* 

5. Sélectionnez **Suivant : Application web >** pour continuer la mise à jour des paramètres. 
    - **App Service**
        - **Nom de l’application** : *identique au **Descripteur du bot** avec **.azurewebsites.net** ajouté automatiquement*
        - **Langage du Kit de développement logiciel (SDK)**  : *choisissez C# ou Node.js*
    - **Plan App Service**
        - **Type de création** : *sélectionnez Créer un plan App Service*.
    - **Paramètres de l’application**
        - **Clé de ressource de langue** : *vous devez copier votre clé de ressource de langue et la coller ici.* 
        
        > **Remarque** Pour accéder à votre clé de ressource de langue, ouvrez [https://portal.azure.com](https://portal.azure.com?azure-portal=true). Dans la page d’accueil, cliquez sur *Groupes de ressources* et recherchez le groupe de ressources dans lequel vous avez créé votre ressource de langue. Sélectionnez votre ressource de langue et accédez à son menu de gauche. Sélectionnez ensuite *Clés et point de terminaison*. Copiez une des clés. 

    -  
        - **Nom du projet de langue** : MargiesTravel
        - **Nom d’hôte du point de terminaison du service de langue** : *prérempli avec votre point de terminaison de service de langue*
    - **Détails du service de langue**
        - **ID d’abonnement** : *prérempli avec votre ID d’abonnement*
        - **Nom du groupe de ressources** : *prérempli avec le nom de votre groupe de ressources*
        - **Nom du compte** : *prérempli avec le nom de votre ressource*

1. Sélectionnez **Vérifier + créer**.

1. Patientez pendant la création de votre bot (l’icône de notification en haut à droite, représentant une cloche, est animée pendant que vous attendez). Ensuite, dans la notification indiquant que le déploiement est terminé, cliquez sur **Accéder à la ressource** (ou bien, dans la page d’accueil, cliquez sur **Groupes de ressources**, ouvrez le groupe de ressources dans lequel vous avez créé le bot d’application web, puis cliquez dessus).

1. Dans le volet gauche de votre bot, recherchez **Paramètres**, cliquez sur **Tester dans Web Chat**, puis attendez que le bot affiche le message **Bonjour et bienvenue** (l’initialisation peut prendre quelques secondes).

1. Utilisez l’interface de test de conversation pour vous assurer que votre bot répond aux questions à partir de votre base de connaissances comme prévu. Par exemple, essayez de soumettre *Je veux annuler mon hôtel*.

Essayez le bot. Vous constaterez probablement qu’il peut répondre à des questions du FAQ de manière très précise, mais qu’il est limité quant à sa capacité à interpréter les questions auxquelles son apprentissage ne l’a pas préparé. Vous pouvez toujours utiliser Language Studio pour modifier la base de connaissances afin de l’améliorer, puis la republier.

## En savoir plus

- Pour en savoir plus sur le service Réponses aux questions, consultez [cette documentation](https://docs.microsoft.com/azure/cognitive-services/language-service/question-answering/overview).
- Pour en savoir plus sur le Microsoft Bot Service, consultez la [page Azure Bot Service](https://azure.microsoft.com/services/bot-service/).
