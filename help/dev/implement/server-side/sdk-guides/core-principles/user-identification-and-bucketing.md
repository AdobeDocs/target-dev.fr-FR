---
title: Identification des utilisateurs et regroupement
description: Identification des utilisateurs et regroupement
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
TQID: https://experienceleague.adobe.com/V9hK5oj7F-SV2wou2sz-Ve3RVJ1EMsFJDmcNF4ctV5o
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1172
ht-degree: 4%

---

# Identification des utilisateurs et regroupement

## Identification de l&#39;utilisateur

Il existe plusieurs façons d’identifier un utilisateur dans [!DNL Adobe Target]. [!UICONTROL Target] utilise les identifiants suivants :

| Nom du champ | Description |
| --- | --- |
| `tntID` | L’`tntId` est l’identifiant principal dans [!DNL Target] pour un utilisateur. Vous pouvez fournir cet identifiant, ou [!DNL Target] le générera automatiquement si la requête n’en contient pas. |
| `thirdPartyId` | Le `thirdPartyId` est l’identifiant de l’utilisateur de votre société, que vous pouvez envoyer à chaque appel. Lorsqu’un utilisateur se connecte au site d’une entreprise, l’entreprise crée généralement un identifiant lié au compte du visiteur, à la carte de fidélité, au numéro d’abonnement ou à d’autres identifiants applicables de cette entreprise. |
| `marketingCloudVisitorId` | Le `marketingCloudVisitorId` est utilisé pour fusionner et partager des données entre différentes solutions Adobe. L’identifiant visiteur marketingCloud est requis pour les intégrations à Adobe Analytics et Adobe Audience Manager. |
| `customerIds` | Outre l’identifiant visiteur Experience Cloud, d’autres [ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) et un statut d’authentification pour chaque visiteur peuvent également être utilisés. |

## [!DNL Target] ID (tntID)

L’ID de [!DNL Target], ou `tntId`, peut être considéré comme un ID d’appareil. Cette `tntId` est générée automatiquement par [!DNL Adobe Target] si elle n’est pas fournie dans la requête. Les requêtes suivantes doivent inclure cette `tntId` pour que le contenu approprié soit diffusé sur un appareil utilisé par le même utilisateur.

L’exemple d’appel suivant illustre une situation dans laquelle un `tntId` n’est pas transmis à [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

En l&#39;absence de `tntId`, [!DNL Adobe Target] génère un `tntId` et le fournit dans la réponse, comme suit.

```json {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "acmeclient",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.35_0"
  },
  "edgeHost": "mboxedge35.tt.omtrdc.net",
  ...
}
```

Dans cet exemple, le `tntId` généré est `10abf6304b2714215b1fd39a870f01afc.35_0`. Notez que ce `tntId` doit être utilisé pour le même utilisateur entre les sessions.

## ID tiers (thirdPartyId)

Si votre organisation utilise un identifiant pour identifier votre visiteur, vous pouvez utiliser `thirdPartyID` pour diffuser du contenu. Un `thirdPartyID` est un identifiant persistant que votre entreprise utilise pour identifier un utilisateur final, qu’il interagisse avec votre entreprise à partir de canaux web, mobiles ou IoT. En d’autres termes, le `thirdPartyId` fait référence aux données de profil utilisateur qui peuvent être utilisées sur plusieurs canaux. Cependant, vous devez fournir la `thirdPartyID` pour chaque appel API de diffusion [!DNL Adobe Target] que vous effectuez.

L’exemple d’appel suivant illustre l’utilisation d’un `thirdPartyId` .

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      thirdPartyId: "B234A029348"
    },
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .thirdPartyId("B234A029348");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Dans ce scénario, [!DNL Adobe Target] générera un `tntId` puisqu’il n’a pas été transmis à l’appel d’origine, qui sera mappé au `thirdPartyId` fourni.

## Identifiant visiteur Marketing Cloud (marketingCloudVisitorId)

Le `marketingCloudVisitorId` est un identifiant universel et persistant qui identifie vos visiteurs dans toutes les solutions de Adobe Experience Cloud. Lorsque votre organisation met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions Experience Cloud, notamment [!DNL Adobe Target], Adobe Analytics et Adobe Audience Manager. Notez que la `marketingCloudVisitorId` est requise lors de l’intégration de [!DNL Target] à [!DNL Adobe Analytics] et [!DNL Adobe Audience Manager].

L’exemple d’appel suivant montre comment un `marketingCloudVisitorId` récupéré à partir du service Experience Cloud ID est transmis à [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId: "10527837386392355901041112038610706884"
    },
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Dans ce scénario, [!DNL Target] générera un `tntId` puisqu’il n’a pas été transmis à l’appel d’origine, qui sera mappé au `marketingCloudVisitorId` fourni.

## ID de client (customerIds)

Les [ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) peuvent être ajoutés ou associés à un ID de visiteur Experience Cloud. Lors de l’envoi de `customerIds`, le `marketingCloudVisitorId` doit également être fourni. De plus, un statut d’authentification peut être fourni avec chaque `customerId` pour chaque visiteur. Les statuts d’authentification suivants peuvent être utilisés :

| État d’authentification | État d’utilisateur |
| --- | --- |
| `unknown` | Inconnu ou jamais authentifié. Cet état peut être utilisé dans des scénarios tels que celui où un visiteur arrive sur votre site en cliquant sur une publicité display. |
| `authenticated` | L’utilisateur est actuellement authentifié dans une session active sur votre site web ou votre application. |
| `logged_out` | L’utilisateur était authentifié, mais actuellement déconnecté. L’utilisateur avait l’intention de se déconnecter de l’état authentifié. Il ne souhaite plus être considéré comme authentifié. |

