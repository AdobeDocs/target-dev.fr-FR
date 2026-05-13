---
title: Journalisation d’Adobe Analytics for Target (A4T) dans Experience Platform Web SDK
description: Découvrez comment contrôler la collecte des données Adobe Analytics for Target (A4T) à l’aide de la SDK Web d’Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;journalisation;analytics;sdk;sdk web;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
TQID: https://experienceleague.adobe.com/cShqvj3wSialxA-ajnROnIpzjuz66pNg3CLM6l2xPLg
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 262
ht-degree: 0%

---

# Connexion [!DNL Adobe Analytics for Target] (A4T) à l’[!DNL Experience Platform Web SDK]

Lors de l’utilisation de [!DNL Adobe Target] pour la personnalisation, vous pouvez choisir le système à utiliser pour la mesure des performances. Chaque [activité Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) vous permet de choisir entre les rapports de [!DNL Target] et les rapports de [!DNL Analytics] Adobe.

Si vous utilisez la création de rapports [!DNL Analytics], [!DNL Target] devez communiquer les informations suivantes à [!DNL Analytics] :

* Quelle activité [!DNL Target] vos visiteurs ont-ils saisie ?
* Quelle expérience ont-ils vécue ?
* Quelle conversion a été atteinte

Le [!DNL Adobe Experience Platform Web SDK] prend en charge deux types de journaux de [!DNL Analytics] pour les cas d’utilisation [!UICONTROL Analytics for Target] (A4T) :

| Méthode de consignation | Description |
| --- | --- |
| Journalisation des [!DNL Analytics] côté serveur | Tous les accès [!DNL Analytics] envoyés via Edge Network sont complétés par des détails [!DNL Target] côté serveur, sans avoir à passer par le processus d’assemblage des accès. |
| Journalisation des [!DNL Analytics] côté client | [!DNL Target] données sont renvoyées côté client, ce qui vous permet d’augmenter et d’envoyer manuellement des données à [!DNL Analytics] à l’aide de l’[API Data Insertion](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

La méthode de journalisation est déterminée par le fait que vous ayez [!DNL Adobe Analytics] activée ou non sur le [flux de données](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) que vous avez configuré :

![Flux de décision de la méthode de journalisation](/help/dev/implement/a4t/assets/analytics-logging.png)

## Étapes suivantes

Ce document présente brièvement les différentes méthodes de journalisation des données A4T dans le SDK Web. Pour plus d’informations sur chacune de ces méthodes, consultez la documentation suivante :

* [Journalisation côté serveur des données A4T dans Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Journalisation côté client pour les données A4T dans Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
