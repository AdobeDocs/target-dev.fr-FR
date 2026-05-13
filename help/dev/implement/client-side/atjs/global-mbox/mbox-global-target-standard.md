---
keywords: mbox globale, target classic, utiliser une mbox globale depuis target classic
description: Découvrez comment utiliser une mbox globale héritée pour vos activités  [!DNL Adobe Target]  si vous avez déjà créé une mbox globale sur vos pages pour vos implémentations héritées.
title: Puis-je utiliser une mbox globale à partir d’une implémentation héritée ?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
TQID: https://experienceleague.adobe.com/BCubNDwB8gxZ9bpuCNhxcnFnjB1xQK8ZRkLveinPj4w
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 285
ht-degree: 20%

---

# Utiliser une mbox globale à partir d’une implémentation héritée

Par défaut, [!DNL Target] crée une mbox globale appelée target-global-mbox, qui est utilisée pour exécuter les activités créées dans [!DNL Target]. Cependant, si vous avez déjà créé une mbox globale sur vos pages pour vos implémentations héritées, vous pouvez utiliser cette mbox pour vos activités [!DNL Target].

>[!NOTE]
>
>Vous ne pouvez avoir qu’une seule mbox globale par compte.

Pour utiliser votre mbox globale existante pour [!DNL Target] comme pour votre mise en œuvre héritée, vous devez définir quelques paramètres.

1. Accédez à [!DNL Target], puis cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

   Par défaut, **[!UICONTROL Page load enabled (Auto-create global mbox]** est activé et la mbox globale personnalisée est nommée `target-global-mbox`.

1. Si vous souhaitez utiliser une mbox existante, désactivez-la, puis spécifiez **[!UICONTROL Page load enabled (Auto-create global mbox]** nom d’une mbox globale créée précédemment dans le champ **[!UICONTROL Global Mbox]** .

   La liste déroulante Mbox globale répertorie toutes les mbox de votre compte. Si vous souhaitez utiliser une mbox qui n’existe pas encore, créez-la.

1. Cliquez sur **[!UICONTROL Save]**.

   Les paramètres de votre compte sont mis à jour.

1. Téléchargez le nouveau fichier at.js et référencez-le sur votre site.

   Toutes les activités existantes se mettent à jour afin d’utiliser la mbox globale indiquée, notamment les activités créées et implémentées antérieurement.

## Résolution des problèmes d’implémentation de mbox globales

Les questions fréquentes suivantes peuvent être utilisées pour résoudre les problèmes liés à l’implémentation de votre mbox globale :

### Pourquoi la mbox globale ne se charge-t-elle pas ou pourquoi y a-t-il une latence lors du chargement de la mbox globale lorsque la page se charge ?

Assurez-vous que la référence at.js est le premier appel JavaScript sur la page. Pour obtenir d’autres solutions à ce problème, consultez [Forum aux questions sur les mbox globales](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
