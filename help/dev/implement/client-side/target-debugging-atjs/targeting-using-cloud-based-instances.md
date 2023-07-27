---
keywords: instances cloud, liste de suffixes publics, suffixe public, cookie, cookie propriétaire, cookie propriétaire, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, firebaseapp.com, herokuapp.com,,, aucuns, targetGlobalSettings, cookieDomain, instances cloud5, instances cloud6, instances cloud7, instances cloud8, instances cloud9, liste de suffixes publics0, liste de suffixes publics1, liste de suffixes publics2, liste3, liste de suffixes publics liste de suffixes publics5
description: Explorez les problèmes (avec les solutions) auxquels les clients sont confrontés lors de l’utilisation d’instances basées sur le cloud pour tester [!DNL Adobe Target] ou à des fins de preuve de concept.
title: Puis-Je Utiliser [!DNL Target] avec les instances basées sur le cloud ?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 49%

---

# Utilisation d’instances basées sur le cloud avec [!DNL Target]

Informations sur des problèmes que rencontrent les clients lors de l’utilisation d’instances basées sur le cloud pour tester [!DNL Adobe Target].

Les clients de [!DNL Target] utilisent parfois des instances basées sur le cloud avec [!DNL Target] à des fins de test ou de preuve de concept. Ces instances peuvent inclure les domaines suivants :

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com`, ou `firebaseapp.com`

Ces domaines, et de nombreux autres, font partie de la [liste des suffixes publics](https://publicsuffix.org/list/public_suffix_list.dat).

**Problème :** Les navigateurs modernes n’enregistrent pas les cookies si vous utilisez ces domaines.

La bibliothèque JavaScript at.js utilise des cookies pour effectuer le suivi des utilisateurs afin de s’assurer que [!DNL [!DNL Target]] présente toujours une expérience cohérente. Si la variable [!DNL Target] La bibliothèque JavaScript ne peut pas enregistrer les cookies, les requêtes Target sont désactivées.

**Solution :** Pour respecter les bonnes pratiques, si vous envisagez d’utiliser des instances basées sur le cloud avec des domaines inclus dans la liste des suffixes publics, veillez à personnaliser le paramètre `cookieDomain`. Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
