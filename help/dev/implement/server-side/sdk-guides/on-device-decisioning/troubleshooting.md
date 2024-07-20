---
title: Résolution des problèmes de prise de décision sur les appareils
description: Découvrez comment résoudre les problèmes [!UICONTROL on-device decisioning]
exl-id: e76f95ce-afae-48e0-9dbb-2097133574dc
feature: APIs/SDKs
source-git-commit: 1d892d4d4d6f370f7772d0308ee0dd0d5c12e700
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Résolution des problèmes [!UICONTROL on-device decisioning]

## Validation de la configuration

### Résumé des étapes

1. Assurez-vous que le `logger` est configuré
1. Assurez-vous que les [!DNL Target] traces sont activées
1. Vérifiez que l’ [!UICONTROL on-device decisioning] *artefact de règle* a été récupéré et mis en cache selon l’intervalle d’interrogation défini.
1. Validez la diffusion de contenu via l’artefact de règle mis en cache en créant une activité de test [!UICONTROL on-device decisioning] via le compositeur d’expérience d’après les formulaires.
1. Erreurs de notification d’envoi Inspect

## 1. Vérifiez que l’enregistreur est configuré.

Lors de l’initialisation du SDK, veillez à activer la journalisation.

**Node.js**

Pour le SDK Node.js, un objet `logger` doit être fourni.

```js {line-numbers="true"}
const CONFIG = {
  client: "<your client code>",
  organizationId: "<your organization ID>",
  logger: console
};
```

**SDK Java**

Pour le SDK Java `logRequests` sur `ClientConfig`, doit être activé.

```js {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("<your client code>")
  .organizationId("<your organization ID>")
  .logRequests(true)
  .build();
```

La JVM doit également être lancée avec le paramètre de ligne de commande suivant :

```bash {line-numbers="true"}
java -Dorg.slf4j.simpleLogger.defaultLogLevel=DEBUG ...
```

## 2. Vérifiez que [!DNL Target]Traces est activé

L’activation des traces génère des informations supplémentaires à partir de [!DNL Adobe Target] en ce qui concerne l’artefact de règles.

1. Accédez à l’[!DNL Target]interface utilisateur dans [!DNL Experience Cloud].

   ![alt image](assets/asset-target-ui-1.png)

1. Accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** et cliquez sur **[!UICONTROL Generate New Authorization Token]**.

   ![alt image](assets/asset-target-ui-2.png)

1. Copiez le jeton d’autorisation nouvellement généré dans le presse-papiers et ajoutez-le à votre requête [!DNL Target]:

   **Node.js**

   ```js {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: "88f1a924-6bc5-4836-8560-2f9c86aeb36b"
     },
     execute: {
       mboxes: [{
         name: "sdk-mbox"
       }]
   }};
   ```

   **Java**

   ```js {line-numbers="true"}
   Trace trace = new Trace()
     .authorizationToken("88f1a924-6bc5-4836-8560-2f9c86aeb36b");
   Context context = new Context()
     .channel(ChannelType.WEB);
   MboxRequest mbox = new MboxRequest()
     .name("sdk-mbox")
     .index(0);
   ExecuteRequest executeRequest = new ExecuteRequest()
     .mboxes(Arrays.asList(mbox));
   
   TargetDeliveryRequest request = TargetDeliveryRequest.builder()
     .trace(trace)
     .context(context)
     .execute(executeRequest)
     .build();
   ```

1. Une fois l’enregistreur et la trace en place, démarrez votre application et surveillez le terminal du serveur. La sortie suivante de l’enregistreur confirme que l’artefact de règle a été récupéré :

   **SDK Node.js**

   ```text {line-numbers="true"}
     AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-code/production/v1/rules.json
     AT: LD.ArtifactProvider artifact received - status=200
   ```

## 3. Vérifiez que l’ [!UICONTROL on-device decisioning] *artefact de règle* a été récupéré et mis en cache selon l’intervalle d’interrogation défini.

1. Patientez pendant la durée de l’intervalle d’interrogation (20 minutes par défaut) et assurez-vous que l’artefact est récupéré par le SDK. Les mêmes journaux de terminal seront générés.

   De plus, les informations de la [!DNL Target]Trace doivent être envoyées au terminal avec des détails sur l’artefact de règle.

   ```text {line-numbers="true"}
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
       "clientCode": "your-client-code",
       "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```

