---
keywords: adobe.target.sendNotifications, sendNotifications, sendnotifications, send notifications, notifications, at.js, fonctions, fonction, $9
description: Utilisez [!UICONTROL adobe.target.sendNotifications()] pour at.js afin d’envoyer des notifications à  [!DNL Target]  Edge lorsqu’une expérience est rendue sans utiliser [!UICONTROL applyOffer]​(s). (at.js.2.1 +)
title: Comment utiliser la fonction adobe.target.sendNotifications() ?
feature: at.js
exl-id: 1a08da10-31a0-4b0b-af7d-91ed7d32c308
TQID: https://experienceleague.adobe.com/QprkTK-0WGq-fzJ9e3FUSAZAandaZFiUY62-zQ6ajY8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 642
ht-degree: 83%

---

# [!UICONTROL adobe.target.sendNotifications(options)]

Cette fonction envoie une notification à [!DNL Target] Edge lorsqu’une expérience est rendue sans utiliser de `[!UICONTROL adobe.target.applyOffer()]` ou de `[!UICONTROL adobe.target.applyOffers()]`.

>[!NOTE]
>
>Cette fonction a été introduite dans at.js 2.1.0 et sera disponible pour toutes les versions ultérieures à 2.1.0.

| Clé | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| consumerId | Chaîne | Non | La valeur par défaut est la mbox globale du client si elle n’est pas fournie. Cette clé sert à générer l’identifiant de données supplémentaire utilisé pour l’intégration A4T. |
| Demande | Objet | Oui | Voir Requêtes ci-dessous. |
| timeout | Nombre | Non | Délai d’expiration de requête. Si cette valeur n’est pas spécifiée, c’est le délai d’expiration par défaut d’at.js qui sera utilisé. |

## Demande

