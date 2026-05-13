---
title: Configurer la collecte de données
description: Assurez-vous que toutes les tâches nécessaires à la collecte de données sont exécutées dans le bon ordre.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
TQID: https://experienceleague.adobe.com/fg3xJnwYAVyz-N-xzT5Piu35Ajd2UMEvuTvTQs2wj3c
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 401
ht-degree: 1%

---

# Configurer la collecte de données

Suivez les étapes du diagramme *Collecte de données* pour vous assurer que toutes les tâches nécessaires à la collecte de données sont exécutées dans le bon ordre.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour les développer en plein écran.

La couche de données est prête lors du chargement de la page ou son changement après le chargement de la page.

Si vous avez déjà mappé des données pendant la phase [initialize SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md), vous devez exécuter les étapes de ce diagramme si :

* Votre couche de données est augmentée de quelque manière que ce soit sur la même page et vous souhaitez envoyer ces données supplémentaires à [!DNL Target]
* Vous souhaitez envoyer des données de catalogue de produits à [!DNL Target Recommendations]

## Collecter le diagramme de données {#diagram}

Les numéros d’étape de l’illustration suivante correspondent aux sections ci-dessous.

![Diagramme de collecte de données](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Cliquez sur les liens suivants pour accéder aux sections de votre choix :

* [2.1 : Configuration du mapping des données](#configure)
* [2.2 Lier aux attributs de l’entité](#entity-attributes)
* [2.3 Déclencher l’API de suivi Adobe Target](#fire-api)

## 2.1 : Configuration du mapping des données {#configure}

Cette étape permet de s’assurer que toutes les données qui doivent être envoyées à [!DNL Adobe Target] sont définies.

+++Afficher les détails

![Configurer le diagramme de mappage des données](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* La couche de données doit être prête avec toutes les données qui doivent être envoyées à [!DNL Target].

**Lectures**

[fonction targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Actions**

Utilisez la fonction `targetPageParams()` pour définir toutes les données requises qui doivent être envoyées à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 2.2 : Lien vers les attributs d’entité {#entity-attributes}

Lier aux attributs d’entité pour mettre à jour le catalogue de produits pour [!DNL Target Recommendations].

+++Afficher les détails

**Lectures**

* [Attributs d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Considérations**

* Pour transmettre les attributs d’entité, une autre méthode consiste à mettre à jour le catalogue de produits dans l’interface utilisateur de [!DNL Target] pour utiliser les [flux de produits Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* La transmission des attributs d’entité s’applique uniquement aux pages où les données du catalogue de produits sont disponibles dans la couche de données.
* La transmission du paramètre `entity.event.detailsOnly=true` dans un appel est prioritaire.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 2.3 Déclencher l’API de suivi Adobe Target {#fire-api}

Cette étape permet de s’assurer que toutes les données qui doivent être envoyées à [!DNL Target] sont envoyées.

+++Afficher les détails

![Diagramme de l’API de suivi d’Adobe Target](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Tous les mappages de données doivent avoir été effectués à l’aide de la fonction [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lectures**

* [méthode adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Actions**

Utilisez la méthode [adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) pour envoyer toutes les données qui doivent être envoyées à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

Passez à l’étape 3 : [ Rendu des expériences ](/help/dev/patterns/recs-atjs/render-experiences.md)
