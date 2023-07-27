---
title: Exécution de tests de fonctionnalités avec des attributs
description: Exécution de tests de fonctionnalités avec des attributs
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Exécution de tests de fonctionnalités avec des attributs

## Résumé des étapes

1. Activer [!UICONTROL prise de décision sur appareil] pour votre organisation
1. Créez un [!UICONTROL Test A/B] activité
1. Définissez vos A et B
1. Ajout d’une audience
1. Définition de l’affectation du trafic
1. Définir la distribution du trafic sur les variations
1. Configuration de la création de rapports
1. Ajout de mesures pour le suivi des indicateurs clés de performance
1. Mise en oeuvre du code pour exécuter des tests de fonctionnalités avec des attributs
1. Mise en oeuvre du code pour suivre les événements de conversion
1. Activation des tests de fonctionnalités avec des attributs

>[!NOTE]
>
>Supposons que vous soyez une société de commerce électronique au détail. Vous souhaitez augmenter le taux de conversion lorsque les clients parcourent votre catalogue de produits et le trient. Vous avez l’hypothèse que certains algorithmes de tri et stratégies de pagination donnent de meilleurs résultats que d’autres. Pour tester cette théorie, vous décidez d’exécuter un test de fonctionnalité qui implique la reconception du widget de tri à l’aide de différentes options de tri pour vos utilisateurs finaux. Vous souhaitez vous assurer que ce test de fonctionnalité est exécuté à une latence proche de zéro afin qu’il n’ait pas d’incidence négative sur les expériences utilisateur et n’ajuste pas les résultats.

## 1. Activez [!UICONTROL prise de décision sur appareil] pour votre organisation

L’activation de la prise de décision sur l’appareil garantit qu’une activité A/B est exécutée à une latence proche de zéro. Pour activer cette fonction, accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]** in [!DNL Adobe Target], puis activez la variable **[!UICONTROL Prise de décision sur appareil]** bascule.

