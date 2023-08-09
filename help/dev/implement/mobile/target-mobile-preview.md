---
keywords: aq, aperçu, lien d’aperçu, mobile, aperçu mobile
description: Utilisez les liens d’aperçu mobile pour vérifier systématiquement la qualité des activités des applications mobiles. Vous pouvez vous inscrire à différentes expériences sans appareils de test spéciaux.
title: Comment utiliser le lien d’aperçu mobile dans [!DNL Target] Mobile ?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: cf39b35e208a99114b3f97df2e9ef7eb8a46e153
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 57%

---

# [!DNL Target] aperçu mobile

Utilisez le lien d’aperçu mobile pour vérifier simplement et de manière exhaustive la qualité des activités des applications mobiles et prenez part à différentes expériences directement sur votre appareil, sans avoir à utiliser de dispositif de test spécifique.

## Aperçu

La fonctionnalité d’aperçu mobile vous permet de tester entièrement vos activités d’applications mobiles avant de les mettre en service.

## Conditions préalables

1. **Utilisez une version prise en charge du SDK :** la fonction d’aperçu mobile requiert de télécharger et d’installer la version appropriée 4.14 (ou ultérieure) du SDK Adobe Mobile dans vos applications correspondantes.

   Pour obtenir des instructions sur le téléchargement du SDK approprié, voir [Versions actuelles du SDK](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} dans le *[!DNL Adobe Experience Platform Mobile SDK]* la documentation.

1. **Configurez un modèle d’URL :** le lien d’aperçu utilise un modèle d’URL pour ouvrir votre application. Vous devez spécifiez un modèle d’URL unique pour l’aperçu.

   Pour plus d’informations, voir [Aperçu visuel](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* dans le *[!DNL Adobe Experience Platform Mobile SDK]* la documentation.

   Les liens suivants contiennent plus d’informations :

   * **iOS**: pour plus d’informations sur la définition de schémas d’URL pour iOS, voir [Définition d’un modèle d’URL personnalisé pour votre application](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} sur le site web du développeur Apple.
   * **Android**: pour plus d’informations sur la définition de schémas d’URL pour Android, voir [Création de liens profonds vers le contenu de l’application](https://developer.android.com/training/app-links/deep-linking){target=_blank} sur le site web des développeurs Android.

1. **Configuration `collectLaunchInfo` API**

   Pour plus d’informations, voir [Aperçu visuel](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* dans le *[!DNL Adobe Experience Platform Mobile SDK]* la documentation.

## Génération d’un lien d’aperçu

1. Dans le [!DNL Target] Cliquez sur l’interface utilisateur **[!UICONTROL Plus d’options]** (points de suspension verticaux), puis sélectionnez **[!UICONTROL Créer un aperçu mobile]**.

   ![image alternative](assets/mobile-preview-create.png)

1. Sélectionnez les activités à prévisualiser, puis cliquez sur **[!UICONTROL Générer un lien d’aperçu mobile]**.

   >[!NOTE]
   >
   >Seules les activités AB et XT basées sur les formulaires peuvent être sélectionnées.

   ![image alternative](assets/mobile-preview-select-activities.png)

1. Spécifiez le modèle d’URL de votre application.

   Il doit être identique à celui présent dans votre application iOS ou Android. Au besoin, répétez ce processus séparément pour iOS et Android.

   ![image alternative](assets/mobile-preview-enter-url-scheme.png)

1. Cliquez sur **[!UICONTROL Générer un lien d’aperçu mobile]**, puis copiez le lien.

   ![image alternative](assets/mobile-preview-generate-and-copy.png)

## Afficher l’aperçu sur votre appareil

Ouvrez le lien dans un navigateur mobile sur l’appareil sur lequel vous avez installé votre application. Il peut s’agir de l’application de production que vous avez téléchargée de la boutique Apple App Store ou Google Play. Pas besoin d’une version spéciale. Si vous avez un lien d’aperçu actif, vous pourrez afficher les expériences sur l’appareil.

1. Ouvrez le lien dans votre navigateur mobile.

   Partagez le lien que vous avez copié à l’étape précédente à partir du [!DNL Target] L’interface utilisateur de votre appareil mobile d’une manière pratique, par exemple en utilisant du texte, du courrier électronique ou du Slack.

   |![aperçu lien profond 1](assets/mobile-preview-open-deeplink.png)|![aperçu lien profond 2](assets/mobile-preview-open-app.png)|

   Votre application s’ouvre et démarre. [!DNL Target] Mode Aperçu mobile.

1. Sélectionnez la combinaison d’expériences que vous souhaitez afficher, puis cliquez sur **[!UICONTROL Démarrer les expériences]**.

   |![aperçu mobile 1](assets/mobile-preview-experience-selection-1.png)|![aperçu mobile 2](assets/mobile-preview-experience-result-1-france.png)|![aperçu mobile 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![aperçu mobile 4](assets/mobile-preview-experience-selection-2.png)|![aperçu mobile 5](assets/mobile-preview-experience-result-2-aus.png)|![aperçu mobile 6](assets/mobile-preview-experience-result-2-10off.png)|

## Limites 

* Après avoir cliqué sur le bouton **[!UICONTROL Démarrer les expériences]**, la vue doit charger à nouveau pour afficher le nouveau contenu. Le moyen le plus simple est de basculer vers un autre écran et de revenir ensuite dans l’écran où la modification doit avoir lieu.
* L’aperçu mobile n’est pas pris en charge pour les versions Android antérieures à API-19 (KitKat).
