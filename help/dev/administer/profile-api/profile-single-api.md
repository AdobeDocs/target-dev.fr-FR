---
title: API de mise à jour de profil unique Adobe Target
description: Découvrez comment utiliser [!DNL Adobe Target] [!UICONTROL API de mise à jour de profil unique] pour envoyer les données de profil d’un visiteur unique à [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 81bff85a9d1fe28ca267c471a470da95568fd06d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

La variable [!DNL Adobe Target] [!UICONTROL API de mise à jour de profil unique] vous permet d’envoyer une mise à jour de profil pour un utilisateur unique. La variable [!UICONTROL API de mise à jour de profil unique] est presque identique au [!UICONTROL API de mise à jour des profils en masse], mais un profil du visiteur est mis à jour à la fois, en ligne avec l’appel API au lieu d’un fichier .cvs.

La variable [!UICONTROL API de mise à jour de profil unique] et est généralement utilisé lorsqu’une mise à jour doit se produire par rapport à une transaction survenant dans un canal qui n’a pas été implémenté [!DNL Target]. Par exemple, vous souhaitez mettre à jour le profil d’un visiteur unique qui effectue une action hors ligne. Les actions peuvent inclure l’accès à un centre d’appel, le financement d’un prêt, l’utilisation d’une carte de fidélité en magasin, l’accès à un kiosque, etc.

Avantages de la variable [!UICONTROL API de mise à jour de profil unique] inclure :

* Nombre d’attributs de profil illimité.
* Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et de la manière inverse.

## Avertissements

* La variable [!UICONTROL API de mise à jour de profil unique] est limitée à effectuer 1 million de mises à jour sur toute période continue de 24 heures.
* Les mises à jour surviennent généralement en moins d’une heure, mais peuvent prendre jusqu’à 24 heures pour être répercutées.

  Si vous devez envoyer d’autres mises à jour ou exiger que les mises à jour soient traitées dans des délais plus courts, envisagez d’envoyer des mises à jour de profil transactionnel par le biais d’une mise à jour côté client (recommandé) ou via la variable [!DNL Adobe Target] côté serveur [API de diffusion](/help/dev/implement/delivery-api/overview.md).

## Format

Définir les paramètres de profil au format `profile.paramName=value`.

Pour mettre à jour le profil d’un `pcId`, utilisez :

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

Pour mettre à jour le profil d’une `mbox3rdPartyId`, utilisez :

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

La variable [!UICONTROL API de mise à jour de profil unique] est réservé aux mises à jour. Si rien n’est trouvé, aucun profil n’est créé.

## Remarques

* Les paramètres et valeurs doivent être encodés au format URL à l’aide du codage UTF-8.
* Le format du paramètre est `profile.paramName`.
* Toutes les valeurs de paramètre ne doivent pas exister pour tous les pcIds et mbox3rdPartyIds.
* Les paramètres et les valeurs sont sensibles à la casse.
* GET et POST sont pris en charge.
* La taille limite actuelle est de 8 Ko pour les GET et de 60 Ko pour les POST.

## Réponse

Voici un exemple de réponse pour les requêtes ci-dessus :

`trueRequest successfully submitted`

Cette réponse indique que la réponse a été envoyée et sera traitée prochainement.