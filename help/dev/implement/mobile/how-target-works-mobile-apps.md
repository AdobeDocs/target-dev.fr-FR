---
description: Découvrez comment utiliser le [!DNL Adobe Mobile SDK] pour présenter les expériences optimales aux visiteurs de votre application mobile.
title: Comment [!DNL Target] Utilisation des applications mobiles ?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 34%

---

# Comment [!DNL Target] fonctionne dans les applications mobiles ;

La variable [!DNL Adobe Mobile SDK] contacte [!DNL Target] pour obtenir le contenu ainsi que d’autres points de données afin d’afficher l’expérience appropriée à l’utilisateur.

>[!IMPORTANT]
>
>Prise en charge de [!DNL Adobe Mobile] version 4.*x* Les SDK ont pris fin le 31 août 2021 et ne sont plus recommandés pour [!DNL Adobe Target] utilisateurs mobiles.
>
>La variable [SDK Adobe Experience Platform pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour la puissance [!DNL Adobe Experience Cloud] solutions et services dans vos applications mobiles.

## [!DNL Target] emplacements et mesures de succès

Un *emplacement cible* est également appelé mbox. Un emplacement identifié dans l’application est activé à des fins de test ou de personnalisation (par exemple, le message de bienvenue sur l’écran d’accueil). Ces emplacements sont identifiés au cours du processus de création des tests.

Une *[mesure de succès](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)* est une action effectuée par un utilisateur qui détermine si une activité spécifique est réussie (il peut s’agir d’une inscription, d’un achat, de la réservation d’un ticket, etc.).

![image alternative](assets/mobile-target-location.png)

* **[!DNL Target]location:** Contenu affiché sous le bouton d’inscription.

  Cet utilisateur particulier se voit proposer une offre d’expédition gratuite jusqu’à 18 h. Cet emplacement peut être réutilisé sur plusieurs [!DNL Target] activités pour exécuter des tests A/B et la personnalisation.

* **Mesure de succès :** Action effectuée par l’utilisateur lorsque l’utilisateur appuie sur le bouton d’enregistrement.

**Comprendre comment [!DNL Target] fonctionne dans le SDK**

![image alternative](assets/how-target-mobile-works.png)
