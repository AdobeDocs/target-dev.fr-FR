---
title: Considérations sur l’API de diffusion Adobe Target et limites connues
description: Quelles considérations et limites connues dois-je prendre en compte lors de l’utilisation de la variable [!UICONTROL API de diffusion Adobe Target]?
keywords: api de diffusion
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# Considérations et restrictions connues

* Il n’existe aucune authentification pour [!DNL Target] API de diffusion.
* Cette API ne traite pas les cookies ni les appels de redirection.
* Prise en charge de [!UICONTROL Automated Personalization] (AP) et [!UICONTROL Recommendations] activités : cette API dispose de deux modes pour récupérer le contenu : le mode d’exécution et de prérécupération. Le mode de prérécupération ne peut être utilisé que pour [!UICONTROL Test AB] et [!UICONTROL Ciblage d’expérience] (XT). N’utilisez pas le mode de prérécupération pour [!UICONTROL Automated Personalization] (AP), [!UICONTROL Affectation automatique], [!UICONTROL Ciblage automatique], ou [!UICONTROL Recommendations] types d’activité.
* Les noms d’en-tête HTTP/1.1 et HTTP/2 ne sont pas sensibles à la casse. Cependant, HTTP/2 applique les noms d’en-tête en minuscules. Pour plus d’informations, voir [Documentation du protocole de transfert hypertexte version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si vous utilisez un point de terminaison qui achemine les visiteurs via notre nouvelle infrastructure d’équilibreur de charge, leurs connexions sont automatiquement mises à niveau vers HTTP/2. Ce processus de mise à niveau convertit les en-têtes de requête en en en en-têtes minuscules afin qu’ils ne soient pas considérés comme incorrects.

  Ce problème peut être un problème pour les clients si leurs bibliothèques sont configurées pour rechercher des en-têtes de requête/réponse sensibles à la casse (et plus particulièrement pas en minuscules).
