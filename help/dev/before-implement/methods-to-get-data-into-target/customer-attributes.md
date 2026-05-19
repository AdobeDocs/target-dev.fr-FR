---
keywords: implémentation, implémentation, configuration, configuration, attributs du client
description: Intégrez des données dans  [!DNL Target]  à l’aide des attributs du client.
title: Comment puis-je intégrer des données dans à l [!DNL Target] aide des attributs du client ?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
TQID: https://experienceleague.adobe.com/bzK915y7fvjfZjTkSK2QWHDzmIN9SdAQiEguiUlc-r8
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
source-wordcount: 216
ht-degree: 13%

---

# Attributs du client

Les attributs du client vous permettent de charger les données du profil du visiteur vers le [!DNL Adobe Experience Cloud] par FTP. Une fois le chargement effectué, utilisez les données dans [!DNL Adobe Analytics] et [!DNL Adobe Target].

Les clients Target Standard peuvent appliquer cinq attributs, [!DNL Target Premium] les clients peuvent en appliquer 200.

## Format

Un fichier .csv avec des identifiants [!DNL Experience Cloud] (ECID) et des paires nom/valeur d’attribut est chargé via FTP ou manuellement dans l’interface utilisateur d’Experience Cloud.

## Exemples de cas d’utilisation

Votre CRM ou tout autre système interne stocke les informations importantes que vous souhaitez partager avec [!DNL Adobe Experience Cloud], y compris les [!DNL Target] et les [!DNL Analytics].

## Avantages de la méthode

Le chargement de données client crée une entrée de profil pour ce visiteur dans Target, même si [!DNL Target] ne l’a pas encore vu.

Les mêmes données sont automatiquement disponibles dans [!DNL Target] et [!DNL Analytics].

Le chargement par FTP peut constituer une méthode d’implémentation plus simple que l’API.

## Avertissements

Les clients Target Standard peuvent appliquer cinq attributs, [!DNL Target Premium] les clients peuvent en appliquer 200

Les valeurs peuvent uniquement être mises à jour par le biais des attributs du client, pas sur la page.

Cette méthode requiert l’implémentation de l’Experience Cloud ID (ECID).

## Exemples de code

Vous trouverez des détails dans [Création d’une source d’attributs du client et chargement du fichier de données](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=fr).

### Liens vers des informations pertinentes

[Créer une source d’attributs du client et charger le fichier de données](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=fr).
