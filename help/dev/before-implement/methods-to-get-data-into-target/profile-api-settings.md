---
keywords: implémentation, api, profil, paramètres d’api de profil, jeton d’authentification
description: Découvrez comment configurer l’authentification pour les mises à jour par lots via  [!DNL Adobe Target]  API et générer un jeton d’authentification de profil.
title: Comment utiliser les paramètres de l’API Profile pour activer ou désactiver les mises à jour par lots ?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
TQID: https://experienceleague.adobe.com/-KYSphaCrm0ICK7g92v9x-uK--nwirs4-DWBR3G5rTM
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d095671a-1355-40aa-8b5f-06c33c68080bid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 347
ht-degree: 33%

---

# Paramètres de l’API de profil

Activez ou désactivez l’authentification pour les mises à jour par lots via les API [!DNL Adobe Target] et générez un jeton d’authentification de profil.

[!DNL Adobe Target] crée et conserve un profil pour chaque utilisateur. Ce profil est stocké sur le cluster Edge de [!DNL Target] et est mis à jour en temps réel après chaque visite. Vous pouvez également mettre à jour un profil individuellement ou en bloc via l’API.

Pour plus de sécurité, vous pouvez exiger que l’appel de l’API de mise à jour en masse requiert qu’un jeton d’accès valide soit transmis dans l’en-tête de la demande.

**Pour exiger une authentification et générer un jeton d’accès à l’aide de l’interface utilisateur [!DNL Target] :**

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Sous **[!UICONTROL Profile API]** diapositive, basculez le bouton **[!UICONTROL Require Authentication]** vers la position activée ou désactivée.

   ![image alternative](assets/profile_api_settings.png)

1. (Conditionnel) Si vous avez activé l’exigence d’authentification, cliquez sur **[!UICONTROL Generate New Profile Authentication Token]**.

   ![image alternative](assets/profile_api_settings_2.png)

   Le jeton expire en fonction de la durée répertoriée dans la zone Expire dans .

   Vous devez disposer de l’une des autorisations utilisateur suivantes pour générer un jeton d’authentification :

   * Rôle d’administrateur ou disposent au moins des droits d’approbateur

     Pour plus d’informations concernant les clients Target Standard, voir [Spécifier les rôles et autorisations](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) dans *Utilisateurs*. Pour plus d’informations concernant les clients [!DNL Target Premium], consultez [Configuration des autorisations d’Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Rôle d’administrateur au niveau de l’espace de travail/du profil de produit

     Les espaces de travail sont disponibles uniquement pour les clients [!DNL Target Premium]. Pour plus d’informations, consultez [Configuration des autorisations d’Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Droits d’administrateur (autorisation Sysadmin) au niveau du produit [!DNL Adobe Target]

Vous pouvez également générer un jeton d’authentification de profil via l’API. Pour plus d’informations, voir « Profils » dans le guide de l’[API d’administration et de profil ](../../administer/admin-api/admin-api-overview-new.md).

1. Copiez le jeton et incluez-le dans l’en-tête de la requête au format : « Authorization » : « Porteur ».

1. Cliquez sur **[!UICONTROL Generate New Profile Authentication Token]** pour régénérer le jeton si nécessaire.

>[!WARNING]
>
>La réinitialisation de ce jeton entraîne l’échec des appels d’API utilisant le jeton actuel. Vous devez, de ce fait, mettre à jour tous les scripts ou applications utilisant ce jeton.
