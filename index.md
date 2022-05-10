---
title: Instructions hébergées en ligne
permalink: index.html
layout: home
ms.openlocfilehash: b85af520a10e63a2f9a5696db03bfd946aff968f
ms.sourcegitcommit: 1ef64e3008a439d0d0bb3d93a27d3df68d3d64a9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/17/2022
ms.locfileid: "140688690"
---
# <a name="azure-ai-fundamentals-exercises"></a>Exercices sur les notions fondamentales de l’IA d'Azure

Utilisez les liens ci-dessous pour faire les exercices pratiques de labo du cours Microsoft [AI-900 *Concepts de base de Microsoft Azure AI*](https://docs.microsoft.com/learn/certifications/courses/ai-900t00).

Pour effectuer ces exercices, vous devez disposer d’un abonnement Microsoft Azure. Si votre instructeur ne vous en a pas fourni un, vous pouvez vous inscrire pour un essai gratuit sur [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Exercices |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
