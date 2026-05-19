---
keywords: api, adobe i/o, classic, adobe developer console
description: Découvrez comment effectuer une transition des API  [!DNL Adobe Target Classic]  vers les API  [!DNL Target]  sur le  [!DNL Adobe Developer Console].
title: Comment passer des API  [!DNL Target Classic]  aux API  [!DNL Target]  sur le  [!DNL Adobe Developer Console] ?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
TQID: https://experienceleague.adobe.com/cIWcraU0O9Ut1VBbD5ScKOyBrXniyIEM5XEVZMJvffk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 595
ht-degree: 32%

---

# Transition des API [!DNL Target Classic] aux API [!DNL Target] sur le [!DNL Adobe Developer Console]

Informations destinées à vous aider à passer des API [!DNL Target Classic] aux API [!DNL Target] sur le [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Avec la mise hors service de [!DNL Adobe Target Classic], les API connectées à votre compte [!DNL Target Classic] ont également été rendues indisponibles. Cet article vous aidera à effectuer la transition de vos intégrations basées sur les API [!DNL Target Classic] vers les API [!DNL Target] optimisées par l’[[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) .

Pour plus d’informations sur les API [!DNL Target], voir [[!DNL Target] API](/help/dev/before-administer/target-api-overview.md). Pour plus d’informations sur les SDK [!DNL Target], voir [[!DNL Target] Implémentation côté serveur](/help/dev/implement/server-side/server-side-overview.md)

## Terminologie

| Terme | Description |
|--- |--- |
| API classique | API liées à votre compte [!DNL Target Classic]. Les appels de ces API sont basés sur une authentification par nom d’utilisateur et mot de passe et utilisent le nom d’hôte `testandtarget.omniture.com`. Si vos appels API contiennent un nom d’utilisateur et un mot de passe dans l’URL de la requête, vous devez passer aux API [!DNL Adobe Developer Console]. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | Le [!DNL Adobe Developer Console] est la passerelle pour les API [!DNL Target]. Ces API sont connectées à votre compte [!DNL Target Standard/Premium]. Les API [!DNL Target] sur le [!DNL Adobe Developer Console] utilisent une [&#x200B; authentification basée sur JWT](../../before-administer/configure-authentication.md), qui est la norme du secteur pour les API d’entreprise sécurisées. |

## Journal

Les API suivantes ont été mises hors service lors de la mise hors service de [!DNL Target Classic] :

| Date | Détails |
|--- |--- |
| 17 octobre 2017 | Toutes les méthodes API qui exécutent une opération d’écriture (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` et `setCampaignState`) ont été déclassées.<P>Il s’agit de la même date que celle à laquelle tous les comptes utilisateur [!DNL Target Classic] ont été définis en lecture seule. |
| 14 novembre 2017 | Les API restantes ont été déclassées. Il s’agit de la date de désactivation de l’interface utilisateur [!DNL Target Classic] |

Les API [!DNL Recommendations Classic] n’ont pas été affectées par cette chronologie.

## Méthodes équivalentes

Le tableau suivant répertorie les méthodes d’API [!DNL Adobe Developer Console] équivalentes pour les méthodes d’API classiques. Les API [!DNL Adobe Developer Console] renvoient le format JSON, tandis que les API classiques renvoient le format XML.

Les méthodes de l’API [!DNL Adobe Developer Console] sont liées à la section correspondante dans le site de documentation de l’API. Un exemple est fourni pour chaque méthode d’API. Vous pouvez également utiliser la Collection de Postman de l’API [!DNL Target] Admin qui contient des exemples d’appels API pour toutes les méthodes de l’API Adobe sur le [!DNL Adobe Developer Console].

| Groupement | Méthode API classique | Méthode API [!DNL Adobe Developer Console] | Remarques |
|--- |--- |--- |--- |
| Campagne/Activité | Création d’une campagne | [Création d’une activité AB](https://developers.adobetarget.com/api/#create-ab-activity)<P>[Création d’une activité XT](https://developers.adobetarget.com/api/#create-xt-activity) | Les nouvelles API fournissent des méthodes de création distinctes pour AB et XT. |
|  | Mise à jour d’une campagne | [Mise à jour d’une activité AB](https://developers.adobetarget.com/api/#update-ab-activity)<P>[Mise à jour d’une activité XT](https://developers.adobetarget.com/api/#update-xt-activity) |  |
|  | Copie d’une campagne | S.O. | Utilisez les API de création d’activités. |
|  | Liste des campagnes | [Liste des activités](https://developers.adobetarget.com/api/#list-activities) |  |
|  | État d’une campagne | [Mise à jour de l’état d’une activité](https://developers.adobetarget.com/api/#update-activity-state) |  |
|  | Affichage d’une campagne | [Obtention d’une activité AB par ID](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[Obtention d’une activité XT par ID](https://developers.adobetarget.com/api/#get-xt-activity-by-id) |  |
|  | ID de campagne tiers | S.O. | Si vous utilisez un paramètre thirdpartyID, les méthodes d’activité pertinentes peuvent être utilisées. |
| Offres | Création d’une offre | [Création d’une offre](https://developers.adobetarget.com/api/#create-offer) |  |
|  | Obtention d’une offre | [Obtention d’une offre par ID](https://developers.adobetarget.com/api/#get-offer-by-id) |  |
|  | Liste des offres | [Liste des offres](https://developers.adobetarget.com/api/#list-offers) |  |
|  | Liste des dossiers | S.O. | Les dossiers ne sont pas pris en charge dans [!DNL Target Standard/Premium] |
| Création de rapports | Rapport sur les performances d’une campagne | [Obtenir un rapport sur les performances AB](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[Obtenir un rapport sur les performances XT](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | Rapport d’audit | [Obtenir le rapport d’audit](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | Rapport de contenu 1-1 | [Obtenir un rapport sur les performances AP](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Paramètres du compte | Obtention de groupes d’hôtes | [Liste des environnements](https://developers.adobetarget.com/api/#list-environments) |  |

## Exceptions

Si vous avez besoin d’une exception, contactez votre gestionnaire de succès client.

## Aide

Veuillez contacter [!DNL Adobe Target Client Care] (tt-support@adobe.com) si vous avez des questions ou si vous avez besoin d’aide pour passer des API classiques aux API [!DNL Target] sur le [!DNL Adobe Developer Console].
