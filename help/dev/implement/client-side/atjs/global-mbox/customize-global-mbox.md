---
keywords: mbox globale, personnaliser la mbox globale, modifier at.js, at.js, implémenter at.js
description: Découvrez comment personnaliser une mbox globale pour at.js sur la page [!UICONTROL Administration]-[!UICONTROL Implementation] dans [!DNL Adobe Target].
title: Comment personnaliser une mbox globale ?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 18%

---

# Personnalisation d’une mbox globale

Informations pour vous aider à personnaliser une mbox globale [!DNL Adobe Target] pour at.js.

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

1. Désactivez **[!UICONTROL Page load enabled (Auto create global mbox)]**, puis ajoutez le nom de la mbox globale personnalisée que vous souhaitez utiliser pour dispenser les activités de [!DNL Target].

>[!WARNING]
>
>La modification est automatiquement enregistrée lorsque vous sélectionnez une autre mbox globale.

Cette mbox globale personnalisée est également utilisée pour le suivi des clics.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. Implémentez la bibliothèque at.js sur votre site.

   Pour plus d’informations, voir [Déploiement d’at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) .

1. Synchronisation de la transition avec votre publication.

   Lorsque vous êtes prêt à ce que [!DNL Target] commence à utiliser votre mbox globale pour toutes les activités à l’avenir, vous pouvez passer à cette étape.

   Mettez à jour le nom de la mbox globale personnalisée afin qu’il corresponde au nom utilisé dans l’étape 2 ci-dessus.


>[!WARNING]
>
>Toutes les activités de votre compte sont synchronisées avec cette mbox. Assurez-vous que la mbox globale est présente sur votre site afin que les activités continuent à fonctionner. Veillez à modifier et à enregistrer à nouveau les activités affectées qui ont été créées avec le [!UICONTROL Visual Experience Composer] (VEC) synchronisé avec cette mbox. Il n’est pas nécessaire de réenregistrer les activités créées dans [!UICONTROL Form-Based Experience Composer] ou via l’API.
