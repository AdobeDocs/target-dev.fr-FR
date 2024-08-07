---
keywords: aq, aperçu, lien d’aperçu, mobile, aperçu mobile
description: Utilisez les liens d’aperçu mobile pour vérifier systématiquement la qualité des activités des applications mobiles.
title: Comment utiliser les liens d’aperçu mobile dans  [!DNL Adobe Target] Mobile ?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 15e42d0fb049f9243ff5468ff5f22a8e79c55c79
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 23%

---

# [!DNL Target] aperçu mobile

Utilisez les liens d’aperçu mobile pour vérifier simplement et de manière exhaustive la qualité des activités des applications mobiles et vous inscrire à différentes expériences à l’aide de votre appareil sans périphérique de test spécial.

La fonctionnalité d’aperçu mobile vous permet de tester entièrement vos activités d’application mobile avant de les lancer en ligne.

## Conditions préalables

1. **Utiliser une version prise en charge du SDK :** La fonctionnalité d’aperçu mobile requiert que vous téléchargiez et installez la version appropriée de [!DNL Adobe Mobile SDK] dans vos applications correspondantes.

   Pour obtenir des instructions sur le téléchargement du SDK approprié, reportez-vous à la section [Versions actuelles du SDK](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} de la documentation *[!DNL Adobe Experience Platform Mobile SDK]*.

1. **Configurez un modèle d’URL :** le lien d’aperçu utilise un modèle d’URL pour ouvrir votre application. Spécifiez un modèle d’URL unique pour l’aperçu.

   Pour plus d’informations, voir [Aperçu visuel](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} dans *Configuration de l’extension Target dans l’interface utilisateur de la connexion aux données* dans la documentation *[!DNL Mobile SDK]*.

   Les liens suivants contiennent plus d’informations :

   * **iOs** : pour plus d’informations sur la définition de schémas d’URL pour iOS, voir [Définition d’un modèle d’URL personnalisé pour votre application](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} sur le site Web *Développeur Apple*.
   * **Android** : pour plus d’informations sur la définition de schémas d’URL pour Android, voir [Création de liens profonds vers le contenu de l’application](https://developer.android.com/training/app-links/deep-linking){target=_blank} sur le site Web *Développeurs Android*.

1. **Configuration de l’API `collectLaunchInfo` (i0S uniquement)**

   Pour plus d’informations, voir [Aperçu visuel](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} dans *Configuration de l’extension Target dans l’interface utilisateur de la connexion aux données* dans la documentation *[!DNL Mobile SDK]*.

## Génération d’un lien d’aperçu

1. Dans l’interface utilisateur de [!DNL Target], cliquez sur l’icône **[!UICONTROL More Options]** (points de suspension alignés verticalement), puis sélectionnez **[!UICONTROL Create Mobile Preview Link]**.

   ![alt image](assets/mobile-preview-create.png)

1. Sélectionnez les activités à prévisualiser, puis cliquez sur **[!UICONTROL Generate Mobile Preview Link]**.

   >[!NOTE]
   >
   >Vous pouvez sélectionner uniquement les activités [!UICONTROL A/B Test] et [!UICONTROL Experience Targeting] (XT) basées sur des formulaires.

   ![alt image](assets/mobile-preview-select-activities.png)

1. Spécifiez le modèle d’URL de votre application.

   Le modèle d’URL doit être identique à celui existant dans votre application iOS ou Android. Répétez cette opération séparément pour iOS et Android, si nécessaire.

   ![alt image](assets/mobile-preview-enter-url-scheme.png)

1. Cliquez sur **[!UICONTROL Generate Mobile Preview Link]**, puis copiez le lien.

   ![alt image](assets/mobile-preview-generate-and-copy.png)

## Afficher l’aperçu sur votre appareil

Ouvrez le lien dans un navigateur mobile sur l’appareil sur lequel vous avez installé votre application. Cette application peut être l’application de production que vous avez téléchargée à partir de [!DNL Apple App Store] ou de [!DNL Google Play Store]. L’application n’a pas besoin d’être une version spéciale. Si vous disposez d’un lien d’aperçu actif, vous pouvez afficher les expériences sur l’appareil.

1. Ouvrez le lien dans votre navigateur mobile.

   Partagez le lien que vous avez copié dans la section précédente de l’interface utilisateur de [!DNL Target] vers votre appareil mobile de manière pratique, par exemple en utilisant du texte, du courrier électronique ou [!DNL Slack].

   |![aperçu lien profond 1](assets/mobile-preview-open-deeplink.png)|![aperçu lien profond 2](assets/mobile-preview-open-app.png)|

   Votre application s’ouvre et démarre le [!DNL Target] [!UICONTROL Mobile Preview Mode].

1. Sélectionnez la combinaison d’expériences que vous souhaitez afficher, puis cliquez sur **[!UICONTROL Launch Experiences]**.

   |![aperçu mobile 1](assets/mobile-preview-experience-selection-1.png)|![aperçu mobile 2](assets/mobile-preview-experience-result-1-france.png)|![aperçu mobile 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![aperçu mobile 4](assets/mobile-preview-experience-selection-2.png)|![aperçu mobile 5](assets/mobile-preview-experience-result-2-aus.png)|![aperçu mobile 6](assets/mobile-preview-experience-result-2-10off.png)|

## Limites 

* La vue doit se charger à nouveau pour que le nouveau contenu s’affiche après avoir cliqué sur le bouton **[!UICONTROL Launch Experiences]**. Le moyen le plus simple est de basculer vers un autre écran et de revenir ensuite dans l’écran où la modification doit avoir lieu.
* L’aperçu mobile n’est pas pris en charge pour les versions Android antérieures à API-19 (KitKat).
