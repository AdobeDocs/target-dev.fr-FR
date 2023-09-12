---
title: Modèle de mise en oeuvre Recommendations à l’aide d’at.js
description: Comprendre comment utiliser le modèle de mise en oeuvre pour Recommendations avec at.js
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 752c52c0db5173f49fd828c297fa7afd7c53c6ce
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# [!DNL Recommendations] modèle d’implémentation à l’aide de la présentation d’at.js

Ce modèle d’implémentation vous aide à comprendre et à créer votre [!DNL Adobe Target Recommendations] lors de l’utilisation de la variable [Bibliothèque JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Cliquez sur l’image pour passer en mode plein écran.

![Diagramme d’architecture Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Notez que les nombres dans l’image n’indiquent pas la séquence des opérations :

1. SDK côté client pour [!DNL Adobe Target] et [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] appel
1. [!UICONTROL Identifiant Experience Cloud] Appel d’acquisition (ECID)
1. API de mise à jour des profils en masse et [!DNL Customer Attributes] Service (CA)
1. Ingestion des données de profil des sources de données du client vers [!DNL Target] banque de profils
1. Collecte des données de profil et de comportement et choix de l’expérience à présenter au visiteur
1. Rendu des expériences sur la page
1. at.js effectue le rendu des expériences sur la page

Chaque modèle se compose de différentes parties, chacune d’elles correspondant à une exigence d’implémentation critique pour votre [!DNL Target] implémentation.

Chaque partie est expliquée dans un article distinct de ce guide :

* [Initialisation des SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configuration de la collecte de données](/help/dev/patterns/recs-atjs/data-collection.md)
* [Rendu d’expériences](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notifier Target](/help/dev/patterns/recs-atjs/notify-target.md)

