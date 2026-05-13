---
title: Rendu des expériences
description: Assurez-vous que toutes les étapes nécessaires au rendu des expériences sont exécutées dans le bon ordre.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 7cf0c70b-a4bc-46f4-9b33-099bdb7dd9a9
TQID: https://experienceleague.adobe.com/uHFbc8JEhjjGYIulJUvhkH7cXXht6Rht9rY43HjuNqg
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1060
ht-degree: 3%

---

# Rendu des expériences

Suivez les étapes du diagramme *Rendu d’expériences* pour vous assurer que toutes les tâches nécessaires au rendu des expériences sont exécutées dans le bon ordre.

>[!NOTE]
>
>Si vous avez activé la demande de chargement de page automatique lors de l’étape [Configurer la demande de chargement de page automatique](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic) dans *Initialiser les SDK* , vous pouvez ignorer cette activité, sauf si vous souhaitez appeler la SDK Adobe Target pour effectuer le rendu d’expériences supplémentaires à l’aide d’une demande d’emplacement régional.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour les développer en plein écran.

## Diagramme d’expériences de rendu {#diagram}

La gestion automatique du scintillement prête à l’emploi disponible avec at.js n’a de sens que lorsque les [!UICONTROL Automatic Page Load Request] sont activées. Cette option masque l’ensemble du corps d’HTML lors de la récupération des expériences à partir de [!DNL Target]. Dans ce cas, il est de votre responsabilité de gérer le scintillement. Recherchez des modèles d’implémentation disponibles pour la gestion du scintillement à titre indicatif.

>[!NOTE]
>
>Les numéros d’étape de l’illustration suivante correspondent aux sections ci-dessous. Les numéros d’étape ne sont pas dans un ordre particulier et ne reflètent pas l’ordre des étapes effectuées dans l’interface utilisateur de [!DNL Target] lors de la création de l’activité.

![Diagramme d’expériences de rendu](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

Cliquez sur les liens suivants pour accéder aux sections de votre choix :

* [3.1 : Promotion](#promotion)
* [3.2 : Critères basés sur le panier](#cart)
* [3.3 : Critères de popularité](#popularity)
* [3.4 : Critères par article](#item)
* [3.5 : Critères fondés sur l&#39;utilisateur](#user)
* [3.6 : Critères personnalisés](#custom)
* [3.7 : fournir les attributs utilisés dans les règles d’inclusion](#inclusion)
* [3.8 : Fournir des ID exclus](#exclude)
* [3.9 : fournir des attributs d’entité pour mettre à jour le catalogue de produits pour Recommendations](#entity-attributes)
* [3.10 : fournir des attributs de profil utilisés comme clés pour les règles d’inclusion](#keys)
* [3.11 : déclenchement de la requête de chargement de page](#fire)
* [3.12 : Demande d’emplacement régional pour les incendies](#location)

## 3.1 : Promotion {#promotion}

Ajoutez des éléments en promotion et contrôlez leur emplacement dans la conception de vos recommandations en choisissant les promotions Front ou Back dans l’interface utilisateur de [!DNL Target] lors de la création de l’activité.

+++Afficher les détails

**Options disponibles**

* Promouvoir par ID
* [Promouvoir par collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promouvoir par attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Paramètres d’entité requis**

* Les attributs d’article dans les promotions doivent être transmis lors de l’utilisation de l’option « promouvoir par attribut ».

**Lectures**

* [Ajout de promotions](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.2 : Critères basés sur le panier {#cart}

Faites des recommandations en fonction du contenu du panier de l’utilisateur.

+++Afficher les détails

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

## 3.3 : Critères de popularité {#popularity}

Faites des recommandations en fonction de la popularité globale d’un élément sur votre site ou de la popularité des éléments dans la catégorie, la marque, le genre ou la catégorie préférée ou la plus consultée d’un visiteur, etc.

+++Afficher les détails

**Critères disponibles**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Paramètres d’entité requis**

* `entity.categoryId` ou l’attribut d’élément pour la popularité basée sur si le critère est basé sur l’attribut actuel ou l’attribut d’élément.
* Rien ne doit être transmis pour les objets les plus consultés/les plus vendus sur le site.

**Lectures**

* [Basé sur la popularité](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.4 : Critères par article {#item}

Faites des recommandations basées sur la recherche d’éléments similaires à un élément que l’utilisateur consulte ou a récemment consulté.

+++Afficher les détails

**Critères disponibles**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Paramètres d’entité requis**

* `entity.id`
* Si un attribut de profil est utilisé comme clé

**Lectures**

* [Basé sur un article](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.5 : Critères fondés sur l&#39;utilisateur {#user}

Faites des recommandations basées sur le comportement de l’utilisateur.

+++Afficher les détails

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

Faites des recommandations basées sur un fichier personnalisé que vous téléchargez.

+++Afficher les détails

**Critères disponibles**

* [!UICONTROL Custom algorithm]

**Paramètres d’entité requis**

`entity.id` ou l’attribut utilisé comme clé pour l’algorithme personnalisé

**Lectures**

* [Critères personnalisés](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.7 : fournir les attributs utilisés dans les règles d’inclusion {#inclusion}

+++Afficher les détails

**Lectures**

* [Utilisation de règles d’inclusion dynamiques et statiques](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.8 : Fournir des ID exclus {#exclude}

Transmettez les ID d’entité pour les entités que vous souhaitez exclure de vos recommandations. Par exemple, vous pouvez exclure des articles déjà présents dans le panier.

+++Afficher les détails

**Lectures**

* [Puis-je exclure dynamiquement une entité ?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.9 : fournir des attributs d’entité pour mettre à jour le catalogue de produits pour [!DNL Recommendations] {#entity-attributes}

+++Afficher les détails

**Lectures**

* [Attributs d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

Vous pouvez également accomplir cette étape en créant des [flux de produits](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} à l’aide de l’interface utilisateur de [!DNL Target] pour mettre à jour le catalogue de produits pour [!DNL Recommendations].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.10 : fournir des attributs de profil utilisés comme clés pour les règles d’inclusion {#keys}

Indiquez les attributs de profil utilisés comme clés pour les règles d’inclusion dans l’un des critères de recommandations mentionnés ci-dessus.

+++ Afficher les détails

**Lectures**

* [Attributs de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.11 : déclenchement de la requête de chargement de page {#fire}

Cette étape déclenche un appel [!DNL Delivery API] avec `execute` > payload `pageLoad` dans la requête. La méthode `getOffers()` récupère l’expérience et `applyOffers()` effectue le rendu de l’expérience sur la page. La requête `pageLoad` est nécessaire au rendu des expériences créées dans le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Afficher les détails

![ Déclencher le diagramme de requête de chargement de page ](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Tous les mappages de données doivent être effectués à l’aide de la fonction `targetPageParams` .

**Lectures**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Actions**

* Utilisez les méthodes `getOffers` et `applyOffers` pour récupérer l’expérience à l’aide d’un appel API de requête de chargement de page.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 3.12 : Demande d&#39;emplacement régional pour les incendies (#location)

Cette étape déclenche un appel [!DNL Delivery API] avec `execute` > payload `mboxes` dans sa requête. La méthode `getOffers` récupère l’expérience et effectue `applyOffers` rendu de l’expérience sur la page. Vous pouvez envoyer plusieurs mbox sous la payload `execute` > `mboxes`.

+++Afficher les détails

![Diagramme de demande d’emplacement régional de déclenchement](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

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
