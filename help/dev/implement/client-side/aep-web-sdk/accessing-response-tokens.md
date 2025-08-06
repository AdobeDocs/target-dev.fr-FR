---
title: Accès aux jetons de réponse à l’aide de Adobe Experience Platform Web SDK
description: Découvrez comment accéder aux jetons de réponse avec le  [!DNL Adobe Experience Platform Web SDK].
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;decisionScopes;result.decisions,jetons de réponse;
feature: AEP Web SDK
source-git-commit: f010ca54aac3c2a644a77fb2f88aff1996f6ddfe
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Accès aux jetons de réponse

Le contenu Personalization renvoyé par [!DNL Adobe Target] comprend des [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr), qui sont des détails sur l’activité, l’offre, l’expérience, le profil utilisateur, les informations géographiques, etc. Ces informations peuvent être partagées avec des outils tiers ou utilisées à des fins de débogage. Les jetons de réponse peuvent être configurés dans l’interface utilisateur d’[!DNL Target].

Pour accéder à n’importe quel contenu de personnalisation, fournissez une fonction de rappel lors de l’envoi d’un événement. Ce rappel est appelé une fois que le SDK a reçu une réponse réussie du serveur. Votre rappel est fourni avec un objet `result`, qui peut contenir une propriété `propositions` contenant tout contenu de personnalisation renvoyé. Vous trouverez ci-dessous un exemple de fonction de rappel.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

Dans cet exemple, `result.propositions`, s’il existe, est un tableau contenant des propositions de personnalisation liées à l’événement. Voir [Rendu du contenu de personnalisation](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) pour plus d’informations sur le contenu de `result.propositions.`

Supposons que vous souhaitiez rassembler tous les noms d’activité de toutes les propositions qui ont été automatiquement rendues par le SDK web et les pousser dans un seul tableau. Vous pouvez ensuite envoyer le tableau unique à un tiers. Dans ce cas :

1. Extrayez des propositions de l’objet `result`.
1. Parcourez chaque proposition en boucle.
1. Déterminez si le SDK a rendu la proposition.
1. Si tel est le cas, parcourez chaque élément de la proposition.
1. Récupérez le nom de l’activité à partir de la propriété `meta` , qui est un objet contenant des jetons de réponse.
1. Placez le nom de l’activité dans un tableau.
1. Envoyez les noms des activités à un tiers.

Votre code se présenterait comme suit :

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
