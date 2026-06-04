---
keywords: Implémentation, non javascript, mbox, adbox
description: Utilisez un AdBox pour diffuser des images dans une implémentation hors site à l’aide de  [!DNL Adobe Target]. Un AdBox est comme un mbox, mais contrôlé par une URL au lieu de JavaScript.
title: Comment créer une adbox pour une image ?
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
TQID: https://experienceleague.adobe.com/OPo9T2Eb7afF8Ir8PAlY62OX83zhxtruUMKWCfUthxY
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 67%

---

# Création d’une adbox pour une image

Utilisez un AdBox pour diffuser des images dans une implémentation hors site à l’aide de [!DNL Adobe Target].

Une AdBox s’apparente à une mbox, mais elle est contrôlée par une URL et non par du code JavaScript. Les AdBox sont créées à l’aide d’une URL d’AdBox spéciale qui charge une mbox publicitaire (ou AdBox) dans votre compte Adobe. Utilisez cette AdBox à la place de la mbox dans les activités. Utilisez l’URL de l’AdBox au lieu d’une référence d’image directe dans les mises en œuvre de messagerie ou d’autres mises en œuvre sans JavaScript.

Pour obtenir de l’aide sur la sélection de la configuration appropriée, voir [&#x200B; Implémentations non basées sur JavaScript &#x200B;](/help/dev/implement/email/overview.md).

1. Créez l’URL de l’AdBox :

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * Où `myClientCode` est le code client de votre société. Le code client de votre entreprise est en minuscules et ne comporte pas de caractères spéciaux.

     Votre code client est disponible en haut de la page **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** de l’interface [!DNL Target].

   * Où `image` est le type d’appel. Dans ce cas, il s’agit d’une image.

   * Où `emailHeroImage123_320x200` est le nom de l’AdBox.

   * Où `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif` est le contenu par défaut de la mbox. Cela doit être une image.

     Elle doit être en codage URL et il doit s’agir d’une référence absolue. Vous pouvez utiliser la [Référence de codage d’URL d’](https://www.w3schools.com/tags/ref_urlencode.asp) pour coder rapidement vos URL.

1. Créez [des offres de redirection](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=fr) pour chaque image alternative.

   >[!NOTE]
   >
   >Les AdBox doivent être chargées avec une offre de redirection ou avec l’offre de contenu par défaut. Les autres types d’offre ne fonctionnent pas. Comme l’AdBox est une URL, elle peut uniquement afficher les URL reçues. Seules les offres de redirection fonctionnent alors.

1. Créez l’activité.

   Voir les [Implémentations non basées sur JavaScript](/help/dev/implement/email/overview.md) pour connaître la configuration appropriée permettant d’atteindre vos objectifs.

1. Effectuez une AQ sur l’activité.

   Pour respecter les bonnes pratiques, créez une page factice et vérifiez que toutes les expériences, le contenu par défaut et les rapports fonctionnent comme prévu sur tous les types de navigateur et ce, dans tous vos environnements.

1. Lancez l’activité.
