---
keywords: Mise en oeuvre, sans JavaScript, mbox, adbox
description: Utilisez une adbox pour diffuser des images dans une mise en oeuvre hors site à l’aide de [!DNL Adobe Target]. Une adbox est semblable à une mbox, mais elle est contrôlée par une URL au lieu de JavaScript.
title: Comment créer une adbox pour une image ?
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 71%

---

# Création d’une adbox pour une image

Utilisez une adbox pour diffuser des images dans une mise en oeuvre hors site à l’aide de [!DNL Adobe Target].

Une AdBox s’apparente à une mbox, mais elle est contrôlée par une URL et non par du code JavaScript. Les AdBox sont créées à l’aide d’une URL d’AdBox spéciale qui charge une mbox publicitaire (ou AdBox) dans votre compte Adobe. Utilisez cette AdBox à la place de la mbox dans les activités. Utilisez l’URL de l’AdBox au lieu d’une référence d’image directe dans les mises en œuvre de messagerie ou d’autres mises en œuvre sans JavaScript.

Pour obtenir de l’aide sur la sélection de la configuration appropriée, voir [Implémentations non basées sur JavaScript](/help/dev/implement/email/overview.md).

1. Créez l’URL de l’AdBox :

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * Où `myClientCode` est le code client de votre société. Le code client de votre entreprise est en minuscules et ne comporte pas de caractères spéciaux.

     Votre code client est disponible en haut de la page **[!UICONTROL Administation]** > **[!UICONTROL Implementation]** de l’interface [!DNL Target].

   * Où `image` est le type d’appel. Dans ce cas, il s’agit d’une image.

   * Où `emailHeroImage123_320x200` est le nom de l’AdBox.

   * Où `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif` est le contenu par défaut de la mbox. Cela doit être une image.

     Elle doit être en codage URL et il doit s’agir d’une référence absolue. Vous pouvez utiliser la [référence de codage d’URL d’HTML](https://www.w3schools.com/tags/ref_urlencode.asp) pour coder rapidement vos URL.

1. Créez [des offres de redirection](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=fr) pour chaque image alternative.

   >[!NOTE]
   >
   >Les AdBox doivent être chargées avec une offre de redirection ou avec l’offre de contenu par défaut. Les autres types d’offre ne fonctionnent pas. Comme l’AdBox est une URL, elle peut uniquement afficher les URL reçues. Seules les offres de redirection fonctionnent alors.

1. Créez l’activité.

   Voir les [Implémentations non basées sur JavaScript](/help/dev/implement/email/overview.md) pour connaître la configuration appropriée permettant d’atteindre vos objectifs.

1. Effectuez une AQ sur l’activité.

   Pour respecter les bonnes pratiques, créez une page factice et vérifiez que toutes les expériences, le contenu par défaut et les rapports fonctionnent comme prévu sur tous les types de navigateur et ce, dans tous vos environnements.

1. Lancez l’activité.
