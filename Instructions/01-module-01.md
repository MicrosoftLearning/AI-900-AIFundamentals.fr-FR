---
lab:
  title: Explorer Azure AI services
---

> **Important**
> **Le labo Détecteur d'anomalies a été déprécié et remplacé par la mise à jour ci-dessous.**

Azure AI services aide les utilisateurs à créer des applications avec des API et modèles prêts à l’emploi, prédéfinis et personnalisables. Dans cet exercice, vous allez examiner l’un des services, Azure AI Sécurité du Contenu, dans le Studio de Sécurité du Contenu. 

Le Studio de Sécurité du Contenu vous permet d’explorer la façon dont le contenu texte et image peut être modéré. Vous pouvez exécuter des tests sur des exemples de texte ou d’images et obtenir un score de gravité allant de sécurisé à élevé pour chaque catégorie. Dans cet exercice de labo, vous allez créer une ressource à service unique dans le Studio de Sécurité du Contenu et tester ses fonctionnalités. 

> **Remarque** L’objectif de cet exercice est d’avoir une idée générale de la façon dont les services Azure AI services sont provisionnés et utilisés. Sécurité du Contenu est utilisé à titre d’exemple, vous n’êtes pas censé devenir un expert en sécurité de contenu après cet exercice.

## Naviguer dans le Studio de Sécurité du Contenu 

![Capture d’écran de la page d’accueil du Studio de Sécurité du Contenu.](./media/content-safety/content-safety-getting-started.png)