![image alternative](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Vous devez avoir l’administrateur ou l’approbateur [rôle utilisateur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) pour activer ou désactiver la fonction **[!UICONTROL Prise de décision sur appareil]** bascule.

Après avoir activé la variable **[!UICONTROL Prise de décision sur appareil]** basculer, [!DNL Adobe Target] commence à générer *artefacts de règle* pour votre client.

## 2. Créez une [!UICONTROL Test A/B] activité

1. Dans [!DNL Adobe Target], accédez à la **[!UICONTROL Activités]** page, puis sélectionnez **[!UICONTROL Créer une activité]** > **[!UICONTROL Test A/B]**.

   ![image alternative](assets/asset-ab.png)

1. Dans le **[!UICONTROL Créer une activité de test A/B]** modale, conservez la valeur par défaut **[!UICONTROL Web]** option sélectionnée (1), sélectionnez **[!UICONTROL Formulaire]** en tant que compositeur d’expérience (2), sélectionnez **[!UICONTROL Espace de travail par défaut]** avec **[!UICONTROL Aucune restriction de propriété]** (3), puis cliquez sur **[!UICONTROL Suivant]** (4).

   ![image alternative](assets/asset-form.png)

## 3. Définissez vos A et B

1. Dans le **[!UICONTROL Expériences]** étape de création de l’activité, attribuez un nom à votre activité (1) et ajoutez une deuxième expérience, l’expérience B, en cliquant sur l’option **[!UICONTROL Ajouter une expérience]** (2). Saisissez le nom de l’emplacement (3) dans votre application où vous souhaitez exécuter votre test de fonctionnalité avec des attributs. Dans l’exemple ci-dessous, `product-results-page` est l’emplacement défini pour l’expérience A. (Il s’agit également de l’emplacement défini pour l’expérience B.)

   ![image alternative](assets/asset-location.png)

   **[!UICONTROL Expérience A]** contiendra le fichier JSON qui signale à votre logique métier d’effectuer les opérations suivantes :

   * Lancez la fonction de l’algorithme de tri via le `test_sorting` indicateur de fonctionnalité
   * Exécutez l’algorithme de tri recommandé défini dans la variable `sorting_algorithm _**_attribute`
   * Renvoie 50 produits par page, tels que définis par la stratégie de pagination définie dans la variable `pagination_limit`

1. Dans l’expérience A, cliquez sur pour modifier le contenu de **[!UICONTROL Contenu par défaut]** au fichier JSON en sélectionnant **[!UICONTROL Création d’une offre JSON]** comme illustré ci-dessous (1).

   ![image alternative](assets/asset-offer.png)

1. Définition du fichier JSON avec `test_sorting`, `sorting_algorithm`, et `pagination_limit` indicateurs et attributs qui seront utilisés pour lancer l’algorithme de tri recommandé avec une limite de pagination de 50 produits.

   >[!NOTE]
   >
   >When [!DNL Adobe Target] regroupe un utilisateur pour afficher l’expérience A. Le fichier JSON avec les attributs définis dans l’exemple est renvoyé. Dans votre code, vous devez vérifier la valeur de l’indicateur de fonctionnalité. `test_sorting` pour déterminer si la fonction de tri doit être activée. Si tel est le cas, vous utiliserez la valeur recommandée de la variable `sorting_algorithm` pour afficher les produits recommandés dans la vue de liste de produits. La limite des produits à afficher pour votre application est de 50, car il s’agit de la valeur de la variable `pagination_limit` attribut.

   ![image alternative](assets/asset-sorting.png)

   **[!UICONTROL Expérience B]** définit le fichier JSON qui signale à votre logique métier les actions suivantes :

   * Lancement de la fonction d’algorithme de tri à l’aide de l’indicateur de fonction test_sorting
   * Exécutez le `best_sellers` algorithme de tri défini dans `sorting_algorithm _**_attribute`
   * Renvoie 50 produits par page, tels que définis par la stratégie de pagination définie dans la variable `pagination_limit`

   >[!NOTE]
   >
   >When [!DNL Adobe Target] Regroupe un utilisateur pour afficher l’expérience B, le fichier JSON avec les attributs définis dans l’exemple est renvoyé. Dans votre code, vous devez vérifier la valeur de l’indicateur de fonctionnalité. `test_sorting` pour déterminer si la fonction de tri doit être activée. Si tel est le cas, vous utiliserez la variable `best_sellers` de la variable `sorting_algorithm` pour afficher les produits les plus vendus dans la vue de liste de produits. La limite des produits à afficher pour votre application est de 50, car il s’agit de la valeur de la variable `pagination_limit` attribut.

   ![image alternative](assets/asset-sorting-b.png)

## 4. Ajout d’une audience

Dans le **[!UICONTROL Ciblage]** , conservez la variable **[!UICONTROL Tous les visiteurs]** audience. Cela vous permettra de comprendre l’impact de votre fonction de tri, ainsi que l’algorithme et le nombre d’éléments qui influencent le mieux les résultats.

![image alternative](assets/asset-audience-b.png)

## 5. Définition de l’affectation du trafic

Définissez le pourcentage de vos visiteurs par rapport auquel vous souhaitez tester vos algorithmes de tri et votre stratégie de pagination. En d’autres termes, à quel pourcentage de vos utilisateurs souhaitez-vous déployer ce test ? Dans cet exemple, pour déployer ce test sur tous les utilisateurs connectés, conservez l’affectation du trafic à 100 %.

![image alternative](assets/asset-allocation-100.png)

## 6. Définir la distribution du trafic sur des variations

Définissez le pourcentage de vos visiteurs qui verront l’algorithme de tri des meilleurs vendeurs et les recommandations, avec une limite de 50 produits par page. Dans cet exemple, conservez la distribution du trafic sous la forme d’une répartition 50/50 entre les expériences A et B.

![image alternative](assets/asset-variations-50.png)

## 7. Configuration de la création de rapports

Dans le **[!UICONTROL Objectifs et paramètres]** étape, choisissez **[!UICONTROL Adobe Target]** comme la propriété **[!UICONTROL Source de création de rapports]** pour afficher les résultats de votre test A/B dans la variable [!DNL Adobe Target] Interface utilisateur ou choisissez **[!UICONTROL Adobe Analytics]** pour les afficher dans l’interface utilisateur Adobe Analytics.

![image alternative](assets/asset-reporting-b.png)

## 8. Ajout de mesures pour les indicateurs clés de performance de suivi

Choisissez une **[!UICONTROL Mesure de l’objectif]** pour mesurer le test de fonctionnalité avec des attributs. Dans cet exemple, la réussite dépend de l’achat ou non d’un produit par l’utilisateur, selon l’algorithme de tri et la stratégie de pagination affichés.

## 9. Mise en oeuvre de tests de fonctionnalités avec des attributs dans votre application

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["product-results-page"]).then(function(attributes) {
    const test_sorting = attributes.getValue("product-results-page", "test-sorting");
    const sorting_algorithm = attributes.getValue("product-results-page", "sorting_algorithm");
    const pagination_limit = attributes.getValue("product-results-page", "pagination_limit");
  });
}
```

>[!TAB Java ]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("product-results-page").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 10. Implémentez le code pour suivre les événements de conversion.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "product-results-page"
          }
        }
      ]
    }
})
```

>[!TAB Java ]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);

Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 11. Activez vos tests de fonctionnalités avec des attributs.

![image alternative](assets/asset-activate.png)
