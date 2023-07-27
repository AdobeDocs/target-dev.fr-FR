---
title: Identification et regroupement des utilisateurs
description: Identification et regroupement des utilisateurs
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 5%

---

# Identification et regroupement des utilisateurs

## Identification de l’utilisateur

Il existe plusieurs façons d’identifier un utilisateur dans [!DNL Adobe Target]. [!UICONTROL Cible] utilise les identifiants suivants :

| Nom du champ | Description |
| --- | --- |
| `tntID` | La variable `tntId` est l’identifiant Principal dans [!DNL Target] pour un utilisateur. Vous pouvez fournir cet identifiant, ou [!DNL Target] la génère automatiquement si la requête ne contient pas. |
| `thirdPartyId` | La variable `thirdPartyId` est l’identifiant de l’utilisateur de votre société, que vous pouvez envoyer avec chaque appel . Lorsqu’un utilisateur se connecte au site d’une entreprise, celle-ci crée généralement un identifiant lié au compte du visiteur, à sa carte de fidélité, à son numéro de membre ou à tout autre identifiant applicable de l’entreprise. |
| `marketingCloudVisitorId` | La variable `marketingCloudVisitorId` est utilisé pour fusionner et partager des données entre différentes solutions d’Adobe. MarketingCloudVisitorId est requis pour les intégrations avec Adobe Analytics et Adobe Audience Manager. |
| `customerIds` | Outre l’identifiant visiteur Experience Cloud, d’autres [ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) et un état authentifié pour chaque visiteur peut également être utilisé. |

## [!DNL Target] ID (tntID)

La variable [!DNL Target] ID ou `tntId`, peut être considéré comme un identifiant d’appareil. Ceci `tntId` est généré automatiquement par [!DNL Adobe Target] s’il n’est pas fourni dans la requête. Les requêtes suivantes doivent inclure ceci : `tntId` afin que le contenu approprié soit diffusé sur un appareil utilisé par le même utilisateur.

L’exemple d’appel suivant illustre une situation dans laquelle un appel `tntId` n’est pas transmis à [!DNL Target].

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

En l’absence d’une `tntId`, [!DNL Adobe Target] génère une `tntId` et le fournit dans la réponse, comme suit.

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

Dans cet exemple, la variable `tntId` is `10abf6304b2714215b1fd39a870f01afc.35_0`. Veuillez noter que `tntId` doit être utilisé pour le même utilisateur sur plusieurs sessions.

## ID tiers (thirdPartyId)

Si votre organisation utilise un ID pour identifier votre visiteur, vous pouvez utiliser `thirdPartyID` pour diffuser du contenu. A `thirdPartyID` est un identifiant persistant utilisé par votre entreprise pour identifier un utilisateur final, qu’il interagisse avec votre entreprise à partir de canaux web, mobiles ou IoT. En d’autres termes, la variable `thirdPartyId` référence les données de profil utilisateur qui peuvent être utilisées sur plusieurs canaux. Cependant, vous devez fournir la variable `thirdPartyID` pour chaque [!DNL Adobe Target] L’API de diffusion vous appelle.

L’exemple d’appel suivant illustre l’utilisation d’une `thirdPartyId`.

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

Dans ce scénario, [!DNL Adobe Target] génère une `tntId` puisqu’il n’a pas été transmis à l’appel d’origine, qui sera mappé à l’élément fourni `thirdPartyId`.

## Identifiant visiteur Marketing Cloud (marketingCloudVisitorId)

La variable `marketingCloudVisitorId` est un identifiant universel et permanent qui identifie vos visiteurs dans toutes les solutions Adobe Experience Cloud. Lorsque votre organisation met en oeuvre le service d’ID, cet ID vous permet d’identifier un même visiteur du site et ses données dans différentes solutions Experience Cloud, y compris [!DNL Adobe Target], Adobe Analytics et Adobe Audience Manager. Veuillez noter que `marketingCloudVisitorId` est requis lors de l’intégration [!DNL Target] avec [!DNL Adobe Analytics] et [!DNL Adobe Audience Manager].

L’exemple d’appel suivant montre comment un appel `marketingCloudVisitorId` qui a été récupéré du service d’ID d’Experience Cloud est transmis à [!DNL Target].

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

