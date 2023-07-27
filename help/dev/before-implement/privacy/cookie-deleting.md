---
keywords: cookie, cookies, supprimer un cookie, supprimer [!DNL Target] cookie, google chrome, chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: Découvrez comment supprimer votre [!DNL Target] des cookies de navigateur afin que vous puissiez valider vos expériences.
title: Comment supprimer la variable [!DNL Target] Cookie ?
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 4%

---

# Supprimez le [!DNL Target] cookie

Vous pouvez supprimer vos [!DNL Adobe Target] le cookie du navigateur (mbox) afin que vous puissiez valider toutes vos expériences lors du test.

S’il n’existe pas [!DNL Target] (mbox), vous êtes considéré comme un nouveau visiteur et vous avez une nouvelle expérience. Il existe plusieurs manières de supprimer votre mbox sans supprimer l’ensemble des cookies de navigateur.

>[!NOTE]
>
>Les instructions suivantes sont correctes pour les navigateurs et les versions répertoriés. Recherchez sur Internet des instructions relatives à votre navigateur ou version spécifique.

## Supprimez le [!DNL Target] cookie depuis Google Chrome

Version 84.0.4147.105

1. Cliquez sur le bouton **[!UICONTROL Chrome]** menu > **[!UICONTROL Préférences]**.
1. Cliquez sur le bouton **[!UICONTROL Confidentialité et sécurité]** .
1. Cliquez sur **[!UICONTROL Cookies et autres données de site]**.
1. Cliquez sur **[!UICONTROL Afficher tous les cookies et les données du site]**.
1. Développez l’objet `adobe.com` , sélectionnez **mbox** , puis cliquez sur l’icône de suppression (X).

## Supprimez le [!DNL Target] cookie de Mozilla Firefox

Version 79.0

### Supprimer tous les cookies associés à `adobe.com`

1. Cliquez sur le bouton **[!UICONTROL Firefox]** menu > **[!UICONTROL Préférences]**.
1. Cliquez sur le bouton **[!UICONTROL Confidentialité et sécurité]** .
1. Sous **Cookies et données du site*, cliquez sur **[!UICONTROL Gérer les données]**.
1. Sélectionnez la variable `adobe.com` site, puis cliquez sur **[!UICONTROL Supprimer la sélection]**.

>[!WARNING]
>
>Cette opération supprime tous les cookies associés à la variable `adobe.com` site. Si vous souhaitez supprimer un cookie individuel d’un site, suivez les instructions ci-dessous.

### Suppression d’un cookie individuel (mbox)

1. Dans Firefo, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Développeur web]** > **[!UICONTROL Inspecteur de stockage]**.
1. Cliquez sur le bouton **[!UICONTROL Avancé]** .
1. Accédez à la page web qui contient le cookie que vous souhaitez supprimer.
1. Développez l’objet **[!UICONTROL Cookies]** , puis cliquez sur `https://experience.adobe.com`.
1. Cliquez avec le bouton droit de la souris sur le **[!UICONTROL mbox]** , puis cliquez sur **[!UICONTROL Supprimer]**.

## Supprimez le [!DNL Target] cookie de Microsoft Edge

Version 84.0.522.52

1. Cliquez sur le bouton **[!UICONTROL Microsoft Edge]** menu > **[!UICONTROL Préférences]**.
1. Cliquez sur le bouton **[!UICONTROL Autorisations du site]** .
1. Cliquez sur **[!UICONTROL Cookies et données du site]**.
1. Cliquez sur **[!UICONTROL Afficher tous les cookies et les données du site]**.
1. Développez l’objet `adobe.com` , sélectionnez **mbox** , puis cliquez sur l’icône de suppression (X).

## Supprimez le [!DNL Target] cookie depuis Apple Safari

Version 13.1.2

### Supprimer tous les cookies associés à `adobe.com`

1. Cliquez sur le bouton **[!UICONTROL Safari]** menu > **[!UICONTROL Préférences]**.
1. Cliquez sur le bouton **[!UICONTROL Privacy]** .
1. Cliquez sur **[!UICONTROL Gérer les données du site web]**.
1. Sélectionnez les sites des cookies que vous souhaitez supprimer, puis cliquez sur **[!UICONTROL Supprimer]**.

>[!WARNING]
>
>Cette opération supprime tous les cookies associés à la variable `adobe.com` site. Si vous souhaitez supprimer un cookie individuel d’un site, suivez les instructions ci-dessous.

### Suppression d’un cookie individuel (mbox)

1. Cliquez sur le bouton **[!UICONTROL Safari]** menu > **[!UICONTROL Préférences]**.
1. Cliquez sur le bouton **[!UICONTROL Avancé]** .
1. Sélectionnez la variable **[!UICONTROL Afficher le menu Développer dans la barre de menus]** .
1. Accédez à la page web qui contient le cookie que vous souhaitez supprimer.
1. Cliquez sur le bouton **[!UICONTROL Développer]** menu > **[!UICONTROL Afficher l’Inspecteur Web]**.
1. Cliquez sur le bouton **[!UICONTROL Stockage]** .
1. Développez l’objet **[!UICONTROL Cookies]** , puis cliquez sur `www.adobe.com`.
1. Cliquez avec le bouton droit de la souris sur le **mbox** , puis cliquez sur **[!UICONTROL Supprimer]**.
