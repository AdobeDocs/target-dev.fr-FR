---
title: Identification et regroupement des utilisateurs
description: Identification et regroupement des utilisateurs
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---

# Identification et regroupement des utilisateurs

## Identification de l’utilisateur

Il existe plusieurs façons d’identifier un utilisateur dans [!DNL Adobe Target]. [!UICONTROL Target] utilise les identifiants suivants :

| Nom du champ | Description |
| --- | --- |
| `tntID` | `tntId` est l’identifiant principal d’un utilisateur dans [!DNL Target]. Vous pouvez fournir cet identifiant ou [!DNL Target] le générera automatiquement si la requête ne contient pas. |
| `thirdPartyId` | `thirdPartyId` est l’identifiant de votre société pour l’utilisateur, que vous pouvez envoyer avec chaque appel . Lorsqu’un utilisateur se connecte au site d’une entreprise, celle-ci crée généralement un identifiant lié au compte du visiteur, à sa carte de fidélité, à son numéro de membre ou à tout autre identifiant applicable de l’entreprise. |
| `marketingCloudVisitorId` | `marketingCloudVisitorId` est utilisé pour fusionner et partager des données entre différentes solutions d’Adobe. MarketingCloudVisitorId est requis pour les intégrations avec Adobe Analytics et Adobe Audience Manager. |
| `customerIds` | Outre l’identifiant visiteur Experience Cloud, d’autres [ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) et un état authentifié pour chaque visiteur peuvent également être utilisés. |

## [!DNL Target] ID (tntID)

L’ [!DNL Target] ID, ou `tntId`, peut être considéré comme un ID d’appareil. Cet `tntId` est généré automatiquement par [!DNL Adobe Target] s’il n’est pas fourni dans la requête. Les demandes suivantes doivent inclure cet `tntId` pour que le contenu approprié soit diffusé sur un appareil utilisé par le même utilisateur.

L’exemple d’appel suivant illustre une situation dans laquelle un `tntId` n’est pas transmis à [!DNL Target].

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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

En l’absence d’un `tntId`, [!DNL Adobe Target] génère un `tntId` et le fournit dans la réponse, comme suit.

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

Dans cet exemple, le `tntId` généré est `10abf6304b2714215b1fd39a870f01afc.35_0`. Notez que cet `tntId` doit être utilisé pour le même utilisateur entre les sessions.

## ID tiers (thirdPartyId)

Si votre organisation utilise un identifiant pour identifier votre visiteur, vous pouvez utiliser `thirdPartyID` pour diffuser du contenu. Un `thirdPartyID` est un identifiant persistant utilisé par votre entreprise pour identifier un utilisateur final, qu’il interagisse avec votre entreprise à partir de canaux web, mobiles ou IoT. En d’autres termes, le `thirdPartyId` référence les données de profil utilisateur qui peuvent être utilisées sur plusieurs canaux. Cependant, vous devez fournir le `thirdPartyID` pour chaque appel de l’API de diffusion [!DNL Adobe Target] que vous effectuez.

L’exemple d’appel suivant illustre l’utilisation d’un `thirdPartyId`.

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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

Dans ce scénario, [!DNL Adobe Target] génère un `tntId` puisqu’il n’a pas été transmis dans l’appel d’origine, qui sera mappé sur le `thirdPartyId` fourni.

## Identifiant visiteur Marketing Cloud (marketingCloudVisitorId)

`marketingCloudVisitorId` est un identifiant universel et permanent qui identifie vos visiteurs dans toutes les solutions Adobe Experience Cloud. Lorsque votre organisation met en oeuvre le service d’ID, cet ID vous permet d’identifier un même visiteur du site et ses données dans différentes solutions Experience Cloud, y compris [!DNL Adobe Target], Adobe Analytics et Adobe Audience Manager. Veuillez noter que `marketingCloudVisitorId` est requis lors de l&#39;intégration de [!DNL Target] à [!DNL Adobe Analytics] et [!DNL Adobe Audience Manager].

L’exemple d’appel suivant montre comment un `marketingCloudVisitorId` récupéré du service d’ID Experience Cloud est transmis à [!DNL Target].

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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

Dans ce scénario, [!DNL Target] génère un `tntId` puisqu’il n’a pas été transmis dans l’appel d’origine, qui sera mappé sur le `marketingCloudVisitorId` fourni.

## ID de client (customerIds)

[Les ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) peuvent être ajoutés ou associés à un ID de visiteur Experience Cloud. Lors de l&#39;envoi de `customerIds`, le `marketingCloudVisitorId` doit également être fourni. De plus, un état d’authentification peut être fourni avec chaque `customerId` pour chaque visiteur. Les statuts d&#39;authentification suivants peuvent être utilisés :

