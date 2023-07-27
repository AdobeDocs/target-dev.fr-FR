---
keywords: implémenter, implémenter, configurer, configurer, paramètre de page, tomcat, encodé URL, attribut de profil interne à la page, paramètre de mbox, attributs de profil internes à la page, attribut de profil de script, API de mise à jour de profil en masse, API de mise à jour de profil individuel, attributs du client, implémenter5, implémenter6, implémenter7, implémenter8, implémenter9, implémenter1, implémenter3, implémenter4, implémenter5, fournisseurs de données
description: Obtenir des données dans [!DNL Target] (paramètres de page, attributs de profil, attributs de profil de script, fournisseurs de données, API de mise à jour de profil uniques et en masse, attributs du client).
title: Comment puis-je obtenir des données dans Target ?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 44%

---

# Présentation des méthodes

Informations sur les différentes méthodes permettant d’intégrer des données dans Adobe Target.

Les méthodes disponibles sont les suivantes :

| Méthode | Détails |
| --- | --- |
| [Paramètres de page](page-parameters.md)<br />(Également appelé &quot;paramètres de mbox&quot;) | Les paramètres de page sont des paires nom/valeur transmises directement par le biais du code de page qui ne sont pas enregistrées dans le profil du visiteur pour une utilisation ultérieure.<br />Les paramètres de page sont utiles pour envoyer des données de page à [!DNL Target] qui n’a pas besoin d’être stocké avec le profil du visiteur pour une utilisation ultérieure dans le cadre du ciblage. Ces valeurs sont utilisées pour décrire la page ou l’action effectuée par l’utilisateur sur cette page spécifique. |
| [Attributs de profil internes à la page](in-page-profile-attributes.md)<br />(Également appelé &quot;attributs de profil internes à la mbox&quot;) | Les attributs de profil internes à la page sont des paires nom/valeur transmises directement par le biais du code de page qui sont enregistrées dans le profil du visiteur pour une utilisation ultérieure.<br />Les attributs de profil internes à la page permettent d’enregistrer les données spécifiques à l’utilisateur dans le profil de Target pour un ciblage et une segmentation ultérieurs. |
| [Attributs de profil de script](script-profile-attributes.md) | Les attributs de profil de script sont des paires nom/valeur définies dans la variable [!DNL Target] solution. La valeur est déterminée grâce à l’exécution d’un fragment de code JavaScript sur le serveur de Target à chaque appel de serveur.<br />Les utilisateurs écrivent de petits fragments de code qui s’exécutent à chaque appel de mbox, avant l’évaluation de l’appartenance d’audience et de l’appartenance à une activité d’un visiteur. |
| [Fournisseurs de données](data-providers.md) | Les fournisseurs de données vous permettent de transmettre facilement des données provenant de tiers à Target. |
| [API de mise à jour des profils en masse](bulk-profile-update-api.md) | Via l’API, envoyez un fichier .csv à [!DNL Target] avec des mises à jour du profil du visiteur pour de nombreux visiteurs. Chaque profil du visiteur peut être mis à jour avec plusieurs attributs de profil internes à la page en un seul appel. |
| [API de mise à jour de profil individuel](single-profile-update-api.md) | Presque identique à l’API de mise à jour de profil en bloc, mais un profil du visiteur est mis à jour à la fois, en ligne dans l’appel d’API au lieu d’être associé à un fichier .csv. |
| [Attributs du client](customer-attributes.md) | Les attributs du client permettent de télécharger les données des profils de visiteur vers Experience Cloud par FTP. Une fois le chargement effectué, utilisez les données dans Adobe Analytics et Adobe Target. |
