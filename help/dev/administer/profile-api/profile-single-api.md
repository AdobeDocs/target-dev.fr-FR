---
title: API de mise à jour de profil unique Adobe Target
description: Découvrez comment utiliser l [!DNL Adobe Target] [!UICONTROL API de mise à jour de profil unique] pour envoyer les données de profil d’un visiteur unique à  [!DNL Target].
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
source-git-commit: 6fac79420aef0a73c109b2c19f363266c1f8027a
workflow-type: tm+mt
source-wordcount: 396
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

L’[!DNL Adobe Target] [!UICONTROL API de mise à jour de profil individuel] vous permet d’envoyer une mise à jour de profil à un seul utilisateur. L’API [!UICONTROL Single Profile Update API] est presque identique à l’API [!UICONTROL Bulk Profile Update API], mais un profil de visiteur est mis à jour à la fois, en ligne avec l’appel API plutôt qu’avec un fichier .cvs.

L’API [!UICONTROL Single Profile Update API] et est généralement utilisée lorsqu’une mise à jour doit se produire en relation avec une transaction se produisant dans un canal qui n’a pas implémenté [!DNL Target]. Par exemple, vous souhaitez mettre à jour le profil d’un seul visiteur qui effectue une action hors ligne. Il peut s’agir de contacter un centre d’appel, d’obtenir un prêt, d’utiliser une carte de fidélité en magasin, d’accéder à un kiosque, etc.

Les avantages de l’[!UICONTROL API de mise à jour de profil unique] sont les suivants :

* Nombre d’attributs de profil illimité.
* Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et inversement.

## Avertissements

* L’[!UICONTROL API de mise à jour de profil unique] est limitée à l’exécution d’un million de mises à jour sur une période mobile de 24 heures.
* Les mises à jour se produisent généralement en moins d’une heure, mais leur prise en compte peut prendre jusqu’à 24 heures.

  Si vous devez envoyer d’autres mises à jour ou si vous souhaitez que les mises à jour soient traitées dans des délais plus courts, pensez à envoyer des mises à jour de profil transactionnel par le biais d’une mise à jour côté client (recommandé) ou via l’[API de diffusion](/help/dev/implement/delivery-api/overview.md) côté serveur [!DNL Adobe Target].

* L’API [!UICONTROL Single Profile Update API] est une API serveur à serveur et n’est pas conçue pour fonctionner dans une page web. Pour mettre à jour un profil du visiteur à partir de votre page web, vous pouvez utiliser la fonction [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) ou l’API [Delivery](/help/dev/implement/delivery-api/overview.md).

## Format

Spécifiez les paramètres de profil au format `profile.paramName=value`.

Pour mettre à jour le profil d’un `pcId`, utilisez :

```
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
```

Pour mettre à jour le profil d’un `mbox3rdPartyId`, utilisez :

```
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
```

L’[!UICONTROL API de mise à jour de profil unique] est réservée aux mises à jour. Si rien n’est trouvé, aucun profil n’est créé.

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
