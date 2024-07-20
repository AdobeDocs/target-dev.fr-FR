---
title: Rendu d’expériences
description: Assurez-vous que toutes les étapes nécessaires au rendu des expériences sont exécutées dans la séquence correcte.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 7cf0c70b-a4bc-46f4-9b33-099bdb7dd9a9
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 4%

---

# Rendu d’expériences

Suivez les étapes du diagramme *Render Experiences* pour vous assurer que toutes les tâches nécessaires au rendu des expériences sont exécutées dans la séquence correcte.

>[!NOTE]
>
>Si vous avez activé la requête de chargement de page automatique lors de l’[ étape de configuration de la requête de chargement de page automatique](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic) dans *Initialiser le SDK* , vous pouvez ignorer cette activité sauf si vous souhaitez appeler le SDK Adobe Target pour effectuer le rendu d’expériences supplémentaires à l’aide d’une requête de localisation régionale.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour passer en mode plein écran.

## Diagramme des expériences de rendu {#diagram}

La gestion automatique du scintillement prêt à l’emploi disponible avec at.js n’a de sens que lorsque [!UICONTROL Automatic Page Load Request] est activé. Cette option masque l’ensemble du corps de l’HTML lors de la récupération des expériences de [!DNL Target]. Dans ce cas, il vous incombe de gérer le scintillement. Recherchez des modèles de mise en oeuvre disponibles pour la gestion du scintillement à titre indicatif.

>[!NOTE]
>
>Les numéros des étapes de l’illustration suivante correspondent aux sections ci-dessous. Les numéros des étapes ne sont pas dans un ordre particulier et ne reflètent pas l’ordre des étapes effectuées dans l’interface utilisateur de [!DNL Target] lors de la création de l’activité.

![ Diagramme des expériences de rendu ](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

Cliquez sur les liens suivants pour accéder aux sections de votre choix :

* [3.1 : Promotion](#promotion)
* [3.2 : critères basés sur le panier](#cart)
* [3.3 : critères basés sur la popularité](#popularity)
* [3.4 : critères basés sur un élément](#item)
* [3.5 : critères basés sur l’utilisateur](#user)
* [3.6 : Critères personnalisés](#custom)
* [3.7 : Fournir les attributs utilisés dans les règles d’inclusion](#inclusion)
* [3.8 : Fournissez excludedIds](#exclude)
* [3.9 : Fournir des attributs d’entité pour mettre à jour le catalogue de produits pour Recommendations](#entity-attributes)
* [3.10 : Fournir des attributs de profil utilisés comme clés des règles d’inclusion](#keys)
* [3.11 : Déclenchement de la requête de chargement de page](#fire)
* [3.12 : Déclenchement de la demande d’emplacement régional](#location)

## 3.1 : Promotion {#promotion}

Ajoutez des éléments en promotion et contrôlez leur placement dans votre conception de recommandations en choisissant des promotions avant ou arrière dans l’interface utilisateur [!DNL Target] lors de la création de l’activité.

+++Voir les détails

**Options disponibles**

* Promouvoir par les identifiants
* [Promouvoir par collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promouvoir par attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Paramètres d’entité requis**

* Les attributs d’élément dans les promotions doivent être transmis lors de l’utilisation de l’option &quot;promouvoir par attribut&quot;.

**Lectures**

* [Ajouter des promotions](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.2 : critères basés sur le panier {#cart}

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

## 3.3 : critères basés sur la popularité {#popularity}

Effectuez des recommandations en fonction de la popularité globale d’un élément sur votre site ou de la popularité des éléments dans la catégorie, la marque, le genre, préférée ou la plus consultée d’un visiteur, etc.

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

* `entity.categoryId` ou l’attribut d’élément pour la popularité basé sur le critère est basé sur l’attribut actuel ou de l’élément .
* Rien ne doit être transmis pour le site le plus consulté/le plus vendu.

**Lectures**

* [Popularity-based](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.4 : critères basés sur un élément {#item}

Effectuez des recommandations sur la base de la recherche d’éléments similaires à un élément que l’utilisateur consulte ou a récemment consulté.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Paramètres d’entité requis**

* `entity.id`
* Si un attribut de profil est utilisé comme clé

**Lectures**

* [Élément basé ](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.5 : critères basés sur l’utilisateur {#user}

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

## 3.6 : Critères personnalisés {#custom}

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

## 3.7 : Fournir les attributs utilisés dans les règles d’inclusion {#inclusion}

+++Voir les détails

**Lectures**

* [Utilisation de règles d’inclusion dynamiques et statiques](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.8 : Fournissez excludedIds {#exclude}

Transmettez les identifiants d’entité pour les entités que vous souhaitez exclure de vos recommandations. Par exemple, vous pouvez exclure des articles déjà présents dans le panier.

+++Voir les détails

**Lectures**

* [Puis-je exclure dynamiquement une entité ?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.9 : Fournir des attributs d’entité pour mettre à jour le catalogue de produits pour [!DNL Recommendations] {#entity-attributes}

+++Voir les détails

**Lectures**

* [Attributs d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

Vous pouvez également accomplir cette étape en créant des [flux de produit](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} à l’aide de l’interface utilisateur [!DNL Target] pour mettre à jour le catalogue de produits pour [!DNL Recommendations].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.10 : Fournir des attributs de profil utilisés comme clés des règles d’inclusion {#keys}

Fournissez les attributs de profil utilisés comme clés pour les règles d’inclusion dans n’importe quel critère Recommendations mentionné ci-dessus.

+++ Voir les détails

**Lectures**

* [Attributs de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.11 : Déclenchement de la requête de chargement de page {#fire}

Cette étape déclenche un appel [!DNL Delivery API] avec la charge utile `execute` > `pageLoad` dans la requête. La méthode `getOffers()` récupère l’expérience et `applyOffers()` effectue le rendu de l’expérience sur la page. La requête `pageLoad` est nécessaire pour le rendu des expériences créées dans le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Voir les détails

![Déclenchement du diagramme de requête de chargement de page](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Tous les mappages de données doivent être effectués à l’aide de la fonction `targetPageParams` .

**Lectures**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Actions**

* Utilisez les méthodes `getOffers` et `applyOffers` pour récupérer l’expérience à l’aide d’un appel API de requête de chargement de page.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.12 : Déclenchement de la demande d’emplacement régional (#location)

Cette étape déclenche un appel [!DNL Delivery API] avec une charge utile `execute` > `mboxes` dans sa requête. La méthode `getOffers` récupère l’expérience et `applyOffers` la rend sur la page. Vous pouvez envoyer plusieurs mbox sous la charge utile `execute` > `mboxes`.

+++Voir les détails

![Déclencher le diagramme de demande d’emplacement régional](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Tous les mappages de données doivent être effectués à l’aide de la fonction `targetPageParams` .

**Lectures**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Actions**

* Utilisez les méthodes `getOffers` et `applyOffers` pour récupérer l’expérience à l’aide d’un appel API de requête de chargement de page.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

Passez à l’étape 4 : [Notifier Target](/help/dev/patterns/recs-atjs/notify-target.md).
