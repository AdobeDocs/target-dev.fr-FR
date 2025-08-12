---
title: Journalisation côté client pour les données A4T dans Experience Platform Web SDK
description: Découvrez comment activer la journalisation côté client pour Adobe Analytics for Target (A4T) à l’aide d’Experience Platform Web SDK.
seo-title: Client-side logging for A4T data in the Experience Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;journalisation;sdk web;experience;platform;
feature: Implementation
source-git-commit: 4d4ca7dcffdbaee5770084bd85c3109df0d6a8d4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Journalisation côté client pour les données A4T dans le [!DNL Experience Platform Web SDK]

Le [!DNL Adobe Experience Platform Web SDK] vous permet de collecter des données [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr) côté client de votre application web.

La journalisation côté client signifie que les données de [!DNL Target] pertinentes sont renvoyées côté client, ce qui vous permet de collecter des données et de les partager avec [!DNL Analytics]. Cette option doit être activée si vous envisagez d’envoyer manuellement des données à Analytics à l’aide de l’[API Data Insertion](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=fr).

>[!NOTE]
>
>Une méthode pour effectuer cette opération à l’aide de [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=fr) est actuellement en cours de développement et sera disponible prochainement.

Ce document décrit les étapes de configuration de la journalisation A4T côté client pour le [!DNL Platform Web SDK] et fournit des exemples d’implémentation pour les cas d’utilisation courants.

## Conditions préalables {#prerequisites}

Ce tutoriel suppose que vous connaissez les concepts et processus fondamentaux liés à l’utilisation de l’[!DNL Platform Web SDK] à des fins de personnalisation. Consultez la documentation suivante si vous avez besoin d’une introduction :

