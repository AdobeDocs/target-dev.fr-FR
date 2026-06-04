---
title: Initialisez le SDK Node.js à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Node.js et instancier le client pour effectuer des appels vers  [!DNL Target]  expériences et  [!DNL Adobe Target]  expériences personnalisées.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
TQID: https://experienceleague.adobe.com/uawle0-l5bcv-FuXMLkPc8kIf8DvbkRqAYelr-ehNLk
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 332
ht-degree: 18%

---

# Initialiser le SDK Node.js

## Description

Utilisez la méthode `create` afin d’initialiser le SDK Node.js et d’instancier le client [!UICONTROL Target] pour effectuer des appels vers [!DNL Adobe Target] afin d’obtenir des expériences et des expériences personnalisées.

## Méthode

**créer**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Paramètres

`options` présente la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| client | Chaîne | Oui | None | [!UICONTROL Identifiant client ] |
| organizationId | Chaîne | Oui | None | [!UICONTROL ID d’organisation Experience Cloud] |
| environnement | Chaîne | Non | production | Nom de l’environnement cible. Dans l’interface utilisateur de [!DNL Target], [!UICONTROL Administration] > [!UICONTROL Environnements]. |
| timeout | Nombre | Non | 3000 | Timeout en millisecondes |
| serverDomain | Chaîne | Non | `*client*.tt.omtrdc.net` | Remplace le nom d’hôte par défaut |
| sécuriser | Booléen | Non | true | Annuler l’application du schéma HTTP |
| bûcheron | Objet | Non | Enregistreur NOOP | Remplace l’enregistreur NOOP par défaut |
| targetLocationHint | Chaîne | Non | None | Indicateur d’emplacement cible |
| fetchApi | Fonction | Non | global.fetch ou window.fetch | [fetch](https://fetch.spec.whatwg.org/) est utilisé par le SDK pour les requêtes http. Par défaut, la récupération des nœuds ou l’implémentation du navigateur de la récupération est utilisée. Mais une autre implémentation peut être fournie à l’aide de `fetchApi` |
| propertyToken | Chaîne | Non | None | **Jeton de propriété cible**. S’il est spécifié ici, tous les appels `getOffers` utiliseront cette valeur. **Pour la prise de décision sur l’appareil**, le SDK télécharge uniquement l’artefact qui contient les activités qualifiées pour le jeton de propriété défini dans `propertyToken` |
| decisioningMethod | Chaîne | Non | côté serveur | Détermine la méthode de prise de décision à utiliser ([sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), côté serveur, hybride). |
| pollingInterval | Nombre | Non | 300000 (5 minutes) | Intervalle d’interrogation de l’artefact [règle de prise de décision sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (en millisecondes) |
| artifactLocation | Chaîne | Non | None | Une URL complète vers l’artefact de règle de prise de décision [ sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Il remplace l’emplacement déterminé en interne. |
| artifactPayload | Objet | Non | None | Payload JSON de l’artefact de règle de prise de décision [sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Si spécifié, il est utilisé au lieu d’en demander un à partir d’une URL. |
| [events](sdk-events.md) | Object&lt;String,Function> | Non | None | Objet facultatif avec clés de nom d’événement et valeurs de fonction de rappel |
| telemetryEnabled | Booléen | Non | true | Lorsqu’il est activé, Adobe collecte des données télémétriques sur l’utilisation des fonctionnalités et les performances de SDK. Les données personnelles ne sont pas collectées. |

## Exemple

### Node.js

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    events: {clientReady: targetClientReady }
};

const targetClient = TargetClient.create(CONFIG);

function targetClientReady() {
    // make calls to Adobe Target
}
```
