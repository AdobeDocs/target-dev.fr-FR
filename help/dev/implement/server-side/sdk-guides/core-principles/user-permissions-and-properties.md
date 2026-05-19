---
title: Autorisations et propriétés de l’utilisateur
description: Les SDK  [!DNL Target]  prennent en charge les autorisations et les propriétés des utilisateurs et utilisatrices.
exl-id: 612faf1a-e8f9-4321-b831-90fba69ead3a
feature: Implement Server-side
TQID: https://experienceleague.adobe.com/4l6qKRuEw14xYjcEsY49-3AAjYl6gouoKWIjkNuchdI
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 123
ht-degree: 8%

---

# Autorisations et propriétés de l’utilisateur

Les SDK [!DNL Target] prennent en charge les autorisations et les propriétés des utilisateurs. Si vous ne connaissez pas la façon dont [!DNL Adobe Target] gère les autorisations d’entreprise via les espaces de travail et les propriétés, vous pouvez en savoir plus à ce sujet dans [Autorisations des utilisateurs d’entreprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=fr).

Le client peut utiliser un jeton de propriété de l’une des deux façons suivantes.

## Jeton de propriété global

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    propertyToken: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({...})
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("emeaprod4")
    .organizationId("0DD934B85278256B0A490D44@AdobeOrg")
    .defaultPropertyToken("8c4630b1-16db-e2fc-3391-8b3d81436cfb")
    .build();

TargetClient targetClient = TargetClient.create(clientConfig);
```

>[!ENDTABS]

## Jeton de propriété accessoire dans l&#39;appel getOffers

Un jeton de propriété peut également être spécifié dans un appel `getOffers` individuel. Pour ce faire, ajoutez un objet de propriété à la requête. Un jeton de propriété spécifié de cette manière est prioritaire sur un jeton défini dans la configuration.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
    request: {
        execute: {
            pageLoad: {}
        },
        property: {
            token: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
        }           
    }
})
```

>[!TAB Java]

```java {line-numbers="true"}
ExecuteRequest executeRequest = new ExecuteRequest()
    .mboxes(getMboxRequests(mbox));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
    .context(getContext(request))
    .execute(executeRequest)
    .cookies(getTargetCookies(request.getCookies()))
    .property(new Property().token("8c4630b1-16db-e2fc-3391-8b3d81436cfb"))
    .build();

TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
```

>[!ENDTABS]
