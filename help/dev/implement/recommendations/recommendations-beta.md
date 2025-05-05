---
keywords: Recommendations, paramètres, préférences, secteur industriel vertical, filtrer les critères incompatibles, groupe d’hôtes par défaut, URL de base de la miniature, jeton API de recommandations,
description: Découvrez comment implémenter des activités [!UICONTROL Recommendations] dans  [!DNL Adobe Target].
title: Comment Mettre En Oeuvre Des Activités [!UICONTROL Recommendations] ?
feature: Recommendations
hidefromtoc: true
hide: true
exl-id: 0a9c9649-195b-44e2-987e-d02eaf98cc54
source-git-commit: aa032255222d92aeddd7238922eb450f1b6b93a0
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 20%

---

# Planification et implémentation de [!UICONTROL Recommendations]

Informations pour vous aider à planifier et à mettre en oeuvre [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>En plus de cet article, le [Guide du praticien d’entreprise Adobe Target](https://experienceleague.adobe.com/fr/docs/target/using/target-home){target=_blank} contient des informations détaillées sur [Target Recommendations](https://experienceleague.adobe.com/fr/docs/target/using/recommendations/recommendations){target=_blank}.

Avant de configurer votre première activité [!UICONTROL Recommendations] dans [!DNL Adobe Target], procédez comme suit :

1. [Implémentez [!UICONTROL Target]](#implement-target) sur les surfaces web et d&#39;application mobile que vous souhaitez utiliser pour capturer le comportement des utilisateurs et pour diffuser des recommandations.
1. [Configurez votre [!UICONTROL Recommendations] catalogue](#set-up-your-recommendations-catalog) de produits ou de contenu que vous souhaitez recommander à vos utilisateurs.
1. [Transmettez les informations comportementales et le contexte](#pass-behavioral-information-and-context) à [!DNL Target Recommendations] pour lui permettre de fournir des recommandations personnalisées.
1. [Configurer les exclusions globales](#configure-global-exclusions).
1. [Configurez les [!UICONTROL Recommendations] paramètres](#configure-recommendations-settings).
1. (Facultatif) [Administrez [!UICONTROL Recommendations] à l’aide des API d’administration](#administer-recommendations-using-admin-apis).

## 1. Implémentation [!UICONTROL Target]

[!DNL Target Recommendations] nécessite la mise en oeuvre de [!DNL Adobe Experience Platform Web SDK] ou at.js 0.9.2 (ou version ultérieure). Pour plus d’informations, consultez les [[!UICONTROL Target] guides de mise en oeuvre côté client](../client-side/overview.md) .

## 2. Configuration de votre catalogue [!UICONTROL Recommendations]

Pour fournir des recommandations de haute qualité, [!UICONTROL Target] doit connaître les produits ou le contenu que vous souhaitez recommander. Les catalogues incluent généralement trois types d’informations sur les articles recommandés. Supposons que vous recommandiez des films. Insérez les éléments suivants :

1. Données que vous souhaitez afficher pour l’utilisateur recevant la recommandation Vous pouvez, par exemple, afficher le nom du film et l’URL d’une miniature de l’affiche.
1. Données qui s’avèrent utiles pour appliquer des contrôles marketing et de marchandisage Par exemple, vous pouvez afficher la note du film afin de ne pas recommander de films NC-17.
1. Données utiles pour déterminer la similarité d’éléments avec d’autres éléments d’éléments. Vous pouvez, par exemple, afficher le genre du film et le réalisateur du film.

[!UICONTROL Target] offre plusieurs options d’intégration pour remplir votre catalogue. Ces options peuvent être utilisées conjointement pour mettre à jour différents éléments du catalogue ou pour mettre à jour différents attributs d’élément sur différentes fréquences.

| Méthode | Qu’est-ce que c’est ? | Quand l’utiliser | Informations supplémentaires |
| --- | --- | --- | --- |
| Flux de catalogue | Planifiez un flux (CSV, [!DNL Google] Product XML ou [!UICONTROL Analytics Product Classifications]) à charger et à ingérer quotidiennement. | Pour envoyer des informations sur plusieurs éléments à la fois. Pour envoyer des informations qui changent rarement. | Voir [Flux](https://experienceleague.adobe.com/fr/docs/target/using/recommendations/entities/feeds). |
| API Entités | Appelez une API pour envoyer des mises à jour instantanées pour un seul élément. | Pour envoyer des mises à jour lorsqu’elles surviennent sur un élément à la fois. Pour envoyer des informations qui changent fréquemment (par exemple, le prix, le stock/le niveau de stock). | Consultez la [documentation destinée aux développeurs de l’API Entities](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Transmission des mises à jour sur la page | Envoyez les mises à jour instantanées d’un seul élément à l’aide de JavaScript sur la page ou de l’API de diffusion. | Pour envoyer des mises à jour lorsqu’elles surviennent sur un élément à la fois. Pour envoyer des informations qui changent fréquemment (par exemple, le prix, le stock/le niveau de stock). | Voir [ consultations d’éléments/pages de produits](#item-views-or-product-pages) ci-dessous. |

La plupart des clients doivent mettre en oeuvre au moins un flux. Vous pouvez ensuite choisir de compléter votre flux avec des mises à jour pour les attributs ou éléments fréquemment modifiés à l’aide de l’API Entités ou de la méthode sur la page.

## 3. Transmission des informations comportementales et du contexte

Les informations comportementales et le contexte que vous devez transmettre à [!UICONTROL Target] dépendent de l’action effectuée par votre visiteur, qui est souvent associée au type de page avec laquelle votre visiteur interagit.

### Consultations d’articles ou pages de produits

Sur les pages où un visiteur consulte un seul élément, comme une page des détails du produit, vous devez transmettre l’identité de l’élément que le visiteur consulte. Transmettez également la catégorie la plus granulaire de l’élément que le visiteur consulte, afin d’autoriser le filtrage des recommandations sur la catégorie actuelle.

Vous pouvez également transmettre certains attributs qui changent rapidement sur la page de produits elle-même. Par exemple, vous pouvez transmettre le prix (`value`) et le niveau stock/stock.

#### Prix et inventaire des transactions

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

Sur une page de catégorie, il est probable que vous souhaitiez limiter vos recommandations aux produits ou au contenu de cette catégorie. Pour ce faire, veillez à transmettre l’identité de la catégorie actuellement consultée.

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

Sur une page de panier, vous pouvez recommander des articles en fonction du contenu du panier actuel du visiteur. Pour ce faire, transmettez les identifiants de tous les éléments du panier actuel du visiteur à l’aide du paramètre spécial `cartIds`.

#### Transmission d’éléments actuellement dans le panier

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Pour plus d’informations sur les recommandations basées sur le panier, voir [Basé sur le panier](https://experienceleague.adobe.com/fr/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key#cart-based) dans le *[!DNL Adobe Target]Guide du praticien d’entreprise*.

### Exclure des éléments déjà présents dans le panier du visiteur

Sur les pages de votre site, vous pouvez exclure certains éléments des recommandations. Par exemple, vous pouvez ne pas recommander des articles qui se trouvent déjà dans le panier actuel du visiteur. Pour ce faire, transmettez les identifiants de tous les éléments que vous souhaitez exclure à l’aide du paramètre spécial `excludedIds`.

#### Transmettre des éléments à exclure

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Pages de confirmation des achats/commandes

Lorsqu’un événement d’achat se produit, transmettez l’identité du ou des articles achetés. Voir [Suivi des conversions](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) dans l’article [Déploiement d’at.js > Implémentation [!UICONTROL Target] sans gestionnaire de balises](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) .

## 4. Configuration des exclusions globales

Excluez tous les éléments à un niveau global que vous ne souhaitez jamais recommander à un visiteur. Voir [Exclusions](https://experienceleague.adobe.com/fr/docs/target/using/recommendations/entities/exclusions) dans le *[!DNL Adobe Target]Guide du praticien d’entreprise*.

## 5. Configuration des paramètres [!UICONTROL Recommendations]

Utilisez les paramètres pour gérer votre implémentation de [!UICONTROL Recommendations].

Pour accéder aux options **[!UICONTROL Recommendations Settings]**, ouvrez [!DNL Target] dans le [!DNL Adobe Experience Cloud], puis cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Recommendations]**.

![Page Paramètres Recommendations](/help/dev/implement/recommendations/assets/recs-settings-new.png)

Configurez les options suivantes :

### [!UICONTROL Recommendations API Token]

Les options suivantes sont disponibles dans la section [!UICONTROL Recommendations API Token] :

#### [!UICONTROL Client code]

[!DNL Target] [!UICONTROL client code].

Si vous ne connaissez pas votre [!UICONTROL client code], dans l’interface utilisateur de [!DNL Target], cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. La valeur [!UICONTROL client code] est affichée dans la section [!UICONTROL Account Details].

#### Jeton d’authentification

Les API d&#39;administration [!DNL Adobe Target], y compris les API [!DNL Recommendations Admin], sont sécurisées par l&#39;authentification pour s&#39;assurer que seuls les utilisateurs autorisés les utilisent pour accéder à [!DNL Adobe Target]. Utilisez [Adobe Developer Console](https://developer.adobe.com/console/home) pour gérer cette authentification pour tous les [!DNL Adobe Experience Cloud solutions], y compris [!DNL Adobe Target].

Pour plus d’informations, voir [Configuration de l’authentification pour les API Adobe Target](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>Soyez prudent lors de la génération d’un nouveau jeton d’authentification. La génération d’un nouveau jeton entraîne l’échec des appels API utilisant le jeton actuel. Mettez à jour les scripts ou les applications avec le nouveau jeton d’authentification généré.

### Critères

Connaître le secteur industriel vertical de votre site permet à Target de sélectionner des critères pour vos recommandations.

Les critères de [!DNL Recommendations] sont des règles qui déterminent quels produits ou contenu recommander selon un jeu prédéterminé de comportements de visiteurs. Les critères peuvent être basés sur les tendances populaires, les comportements actuels et passés d’un visiteur ou des produits et contenus similaires. Vous pouvez tester plusieurs types de recommandations les uns par rapport aux autres en ajoutant plusieurs critères.

Pour plus d’informations, voir [Critère](https://experienceleague.adobe.com/fr/docs/target/using/recommendations/criteria/algorithms){target=_blank} dans le *Guide du praticien Adobe Target Business.*

Les paramètres suivants sont disponibles dans la section [!UICONTROL Criteria] :

#### [!UICONTROL Industry/Vertical]

Le secteur industriel vertical permet de classer les critères de recommandations. Ces informations aident les membres de votre équipe à trouver des critères logiques pour une page spécifique, tels que les critères les mieux adaptés à la page du panier ou à une page multimédia.

Les catégories suivantes sont disponibles dans la liste déroulante :

* Aucun Personalization
* Vente au détail / commerce électronique
* Génération de piste / B2B / Services financiers
* Médias / Publication

#### [!UICONTROL Filter Incompatible Criteria]

Activez cette option pour afficher uniquement les critères pour lesquels la page sélectionnée transmet les données requises. Tous les critères ne s’exécutent pas correctement sur chaque page. La page ou la mbox doit transmettre `entity.id` ou `entity.categoryId` pour que les recommandations d’élément/de catégorie actuel(le) soient compatibles.

En général, il est préférable de n’afficher que les critères compatibles. Toutefois, si vous souhaitez que des critères incompatibles soient disponibles pour l’activité, n’activez pas cette option.

Adobe recommande de désactiver cette option si vous utilisez une solution de gestion des balises.

Pour plus d’informations sur cette option, voir [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/fr/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} dans le *[!DNL Adobe Target]Guide du praticien professionnel*.

### [!UICONTROL Product Catalog]

Les options suivantes sont disponibles dans la section [!UICONTROL Product Catalog] :

#### [!UICONTROL Default Host Group]

Sélectionnez votre groupe d’hôtes par défaut.

Le groupe d’hôtes peut servir à séparer les éléments disponibles dans votre catalogue pour différents usages. Par exemple, vous pouvez utiliser des groupes d’hôtes pour les environnements de développement et de production, des marques différentes ou plusieurs zones géographiques. Par défaut, les résultats d’aperçu dans la recherche de catalogue, les collections et les exclusions sont basés sur le groupe d’hôtes par défaut. (Vous pouvez également sélectionner un autre groupe d’hôtes pour prévisualiser les résultats à l’aide du filtre Environnement.) Par défaut, les éléments nouvellement ajoutés sont disponibles dans tous les groupes d’hôtes, sauf si un identifiant d’environnement est spécifié lors de la création ou de la mise à jour de l’élément. Les recommandations fournies dépendent du groupe d’hôtes spécifié dans la requête.

Si vos produits ne sont pas répertoriés, vérifiez que vous utilisez le groupe d’hôtes approprié. Si, par exemple, vous configurez votre recommandation pour utiliser un environnement d’évaluation et que vous définissez votre groupe d’hôtes sur Évaluation, il se peut que vous deviez recréer vos collections dans l’environnement d’évaluation pour les produits à afficher. Pour voir quels produits sont disponibles dans chaque environnement, utilisez la recherche catalogue pour chaque environnement. Vous pouvez également prévisualiser le contenu de [!UICONTROL Recommendations] collections et exclusions pour un environnement sélectionné (groupe d’hôtes).

>[!NOTE]
>
>Après avoir modifié l’environnement sélectionné, vous devez cliquer sur **[!UICONTROL Search]** pour mettre à jour les résultats renvoyés.

Le filtre **[!UICONTROL Environment]** est disponible à partir des emplacements suivants dans l’interface utilisateur de Target :

* Recherche catalogue (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)
* Collections (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]**)
* Boîte de dialogue Créer une collection (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create collection]**)
* Boîte de dialogue Mettre à jour la collection (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)
* Boîte de dialogue Créer une exclusion (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create exclusion]**)
* Boîte de dialogue Mettre à jour l’exclusion (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)

Pour plus d’informations, voir [Hôtes](https://experienceleague.adobe.com/fr/docs/target/using/administer/hosts){target=_blank} dans le *[!DNL Adobe Target]Guide du praticien d’entreprise*.

#### [!UICONTROL Thumbnail Base]

La définition d’une URL de base pour votre catalogue de produits rend possible l’utilisation d’URL relatives lors de la spécification de miniatures de vos produits lors du transfert de votre URL de miniature.

Par exemple :

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

définit une URL relative à l’URL de base de la miniature.

### [!UICONTROL Custom Attribute Key Configuration]

Axer vos recommandations sur un élément stocké dans le profil du visiteur. Par exemple, &quot;dernier élément ajouté au panier&quot; ou &quot;dernière vidéo visionnée à 90 % ou plus&quot;.

Cliquez sur **[!UICONTROL Add]** pour créer une configuration, indiquez un nom pour la configuration, sélectionnez l’attribut de profil souhaité, puis cliquez sur **[!UICONTROL Save]**.

## 6. (Facultatif) Administrez [!UICONTROL Recommendations] à l’aide des API d’administration

Consultez le guide pratique [ Utilisation des API [!UICONTROL Recommendations]](../../before-administer/recs-api/overview.md) pour découvrir comment configurer et utiliser les API d’administration et de diffusion [!UICONTROL Target] pour [!UICONTROL Recommendations].
