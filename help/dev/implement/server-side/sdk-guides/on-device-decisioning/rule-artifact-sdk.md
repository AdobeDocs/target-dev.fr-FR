---
title: Télécharger, stocker et mettre à jour automatiquement l’artefact de règle de prise de décision sur l’appareil
description: Découvrez comment utiliser l’artefact de règle de prise de décision sur l’appareil lors de l’initialisation du  [!DNL Adobe Target] SDK.
feature: APIs/SDKs
exl-id: be41a723-616f-4aa3-9a38-8143438bd18a
TQID: https://experienceleague.adobe.com/o4oNaCtd3PS1cDndSJHkI10pDke1DTaEnBn8u9pIQk8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7a5aae2510a014c6efaeee63080cde3e7746f91c
workflow-type: tm+mt
source-wordcount: 350
ht-degree: 0%

---

# Téléchargement, stockage et mise à jour automatique de l’artefact de règle via [!DNL Adobe Target] SDK

Cette approche est préférable lorsque vous pouvez initialiser le SDK [!DNL Adobe Target] en même temps que vous initialisez et démarrez votre serveur web. L’artefact de règle sera téléchargé par le SDK [!DNL Adobe Target] et mis en mémoire cache avant que votre application de serveur web ne commence à traiter les requêtes. Une fois votre application web en cours d’exécution, toutes les décisions [!DNL Adobe Target] sont exécutées à l’aide de l’artefact de règle en mémoire. L’artefact de règle mis en cache sera mis à jour en fonction du `pollingInterval` que vous spécifiez lors de l’étape d’initialisation du SDK.

## Résumé des étapes

1. Installation du SDK
1. Initialiser le SDK
1. Stocker et utiliser l’artefact de règle

## &#x200B;1. Installation du SDK

>[!BEGINTABS]

>[!TAB NPM]

```javascript {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB  MVN ]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0</version>
</dependency>
```

>[!ENDTABS]

## &#x200B;2. Initialiser le SDK

1. Tout d’abord, importez le SDK. Effectuez une importation dans le même fichier à partir duquel vous pouvez contrôler le démarrage de votre serveur.

   **Node.js**

   ```javascript {line-numbers="true"}
   const TargetClient = require("@adobe/target-nodejs-sdk");
   ```

   **Java**

   ```javascript {line-numbers="true"}
   import com.adobe.target.edge.client.ClientConfig;
   import com.adobe.target.edge.client.TargetClient;
   ```

1. Pour configurer le SDK, utilisez la méthode create .

   **Node.js**

   ```javascript {line-numbers="true"}
   const CONFIG = {
       client: "<your target client code>",
       organizationId: "your EC org id",
       decisioningMethod: "on-device",
       pollingInterval : 300000,
       events: {
           clientReady: startWebServer
       }
   };
   
   const TargetClient = TargetClient.create(CONFIG);
   
   function startWebServer() {
       //Adobe Target SDK has now downloaded the JSON Artifacts and is available in the memory.
       //You can start your web server now to serve requests now.
   }
   ```

   **Java**

   ```javascript {line-numbers="true"}
   ClientConfig config = ClientConfig.builder()
       .client("<you target client code>")
       .organizationId("<your EC org id>")
       .build();
   TargetClient targetClient = TargetClient.create(config);
   ```

1. Les paramètres client et organizationId peuvent être récupérés à partir de [!DNL Adobe Target] en accédant à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**, comme illustré ici.

   <!-- Insert image-client-code.png -->
   ![Page Implémentation sous Administration dans Target](assets/asset-rule-artifact-3.png)

## &#x200B;3. Stocker et utiliser l’artefact de règle

Vous n’avez pas besoin de gérer vous-même l’artefact de règle et l’appel des méthodes SDK doit être simple.

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
//req is the request object from the server request listener method
const targetCookie = req.cookies[TargetClient.TargetCookieName];
const request = {
    context: {
        channel: "web"
    },
    execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner"
        }],
    },
};

TargetClient.getOffers({
    request,
    targetCookie
}).then(function(response) {
    //This Target response is coming from the In-memory Target artifact.
    console.log("Target response", response);
}).catch(function(err) {
    console.error("Target:", err);
})
```

>[!TAB Java]

```java {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

>[!NOTE]
>
>Dans l’exemple de code ci-dessus, l’objet `TargetClient` contient une référence à l’artefact de règle en mémoire. Lorsque vous utilisez cet objet pour appeler les méthodes SDK standard, il utilise l’artefact de règle en mémoire pour la prise de décision. Si votre application est structurée de manière à appeler les méthodes SDK dans des fichiers autres que celui qui initialise et écoute les requêtes des clients, et si ces fichiers n’ont pas accès à l’objet TargetClient, vous pouvez télécharger la payload JSON et la stocker dans un fichier JSON local pour la consommer dans d’autres fichiers, qui doivent initialiser le SDK. Cela est expliqué dans la section suivante, concernant [le téléchargement de l’artefact de règle à l’aide d’une payload JSON](rule-artifact-json.md).

Voici un exemple qui démarre une application web après l’initialisation du SDK [!DNL Adobe Target].

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
    client: "<your target client code>",
    organizationId: "your EC org id",
    decisioningMethod: "on-device",
    pollingInterval : 300000,
    events: {
        clientReady: startWebServer
    }
};

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());
  saveCookie(res, response.targetCookie);
  res.status(200).send(response);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

function startWebServer() {
    app.get('/*', async (req, res) => {
    const targetCookie = req.cookies[TargetClient.TargetCookieName];
    const request = {
        execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner" // Ensure that you have a LIVE Activity running on this location
        }]
        }};

    try {
        const response = await targetClient.getOffers({ request, targetCookie });
        sendSuccessResponse(res, response);
    } catch (error) {
        console.error("Target:", error);
        sendErrorResponse(res, error);
    }
    });

    app.listen(3000, function () {
    console.log("Listening on port 3000 and watching!");
    });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

@Controller
public class TargetController {

  private TargetClient targetClient;

  TargetController() {
    // You should instantiate TargetClient in a Bean and inject the instance into this class 
    // but we show the code here for demonstration purpose.
    ClientConfig config = ClientConfig.builder()
        .client("<you target client code>")
        .organizationId("<your EC org id>")
        .build();
    targetClient = TargetClient.create(config);
  }

  @GetMapping("/")
  public String homePage() {
    MboxRequest mbox = new MboxRequest().name("homepage").index(0);
    TargetDeliveryRequest request = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
        .build();
    TargetDeliveryResponse response = targetClient.getOffers(request);
    // ...
  }
}
```

>[!ENDTABS]
