---
title: API de mise à jour de profil unique Adobe Target
description: Découvrez comment utiliser  [!DNL Adobe Target] [!UICONTROL Single Profile Update API] pour envoyer les données de profil d’un visiteur unique à  [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
TQID: https://experienceleague.adobe.com/HEjGkrgixufe9wQvaPAljSlZRSaF-idgwKYWs3cuoJ0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 361
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

Le [!UICONTROL Single Profile Update API] [!DNL Adobe Target] vous permet d’envoyer une mise à jour de profil pour un seul utilisateur. Le [!UICONTROL Single Profile Update API] est presque identique au [!UICONTROL Bulk Profile Update API], mais un profil de visiteur est mis à jour à la fois, en ligne avec l’appel API plutôt qu’avec un fichier .cvs.

Le [!UICONTROL Single Profile Update API] et est généralement utilisé lorsqu’une mise à jour doit se produire en relation avec une transaction se produisant dans un canal qui n’a pas implémenté [!DNL Target]. Par exemple, vous souhaitez mettre à jour le profil d’un seul visiteur qui effectue une action hors ligne. Il peut s’agir de contacter un centre d’appel, d’obtenir un prêt, d’utiliser une carte de fidélité en magasin, d’accéder à un kiosque, etc.

Les avantages de la [!UICONTROL Single Profile Update API] sont les suivants :

* Nombre d’attributs de profil illimité.
* Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et inversement.

## Avertissements

* L’[!UICONTROL Single Profile Update API] est limitée à l’exécution d’un million de mises à jour par période de 24 heures consécutives.
* Les mises à jour se produisent généralement en moins d’une heure, mais leur prise en compte peut prendre jusqu’à 24 heures.

  Si vous devez envoyer d’autres mises à jour ou si vous souhaitez que les mises à jour soient traitées dans des délais plus courts, pensez à envoyer des mises à jour de profil transactionnel par le biais d’une mise à jour côté client (recommandé) ou via l’[API de diffusion](/help/dev/implement/delivery-api/overview.md) côté serveur [!DNL Adobe Target].

* Le [!UICONTROL Single Profile Update API] est une API serveur à serveur et n’est pas conçu pour fonctionner dans une page web. Pour mettre à jour un profil du visiteur à partir de votre page web, vous pouvez utiliser la fonction [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) ou l’API [Delivery](/help/dev/implement/delivery-api/overview.md).

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

La [!UICONTROL Single Profile Update API] est réservée aux mises à jour. Si rien n’est trouvé, aucun profil n’est créé.

## Remarques

* Les paramètres et les valeurs doivent être encodés en URL à l’aide d’UTF-8.
* Le format des paramètres est `profile.paramName`.
* Toutes les valeurs de paramètre ne doivent pas exister pour tous les pcIds et mbox3rdPartyIds.
* Les paramètres et les valeurs sont sensibles à la casse.
* GET et POST sont pris en charge.
* La limite de taille actuelle est de 8 Ko pour GET et de 60 Ko pour POST.

## Réponse

Voici un exemple de réponse pour les requêtes ci-dessus :

`trueRequest successfully submitted`

Cette réponse indique que la réponse a été envoyée et sera bientôt traitée.
