---
keywords: implémentation, implémentation, configuration, configuration, attributs du client
description: Récupérez des données dans  [!DNL Target] à l’aide des attributs du client.
title: Comment obtenir des données dans  [!DNL Target] à l’aide des attributs du client ?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 14%

---

# Attributs du client

Les attributs du client vous permettent de transférer les données de profil du visiteur par FTP vers le [!DNL Adobe Experience Cloud]. Une fois le chargement effectué, utilisez les données dans [!DNL Adobe Analytics] et [!DNL Adobe Target].

Les clients Target Standard peuvent appliquer cinq attributs, les clients [!DNL Target Premium] peuvent appliquer 200 attributs.

## Format

Un fichier .csv avec [!DNL Experience Cloud] ID (ECID) et des paires nom/valeur d’attribut est téléchargé via FTP ou manuellement dans l’interface utilisateur Experience Cloud.

## Exemples de cas d’utilisation

Votre système CRM ou autre système interne stocke des informations précieuses que vous souhaitez partager avec [!DNL Adobe Experience Cloud], y compris [!DNL Target] et [!DNL Analytics].

## Avantages de la méthode

Le chargement des données client crée une entrée de profil pour ce visiteur dans Target, même si [!DNL Target] n’a pas encore vu le visiteur.

Les mêmes données sont automatiquement disponibles dans [!DNL Target] et [!DNL Analytics].

Le chargement par FTP peut constituer une méthode d’implémentation plus simple que l’API.

## Avertissements

Les clients Target Standard peuvent appliquer cinq attributs, les clients [!DNL Target Premium] peuvent appliquer 200 attributs.

Les valeurs peuvent uniquement être mises à jour par le biais des attributs du client, pas sur la page.

Cette méthode requiert l’implémentation de l’Experience Cloud ID (ECID).

## Exemples de code

Vous trouverez des détails dans la section [Création d’une source d’attributs du client et transfert du fichier de données](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=fr).

### Liens vers les informations pertinentes

[Créez une source d’attributs du client et chargez le fichier de données](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=fr).