1. Ouvrez [Studio de Sécurité du Contenu](https://contentsafety.cognitive.azure.com?azure-portal=true). Si vous n’êtes pas connecté, vous devez le faire. Sélectionnez **Se connecter** en haut à droite de l’écran. Utilisez l’adresse e-mail et le mot de passe associés à votre abonnement Azure pour vous connecter. 

1. Le Studio de Sécurité du Contenu est configuré comme de nombreux autres studios des services Azure AI services. Dans le menu en haut de l’écran, cliquez sur l’icône à gauche d’*Azure AI*. Vous verrez une liste déroulante d’autres studios conçus pour le développement avec les services Azure AI services. Vous pouvez cliquer à nouveau sur l’icône pour masquer la liste.

![Capture d’écran du menu de Studio de Sécurité du Contenu avec une sélection bascule ouverte au basculement vers d’autres studios.](./media/content-safety/studio-toggle-icon.png)  

## Associer une ressource au studio 

Avant d’utiliser le studio, vous devez associer une ressource Azure AI services au studio. Selon le studio, vous constaterez qu’il vous faut une ressource à service unique spécifique ou que vous pouvez utiliser une ressource à plusieurs services générale. Dans le cas du Studio de Sécurité du Contenu, vous pouvez utiliser le service en créant une ressource *Sécurité du Contenu* à service unique ou une ressource à plusieurs services générale *Azure AI services*. Dans les étapes ci-dessous, nous allons créer une ressource Sécurité du Contenu à service unique. 

1. En haut à droite de l’écran, cliquez sur l’icône **Paramètres**. 

![Capture d’écran de l’icône des paramètres en haut à droite de l’écran, en regard de l’icône de la cloche, du point d’interrogation et du sourire.](./media/content-safety/settings-toggle.png)

1. Dans la page **Paramètres**, vous verrez un onglet *Répertoire* et un onglet *Ressource*. Sous l’onglet *Ressource*, sélectionnez **Créer une ressource**. Cela vous amène à la page pour créer une ressource dans le portail Azure.

> **Remarque** L’onglet *Répertoire* permet aux utilisateurs de sélectionner différents répertoires à partir desquels créer des ressources. Vous n’avez pas besoin de modifier ses paramètres, sauf si vous souhaitez utiliser un autre répertoire. 

![Capture d’écran montrant où sélectionner « Créer une ressource » dans la page des paramètres du Studio de Sécurité du Contenu.](./media/content-safety/create-new-resource-from-studio.png)

1. Dans la page *Créer une sécurité du contenu* dans le [portail Azure](https://portal.azure.com?auzre-portal=true), vous devez configurer plusieurs détails pour créer votre ressource. Configurez-la avec les paramètres suivants :
    - **Abonnement** : *votre abonnement Azure*.
    - **Groupe de ressources** : *sélectionnez ou créez un groupe de ressources portant un nom unique*.
    - **Région** : *choisissez une région disponible*.
    - **Nom** : *entrez un nom unique.*
    - **Niveau tarifaire** : F0 gratuit

1. Sélectionnez **Vérifier + créer**, puis passez en revue la configuration. Sélectionnez ensuite **Créer**. L’écran indique quand le déploiement est terminé. 

*Félicitations ! Vous venez de créer ou d’approvisionner une ressource Azure AI services. Celle que vous avez approvisionnée dans ce cas précis est une ressource du service Sécurité du Contenu à service unique.*

1. Une fois le déploiement terminé, ouvrez un nouvel onglet et revenez au [Studio de Sécurité du Contenu](https://contentsafety.cognitive.azure.com?azure-portal=true). 

1. Sélectionnez à nouveau l’icône **Paramètres** en haut à droite de l’écran. Cette fois, vous devriez voir que votre ressource nouvellement créée a été ajoutée à la liste.  

1. Dans la page Paramètres de Studio de Sécurité du Contenu, sélectionnez la ressource du service Azure AI services que vous venez de créer, puis cliquez sur **Utiliser la ressource** en bas de l’écran. Vous serez redirigé vers la page d’accueil du studio. Vous pouvez maintenant commencer à utiliser le studio avec votre ressource nouvellement créée.

## Essayer la modération de texte dans Studio de Sécurité du Contenu

1. Dans la page d’accueil Studio de Sécurité du Contenu, sous *Exécuter des tests de modération*, accédez à la zone **Modérer le contenu de texte**, puis cliquez sur **Essayer**.
1. Sous Exécuter un test simple, cliquez sur **Contenu sécurisé**. Le texte est affiché dans la zone ci-dessous. 
1. Cliquez sur **Run test**. L’exécution d’un test appelle le modèle de Deep Learning du service Sécurité du Contenu. Le modèle de Deep Learning a déjà été formé pour reconnaître le contenu non sécurisé.
1. Dans le panneau *Résultats*, inspectez les résultats. Il y a quatre niveaux de gravité allant de sécurisé à élevé, et quatre types de contenu nuisible. Le service AI Sécurité du Contenu considère-t-il cet exemple comme acceptable ou non ? Il est important de souligner que les résultats se situent dans un intervalle de confiance. Un modèle bien entraîné, comme l’un des modèles prêts à l’emploi d’Azure AI, peut retourner des résultats qui ont une forte probabilité de correspondre à ce qu’un humain étiquetterait pour le résultat. Chaque fois que vous exécutez un test, vous appelez à nouveau le modèle. 
1. Essayez maintenant un autre échantillon. Sélectionnez le texte sous Contenu violent avec une faute d’orthographe. Vérifiez que le contenu s’affiche dans la zone ci-dessous.
1. Cliquez sur **Exécuter le test** et examinez à nouveau les résultats dans le panneau Résultats. 

Vous pouvez exécuter des tests sur tous les exemples fournis, puis examiner les résultats.

## Examinez les clés et le point de terminaison

Ces fonctionnalités que vous avez testées peuvent être programmées dans toutes sortes d’applications. Les clés et le point de terminaison utilisés pour le développement d’applications se trouvent tous dans le studio de sécurité du contenu et le portail Azure. 

1. Dans le studio de sécurité du contenu, revenez à la page **Paramètres**, avec l’onglet *Ressources* sélectionné. Recherchez la ressource que vous avez utilisée. Faites défiler l’écran pour voir le point de terminaison et la clé de votre ressource. 
1. Dans le portail Azure, vous verrez qu’il s’agit du *même* point de terminaison et de *différentes* clés que dans votre ressource. Pour vérifier cela, accédez au [portail Azure](https://portal.azure.com?auzre-portal=true). Recherchez *Sécurité du Contenu* dans la barre de recherche supérieure. Recherchez votre ressource et cliquez dessus. Dans le menu de gauche, en dessous de *Gestion des ressources*, cherchez *Clés et points de terminaison*. Sélectionnez **Clés et points de terminaison** pour afficher le point de terminaison et les clés de votre ressource. 

Une fois que vous avez terminé, vous pouvez supprimer la ressource Sécurité du Contenu du portail Azure. La suppression de la ressource est un moyen de réduire les coûts qui s’accumulent lorsque la ressource existe déjà dans l’abonnement. Pour cela, accédez à la page **Vue d’ensemble** de votre ressource Sécurité du Contenu. En haut de l’écran, sélectionnez **Supprimer**. 
