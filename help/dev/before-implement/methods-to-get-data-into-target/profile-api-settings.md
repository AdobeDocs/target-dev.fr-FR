---
keywords: implémentation, api, profil, paramètres d’api de profil, jeton d’authentification
description: Découvrez comment configurer l’authentification pour les mises à jour par lots via les API  [!DNL Adobe Target] et générer un jeton d’authentification de profil.
title: Comment utiliser les paramètres de l’API de profil pour activer ou désactiver les mises à jour par lots ?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 28%

---

# Paramètres de l’API de profil

Activez ou désactivez l’authentification pour les mises à jour par lots via les API [!DNL Adobe Target] et générez un jeton d’authentification de profil.

[!DNL Adobe Target] crée et conserve un profil pour chaque utilisateur individuel. Ce profil est stocké sur la grappe [!DNL Target] Edge et est mis à jour en temps réel après chaque visite. Vous pouvez également mettre à jour un profil individuellement ou en bloc via l’API.

Pour plus de sécurité, vous pouvez exiger que l’appel de l’API de mise à jour en bloc requiert un jeton d’accès valide à transmettre dans l’en-tête de la requête.

**Pour exiger une authentification et générer un jeton d’accès à l’aide de l’interface utilisateur [!DNL Target] :**

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Sous **[!UICONTROL Profile API]**, faites glisser la bascule **[!UICONTROL Require Authentication]** vers la position activée ou désactivée.

   ![alt image](assets/profile_api_settings.png)

1. (Conditionnel) Si vous avez activé l’exigence d’authentification, cliquez sur **[!UICONTROL Generate New Profile Authentication Token]**.

   ![alt image](assets/profile_api_settings_2.png)

   Le jeton expire selon l’heure indiquée dans la zone Expire dans .

   Vous devez disposer de l’une des autorisations utilisateur suivantes pour générer un jeton d’authentification :

   * Rôle d’administrateur ou au moins droits d’approbateur

     Pour plus d’informations sur les clients Target Standard, voir [Spécification des rôles et autorisations](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) dans *Utilisateurs*. Pour plus d’informations concernant les clients [!DNL Target Premium], consultez [Configuration des autorisations d’Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Rôle d’administrateur au niveau de l’espace de travail/du profil de produit

     Les espaces de travail sont disponibles uniquement pour les clients [!DNL Target Premium]. Pour plus d’informations, consultez [Configuration des autorisations d’Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Droits d’administrateur (autorisation Sysadmin) au niveau du produit [!DNL Adobe Target]

Vous pouvez également générer un jeton d’authentification de profil via l’API. Pour plus d’informations, voir &quot;Profils&quot; dans le [guide d’administration et d’API de profil Adobe Target](../../administer/admin-api/admin-api-overview-new.md).

1. Copiez le jeton et incluez-le dans l’en-tête de la requête au format : &quot;Authorization&quot; : &quot;Bearer&quot;.

1. Cliquez sur **[!UICONTROL Generate New Profile Authentication Token]** pour régénérer le jeton selon vos besoins.

>[!WARNING]
>
>La réinitialisation de ce jeton entraîne l’échec des appels d’API utilisant le jeton actuel. Vous devez, de ce fait, mettre à jour tous les scripts ou applications utilisant ce jeton.
