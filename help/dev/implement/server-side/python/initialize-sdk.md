---
title: Initialisation du SDK Python à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Python et instancier le [!UICONTROL TargetClient] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 19%

---

# Initialiser le SDK Python

Description Utilisez la variable `create` pour initialiser le SDK Python et instancier la méthode [!UICONTROL Client Target] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.

## Méthode

### create

```python {line-numbers="true"}
TargetClient.create(options)
```

## Paramètres

`options` possède la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| client | str | Oui | None | [!UICONTROL Identifiant client Adobe Target] |
| organization_id | str | Oui | None | [!UICONTROL ID d’organisation Experience Cloud] |
| timeout | int | Non | 3000 | Délai d’attente exprimé en secondes |
| server_domain | str | Non | `client.tt.omtrdc.net` |  | Remplace le nom d’hôte par défaut |
| secure | bool | Non | true | Non défini pour appliquer le schéma HTTP |
| logger | objet | Non | Enregistreur d’informations |  | Remplace l’enregistreur d’informations par défaut. |
| target_location_hint | str | Non | None | [!DNL Target] indicateur de location |
| property_token | str | Non | None | [!DNL Target] Jeton de propriété. Si spécifié ici, tous les appels get_offer utiliseront cette valeur. |
| decisioning_method | str | Non | côté serveur | Détermine la méthode de prise de décision à utiliser ([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), côté serveur, hybride) |
| polling_interval | int | Non | 300000 (5 minutes) | Intervalle d’interrogation des [artefact de règle de prise de décision sur périphérique](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (en ms) |
| artifact_location | str | Non | None | Une URL complète au niveau de la variable [artefact de règle de prise de décision sur périphérique](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Permet de remplacer un emplacement déterminé en interne. |
| artifact_payload | objet | Non | None | La charge utile JSON de la variable [artefact de règle de prise de décision sur périphérique](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). S’il est spécifié, il est utilisé au lieu d’en demander un à partir d’une URL. |
| [events](sdk-events.md) | dict &lt;str callable=&quot;&quot;> | Non | None | Objet facultatif avec clés de nom d’événement et valeurs de fonction de rappel |
| environment_id | int | Non | production | La variable [!DNL Target] ID d’environnement |
| environnement | str | Non | production | La variable [!DNL Target] nom de l&#39;environnement |
| cdn_environment | str | Non | production | Nom de l’environnement CDN |
| telemetry_enabled | bool | Non | True | Si la valeur est False, les données de télémétrie ne sont pas envoyées à [!DNL Adobe] |
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
