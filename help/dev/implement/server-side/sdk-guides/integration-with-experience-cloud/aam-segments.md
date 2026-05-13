---
title: Intégration avec les segments Experience Cloud AAM
description: Intégration à Experience Cloud, intégration à Audience Manager
keywords: api de diffusion, côté serveur, côté serveur, intégration, audience manager, aam
exl-id: c21e0200-23ba-4a0b-adf4-38e03c087f00
feature: Implement Server-side
TQID: https://experienceleague.adobe.com/mc55SxaUU8BJ81hKLji9xi0-OHCux3W4R0syuVoGrIo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 431
ht-degree: 4%

---

# Segments AAM

[!DNL Adobe Audience Manager] segments peuvent être utilisés via les SDK [!DNL Adobe Target]. Afin d’exploiter les segments AAM, les champs suivants doivent être fournis :

>[!NOTE]
>
>Les segments AAM ne sont pas pris en charge pour les activités de prise de décision sur l’appareil.

| Nom du champ | Requis | Description |
| --- | --- | --- |
| `locationHint` | Oui | L’indicateur d’emplacement du serveur de collecte de données est utilisé pour déterminer le point d’entrée du serveur de collecte de données AAM à atteindre afin de récupérer le profil. Doit être >= 1. |
| `marketingCloudVisitorId` | Oui | Identifiant visiteur Marketing Cloud |
| `blob` | Oui | L’objet Blob d’AAM est utilisé pour envoyer des données supplémentaires à AAM. Ne doit pas être vide et la taille &lt;= 1024. |

Le SDK renseigne automatiquement ces champs pour vous lors d’un appel de méthode `getOffers`, mais vous devez vous assurer qu’un cookie visiteur valide est fourni. Pour obtenir ce cookie, vous devez implémenter VisitorAPI.js dans le navigateur.

## Guide de mise en œuvre

### Utilisation des cookies

Les cookies sont utilisés pour corréler les requêtes [!DNL Adobe Audience Manager] aux requêtes [!DNL Adobe Target]. Il s’agit des cookies utilisés dans cette implémentation.

| Cookie | Nom | Description |
| --- | --- | --- |
| cookie visiteur | `AMCVS_XXXXXXXXXXXXXXXXXXXXXXXX%40AdobeOrg` | Ce cookie est défini par `VisitorAPI.js` lorsqu’il est initialisé avec `visitorState` à partir de la réponse `getOffers` cible. |
| cookie target | `mbox` | Votre serveur web doit définir ce cookie à l’aide du nom et de la valeur de `targetCookie` de la réponse `getOffers` cible. |

### Présentation des étapes

Supposons qu’un utilisateur saisisse une URL dans un navigateur qui envoie une requête à votre serveur web. Lorsque vous répondez à cette demande :

1. Le serveur lit les cookies visiteur et cible à partir de la requête.
1. Le serveur effectue un appel à la méthode `getOffers` du SDK [!DNL Target], en spécifiant les cookies visiteur et cible, le cas échéant.
1. Lorsque l’appel `getOffers` est terminé, les valeurs de `targetCookie` et de `visitorState` de la réponse sont utilisées.
   1. Un cookie est défini sur la réponse avec des valeurs issues de `targetCookie`. Cette opération s’effectue à l’aide de l’en-tête de réponse `Set-Cookie`, qui indique au navigateur de conserver le cookie cible.
   1. Une réponse HTML est préparée qui initialise le `VisitorAPI.js` et transmet le `visitorState` à partir de la réponse cible.
1. La réponse d’HTML est chargée dans le navigateur......................................................................................................................................................................................................................................................................................................................
   1. `VisitorAPI.js` est inclus dans l’en-tête du document.
   1. VisitorAPI est initialisé avec `visitorState` à partir de la réponse SDK `getOffers`. Le cookie du visiteur sera alors défini dans le navigateur afin d’être envoyé au serveur lors des requêtes ultérieures.

### Exemple de code

L’exemple de code suivant met en œuvre chacune des étapes décrites ci-dessus. Chaque étape apparaît dans le code sous la forme d’un commentaire intégré en regard de son implémentation.

#### Node.js