| État d’authentification | État d’utilisateur |
| --- | --- |
| `unknown` | Inconnu ou jamais authentifié. Cet état peut être utilisé pour des scénarios tels que celui où un visiteur arrive sur votre site en cliquant sur une publicité display. |
| `authenticated` | L’utilisateur est actuellement authentifié dans une session active sur votre site web ou votre application. |
| `logged_out` | L’utilisateur était authentifié, mais actuellement déconnecté. L’utilisateur avait l’intention de se déconnecter de l’état authentifié. Il ne souhaite plus être considéré comme authentifié. |

Veuillez noter que seule la présence de `customerId` dans un état authentifié [!DNL Target] référence les données de profil utilisateur stockées et liées à customerId. Si l’état `customerId` est inconnu ou `logged_out`, il sera ignoré et les données de profil utilisateur qui peuvent être associées à cet état `customerId` ne seront pas utilisées pour le ciblage des audiences.

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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

L’exemple ci-dessus montre comment envoyer un `customerId` avec un `authenticatedState`. Lors de l&#39;envoi d&#39;un `customerId`, les `integrationCode`, `id` et `authenticatedState` ainsi que les `marketingCloudVisitorId` sont requis. `integrationCode` est l’alias du [fichier d’attributs du client](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=fr) que vous avez fourni via CRS.

## Profil fusionné

Vous pouvez combiner `tntId`, `thirdPartyID` et `marketingCloudVisitorId` dans la même requête. Dans ce scénario, [!DNL Adobe Target] conserve le mappage de tous ces identifiants et les épingle à un visiteur. Découvrez comment les profils sont [fusionnés et synchronisés en temps réel](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) à l’aide des différents identifiants.

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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

## Bucketing

Vos utilisateurs sont redirigés vers l’affichage d’une expérience selon la manière dont vous configurez vos activités [!DNL Adobe Target]. Dans [!DNL Adobe Target], le regroupement est :

* **Déterministe** : MurmurHash3 permet de s’assurer que votre utilisateur est regroupé et qu’il voit la variation appropriée à chaque fois que l’ID utilisateur est cohérent.
* **Attractif** : [!DNL Adobe Target] stocke la variation que votre utilisateur voit dans le profil utilisateur afin de s’assurer que la variation est systématiquement affichée pour cet utilisateur entre les sessions et les canaux. Les variations et l’attractivité sont garanties lors de l’utilisation de la prise de décision côté serveur. Lorsque la prise de décision sur l’appareil est utilisée, l’attractivité n’est pas garantie.

## Workflow de regroupement de bout en bout

Avant de passer à l’algorithme de regroupement, il est important de souligner que des étapes similaires sont utilisées pour sélectionner des activités en fonction de leur pourcentage d’affectation du trafic, ainsi que pour sélectionner une expérience au sein d’une activité.

### Etapes de sélection de l’activité

1. Générer un identifiant d’appareil, généralement un UUID
1. Obtention du code client
1. Obtention de l’ID d’activité
1. Procurez-vous le sel, qui est généralement une chaîne comme &quot;activité&quot;.
1. Calcul du hachage à l’aide de MurmurHash3
1. Obtention de la valeur absolue du hachage
1. Divisez la valeur absolue du hachage par 10 000
1. Divisez le reste par 1 000, ce qui devrait produire une valeur comprise entre 0 et 1.
1. Multiplier le résultat de 100 %
1. Comparez le pourcentage d’affectation du trafic d’activité au pourcentage obtenu. Si le pourcentage d’affectation du trafic est inférieur, l’activité est sélectionnée. Sinon, l’activité est ignorée.

### Etapes de sélection de l’expérience

1. Générer un identifiant d’appareil, généralement un UUID
1. Obtention du code client
1. Obtention de l’ID d’activité
1. Obtenez le sel, qui est généralement une chaîne comme &quot;expérience&quot;.
1. Calcul du hachage à l’aide de MurmurHash3
1. Obtention de la valeur absolue du hachage
1. Divisez la valeur absolue du hachage par 10 000
1. Divisez le reste par 1 000, ce qui devrait produire une valeur comprise entre 0 et 1.
1. Multiplier le résultat par le nombre total d’expériences dans l’activité.
1. Arrondir le résultat. Cela devrait produire l’index d’expérience.

### Exemple

Prenons l’exemple suivant :

* Client C avec code client `acmeclient`
* Activité A ayant l’identifiant `1111` et trois expériences `E1`, `E2`, `E3`
* Les expériences ont la distribution suivante : `E1` - 33 %, `E2` - 33 %, `E3` - 34 %

Le flux de sélection se présente comme suit :

1. ID de l’appareil `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. Code client `acmeclient`
1. ID d’activité `1111`
1. Sel `experience`
1. Valeur de hachage `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, valeur de hachage `-919077116`
1. Valeur absolue du hachage `919077116`
1. Reste après division par 10 000, `7116`
1. La valeur après le reste est divisée par 10 000, `0.7116`
1. Résultat après avoir multiplié la valeur par rapport au nombre total d’expériences `3 * 0.7116 = 2.1348`
1. L’index d’expérience est `2`, ce qui signifie la troisième expérience, puisque nous utilisons l’indexation basée sur `0`.
