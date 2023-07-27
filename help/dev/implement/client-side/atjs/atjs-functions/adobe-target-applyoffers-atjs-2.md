---
keywords: adobe.target.applyOffers, applyOffers, appliquer des offres, at.js, fonctions, fonction,
description: Utilisez la variable [!UICONTROL adobe.target.applyOffers()] pour la fonction [!DNL Adobe Target] Bibliothèque JavaScript at.js pour appliquer plusieurs offres dans la réponse. (at.js 2.x)
title: Comment utiliser la variable [!UICONTROL adobe.target.applyOffers()] Fonction ?
feature: at.js
exl-id: c391e3f4-fdf1-4e33-8dcb-6bf46e390538
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 85%

---

# [!UICONTROL adobe.target.applyOffers(options)] - at.js 2.x

Cette fonction vous permet d’appliquer plusieurs offres récupérées par `adobe.target.getOffers()`.

>[!NOTE]
>
>Cette fonction a été introduite avec at.js 2.*x*. Cette fonction n’est pas disponible pour at.js version 1.*x*.

| Clé | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| selector | Chaîne | Non | Élément HTML ou sélecteur CSS utilisé pour identifier l’élément HTML dans lequel [!DNL Target] doit placer le contenu de l’offre. Si aucun sélecteur n’est fourni, [!DNL Target] suppose que l’élément de HTML à utiliser est HTML HEAD. |
| Réponse | Objet | Oui | Objet réponse de `getOffers()`.<br />Voir Requêtes ci-dessous. |

## Réponse

>[!NOTE]
>
>Consultez la [Documentation de l’API de diffusion](/help/dev/implement/delivery-api/overview.md) pour plus d’informations sur les types acceptables pour tous les champs répertoriés ci-dessous.

| Nom du champ | Description |
| --- | --- |
| réponse > prérécupérer > vues > options > contenu | Notez que le contenu de l’« option » n’est pas bien défini et dépend directement de la structure du type/modèle d’option. |
| réponse > prérécupérer > vues > options > type | Type d’option. Reflète le type de champ « contenu ». Le type pris en charge est Actions. |
| réponse > prérécupérer > vues > état | Jeton d’état d’affichage opaque qui doit être transféré avec une notification d’affichage pour la vue |
| réponse > prérécupérer > vues > options > jetonsderéponse | Contient le mappage de `responseTokens` qui a été collecté lorsque l’option actuelle était en cours de traitement. |
| réponse > prérécupérer > vues > analytics > charge utile | [!DNL Analytics]Charge utile pour l’intégration côté client qui doit être envoyée à après l’application de la vue.[!DNL Analytics] |
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
| réponse > exécuter > mbox > mbox > analytics > charge | [!DNL Analytics]Charge pour l’intégration côté client, qui doit être envoyée à après l’application de la mbox. [!DNL Analytics] (Voir la section Campagnes compatibles avec A4T). |
| réponse > exécuter > mbox | Liste des mbox exécutées. |
| réponse > exécuter > pageLoad > options > contenu | Notez que le contenu de l’« option » n’est pas bien défini et dépend directement de la structure du type/modèle d’option. |
| réponse > exécuter > pageLoad > options > type | Type d’option. Reflète le type de champ « contenu ». Les types pris en charge sont : html, rediriger, JSON, dynamique et actions. |
| réponse > exécuter > pageLoad > options | Options qui ne sont pas regroupées par affichage (target-global-mbox + options issues d’activités dont les vues ne sont pas regroupées par affichage). |
| réponse > exécuter > pageLoad > mesures | Cliquez sur les mesures qui n’ont pas été définies pour appartenir à une vue spécifique. |
| réponse > exécuter > pageLoad > suivi | Objet contenant toutes les données de suivi pour la requête pageLoad. |
| réponse > exécuter > pageLoad > analytics > charge | [!DNL Analytics]Charge pour l’intégration côté client, qui doit être envoyée à après application du contenu de chargement de la page. [!DNL Analytics] (Voir la section Campagnes compatibles avec A4T). |

## Exemple [!UICONTROL applyOffers()] appel

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

## Exemples d’appels de promesse liés à `[!UICONTROL getOffers()]` et `[!UICONTROL applyOffers()]`, car ces fonctions sont basées sur les promesses.

```javascript {line-numbers="true"}
adobe.target.getOffers({...})
.then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```

Pour plus d’exemples sur l’utilisation de getOffers(), reportez-vous à getOffers . [documentation](adobe-target-getoffers-atjs-2.md)

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
