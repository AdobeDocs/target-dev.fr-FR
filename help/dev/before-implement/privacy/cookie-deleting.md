---
keywords: cookie, cookies, supprimer un cookie, supprimer [!DNL Target] cookie, google chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: Découvrez comment supprimer les cookies de navigateur  [!DNL Target] pour pouvoir valider vos expériences.
title: Comment supprimer le cookie  [!DNL Target] ?
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 3%

---

# Suppression du cookie [!DNL Target]

Vous pouvez supprimer le cookie de votre navigateur [!DNL Adobe Target] (mbox) afin de pouvoir valider toutes vos expériences lors du test.

S’il n’existe pas de cookie [!DNL Target] (mbox), vous êtes considéré comme un nouveau visiteur et une nouvelle expérience vous est présentée. Il existe plusieurs façons de supprimer votre mbox sans supprimer tous les cookies de navigateur.

>[!NOTE]
>
>Les instructions suivantes sont correctes pour les navigateurs et les versions répertoriés. Recherchez sur Internet des instructions relatives à votre navigateur ou version spécifique.

## Suppression du cookie [!DNL Target] de Google Chrome

Version 84.0.4147,105

1. Cliquez sur le menu **[!UICONTROL Chrome]** > **[!UICONTROL Preferences]**.
1. Cliquez sur l’onglet **[!UICONTROL Privacy and Security]** .
1. Cliquez sur **[!UICONTROL Cookies and other site data]**.
1. Cliquez sur **[!UICONTROL See all cookies and site data]**.
1. Développez la section `adobe.com`, sélectionnez le cookie **mbox**, puis cliquez sur l’icône de suppression (X).

## Suppression du cookie [!DNL Target] de Mozilla Firefox

Version 79.0

### Supprimer tous les cookies associés à `adobe.com`

1. Cliquez sur le menu **[!UICONTROL Firefox]** > **[!UICONTROL Preferences]**.
1. Cliquez sur l’onglet **[!UICONTROL Privacy and Security]** .
1. Sous **Cookies et données du site*, cliquez sur &#x200B;** [!UICONTROL Manage Data]**.
1. Sélectionnez le site `adobe.com`, puis cliquez sur **[!UICONTROL Remove Selected]**.

>[!WARNING]
>
>Cela supprime tous les cookies associés au site `adobe.com`. Si vous souhaitez supprimer un cookie individuel d’un site, suivez les instructions ci-dessous.

### Suppression d’un cookie individuel (mbox)

1. Dans Firefo, cliquez sur **[!UICONTROL Tools]** > **[!UICONTROL Web Developer]** > **[!UICONTROL Storage Inspector]**.
1. Cliquez sur l’onglet **[!UICONTROL Advanced]** .
1. Accédez à la page web qui contient le cookie que vous souhaitez supprimer.
1. Développez la section **[!UICONTROL Cookies]**, puis cliquez sur `https://experience.adobe.com`.
1. Cliquez avec le bouton droit sur le cookie **[!UICONTROL mbox]**, puis cliquez sur **[!UICONTROL Delete]**.

## Suppression du cookie [!DNL Target] de Microsoft Edge

Version 84.0.522.52

1. Cliquez sur le menu **[!UICONTROL Microsoft Edge]** > **[!UICONTROL Preferences]**.
1. Cliquez sur l’onglet **[!UICONTROL Site Permissions]** .
1. Cliquez sur **[!UICONTROL Cookies and site data]**.
1. Cliquez sur **[!UICONTROL See all cookies and site data]**.
1. Développez la section `adobe.com`, sélectionnez le cookie **mbox**, puis cliquez sur l’icône de suppression (X).

## Suppression du cookie [!DNL Target] d’Apple Safari

Version 13.1.2

### Supprimer tous les cookies associés à `adobe.com`

1. Cliquez sur le menu **[!UICONTROL Safari]** > **[!UICONTROL Preferences]**.
1. Cliquez sur l’onglet **[!UICONTROL Privacy]** .
1. Cliquez sur **[!UICONTROL Manage Website Data]**.
1. Sélectionnez les sites des cookies que vous souhaitez supprimer, puis cliquez sur **[!UICONTROL Remove]**.

>[!WARNING]
>
>Cela supprime tous les cookies associés au site `adobe.com`. Si vous souhaitez supprimer un cookie individuel d’un site, suivez les instructions ci-dessous.

### Suppression d’un cookie individuel (mbox)

1. Cliquez sur le menu **[!UICONTROL Safari]** > **[!UICONTROL Preferences]**.
1. Cliquez sur l’onglet **[!UICONTROL Advanced]** .
1. Sélectionnez l’option **[!UICONTROL Show Develop menu in menu bar]** .
1. Accédez à la page web qui contient le cookie que vous souhaitez supprimer.
1. Cliquez sur le menu **[!UICONTROL Develop]** > **[!UICONTROL Show Web Inspector]**.
1. Cliquez sur l’onglet **[!UICONTROL Storage]** .
1. Développez la section **[!UICONTROL Cookies]**, puis cliquez sur `www.adobe.com`.
1. Cliquez avec le bouton droit sur le cookie **mbox**, puis cliquez sur **[!UICONTROL Delete]**.
