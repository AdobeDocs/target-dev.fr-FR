---
keywords: Recommendations, paramètres, préférences, secteur vertical, critères de filtrage incompatibles, groupe d’hôtes par défaut, URL de base de pouces, jeton d’API Recommendations, 9 $
description: Découvrez comment implémenter [!UICONTROL Recommendations] activités dans  [!DNL Adobe Target].
title: Comment Mettre En Œuvre [!UICONTROL Recommendations] Activités ?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
source-git-commit: 94a4122244065384f487ca9a29dfa1b414168cb8
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 21%

---

# Planification et implémentation de [!UICONTROL Recommendations]

Informations destinées à vous aider à planifier et à implémenter des [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Outre cet article, le [Guide du professionnel Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr){target=_blank} contient des informations détaillées sur [Target Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html){target=_blank}.

Avant de configurer votre première activité [!UICONTROL Recommendations] dans [!DNL Adobe Target], procédez comme suit :

1. [Implémentez des [!UICONTROL Target]](#implement-target) sur les surfaces d’applications web et mobiles que vous souhaitez utiliser pour capturer le comportement des utilisateurs et fournir des recommandations.
1. [Configurez votre catalogue de [!UICONTROL Recommendations]](#set-up-your-recommendations-catalog) de produits ou de contenu que vous souhaitez recommander à vos utilisateurs.
1. [Transmettez des informations comportementales et contextuelles](#pass-behavioral-information-and-context) aux [!DNL Target Recommendations] afin de leur permettre de fournir des recommandations personnalisées.
1. [Configurer les exclusions globales](#configure-global-exclusions).
1. [Configurer [!UICONTROL Recommendations] paramètres](#configure-recommendations-settings).
1. (Facultatif) [Administrer des [!UICONTROL Recommendations] à l’aide des API d’administration](#administer-recommendations-using-admin-apis).

## &#x200B;1. Implémenter [!UICONTROL Target]

[!DNL Target Recommendations] nécessite l’implémentation de Adobe Experience Platform Web SDK ou at.js 0.9.2 (ou version ultérieure). Pour plus d’informations[[!UICONTROL Target] consultez les guides de mise en œuvre côté client ](../client-side/overview.md) .

## &#x200B;2. Configurer votre catalogue [!UICONTROL Recommendations]

Pour fournir des recommandations de haute qualité, [!UICONTROL Target] devez connaître les produits ou le contenu que vous souhaitez recommander. Les catalogues incluent généralement trois types d’informations sur les éléments recommandés. Supposons que vous recommandiez des films. Inclure les éléments suivants :

1. Données que vous souhaitez afficher pour l’utilisateur recevant la recommandation Par exemple, vous pouvez afficher le nom de l’animation et l’URL d’une miniature de l’affiche de l’animation.
1. Données qui s’avèrent utiles pour appliquer des contrôles marketing et de marchandisage Par exemple, vous pouvez afficher la classification du film afin de ne pas recommander de films NC-17.
1. Données utiles pour déterminer la similitude des éléments avec d’autres éléments d’éléments. Par exemple, vous pouvez afficher le genre du film et le réalisateur du film.

[!UICONTROL Target] propose plusieurs options d’intégration pour renseigner votre catalogue. Ces options peuvent être utilisées conjointement pour mettre à jour différents articles du catalogue ou pour mettre à jour différents attributs d&#39;article à différentes fréquences.

| Méthode | Ce que c&#39;est | Quand l’utiliser | Informations supplémentaires |
| --- | --- | --- | --- |
| Flux de catalogue | Planifiez un flux (CSV, XML de produit Google ou classifications de produit Analytics) à charger et à ingérer quotidiennement. | Pour envoyer des informations sur plusieurs éléments à la fois. Pour envoyer des informations qui changent rarement. | Voir [Flux](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html). |
| API des entités | Appelez une API pour envoyer des mises à jour à la minute près pour un seul élément. | Pour envoyer des mises à jour lorsqu’elles se produisent sur un élément à la fois. Pour envoyer des informations qui changent fréquemment (par exemple, le prix, le stock/le niveau de stock). | Consultez la [documentation destinée aux développeurs et développeuses de l’API Entities](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Transmission des mises à jour sur la page | Envoyez des mises à jour à la minute pour un seul élément à l’aide de JavaScript sur la page ou de l’API de diffusion. | Pour envoyer des mises à jour lorsqu’elles se produisent sur un élément à la fois. Pour envoyer des informations qui changent fréquemment (par exemple, le prix, le stock/le niveau de stock). | Voir [Pages de produits/consultations d’articles](#item-views-or-product-pages) ci-dessous. |

>[!IMPORTANT]
>
>Soyez prudent lors de la mise à jour de vos [!DNL Recommendations] [!UICONTROL Catalog] via le [!DNL Delivery API]. Le [!DNL Delivery API] est public. Évitez donc de l’utiliser pour remplir les éléments cliquables de votre catalogue de recommandations. Vous risquez ainsi d’introduire du contenu non validé et de polluer votre catalogue.
>
>**Bonnes pratiques** : utilisez le [!DNL Delivery API] uniquement pour mettre à jour les attributs de catalogue qui :
>
>* Changez fréquemment (par exemple, le prix, le niveau des stocks).
>
>* Suivez un format prédéfini qui peut être facilement validé sur votre site web.
>
>* Ne l’utilisez pas pour ajouter ou modifier des éléments cliquables ou tout autre contenu non vérifié.
>
>* Si nécessaire, vous pouvez demander au service clientèle de désactiver les mises à jour du catalogue via l’API de diffusion.
>
>Pour plus d’informations, voir la documentation [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.

La plupart des clients doivent implémenter au moins un flux. Vous pouvez ensuite choisir de compléter votre flux par des mises à jour des attributs ou des éléments fréquemment modifiés à l’aide de l’API Entities ou de la méthode sur la page.

## &#x200B;3. Transmission d’informations comportementales et de contexte

Les informations comportementales et le contexte que vous devez transmettre à [!UICONTROL Target] dépendent de l’action entreprise par votre visiteur, qui est souvent associée au type de page avec laquelle il interagit.

### Vues d’éléments ou pages de produits

Sur les pages où un visiteur consulte un seul élément, comme la page des détails d’un produit, vous devez transmettre l’identité de l’élément que le visiteur consulte. Vous devez également transmettre la catégorie la plus granulaire de l’élément que le visiteur consulte, pour permettre le filtrage des recommandations sur la catégorie actuelle.

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

Pour plus d’informations sur les recommandations basées sur le panier, voir [Basées sur le panier](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based) dans le Guide du professionnel *[!DNL Adobe Target]*.

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

Excluez de la liste tous les éléments à un niveau global que vous ne souhaitez jamais recommander à un visiteur. Voir [Exclusions](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html) dans le Guide *[!DNL Adobe Target]du professionnel*.

## &#x200B;5. Configurer les paramètres [!UICONTROL Recommendations]

Utilisez les paramètres pour gérer votre implémentation de [!UICONTROL Recommendations].

Pour accéder aux options de **[!UICONTROL Recommendations Settings]**, ouvrez Target dans le [!DNL Adobe Experience Cloud], puis cliquez sur **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**.

![Page Paramètres Recommendations](/help/dev/implement/recommendations/assets/recs_settings.png)

Les options disponibles sont les suivantes :

| Paramètre | Description |
|--- |--- |
| Mbox globale personnalisée | (Facultatif) Indiquez la mbox globale personnalisée utilisée pour les activités [!UICONTROL Target]. Par défaut, la mbox globale utilisée par [!UICONTROL Target] est utilisée pour [!UICONTROL Recommendations].<P>Remarque : cette option est définie sur la page [!UICONTROL Target] **[!UICONTROL Administration]**. Ouvrez [!UICONTROL Target], puis cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**. |
| Secteur industriel vertical | Le secteur industriel vertical permet de classer les critères de recommandations. Ces informations aident les membres de votre équipe à trouver les critères pertinents pour une page particulière, tels que les critères les plus adaptés à la page du panier ou à une page multimédia. |
| Filtrer les critères incompatibles | Activez cette option pour afficher uniquement les critères pour lesquels la page sélectionnée transmet les données requises. Tous les critères ne s’exécutent pas correctement sur chaque page. La page ou la mbox doit être transmise `entity.id` ou `entity.categoryId` pour que les recommandations d’élément/de catégorie actuelles soient compatibles. En général, il est préférable de n’afficher que les critères compatibles. Néanmoins, si vous souhaitez que des critères incompatibles soient disponibles pour l’activité, décochez l’option.<P>Il est recommandé de désactiver cette option si vous utilisez une solution de gestion des balises.<P>Pour plus d’informations sur cette option, voir [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html) dans le Guide du professionnel *[!DNL Adobe Target]*. |
| Groupe d’hôtes par défaut | Sélectionnez votre groupe d’hôtes par défaut.<P>Le groupe d’hôtes peut servir à séparer les éléments disponibles dans votre catalogue pour différents usages. Par exemple, vous pouvez utiliser des groupes d’hôtes pour les environnements de développement et de production, des marques différentes ou plusieurs zones géographiques. Par défaut, les résultats d’aperçu dans la recherche de catalogue, les collections et les exclusions sont basés sur le groupe d’hôtes par défaut. (Vous pouvez également sélectionner un autre groupe d&#39;hôtes pour prévisualiser les résultats à l&#39;aide du filtre Environnement.) Par défaut, les nouveaux éléments ajoutés sont disponibles dans tous les groupes d’hôtes, sauf si un identifiant d’environnement est spécifié lors de la création ou de la mise à jour de l’élément. Les recommandations fournies dépendent du groupe d’hôtes spécifié dans la requête.<P>Si vos produits ne sont pas répertoriés, vérifiez que vous utilisez le groupe d’hôtes approprié. Si, par exemple, vous configurez votre recommandation pour utiliser un environnement d’évaluation et que vous définissez votre groupe d’hôtes sur Évaluation, il se peut que vous deviez recréer vos collections dans l’environnement d’évaluation pour les produits à afficher. Pour voir quels produits sont disponibles dans chaque environnement, utilisez la recherche catalogue pour chaque environnement. Vous pouvez également prévisualiser le contenu des collections et exclusions de [!UICONTROL Recommendations] pour un environnement sélectionné (groupe d’hôtes).<P>**Remarque :** après avoir modifié l’environnement sélectionné, vous devez cliquer sur Rechercher pour mettre à jour les résultats renvoyés.<P> **[!UICONTROL The Environment]** filtre est disponible aux emplacements suivants dans l’interface utilisateur de Target :<ul><li>Recherche catalogue (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)</li><li>Boîte de dialogue Créer une collection (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create New]**)</li><li>Boîte de dialogue Mettre à jour la collection (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)</li><li>Boîte de dialogue Créer une exclusion (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create New]**)</li><li>Boîte de dialogue Mettre à jour l’exclusion (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)</li></ul>Pour plus d’informations, consultez [Hôtes](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) dans le Guide du professionnel *[!DNL Adobe Target]*. |
| URL de base de la miniature | La définition d’une URL de base pour votre catalogue de produits rend possible l’utilisation d’URL relatives lors de la spécification de miniatures de vos produits lors du transfert de votre URL de miniature.<P>Par exemple :<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>définit une URL relative à l’URL de base de la miniature. |
| Jeton API [!UICONTROL Recommendations] | Utilisez ce jeton dans les appels API [!UICONTROL Recommendations], tels que l’API de téléchargement. |

## &#x200B;6. (Facultatif) Administration de [!UICONTROL Recommendations] à l’aide des API d’administration

Consultez le guide pratique [Utiliser les API [!UICONTROL Recommendations]](../../before-administer/recs-api/overview.md) pour savoir comment configurer et utiliser les API d’administration et de diffusion [!UICONTROL Target] pour les [!UICONTROL Recommendations].
