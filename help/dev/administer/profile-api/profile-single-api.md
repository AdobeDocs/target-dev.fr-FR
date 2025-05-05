---
title: API de mise à jour de profil unique Adobe Target
description: Découvrez comment utiliser [!DNL Adobe Target] [!UICONTROL Single Profile Update API] pour envoyer les données de profil d’un visiteur unique à [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# [!DNL Adobe Target Single Profile Update API]

[!DNL Adobe Target] [!UICONTROL Single Profile Update API] permet d&#39;envoyer une mise à jour de profil pour un utilisateur unique. [!UICONTROL Single Profile Update API] est presque identique à [!UICONTROL Bulk Profile Update API], mais un profil du visiteur est mis à jour à la fois, en ligne avec l’appel API au lieu d’un fichier .cvs.

Le [!UICONTROL Single Profile Update API] et est généralement utilisé lorsqu’une mise à jour doit se produire par rapport à une transaction survenant dans un canal qui n’a pas implémenté [!DNL Target]. Par exemple, vous souhaitez mettre à jour le profil d’un visiteur unique qui effectue une action hors ligne. Les actions peuvent inclure l’accès à un centre d’appel, le financement d’un prêt, l’utilisation d’une carte de fidélité en magasin, l’accès à un kiosque, etc.

Les avantages de [!UICONTROL Single Profile Update API] incluent :

* Nombre d’attributs de profil illimité.
* Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et de la manière inverse.

## Avertissements

* [!UICONTROL Single Profile Update API] est limité à l’exécution d’1 million de mises à jour par période variable de 24 heures.
* Les mises à jour surviennent généralement en moins d’une heure, mais peuvent prendre jusqu’à 24 heures pour être répercutées.

  Si vous devez envoyer d’autres mises à jour ou exiger que les mises à jour soient traitées dans des délais plus courts, envisagez d’envoyer des mises à jour de profil transactionnel par le biais d’une mise à jour côté client (préférée) ou via l’ [!DNL Adobe Target] API de diffusion [ côté serveur ](/help/dev/implement/delivery-api/overview.md).

* [!UICONTROL Single Profile Update API] est une API serveur à serveur qui n’est pas conçue pour fonctionner dans une page web. Pour mettre à jour un profil du visiteur depuis votre page web, vous pouvez utiliser la fonction [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) ou l’ [ API de diffusion](/help/dev/implement/delivery-api/overview.md).

## Format

Spécifiez les paramètres de profil au format `profile.paramName=value`.

Pour mettre à jour le profil d’un `pcId`, utilisez :

``` ```
https://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``` ```

Pour mettre à jour le profil d’un `mbox3rdPartyId`, utilisez :

``` ```
shell http://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``` ```

[!UICONTROL Single Profile Update API] est réservé aux mises à jour. Si rien n’est trouvé, aucun profil n’est créé.

## Remarques

* Les paramètres et valeurs doivent être encodés au format URL à l’aide du codage UTF-8.
* Le format des paramètres est `profile.paramName`.
* Toutes les valeurs de paramètre ne doivent pas exister pour tous les pcIds et mbox3rdPartyIds.
* Les paramètres et valeurs sont sensibles à la casse.
* GET et POST sont pris en charge.
* La taille limite actuelle est de 8 Ko pour les GET et de 60 Ko pour les POST.

## Réponse

Voici un exemple de réponse pour les requêtes ci-dessus :

`trueRequest successfully submitted`

Cette réponse indique que la réponse a été envoyée et sera traitée prochainement.
