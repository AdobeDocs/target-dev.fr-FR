---
title: Présentation de l’API d’administration Adobe Target
description: Présentation de  [!DNL Adobe Target Admin API]
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 2%

---

# Présentation de l’API d’administration de Target

Cet article présente un aperçu des informations générales nécessaires pour comprendre et utiliser correctement les [!DNL Adobe Target Admin API]s. Le contenu suivant suppose que vous comprenez comment [configurer l’authentification](../configure-authentication.md) pour les [!DNL Adobe Target Admin API]s.

>[!NOTE]
>
>Si vous souhaitez administrer [!DNL Target] via l’interface utilisateur, reportez-vous à la [section d’administration du *Guide du praticien d’entreprise Adobe Target*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).
>
>Les API d’administration et les API de profil sont souvent appelées collectivement (&quot;API d’administration et de profil&quot;), mais peuvent également être référencées séparément (&quot;API d’administration&quot; et &quot;API de profil&quot;). L’API Recommendations est une implémentation spécifique d’une API d’administration [!DNL Target].

## Avant de commencer

Dans tous les exemples de code fournis pour les [API d&#39;administration](../../administer/admin-api/admin-api-overview-new.md), remplacez {tenant} par la valeur de votre client, `your-bearer-token` par le jeton d&#39;accès que vous générez avec vos JWT et `your-api-key` avec votre clé d&#39;API provenant de [Adobe Developer Console](https://developer.adobe.com/console/home). Pour plus d’informations sur les clients et les JWT, consultez l’article sur la [configuration de l’authentification](../configure-authentication.md) pour les API d’administration d’Adobe [!DNL Target].

## Contrôle de version

Toutes les API sont associées à une version. Il est important de fournir la version appropriée de l’API que vous souhaitez utiliser.

Si la requête contient un payload (POST ou PUT), l’en-tête `Content-Type` de la requête est utilisé pour spécifier la version.

Si la requête ne contient pas de payload (GET, DELETE ou OPTIONS), l’en-tête `Accept` est utilisé pour spécifier la version.

Si aucune version n’est fournie, l’appel est défini par défaut sur V1 (application/vnd.adobe.target.v1+json).

>[!NOTE]
>
>Si la version correcte n’est pas spécifiée (par exemple, si vous utilisez une payload V2 mais ne spécifiez pas l’en-tête Content-Type), l’API répondra avec une erreur non prise en charge si l’API n’est pas rétrocompatible.

Message d’erreur pour les fonctionnalités non prises en charge

```
{
    "httpStatus": 406,
    "requestId": "8752b736-cf71-4d81-86c3-94be2b5ae648",
    "requestTime": "2018-02-02T21:39:06.405Z",
    "errors": [
        {
            "errorCode": "Unsupported.Feature",
            "message": "Unsupported features detected"
        }
    ]
}
```

Collecte Postman d’administration

Postman est une application qui permet de déclencher facilement des appels API. Cette [ collection Postman de l’API d’administration Target ](https://developers.adobetarget.com/api/#admin-postman-collection) contient tous les appels de l’API d’administration Target qui nécessitent une authentification à l’aide des activités, audiences, offres, rapports, mbox et environnements.

## Codes de réponse

Voici les codes de réponse courants pour les API d’administration Target.

| État | Signification | Description |
| --- | --- | --- |
| 200 | [OK](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | OK |  |
| 400 | [Requête incorrecte](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | Requête incorrecte. Il est probable que les données fournies dans la requête ne soient pas valides. |  |
| 401 | [Non autorisé](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | L’utilisateur n’est pas autorisé à effectuer cette opération. |  |
| 403 | [Forbidden](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | L&#39;accès à cette ressource est interdit. |  |
| 404 | [Introuvable](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | La ressource référencée est introuvable. |  |

## Activités

Une activité vous permet de tester ou de personnaliser du contenu pour vos utilisateurs. Les activités peuvent être de l’un des types suivants :

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Ciblage d’expérience (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html)
* [Recommendations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html)
* [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Test multivarié (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)

## Mises à jour par lots

Plusieurs API d’administration peuvent être exécutées en tant que requête de lot unique.

### Exécution des appels par lot

`POST /{tenant}/target/batch`

Empilez plusieurs appels d’API ensemble et exécutez-les dans un seul lot.

Le traitement par lot vous permet de transmettre des instructions pour plusieurs opérations dans une seule requête HTTP. Vous pouvez également spécifier des dépendances entre les opérations associées (décrites dans une section ci-dessous). TNT traitera chacune de vos opérations indépendantes (éventuellement en parallèle) et traitera vos opérations dépendantes de manière séquentielle. Une fois toutes les opérations terminées, une réponse consolidée est renvoyée et la connexion HTTP est fermée.

L’API de lot accepte un tableau de requêtes HTTP logiques représentées sous la forme de tableaux JSON : chaque requête comporte une méthode (correspondant à la méthode HTTP GET/PUT/POST/DELETE, etc.), une valeur relativeUrl (la partie de l’URL après admin/rest/), un tableau d’en-têtes facultatifs (correspondant aux en-têtes HTTP) et un corps facultatif (pour les requêtes de POST et de PUT). L’API de lot renvoie un tableau de réponses HTTP logiques représentées sous la forme de tableaux JSON : chaque réponse comporte un code d’état, un tableau d’en-têtes facultatif et un corps facultatif (qui est une chaîne codée au format JSON). Pour effectuer des requêtes par lot, créez un objet JSON qui décrit chaque opération à effectuer. Le nombre maximal d’opérations autorisées est de 256 (de 0 à 255).

Spécification des dépendances entre les opérations dans la requête Par défaut, les opérations spécifiées dans la requête de l’API de lot sont indépendantes : elles peuvent être exécutées dans un ordre arbitraire sur le serveur et une erreur dans une opération n’a aucune incidence sur l’exécution d’autres opérations.

Souvent, les opérations de la requête dépendent ; par exemple, la sortie d’une opération peut être utilisée dans l’entrée de l’opération suivante. Par exemple, l’offre créée dans operationId=0 doit être utilisée dans operationId=1 de création de campagne.

Afin de lier deux opérations par lots ensemble, spécifiez dans l’opération dépendante l’identifiant de l’opération requise, par exemple : &quot;dépendOnOperationId&quot; : 5. En outre, les identifiants des ressources créées via les demandes POST d’opérations par lots peuvent être utilisés dans des opérations dépendantes à la fois dans &quot;relativeUrl&quot; et &quot;body&quot;.

#### Autorisations et limitation

Pour exécuter des actions d’API par lot, l’utilisateur sous-jacent doit disposer au moins des droits &quot;d’éditeur&quot; (pour chaque opération individuelle, au cas où des droits supplémentaires seraient requis par rapport à l’utilisateur, l’opération individuelle échouera). Les stratégies de ralentissement classiques sont appliquées aux actions de l’API de lot comme si chaque opération avait été effectuée individuellement.

Le traitement par lots se termine une fois toutes les opérations terminées, une opération peut être une réussite (2xx statusCode), un échec (4xx, 5xx status code) ou une saut en raison d’un échec ou d’une saut d’une opération de dépendance.

#### Paramètres de l’objet de requête

| Attribut | Description | Limites | Par défaut |
| --- | --- | --- | --- |
| corps | corps pour l’opération de lot HTTP. seront ignorés pour toutes les actions, à l’exception de POST et de PUT. peut faire référence aux identifiants des actions par lots précédentes, par exemple : &quot;offerId&quot;: &quot;{operationIdResponse:0}&quot;, &quot;segmentId&quot;: &quot;{operationIdResponse:1}&quot; | doit être un JSON valide ; si vous référencez une operationIdResponse, la réponse operationId référencée doit être un ID valide et la méthode de cette action doit être POST. | objet vide {} |  |
| dependingOnOperationIds | liste des ID de contrainte qui garantissent que l’opération en cours s’exécutera uniquement si les opérations spécifiées sont terminées avec succès. Peuvent être utilisées pour enchaîner les opérations. | 255 opérations au maximum sont autorisées ; les valeurs uniques ne sont autorisées que ; doit pointer vers un operationId valide dans le tableau ; les dépendances cycliques ne sont pas autorisées |  |  |
| en-têtes | tableau d’en-têtes clé-valeur à envoyer avec une opération particulière. Si l’authentification pour l’API de lot a été effectuée via l’en-tête d’autorisation, elle sera également copiée pour des opérations individuelles. | Le nombre maximal d’en-têtes dans le tableau autorisé est de 50. | Content-Type: application/json |  |
| headers->name | nom de l’en-tête | doit être unique parmi d’autres noms d’en-tête. les en-têtes ne sont pas sensibles à la casse par rfc, sinon les valeurs se remplaceront les unes les autres. |  |  |
| headers->value | valeur d’en-tête | S.O. | chaîne vide |  |
| method | méthode HTTP à utiliser. Options disponibles : GET, POST, PUT, PATCH, DELETE | seules les méthodes GET, POST, PUT, PATCH et DELETE sont autorisées |  |  |
| operationId | identifiant d’opération utilisé pour identifier une opération parmi d’autres opérations pour les réponses et le référencement des résultats. | unique parmi d’autres opérations ; valeurs comprises entre 0 et 255 |  |  |
| opérations | liste des opérations à effectuer dans un lot. l’ordre n’est pas pertinent. | 256 opérations au maximum sont autorisées |  |  |
| relativeUrl | URL relative de l’API de repos de l’administrateur, partie après &quot;/admin/rest/&quot;. Peut contenir des paramètres de chaîne de requête tels que : &quot;/v2/campaigns?limit=10&amp;offset=10&quot;. peut faire référence aux URL contenant des identifiants provenant d’actions par lots précédentes, par exemple : &quot;/v1/offer/{operationIdResponse:0}&quot;. Si des paramètres de requête sont envoyés, ils doivent être codés en URL. | doit commencer par / (être relatif) ; seules les nouvelles API JSON valides sont prises en charge ; en cas d’URL relative non valide, une réponse 404 pour une opération particulière est renvoyée ; en cas de référencement d’une operationIdResponse, la réponse operationId référencée doit être un ID valide et la méthode de cette action doit être POST. |  |  |

#### Exemple d’objet de requête

```
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}
```

#### Paramètres d’objet de réponse

| Paramètre | Description |
| --- | --- |
| operationId | identifiant d’opération utilisé pour identifier une opération parmi d’autres opérations, même identifiant qu’il a été envoyé dans une demande de POST. |  |
| ignoré | indicateur boolean pour marquer si l’opération a été exécutée ou ignorée. Est définie sur true si l’opération en cours dépend d’une opération qui a échoué (a renvoyé une valeur statusCode différente de 2xx). |  |
| statusCode | renvoyée, alors toutes les opérations dépendantes seront ignorées (non exécutées). |  |
| en-têtes | tableau d’en-têtes clé-valeur à envoyer en tant que réponse pour une opération particulière. |  |
| headers->name | nom de l’en-tête |  |
| headers->value | valeur d’en-tête |  |
| corps | corps de l’opération de réponse par lots HTTP |  |

#### Exemple d’objet Response

```
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}
```