Dans ce scénario, [!DNL Target] génère une `tntId` puisqu’il n’a pas été transmis à l’appel d’origine, qui sera mappé à l’élément fourni `marketingCloudVisitorId`.

## ID de client (customerIds)

[ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) peuvent être ajoutés ou associés à un identifiant visiteur Experience Cloud. Lors de l’envoi `customerIds`, la variable `marketingCloudVisitorId` doit également être fourni. En outre, un état d’authentification peut être fourni avec chaque `customerId` pour chaque visiteur. Les statuts d&#39;authentification suivants peuvent être utilisés :

| État d’authentification | État d’utilisateur |
| --- | --- |
| `unknown` | Inconnu ou jamais authentifié. Cet état peut être utilisé pour des scénarios tels que celui où un visiteur arrive sur votre site en cliquant sur une publicité display. |
| `authenticated` | L’utilisateur est actuellement authentifié dans une session active sur votre site web ou votre application. |
| `logged_out` | L’utilisateur était authentifié, mais actuellement déconnecté. L’utilisateur avait l’intention de se déconnecter de l’état authentifié. Il ne souhaite plus être considéré comme authentifié. |

Notez que lorsque la variable `customerId` se trouve dans un état authentifié [!DNL Target] référencez les données de profil utilisateur stockées et liées à customerId. Si la variable `customerId` est dans une zone inconnue ou `logged_out` , il sera ignoré et toutes les données de profil utilisateur qui peuvent être associées à cet état. `customerId` ne sera pas utilisé pour le ciblage des audiences.

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

L’exemple ci-dessus montre comment envoyer une `customerId` avec un `authenticatedState`. Lors de l’envoi d’un `customerId`, la variable `integrationCode`, `id`, et `authenticatedState` ainsi que la variable `marketingCloudVisitorId` sont obligatoires. La variable `integrationCode` est l’alias de la variable [fichier d’attributs du client](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=fr) vous avez fourni via CRS.

## Profil fusionné

Vous pouvez combiner des `tntId`, `thirdPartyID`, et `marketingCloudVisitorId` dans la même requête. Dans ce scénario, [!DNL Adobe Target] maintiendra le mappage de tous ces identifiants et les épinglera à un visiteur. Découvrez comment les profils [fusionné et synchronisé en temps réel](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) en utilisant les différents identifiants.

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

L’exemple ci-dessus montre comment combiner des `tntId`, `thirdPartyID`, et `marketingCloudVisitorId` dans la même requête.

## Bucketing

Vos utilisateurs sont redirigés vers l’affichage d’une expérience en fonction de la configuration de votre [!DNL Adobe Target] activités. Dans [!DNL Adobe Target], le regroupement est :

* **Déterministe**: MurmurHash3 est utilisé pour s’assurer que votre utilisateur est regroupé et qu’il voit la variation appropriée à chaque fois que l’ID utilisateur est cohérent.
* **Attractif**: [!DNL Adobe Target] stocke la variation que votre utilisateur voit dans le profil utilisateur afin de s’assurer qu’elle est systématiquement présentée à cet utilisateur par sessions et canaux. Les variations et l’attractivité sont garanties lors de l’utilisation de la prise de décision côté serveur. Lorsque la prise de décision sur l’appareil est utilisée, l’attractivité n’est pas garantie.

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
* Activité A avec un ID `1111` et trois expériences `E1`, `E2`, `E3`
* Les expériences se répartissent comme suit : `E1` - 33%, `E2` - 33%, `E3` - 34 %

Le flux de sélection se présente comme suit :

1. ID de l’appareil `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. Code client `acmeclient`
1. Code d’activité `1111`
1. Sel `experience`
1. Valeur à hacher `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, valeur de hachage `-919077116`
1. Valeur absolue du hachage `919077116`
1. Reste après division à 10 000, `7116`
1. Valeur après le reste divisé par 10 000, `0.7116`
1. Résultat après avoir multiplié la valeur par rapport au nombre total d’expériences `3 * 0.7116 = 2.1348`
1. L’index d’expérience est `2`, ce qui signifie la troisième expérience, puisque nous utilisons `0` indexation basée sur .
