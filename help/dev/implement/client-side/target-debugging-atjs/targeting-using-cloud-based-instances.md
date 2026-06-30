---
keywords: instances cloud, liste des suffixes publics, suffixe public, cookie, cookie propriétaire, cookie propriétaire, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com, targetGlobalSettings, cookieDomain, instances cloud5, instances cloud6, instances cloud7, instances cloud8, instances cloud9, liste des suffixes publics0, liste des suffixes publics1, liste des suffixes publics2, liste des suffixes publics3, liste des suffixes publics4, liste des suffixes publics5
description: Explorez les problèmes (avec les solutions) auxquels les clients sont confrontés lorsqu’ils utilisent des instances basées sur le cloud à des fins de test [!DNL Adobe Target] ou de preuve de concept.
title: Puis [!DNL Target] je utiliser avec des instances basées sur le cloud ?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
TQID: https://experienceleague.adobe.com/df63sTQxukCfa4pYc1X6FRvxV3cY2UG-ixk5v9Fqh-c
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 203
ht-degree: 46%

---

# Utilisation d’instances basées sur le cloud avec [!DNL Target]

Informations sur des problèmes que rencontrent les clients lors de l’utilisation d’instances basées sur le cloud pour tester [!DNL Adobe Target].

Les clients de [!DNL Target] utilisent parfois des instances basées sur le cloud avec [!DNL Target] à des fins de test ou de preuve de concept. Ces instances peuvent inclure les domaines suivants :

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com`, ou `firebaseapp.com`

Ces domaines, et de nombreux autres, font partie de la [liste des suffixes publics](https://publicsuffix.org/list/public_suffix_list.dat).

**Problème :** Les navigateurs modernes n’enregistrent pas les cookies si vous utilisez ces domaines.

La bibliothèque JavaScript at.js utilise des cookies pour suivre les utilisateurs afin de s’assurer que [!DNL [!DNL Target]] présente toujours une expérience cohérente. Si la bibliothèque JavaScript [!DNL Target] ne peut pas enregistrer de cookies, les requêtes Target sont désactivées.

**Solution :** Pour respecter les bonnes pratiques, si vous envisagez d’utiliser des instances basées sur le cloud avec des domaines inclus dans la liste des suffixes publics, veillez à personnaliser le paramètre `cookieDomain`. Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).