## 4. Validez la diffusion de contenu via l’artefact de règle mis en cache en créant une activité de test [!UICONTROL on-device decisioning] via le compositeur d’expérience d’après les formulaires

1. Accédez à l’interface utilisateur de [!DNL Target]dans Experience Cloud

   ![alt image](assets/asset-target-ui-1.png)

1. Créez une activité XT à l’aide du compositeur d’expérience d’après les formulaires.

   ![alt image](assets/asset-form-base-composer-ui.png)

1. Saisissez le nom de mbox utilisé dans votre requête [!DNL Target]comme emplacement de l’activité XT (notez qu’il doit s’agir d’un nom de mbox unique, spécifiquement à des fins de développement).

   ![alt image](assets/asset-mbox-location-ui.png)

1. Remplacez le contenu par une offre d’HTML ou JSON. Cela sera renvoyé dans la requête[!DNL Target]à votre application. Laissez le ciblage de l’activité &quot;Tous les visiteurs&quot; et sélectionnez une mesure de votre choix. Nommez l’activité, enregistrez-la, puis activez-la pour vous assurer que la mbox/l’emplacement utilisé est réservé au développement.

   ![alt image](assets/asset-target-content-ui.png)

1. Dans votre application, ajoutez une instruction de journal pour le contenu reçu dans la réponse de votre requête [!DNL Target].

   **SDK Node.js**

   ```js {line-numbers="true"}
   try {
     const response = await targetClient.getOffers({ request });
     console.log('Response: ', response.response.execute.mboxes[0].options[0].content);
   } catch (error) {
     console.error('Something went wrong', error);
   }
   ```

   **SDK Java**

   ```js {line-numbers="true"}
   try {
     Context context = new Context()
       .channel(ChannelType.WEB);
     MboxRequest mbox = new MboxRequest()
       .name("sdk-mbox")
       .index(0);
     ExecuteRequest executeRequest = new ExecuteRequest()
       .mboxes(Arrays.asList(mbox));
   
     TargetDeliveryRequest request = TargetDeliveryRequest.builder()
       .context(context)
       .decisioningMethod(DecisioningMethod.ON_DEVICE)
       .execute(executeRequest)
       .build();
   
       TargetDeliveryResponse response = targetClient.getOffers(request);
     logger.debug("Response: ", response.getResponse().getExecute().getMboxes().get(0).getOptions().get(0).getContent());
   } catch (Exception exception) {
     logger.error("Something went wrong", exception);
   }
   ```

1. Consultez les journaux de votre terminal pour vérifier que votre contenu est en cours de diffusion et qu’il a été diffusé via l’artefact de règles sur votre serveur. L’objet `LD.DeciscionProvider` est généré lorsque la qualification et la prise de décision de l’activité ont été déterminées sur l’appareil en fonction de l’artefact de règles. De plus, en raison de la journalisation de `content`, vous devriez voir `<div>test</div>` ou la réponse que vous avez choisie lors de la création de l’activité de test.

   **Sortie de journalisation**

   ```text {line-numbers="true"}
   AT: LD.DecisionProvider {...}
   AT: Response received {...}
   Response:  <div>test</div>
   ```

## Erreurs de notification d’envoi Inspect

Lors de l’utilisation de la prise de décision sur l’appareil, des notifications sont envoyées automatiquement pour que getOffers exécute les requêtes. Ces demandes sont envoyées en arrière-plan de manière silencieuse. Toutes les erreurs peuvent être inspectées en s’abonnant à un événement appelé `sendNotificationError`. Voici un exemple de code montrant comment s’abonner aux erreurs de notification à l’aide du SDK Node.js.

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
let client;

function onSendNotificationError({ notification, error }) {
  console.log(
    `There was an error when sending a notification: ${error.message}`
  );
  console.log(`Notification Payload: ${JSON.stringify(notification, null, 2)}`);
}

async function targetClientReady() {
  const request = {
    context: { channel: "web" },
    execute: {
      mboxes: [{
        name: "a1-serverside-ab",
        index: 1
      }]
    }
  };
  const targetResponse = await client.getOffers({ request });
}

