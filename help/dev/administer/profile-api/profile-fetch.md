---
title: Récupération de profils
description: Découvrez comment utiliser les API de profil Adobe Target pour récupérer les données de visiteur à utiliser dans [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Récupération de profils

A [!DNL Target] Le profil peut être récupéré de trois façons : à l’aide d’une `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` ou `thirdPartyId`.

## Utilisation d’une [!DNL Experience Cloud Visitor ID] (ECID)

Vous pouvez récupérer un profil en fonction de la variable `ECID`. La méthode HTTP doit être GET.

L’URL ressemble à l’exemple suivant :

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Remplacer `<clientCode>` avec votre [!DNL Target] [!UICONTROL Code client] et `<ECID>` avec votre [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Utilisation d’un tntid

[!DNL Target] affecte automatiquement une `tntid` pour chaque requête.

L’exemple suivant illustre le format de requête pour récupérer un profil à l’aide d’un `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Remplacer `<your-client-code>` et `your-tnt-id` et déclenchez une requête de GET. Voici un exemple d’appel de récupération de profil utilisant un `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Utilisation d’un thirdPartyId

[!DNL Adobe Target] les profils peuvent être augmentés avec votre propre identifiant (par exemple : identifiant CRM, `uuid`, numéro d’adhésion, etc.).

Voir [Mise à jour de profils](/help/dev/administer/profile-api/profile-api-overview.md) pour savoir comment joindre une `thirdPartyId` à votre profil.

L’exemple suivant illustre le format de requête pour récupérer un profil à l’aide d’un `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Remplacer `<your-client-code>` et `your-thirdpartyid` et déclenchez une requête de GET. Voici un exemple d’appel de récupération de profil utilisant un [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Lorsque cet appel est effectué, [!DNL Target] tente de localiser le profil en premier dans la grappe indiquée dans la requête edge ou partout où le profil est situé et renvoie le contenu. Le contenu du profil est renvoyé au format JSON.

## Authentification

La variable [!DNL Target Profile API] peut être sécurisé en activant l’authentification à partir de la variable [!DNL Target] IU comme décrit ici. Une fois l’authentification activée, le jeton d’authentification de profil doit être défini dans les en-têtes de requête pour toutes les requêtes d’API de profil. Le jeton lui-même peut être généré à l’aide de la fonction [!DNL Target] ou en suivant les étapes décrites ci-dessus dans la section [Jeton d’authentification de profil](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} .

## Mesures

Ces appels ne sont pas pris en compte dans vos appels de mbox.

## Gestion des erreurs

Dans le cas d’un appel à `/thirdPartyId` avec une valeur non valide ou un `thirdPartyId` specified :

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Si le profil ne peut pas être localisé ou a expiré :

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
