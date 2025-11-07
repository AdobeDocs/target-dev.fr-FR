---
title: Initialisez le SDK Python à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Python et instancier le [!UICONTROL TargetClient] pour effectuer des appels vers  [!DNL Adobe Target]  expériences et des expériences personnalisées.
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 17%

---

# Initialiser le SDK Python

Description
Utilisez la méthode `create` afin d’initialiser le SDK Python et d’instancier le [!UICONTROL Target Client] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.

## Méthode

### créer

```python {line-numbers="true"}
TargetClient.create(options)
```

## Paramètres

`options` présente la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| client | str | Oui | None | [!UICONTROL Adobe Target client ID] |
| organization_id | str | Oui | None | [!UICONTROL Experience Cloud Organization ID] |
| timeout | int | Non | 3000 | Timeout en millisecondes |
| server_domain | str | Non | `client.tt.omtrdc.net` | Remplace le nom d’hôte par défaut |
| sécuriser | booléen | Non | true | Annuler l’application du schéma HTTP |
| bûcheron | objet | Non | ENREGISTREUR D’INFORMATIONS | Remplace la journalisation INFO par défaut |
| target_location_hint | str | Non | None | [!DNL Target] l’indicateur d’emplacement |
| property_token | str | Non | None | Jeton de propriété [!DNL Target]. Si spécifié ici, tous les appels get_offers utiliseront cette valeur. |
| decisioning_method | str | Non | côté serveur | Détermine la méthode de prise de décision à utiliser ([sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), côté serveur, hybride). |
| polling_interval | int | Non | 300000 (5 minutes) | Intervalle d’interrogation pour l’artefact de règle de prise de décision [sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (en ms) |
| artifact_location | str | Non | None | Une URL complète vers l’artefact de règle de prise de décision [ sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Il remplace l’emplacement déterminé en interne. |
| artifact_payload | objet | Non | None | Payload JSON de l’artefact de règle de prise de décision [sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Si spécifié, il est utilisé au lieu d’en demander un à partir d’une URL. |
| [events](sdk-events.md) | dict &lt;str, callable> | Non | None | Objet facultatif avec clés de nom d’événement et valeurs de fonction de rappel |
| environment_id | int | Non | production | L’identifiant d’environnement [!DNL Target] |
| environnement | str | Non | production | Nom de l’environnement [!DNL Target] |
| cdn_environment | str | Non | production | Nom de l’environnement CDN |
| telemetry_enabled | booléen | Non | True | Si elle est définie sur False, les données de télémétrie ne seront pas envoyées à [!DNL Adobe] |
| version | str | Non | None | Numéro de version de ce SDK |

## Exemple

### Python

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def client_ready_callback(ready_event):
    # make calls to Adobe Target

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
