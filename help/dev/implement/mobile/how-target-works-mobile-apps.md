---
description: Découvrez comment utiliser le  [!DNL Adobe Mobile SDK]  pour présenter les expériences optimales aux visiteurs de vos applications mobiles.
title: Comment  [!DNL Target] fonctionne-t-il dans les applications mobiles ?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 17%

---

# Fonctionnement de [!DNL Target] dans les applications mobiles

[!DNL Adobe Mobile SDK] contacte le serveur [!DNL Target] pour obtenir le contenu ainsi que d’autres points de données afin d’afficher l’expérience appropriée à l’utilisateur.

>[!IMPORTANT]
>
>Prise en charge de la version 4 de [!DNL Adobe Mobile].Les SDK *x* ont pris fin le 31 août 2021 et ne sont plus recommandés pour les utilisateurs mobiles [!DNL Adobe Target].
>
>Le [SDK Adobe Experience Platform pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les services et solutions [!DNL Adobe Experience Cloud] de vos applications mobiles.

## [!DNL Target] emplacements et mesures de succès

Un *emplacement cible* est également appelé mbox. Un emplacement identifié dans l’application est activé à des fins de test ou de personnalisation (par exemple, le message de bienvenue sur l’écran d’accueil). Ces emplacements sont identifiés au cours du processus de création des tests.

Une *[mesure de succès](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=fr)* est une action effectuée par l’utilisateur qui identifie si une activité spécifique a réussi (par exemple, s’inscrire, effectuer un achat, réserver un ticket, etc.).

![alt image](assets/mobile-target-location.png)

* **[!DNL Target]location :** contenu affiché sous le bouton d’inscription.

  Cet utilisateur particulier se voit proposer une offre d’expédition gratuite jusqu’à 18 h. Cet emplacement peut être réutilisé dans plusieurs activités [!DNL Target] pour exécuter des tests A/B et la personnalisation.

* **Mesure de succès :** action effectuée par l’utilisateur lorsque celui-ci clique sur le bouton d’enregistrement.

**Comprendre le fonctionnement de [!DNL Target] dans le SDK**

![alt image](assets/how-target-mobile-works.png)
