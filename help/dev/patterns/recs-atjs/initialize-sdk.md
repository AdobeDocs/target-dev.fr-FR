---
title: Initialisation des SDK
description: Assurez-vous que toutes les étapes nécessaires au chargement de la bibliothèque JavaScript at [!DNL Adobe Target] js sont exécutées dans l’ordre approprié.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 250a8382-1fdd-4a70-b712-a25af5adad71
TQID: https://experienceleague.adobe.com/PxAKvxntUCdacBLopvANAI7-8OWe-ELQqFRJu-n3RWo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1797
ht-degree: 4%

---

# Initialisation des SDK

Suivez les étapes du diagramme *Initialiser SDK* pour vous assurer que toutes les tâches nécessaires au chargement de la bibliothèque JavaScript at.js [!DNL Adobe Target] sont exécutées dans l’ordre approprié.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour les développer en plein écran.

## Diagramme Initialiser les SDK {#diagram}

Pour les applications comportant plusieurs pages, ce flux se produit chaque fois que la page se recharge ou que le visiteur accède à une nouvelle page du site web.

>[!NOTE]
>
>Les numéros d’étape de l’illustration suivante correspondent aux sections ci-dessous. Les numéros d’étape ne sont pas dans un ordre particulier et ne reflètent pas l’ordre des étapes effectuées dans l’interface utilisateur de [!DNL Target] lors de la création de l’activité.

