---
title: Notifier Target
description: Assurez-vous que tous les événements qui doivent être suivis par [!DNL Target] sont envoyés à l’aide de la méthode trackEvent.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: efccadab-d139-4423-8613-c2743d87b3a0
source-git-commit: 3301d88bc47208ab5439c1a9f7933e99c22a4521
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Notifier [!DNL Target]

En suivant cette étape, vous vous assurez que tous les événements qui doivent être envoyés à [!DNL Adobe Target] sont envoyés à l’aide de la méthode `trackEvent`.

Tout événement devant faire l’objet d’un suivi dans [!DNL Target] peut être un événement de conversion principal ou une mesure de succès.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour les développer en plein écran.

## Notifier [!DNL Target] diagramme {#diagram}

Le numéro d’étape de l’illustration suivante correspond à la section ci-dessous.

![Diagramme Notifier Target](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1 : Déclencher l’API de suivi des [!DNL Adobe Target]

Cette étape vous permet de vous assurer que tous les événements qui doivent être envoyés à [!DNL Target] sont envoyés à l’aide de la méthode `trackEvent`.

+++Afficher les détails

![Diagramme de l’API de suivi d’Adobe Target](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

Vous envoyez les attributs de conversion de commande comme indiqué dans la section *Conditions préalables* ci-dessous. Le nom de la mbox n’a pas d’importance, mais la conversion consiste à utiliser `orderConfirmPage`.

Il n’est pas nécessaire d’inclure les attributs de conversion de commande dans cet appel. Ces appels enregistrent idéalement des mesures de succès qui peuvent être considérées comme des événements de mini-conversion avant les événements de conversion principaux. `CardIds` doit être inclus dans les recommandations basées sur le panier en fonction de l’événement `Add to Cart`.

+++

**Conditions préalables**

* Rencontrez votre équipe commerciale pour identifier tous les événements qui peuvent être considérés comme des mesures de conversion ou de succès. Vous devez également identifier l’événement de conversion qui génère un chiffre d’affaires afin que ces détails puissent être envoyés à [!DNL Target] avec les données d’événement.
* Assurez-vous que les attributs suivants sont disponibles dans la couche de données afin de pouvoir les envoyer avec l’événement de conversion. L’événement de conversion génère un chiffre d’affaires, tel qu’un achat de produit ou un événement Ajouter au panier.

   * `productPurchaseId` : ID de produit achetés dans le cadre de la commande. Séparez plusieurs produits en utilisant des virgules.
   * `orderTotal` : total de la commande pour l&#39;achat.
   * `orderId` : ID de commande de l’achat.

  L’illustration suivante présente une [règle for [!DNL tags] in [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html){target=_blank} qui ne doit être déclenchée que sur la page [!UICONTROL Confirmation].

  ![Page de configuration de l’action](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* Si vous effectuez le suivi d’un événement pour l’ajout au panier, envoyez `cartIds` en tant que paramètre. Une liste d’ID de produit séparés par des virgules peut être transmise pour `cardIds`.

**Lectures**

* [méthode adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds pour les critères basés sur le panier](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Actions**

* Utilisez `adobe.target-trackEvent()` méthode pour envoyer toutes les données qui doivent être envoyées à [!DNL Target].
