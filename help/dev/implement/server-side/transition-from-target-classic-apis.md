---
keywords: api, adobe i/o, classic, adobe developer console
description: Découvrez comment passer des  [!DNL Adobe Target Classic]  API aux  [!DNL Target]  API sur le  [!DNL Adobe Developer Console].
title: Comment effectuer une transition de [!DNL Target Classic] API vers [!DNL Target] API sur le  [!DNL Adobe Developer Console] ?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# Transition des API [!DNL Target Classic] vers les API [!DNL Target] sur le [!DNL Adobe Developer Console]

Informations pour vous aider à passer des API [!DNL Target Classic] aux API [!DNL Target] sur le [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Avec la mise hors service de [!DNL Adobe Target Classic], les API connectées à votre compte [!DNL Target Classic] ont également été rendues indisponibles. Cet article vous aidera à faire la transition de vos intégrations basées sur l’API [!DNL Target Classic] vers les API [!DNL Target] optimisées par [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Pour plus d’informations sur les API [!DNL Target], voir [[!DNL Target] APIs](/help/dev/before-administer/target-api-overview.md). Pour plus d’informations sur les [!DNL Target] SDK, voir [[!DNL Target] Mise en oeuvre côté serveur](/help/dev/implement/server-side/server-side-overview.md)

## Terminologie 

| Terme | Description |
|--- |--- |
| API classique | API liées à votre compte [!DNL Target Classic]. Les appels de ces API sont basés sur une authentification par nom d’utilisateur et mot de passe et utilisent le nom d’hôte `testandtarget.omniture.com`. Si vos appels API contiennent un nom d’utilisateur et un mot de passe dans l’URL de demande, vous devez passer aux API [!DNL Adobe Developer Console]. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | [!DNL Adobe Developer Console] est la passerelle des API [!DNL Target]. Ces API sont connectées à votre compte [!DNL Target Standard/Premium]. Les API [!DNL Target] de [!DNL Adobe Developer Console] utilisent une [ authentification basée sur JWT ](../../before-administer/configure-authentication.md), qui est la norme du secteur pour les API d’entreprise sécurisées. |

## Journal

Les API suivantes ont été déclassées lorsque [!DNL Target Classic] a été mis hors service :

| Date | Détails |
|--- |--- |
| 17 octobre 2017 | Toutes les méthodes API qui exécutent une opération d’écriture (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` et `setCampaignState`) ont été déclassées.<P>Il s’agit de la date à laquelle tous les comptes d’utilisateurs [!DNL Target Classic] ont été définis sur le statut en lecture seule. |
| 14 novembre 2017 | Les API restantes ont été déclassées. Il s’agit de la date à laquelle l’interface utilisateur [!DNL Target Classic] a été désactivée. |

[!DNL Recommendations Classic] Les API n’ont pas été affectées par cette chronologie.

## Méthodes équivalentes

Le tableau suivant répertorie les méthodes d’API [!DNL Adobe Developer Console] équivalentes pour les méthodes d’API classiques. Les API [!DNL Adobe Developer Console] renvoient JSON, tandis que les API classiques renvoient du code XML.

Les méthodes d’API [!DNL Adobe Developer Console] sont liées à la section correspondante dans le site de documentation de l’API. Un exemple est fourni pour chaque méthode d’API. Vous pouvez également utiliser la collection Postman d’API d’administration [!DNL Target] qui contient des exemples d’appels API pour toutes les méthodes d’API d’Adobe sur [!DNL Adobe Developer Console].

| Groupement | Méthode d’API classique | Méthode d’API [!DNL Adobe Developer Console] | Remarques |
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

Contactez [!DNL Adobe Target Client Care] (tt-support@adobe.com) si vous avez des questions ou si vous avez besoin d’aide pour passer des API Classic aux API [!DNL Target] sur le [!DNL Adobe Developer Console].
