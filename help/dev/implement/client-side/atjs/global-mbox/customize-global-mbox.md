---
keywords: mbox globale, personnaliser la mbox globale, modifier at.js, at.js, implémenter at.js
description: Découvrez comment personnaliser une mbox globale pour at.js sur la page [!UICONTROL Administration]-[!UICONTROL Implementation] dans [!DNL Adobe Target].
title: Comment personnaliser une mbox globale ?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
TQID: https://experienceleague.adobe.com/MtbjwpKrZ-WmBnE5tBY74oJgQVB-zPLrCuFDrFshkGo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 209
ht-degree: 18%

---

# Personnalisation d’une mbox globale

Informations destinées à vous aider à personnaliser une mbox globale [!DNL Adobe Target] pour at.js.

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

1. Désactivez-**[!UICONTROL Page load enabled (Auto create global mbox)]**, puis ajoutez le nom de la mbox globale personnalisée que vous souhaitez utiliser pour diffuser des activités à partir de [!DNL Target].

>[!WARNING]
>
>La modification est automatiquement enregistrée lorsque vous sélectionnez une autre mbox globale.

Cette mbox globale personnalisée est également utilisée pour le suivi des clics.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. Implémentez la bibliothèque at.js sur votre site.

   Pour plus d’informations, consultez [Déploiement d’at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md).

1. Synchronisation de la transition avec votre publication.

   Lorsque vous serez prêt à ce que [!DNL Target] commenciez à utiliser votre mbox globale pour toutes les activités à l’avenir, vous pourrez passer à cette étape.

   Mettez à jour le nom de la mbox globale personnalisée afin qu’il corresponde au nom utilisé dans l’étape 2 ci-dessus.


>[!WARNING]
>
>Toutes les activités de votre compte sont synchronisées avec cette mbox. Assurez-vous que la mbox globale est présente sur votre site afin que les activités continuent de fonctionner. Veillez à modifier et à enregistrer à nouveau les activités affectées créées avec le [!UICONTROL Visual Experience Composer] (VEC) qui se synchronisent avec cette mbox. Il n’est pas nécessaire de réenregistrer les activités créées dans le [!UICONTROL Form-Based Experience Composer] ou via l’API.
