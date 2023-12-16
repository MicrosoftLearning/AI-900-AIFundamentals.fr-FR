---
lab:
  title: Explorez l’IA générative avec Bing Copilot
---

Dans cet exercice, vous allez explorer l’IA générative avec Bing Copilot. 

## Avant de commencer
Il vous faut un compte Microsoft personnel. Si vous n’en avez pas, accédez à [signup.live.com](https://signup.live.com/signup?azure-portal=true) pour vous inscrire.

# Explorez l’IA générative avec Bing

1. Ouvrez [Bing.com](https://www.bing.com?azure-portal=true) et connectez-vous avec votre compte Microsoft personnel.

**Remarque** : bien que vous puissiez vous connecter avec votre compte professionnel ou scolaire, vous verrez une expérience utilisateur légèrement différente de celle de la connexion avec votre compte personnel. À l’aide de votre compte professionnel ou scolaire, vous verrez une conversation Bing Entreprise. 

1. Cliquez sur **Conversation** dans le menu en haut de l’écran. La conversation vous amène à Bing Copilot, qui utilise l’IA générative pour alimenter les résultats de recherche. Cela signifie que contrairement à la recherche seule, qui retourne du contenu existant, Bing Copilot peut mettre en place de nouvelles réponses basées sur la modélisation du langage naturel et les informations du web.  
    
1. Vers le bas de l’écran, vous verrez une fenêtre **Demandez-moi ce que vous voulez**. Lorsque vous entrez des demandes dans la fenêtre, Bing Copilot utilise l’intégralité du thread de conversation pour renvoyer des réponses. Par exemple, essayons de poser une série de questions sur les voyages. 

## Utiliser des demandes pour générer des réponses

1. Entrez une demande : `What are 3 pros and cons of traveling in the winter?`. Vous verrez les éléments *Recherche de :...* et *Génération en cours...* s’afficher avant la réponse. Le modèle utilise les réponses recherchées comme informations de base pour générer des réponses originales. Notez que la fin de la réponse contient des liens vers ses sources. 

![Capture d’écran de la réponse de Bing Copilot à une demande concernant un voyage, avec trois avantages et trois inconvénients.](../media/generative-ai/bing-copilot-response-traveling.png) 

**Remarque** : si vous ne voyez pas le message **Génération en cours...* ou une liste à puces de réponses, vous n’avez pas encore vu Bing Copilot en action. Vous devez revenir au menu de connexion et connecter le compte actuel que vous utilisez avec un compte personnel. 
 
1. Entrez une demande : `Find me 3 more pros`. En faisant cette demande, vous aimeriez voir 3 raisons plus positives de voyager en hiver qui n’ont pas déjà été répertoriées. Notez qu’avec cette demande, vous demandez à Bing Copilot d’effectuer deux actions que la recherche seule ne fait pas : utiliser la réponse de conversation précédente pour exclure ce qui est retourné dans la nouvelle réponse, et utiliser la rubrique de la conversation précédente sans l’indiquer explicitement. 

1. Entrez une demande : `Where are 3 places I can go to find fewer crowds?`. 

**Remarque** : notez que même si Bing Copilot est en mesure de donner une réponse associée, il peut supprimer des « souvenirs » antérieurs du fil de conversation à mesure qu’il continue. Par conséquent, les réponses que vous obtenez peuvent ne pas être directement liées aux voyages en hiver. Cela relève en grande partie des limitations d’entrées de jeton. La conversation se « souvient » d’éléments antérieurs d’une conversation parce qu’elle a enregistré une certaine quantité de jetons de la conversation. À mesure que de nouveaux jetons sont introduits avec de nouvelles demandes et réponses, la conversation délaissera les jetons plus anciens. 

1. Le bouton **Nouveau sujet** en regard de la fenêtre de conversation permet à Bing Copilot d’effacer le thread de conversation précédent afin que les réponses du nouveau sujet ne se basent pas sur le sujet précédent. Utilisez l’icône **Nouveau sujet** en regard de la fenêtre de conversation pour effacer l’historique des conversations. 

## Essayer la génération d’images

1. Voyons maintenant un exemple de génération d’images. Entrez une demande : `Create an image of an elephant eating a hamburger`. Un message *Je vais essayer de créer ça...* s’affiche avant que Bing Copilot retourne une réponse. 

![Capture d’écran d’éléphants mangeant des hamburgers.](../media/generative-ai/dall-e-elephant.png)

Notez que la réponse peut être similaire, mais pas la même. Cela est dû au fait que les réponses sont variées.  

1. Dans la réponse, un texte en bas indique « Optimisé par DALL-E ». Considérez que DALL-E est basé sur de nombreux modèles de langage, car votre entrée en langage naturel génère des images. 

1. Revenez à la conversation de Bing Copilot en cliquant sur l’icône Microsoft Bing dans le coin supérieur droit de l’écran. 

## Essayer une génération de code

1. Voyons maintenant un exemple de génération et de traduction de code. Entrez une demande : `Use Python to create a list`. 

1. Entrez la demande : `Translate that into C#`. Notez que vous n’avez pas besoin de spécifier la nature de « ça » car Bing Copilot sait faire référence à l’historique des conversations. 

## Prime 

1. Entrez une demande : `What are 3 examples of generative AI helping people?`. Servez-vous-en pour réfléchir à vos propres idées de copilote !  

