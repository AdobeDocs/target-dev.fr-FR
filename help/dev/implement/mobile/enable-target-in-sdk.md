---
keywords: application mobile, application mobile sdk, application mobile target, sdk target mobile, sdk d’application mobile, activer target dans sdk
description: Découvrez comment ajouter le SDK Mobile Services Adobe à votre application mobile.
title: Comment activer [!DNL Target] dans le [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 49%

---

# Activer [!DNL Target] dans le SDK

Ajoutez la variable [!UICONTROL SDK Adobe Mobile Services] à votre application.

>[!IMPORTANT]
>
>Prise en charge de [!DNL Adobe Mobile] version 4.*x* Les SDK ont pris fin le 31 août 2021 et ne sont plus recommandés pour [!DNL Adobe Target] utilisateurs mobiles.
>
>La variable [SDK Adobe Experience Platform pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour la puissance [!DNL Adobe Experience Cloud] solutions et services dans vos applications mobiles.

1. Si vous n’avez pas encore installé le SDK Adobe Mobile Services dans votre application, utilisez vos informations d’identification Analytics ou Experience Cloud pour le télécharger depuis le site web [Adobe Mobile Services](https://mobilemarketing.adobe.com/).

1. Ajoutez la variable [!DNL Adobe Mobile Services SDK] à votre application.

   Les instructions sont disponibles sous [Mise en œuvre principale et cycle de vie](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Ajoutez le code client, le délai et activez SSL.

   Dans Experience Cloud, ouvrez Mobile Services, puis allez dans **[!UICONTROL Gérer les paramètres d’application]** > **[!UICONTROL Options Target du SDK]**.

   Ajoutez [!DNL Target] clientcode et délai d’expiration. Le code client est spécifique à votre compte ou entreprise. Le délai d’expiration est la durée en secondes pendant laquelle [!DNL Target] attend une réponse avant d’afficher le contenu par défaut. Assurez-vous que l’option **[!UICONTROL Utiliser HTTPS]** est sélectionnée sur la page de gestion des paramètres d’application d’Adobe Mobile Services. Si HTTPS n’est pas activé, tous les appels dans iOS9+ seront bloqués, sauf si vous placez sur la liste autorisée la variable [!DNL Target] serveur.

   ![image alternative](assets/mobile-clientcode.png)

1. Après avoir créé/localisé votre application, recherchez les paramètres de l’application et téléchargez le SDK souhaité.

   ![image alternative](assets/download-sdk.png)

>[!WARNING]
>
> Si vous n’avez pas accès à l’interface marketing mobile, vous pouvez effectuer les changements directement dans le fichier de configuration du code de votre application. Toutefois, celui-ci ne sera pas synchronisé avec la page des paramètres de votre interface utilisateur.