| Nom du champ | Type | Obligatoire ? | Limite | Description |
| --- | --- | --- | --- | --- |
| Request > notifications | Tableau d’objets | Oui |  | Notifications pour le contenu affiché, les sélecteurs cliqués et/ou les affichages ou mbox consultés. |
| Request > notifications > address | Objet | Non |  |  |
| Request > notifications > address > url | Chaîne | Non |  | URL à partir de laquelle la notification a été déclenchée. |
| Request > notifications > address > referringUrl | Chaîne | Non |  | URL de référence à partir de laquelle la notification a été déclenchée. |
| Request > notifications > parameters | Chaîne | Non | Les noms suivants ne sont pas autorisés pour les paramètres :<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>Tenez compte des points suivants :<ul><li>Limite de 50 paramètres max.</li><li>Le nom du paramètre ne doit pas être vide.</li><li>Longueur de paramètre 128 max.</li><li>Le nom du paramètre ne doit pas commencer par « profile ».</li><li>Longueur de la valeur du paramètre 5 000 max.</li></ul> |  |
| Request > notifications > profileParameters | Chaîne | Non | Les noms suivants ne sont pas autorisés pour les paramètres :<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>Tenez compte des points suivants :<ul><li>Limite de 50 paramètres max.</li><li>Le nom du paramètre ne doit pas être vide.</li><li>Longueur de paramètre 128 max.</li><li>Le nom du paramètre ne doit pas commencer par « profile ».</li><li>Longueur de la valeur du paramètre 5 000 max.</li></ul> |  |
| Request > notifications > order | Objet | Non |  | Objet décrivant les détails de la commande. |
| Request > notifications > order > id | Chaîne | Non | `<=` 250 caractères. | ID de commande. |
| Request > notifications > order > total | Chaîne | Non | `>=` 0 | Total de la commande. |
| Request > notifications > order > purchasedProductIds | Tableau de chaîne | Non | <ul><li>Aucune valeur vide n’est autorisée.</li><li>Longueur de chaque id de produit 50 max.</li><li>Les ID de produit, séparés par des virgules et concaténées, ne doivent pas dépasser 250.</li></ul> | ID des produits commandés. |
| Request > notifications > product | Objet | Non |  |  |
| Request > notifications > product > id | Chaîne | Non | `<=` 128 caractères ; ne peut pas être vide. | ID de produit. |
| Request > notifications > product > categoryId | Chaîne | Non | `<=` 128 caractères ; ne peut pas être vide. | ID de catégorie |
| Request > notifications > id | Chaîne | Oui | `<=` 200 caractères. | L’ID de notification est renvoyé en réponse et indique que la notification a bien été traitée. |
| Request > notifications > impressionId | Chaîne | Non | `<= 128` caractères. | L’ID d’impression est utilisé pour associer (lier) la notification actuelle à une notification précédente ou à une demande d’exécution. Au cas où ces deux requêtes correspondent, la deuxième requête et les requêtes suivantes ne généreront pas de nouvelle impression pour l’activité ou l’expérience. |
| Request > notifications > type | Chaîne | Oui | « click » ou « display » est pris en charge. | Type de notification. |
| Request > notifications > timestamp | Nombre`<int64>` | Oui |  | Horodatage de la notification en millisecondes écoulées depuis l’époque UNIX considérée. |
| Request > notifications > tokens | Tableau de chaîne | Oui |  | Liste des jetons pour le contenu affiché ou les sélecteurs cliqués, en fonction du type de notification. |
| Request > notifications > mbox | Objet | Non |  | Notifications pour la mbox. |
| Request > notifications > mbox > name | Chaîne | Non | Aucune valeur vide n’est autorisée.<p>Graphiques autorisés : voir la remarque suivant ce tableau. | nom de mbox. |
| Request > notifications > mbox > state | Chaîne | Non |  | jeton d’état de mbox. |
| Request > notifications > view | Objet | Non |  |  |
| Request > notifications > view > id | Entier `<int64>` | Non |  | Id de la vue. ID affecté à la vue lorsque la vue a été créée via l’API d’affichage. |
| Request > notifications > view > name | Chaîne | Non | `<= 128` caractères. | Nom de la vue. |
| Request > notifications > view > key | Chaîne | Non | `<=` 512 caractères. | Clé de la vue. Clé qui a été définie avec la vue via l’API. |
| Request > notifications > view > state | Chaîne | Non |  | jeton d’état de la vue. |

**Remarque** : les caractères suivants ne sont *pas* autorisés pour les `Request > notifications > mbox > name` :

```
- '-, ./=`:;&!@#$%^&*()+|?~[]{}'
```

## Appel sendNotifications() après le rendu des mbox prérécupérées

```javascript {line-numbers="true"}
function createTokens(options) {
  return options.map(e => e.eventToken);
}

function createNotification(mbox, type, tokens) {
  const id = 11111; // here we should use a random ID like UUID
  const timestamp = Date.now();
  const { name, state, parameters, profileParameters, order, product } = mbox;
  const result = {
    id,
    type,
    timestamp,
    parameters,
    profileParameters,
    order,
    product
  };

  result.mbox = { name, state };
  result.tokens = tokens;

  return result;
}

adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "a1-serverside-ab"
        }
      ]
    }
  }
})
.then(response => {
  const mboxes = response.prefetch.mboxes;
  const notifications = mboxes.map(mbox => {
    const type = "display";
    const tokens = createTokens(mbox.options);

    return createNotification(mbox, type, tokens);
  });
  
  adobe.target.sendNotifications({
    request: { notifications }
  });
})
```

>[!NOTE]
>
>Si vous utilisez [!DNL Adobe Analytics], `[!UICONTROL getOffers()]` avec la prérécupération uniquement et `[!UICONTROL sendNotifications()]`, la requête [!DNL Analytics] doit être déclenchée après l’exécution de `[!UICONTROL sendNotifications()]`. L’objectif est de s’assurer que le SDID généré par `[!UICONTROL sendNotifications()]` correspond au SDID envoyé à [!DNL Analytics] et [!DNL Target].