client = TargetClient.create({
  events: {
    clientReady: targetClientReady,
    sendNotificationError: onSendNotificationError
  }
});
```

## Scénarios de dépannage courants

Veillez à passer en revue les [fonctionnalités prises en charge](supported-features.md) pour [!UICONTROL on-device decisioning] lorsque vous rencontrez des problèmes.

### Les activités de prise de décision sur appareil ne s’exécutent pas en raison d’une audience ou d’une activité non prise en charge

Un problème courant qui peut se produire est que les activités [!UICONTROL on-device decisioning] ne s’exécutent pas en raison de l’audience utilisée ou du type d’activité non pris en charge.

(1) À l’aide de la sortie du journal, passez en revue les entrées de la propriété trace dans votre objet de réponse. Identifiez spécifiquement la propriété des campagnes :

**Sortie de suivi**

```text {line-numbers="true"}
  "execute": {
  "mboxes": [
    {
      "name": "your-mbox-name",
      "index": 0,
      "trace": {
        "clientCode": "your-client-code",
        ...
        "campaigns": [],
        ...
      }
    }
```

Vous remarquerez que l’activité pour laquelle vous essayez de vous qualifier ne figure pas dans la propriété `campaigns`, car l’audience ou le type d’activité n’est pas pris en charge. Si l’activité est répertoriée sous la propriété `campaigns`, votre problème n’est pas dû à une audience ou à un type d’activité non pris en charge.

(2) Recherchez également le fichier `rules.json` en regardant `trace` > `artifact` > `artifactLocation` dans la sortie de l’enregistreur et notez que votre activité est absente de la propriété `rules` > `mboxes` :

**Sortie de journalisation**

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: { },
   views: { }
 }
```

Enfin, accédez à l’[!DNL Target]interface utilisateur et localisez l’activité en question : [experience.adobe.com/target](https://experience.adobe.com/target)

Passez en revue les règles utilisées dans l’audience et assurez-vous de n’utiliser que celles mentionnées ci-dessus qui sont prises en charge. De plus, assurez-vous que le type d’activité est A/B ou XT.

![alt image](assets/asset-target-audience-ui.png)

### Les activités de prise de décision sur appareil ne s’exécutent pas en raison d’une audience non qualifiée

Si une activité de prise de décision sur l’appareil ne s’exécute pas, mais que vous avez vérifié que votre fichier rules.json contient l’activité, procédez comme suit :

(1) Assurez-vous que la mbox que vous exécutez dans votre application est la même que celle utilisée par l’activité :

>[!BEGINTABS]

>[!TAB rule.json]

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: {
    target-only-node-sdk-mbox: [{ // this mbox name must match the mbox in your request
      ...
    }]
   }
 ...
```

>[!TAB SDK Node.js]

```js {line-numbers="true"}
 const request = {
   trace: {
     authorizationToken: '2dfc1dce-1e58-4e05-bbd6-a6725893d4d6'
   },
   execute: {
     mboxes: [{
       address: getAddress(req),
       name: "target-only-node-sdk-mbox-two" // this mbox name must match the mbox the activity is using
     }]
   }};
```

>[!TAB SDK Java]

```js {line-numbers="true"}
Context context = new Context()
  .channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("target-only-node-sdk-mbox-two")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .decisioningMethod(DecisioningMethod.ON_DEVICE)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

(2) Assurez-vous que vous êtes qualifié pour l’audience de votre activité en examinant la propriété `matchedRuleConditions` ou `unmatchedRuleConditions` de votre sortie de trace :

**Sortie de suivi**

```text {line-numbers="true"}
...
},
"campaignId": 368564,
"campaignType": "landing",
"matchedSegmentIds": [],
"unmatchedSegmentIds": [
  6188838
      ],
      "matchedRuleConditions": [],
          "unmatchedRuleConditions": [
            {
              "in": [
                "true",
                {
                  "var": "mbox.auth_lc"
                }
              ]
            }
          ]
    ...
```

Si vous avez des conditions de règle sans correspondance, vous n’êtes pas qualifié pour l’activité et l’activité ne s’exécutera donc pas. Passez en revue les règles de votre audience pour voir pourquoi vous n’êtes pas qualifié.

### L’activité de prise de décision sur appareil ne s’exécute pas, mais la raison n’est pas apparente

Il n’est peut-être pas évident de comprendre pourquoi une activité de prise de décision sur appareil ne s’exécute pas. Dans ce cas, procédez comme suit pour identifier le problème :

(1) Lisez la sortie de trace de journal dans votre console et identifiez la propriété d’artefact, qui ressemblera à ce qui suit :

**Sortie de suivi**

```text {line-numbers="true"}
...
      "artifact": {
          "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
          "pollingInterval": 300000,
          "pollingHalted": false,
          "artifactVersion": "1.0.0",
          "artifactRetrievalCount": 3,
          "artifactLastRetrieved": "2020-10-16T00:56:27.596Z",
          "clientCode": "adobeinterikleisch",
          "environment": "production"
        },
...
```

Examinez la date `artifactLastRetrieved` de l’artefact et assurez-vous que le dernier fichier `rules.json` est téléchargé dans votre application.

(2) Recherchez la propriété `evaluatedCampaignTargets` dans la sortie de l&#39;enregistreur :

**Sortie de journalisation**

```text {line-numbers="true"}
...
  "evaluatedCampaignTargets": [
      {
        "context": {
          "current_timestamp": 1602812599608,
          "current_time": "0143",
          "current_day": 5,
          "user": {
            "browserType": "unknown",
            "platform": "Unknown",
            "locale": "en",
            "browserVersion": -1
          },
          "page": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "referring": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "geo": {},
          "mbox": {},
          "allocation": 23.79
        },
        "campaignId": 368564,
        "campaignType": "landing",
        "matchedSegmentIds": [],
        "unmatchedSegmentIds": [
          6188838
        ],
        "matchedRuleConditions": [],
        "unmatchedRuleConditions": [
          {
            "in": [
              "true",
              {
                "var": "mbox.auth_lc"
              }
            ]
          }
        ]
...
```

(3) Examinez les données `context`, `page` et `referring` pour vous assurer qu’elles sont aussi bonnes que prévu, car elles peuvent affecter la qualification de ciblage de l’activité.

(4) Vérifiez le `campaignId` pour vous assurer que l’activité ou les activités que vous prévoyez d’exécuter sont évaluées. Le `campaignId` correspondra à l’ID d’activité sur l’onglet d’aperçu de l’activité dans l’[!DNL Target]interface utilisateur :

![alt image](assets/asset-activity-id-target-ui.png)

(5) Passez en revue les `matchedRuleConditions` et `unmatchedRuleConditions` afin d’identifier les problèmes admissibles aux règles d’audience pour une activité donnée.

(6) Consultez le dernier fichier `rules.json` pour vous assurer que l’activité ou les activités que vous souhaitez exécuter localement sont incluses. L’emplacement est référencé ci-dessus à l’étape 1.

(7) Assurez-vous que vous utilisez les mêmes noms de mbox dans votre requête et dans vos activités.

(8) Assurez-vous d’utiliser les règles d’audience prises en charge et les types d’activité pris en charge.

### Un appel au serveur est effectué même si la configuration de l’activité sous une mbox indique &quot;On Device Decisioning Eligible&quot; dans l’interface utilisateur de [!DNL Target].

Il existe plusieurs raisons pour lesquelles un appel au serveur est effectué même si l’appareil est éligible pour la prise de décision sur l’appareil :

* Lorsque la mbox utilisée pour une activité &quot;On Device Decisioning Eligible&quot; est également utilisée pour d’autres activités qui ne sont pas &quot;On Device Decisioning Eligible&quot;, la mbox est répertoriée sous la section `remoteMboxes` de l’artefact `rules.json`. Lorsqu’une mbox est répertoriée sous `remoteMboxes`, tout appel `getOffer(s)` à cette mbox déclenche un appel au serveur.

* Si vous configurez une activité sous un espace de travail/une propriété et que vous n’en incluez pas la même lors de la configuration du SDK, cela peut entraîner le téléchargement de l’`rules.josn` de l’espace de travail par défaut, qui peut utiliser la mbox sous la section `remoteMboxes` .
