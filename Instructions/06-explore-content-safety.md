Le Studio de Sécurité du Contenu vous permet d’explorer la façon dont le contenu texte et image peut être modéré. Vous pouvez exécuter des tests sur des exemples de texte ou d’images et obtenir un score de gravité allant de sécurisé à élevé pour chaque catégorie. Vous pouvez découvrir rapidement le fonctionnement du service AI Sécurité du Contenu et ce dont il est capable. 

Dans cet exercice de labo, vous créerez une ressource Azure AI Services multiservices dans le Portail Azure et vous examinerez son point de terminaison et ses clés. Vous utiliserez ensuite le Studio de Sécurité du Contenu pour explorer les fonctionnalités du service AI Sécurité du Contenu. 

## Créer une ressource Azure AI Services

1.  Sous un autre onglet de navigateur, ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com?azure-portal=true) en vous connectant avec votre compte Microsoft.
1.  Cliquez sur le bouton **&#65291;Créer une ressource** et recherchez *Azure AI services*. Sélectionnez **créer** un plan **Azure AI services**. Vous accédez à une page pour créer une ressource Azure AI services. Configurez-la avec les paramètres suivants :
- **Abonnement**: Votre abonnement Azure.
- **Groupe de ressources** : sélectionner ou créer un groupe de ressources approprié.
- **Région** : Choisissez une région disponible.
- **Nom** : Entrez un nom unique.
- **Niveau tarifaire** : F0 
2.  Examinez et créez la ressource, puis attendez la fin du déploiement. 

## Associer la ressource au Studio de Sécurité du Contenu 
Dans un onglet de navigateur distinct, ouvrez le Studio de Sécurité du Contenu et connectez-vous. L’écran de Démarrage s’affiche.

1.  Cliquez sur la roue dentée Paramètres dans le menu supérieur droit.
2.  Sélectionnez la ressource Azure AI Service vous venez de créer, puis cliquez sur Utiliser la ressource.
3.  Affichez le point de terminaison et la clé de votre ressource, en faisant défiler si nécessaire. Si vous cochez le portail Azure, vous verrez qu’il s’agit du point de terminaison et de la clé de votre ressource, montrant que vous avez correctement associé votre ressource au Studio de Sécurité du Contenu.
4.  Cliquez sur le Studio de Sécurité du Contenu pour revenir à la page d’accueil. Sous Modération du contenu du texte, cliquez sur Essayer.
5.  Sous Exécuter un test simple, cliquez sur Contenu sécurisé. Le texte est affiché dans la zone ci-dessous. 
6.  Cliquez sur Run test. 
7.  Dans le panneau Résultats, inspectez les résultats. Il y a quatre niveaux de gravité allant de sécurisé à élevé, et quatre types de contenu nuisible. Le service AI Sécurité du Contenu considère-t-il cet exemple comme acceptable ou non ? 
8.  Essayez maintenant un autre échantillon. Sélectionnez le texte sous Contenu violent avec une faute d’orthographe. Vérifiez que le contenu s’affiche dans la zone ci-dessous.
9.  Cliquez sur Exécuter le test et examinez les résultats dans le panneau Résultats ci-dessous. Cet exemple est-il acceptable ? Si ce n’est pas le cas, pourquoi ?

Vous pouvez exécuter des tests sur tous les exemples fournis, puis examiner les résultats.

Une fois que vous avez terminé, supprimez la ressource Azure AI services dans le portail Azure. 
