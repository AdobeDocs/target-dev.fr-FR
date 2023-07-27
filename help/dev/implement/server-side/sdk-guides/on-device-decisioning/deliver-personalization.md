---
title: Personnalisation à l’aide des SDK Adobe Target
description: Découvrez comment diffuser de la personnalisation à l’aide de [!UICONTROL prise de décision sur appareil].
feature: APIs/SDKs
exl-id: bac64c78-0d3a-40d7-ae2b-afa0f1b8dc4f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Personnalisation de la diffusion

## Résumé des étapes

1. Activer [!UICONTROL prise de décision sur appareil] pour votre organisation
1. Créez un [!UICONTROL Ciblage d’expérience] Activité (XT)
1. Définition d’une expérience personnalisée par audience
1. Vérifier l’expérience personnalisée par audience
1. Configuration de la création de rapports
1. Ajout de mesures pour le suivi des indicateurs clés de performance
1. Mettre en oeuvre des offres personnalisées dans votre application
1. Mise en oeuvre du code pour suivre les événements de conversion
1. Activez votre [!UICONTROL Ciblage d’expérience] (XT) activité de personnalisation

Supposons que vous soyez une compagnie touristique. Vous souhaitez proposer une offre personnalisée de 25 % sur certains forfaits de voyage. Pour que l’offre interagisse avec vos utilisateurs, vous décidez d’afficher un point de repère de la ville de destination. Vous souhaitez également vous assurer que la diffusion de vos offres personnalisées est exécutée à une latence proche de zéro afin qu’elle n’ait pas d’incidence négative sur les expériences utilisateur et n’influence pas les résultats.

## 1. Activez [!UICONTROL prise de décision sur appareil] pour votre organisation

1. L’activation de la prise de décision sur l’appareil garantit qu’une activité A/B est exécutée à une latence proche de zéro. Pour activer cette fonction, accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]** in [!DNL Adobe Target], puis activez la variable **[!UICONTROL Prise de décision sur appareil]** bascule.

   ![image alternative](assets/asset-odd-toggle.png)

   >[!NOTE]
   >
   >Vous devez avoir l’administrateur ou l’approbateur [rôle utilisateur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) pour activer ou désactiver la fonction [!UICONTROL Prise de décision sur appareil] bascule.

   Après avoir activé la variable **[!UICONTROL Prise de décision sur appareil]** basculer, [!DNL Adobe Target] commence à générer *artefacts de règle* pour votre client.

## 2. Créez une [!UICONTROL Ciblage d’expérience] Activité (XT)

1. Dans [!DNL Adobe Target], accédez à la **[!UICONTROL Activités]** page, puis sélectionnez **[!UICONTROL Créer une activité]** > **[!UICONTROL Ciblage d’expérience]**.

   ![image alternative](assets/asset-xt.png)

1. Dans le **[!UICONTROL Création d’une activité de ciblage d’expérience]** modale, conservez la valeur par défaut **[!UICONTROL Web]** option sélectionnée (1), sélectionnez **[!UICONTROL Formulaire]** comme compositeur d’expérience (2), sélectionnez un espace de travail et une propriété (3), puis cliquez sur **[!UICONTROL Suivant]** (4).

   ![image alternative](assets/asset-xt-next.png)

## 3. Définir une expérience personnalisée par audience

1. Dans le **[!UICONTROL Expériences]** étape de création de l’activité, cliquez sur **[!UICONTROL Modification de l’audience]** pour créer une audience de ces visiteurs qui souhaitent se rendre à San Francisco, en Californie.

   ![image alternative](assets/asset-change-audience.png)

1. Dans le **[!UICONTROL Création d’une audience]** modale, définissez une règle personnalisée où `destinationCity = San Francisco`. Cela définit le groupe d’utilisateurs qui souhaitent se rendre à San Francisco.

   ![image alternative](assets/asset-audience-sf.png)

1. Toujours dans la variable **[!UICONTROL Expériences]** saisissez le nom de l’emplacement (1) dans votre application où vous souhaitez effectuer le rendu d’une offre spéciale concernant le pont Golden Gate, mais uniquement pour ceux qui se sont dirigés vers San Francisco. Dans l’exemple illustré ici, la page d’accueil est l’emplacement sélectionné pour l’offre de HTML (2), qui est défini dans la variable **[!UICONTROL Contenu]** zone.

   ![image alternative](assets/asset-content-sf.png)

1. Ajoutez une autre audience de ciblage en cliquant sur **[!UICONTROL Ajout du ciblage d’expérience]**. Cette fois, ciblez une audience qui souhaite se rendre à New York en définissant une règle d’audience où `destinationCity = New York`. Définissez l’emplacement dans votre application où vous souhaitez effectuer le rendu d’une offre spéciale concernant l’Empire State Building. Dans l’exemple illustré ici, `homepage` est l’emplacement sélectionné pour l’offre par HTML (2), qui est défini dans la variable **[!UICONTROL Contenu]** zone.

   ![image alternative](assets/asset-content-ny.png)

## 4. Vérifier l’expérience personnalisée par audience

Dans le **[!UICONTROL Ciblage]** vérifiez que vous avez configuré l’expérience personnalisée souhaitée par audience.

![image alternative](assets/asset-verify-sf-ny.png)

## 5. Configuration de la création de rapports

Dans le **[!UICONTROL Objectifs et paramètres]** étape, choisissez **[!UICONTROL Adobe Target]** comme la propriété **[!UICONTROL Source de création de rapports]** pour afficher les résultats de l’activité dans la variable [!DNL Adobe Target] Interface utilisateur ou choisissez **[!UICONTROL Adobe Analytics]** pour les afficher dans l’interface utilisateur Adobe Analytics.

![image alternative](assets/asset-reporting-sf-ny.png)

## 6. Ajout de mesures pour le suivi des indicateurs clés de performance

Choisissez une **[!UICONTROL Mesure de l’objectif]** pour mesurer le succès de l’activité. Dans cet exemple, une conversion réussie dépend du clic de l’utilisateur sur l’offre de destination personnalisée.

## 7. Mettre en oeuvre vos offres personnalisées dans votre application

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {      
    execute: {
      pageLoad: {
        parameters: {
          destinationCity: "San Francisco"
        }
      }
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java ]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## 8. Mise en oeuvre du code pour suivre les événements de conversion

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "destinationOffer"
          }
        }
      ]
    }
})
```

>[!TAB Java ]

```java {line-numbers="true"
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);
NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);
```

>[!ENDTABS]

## 9. Activez votre activité de ciblage d’expérience (XT).

![image alternative](assets/asset-xt-activate.png)
