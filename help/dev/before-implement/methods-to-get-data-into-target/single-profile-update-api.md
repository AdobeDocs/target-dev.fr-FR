---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil unique
description: Obtenir des données dans [!DNL Target] à l’aide de l’API de mise à jour de profil unique.
title: Comment obtenir des données dans [!DNL Target] Utilisation de l’API de mise à jour de profil unique ?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 35%

---

# API de mise à jour de profil individuel

Presque identique au [!UICONTROL API de mise à jour des profils en masse] in [!DNL Adobe Target], mais un profil du visiteur est mis à jour à la fois, dans la ligne de l’appel API au lieu d’un fichier .csv .

## Format

Le visiteur doit être identifié à l’aide de la valeur [!DNL Target]mboxPC ou `mbox3rdPartyId` de L’Experience Cloud ID (ECID) n’est pas pris en charge.

## Exemples de cas d’utilisation

Vous souhaitez mettre à jour le profil d’un visiteur unique qui effectue une action hors ligne. Les actions peuvent inclure l’accès à un centre d’appel, le financement d’un prêt, l’utilisation d’une carte de fidélité en magasin, l’accès à un kiosque, etc.

## Avantages de la méthode

Nombre d’attributs de profil illimité.

Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et vice versa.

## Avertissements

Limite de 1 000 000 d’appels de l’API (1 million) par période de 24 heures.

Met à jour le profil uniquement. Impossible de créer un profil pour un utilisateur potentiel [!DNL Target] n&#39;a pas encore vu.

Les mises à jour surviennent généralement en moins d’une heure, mais peuvent prendre jusqu’à 24 heures pour être répercutées.

## Exemples de code

Prise en charge des commandes GET et POST.

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## Ressources

* [Mise à jour des profils](https://developers.adobetarget.com/api/#updating-profiles)