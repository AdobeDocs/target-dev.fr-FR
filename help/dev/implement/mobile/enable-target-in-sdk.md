---
keywords: application mobile, application mobile sdk, application mobile target, sdk target mobile, sdk d’application mobile, activer target dans sdk
description: Découvrez comment ajouter le SDK Mobile Services Adobe à votre application mobile.
title: Comment activer [!DNL Target] dans le  [!DNL Adobe Mobile SDK] ?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 29%

---

# Activation de [!DNL Target] dans le SDK

Ajoutez le [!UICONTROL Adobe Mobile Services SDK] à votre application.

>[!IMPORTANT]
>
>Prise en charge de la version 4 de [!DNL Adobe Mobile].Les SDK *x* ont pris fin le 31 août 2021 et ne sont plus recommandés pour les utilisateurs mobiles [!DNL Adobe Target].
>
>Le [SDK Adobe Experience Platform pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les services et solutions [!DNL Adobe Experience Cloud] de vos applications mobiles.

1. Si vous n’avez pas encore installé le SDK Adobe Mobile Services dans votre application, utilisez vos informations d’identification Analytics ou Experience Cloud et téléchargez le SDK à partir du site Web [Adobe Mobile Services](https://mobilemarketing.adobe.com/).

1. Ajoutez le [!DNL Adobe Mobile Services SDK] à votre application.

   Les instructions sont disponibles sous [Mise en œuvre principale et cycle de vie](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html?lang=fr).

1. Ajoutez le code client, le délai et activez SSL.

   Dans l’Experience Cloud, ouvrez Mobile Services, puis accédez à **[!UICONTROL Manage App Settings]** > **[!UICONTROL SDK Target Options]**.

   Ajoutez votre code client [!DNL Target] et votre délai d’expiration. Le code client est spécifique à votre compte ou entreprise. Le délai d’expiration est le temps en secondes pendant lequel [!DNL Target] attend une réponse avant d’afficher le contenu par défaut. Assurez-vous que l’option **[!UICONTROL Use HTTPS]** est cochée sur la page Gérer les paramètres de l’application dans Adobe Mobile Services. Si HTTPS n’est pas activé, tous les appels dans iOS9+ seront bloqués, sauf si vous placez sur la liste autorisée le serveur [!DNL Target].

   ![alt image](assets/mobile-clientcode.png)

1. Après avoir créé/localisé votre application, recherchez les paramètres de l’application et téléchargez le SDK souhaité.

   ![alt image](assets/download-sdk.png)

>[!WARNING]
>
> Si vous n’avez pas accès à l’interface marketing mobile, vous pouvez effectuer les changements directement dans le fichier de configuration du code de votre application. Toutefois, celui-ci ne sera pas synchronisé avec la page des paramètres de votre interface utilisateur.
