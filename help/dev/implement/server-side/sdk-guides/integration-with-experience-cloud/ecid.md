---
title: Service d’ID Experience Cloud (ECID)
description: Bien que la variable [!DNL Target] SDK pour la récupération de contenu à partir de [!DNL Target] peut être puissant, ce qui ajoute la valeur ajoutée de l’utilisation de la variable [!UICONTROL Identifiant Experience Cloud] (ECID) pour le suivi des utilisateurs s’étend au-delà de l’Adobe [!DNL Target]. The ECID enables you to leverage [!DNL Adobe Experience Cloud] produits et fonctionnalités, tels que les rapports A4T et [!DNL Adobe Audience Manager] (AAM) .
exl-id: fd7e5c3e-51c1-4965-ab6a-f50a6b0c910b
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# [!UICONTROL Identifiant Experience Cloud] Service (ECID)

## [!UICONTROL Identifiant Experience Cloud] Intégration (ECID)

Bien que la variable [!DNL Target] SDK pour la récupération de contenu à partir de [!DNL Target] peut être puissant, ce qui ajoute la valeur ajoutée de l’utilisation de la variable [!UICONTROL Identifiant Experience Cloud] (ECID) pour le suivi des utilisateurs s’étend au-delà de [!DNL Adobe Target]. L’ECID vous permet d’exploiter [!DNL Adobe Experience Cloud] produits et fonctionnalités, tels que les rapports A4T et [!DNL Adobe Audience Manager] (AAM) .

L’ECID est généré et géré par `visitor.js`, qui conserve son propre état. La variable `visitor.js` crée un cookie nommé `AMCV_{organizationId}`, qui est utilisé par [!DNL Target] SDK pour l’intégration ECID. Lorsque la variable [!DNL Target] la réponse est renvoyée, vous devez mettre à jour l’instance Visiteur côté client avec `thevisitorState` renvoyé par la variable [!DNL Target] SDK.

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>Sample content</pre>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>${content}</pre>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js is stored in "public" folder
app.use(express.static(__dirname + "/public"));

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

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const request = {
      execute: {
        mboxes: [{
          address: { url: req.headers.host + req.originalUrl },
          name: "a1-serverside-ab"
        }]
      }};
```

>[!TAB Java ]

```java {line-numbers="true"
  console.log("Request", request);

  try {
      const response = await targetClient.getOffers({ request, visitorCookie, targetCookie });
      sendSuccessResponse(res, response);
    } catch (error) {
      sendErrorResponse(res, error);
    }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
@Controller
public class TargetControllerSample {

  @Autowired
  private TargetClient targetClient;

  @GetMapping("/")
  public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
    Context context = getContext(request);
    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(context)
        .prefetch(getPrefetchRequest())
        .cookies(getTargetCookies(request.getCookies()))
        .build();

    TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
    model.addAttribute("visitorState", targetResponse.getVisitorState());
    model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
    setCookies(targetResponse.getCookies(), response);
    return "targetMcid";
  }
}
```

>[!ENDTABS]

## Intégration d’ECID avec l’ID de client

Pour effectuer le suivi des comptes d’utilisateurs des visiteurs et des détails d’état de connexion, `customerIds` peut être transmis via [!DNL Target] SDK.

```html {line-numbers="true"
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>Sample content</pre>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) with Customer IDs Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>${content}</pre>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js is stored in "public" folder
app.use(express.static(__dirname + "/public"));

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

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const customerIds = {
      "userid": {
        "id": "67312378756723456",
        "authState": TargetClient.AuthState.AUTHENTICATED
      }
    };
  const request = {
    execute: {
      mboxes: [{
        address: { url: req.headers.host + req.originalUrl },
        name: "a1-serverside-ab"
      }]
    }};

  try {
    const response = await targetClient.getOffers({ request, visitorCookie, targetCookie, customerIds });
    sendSuccessResponse(res, response);
  } catch (error) {
    sendErrorResponse(res, error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB Java ]

```java {line-numbers="true"}
@Controller
public class TargetControllerSample {

  @Autowired
  private TargetClient targetJavaClient;

  @GetMapping("/targetMcid")
  public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
    Context context = getContext(request);
    Map<String, CustomerState> customerIds = new HashMap<>();
    customerIds.put("userid", CustomerState.authenticated("67312378756723456"));
    customerIds.put("puuid", CustomerState.unknown("550e8400-e29b-41d4-a716-446655440000"));
    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
       .context(context)
       .prefetch(getPrefetchRequest())
       .cookies(getTargetCookies(request.getCookies()))
       .customerIds(customerIds)
       .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
    model.addAttribute("visitorState", targetResponse.getVisitorState());
    model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
    setCookies(targetResponse.getCookies(), response);
    return "targetMcid";
  }
}
```

>[!ENDTABS]

## ECID et [!DNL Analytics] Intégration

Pour tirer le meilleur parti du [!DNL Target] SDK et pour utiliser les puissantes fonctionnalités d’analyse fournies par [!DNL Adobe Analytics], vous pouvez utiliser des intégrations dans ECID, [!DNL Analytics], et [!DNL Target].

Utilisation d’intégrations entre ECID, [!DNL Analytics], et [!DNL Target] vous permet :

* Utilisation de segments de Adobe Audience Manager (AAM)
* Personnaliser l’expérience utilisateur en fonction du contenu récupéré à partir de [!DNL Target]
* Assurez-vous que tous les événements et mesures de succès sont collectés dans [!DNL Analytics]
* Utilisation [!DNL Analytics]&quot;requêtes puissantes et bénéficier de ses formidables visualisations de rapports

Intégrations dans ECID, [!DNL Analytics], et [!DNL Target] ne nécessitent aucune gestion spéciale pour les analyses côté serveur. Une fois que l’ECID est intégré, ajoutez `AppMeasurement.js` ([!DNL Analytics] ) côté client. [!DNL Analytics] utilise ensuite l’instance Visitor pour la synchronisation avec [!DNL Target].

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID and Analytics integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <p>Sample content</p>
  <script src="AppMeasurement.js"></script>
  <script>var s_code=s.t();if(s_code)document.write(s_code);</script>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID and Analytics integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <p>${content}</p>
  <script src="AppMeasurement.js"></script>
  <script>var s_code=s.t();if(s_code)document.write(s_code);</script>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js and AppMeasurement.js are stored in "public" directory
app.use(express.static(__dirname + "/public"));

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

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());

  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const request = {
      execute: {
        mboxes: [{
          address: { url: req.headers.host + req.originalUrl },
          name: "a1-serverside-ab"
        }]
      }};

    try {
      const response = await targetClient.getOffers({ request, visitorCookie, targetCookie });
      sendSuccessResponse(res, response);
    } catch (error) {
      sendErrorResponse(res, error);
    }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB Java ]

```java {line-numbers="true"}
@Controller
public class TargetControllerSample {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/targetAnalytics")
    public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
        Context context = getContext(request);
        Map<String, CustomerState> customerIds = new HashMap<>();
        customerIds.put("userid", CustomerState.authenticated("67312378756723456"));
        customerIds.put("puuid", CustomerState.unknown("550e8400-e29b-41d4-a716-446655440000"));
        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .prefetch(getPrefetchRequest())
                .cookies(getTargetCookies(request.getCookies()))
                .customerIds(customerIds)
                .trackingServer("imsbrims.sc.omtrds.net")
                .build();

        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
        model.addAttribute("visitorState", targetResponse.getVisitorState());
        model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
        setCookies(targetResponse.getCookies(), response);
        return "targetAnalytics";
    }
```

>[!ENDTABS]
