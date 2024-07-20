---
title: Initialisation des SDK
description: Assurez-vous que toutes les étapes nécessaires au chargement de la bibliothèque JavaScript  [!DNL Adobe Target] at.js sont exécutées dans la séquence correcte.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 250a8382-1fdd-4a70-b712-a25af5adad71
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 5%

---

# Initialisation des SDK

Suivez les étapes du diagramme *Initialiser le SDK* pour vous assurer que toutes les tâches nécessaires au chargement de la bibliothèque JavaScript at.js [!DNL Adobe Target] sont exécutées dans la séquence correcte.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour passer en mode plein écran.

## Diagramme Initialisation des SDK {#diagram}

Pour les applications multi-pages, ce flux se produit chaque fois que la page se recharge ou que le visiteur accède à une nouvelle page du site web.

>[!NOTE]
>
>Les numéros des étapes de l’illustration suivante correspondent aux sections ci-dessous. Les numéros des étapes ne sont pas dans un ordre particulier et ne reflètent pas l’ordre des étapes effectuées dans l’interface utilisateur de [!DNL Target] lors de la création de l’activité.

![Diagramme Initialiser les SDK](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Cliquez sur les liens suivants pour accéder aux sections de votre choix :

* [1.1 : Chargement du SDK de l’API visiteur](#load)
* [1.2 : Définition de l’ID de client](#set)
* [1.3 : Configuration d’une requête de chargement de page automatique](#automatic)
* [1.4 : Configuration de la gestion du scintillement](#flicker)
* [1.5 : Configuration du mappage des données](#data-mapping)
* [1.6 : Promotion](#promotion)
* [1.7 : critères basés sur le panier](#cart)
* [1.8 : critères basés sur la popularité](#popularity)
* [1.9 : critères basés sur un élément](#item)
* [1.10 : critères basés sur l’utilisateur](#user)
* [1.11 : Critères personnalisés](#custom)
* [1.12 : Fournir les attributs utilisés dans les règles d’inclusion](#inclusion)
* [1.13 : Fournissez excludedIds](#exclude)
* [1.14 : transmettez le paramètre entity.event.detailsOnly=true](#true)
* [1.15 : Configuration du mapping des données distantes](#remote)
* [1.16 : Chargement d’at.js](#web)

## 1.1 : Chargement du SDK de l’API visiteur {#load}

Cette étape permet de s’assurer que la bibliothèque `VisitorAPI.js` est chargée, configurée et initialisée correctement.

+++Voir les détails

![ Diagramme de chargement du SDK de l’API visiteur ](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Pour utiliser le service d’identification des visiteurs/API, votre entreprise doit être activée pour le [!DNL Adobe Experience Cloud] et disposer d’un [!UICONTROL Organization ID]. Pour plus d’informations, voir [Configuration requise de l’Experience Cloud : ID d’organisation](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} dans le guide *Aide d’Identity Service*.
* Vous avez besoin du fichier `VisitorAPI.js`. Vous devriez déjà avoir ce fichier si [!DNL Adobe Analytics] est implémenté. Ce fichier peut également être ajouté par le biais de l’ [[!DNL Adobe Experience Platform] extension de balises](https://experienceleague.adobe.com/docs/tags.html){target=_blank} ou téléchargé à partir du [Gestionnaire de code Adobe Analytics](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**Configuration et référence VisitorAPI.js**

Pour plus d’informations, voir [Mise en oeuvre du service Experience Cloud pour Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Lectures**

* [Présentation du service d’identité Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [À propos du service d’ID](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies et service Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Requête et définition d’ID par le service Identity Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Comprendre la synchronisation des identifiants et les taux de correspondance](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Actions**

* Incorporez le fichier `VisitorAPI.js` sur vos pages web.
* Découvrez les [ configurations disponibles pour le service d’identification des visiteurs/API](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Une fois le fichier `VisitorAPI.js` chargé, utilisez la méthode `Visitor.getInstance` pour l’initialisation à l’aide des configurations nécessaires.
* Familiarisez-vous avec les [méthodes disponibles](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.2 : Définition de l’ID de client {#set}

Cette étape permet de s’assurer que les identifiants connus de vos visiteurs (ID CRM, ID utilisateur, etc.) sont liés à l’identifiant anonyme de [!DNL Adobe] pour la personnalisation sur plusieurs appareils.

+++Voir les détails

![Définition de l’ID de client](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* L’identifiant connu des visiteurs doit être disponible dans la couche de données.

**Définition de l’ID de client**
Pour plus d’informations, voir [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Lectures**

* [ Synchronisation des profils en temps réel pour mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Actions**

* Utilisez `visitor.setCustomerIDs` pour définir l’identifiant connu du visiteur.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.3 : Configuration d’une requête de chargement de page automatique {#automatic}

Cette étape permet à at.js de récupérer toutes les expériences qui doivent être rendues sur la page lors du chargement du fichier de bibliothèque JavaScript at.js.

+++Voir les détails

![Configuration d’une requête de chargement de page automatique](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Toutes les données de la couche de données ne doivent pas être envoyées à [!DNL Target]. Consultez votre équipe d’entreprise (équipe marketing numérique) pour déterminer les données qui sont utiles à l’expérimentation, l’optimisation et la personnalisation. Seules ces données doivent être envoyées à [!DNL Target].
* Assurez-vous de ne pas envoyer de données d’informations d’identification personnelle à [!DNL Target].

**Configuration d’une requête de chargement de page automatique**

Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Lectures**

Découvrez le paramètre `pageLoadEnabled` dans [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Actions**

* Modifiez l’objet `window.targetGlobalSettings` pour activer les requêtes de chargement automatique de page.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.4 : Configuration de la gestion du scintillement {#flicker}

Cette étape permet de s’assurer qu’il n’y a pas de scintillement de page lors de la diffusion d’expériences.

+++Voir les détails

![ Configuration du diagramme de gestion du scintillement ](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Contactez l’équipe responsable des performances des pages web au sujet des avantages et des inconvénients du contrôle du scintillement à l’aide de la méthode par défaut utilisée par at.js. Vous pouvez rechercher des modèles de conception qui vous permettent d’utiliser une solution de gestion du scintillement personnalisée, telle que l’animation du chargeur. Si vous ne trouvez pas de modèle, vous pouvez en demander un nouveau.

**Configuration de la gestion du scintillement**

Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

La définition de `bodyHidingEnabled` sur `true` masque l’intégralité du corps de la page pendant la requête de chargement de page. Si vous n’avez pas activé la requête de chargement de page automatique pour une raison quelconque (données ultérieurement non prêtes, par exemple), il est préférable de définir ce paramètre sur `false`.

Si vous avez désactivé `bodyHidingEnabled` car vous ne souhaitez pas déclencher APLR et que vous souhaitez déclencher la demande de page ultérieurement, ou si vous n’avez pas besoin de gestion du scintillement, vous devez mettre en oeuvre votre propre gestion du scintillement. Vous pouvez gérer le scintillement de deux manières : en masquant les sections sous test ou en affichant un robot sur les sections sous test.

**Lectures**

* [Gestion du scintillement par at.js](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Découvrez les objets bodyHiddenStyle et bodyHidingEnabled dans [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Actions**

* Modifiez l’objet `window.targetGlobalSettings` pour définir `bodyHiddenStyle` et `bodyHidingEnabled`.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.5 : Configuration du mappage des données {#data-mapping}

Cette étape permet de s’assurer que toutes les données qui doivent être envoyées à [!DNL Target] sont définies.

+++Voir les détails

![ Diagramme de mappage de données](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* La couche de données doit être prête avec toutes les données qui doivent être envoyées à [!DNL Target].
* Recommendations : enrichissez le profil.
   * Transmettez `entity.id` pour capturer des données pour des critères et des éléments récemment consultés en fonction de critères basés sur le dernier produit consulté.
   * Transmettez `entity.id` pour capturer des données pour les critères de popularité basés sur la catégorie préférée.
   * Transmettez l’attribut de profil si des critères personnalisés sont basés sur celui-ci ou utilisés dans le filtrage des règles d’inclusion dans n’importe quel critère.
* Recommendations : ingérez des données de produit.
   * D’autres paramètres d’entité (réservés et personnalisés) peuvent être transmis pour ingestion ou mise à jour du catalogue de produits dans [!DNL Recommendations].
   * Le catalogue de produits peut également être mis à jour à l’aide de flux d’entités à l’aide de l’interface utilisateur ou de l’API [!DNL Target].

**Mapper les données à[!DNL Target]**

Pour plus d’informations, voir [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lectures**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planification et implémentation de Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Configuration de votre catalogue Recommendations](/help/dev/implement/recommendations/recommendations.md)

**Actions**

* Utilisez la fonction `targetPageParams()` pour définir toutes les données requises à envoyer à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.6 : Promotion {#promotion}

Ajoutez des éléments en promotion et contrôlez leur emplacement dans vos [!DNL Target Recommendations] [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Voir les détails

**Options disponibles**

* Promouvoir par les identifiants
* [Promouvoir par collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promouvoir par attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Paramètres d’entité requis**

* L’attribut d’élément dans la promotion doit être transmis lors de l’utilisation de l’option &quot;promouvoir par attribut&quot;.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.7 : critères basés sur le panier {#cart}

Effectuez des recommandations en fonction du contenu du panier de l’utilisateur.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Paramètres d’entité requis**

* cartIds

**Lectures**

* [Basé sur le panier](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.8 : critères basés sur la popularité {#popularity}

Effectuez des recommandations en fonction de la popularité globale d’un élément sur votre site ou de la popularité des éléments au sein de la catégorie, de la marque, du genre, préférée ou la plus consultée d’un utilisateur, etc.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Paramètres d’entité requis**

* `entity.categoryId` ou l’attribut d’élément pour la popularité basée sur si le critère est basé sur l’élément actif ou l’attribut d’élément.
* Aucun élément ne doit être transmis pour le site le plus consulté/le plus vendu.

**Lectures**

* [Popularity-based](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.9 : critères basés sur un élément {#item}

Effectuez des recommandations sur la base de la recherche d’éléments similaires à un élément que l’utilisateur consulte ou a récemment consulté.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Paramètres d’entité requis**

* `entity.id` ou tout attribut de profil utilisé comme clé

**Lectures**

* [Élément basé ](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.10 : critères basés sur l’utilisateur {#user}

Effectuez des recommandations en fonction du comportement de l’utilisateur.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Paramètres d’entité requis**

* `entity.id`

**Lectures**

* [Basé sur l’utilisateur](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.11 : Critères personnalisés {#custom}

Faites des recommandations en fonction d’un fichier personnalisé que vous chargez.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Custom algorithm]

**Paramètres d’entité requis**

`entity.id` ou attribut utilisé comme clé pour l’algorithme personnalisé

**Lectures**

* [Critères personnalisés](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.12 : Fournir les attributs utilisés dans les règles d’inclusion {#inclusion}

+++Voir les détails

**Lectures**

* [Utilisation de règles d’inclusion dynamiques et statiques](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.13 : Fournissez excludedIds {#exclude}

Transmettez les identifiants d’entité pour les entités que vous souhaitez exclure de vos recommandations. Par exemple, vous pouvez exclure des articles déjà présents dans le panier.

+++Voir les détails

**Lectures**

* [Puis-je exclure dynamiquement une entité ?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.14 : transmettez le paramètre `entity.event.detailsOnly=true` {#true}

Utilisez les attributs d’entité pour transmettre des informations sur les produits ou le contenu à [!DNL Target Recommendations].

+++Voir les détails

**Lectures**

* [Attributs d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.15 : configuration du mapping des données distantes (à distance)

Cette étape garantit que toutes les données qui doivent être envoyées à [!DNL Target] sont définies.

+++Voir les détails

![ Diagramme de mappage de données distant](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* La couche de données doit être prête avec toutes les données qui doivent être envoyées à [!DNL Target].

**Configuration des fournisseurs de données**

Pour plus d’informations, voir [Fournisseurs de données](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Lectures**

[fonction targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Actions**

Utilisez la fonction `targetPageParams()` pour définir toutes les données requises à envoyer à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.16 : Chargement d’at.js {#web}

Cette étape garantit que la bibliothèque JavaScript at.js est chargée et initialisée.

+++Voir les détails

![Chargement du diagramme Adobe Target at.js](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Téléchargez ou demandez à votre équipe de marketing numérique le fichier de bibliothèque JavaScript `at.js 2.*x*`.

*Lectures*

* [Fonctionnement de Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Fonctionnement d’at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Mise en œuvre de Target sans gestionnaire de balises](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Actions**

Incorporez le fichier at.js sur toutes vos pages web où l’expérimentation, l’optimisation, la personnalisation et la collecte de données doivent se produire.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

Passez à l’étape 2 : [Configuration de la collecte de données](/help/dev/patterns/recs-atjs/data-collection.md).
