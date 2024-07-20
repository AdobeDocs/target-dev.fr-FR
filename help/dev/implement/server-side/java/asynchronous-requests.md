---
title: Utilisation de requêtes asynchrones dans le kit SDK  [!DNL Adobe Target] Java
description: Découvrez comment le SDK Java  [!DNL Target] prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Requêtes asynchrones (Java)

## Description

L’un des avantages de l’intégration côté serveur est que vous pouvez exploiter l’énorme bande passante et les ressources informatiques disponibles côté serveur en utilisant le parallélisme. [!DNL Target] Le SDK Java prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.

## Méthodes prises en charge

### Méthodes

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Exemple

Voici un exemple de contrôleur d’application `Spring` :

### Sample Controller

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

Cet exemple suppose que vous avez [initialisé le SDK](initialize-sdk.md) en tant que bean printemps et que vous disposez des [méthodes d’utilitaire](utility-methods.md).

La requête [!DNL Target] est déclenchée avant `simulateIO` et au moment de son exécution, le résultat cible doit également être prêt. Même si ce n&#39;est pas le cas, vous allez réaliser des économies importantes dans la plupart des cas.
