---
title: Instructions hébergées en ligne
permalink: index.html
layout: home
---

# Exercices de la formation Azure AI - Notions fondamentales

Ce référentiel contient les exercices pratiques de laboratoire du cours Microsoft [AI-900 *Microsoft Azure iAI*](https://docs.microsoft.com/fr-fr/learn/certifications/courses/ai-900t00) et les modules autodidactes équivalents sur Microsoft Learn : [Premiers pas avec l’intelligence artificielle sur Azure](https://docs.microsoft.com/learn/paths/get-started-with-artificial-intelligence-on-azure/), [Créer des modèles de prédiction avec Azure Machine Learning](https://docs.microsoft.com/fr-fr/learn/paths/create-no-code-predictive-models-azure-machine-learning/),  [Découvrir la vision par ordinateur dans Microsoft Azure](https://docs.microsoft.com/learn/paths/explore-computer-vision-microsoft-azure/), [Découvrir le traitement du langage naturel](https://docs.microsoft.com/learn/paths/explore-natural-language-processing/) et [Découvrir l’IA conversationnelle](https://docs.microsoft.com/learn/paths/explore-conversational-ai/). Les exercices sont conçus pour accompagner les supports de cours d’apprentissage et vous permettre de vous exercer à utiliser les technologies qu’ils décrivent. 

Pour effectuer ces exercices, vous devez disposer d’un abonnement Microsoft Azure. Si votre instructeur ne vous en a pas fourni un, vous pouvez vous inscrire pour un essai gratuit à l’adresse [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Exercices |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
