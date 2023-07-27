---
title: Rendu d’expériences
description: Assurez-vous que toutes les étapes nécessaires au rendu des expériences sont exécutées dans la séquence correcte.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 5321ce43be26e8f0776da49e597ecb5f8dfb5984
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 5%

---

# Rendu d’expériences

Suivez les étapes de la section *Expériences de rendu* diagramme pour s’assurer que toutes les tâches nécessaires au rendu des expériences sont exécutées dans le bon ordre.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour passer en mode plein écran.

## Diagramme des expériences de rendu {#diagram}

La gestion automatique du scintillement prêt à l’emploi disponible avec at.js n’a de sens que lorsque vous avez [!UICONTROL Requête de chargement de page automatique] activée. Cette option masque l’intégralité du corps du HTML lors de la récupération des expériences à partir de [!DNL Target]. Dans ce cas, il vous incombe de gérer le scintillement. Recherchez des modèles de mise en oeuvre disponibles pour la gestion du scintillement à titre indicatif.

Les numéros des étapes de l’illustration suivante correspondent aux sections ci-dessous.

![Diagramme des expériences de rendu](/help/dev/patterns/assets/render-experiences-diagram.png){width="600" zoomable="yes"}

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

Ajout d’éléments en promotion et contrôle leur placement dans Target Recommendations [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Voir les détails

**Options disponibles**

* Promouvoir par les identifiants
* [Promouvoir par collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promouvoir par attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Paramètres d’entité requis**

* L’attribut d’élément dans les promotions doit être transmis lors de l’utilisation de l’option &quot;promouvoir par attribut&quot;.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.2 : critères basés sur le panier {#cart}

Effectuez des recommandations en fonction du contenu du panier de l’utilisateur.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Les personnes qui les ont consultés ont consulté ceux-ci]
* [!UICONTROL Les personnes qui les ont consultés ont acheté ces]
* [!UICONTROL Les personnes qui les ont achetés ont acheté ces]

**Paramètres d’entité requis**

* cartIds

**Lectures**

* [Basé sur le panier](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.3 : critères basés sur la popularité {#popularity}

Effectuez des recommandations en fonction de la popularité globale d’un élément sur votre site ou de la popularité des éléments au sein de la catégorie, de la marque, du genre, préférée ou la plus consultée d’un utilisateur, etc.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Les plus consultés sur l’ensemble du site]
* [!UICONTROL Les plus consultés par catégorie]
* [!UICONTROL Attribut d’élément le plus consulté]
* [!UICONTROL Meilleurs vendeurs sur le site]
* [!UICONTROL Meilleurs vendeurs par catégorie]
* [!UICONTROL Meilleurs vendeurs par attribut d’article]
* [!UICONTROL Mesure Début par Analytics]

**Paramètres d’entité requis**

* `entity.categoryId` ou l’attribut item pour popularité basé sur le critère est basé sur l’attribut current ou l’attribut item .
* Aucun élément ne doit être transmis pour le site le plus consulté/le plus vendu.

**Lectures**

* [Basé sur la popularité](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.4 : critères basés sur un élément {#item}

Effectuez des recommandations sur la base de la recherche d’éléments similaires à un élément que l’utilisateur consulte ou a récemment consulté.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Les personnes ayant consulté ceci ont consulté cela]
* [!UICONTROL Les personnes ayant consulté ceci ont acheté cela]
* [!UICONTROL Les personnes ayant acheté ceci ont acheté cela]
* [!UICONTROL Éléments avec des attributs similaires]

**Paramètres d’entité requis**

* `entity.id`
* Si un attribut de profil est utilisé comme clé

**Lectures**

* [Élément basé](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.5 : critères basés sur l’utilisateur {#user}

Effectuez des recommandations en fonction du comportement de l’utilisateur.

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Éléments récemment consultés]
* [!UICONTROL Recommandé pour vous]

**Paramètres d’entité requis**

* `entity.id`

**Lectures**

* [Basé sur les utilisateurs](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.6 : Critères personnalisés {#custom}

Recommandations basées sur un fichier personnalisé que vous chargez

+++Voir les détails

**Critères disponibles**

* [!UICONTROL Algorithme personnalisé]

**Paramètres d’entité requis**

`entity.id` ou l’attribut utilisé comme clé pour l’algorithme personnalisé

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

* [Puis-je exclure dynamiquement une entité ? ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.9 : Fournir des attributs d’entité pour mettre à jour le catalogue de produits pour [!DNL Recommendations] {#entity-attributes}

+++Voir les détails

**Lectures**

* [Attributs d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

Vous pouvez également accomplir cette étape en créant des flux de produit à l’aide de la variable [!DNL Target] Interface utilisateur permettant de mettre à jour le catalogue de produits pour [!DNL Recommendations].

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

Cette étape déclenche une [!DNL Delivery API] appelez avec `execute` > `pageLoad` payload dans la requête. La variable `getOffers()` récupère l’expérience et `applyOffers()` effectue le rendu de l’expérience sur la page. La requête pageLoad est nécessaire pour le rendu des expériences créées dans la variable [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Voir les détails

![Déclenchement du diagramme de requête de chargement de page](/help/dev/patterns/assets/fire-page-load-request.png){width="100" zoomable="yes"}

**Conditions préalables**

* Tous les mappages de données doivent être effectués à l’aide de la variable `targetPageParams` de la fonction

**Lectures**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Actions**

* Utilisez la variable `getOffers` et `applyOffers` méthodes pour récupérer l’expérience à l’aide d’un appel API de requête de chargement de page.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.12 : Déclenchement de la demande d’emplacement régional (#location)

Cette étape déclenche une [!DNL Delivery API] appelez avec `execute` > `mboxes` payload dans sa requête. La variable `getOffers` récupère l’expérience et `applyOffers` effectue le rendu de l’expérience sur la page. Vous pouvez envoyer plusieurs mbox sous le `execute` > `mboxes` payload.

+++Voir les détails

![Déclencher le diagramme de demande d’emplacement régional](/help/dev/patterns/assets/fire-regional-location-request.png){width="100" zoomable="yes"}

**Conditions préalables**

* Tous les mappages de données doivent être effectués à l’aide de la variable `targetPageParams` de la fonction

**Lectures**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Actions**

* Utilisez la variable `getOffers` et `applyOffers` méthodes pour récupérer l’expérience à l’aide d’un appel API de requête de chargement de page.

+++

[Revenez au diagramme en haut de cette page.](#diagram)