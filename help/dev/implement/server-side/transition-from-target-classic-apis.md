---
keywords: api, adobe i/o, classic, adobe developer console
description: Découvrez comment effectuer une transition à partir du [!DNL Adobe Target Classic] API à la variable [!DNL Target] API sur la [!DNL Adobe Developer Console].
title: Comment effectuer une transition depuis [!DNL Target Classic] API vers [!DNL Target] API sur la [!DNL Adobe Developer Console]?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 34%

---

# Transition depuis [!DNL Target Classic] API vers [!DNL Target] API sur la [!DNL Adobe Developer Console]

Informations pour vous aider à effectuer la transition depuis le [!DNL Target Classic] API à la variable [!DNL Target] API sur la [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Avec la mise hors service de [!DNL Adobe Target Classic], les API connectées à votre [!DNL Target Classic] ont également été rendues indisponibles. Cet article vous aidera à effectuer votre transition [!DNL Target Classic] Intégrations basées sur des API à la variable [!DNL Target] API optimisées par le [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Pour plus d’informations sur [!DNL Target] API, voir [[!DNL Target] API](/help/dev/before-administer/target-api-overview.md). Pour plus d’informations sur [!DNL Target] SDK, voir [[!DNL Target] Mise en oeuvre côté serveur](/help/dev/implement/server-side/server-side-overview.md)

## Terminologie 

| Terme | Description |
|--- |--- |
| API classique | API liées à votre [!DNL Target Classic] compte . Les appels de ces API sont basés sur une authentification par nom d’utilisateur et mot de passe et utilisent le nom d’hôte `testandtarget.omniture.com`. Si vos appels API contiennent un nom d’utilisateur et un mot de passe dans l’URL de demande, vous devez passer à la variable [!DNL Adobe Developer Console] API. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | La variable [!DNL Adobe Developer Console] est la passerelle pour [!DNL Target] API. Ces API sont connectées à vos [!DNL Target Standard/Premium] compte . La variable [!DNL Target] API sur la [!DNL Adobe Developer Console] utiliser une [Authentification basée sur JWT](../../before-administer/configure-authentication.md), qui est la norme du secteur pour les API d’entreprise sécurisées. |

## Journal

Les API suivantes ont été mises hors service lors de la [!DNL Target Classic] a été mis hors service :

| Date | Détails |
|--- |--- |
| 17 octobre 2017 | Toutes les méthodes API qui exécutent une opération d’écriture (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` et `setCampaignState`) ont été déclassées.<P>Il s’agit de la même date à laquelle toutes les [!DNL Target Classic] Les comptes d’utilisateurs ont été définis sur le statut en lecture seule. |
| 14 novembre 2017 | Les API restantes ont été déclassées. Il s’agit de la date à laquelle la variable [!DNL Target Classic] L’interface utilisateur a été désactivée |

[!DNL Recommendations Classic] Les API n’ont pas été affectées par cette chronologie.

## Méthodes équivalentes

Le tableau suivant répertorie l’équivalent [!DNL Adobe Developer Console] Méthodes d’API pour les méthodes d’API Classic. La variable [!DNL Adobe Developer Console] Les API renvoient JSON, tandis que les API classiques renvoient du code XML.

La variable [!DNL Adobe Developer Console] Les méthodes d’API sont liées à la section correspondante dans le site de documentation de l’API. Un exemple est fourni pour chaque méthode d’API. Vous pouvez également utiliser la variable [!DNL Target] Collection Postman de l’API d’administration qui contient des exemples d’appels API pour toutes les méthodes API d’Adobe sur la [!DNL Adobe Developer Console].

| Groupement | Méthode d’API classique | [!DNL Adobe Developer Console] Méthode d’API | Remarques |
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
|  | Rapport d’audit | [Obtention d’un rapport d’audit](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | Rapport de contenu 1-1 | [Obtenir un rapport sur les performances AP](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Paramètres du compte | Obtention de groupes d’hôtes | [Liste des environnements](https://developers.adobetarget.com/api/#list-environments) |  |

## Exceptions

Si vous avez besoin d’une exception, contactez votre gestionnaire de succès client.

## Aide

Veuillez contacter [!DNL Adobe Target Client Care] (tt-support@adobe.com) si vous avez des questions ou avez besoin d’aide pour passer des API Classic aux [!DNL Target] API sur la [!DNL Adobe Developer Console].
