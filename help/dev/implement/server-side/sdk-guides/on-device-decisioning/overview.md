---
keywords: côté serveur, côté serveur, sdk, sdk, on-device, prise de décision, on device, ondevice, zero latency, quasi-zero, node.js, server side3
description: Découvrez comment utiliser [!UICONTROL on-device decisioning] pour mettre en cache vos activités  [!DNL Target] A/B et MVT sur votre serveur afin d’effectuer une prise de décision en mémoire à une latence proche de zéro.
title: Qu’est-ce que la prise de décision sur appareil ?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 9%

---

# Présentation de la prise de décision sur l’appareil

Les SDK [!DNL Adobe Target] de nouvelle génération proposent désormais [!UICONTROL on-device decisioning], qui permettent de mettre en cache vos campagnes A/B et de ciblage d’expérience (XT) sur votre serveur et d’effectuer une prise de décision en mémoire à une latence proche de zéro, sans bloquer les demandes réseau à l’Edge Network de [!DNL Adobe Target].

[!DNL Adobe Target] offre également la flexibilité de fournir l’expérience la plus pertinente et la plus à jour à partir de vos campagnes d’expérimentation et de personnalisation pilotées par ML via un appel serveur actif. En d’autres termes, lorsque les performances sont plus importantes, vous pouvez choisir d’utiliser [!UICONTROL on-device decisioning], mais lorsque l’expérience la plus pertinente et la plus à jour est nécessaire, un appel au serveur peut être effectué à la place. Pour en savoir plus sur les cas d’utilisation qui justifient l’utilisation de l’un par rapport à l’autre, voir [Quand utiliser la prise de décision sur l’appareil par rapport à la prise de décision sur l’autre ](../../sdk-guides/on-device-decisioning/supported-features.md).

>[!NOTE]
>
>La prise de décision sur appareil est disponible pour les mises en oeuvre côté client et côté serveur. Cet article décrit [!UICONTROL on-device decisioning] côté serveur. Pour plus d’informations sur [!UICONTROL on-device decisioning] côté client, consultez la documentation de mise en oeuvre côté client [ici](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## Comment cela fonctionne-t-il ?

Lorsque vous installez et initialisez un SDK [!DNL Adobe Target] avec [!UICONTROL on-device decisioning] activé, un *artefact de règle* est téléchargé et mis en cache localement sur votre serveur, à partir du réseau de diffusion de contenu Akamai le plus proche de votre serveur. Lorsqu’une demande de récupération d’une expérience [!DNL Adobe Target] est effectuée dans votre application côté serveur, la décision concernant le contenu à renvoyer est prise en mémoire, en fonction des métadonnées codées dans l’artefact de règle mis en cache, qui définit toutes vos activités A/B et XT [!UICONTROL on-device decisioning].

Le diagramme suivant montre l’architecture [!UICONTROL on-device decisioning]. Cliquez sur pour développer l’image.

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Diagramme de l’architecture de prise de décision sur appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Diagramme de l’architecture de prise de décision sur appareil"){zoomable="yes"}

## Quels sont les avantages ?

* **Prendre des décisions de latence proches de zéro.** Le regroupement et la prise de décision sont effectués en mémoire et sur l’appareil afin d’éviter de bloquer les requêtes réseau.
* **Améliorez les performances de l’application.** Exécutez des expériences et diffusez la personnalisation à vos clients et utilisateurs sans compromettre les expériences de l’utilisateur final.
* **Améliorez le score de qualité du site Google.** Une fois la prise de décision effectuée en mémoire et côté serveur, améliorez le score de qualité du site Google de votre entreprise en ligne pour le rendre plus facilement détectable par les consommateurs.
* **Découvrez les analyses en temps réel.** Obtenez des informations sur les performances de votre activité en temps réel via les rapports [!DNL Adobe Target] ou A4T, ce qui vous permet de faire pivoter votre stratégie à des moments critiques.

## Fonctionnalité prise en charge

### Activités

La prise de décision sur appareil prend en charge les types d’activité suivants créés par le [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr) :

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### Méthode d’affectation

La prise de décision sur appareil prend en charge la méthode d’attribution suivante :

* Manuel

### Ciblage d’audience

La prise de décision sur les appareils prend en charge les règles d’audience suivantes :

| Règle d’audience | Prise de décision sur appareil |
| --- | --- |
| [Géo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=fr) | Oui<P>Lors de l’utilisation de la prise de décision sur l’appareil, les attributs géographiques suivants sont pris en charge :<ul><li>Pays/zone géographique</li><li>Ville</li><li>Latitude</li><li>Longitude</li></ul> |
| [Réseau](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=fr) | Non |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=fr) | Non |
| [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=fr) | Oui |
| [Système d’exploitation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=fr) | Oui |
| [Pages du site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=fr) | Oui |
| [Navigateur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=fr) | Oui |
| [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=fr) | Non |
| [Sources de trafic](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=fr) | Non |
| [Période](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=fr) | Oui |
| [Audiences Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=fr) (audiences de Adobe Audience Manager, Adobe Analytics et Adobe Experience Manager) | Non |

## Comment configurer mon client pour utiliser [!UICONTROL on-device decisioning] ?

La prise de décision sur l’appareil est disponible pour tous les clients [!DNL Adobe Target] qui utilisent des SDK côté serveur [!DNL Adobe Target]. Pour activer cette fonction, accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** dans l’interface utilisateur de [!DNL Adobe Target] et activez le bouton d’activation/désactivation de **[!UICONTROL On-Device Decisioning]**.

