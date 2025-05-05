---
title: Présentation de l’API Adobe Target
description: Présentation des différentes API d’Adobe Target, notamment l’api de diffusion, l’api de création de rapports, l’api d’administration, l’api de profil, l’api de recommandations et les liens vers des collections postman.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Présentation de l’API Target

Cet article décrit les différentes API de Target en général, avant de se concentrer sur les exigences spécifiques aux API d’administration et de profil. Si vous souhaitez administrer Target via l’interface utilisateur, reportez-vous à la section [Administration du *Guide de l’utilisateur d’Adobe Target Business*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=fr).

## Types d’API

Les API Adobe Target sont un ensemble d’API qui alimentent les produits Adobe Target, comme Adobe Recommendations. Ces API permettent de créer des interfaces utilisateur riches en données que vous pouvez utiliser pour manipuler et intégrer des données.

Les API Adobe Target peuvent être regroupées en fonction du type : Admin, Profil, Diffusion et Création de rapports.

>[!NOTE]
>
>Les API d’administration et les API de profil sont souvent appelées collectivement (&quot;API d’administration et de profil&quot;), mais peuvent également être référencées séparément (&quot;API d’administration&quot; et &quot;API de profil&quot;). L’API Recommendations est une implémentation spécifique d’une API d’administration Target.

| Type d’API | Ce qu’il vous permet de faire | Lien de téléchargement | Autres liens utiles |
| --- | --- | --- |--- |
| [Admin](../administer/admin-api/admin-api-overview-new.md) | Créez, modifiez et supprimez des activités, des audiences, des offres et d’autres objets (y compris les entités Recommendations, les critères, les conceptions, etc.). Les API Recommendations sont un type d’API d’administration.) | <UL><li>[ Collection Postman de l’API d’administration Target ](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Collection Postman de l’API Recommendations](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [ Utilisation des API Recommendations](../before-administer/recs-api/overview.md) |
| Profil | Récupérez et modifiez les profils utilisateur stockés dans Adobe Target. | [ Collection Postman de l’API de profil Target ](https://developers.adobetarget.com/api/#profiles) |  |
| [Livraison](../implement/delivery-api/overview.md) | Récupérez du contenu optimisé et personnalisé de Target pour une diffusion à un utilisateur final. | [Collection Postman de l’API de diffusion cible](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [Création de rapports](../administer/admin-api/admin-api-overview-new.md) | Exporter les résultats des activités et d’autres résultats des rapports. | Les API de création de rapports sont incluses dans la [collection Postman de l’API d’administration Target](https://developers.adobetarget.com/api/#admin-postman-collection). |  |
| [Modèles](../administer/models-api/models-api-overview.md) | Gérez la liste des fonctionnalités que Target doit exclure de ses modèles d’apprentissage automatique (la &quot;liste bloquée&quot;). L’API Modèles est un type d’API d’administration, mais elle est répertoriée séparément en raison de ses opérations uniques par rapport aux objets (listes bloquées) non accessibles par le biais de l’interface utilisateur. |  |  |

## Différences entre les API

Il existe d’importantes différences entre les API d’administration de Target (y compris les API Recommendations) et les API de diffusion de Target :

* Les API d’administration vous permettent de configurer différents aspects de Target que vous pouvez également configurer dans l’interface utilisateur de Target. L’exception à cette règle est l’API Modèles, qui vous permet de configurer certains aspects de Target non disponibles dans l’interface utilisateur. Quoi qu&#39;il en soit, **toutes les API d&#39;administration nécessitent une authentification.**

* Les API de diffusion vous permettent de récupérer du contenu. Les API de diffusion ne nécessitent pas d’authentification.

Pour utiliser les API d’administration de Target, vous devez configurer l’authentification à l’aide de [Adobe Developer Console](https://developer.adobe.com/console/home). Pour plus d’informations, voir [Configuration de l’authentification](../before-administer/configure-authentication.md).