* [Configuration du SDK Web](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/commands/configure/overview)
* [Envoi d’événements](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/commands/sendevent/overview)
* [Rendu du contenu de personnalisation](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Configurer [!DNL Analytics] journalisation côté client {#set-up-client-side-logging}

Les sous-sections suivantes décrivent comment activer [!DNL Analytics] journalisation côté client pour votre implémentation [!DNL Platform Web SDK].

### Activer la journalisation côté client [!DNL Analytics] {#enable-analytics-client-side-logging}

Pour que [!DNL Analytics] journalisation côté client soit activée pour votre implémentation, vous devez désactiver la configuration [!DNL Adobe Analytics] dans votre [flux de données](https://experienceleague.adobe.com/fr/docs/experience-platform/datastreams/overview).

![Configuration du flux de données Analytics désactivée](/help/dev/implement/a4t/assets/disable-analytics-datastream.png)

### Récupérez [!DNL A4T] données du SDK et envoyez-les à [!DNL Analytics] {#a4t-to-analytics}

Pour que cette méthode de création de rapports fonctionne correctement, vous devez envoyer les données liées au [!DNL A4T] récupérées à partir de la commande [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/commands/sendevent/overview) dans l’accès au [!DNL Analytics].

Lorsqu’[!DNL Target] Edge calcule une réponse de propositions, il vérifie si [!DNL Analytics] journalisation côté client est activée (par exemple, si [!DNL Analytics] est désactivé dans votre flux de données). Si la journalisation côté client est activée, le système ajoute un jeton [!DNL Analytics] à chaque proposition dans la réponse.

Le flux ressemble à ceci :

![Flux de journalisation côté client](/help/dev/implement/a4t/assets/analytics-client-side-logging.png)

Voici un exemple de réponse `interact` lorsque [!DNL Analytics] journalisation côté client est activée. Si la proposition concerne une activité qui fait l&#39;objet de rapports [!DNL Analytics], elle possède une propriété `scopeDetails.characteristics.analyticsToken`.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            }
          ]
        },
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Les propositions d’activités [!UICONTROL Form-based Experience Composer] peuvent contenir à la fois du contenu et des éléments de mesure de clic sous la même proposition. Ainsi, au lieu d’avoir un seul jeton d’analyse pour l’affichage du contenu dans `scopeDetails.characteristics.analyticsToken` propriété , ceux-ci peuvent avoir à la fois un jeton d’affichage et un jeton d’analyse de clic spécifiés dans les propriétés `scopeDetails.characteristics.analyticsDisplayToken` et `scopeDetails.characteristics.analyticsClickToken`, en conséquence.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            },
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Toutes les valeurs de `scopeDetails.characteristics.analyticsToken`, ainsi que `scopeDetails.characteristics.analyticsDisplayToken` (pour le contenu affiché) et `scopeDetails.characteristics.analyticsClickToken` (pour les mesures de clics) sont les payloads A4T qui doivent être collectées et incluses en tant que balise `tnta` dans l’appel [API Data Insertion](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

>[!IMPORTANT]
>
>Les propriétés `analyticsToken`, `analyticsDisplayToken` et `analyticsClickToken` peuvent contenir plusieurs jetons, concaténés sous la forme d’une seule chaîne délimitée par des virgules.
>
>Dans les exemples d’implémentation fournis dans la section suivante, plusieurs jetons [!DNL Analytics] sont collectés de manière itérative. Pour concaténer un tableau de jetons [!DNL Analytics], utilisez une fonction similaire à celle-ci :
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Exemples de mises en œuvre {#implementation-examples}

Les sous-sections suivantes montrent comment implémenter la journalisation côté client [!DNL Analytics] pour les cas d’utilisation courants.

### activités [!UICONTROL Form-Based Experience Composer] {#form-based-composer}

Vous pouvez utiliser l’[!DNL Platform Web SDK] pour contrôler l’exécution des propositions à partir des activités du [Compositeur d’expérience d’après les formulaires d’Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr).

Lorsque vous demandez des propositions pour une portée de décision spécifique, la proposition renvoyée contient son jeton d’[!DNL Analytics] approprié. Une bonne pratique consiste à enchaîner la commande [!DNL Experience Platform Web SDK] `sendEvent` et à effectuer une itération sur les propositions renvoyées pour les exécuter tout en collectant les jetons [!DNL Analytics] en même temps.

Vous pouvez déclencher une commande `sendEvent` pour une portée d’activité [!UICONTROL Form-Based Experience Composer] comme celle-ci :

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

À partir de là, vous devez implémenter le code pour exécuter les propositions et construire une payload qui sera finalement envoyée à [!DNL Analytics]. Voici un exemple de ce que `results.propositions` peut contenir :

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Pour extraire le jeton [!DNL Analytics] d’une proposition avec des éléments de contenu, vous pouvez implémenter une fonction similaire à ce qui suit :

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Une proposition peut comporter différents types d’éléments, comme indiqué par la propriété `schema` de l’élément en question. Quatre schémas d&#39;élément de proposition sont pris en charge pour les activités [!UICONTROL Form-Based Experience Composer] :

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` et `JSON_SCHEMA` sont les schémas qui reflètent le type de l’offre, tandis que `MEASUREMENT_SCHEMA` reflète les mesures qui doivent être jointes à un élément DOM.

[!DNL Analytics] payloads pour les mesures de clics doivent être collectées et envoyées aux [!DNL Analytics] séparément des éléments de contenu, au moment où le visiteur clique réellement sur le contenu précédemment affiché.

La fonction d’assistance suivante permettant d’obtenir les payloads A4T des mesures de clic s’avère pratique dans ce cas :

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Résumé de la mise en œuvre {#implementation-summary}

En résumé, les étapes suivantes doivent être exécutées lors de l’application d’activités [!UICONTROL Form-Based Experience Composer] avec le [!DNL Experience Platform Web SDK] :

1. envoyer un événement qui récupère [!UICONTROL Form-Based Experience Composer] offres d’activité ;
1. appliquer les modifications du contenu à la page ;
1. Envoyer l’événement de notification `decisioning.propositionDisplay` ;
1. Collectez les jetons d’affichage [!DNL Analytics] à partir de la réponse SDK et construisez une payload pour l’accès [!DNL Analytics] ;
1. Envoyez la payload à [!DNL Analytics] à l’aide de l’API [Data Insertion](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) ;
1. Si des mesures de clic sont présentes dans les propositions diffusées, les écouteurs de clic doivent être configurés de sorte que lorsqu’un clic est effectué, il envoie l’événement de notification `decisioning.propositionInteract`. Le gestionnaire de `onBeforeEventSend` doit être configuré de sorte que, lors de l’interception d’événements `decisioning.propositionInteract`, les actions suivantes se produisent :
   1. Collecte des jetons de [!DNL Analytics] de clics depuis `xdm._experience.decisioning.propositions`
   1. Envoi de l’accès au [!DNL Analytics] de clics avec la payload [!DNL Analytics] collectée via [API Data Insertion](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) ;

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Activités [!UICONTROL Visual Experience Composer] (VEC) {#visual-experience-composer-acitivties}

Le [!DNL Platform Web SDK] vous permet de gérer les offres qui ont été créées à l’aide du [compositeur d’expérience visuelle (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr).

>[!NOTE]
>
>Les étapes de mise en œuvre de ce cas pratique sont très similaires aux étapes des [activités du compositeur d’expérience d’après les formulaires](#form-based-composer). Consultez la section précédente pour plus de détails.

Lorsque le rendu automatique est activé, vous pouvez collecter les jetons [!DNL Analytics] à partir des propositions qui ont été exécutées sur la page. Une bonne pratique consiste à enchaîner la commande [!DNL Experience Platform Web SDK] `sendEvent` et à effectuer une itération sur les propositions renvoyées pour filtrer celles que le SDK Web a tenté de rendre.

**Exemple**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  
  for (var i = 0; i < results.propositions.length; i++) {
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Utilisation de `onBeforeEventSend` pour gérer les mesures de page {#using-onbeforeeventsend}

À l’aide des activités [!DNL Adobe Target], vous pouvez configurer différentes mesures sur la page, soit manuellement rattachées au modèle DOM, soit automatiquement rattachées au modèle DOM (activités créées par le compositeur d’expérience visuelle). Les deux types correspondent à une interaction différée de l’utilisateur final sur la page web.

Pour en tenir compte, il est recommandé de collecter les payloads [!DNL Analytics] à l’aide du hook de `onBeforeEventSend` [!DNL Adobe Experience Platform Web SDK]. Le hook `onBeforeEventSend` doit être configuré à l’aide de la commande `configure` et est reflété sur tous les événements envoyés par le biais du flux de données.

Voici un exemple de configuration d’`onBeforeEventSent` pour déclencher des accès [!DNL Analytics] :

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Étapes suivantes {#next-steps}

Ce guide couvre la journalisation côté client pour les données A4T dans le [!DNL Platform Web SDK] . Pour plus d’informations sur la gestion des données A4T sur Edge Network[ consultez le guide sur la ](/help/dev/implement/a4t/server-side-a4t.md) journalisation côté serveur .