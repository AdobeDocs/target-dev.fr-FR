---
title: Considérations sur l’API de diffusion Adobe Target et limites connues
description: Quelles considérations et limites connues dois-je prendre en compte lors de l’utilisation du [!UICONTROL Adobe Target Delivery API] ?
keywords: api de diffusion
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 94a4122244065384f487ca9a29dfa1b414168cb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# Considérations et limites connues

Les informations suivantes répertorient les considérations et les limites connues liées à l’utilisation du [!DNL Adobe Target] [!DNL Delivery API].

* Il n’existe aucune authentification pour les API de diffusion [!DNL Target].
* Cette API ne traite pas les cookies ni les appels de redirection.
* Les noms d’en-tête HTTP/1.1 et HTTP/2 ne respectent pas la casse ; toutefois, HTTP/2 applique les noms d’en-tête en minuscules. Pour plus d’informations, consultez la documentation [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si vous utilisez un point d’entrée qui achemine les visiteurs via notre nouvelle infrastructure d’équilibreur de charge, leurs connexions sont automatiquement mises à niveau vers HTTP/2. Ce processus de mise à niveau convertit les en-têtes de requête en minuscules afin qu’ils ne soient pas considérés comme incorrects.

  Ce problème peut potentiellement se révéler problématique pour les clients si leurs bibliothèques sont configurées pour rechercher des en-têtes de requête/réponse sensibles à la casse (en particulier pas en minuscules).
