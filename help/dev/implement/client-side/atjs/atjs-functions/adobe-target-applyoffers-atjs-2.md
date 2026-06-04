---
keywords: adobe.target.applyOffers, applyOffers, applyoffers, apply offres, at.js, functions, function,
description: Utilisez la fonction [!UICONTROL adobe.target.applyOffers()] pour que la bibliothèque JavaScript at [!DNL Adobe Target] js applique plusieurs offres dans la réponse. (at.js 2.x)
title: Comment utiliser la fonction [!UICONTROL adobe.target.applyOffers()] ?
feature: at.js
exl-id: c391e3f4-fdf1-4e33-8dcb-6bf46e390538
TQID: https://experienceleague.adobe.com/9WIJvPZIlrtLkv-vv-HRkctgwHn3nX-jrE4-4usXW0Y
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 825
ht-degree: 78%

---

# [!UICONTROL adobe.target.applyOffers(options)] - at.js 2.x

Cette fonction vous permet d’appliquer plusieurs offres récupérées par `adobe.target.getOffers()`.

>[!NOTE]
>
>Cette fonction a été introduite avec at.js 2.*x*. Cette fonction n’est pas disponible pour at.js version 1.*x*.

| Clé | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| selector | Chaîne | Non | Élément HTML ou sélecteur CSS utilisé pour identifier l’élément HTML dans lequel [!DNL Target] doit placer le contenu de l’offre. Si aucun sélecteur n’est fourni, [!DNL Target] suppose que l’élément HTML à utiliser est HTML HEAD. |
| Réponse | Objet | Oui | Objet de réponse de `getOffers()`.<br />Voir le tableau Demandes ci-dessous. |

## Réponse

>[!NOTE]
>
>Consultez la [documentation relative à l’API de diffusion](/help/dev/implement/delivery-api/overview.md) pour plus d’informations sur les types acceptables pour tous les champs répertoriés ci-dessous.

