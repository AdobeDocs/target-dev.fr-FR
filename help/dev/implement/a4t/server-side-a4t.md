---
title: Journalisation côté serveur des données A4T dans Experience Platform Web SDK
description: Découvrez comment activer la journalisation côté serveur pour Adobe Analytics for Target (A4T) à l’aide d’Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;journalisation;
feature: Implementation
exl-id: 716f7343-69a6-44d7-baec-a0a0df1b6e1f
TQID: https://experienceleague.adobe.com/I7-G2VO2AN3qFsgkk4JX2Pg6WJfZq0HZkcGL4XQNoWg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 153
ht-degree: 0%

---

# Journalisation côté serveur pour les données A4T dans [!DNL Experience Platform Web SDK]

Le [!DNL Adobe Experience Platform Web SDK] vous permet d’implémenter [!UICONTROL Adobe Analytics for Target] fonctionnalité (A4T) sur [!UICONTROL Experience Platform Edge Network]. Lorsque la journalisation côté serveur est activée, tous les accès [!DNL Analytics] envoyés par le biais d’Edge Network sont complétés par des détails [!DNL Target] côté serveur, sans avoir à passer par le processus d’assemblage des accès.

La journalisation côté serveur pour [!DNL Analytics] est activée lorsque [!DNL Analytics] est activé dans la configuration du flux de données :

![Configuration de train de données Analytics activée](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

Le diagramme suivant montre le flux de données dans le système lorsque la journalisation des [!DNL Analytics] côté serveur est activée :

![Flux de journalisation côté serveur](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Étapes suivantes

Ce guide couvrait la journalisation côté serveur pour les données A4T dans le Web SDK. Pour plus d’informations sur la gestion des données A4T côté client[&#128279;](/help/dev/implement/a4t/client-side-logging.md) consultez le guide sur la  journalisation côté client .
