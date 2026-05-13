---
title: Modèle d’implémentation de Recommendations utilisant at.js
description: Comprendre comment utiliser le modèle d’implémentation pour Recommendations avec at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
TQID: https://experienceleague.adobe.com/uYNa5mL-8ffPS-ddjnQzILnPFMbjNJqKZDmQT8qFeGA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 152
ht-degree: 0%

---

# Modèle d’implémentation [!DNL Recommendations] à l’aide d’at.js - Aperçu

Ce modèle d’implémentation permet de comprendre et de créer votre implémentation [!DNL Adobe Target Recommendations] lors de l’utilisation de la bibliothèque JavaScript [at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md).

Cliquez sur l’image pour l’afficher en plein écran.

![Diagramme d’architecture ](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Notez que les nombres dans l’image n’indiquent pas la séquence des opérations :

1. SDK côté client pour [!DNL Adobe Target] et [!DNL Experience Cloud ID Service]
1. appel [!DNL Target Delivery API]
1. Appel d’acquisition [!UICONTROL Experience Cloud ID] (ECID)
1. API de mise à jour de profil en masse et service [!DNL Customer Attributes] (CA)
1. Ingestion des données de profil à partir des sources de données du client vers [!DNL Target] banque de données de profils
1. Collecte de données de profil et de comportement et choix de l’expérience à présenter au visiteur
1. Les expériences s’affichent sur la page
1. at.js effectue le rendu des expériences sur la page

Chaque modèle se compose de différentes parties, chacune d’elles correspondant à un besoin critique d’implémentation pour votre implémentation [!DNL Target].

Chaque partie est expliquée dans un article distinct dans ce guide :

* [Initialiser les SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configurer la collecte de données](/help/dev/patterns/recs-atjs/data-collection.md)
* [Rendu des expériences](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notifier Target](/help/dev/patterns/recs-atjs/notify-target.md)
