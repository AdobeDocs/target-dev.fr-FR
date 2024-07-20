---
title: Configuration de la collecte de données
description: Assurez-vous que toutes les tâches nécessaires à la collecte de données sont exécutées dans l’ordre approprié.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Configuration de la collecte de données

Suivez les étapes du diagramme *Collecte de données* pour vous assurer que toutes les tâches nécessaires à la collecte de données sont exécutées dans l’ordre correct.

>[!TIP]
>
>Cliquez sur les images de cette rubrique pour passer en mode plein écran.

La couche de données est prête au chargement de la page ou la couche de données change après le chargement de la page.

Si vous avez déjà mappé des données pendant la [phase d’initialisation du SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md), vous devez exécuter les étapes de ce diagramme si :

* Votre couche de données est augmentée de quelque manière que ce soit sur la même page et vous souhaitez envoyer ces données supplémentaires à [!DNL Target].
* Vous souhaitez envoyer des données de catalogue de produits à [!DNL Target Recommendations]

## Diagramme de collecte de données {#diagram}

Les numéros des étapes de l’illustration suivante correspondent aux sections ci-dessous.

![ Diagramme de collecte de données](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Cliquez sur les liens suivants pour accéder aux sections de votre choix :

* [2.1 : Configuration du mapping des données](#configure)
* [2.2 Lien vers les attributs d’entité](#entity-attributes)
* [2.3 Déclenchement de l’API de suivi Adobe Target](#fire-api)

## 2.1 : Configuration du mapping des données {#configure}

Cette étape permet de s’assurer que toutes les données qui doivent être envoyées à [!DNL Adobe Target] sont définies.

+++Voir les détails

![ Configuration du diagramme de mappage de données ](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* La couche de données doit être prête avec toutes les données qui doivent être envoyées à [!DNL Target].

**Lectures**

[fonction targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Actions**

Utilisez la fonction `targetPageParams()` pour définir toutes les données requises à envoyer à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 2.2 : Lien vers les attributs d’entité {#entity-attributes}

Lien vers les attributs d’entité pour mettre à jour le catalogue de produits pour [!DNL Target Recommendations].

+++Voir les détails

**Lectures**

* [Attributs d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Considérations**

* Une autre manière de transmettre des attributs d’entité consiste à mettre à jour le catalogue de produits dans l’interface utilisateur [!DNL Target] pour utiliser les [flux de produits Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* La transmission des attributs d’entité n’est applicable que sur les pages où des données de catalogue de produits sont disponibles dans la couche de données.
* La transmission du paramètre `entity.event.detailsOnly=true` dans n’importe quel appel est prioritaire.

+++

[Revenez au diagramme en haut de cette page.](#diagram)

## 2.3 Déclenchement de l’API de suivi Adobe Target {#fire-api}

Cette étape permet de s’assurer que toutes les données qui doivent être envoyées à [!DNL Target] sont envoyées.

+++Voir les détails

![ Déclenchement du diagramme de l’API de suivi Adobe Target ](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**Conditions préalables**

* Tous les mappages de données doivent avoir été effectués à l’aide de la fonction [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lectures**

* [méthode adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Actions**

Utilisez la méthode [adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) pour envoyer toutes les données qui doivent être envoyées à [!DNL Target].

+++

[Revenez au diagramme en haut de cette page.](#diagram)

Passez à l’étape 3 : [Render experience](/help/dev/patterns/recs-atjs/render-experiences.md)
