---
description: Découvrez comment utiliser l’pour  [!DNL Adobe Mobile SDK]  les expériences optimales aux visiteurs de votre application mobile.
title: Comment fonctionne [!DNL Target] t-il dans les applications mobiles ?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
TQID: https://experienceleague.adobe.com/R3B-i9BFKaoTkbfzVLOU-j8VV2K-MpNrf0WTCkMceT8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 16%

---

# Fonctionnement de la [!DNL Target] dans les applications mobiles

Le [!DNL Adobe Mobile SDK] contacte le serveur [!DNL Target] pour obtenir le contenu ainsi que d’autres points de données afin d’afficher l’expérience appropriée à l’utilisateur.

>[!IMPORTANT]
>
>La prise en charge des SDK [!DNL Adobe Mobile] version 4.*x* a pris fin le 31 août 2021 et n’est plus recommandée pour les utilisateurs d’[!DNL Adobe Target] mobile.
>
>[Adobe Experience Platform SDK pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les solutions et services [!DNL Adobe Experience Cloud] dans vos applications mobiles.

## [!DNL Target] des emplacements et des mesures de succès

Un *emplacement cible* est également appelé mbox. Un emplacement identifié dans l’application est activé à des fins de test ou de personnalisation (par exemple, le message de bienvenue sur l’écran d’accueil). Ces emplacements sont identifiés au cours du processus de création des tests.

Une *[mesure de succès](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)* est une action effectuée par l’utilisateur qui identifie si une activité spécifique a réussi (comme l’inscription, l’achat, la réservation d’un ticket, etc.).

![image alternative](assets/mobile-target-location.png)

* Emplacement **[!DNL Target]:** contenu affiché sous le bouton d’enregistrement.

  Cet utilisateur particulier se voit proposer une offre d’expédition gratuite jusqu’à 18 h. Cet emplacement peut être réutilisé dans plusieurs activités [!DNL Target] pour exécuter des tests A/B et la personnalisation.

* **Mesure de succès :** action effectuée par l’utilisateur lorsque celui-ci appuie sur le bouton d’enregistrement.

**Comprendre comment fonctionne [!DNL Target] dans SDK**

![image alternative](assets/how-target-mobile-works.png)
