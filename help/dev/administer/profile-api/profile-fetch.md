---
title: Récupération des profils
description: Découvrez comment utiliser les API de profil Adobe Target pour récupérer les données du visiteur à utiliser dans  [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
TQID: https://experienceleague.adobe.com/sCVfAY8W0oYu2ak-W4MYvcWSoUiAuaU3762JEhocZSE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 297
ht-degree: 0%

---

# Récupération des profils

Un profil de [!DNL Target] peut être récupéré de trois façons : à l’aide d’un `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` ou `thirdPartyId`.

## Utilisation d’un [!DNL Experience Cloud Visitor ID] (ECID)

Vous pouvez récupérer un profil en fonction de la `ECID`. La méthode HTTP doit être GET.

L’URL ressemble à l’exemple suivant :

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Remplacez `<clientCode>` par votre [!DNL Target] [!UICONTROL Code client] et `<ECID>` par votre [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Utilisation d’un tntid

[!DNL Target] attribue automatiquement un `tntid` pour chaque demande.

L’exemple suivant illustre le format de requête pour récupérer un profil à l’aide d’un `tntid` :

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Remplacez `<your-client-code>` et `your-tnt-id`, puis déclenchez une requête GET. Voici un exemple d’appel de récupération de profil à l’aide d’un `tntid` :

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Utilisation d’un thirdPartyId

[!DNL Adobe Target] profils peuvent être augmentés avec votre propre identifiant (par exemple : identifiant CRM, `uuid`, numéro d’abonnement, etc.).

Voir [Mettre à jour les profils](/help/dev/administer/profile-api/profile-api-overview.md) pour savoir comment joindre un `thirdPartyId` à votre profil.

L’exemple suivant illustre le format de requête pour récupérer un profil à l’aide d’un `thirdPartyId` :

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Remplacez `<your-client-code>` et `your-thirdpartyid`, puis déclenchez une requête GET. Voici un exemple d’appel de récupération de profil à l’aide d’un [!UICONTROL thirdpartyid] :

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Lorsque cet appel est effectué, [!DNL Target] tente de localiser le profil en premier dans le cluster noté dans la requête Edge, ou à l’endroit où se trouve le profil et de renvoyer le contenu. Le contenu du profil est renvoyé au format JSON.

## Authentification

Le [!DNL Target Profile API] peut être sécurisé en activant l’authentification à partir de l’interface utilisateur de [!DNL Target], comme décrit ici. Une fois l’authentification ACTIVÉE, le jeton d’authentification du profil doit être défini dans les en-têtes de toutes les requêtes API de profil. Le jeton lui-même peut être généré à l’aide de l’interface utilisateur de [!DNL Target] ou en suivant les étapes décrites ci-dessus dans la section [Jeton d’authentification de profil](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank}.

## Mesure

Ces appels ne sont pas pris en compte dans vos appels de mbox.

## Gestion des erreurs

Dans le cas d&#39;un appel à `/thirdPartyId` avec un `thirdPartyId` spécifié non valide ou expiré :

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Si le profil est introuvable ou a expiré :

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
