---
title: Notifier Target
description: Assurez-vous que tous les événements qui doivent être suivis par [!DNL Target] sont envoyés à l’aide de la méthode trackEvent .
feature: APIs/SDKs
level: Experienced
role: Developer
source-git-commit: 723bb2f33a011995757009193ee9c48757ae1213
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# Notifier [!DNL Target]

Cette étape permet de s’assurer que tous les événements qui doivent être envoyés à [!DNL Adobe Target] sont envoyés à l’aide de la fonction `trackEvent` .

Tout événement qui doit être suivi dans [!DNL Target] peut être un événement de conversion principal ou une mesure de succès.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour passer en mode plein écran.

## Notifier [!DNL Target] diagramme {#diagram}

Le numéro de l’étape dans l’illustration suivante correspond à la section ci-dessous.

![Diagramme Notifier Target](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1 : Déclenchement [!DNL Adobe Target] Suivi de l’API

Cette étape vous permet de vous assurer que tous les événements qui doivent être envoyés à [!DNL Target] sont envoyés à l’aide de la fonction `trackEvent` .

+++Voir les détails

![Déclenchement du diagramme de l’API de suivi Adobe Target](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

Vous envoyez les attributs de conversion de commande comme indiqué dans la variable *Conditions préalables* ci-dessous. Le nom de la mbox n’a pas d’importance, mais la conversion doit utiliser `orderConfirmPage`.

Vous n’avez pas besoin d’inclure les attributs de conversion de commande dans cet appel. Ces appels enregistrent idéalement des mesures de succès qui peuvent être considérées comme des événements de mini-conversion avant les principaux événements de conversion. `CardIds` doit être inclus dans les recommandations basées sur le panier en fonction de la variable `Add to Cart` .

**Conditions préalables**

* Rencontrez votre équipe d’entreprise afin d’identifier tous les événements pouvant être considérés comme des mesures de conversion ou de succès. Vous devez également identifier l’événement de conversion qui génère des recettes afin que ces détails puissent être envoyés à [!DNL Target] ainsi que les données d’événement.
* Assurez-vous que les attributs suivants sont disponibles dans la couche de données afin que vous puissiez les envoyer avec l’événement de conversion. L’événement de conversion génère des recettes, telles qu’un achat de produit ou l’événement Ajouter au panier.

   * `productPurchaseId`: ID de produit achetés dans le cadre de la commande. Séparez plusieurs produits à l’aide de virgules.
   * `orderTotal`: total de la commande pour l’achat.
   * `orderId`: identifiant de la commande de l’achat.

  L’illustration suivante présente une [règle pour [!DNL tags] in [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html){target=_blank} qui ne doit être déclenché que sur la variable [!UICONTROL Confirmation] page.

  ![Page Configuration de l’action](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* Si vous effectuez le suivi d’un événement pour l’ajout de panier, envoyez `cartIds` comme paramètre. Une liste d’ID de produit séparés par des virgules peut être transmise pour `cardIds`.

**Lectures**

* [méthode adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds pour les critères basés sur le panier](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Actions**

* Utilisation `adobe.target-trackEvent()` pour envoyer toutes les données qui doivent être envoyées à [!DNL Target].