>[!NOTE]
>
>Vous devez disposer du rôle d’administrateur ou d’approbateur *utilisateur* pour activer ou désactiver le bouton d’activation/désactivation de [!UICONTROL On-Device Decisioning].

![alt image](assets/asset-odd-toggle.png)

Après avoir activé le bouton bascule de prise de décision sur l’appareil, [!DNL Adobe Target] commencera à générer et à propager les *artefacts de règle* pour votre client.

>[!NOTE]
>
>Assurez-vous d’activer le bouton bascule avant d’initialiser le SDK [!DNL Adobe Target] pour utiliser [!UICONTROL on-device decisioning]. Les artefacts de règle devront d’abord être générés et propagés aux réseaux de diffusion de contenu Akamai pour que [!UICONTROL on-device decisioning] fonctionne.

### Incluez toutes les activités qualifiées [!UICONTROL on-device decisioning] existantes dans le bouton d’activation/désactivation de l’artefact.

Activez/désactivez cette **on** lorsque vous souhaitez que toutes vos activités [!DNL Target] actives qui remplissent les critères de [!UICONTROL on-device decisioning] soient automatiquement incluses dans l’artefact.

Si vous laissez ce bouton **désactivé**, vous devrez recréer et activer toute activité [!UICONTROL on-device decisioning] pour qu’elle soit incluse dans l’artefact de règles généré.

## Comment puis-je savoir qu’une activité est [!UICONTROL on-device decisioning] compatible ?

Une fois que vous avez créé une activité, un libellé appelé **[!UICONTROL Decisioning Method]**, visible dans la page des détails de l’activité, indique si l’activité est [!UICONTROL on-device decisioning] compatible.

![alt image](assets/asset-odd9.png)

Vous pouvez également afficher toutes les activités [!UICONTROL on-device decisioning] compatibles avec la page **[!UICONTROL Activities]** en ajoutant la colonne **[!UICONTROL Decisioning Method]** à la liste des activités.

![alt image](assets/asset-odd7.png)

>[!NOTE]
>
>Après avoir créé et activé une activité [!UICONTROL on-device decisioning] compatible, il peut s’écouler 20 minutes avant qu’elle ne soit incluse dans l’artefact de règles généré et propagé vers les PoPs du réseau de diffusion de contenu Akamai.

## Quel est le résumé des étapes que je dois suivre pour m’assurer que mes activités [!UICONTROL on-device decisioning] sont diffusées avec succès via le SDK côté serveur de [!DNL Adobe Target] ?

1. Accédez à l’interface utilisateur de [!DNL Adobe Target] et accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** pour activer le bouton d’activation/désactivation de **[!UICONTROL On-Device Decisioning]**.
1. Activez le bouton bascule **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]** .
1. Créez et activez un type d’activité pris en charge par [!UICONTROL on-device decisioning] et vérifiez que **[!UICONTROL Decisioning Method]** est **[!UICONTROL On-Device Decisioning]** pour cette activité.
1. Installez et initialisez le SDK [Node.js](../../node-js/overview.md) ou [Java](../../java/overview.md) avec `decisioningMethod = on-device`.
1. Mettez en oeuvre `getOffers()` ou `getAttributes()` dans votre code pour récupérer une expérience sur l’appareil.
1. Déployez votre code.

Pour obtenir des exemples illustrant la prise en main des étapes 1 à 3 ci-dessus, reportez-vous à la section [Prise en main](../getting-started/getting-started.md) .


## Ressources supplémentaires

### Webinaire : personnaliser et tester sans latence avec prise de décision sur l’appareil à partir d’[!DNL Adobe Target]

Plus que jamais, les spécialistes marketing, les propriétaires et les développeurs de produits sont chargés d’optimiser l’expérience client globale sur les sites, les applications et dans toutes les situations où ils sont en contact avec leurs clients. Les multiples outils avec des silos de données et des mises en oeuvre complexes sont inadéquats.

Dans ce webinaire enregistré, [!DNL Adobe Target] experts du produit expliquent comment le déplacement des décisions d’optimisation de l’expérience critique sur l’appareil pour s’exécuter localement avec une latence proche de zéro peut ouvrir des portes à de nouveaux cas d’utilisation excitants tout en améliorant les performances du site pour vos clients.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutoriel : prise de décision sur l’appareil

[!DNL Adobe Target] [!UICONTROL on-device decisioning] active la diffusion de contenu de latence proche de zéro.

Cette vidéo de 7 minutes :

* Décrit [!UICONTROL on-device decisioning], y compris la comparaison avec d’autres méthodes de mise en oeuvre de [!DNL Target].
* Illustre comment activer [!UICONTROL on-device decisioning] dans Target
* Examiner un exemple d’activité de compositeur d’après les formulaires qui a été configuré avec du contenu JSON
* Affiche un exemple de code du SDK Node.JS contenant la configuration de clé requise pour [!UICONTROL on-device decisioning].
* Illustre les résultats dans un navigateur

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Pour plus de vidéos et de tutoriels, voir le [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=fr).

### Adobe Tech Blog - Partie 1 : Exécutez le SDK NodeJS [!DNL Adobe Target] pour l’expérimentation et la personnalisation sur les plateformes Edge (Akamai Edge Workers).

[Cliquez ici pour accéder à la publication de blog](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Blog Adobe Tech - Partie 2 : exécutez le SDK NodeJS [!DNL Adobe Target] pour permettre l’expérimentation et la personnalisation sur les plateformes Edge (AWS Lambda@Edge)

[Cliquez ici pour accéder à la publication de blog](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