Cet exemple repose sur [express, un framework web Node.js](https://expressjs.com/).

>[!BEGINTABS]

>[!TAB server.js]

```js {line-numbers="true"}
const fs = require("fs");
const express = require("express");
const cookieParser = require("cookie-parser");
const Handlebars = require("handlebars");
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  timeout: 10000,
  logger: console,
};
const targetClient = TargetClient.create(CONFIG);
const TEMPLATE = fs.readFileSync(`${__dirname}/index.handlebars`).toString();
const handlebarsTemplate = Handlebars.compile(TEMPLATE);

Handlebars.registerHelper("toJSON", function (object) {
  return new Handlebars.SafeString(JSON.stringify(object, null, 4));
});

const app = express();
app.use(cookieParser());
app.use(express.static(__dirname + "/public"));

app.get("/", async (req, res) => {
  // The server reads the visitor and target cookies from the request.
  const visitorCookie =
    req.cookies[
      encodeURIComponent(
        TargetClient.getVisitorCookieName(CONFIG.organizationId)
      )
    ];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const address = { url: req.headers.host + req.originalUrl };

  const targetRequest = {
    execute: {
      mboxes: [
        { name: "homepage", index: 1, address },
        { name: "SummerShoesOffer", index: 2, address },
        { name: "SummerDressOffer", index: 3, address }
      ],
    },
  };

  res.set({
    "Content-Type": "text/html",
    Expires: new Date().toUTCString(),
  });

  try {
    // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
    const targetResponse = await targetClient.getOffers({
      request: targetRequest,
      visitorCookie,
      targetCookie,
    });

    // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
    // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
    res.cookie(
      targetResponse.targetCookie.name,
      targetResponse.targetCookie.value,
      { maxAge: targetResponse.targetCookie.maxAge * 1000 }
    );

    // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
    const html = handlebarsTemplate({
      organizationId: CONFIG.organizationId,
      targetResponse,
    });

    res.status(200).send(html);
  } catch (error) {
    console.error("Target:", error);
    res.status(500).send(error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB index.handlebars]

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>

  <!-- VisitorAPI.js is included in the document header. -->
  <script src="VisitorAPI.js"></script>
  <script>
    // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
    Visitor.getInstance("{{organizationId}}", {serverState: {{toJSON targetResponse.visitorState}} });
  </script>
</head>
<body>
  <h1>response</h1>
  <pre>{{toJSON targetResponse}}</pre>
</body>
</html>
```

>[!ENDTABS]

#### Java

Cet exemple utilise [spring, un framework web Java](https://spring.io/).

>[!BEGINTABS]

>[!TAB ClientSampleApplication.java]

```java {line-numbers="true"}
@SpringBootApplication
public class ClientSampleApplication {

    public static void main(String[] args) {
        System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
        SpringApplication.run(ClientSampleApplication.class, args);
    }

    @Bean
    TargetClient marketingCloudClient() {
        ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .defaultDecisioningMethod(DecisioningMethod.SERVER_SIDE)
                .build();

        return TargetClient.create(clientConfig);
    }
}
```

>[!TAB TargetController.java]

```java {line-numbers="true"}
@Controller
@RequestMapping("/")
public class TargetController {

    @Autowired
    private TargetClientService targetClientService;

    @GetMapping
    public String index(Model model, HttpServletRequest request, HttpServletResponse response) {
        // The server reads the visitor and target cookies from the request.
        List<TargetCookie> targetCookies = getTargetCookies(request.getCookies());

        Address address = getAddress(request);

        List<MboxRequest> mboxRequests = new ArrayList<>();
        mboxRequests.add((MboxRequest) new MboxRequest().name("homepage").index(1).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerShoesOffer").index(2).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerDressOffer").index(3).address(address));

        TargetDeliveryResponse targetDeliveryResponse = targetClientService.getOffers(mboxRequests, targetCookies, request,
                response);

        // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
        model.addAttribute("visitorState", targetDeliveryResponse.getVisitorState());
        model.addAttribute("targetResponse", targetDeliveryResponse);
        model.addAttribute("organizationId", "1234567890@AdobeOrg");

        return "index";
    }
}
```

>[!TAB TargetClientService.java]

```java {line-numbers="true"}
@Service
public class TargetClientService {

    private final TargetClient targetJavaClient;

    public TargetClientService(TargetClient targetJavaClient) {
        this.targetJavaClient = targetJavaClient;
    }

    public TargetDeliveryResponse getOffers(List<MboxRequest> executeMboxes, List<TargetCookie> cookies, HttpServletRequest request, HttpServletResponse response) {

        Context context = getContext(request);
        ExecuteRequest executeRequest = new ExecuteRequest();
        executeRequest.setMboxes(executeMboxes);

        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .execute(executeRequest)
                .cookies(cookies)
                .build();

        // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);

        // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
        // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
        setCookies(targetResponse.getCookies(), response);
        return targetResponse;
    }
}
```

>[!TAB TargetRequestUtils.java]

```java {line-numbers="true"}
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Target Only : GetOffer</title>

    <!-- VisitorAPI.js is included in the document header. -->
    <script src="../../js/VisitorAPI.js"></script>
    <script th:inline="javascript">
        // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
        Visitor.getInstance(/*[[${organizationId}]]*/ "", {serverState: /*[[${visitorState}]]*/ {}});
    </script>
</head>
<body>
    <h1>response</h1>
    <pre>[[${targetResponse}]]</pre>
</body>
</html>
```

>[!ENDTABS]

Pour plus d’informations sur `TargetRequestUtils.java`, voir [Méthodes utilitaires (Java) &#x200B;](https://experienceleague.adobe.com/docs/target-dev/developer/server-side/java/utility-methods.html){target=_blank}