| Nom du champ | Description |
| --- | --- |
| réponse > prérécupérer > vues > options > contenu | Notez que le contenu de l’« option » n’est pas bien défini et dépend directement de la structure du type/modèle d’option. |
| réponse > prérécupérer > vues > options > type | Type d’option. Reflète le type de champ « contenu ». Le type pris en charge est Actions. |
| réponse > prérécupérer > vues > état | Jeton d’état d’affichage opaque qui doit être transféré avec une notification d’affichage pour la vue |
| réponse > prérécupérer > vues > options > jetonsderéponse | Contient le mappage de `responseTokens` qui a été collecté lorsque l’option actuelle était en cours de traitement. |
| réponse > prérécupérer > vues > analytics > charge utile | [!DNL Analytics] payload pour l’intégration côté client qui doit être envoyée à [!DNL Analytics] une fois la vue appliquée. |
| réponse > prérécupérer > vues > trace | Objet contenant toutes les données de suivi pour l’appel de prérécupération par affichage.<br />L’objet trace comprend également une version pour la trace.<br />L’objet trace comprend également des détails sur la vue actuelle. |
| réponse > prérécupérer > vues > options > jetonDévénement | La journalisation d’événements est effectuée par option. Pour chaque option appliquée, le jeton d’événement correspondant doit être ajouté à la liste des jetons de notification. Notez qu’une vue est composée de plusieurs options. Si toutes les options ont été appliquées et affichées, toutes `eventTokens` doivent être incluses dans la notification. |
| réponse > prérécupérer > vues > nom | Nom d’affichage lisible. |
| réponse > prérécupérer > vues > mesures | Mesures de création de rapports qui doivent être regardées, puis notifiées [!DNL Target]. Actuellement, il suffit de cliquer sur Mesure pour afficher la mesure. Si un clic sur l’élément se produit, les informations appropriées `eventTokens` doivent être collectées et une notification doit être envoyée. |
| réponse > prérécupérer > vues > clé | Clé ou empreinte digitale qui identifie la vue. |
| réponse > prérécupérer > vues > id | ID de la vue. |
| réponse > notifications > id | Identifiant de notification. |
| réponse > notifications > événements > type | Type de notification, du clic ou de l’affichage. |
| réponse > notifications > événements > trace | Trace de l’événement de notification. |
| réponse > notifications > événements > jeton | Jeton envoyé avec l’événement de notification. |
| réponse > notifications > événements > horodatage | Horodatage envoyé avec l’événement de notification. |
| réponse > notifications > événements > erreurCode | Si la notification a échoué, le code indique la raison de l’échec. |
| réponse > notifications > événements | Événements consignés ou non répertoriés pour la notification actuelle. |
| réponse > notifications | Indique les notifications enregistrées ou non. |
| réponse > exécuter > mbox > mbox > trace | Objet contenant toutes les données de suivi pour la requête de mbox individuelle. |
| réponse > exécuter > mbox > mbox > jetons de réponse | Contient le mappage `responseTokens` pour l’exécution spécifique de la requête de mbox. |
| réponse > exécuter > mbox > mbox > option > contenu | Notez que le contenu de l’« option » n’est pas bien défini et dépend directement de la structure du type/modèle d’option. |
| réponse > exécuter > mbox > mbox > option > type | Type d’option. Reflète le type de champ « contenu ». Les types pris en charge sont les suivants : html, redirect, JSON et dynamique. |
| réponse > exécuter > mbox > mbox > options | Option de réponse. |
| réponse > exécuter > mbox > mbox > mesures > eventtoken | Jeton d’événement de clic. |
| réponse > exécuter > mbox > mbox > mesures > type | &quot;click&quot; |
| réponse > exécuter > mbox > mbox > mesures | Contient la liste des mesures `clickThrough`. |
| réponse > exécuter > mbox > mbox > mbox | Nom de la mbox. |
| réponse > exécuter > mbox > mbox > index | Indique que la réponse est destinée à la mbox avec cet index de la requête. |
| réponse > exécuter > mbox > mbox > analytics > charge | [!DNL Analytics] payload pour l’intégration côté client qui doit être envoyée à [!DNL Analytics] après l’application de la mbox. (Voir la section Campagnes compatibles avec A4T). |
| réponse > exécuter > mbox | Liste des mbox exécutées. |
| réponse > exécuter > pageLoad > options > contenu | Notez que le contenu de l’« option » n’est pas bien défini et dépend directement de la structure du type/modèle d’option. |
| réponse > exécuter > pageLoad > options > type | Type d’option. Reflète le type de champ « contenu ». Les types pris en charge sont : html, rediriger, JSON, dynamique et actions. |
| réponse > exécuter > pageLoad > options | Options qui ne sont pas regroupées par affichage (target-global-mbox + options issues d’activités dont les vues ne sont pas regroupées par affichage). |
| réponse > exécuter > pageLoad > mesures | Cliquez sur les mesures qui n’ont pas été définies pour appartenir à une vue spécifique. |
| réponse > exécuter > pageLoad > suivi | Objet contenant toutes les données de suivi pour la requête pageLoad. |
| réponse > exécuter > pageLoad > analytics > charge | [!DNL Analytics] payload pour l’intégration côté client qui doit être envoyée à [!DNL Analytics] après l’application du contenu de chargement de la page. (Voir la section Campagnes compatibles avec A4T). |

## Exemple d&#39;appel [!UICONTROL applyOffers()]

```javascript {line-numbers="true"}
adobe.target.applyOffers({response:{
  "execute": {
    "pageLoad": {
      "options": [{
        "type": "html",
        "content": "page-load"
      },
      {
        "type": "actions",
        "content": [{
          "type": "setHtml",
          "content": "<h1>Container 1</h1>",
          "selector": "#container1",
          "cssSelector": "#container1"
        },
        {
          "type": "setHtml",
          "content": "<h3>Container 3</h3>",
          "selector": "#container3",
          "cssSelector": "#container3"
        }]
      }],
 
 
      "metrics": [{
        "type": "click",
        "selector": "#container1",
        "eventToken": "page-load-click-metric" 
      }]
    }
  }
}});
```

## Exemples d&#39;appels de chaînage de promesse avec `[!UICONTROL getOffers()]` et `[!UICONTROL applyOffers()]`, car ces fonctions sont basées sur la promesse

```javascript {line-numbers="true"}
adobe.target.getOffers({...})
.then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```

Pour plus d’exemples sur l’utilisation de getOffers(), reportez-vous à la documentation getOffers [&#128279;](adobe-target-getoffers-atjs-2.md)

### Exemple de requête de chargement de page


```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {}
        }
    }
}).
then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```