Notez que ce n’est que lorsque le `customerId` est authentifié que les données de profil utilisateur stockées et liées à l’ID client sont [!DNL Target] référencées. Si le `customerId` est dans un état inconnu ou `logged_out`, il sera ignoré et les données de profil utilisateur éventuellement associées à ce `customerId` ne seront pas utilisées pour le ciblage d’audience.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId : "10527837386392355901041112038610706884",
      customerIds: [{
        id: "134325423",
        integrationCode : "crm_data",
        authenticatedState : "authenticated"
      }]
    },
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

CustomerId customerId = new CustomerId()
  .id("134325423")
  .integrationCode("crm_data")
  .authenticatedState(AuthenticatedState.AUTHENTICATED);
VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884")
  .customerIds(Arrays.asList(customerId));
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

L’exemple ci-dessus montre comment envoyer un `customerId` avec un `authenticatedState`. Lors de l’envoi d’un `customerId`, les `integrationCode`, `id` et `authenticatedState` ainsi que les `marketingCloudVisitorId` sont requis. Le `integrationCode` est l’alias du fichier [attributs du client](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=fr) que vous avez fourni via CRS.

## Profil fusionné

Vous pouvez combiner `tntId`, `thirdPartyID` et `marketingCloudVisitorId` dans la même requête. Dans ce scénario, [!DNL Adobe Target] conservera le mappage de tous ces identifiants et les épinglera sur un visiteur. Découvrez comment les profils sont [fusionnés et synchronisés en temps réel](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) à l’aide des différents identifiants.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId: "B234A029348",
      marketingCloudVisitorId : "10527837386392355901041112038610706884"
    },
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

L’exemple ci-dessus montre comment combiner `tntId`, `thirdPartyID` et `marketingCloudVisitorId` dans la même requête.

## Groupement

Les utilisateurs sont regroupés pour afficher une expérience en fonction de la configuration des activités [!DNL Adobe Target]. Dans [!DNL Adobe Target], le regroupement est :

* **Déterministe** : MurmurHash3 est utilisé pour s’assurer que votre utilisateur est regroupé et voit la bonne variation à chaque fois, tant que l’identifiant utilisateur est cohérent.
* **Persistante** : [!DNL Adobe Target] stocke la variation que votre utilisateur voit dans le profil utilisateur pour vous assurer que la variation est présentée de manière cohérente à cet utilisateur sur l’ensemble des sessions et des canaux. Les variations et l’adhérence sont garanties lors de l’utilisation de la prise de décision côté serveur. Lorsque la prise de décision sur l’appareil est utilisée, la conformité n’est pas garantie.

## Workflow de regroupement de bout en bout

Avant de passer à l’algorithme de regroupement proprement dit, il est important de souligner que des étapes similaires sont utilisées à la fois pour sélectionner des activités en fonction de leur pourcentage d’affectation du trafic et pour sélectionner une expérience au sein d’une activité.

### Étapes de sélection des activités

1. Générer un identifiant d’appareil, généralement un UUID
1. Obtenir le code client
1. Obtention de l’identifiant d’activité
1. Prenez le sel, qui est généralement une chaîne comme « activité »
1. Calculer le hachage en utilisant MurmurHash3
1. Obtenir la valeur absolue du hachage
1. Diviser la valeur absolue de hachage par 10000
1. Divisez le reste par 10000, ce qui devrait produire une valeur comprise entre 0 et 1
1. Multiplier le résultat par 100 %
1. Comparez le pourcentage d’affectation du trafic d’activité au pourcentage obtenu. Si le pourcentage d’affectation du trafic est inférieur, l’activité est sélectionnée. Sinon, l’activité est ignorée.

### Étapes de sélection de l’expérience

1. Générer un identifiant d’appareil, généralement un UUID
1. Obtenir le code client
1. Obtention de l’identifiant d’activité
1. Prenez le sel, qui est généralement une chaîne comme « expérience »
1. Calculer le hachage en utilisant MurmurHash3
1. Obtenir la valeur absolue du hachage
1. Diviser la valeur absolue de hachage par 10000
1. Divisez le reste par 10000, ce qui devrait produire une valeur comprise entre 0 et 1
1. Multipliez le résultat par le nombre total d’expériences dans l’activité
1. Arrondissez le résultat. Cela devrait produire l’index d’expérience.

### Exemple

Supposons ce qui suit :

* Client C avec code client `acmeclient`
* Activité A avec ID `1111` et trois expériences `E1`, `E2` et `E3`
* Les expériences ont la distribution suivante : `E1` - 33 %, `E2` - 33 %, `E3` - 34 %

Le flux de sélection se présente comme suit :

1. `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15` de l’ID de l’appareil
1. `acmeclient` du code client
1. ID d’activité `1111`
1. `experience` De Sel
1. Valeur à hacher `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, valeur de hachage `-919077116`
1. Valeur absolue du `919077116` de hachage
1. Reste après division par 10000, `7116`
1. La valeur après le reste est divisée par 10000, `0.7116`
1. Résultat après multiplication de la valeur par rapport au nombre total d’expériences `3 * 0.7116 = 2.1348`
1. L’index d’expérience est `2`, ce qui signifie la troisième expérience, car nous utilisons l’indexation basée sur les `0`.
