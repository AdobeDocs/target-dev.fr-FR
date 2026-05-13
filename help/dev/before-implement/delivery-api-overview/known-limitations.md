---
title: Considérations sur l’API de diffusion Adobe Target et limites connues
description: Quelles considérations et limites connues dois-je prendre en compte lors de l’utilisation du [!UICONTROL Adobe Target Delivery API] ?
keywords: API de diffusion
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/LCgGZONQpYfw6JxNCNc2Iu13Mft8Zfx-3Uxvm2EeUVk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 7%

---

# Considérations et limites connues

Les informations suivantes répertorient les considérations et les limites connues liées à l’utilisation du [!DNL Delivery API] [!DNL Adobe Target].

* Il n’existe aucune authentification pour les API de diffusion [!DNL Target].
* Cette API ne traite pas les cookies ni les appels de redirection.
* Les noms d’en-tête HTTP/1.1 et HTTP/2 ne respectent pas la casse ; toutefois, HTTP/2 applique les noms d’en-tête en minuscules. Pour plus d’informations, consultez la documentation [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si vous utilisez un point d’entrée qui achemine les visiteurs via notre nouvelle infrastructure d’équilibreur de charge, leurs connexions sont automatiquement mises à niveau vers HTTP/2. Ce processus de mise à niveau convertit les en-têtes de requête en minuscules afin qu’ils ne soient pas considérés comme incorrects.

  Ce problème peut potentiellement se révéler problématique pour les clients si leurs bibliothèques sont configurées pour rechercher des en-têtes de requête/réponse sensibles à la casse (en particulier pas en minuscules).
