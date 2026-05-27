---
keywords: application mobile, application mobile sdk, application mobile target, sdk target mobile, sdk d’application mobile, activer target dans sdk
description: Découvrez comment ajouter le SDK Adobe Mobile Services à votre application mobile.
title: Comment activer  [!DNL Target]  dans  [!DNL Adobe Mobile SDK] ?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 28%

---

# Activation du [!DNL Target] dans le SDK

Ajoutez le [!UICONTROL Adobe Mobile Services SDK] à votre application.

>[!IMPORTANT]
>
>La prise en charge des SDK [!DNL Adobe Mobile] version 4.*x* a pris fin le 31 août 2021 et n’est plus recommandée pour les utilisateurs d’[!DNL Adobe Target] mobile.
>
>[Adobe Experience Platform SDK pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les solutions et services [!DNL Adobe Experience Cloud] dans vos applications mobiles.

1. Si vous n’avez pas installé Adobe Mobile Services SDK dans votre application, utilisez vos informations d’identification Analytics ou Experience Cloud et téléchargez SDK à partir du site Web [Adobe Mobile Services](https://mobilemarketing.adobe.com/).

1. Ajoutez le [!DNL Adobe Mobile Services SDK] à votre application.

   Les instructions sont disponibles sous [Mise en œuvre principale et cycle de vie](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html?lang=fr).

1. Ajoutez le code client, le délai d’expiration et activez SSL.

   Dans Experience Cloud, ouvrez Mobile Services, puis accédez à **[!UICONTROL Manage App Settings]** > **[!UICONTROL SDK Target Options]**.

   Ajoutez votre code client [!DNL Target] et le délai d’expiration. Le code client est spécifique à votre compte ou entreprise. Le délai d’expiration est le temps, en nombre de secondes, pendant lequel [!DNL Target] attendez une réponse avant d’afficher le contenu par défaut. Assurez-vous que l’option **[!UICONTROL Use HTTPS]** est cochée dans la page Gérer les paramètres d’application d’Adobe Mobile Services. Si le protocole HTTPS n’est pas activé, tous les appels dans iOS9+ seront bloqués à moins que vous ne placiez sur la liste autorisée le serveur [!DNL Target].

   ![image alternative](assets/mobile-clientcode.png)

1. Une fois que vous avez créé/localisé votre application, recherchez les paramètres de l’application et téléchargez le SDK souhaité.

   ![image alternative](assets/download-sdk.png)

>[!WARNING]
>
> Si vous n’avez pas accès à l’interface marketing mobile, vous pouvez effectuer les changements directement dans le fichier de configuration du code de votre application. Toutefois, celui-ci ne sera pas synchronisé avec la page des paramètres de votre interface utilisateur.
