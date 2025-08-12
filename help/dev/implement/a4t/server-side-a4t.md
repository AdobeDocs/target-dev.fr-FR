---
title: Journalisation côté serveur des données A4T dans Experience Platform Web SDK
description: Découvrez comment activer la journalisation côté serveur pour Adobe Analytics for Target (A4T) à l’aide d’Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;journalisation;
feature: Implementation
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Journalisation côté serveur pour les données A4T dans [!DNL Experience Platform Web SDK]

Le [!DNL Adobe Experience Platform Web SDK] vous permet d’implémenter [!UICONTROL Adobe Analytics for Target] fonctionnalité (A4T) sur [!UICONTROL Experience Platform Edge Network]. Lorsque la journalisation côté serveur est activée, tous les accès [!DNL Analytics] envoyés par le biais d’Edge Network sont complétés par des détails [!DNL Target] côté serveur, sans avoir à passer par le processus d’assemblage des accès.

La journalisation côté serveur pour [!DNL Analytics] est activée lorsque [!DNL Analytics] est activé dans la configuration du flux de données :

![Configuration de train de données Analytics activée](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

Le diagramme suivant montre le flux de données dans le système lorsque la journalisation des [!DNL Analytics] côté serveur est activée :

![Flux de journalisation côté serveur](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Étapes suivantes

Ce guide couvrait la journalisation côté serveur pour les données A4T dans le Web SDK. Pour plus d’informations sur la gestion des données A4T côté client[ consultez le guide sur la ](/help/dev/implement/a4t/client-side-logging.md) journalisation côté client .