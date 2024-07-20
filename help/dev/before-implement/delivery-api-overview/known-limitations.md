---
title: Considérations sur l’API de diffusion Adobe Target et limites connues
description: Quelles considérations et limites connues dois-je prendre en compte lors de l’utilisation de [!UICONTROL Adobe Target Delivery API] ?
keywords: api de diffusion
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 49acf92bbe06dbcee36fef2b7394acd7ce37baad
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---

# Considérations et limites connues

* Il n’existe aucune authentification pour les API de diffusion [!DNL Target].
* Cette API ne traite pas les cookies ni les appels de redirection.
* Les noms d’en-tête HTTP/1.1 et HTTP/2 ne sont pas sensibles à la casse. Cependant, HTTP/2 applique les noms d’en-tête en minuscules. Pour plus d’informations, consultez la [documentation sur le protocole de transfert hypertexte version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si vous utilisez un point de terminaison qui achemine les visiteurs via notre nouvelle infrastructure d’équilibreur de charge, leurs connexions sont automatiquement mises à niveau vers HTTP/2. Ce processus de mise à niveau convertit les en-têtes de requête en en en en-têtes minuscules afin qu’ils ne soient pas considérés comme incorrects.

  Ce problème peut être un problème pour les clients si leurs bibliothèques sont configurées pour rechercher des en-têtes de requête/réponse sensibles à la casse (et plus particulièrement pas en minuscules).
