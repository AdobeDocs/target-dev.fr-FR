---
keywords: implémentation, implémentation, configuration, paramètre de page, tomcat, url encodée, attribut de profil sur la page, paramètre mbox, attributs de profil sur la page, attribut de profil de script, API de mise à jour de profil en masse, API de mise à jour de fichier unique, attributs du client, implementation5, implementation6, implementation7, implementation8, implementation9, implementation0, implementation1, implementation2, implementation3, implementation4, implementation5, fournisseurs de données, fournisseur de données, fournisseur de données
description: Obtention de données dans  [!DNL Target] (paramètres de page, attributs de profil, attributs de profil de script, fournisseurs de données, API de mise à jour de profil en bloc et unique, attributs du client).
title: Comment puis-je importer des données dans Target ?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
TQID: https://experienceleague.adobe.com/pmlPWRHb9tnrdSFm7s5OZ-RRsJJOxw-ntBY5AeswIcM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 377
ht-degree: 27%

---

# Présentation des méthodes

Informations sur les différentes méthodes que vous pouvez utiliser pour importer des données dans Adobe Target.

Les méthodes disponibles sont les suivantes :

| Méthode | Détails |
| --- | --- |
| [Paramètres de page](page-parameters.md)<br />(également appelés « paramètres de mbox ») | Les paramètres de page sont des paires nom/valeur transmises directement par le biais du code de page qui ne sont pas enregistrées dans le profil du visiteur pour une utilisation ultérieure.Les paramètres de page <br /> sont utiles pour envoyer des données de page à des [!DNL Target] qui n’ont pas besoin d’être stockées avec le profil du visiteur pour une utilisation ultérieure de ciblage. Ces valeurs sont utilisées pour décrire la page ou l’action effectuée par l’utilisateur sur cette page spécifique. |
| [Attributs de profil sur la page](in-page-profile-attributes.md)<br />(également appelés « attributs de profil sur la mbox ») | Les attributs de profil sur la page sont des paires nom/valeur transmises directement par le biais du code de page qui sont stockées dans le profil du visiteur pour une utilisation ultérieure. Les attributs de profil sur la page <br /> permettent de stocker des données spécifiques à l’utilisateur dans le profil de Target pour un ciblage et une segmentation ultérieurs. |
| [Attributs de profil de script](script-profile-attributes.md) | Les attributs de profil de script sont des paires nom/valeur définies dans la solution [!DNL Target]. La valeur est déterminée grâce à l’exécution d’un fragment de code JavaScript sur le serveur de Target à chaque appel de serveur.<br />Les utilisateurs écrivent de petits fragments de code qui s’exécutent par appel de mbox, et avant qu’un visiteur ne soit évalué pour son audience et son appartenance à une activité. |
| [Fournisseurs de données](data-providers.md) | Les fournisseurs de données vous permettent de transmettre facilement des données de tiers à Target. |
| [API de mise à jour des profils en masse](bulk-profile-update-api.md) | Via l’API, envoyez un fichier .csv pour [!DNL Target] avec les mises à jour du profil du visiteur pour de nombreux visiteurs. Chaque profil du visiteur peut être mis à jour avec plusieurs attributs de profil internes à la page en un seul appel. |
| [API de mise à jour de profil individuel](single-profile-update-api.md) | Presque identique à l’API de mise à jour de profil en bloc, mais un profil visiteur est mis à jour à la fois, en ligne dans l’appel API plutôt qu’avec un fichier .csv. |
| [Attributs du client](customer-attributes.md) | Les attributs du client permettent de télécharger les données des profils de visiteur vers Experience Cloud par FTP. Une fois le chargement effectué, utilisez les données dans Adobe Analytics et Adobe Target. |
