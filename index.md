---
title: Instructions hébergées en ligne
permalink: index.html
layout: home
---

# <a name="azure-ai-fundamentals-exercises"></a>Exercices sur les notions fondamentales de l’IA d'Azure

Ces exercices pratiques sont conçus pour accompagner le contenu des formations sur [Microsoft Learn](https://docs.microsoft.com/training/).

Pour effectuer ces exercices, vous devez disposer d’un abonnement Microsoft Azure. Vous pouvez vous inscrire à un essai gratuit sur [https://azure.microsoft.com](https://azure.microsoft.com).

## <a name="labs"></a>Laboratoires

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions'" %}
| Module | Laboratoire |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}