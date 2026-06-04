---
title: Utilisation des requêtes asynchrones dans le SDK  [!DNL Adobe Target]  Java
description: Découvrez comment Java SDK prend  [!DNL Target]  charge les requêtes asynchrones, ce qui peut réduire à zéro le temps cible effectif.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
TQID: https://experienceleague.adobe.com/Y9oTl8aU4-4HpMajdmy5KfvAwEFOpV0y9vUg7BdBRk8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 130
ht-degree: 3%

---

# Requêtes Asynchrones (Java)

## Description

L’un des avantages de l’intégration côté serveur est que vous pouvez tirer parti de l’énorme bande passante et des ressources informatiques disponibles côté serveur en utilisant le parallélisme. [!DNL Target] Java SDK prend en charge les requêtes asynchrones, ce qui peut réduire à zéro le temps cible effectif.

## Méthodes prises en charge

### Méthodes

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Exemple

Voici un exemple de contrôleur d’application `Spring` :

### Exemple de contrôleur

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

Cet exemple suppose que vous avez [initialisé le SDK](initialize-sdk.md) en tant que bean printanier et que vous disposez de [méthodes utilitaires](utility-methods.md).

La requête [!DNL Target] est déclenchée avant le `simulateIO` et, au moment de son exécution, le résultat cible doit également être prêt. Même si ce n&#39;est pas le cas, vous aurez des économies importantes dans la plupart des cas.
