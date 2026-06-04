---
title: Présentation de l’API Adobe Target
description: Présentation des différentes API d’Adobe Target, notamment l’api de diffusion, l’api de création de rapports, l’api d’administration, l’api de profil, l’api de recommandations et les liens vers les collections Postman.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/GbrWhrZxH-sTtpxotpJGbr-sHuIXrX7rZFQhju76-vM
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 448
ht-degree: 0%

---

# Présentation de l’API Target

Cet article décrit les différentes API de Target en général, avant de se concentrer sur les exigences spécifiques aux API d’administration et de profil. Si vous souhaitez administrer Target via l’interface utilisateur, consultez la section [ administration du *Guide d’utilisation d’Adobe Target Business*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).

## Types d’API

Les API Adobe Target sont un ensemble d’API qui alimentent les produits Adobe Target tels qu’Adobe Recommendations. Ces API permettent de créer des interfaces utilisateur riches en données que vous pouvez utiliser pour manipuler et intégrer des données.

Les API d&#39;Adobe Target peuvent être regroupées selon le type : Admin, Profil, Diffusion et Reporting.

>[!NOTE]
>
>Les API Admin et Profile sont souvent désignées collectivement (« API Admin et Profile »), mais peuvent également être désignées séparément (« API Admin » et « API Profile »). L’API Recommendations est une implémentation spécifique d’une API d’administration Target.

| Type d’API | Ce qu’il vous permet de faire | Lien de téléchargement | Autres liens utiles |
| --- | --- | --- |--- |
| [Admin](../administer/admin-api/admin-api-overview-new.md) | Créez, modifiez et supprimez des activités, des audiences, des offres et d’autres objets (y compris les entités Recommendations, les critères, les conceptions, etc.). Les API Recommendations sont un type d’API d’administration.) | <UL><li>[Collection Postman de l’API d’administration Target](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Collection Postman de l’API Recommendations](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [Utilisation des API Recommendations](../before-administer/recs-api/overview.md) |
| Profil | Récupérez et modifiez les profils utilisateur stockés dans Adobe Target. | [Collection Postman de l’API Profil Target](https://developers.adobetarget.com/api/#profiles) |  |
| [Livraison](../implement/delivery-api/overview.md) | Récupérez du contenu optimisé et personnalisé à partir de Target pour le diffuser à un utilisateur final. | [Collection Postman de l’API de diffusion Target](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [Création de rapports](../administer/admin-api/admin-api-overview-new.md) | Exportez les résultats des activités et d’autres résultats de rapports. | Les API de création de rapports sont incluses dans la [collection Postman de l’API Target Admin](https://developers.adobetarget.com/api/#admin-postman-collection). |  |
| [ Modèles ](../administer/models-api/models-api-overview.md) | Gérer la liste des fonctionnalités que Target doit exclure de ses modèles de machine learning (la « liste bloquée »). L’API Modèles est un type d’API d’administration, mais elle est répertoriée ici séparément en raison de ses opérations uniques sur des objets (places sur la liste bloquée) non accessibles via l’interface utilisateur. |  |  |

## Différences d’API

Il existe des différences importantes entre les API d’administration de Target (y compris les API Recommendations) et les API de diffusion de Target :

* Les API d’administration vous permettent de configurer divers aspects de Target que vous pouvez également configurer dans l’interface utilisateur de Target. L’exception à cette règle est l’API Modèles , qui vous permet de configurer des aspects de Target qui ne sont pas disponibles dans l’interface utilisateur. Quoi qu’il en soit, **toutes les API d’administration nécessitent une authentification.**

* Les API de diffusion permettent de récupérer du contenu. Les API de diffusion ne nécessitent pas d’authentification.

Pour utiliser les API d’administration Target, vous devez configurer l’authentification à l’aide de [](https://developer.adobe.com/console/home). Pour plus d’informations, voir [Configuration de l’authentification](../before-administer/configure-authentication.md).
