---
title: Présentation de l’API d’administration Adobe Target
description: Vue d’ensemble du  [!DNL Adobe Target Admin API]
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/pJIaDbvs5sAFD8KPsnaNAMQAoq-lowmLs-B0zRAGzDY
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1400
ht-degree: 2%

---

# Présentation de l’API d’administration Target

Cet article présente les informations générales nécessaires pour comprendre et utiliser les [!DNL Adobe Target Admin API] avec succès. Le contenu suivant suppose que vous comprenez comment [configurer l’authentification](../configure-authentication.md) pour les [!DNL Adobe Target Admin API] .

>[!NOTE]
>
>Si vous souhaitez administrer [!DNL Target] via l’interface utilisateur, consultez la section [ administration du *Guide du professionnel Adobe Target*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).
>
>Les API Admin et Profile sont souvent désignées collectivement (« API Admin et Profile »), mais peuvent également être désignées séparément (« API Admin » et « API Profile »). L’API Recommendations est une implémentation spécifique d’une API d’administration [!DNL Target].

## Avant de commencer

Dans tous les exemples de code fournis pour les [API d’administration](../../administer/admin-api/admin-api-overview-new.md), remplacez {tenant} par votre valeur client, `your-bearer-token` par le jeton d’accès que vous générez avec votre JWT et `your-api-key` par votre clé API provenant de [Adobe Developer Console](https://developer.adobe.com/console/home). Pour plus d’informations sur les clients et les JWT, consultez l’article sur la [configuration de l’authentification](../configure-authentication.md) pour les API d’administration [!DNL Target] d’Adobe.

## Contrôle de version

Toutes les API sont associées à une version . Il est important de fournir la version appropriée de l’API que vous souhaitez utiliser.

Si la requête contient une payload (POST ou PUT), l’en-tête `Content-Type` de la requête est utilisé pour spécifier la version.

Si la requête ne contient pas de payload (GET, DELETE ou OPTIONS), l’en-tête `Accept` est utilisé pour spécifier la version.

Si aucune version n’est fournie, l’appel est défini par défaut sur V1 (application/vnd.adobe.target.v1+json).

>[!NOTE]
>
>Si la version correcte n’est pas spécifiée (par exemple, si vous utilisez une payload V2 mais que vous ne spécifiez pas l’en-tête Type de contenu ), l’API répond avec une erreur non prise en charge si l’API n’est pas rétrocompatible.

Message d’erreur concernant les fonctionnalités non prises en charge

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

Admin Postman Collection

Postman est une application qui facilite le déclenchement des appels API. Cette [collection Postman de l’API Target Admin](https://developers.adobetarget.com/api/#admin-postman-collection) contient tous les appels de l’API Target Admin qui nécessitent une authentification à l’aide des activités, audiences, offres, rapports, mbox et environnements

## Codes de réponse

Voici les codes de réponse courants pour les API Target Admin.

| État | Signification | Description |
| --- | --- | --- |
| 200 | [ OK ](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | OK |
| 400 | [Requête incorrecte](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | Requête incorrecte. Les données fournies dans la requête ne sont probablement pas valides. |
| 401 | [Non Autorisé](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | L’utilisateur n’est pas autorisé à effectuer cette opération. |
| 403 | [Interdit](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | L’accès à cette ressource est interdit. |
| 404 | [ Introuvable ](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | La ressource référencée est introuvable. |

## Activités

Une activité vous permet de tester ou de personnaliser du contenu pour vos utilisateurs et utilisatrices. Les activités peuvent être de l’un des types suivants :

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Ciblage d’expérience (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html)
* [Recommandations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html)
* [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Test multivarié (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)

## Mises à jour par lots

Plusieurs API d’administration peuvent être exécutées en tant que requête par lots unique.

### Exécuter les appels par lots

`POST /{tenant}/target/batch`

Empilez plusieurs appels API ensemble et exécutez-les dans un seul lot.

Le traitement par lots vous permet de transmettre des instructions pour plusieurs opérations dans une seule requête HTTP. Vous pouvez également spécifier des dépendances entre les opérations associées (décrites dans une section ci-dessous). TNT traitera chacune de vos opérations indépendantes (éventuellement en parallèle) et traitera vos opérations dépendantes de manière séquentielle. Une fois toutes les opérations terminées, une réponse consolidée est renvoyée et la connexion HTTP est fermée.

L’API par lot prend en charge un tableau de requêtes HTTP logiques représentées sous la forme de tableaux JSON ; chaque requête comporte une méthode (correspondant à la méthode HTTP GET/PUT/POST/DELETE, etc.), une relativeUrl (la partie de l’URL après admin/rest/), un tableau d’en-têtes facultatifs (correspondant aux en-têtes HTTP) et un corps facultatif (pour les requêtes POST et PUT). L’API Batch renvoie un tableau de réponses HTTP logiques représentées sous la forme de tableaux JSON - chaque réponse comporte un code d’état, un tableau d’en-têtes facultatifs et un corps facultatif (qui est une chaîne codée JSON). Pour effectuer des requêtes par lots, créez un objet JSON qui décrit chaque opération individuelle à effectuer. Le nombre maximal d’opérations autorisées est de 256 (de 0 à 255).

Spécification de dépendances entre les opérations de la requête Par défaut, les opérations spécifiées dans la requête d’API par lots sont indépendantes : elles peuvent être exécutées dans un ordre arbitraire sur le serveur et une erreur dans une opération n’affecte pas l’exécution d’autres opérations.

Souvent, les opérations de la requête sont dépendantes ; par exemple, la sortie d’une opération peut être utilisée en entrée de l’opération suivante. Par exemple, l’offre créée dans operationId=0 doit être utilisée dans operationId=1 de création de campagne.

Pour lier deux opérations par lots, spécifiez dans l’opération dépendante l’identifiant de l’opération requise, par exemple : « dependanceOnOperationId » : 5. En outre, les identifiants des ressources créées via des requêtes POST d’opérations par lots peuvent être utilisés dans des opérations dépendantes dans « relativeUrl » et « body ».

#### Autorisations et limitation

Pour exécuter des actions d’API par lot, l’utilisateur sous-jacent doit au moins disposer des droits d’« éditeur » (pour chaque opération individuelle, si des droits supplémentaires sont requis, et non l’utilisateur lui-même, l’opération individuelle échoue). Les stratégies de limitation habituelles sont appliquées aux actions de l’API par lots comme si chaque opération avait été effectuée individuellement.

Le traitement par lots se termine lorsque toutes les opérations sont terminées, une opération peut être réussie (code d’état 2xx), en échec (code d’état 4xx, 5xx) ou ignorée, car une opération de dépendance a échoué ou a été ignorée.

#### Paramètres d&#39;objet de demande

| Attribut | Description | Limites | Par défaut |
| --- | --- | --- | --- |
| corps | corps pour l’opération HTTP par lots. sera ignoré pour toutes les actions, à l’exception des actions POST et PUT. peuvent faire référence aux identifiants d’actions par lots précédentes, par exemple : « offerId » : « {operationIdResponse:0} », « segmentId » : « {operationIdResponse:1} » | doit être un JSON valide. Dans le cas du référencement d’un operationIdResponse, la réponse operationId référencée doit être un ID valide et la méthode sur cette action doit être POST. | objet vide {} |
| dependanceOperationIds | liste des identifiants de contrainte qui garantissent que l&#39;opération en cours ne s&#39;exécutera que si les opérations spécifiées sont terminées avec succès. Peut être utilisé pour réaliser un chaînage d’opérations. | 255 opérations au maximum sont autorisées ; les valeurs uniques ne sont autorisées que ; elles doivent pointer vers un operationId valide dans le tableau ; les dépendances cycliques ne sont pas autorisées |  |
| en-têtes | tableau des en-têtes clé-valeur à envoyer avec une opération particulière. Si l’authentification pour l’API par lots a été effectuée via l’en-tête d’autorisation , elle sera également copiée pour les opérations individuelles. | le nombre maximal d’en-têtes dans le tableau autorisé est de 50 | Type de contenu : application/json |
| headers->name | nom de l’en-tête | doit être unique parmi les autres noms d’en-tête. les en-têtes ne respectent pas la casse définie par rfc, sinon les valeurs se remplacent les unes les autres. |  |
| headers->value | valeur de l’en-tête | S.O. | chaîne vide |
| method | Méthode HTTP à utiliser. Options disponibles : GET, POST, PUT, PATCH, DELETE | seules les méthodes GET, POST, PUT, PATCH et DELETE sont autorisées. |  |
| operationId | Identifiant d’opération utilisé pour identifier une opération parmi d’autres opérations pour les réponses et le référencement des résultats. | unique parmi d’autres opérations ; valeurs comprises entre 0 et 255 |  |
| opérations | liste des opérations à effectuer dans un lot. l’ordre n’est pas pertinent. | 256 opérations maximum sont autorisées |  |
| relativeUrl | URL relative pour l’API REST d’administration, la partie après « /admin/rest/ ». Peut contenir des paramètres de chaîne de requête tels que : « /v2/campaigns?limit=10&amp;offset=10 ». peut se référer à des URL avec des ID provenant d’actions par lots précédentes, par exemple : « /v1/offers/{operationIdResponse:0} ». Si des paramètres de requête sont envoyés, ils doivent être encodés en URL. | doit commencer par / (être relatif) ; seules les nouvelles API JSON valides sont prises en charge ; en cas d’URL relativeURL non valide, une réponse 404 pour une opération particulière est renvoyée ; en cas de référencement d’une operationIdResponse, la réponse operationId référencée doit être un identifiant valide et la méthode sur cette action doit être POST |  |

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

#### Paramètres de l’objet de réponse

| Paramètre | Description |
| --- | --- |
| operationId | Identifiant d’opération utilisé pour identifier une opération parmi d’autres opérations, identique à l’identifiant qui lui a été envoyé dans la requête POST. |
| ignoré | indicateur booléen pour indiquer si l’opération a été exécutée ou ignorée. Sera « true » si l’opération actuelle dépend d’une opération qui a échoué (a renvoyé une valeur statusCode différente de 2xx). |
| statusCode | renvoyé, puis toutes les opérations dépendantes seront ignorées (non exécutées). |
| en-têtes | tableau d’en-têtes clé-valeur à envoyer en réponse à une opération particulière. |
| headers->name | nom de l’en-tête |
| headers->value | valeur de l’en-tête |
| corps | corps pour l’opération de réponse par lots HTTP |

#### Exemple d’objet de réponse

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
