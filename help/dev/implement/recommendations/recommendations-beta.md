---
keywords: Recommendations, paramètres, préférences, secteur vertical, critères de filtrage incompatibles, groupe d’hôtes par défaut, URL de base de pouces, jeton d’API Recommendations,
description: Découvrez comment implémenter [!UICONTROL Recommendations] activités dans  [!DNL Adobe Target].
title: Comment Mettre En Œuvre [!UICONTROL Recommendations] Activités ?
feature: Recommendations
hide: true
exl-id: 0a9c9649-195b-44e2-987e-d02eaf98cc54
TQID: https://experienceleague.adobe.com/A7j0oJbyO3oei-a2l02I58o9I0vCPrRcqWC-QgQUxBo
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
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 1644
ht-degree: 18%

---

# Planification et implémentation de [!UICONTROL Recommendations]

Informations destinées à vous aider à planifier et à implémenter des [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Outre cet article, le [Guide du professionnel &#x200B;](https://experienceleague.adobe.com/en/docs/target/using/target-home){target=_blank} contient des informations détaillées sur [Target Recommendations](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations){target=_blank}.

Avant de configurer votre première activité [!UICONTROL Recommendations] dans [!DNL Adobe Target], procédez comme suit :

1. [Implémentez des [!UICONTROL Target]](#implement-target) sur les surfaces d’applications web et mobiles que vous souhaitez utiliser pour capturer le comportement des utilisateurs et fournir des recommandations.
1. [Configurez votre catalogue de [!UICONTROL Recommendations]](#set-up-your-recommendations-catalog) de produits ou de contenu que vous souhaitez recommander à vos utilisateurs.
1. [Transmettez des informations comportementales et contextuelles](#pass-behavioral-information-and-context) aux [!DNL Target Recommendations] afin de leur permettre de fournir des recommandations personnalisées.
1. [Configurer les exclusions globales](#configure-global-exclusions).
1. [Configurer [!UICONTROL Recommendations] paramètres](#configure-recommendations-settings).
1. (Facultatif) [Administrer des [!UICONTROL Recommendations] à l’aide des API d’administration](#administer-recommendations-using-admin-apis).

## &#x200B;1. Implémentation de [!UICONTROL Target]

[!DNL Target Recommendations] nécessite l’implémentation de [!DNL Adobe Experience Platform Web SDK] ou d’at.js 0.9.2 (ou version ultérieure). Pour plus d’informations[&#128279;](../client-side/overview.md) consultez les guides de mise en œuvre côté client [!UICONTROL Target] .

## &#x200B;2. Configurer votre catalogue [!UICONTROL Recommendations]

Pour fournir des recommandations de haute qualité, [!UICONTROL Target] devez connaître les produits ou le contenu que vous souhaitez recommander. Les catalogues incluent généralement trois types d’informations sur les éléments recommandés. Supposons que vous recommandiez des films. Inclure les éléments suivants :

1. Données que vous souhaitez afficher pour l’utilisateur recevant la recommandation Par exemple, vous pouvez afficher le nom de l’animation et l’URL d’une miniature de l’affiche de l’animation.
1. Données qui s’avèrent utiles pour appliquer des contrôles marketing et de marchandisage Par exemple, vous pouvez afficher la classification du film afin de ne pas recommander de films NC-17.
1. Données utiles pour déterminer la similitude des éléments avec d’autres éléments d’éléments. Par exemple, vous pouvez afficher le genre du film et le réalisateur du film.

[!UICONTROL Target] propose plusieurs options d’intégration pour renseigner votre catalogue. Ces options peuvent être utilisées conjointement pour mettre à jour différents articles du catalogue ou pour mettre à jour différents attributs d&#39;article à différentes fréquences.

| Méthode | Ce que c&#39;est | Quand l’utiliser | Informations supplémentaires |
| --- | --- | --- | --- |
| Flux de catalogue | Planifiez le chargement et l’ingestion quotidiens d’un flux (CSV, [!DNL Google] Product XML ou [!UICONTROL Analytics Product Classifications]). | Pour envoyer des informations sur plusieurs éléments à la fois. Pour envoyer des informations qui changent rarement. | Voir [Flux](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/feeds). |
| API des entités | Appelez une API pour envoyer des mises à jour à la minute près pour un seul élément. | Pour envoyer des mises à jour lorsqu’elles se produisent sur un élément à la fois. Pour envoyer des informations qui changent fréquemment (par exemple, le prix, le stock/le niveau de stock). | Consultez la [documentation destinée aux développeurs et développeuses de l’API Entities](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Transmission des mises à jour sur la page | Envoyez des mises à jour à la minute pour un seul élément à l’aide de JavaScript sur la page ou de l’API de diffusion. | Pour envoyer des mises à jour lorsqu’elles se produisent sur un élément à la fois. Pour envoyer des informations qui changent fréquemment (par exemple, le prix, le stock/le niveau de stock). | Voir [Pages de produits/consultations d’articles](#item-views-or-product-pages) ci-dessous. |

La plupart des clients doivent implémenter au moins un flux. Vous pouvez ensuite choisir de compléter votre flux par des mises à jour des attributs ou des éléments fréquemment modifiés à l’aide de l’API Entities ou de la méthode sur la page.

## &#x200B;3. Transmission d’informations comportementales et de contexte

Les informations comportementales et le contexte que vous devez transmettre à [!UICONTROL Target] dépendent de l’action entreprise par votre visiteur, qui est souvent associée au type de page avec laquelle il interagit.

### Vues d’éléments ou pages de produits

Sur les pages où un visiteur consulte un seul élément, comme la page des détails d’un produit, vous devez transmettre l’identité de l’élément que le visiteur consulte. Transmettez également la catégorie la plus granulaire de l’élément que le visiteur consulte, afin de permettre le filtrage des recommandations vers la catégorie actuelle.

Vous pouvez également transmettre certains attributs qui changent rapidement sur la page de produit elle-même. Par exemple, vous pouvez transmettre le prix (`value`) et le niveau de stock/stock.

#### Transmettre le prix et l’inventaire

```js {line-numbers="true"}
<script type="text/javascript">
function targetPageParams() { 
   return { 
      "entity": { 
         "id": "32323", 
         "categoryId": "running-shoes", 
         "value": 119.99, 
         "inventory": 329 
      } 
   } 
}
</script>
```

### Vues de catégorie/pages de catégorie

Sur une page de catégorie, vous souhaiterez probablement limiter vos recommandations aux produits ou au contenu de cette catégorie. Pour ce faire, veillez à transmettre l’identité de la catégorie actuellement consultée.

#### Transmettre la catégorie actuelle

```js {line-numbers="true"}
function targetPageParams() { 
   return { 
      "entity": { 
         "categoryId": "running-shoes" 
      } 
   } 
}
```

### Pages Ajouts au panier/consultations de panier/passage en caisse

Sur une page de panier, vous pouvez recommander des articles en fonction du contenu du panier actuel du visiteur. Pour ce faire, transmettez les identifiants de tous les articles du panier actuel du visiteur à l’aide du paramètre spécial `cartIds`.

#### Transmettre les articles actuellement dans le panier

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Pour plus d’informations sur les recommandations basées sur le panier, voir [Basées sur le panier](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key#cart-based) dans le Guide du professionnel *[!DNL Adobe Target]*.

### Exclure des éléments déjà présents dans le panier du visiteur

Sur toutes les pages de votre site, vous pouvez exclure certains éléments des recommandations. Par exemple, vous pouvez ne pas recommander d’articles qui se trouvent déjà dans le panier actuel du visiteur. Pour ce faire, transmettez les identifiants de tous les éléments que vous souhaitez exclure à l’aide du paramètre spécial `excludedIds`.

#### Transmettre les éléments à exclure

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Pages de confirmation des achats/commandes

Lorsqu’un événement d’achat se produit, transmettez l’identité du ou des articles achetés. Consultez la section [Suivi des conversions](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) dans l’article [Comment déployer at.js > Implémenter [!UICONTROL Target] sans gestionnaire de balises](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

## &#x200B;4. Configuration des exclusions globales

Excluez de la liste tous les éléments à un niveau global que vous ne souhaitez jamais recommander à un visiteur. Voir [Exclusions](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/exclusions) dans le Guide *[!DNL Adobe Target]du professionnel*.

## &#x200B;5. Configurer les paramètres [!UICONTROL Recommendations]

Utilisez les paramètres pour gérer votre implémentation de [!UICONTROL Recommendations].

Pour accéder aux options de **[!UICONTROL Recommendations Settings]**, ouvrez [!DNL Target] dans le [!DNL Adobe Experience Cloud], puis cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Recommendations]**.

![Page Paramètres Recommendations](/help/dev/implement/recommendations/assets/recs-settings-new.png)

Configurez les options suivantes :

### [!UICONTROL Recommendations API Token]

Les options suivantes sont disponibles dans la section [!UICONTROL Recommendations API Token] :

#### [!UICONTROL Client code]

La [!UICONTROL client code] [!DNL Target].

Si vous ne connaissez pas votre [!UICONTROL client code], dans l’interface utilisateur [!DNL Target], cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. Le [!UICONTROL client code] s’affiche dans la section [!UICONTROL Account Details] .

#### Jeton d’authentification

Les API [!DNL Adobe Target] Admin, y compris les API [!DNL Recommendations Admin], sont sécurisées par authentification afin de s’assurer que seuls les utilisateurs autorisés les utilisent pour accéder aux [!DNL Adobe Target]. Utilisez [&#128279;](https://developer.adobe.com/console/home) pour gérer cette authentification pour tous les [!DNL Adobe Experience Cloud solutions], y compris les [!DNL Adobe Target].

Pour plus d’informations, voir [Configuration de l’authentification pour les API Adobe Target](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>Soyez prudent lorsque vous générez un nouveau jeton d’authentification. La génération d’un nouveau jeton entraîne l’échec des appels API utilisant le jeton actuel. Mettez à jour les scripts ou les applications avec le nouveau jeton d’authentification généré.

### Critères

Connaître le secteur vertical de votre site permet à Target de choisir les critères de vos recommandations.

Les critères de [!DNL Recommendations] sont des règles qui déterminent quels produits ou contenus recommander selon un ensemble prédéterminé de comportements de visiteurs. Les critères peuvent être basés sur des tendances populaires, les comportements actuel et passé d’un visiteur ou des produits et contenus similaires. Vous pouvez tester plusieurs types de recommandations les uns par rapport aux autres en ajoutant plusieurs critères.

Pour plus d’informations, voir [Critères](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/algorithms){target=_blank} dans le *Guide du professionnel Adobe Target.*

Les paramètres suivants sont disponibles dans la section [!UICONTROL Criteria] :

#### [!UICONTROL Industry/Vertical]

Le secteur industriel vertical permet de classer les critères de recommandations. Ces informations aident les membres de votre équipe à trouver les critères pertinents pour une page particulière, tels que les critères les plus adaptés à la page du panier ou à une page multimédia.

Les catégories suivantes sont disponibles à partir de la liste déroulante :

* Aucun Personalization
* Vente au détail / commerce électronique
* Génération de piste / B2B / Services financiers
* Médias / Publication

#### [!UICONTROL Filter Incompatible Criteria]

Activez cette option pour afficher uniquement les critères pour lesquels la page sélectionnée transmet les données requises. Tous les critères ne s’exécutent pas correctement sur chaque page. La page ou la mbox doit être transmise `entity.id` ou `entity.categoryId` pour que les recommandations d’élément/de catégorie actuelles soient compatibles.

En général, il est préférable de n’afficher que les critères compatibles. Toutefois, si vous souhaitez que des critères incompatibles soient disponibles pour l’activité, n’activez pas cette option.

Adobe recommande de désactiver cette option si vous utilisez une solution de gestion des balises.

Pour plus d’informations sur cette option, voir [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} dans le Guide du professionnel *[!DNL Adobe Target]*.

### [!UICONTROL Product Catalog]

Les options suivantes sont disponibles dans la section [!UICONTROL Product Catalog] :

#### [!UICONTROL Default Host Group]

Sélectionnez votre groupe d’hôtes par défaut.

Le groupe d’hôtes peut servir à séparer les éléments disponibles dans votre catalogue pour différents usages. Par exemple, vous pouvez utiliser des groupes d’hôtes pour les environnements de développement et de production, des marques différentes ou différentes zones géographiques. Par défaut, les résultats d’aperçu dans la recherche de catalogue, les collections et les exclusions sont basés sur le groupe d’hôtes par défaut. (Vous pouvez également sélectionner un autre groupe d&#39;hôtes pour prévisualiser les résultats à l&#39;aide du filtre Environnement.) Par défaut, les nouveaux éléments ajoutés sont disponibles dans tous les groupes d’hôtes, sauf si un identifiant d’environnement est spécifié lors de la création ou de la mise à jour de l’élément. Les recommandations fournies dépendent du groupe d’hôtes spécifié dans la requête.

Si vos produits ne sont pas répertoriés, vérifiez que vous utilisez le groupe d’hôtes approprié. Si, par exemple, vous configurez votre recommandation pour utiliser un environnement d’évaluation et que vous définissez votre groupe d’hôtes sur Évaluation, il se peut que vous deviez recréer vos collections dans l’environnement d’évaluation pour les produits à afficher. Pour voir quels produits sont disponibles dans chaque environnement, utilisez la recherche catalogue pour chaque environnement. Vous pouvez également prévisualiser le contenu des collections et exclusions de [!UICONTROL Recommendations] pour un environnement sélectionné (groupe d’hôtes).

>[!NOTE]
>
>Après avoir modifié l’environnement sélectionné, vous devez cliquer sur **[!UICONTROL Search]** pour mettre à jour les résultats renvoyés.

Le filtre **[!UICONTROL Environment]** est disponible aux emplacements suivants de l’interface utilisateur de Target :

* Recherche catalogue (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)
* Collections (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]**)
* Boîte de dialogue Créer une collection (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create collection]**)
* Boîte de dialogue Mettre à jour la collection (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)
* Boîte de dialogue Créer une exclusion (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create exclusion]**)
* Boîte de dialogue Mettre à jour l’exclusion (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)

Pour plus d’informations, consultez [Hôtes](https://experienceleague.adobe.com/en/docs/target/using/administer/hosts){target=_blank} dans le Guide du professionnel *[!DNL Adobe Target]*.

#### [!UICONTROL Thumbnail Base]

La définition d’une URL de base pour votre catalogue de produits rend possible l’utilisation d’URL relatives lors de la spécification de miniatures de vos produits lors du transfert de votre URL de miniature.

Par exemple :

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

définit une URL relative à l’URL de base de la miniature.

### [!UICONTROL Custom Attribute Key Configuration]

Basez vos recommandations sur un élément stocké dans le profil du visiteur. Par exemple, « dernier élément ajouté au panier » ou « dernière vidéo visionnée à 90 % ou plus ».

Cliquez sur **[!UICONTROL Add]** pour créer une configuration, spécifiez un nom pour la configuration, sélectionnez l’attribut de profil souhaité, puis cliquez sur **[!UICONTROL Save]**.

## &#x200B;6. (Facultatif) Administration de [!UICONTROL Recommendations] à l’aide des API d’administration

Consultez le guide pratique [Utiliser les API [!UICONTROL Recommendations]](../../before-administer/recs-api/overview.md) pour savoir comment configurer et utiliser les API d’administration et de diffusion [!UICONTROL Target] pour les [!UICONTROL Recommendations].