![Diagramme Initialiser les SDK](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Cliquez sur les liens suivants pour accéder aux sections de votre choix :

* [1.1 : chargement du SDK de l’API visiteur](#load)
* [1.2 : Définition de l’ID de client](#set)
* [1.3 : Configuration de la requête de chargement automatique de page](#automatic)
* [1.4 : Configuration de la gestion du scintillement](#flicker)
* [1.5 : Configuration du mapping des données](#data-mapping)
* [1.6 : Promotion](#promotion)
* [1.7 : Critères basés sur le panier](#cart)
* [1.8 : Critères de popularité](#popularity)
* [1.9 : Critères par article](#item)
* [1.10 : Critères fondés sur l&#39;utilisateur](#user)
* [1.11 : Critères personnalisés](#custom)
* [1.12 : fournir les attributs utilisés dans les règles d’inclusion](#inclusion)
* [1.13 : Fournir des ID exclus](#exclude)
* [1.14 : transmettez le paramètre entity.event.detailsOnly=true .](#true)
* [1.15 : Configuration du mappage des données distantes](#remote)
* [1.16 : chargement d’at.js](#web)

## 1.1 : chargement du SDK de l’API visiteur {#load}

Cette étape permet de s’assurer que la bibliothèque `VisitorAPI.js` est chargée, configurée et initialisée correctement.

+++Afficher les détails

![Diagramme SDK de chargement de l’API visiteur](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Pour utiliser le service d’ID visiteur/API, votre entreprise doit être activée pour le [!DNL Adobe Experience Cloud] et disposer d’une [!UICONTROL Organization ID]. Pour plus d’informations, voir [Conditions requises pour Experience Cloud : ID d’organisation](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?lang=fr ?){target=_blank} dans le guide *Aide d’Identity Service*.
* Vous avez besoin du fichier `VisitorAPI.js`. Vous devriez déjà disposer de ce fichier si vous l’avez [!DNL Adobe Analytics] implémenté. Ce fichier peut également être ajouté via l’extension [[!DNL Adobe Experience Platform] tags](https://experienceleague.adobe.com/docs/tags.html?lang=fr){target=_blank} ou téléchargé à partir du [Gestionnaire de code Adobe Analytics](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=fr){target=_blank}.

**Configuration et renvoi de VisitorAPI.js**

Pour plus d’informations, voir [Implémentation du service Experience Cloud pour Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=fr){target=_blank}.

**Lectures**

* [Présentation d’Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr){target=_blank}
* [À propos du service d’ID](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html?lang=fr){target=_blank}
* [Cookies et Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=fr){target=_blank}
* [Requête et définition d’ID par Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html?lang=fr){target=_blank}
* [Comprendre la synchronisation des identifiants et les taux de correspondance](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html?lang=fr){target=_blank}

**Actions**

* Incorporez le fichier `VisitorAPI.js` dans vos pages web.
* Découvrez les [configurations disponibles pour le service d’ID visiteur/API](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?lang=fr){target=_blank}.
* Une fois le fichier `VisitorAPI.js` chargé, utilisez la méthode `Visitor.getInstance` pour initialiser à l’aide des configurations nécessaires.
* Familiarisez-vous avec les [&#x200B; méthodes disponibles &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html?lang=fr){target=_blank}.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.2 : Définition de l’ID de client {#set}

Cette étape permet de s’assurer que les identifiants connus de vos visiteurs (identifiant CRM, identifiant utilisateur, etc.) sont liés à l’identifiant anonyme d’[!DNL Adobe] pour la personnalisation sur l’ensemble des appareils.

+++Afficher les détails

![Définir l’ID de client](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* L’identifiant connu des visiteurs doit être disponible dans la couche de données.

**Définition de l’ID de client**
Pour plus d’informations, voir [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=fr){target=_blank}.

**Lectures**

* [Synchronisation des profils en temps réel pour mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=fr){target=_blank}

**Actions**

* Utilisez `visitor.setCustomerIDs` pour définir l’identifiant connu du visiteur.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.3 : Configuration de la requête automatique de chargement de page {#automatic}

Cette étape permet à at.js de récupérer toutes les expériences qui doivent être rendues sur la page lors du chargement du fichier de bibliothèque JavaScript at.js.

+++Afficher les détails

![Configurer la requête de chargement automatique de page](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Toutes les données de la couche de données ne doivent pas être envoyées à [!DNL Target]. Consultez votre équipe commerciale (équipe de marketing numérique) pour déterminer quelles données sont utiles à des fins d’expérimentation, d’optimisation et de personnalisation. Seules ces données doivent être envoyées à [!DNL Target].
* Assurez-vous de ne pas envoyer de données d’informations d’identification personnelle (PII) à [!DNL Target].

**Configurer la requête de chargement automatique de page**

Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Lectures**

Découvrez le paramètre `pageLoadEnabled` dans [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Actions**

* Modifiez l’objet `window.targetGlobalSettings` pour activer les requêtes de chargement de page automatique.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.4 : Configuration de la gestion du scintillement {#flicker}

Cette étape permet de s’assurer qu’aucune page ne scintille lors de la diffusion d’expériences.

+++Afficher les détails

![Configurer le diagramme de gestion du scintillement](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Discutez des avantages et des inconvénients du contrôle du scintillement à l’aide de la méthode par défaut utilisée par at.js avec l’équipe responsable des performances des pages web. Vous pouvez rechercher des modèles de conception qui vous permettent d’utiliser une solution personnalisée de gestion du scintillement, telle que l’animation du chargeur. Si vous ne trouvez pas de modèle, vous pouvez demander un nouveau modèle.

**Configurer la gestion du scintillement**

Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

La définition de `bodyHidingEnabled` sur `true` masque l’intégralité du corps de la page lorsque la requête de chargement de page est en cours. Si vous n’avez pas activé la demande de chargement automatique de page pour une raison quelconque (les données ne sont pas prêtes ultérieurement, par exemple), il est préférable de définir ce paramètre sur `false`.

Si vous avez désactivé `bodyHidingEnabled` parce que vous ne souhaitez pas déclencher APLR et que vous souhaitez déclencher la requête de page ultérieurement, ou que vous n’avez pas besoin de gérer le scintillement, vous devez implémenter votre propre gestion du scintillement. Vous pouvez gérer le scintillement de deux manières : en masquant les sections en cours de test ou en affichant un déclencheur sur les sections en cours de test.

**Lectures**

* [Gestion du scintillement par at.js](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Découvrez les objets bodyHiddenStyle et bodyHiddenEnabled dans [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Actions**

* Modifiez l’objet `window.targetGlobalSettings` pour définir `bodyHiddenStyle` et `bodyHidingEnabled`.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.5 : Configuration du mapping des données {#data-mapping}

Cette étape permet de s’assurer que toutes les données qui doivent être envoyées à [!DNL Target] sont définies.

+++Afficher les détails

![Diagramme de mappage des données](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* La couche de données doit être prête avec toutes les données qui doivent être envoyées à [!DNL Target].
* Recommendations : enrichissement du profil.
   * Transmettez des `entity.id` pour capturer des données pour les critères récemment consultés et les éléments basés sur les critères du dernier produit consulté.
   * Transmettez des `entity.id` pour capturer des données pour les critères de popularité en fonction de la catégorie préférée.
   * Transmettez l’attribut de profil si des critères personnalisés sont basés sur celui-ci ou utilisés dans le filtrage des règles d’inclusion dans n’importe quel critère.
* Recommendations : ingestion des données de produit.
   * D’autres paramètres d’entité (réservés et personnalisés) peuvent être transmis pour ingérer ou mettre à jour le catalogue de produits dans [!DNL Recommendations].
   * Le catalogue de produits peut également être mis à jour à l’aide de flux d’entités dans l’interface utilisateur ou l’API [!DNL Target].

**Mapper les données à[!DNL Target]**

Pour plus d’informations, voir [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lectures**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planifier et implémenter des recommandations](/help/dev/implement/recommendations/recommendations.md)
* [Configurer votre catalogue de recommandations](/help/dev/implement/recommendations/recommendations.md)

**Actions**

* Utilisez la fonction `targetPageParams()` pour définir toutes les données requises qui doivent être envoyées à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.6 : Promotion {#promotion}

Ajoutez des éléments en promotion et contrôlez leur placement dans vos [!DNL Target Recommendations] [conceptions](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=fr){target=_blank}.

+++Afficher les détails

**Options disponibles**

* Promouvoir par ID
* [Promouvoir par collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html?lang=fr){target=_blank}
* [Promouvoir par attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=fr){target=_blank}

**Paramètres d’entité requis**

* L’attribut d’élément dans la promotion doit être transmis lors de l’utilisation de l’option « promouvoir par attribut ».

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.7 : Critères basés sur le panier {#cart}

Faites des recommandations en fonction du contenu du panier de l’utilisateur.

+++Afficher les détails

**Critères disponibles**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Paramètres d’entité requis**

* cartIds

**Lectures**

* [Basé sur le panier](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=fr#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.8 : Critères de popularité {#popularity}

Faites des recommandations en fonction de la popularité globale d’un élément sur votre site ou en fonction de la popularité des éléments dans la catégorie, la marque, le genre préféré ou le plus consulté d’un utilisateur, etc.

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

* `entity.categoryId` ou l&#39;attribut article pour la popularité basée sur l&#39;article actuel ou l&#39;attribut article si le critère est basé sur l&#39;article actuel.
* Rien ne doit être transmis pour les objets les plus consultés/les plus vendus sur le site.

**Lectures**

* [Basé sur la popularité](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=fr#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.9 : Critères par article {#item}

Faites des recommandations basées sur la recherche d’éléments similaires à un élément que l’utilisateur consulte ou a récemment consulté.

+++Afficher les détails

**Critères disponibles**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Paramètres d’entité requis**

* `entity.id` ou tout attribut de profil utilisé comme clé

**Lectures**

* [Basé sur un article](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=fr#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.10 : Critères fondés sur l&#39;utilisateur {#user}

Faites des recommandations basées sur le comportement de l’utilisateur.

+++Afficher les détails

**Critères disponibles**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Paramètres d’entité requis**

* `entity.id`

**Lectures**

* [Basé sur l’utilisateur](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=fr#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.11 : Critères personnalisés {#custom}

Faites des recommandations basées sur un fichier personnalisé que vous téléchargez.

+++Afficher les détails

**Critères disponibles**

* [!UICONTROL Custom algorithm]

**Paramètres d’entité requis**

`entity.id` ou l’attribut utilisé comme clé pour l’algorithme personnalisé

**Lectures**

* [Critères personnalisés](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=fr#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.12 : fournir les attributs utilisés dans les règles d’inclusion {#inclusion}

+++Afficher les détails

**Lectures**

* [Utilisation de règles d’inclusion dynamiques et statiques](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html?lang=fr){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.13 : Fournir des ID exclus {#exclude}

Transmettez les ID d’entité pour les entités que vous souhaitez exclure de vos recommandations. Par exemple, vous pouvez exclure des articles déjà présents dans le panier.

+++Afficher les détails

**Lectures**

* [Puis-je exclure dynamiquement une entité ?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=fr#exclude){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.14 : Transmettre le paramètre `entity.event.detailsOnly=true` {#true}

Utilisez les attributs d’entité pour transmettre des informations sur les produits ou le contenu aux [!DNL Target Recommendations].

+++Afficher les détails

**Lectures**

* [Attributs d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=fr){target=_blank}

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.15 : Configuration du mappage de données à distance (à distance)

Cette étape permet de s’assurer que toutes les données qui doivent être envoyées à [!DNL Target] sont définies.

+++Afficher les détails

![Diagramme de mappage des données distantes](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* La couche de données doit être prête avec toutes les données qui doivent être envoyées à [!DNL Target].

**Configurer des fournisseurs de données**

Pour plus d’informations, voir [Fournisseurs de données](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Lectures**

[fonction targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Actions**

Utilisez la fonction `targetPageParams()` pour définir toutes les données requises qui doivent être envoyées à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 1.16 : chargement d’at.js {#web}

Cette étape garantit que la bibliothèque JavaScript at.js est chargée et initialisée.

+++Afficher les détails

![Charger le diagramme d’Adobe Target at.js](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Téléchargez le fichier de bibliothèque JavaScript `at.js 2.*x*` ou demandez-le à votre équipe de marketing numérique.

*Lectures*

* [Fonctionnement de Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=fr){target=_blank}
* [Fonctionnement d’at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Mise en œuvre de Target sans gestionnaire de balises](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Actions**

Insérez le fichier at.js dans toutes les pages web où l’expérimentation, l’optimisation, la personnalisation et la collecte de données doivent avoir lieu.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

Passez à l’étape 2 : [Configurer la collecte de données](/help/dev/patterns/recs-atjs/data-collection.md).
