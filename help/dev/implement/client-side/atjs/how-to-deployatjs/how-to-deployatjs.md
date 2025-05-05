---
keywords: implémentation, at.js, bibliothèque JavaScript
description: Découvrez comment déployer la bibliothèque JavaScript at.js [!DNL Adobe Target]  à l’aide de balises dans  [!DNL Adobe Experience Platform]  ou sans gestionnaire de balises.
title: Comment déployer at.js ?
feature: Implement Server-side
exl-id: e62cb27e-ea80-462b-90f8-0a033b128031
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 28%

---

# Déploiement d’at.js

Informations sur le déploiement de la bibliothèque [!DNL Adobe Target] JavaScript, at.js, à l’aide de balises dans [!DNL Adobe Experience Platform] ou sans gestionnaire de balises.

Vous pouvez déployer at.js à l’aide des méthodes suivantes :

* **[Implémentation [!DNL Target] à l’aide de balises dans Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)** : les balises dans [!DNL Adobe Experience Platform] représentent la nouvelle génération de fonctionnalités de gestion des balises d’Adobe. Les balises offrent aux clients un moyen simple de déployer et gérer les balises d’analyse, de marketing et de publicité nécessaires pour proposer des expériences client pertinentes.

>[!NOTE]
>
> [!DNL Adobe Experience Platform Launch] est désormais une suite de technologies dédiée à la collecte de données dans [!DNL Adobe Experience Platform]. Plusieurs modifications terminologiques ont par conséquent été déployées dans la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour obtenir une référence consolidée des modifications terminologiques.

* **[Implémentez [!DNL Target] sans gestionnaire de balises](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)** : vous pouvez implémenter [!DNL Target] sans utiliser de gestionnaire de balises (par exemple, des balises dans [!DNL Adobe Experience Platform]).
* **Implémentez [!DNL Target] à l’aide d’un gestionnaire de balises tiers** : [Les balises dans Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sont la méthode recommandée pour implémenter [!DNL Target]. Cependant, vous pouvez également implémenter [!DNL Target] à l’aide d’un gestionnaire de balises tiers, notamment Tealium, Ensighten et Google Tag. Pour obtenir la liste des avantages de l’utilisation de Launch, voir [Avantages de l’implémentation d’at.js à l’aide de l’extension  [!DNL Adobe Target] ](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md#advantages-of-implementing-atjs-using-the-target-extension).

  Cependant, si vous savez comment implémenter [!DNL Target] sans gestionnaire de balises, vous pouvez facilement l’implémenter avec un gestionnaire de balises tiers au lieu de coder en dur at.js dans le code du site.

  Voici deux rubriques pertinentes qui vous aideront à mettre en oeuvre [!DNL Target] avec un gestionnaire de balises tiers :

   * [Avant l’implémentation](/help/dev/before-implement/prepare-to-implement-target.md)
   * [Mise en oeuvre de  [!DNL Target]  sans gestionnaire de balises](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

  Pour plus d’informations, consultez la documentation de votre gestionnaire de balises tiers.

Pour mettre en oeuvre [!DNL Target] lors de l’utilisation d’applications d’une seule page (SPA), voir [Implémentation d’applications d’une seule page](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).
