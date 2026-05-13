---
keywords: implémentation, at.js, bibliothèque JavaScript
description: Découvrez comment déployer la bibliothèque JavaScript at.js  [!DNL Adobe Target]  à l’aide de balises dans ou sans  [!DNL Adobe Experience Platform]  gestionnaire de balises.
title: Comment déployer at.js ?
feature: Implement Server-side
exl-id: e62cb27e-ea80-462b-90f8-0a033b128031
TQID: https://experienceleague.adobe.com/V80R3Ds7eaUkkJazzCLK-tIePgqund6rMfQfLBZZvRQ
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 27%

---

# Déploiement d’at.js

Informations sur le déploiement de la bibliothèque JavaScript [!DNL Adobe Target], at.js, à l’aide de balises dans [!DNL Adobe Experience Platform] ou sans gestionnaire de balises.

Vous pouvez déployer at.js à l’aide des méthodes suivantes :

* **[Implémentation [!DNL Target] utilisation de balises dans Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)** : les balises dans [!DNL Adobe Experience Platform] représentent la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Les balises offrent aux clients un moyen simple de déployer et gérer les balises d’analyse, de marketing et de publicité nécessaires pour proposer des expériences client pertinentes.

>[!NOTE]
>
> [!DNL Adobe Experience Platform Launch] est désormais une suite de technologies dédiée à la collecte de données dans [!DNL Adobe Experience Platform]. Plusieurs modifications terminologiques ont par conséquent été déployées dans la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) suivant pour obtenir une référence consolidée des modifications terminologiques.

* **[Implémentation  [!DNL Target]  sans gestionnaire de balises](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)** : vous pouvez implémenter des [!DNL Target] sans utiliser de gestionnaire de balises (par exemple, les balises dans [!DNL Adobe Experience Platform]).
* **Implémentation de [!DNL Target] à l’aide d’un gestionnaire de balises tiers** : [Les balises dans Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sont la méthode recommandée pour implémenter [!DNL Target]. Vous pouvez toutefois implémenter [!DNL Target] à l’aide d’un gestionnaire de balises tiers, notamment Tealium, Ensighten et Google Tag. Pour obtenir la liste des avantages de l’utilisation de Launch, voir [Avantages de l’implémentation d’at.js à l’aide de l’extension  [!DNL Adobe Target] ](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md#advantages-of-implementing-atjs-using-the-target-extension).

  Cependant, si vous savez comment implémenter [!DNL Target] sans gestionnaire de balises, vous pouvez facilement le faire avec un gestionnaire de balises tiers au lieu de coder en dur at.js dans le code du site.

  Voici deux rubriques pertinentes qui vous aideront à implémenter [!DNL Target] avec un gestionnaire de balises tiers :

   * [Avant l’implémentation](/help/dev/before-implement/prepare-to-implement-target.md)
   * [Implémentation  [!DNL Target]  sans gestionnaire de balises](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

  Pour plus d’informations, consultez la documentation de votre gestionnaire de balises tiers.

Pour implémenter des [!DNL Target] lors de l’utilisation d’applications d’une seule page (SPA), consultez [Implémentation d’applications d’une seule page](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).
