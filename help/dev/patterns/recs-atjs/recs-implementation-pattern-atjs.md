---
title: Modèle de mise en oeuvre Recommendations à l’aide d’at.js
description: Comprendre comment utiliser le modèle de mise en oeuvre pour Recommendations avec at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Modèle d’implémentation [!DNL Recommendations] à l’aide de la présentation d’at.js

Ce modèle d’implémentation vous aide à comprendre et à créer votre implémentation [!DNL Adobe Target Recommendations] lors de l’utilisation de la [bibliothèque JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Cliquez sur l’image pour passer en mode plein écran.

![Diagramme d’architecture Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Notez que les nombres dans l’image n’indiquent pas la séquence des opérations :

1. SDK côté client pour [!DNL Adobe Target] et [!DNL Experience Cloud ID Service]
1. appel [!DNL Target Delivery API]
1. Appel d’acquisition [!UICONTROL Experience Cloud ID] (ECID)
1. API de mise à jour des profils en masse et service [!DNL Customer Attributes] (CA)
1. Ingestion des données de profil des sources de données du client vers la banque de profils [!DNL Target]
1. Collecte des données de profil et de comportement et choix de l’expérience à présenter au visiteur
1. Rendu des expériences sur la page
1. at.js effectue le rendu des expériences sur la page

Chaque modèle se compose de différentes parties, chacune correspondant à une exigence d’implémentation critique pour votre implémentation [!DNL Target].

Chaque partie est expliquée dans un article distinct de ce guide :

* [Initialisation des SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configuration de la collecte de données](/help/dev/patterns/recs-atjs/data-collection.md)
* [Rendu d’expériences](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notifier Target](/help/dev/patterns/recs-atjs/notify-target.md)
