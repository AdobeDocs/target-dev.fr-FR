---
title: Initialisation du SDK Node.js à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Node.js et instancier le client  [!DNL Target] pour effectuer des appels à [!DNL Adobe Target] pour des expériences et des expériences personnalisées.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 19%

---

# Initialisation du SDK Node.js

## Description

Utilisez la méthode `create` pour initialiser le SDK Node.js et instancier le client [!UICONTROL Target] afin d’effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.

## Méthode

**create**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Paramètres

`options` a la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| client | Chaîne | Oui | None | [!UICONTROL Adobe Target Client ID] |
| organizationId | Chaîne | Oui | None | [!UICONTROL Experience Cloud Organization ID] |
| environnement | Chaîne | Non | production | Nom de l’environnement cible. Dans l’interface utilisateur de [!DNL Target], [!UICONTROL Administration] > [!UICONTROL Environments]. |
| timeout | Nombre | Non | 3000 | Timeout en millisecondes |
| serverDomain | Chaîne | Non | `*client*.tt.omtrdc.net` | Remplace le nom d’hôte par défaut |
| secure | Booléen | Non | true | Non défini pour appliquer le schéma HTTP |
| logger | Objet | Non | Enregistreur NOOP | Remplace le journal par défaut NOOP |
| targetLocationHint | Chaîne | Non | None | Conseil sur l’emplacement cible |
| fetchApi | Fonction | Non | global.fetch ou window.fetch | [fetch](https://fetch.spec.whatwg.org/) est utilisé par le SDK pour les requêtes http. Par défaut, node-fetch ou l’implémentation de la récupération dans le navigateur est utilisée. Mais une autre implémentation peut être fournie en utilisant `fetchApi` |
| propertyToken | Chaîne | Non | None | **Jeton de propriété Target**. Si spécifié ici, tous les appels `getOffers` utiliseront cette valeur. **Pour la prise de décision sur l’appareil**, le SDK ne télécharge que l’artefact qui contient les activités qualifiées pour le jeu de jetons de propriété dans `propertyToken` |
| decisioningMethod | Chaîne | Non | côté serveur | Détermine la méthode de prise de décision à utiliser ([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), côté serveur, hybride) |
| pollingInterval | Nombre | Non | 300000 (5 minutes) | Intervalle d’interrogation de l’[ artefact de règle de prise de décision sur l’appareil ](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (en millisecondes) |
| artifactLocation | Chaîne | Non | None | URL complète à l’artefact de règle de prise de décision sur l’appareil [. ](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) Permet de remplacer un emplacement déterminé en interne. |
| artifactPayload | Objet | Non | None | Charge JSON de l’artefact de règle de prise de décision sur l’appareil [. ](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) S’il est spécifié, il est utilisé au lieu d’en demander un à partir d’une URL. |
| [events](sdk-events.md) | Objet&lt;String,Function> | Non | None | Objet facultatif avec clés de nom d’événement et valeurs de fonction de rappel |
| telemetryEnabled | Booléen | Non | true | Lorsqu’il est activé, Adobe collecte les données de télémétrie des performances et de l’utilisation des fonctionnalités du SDK. Les données personnelles ne sont pas collectées. |

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
