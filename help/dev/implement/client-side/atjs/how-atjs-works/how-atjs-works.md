---
keywords: schéma système, scintillement, at.js, implémentation, bibliothèque javascript, js, atjs, 8 $
description: Découvrez le fonctionnement de la bibliothèque JavaScript at.js de  [!DNL Target] , y compris celui des diagrammes système pour vous aider à comprendre le workflow lors du chargement des pages.
title: Comment fonctionne la bibliothèque JavaScript at.js ?
feature: at.js
exl-id: 9183797c-857b-4b7f-a573-6bb1d583f7b1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 66%

---

# Fonctionnement d’at.js

Pour implémenter [!DNL Adobe Target] côté client, vous devez utiliser la bibliothèque JavaScript at.js.

Dans une implémentation côté client de [!DNL Adobe Target], [!DNL Target] fournit les expériences associées directement à une activité dans le navigateur client. Le navigateur décide de l’expérience à afficher et l’affiche. Avec une implémentation côté client, vous pouvez utiliser un éditeur WYSIWYG, le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr) (VEC) ou une interface non visuelle, le [compositeur d’expérience basé sur les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr), pour créer vos expériences de test et de personnalisation.

## Qu’est-ce qu’at.js ?

La bibliothèque at.js est la bibliothèque d’implémentation pour l’implémentation côté client de [!DNL Adobe Target]. La bibliothèque at.js réduit les délais de chargement des pages pour les implémentations web et offre des options d’implémentation optimisées pour les applications d’une seule page. at.js est la bibliothèque d’implémentation recommandée. Elle est régulièrement mise à jour avec de nouvelles fonctionnalités. Nous recommandons à tous les clients de mettre en oeuvre la [dernière version d’at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md) ou de migrer vers cette dernière.

Pour plus d’informations, voir [Bibliothèques JavaScript Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=fr#libraries).

Dans la [!DNL Target]mise en oeuvre illustrée ci-dessous, les solutions Adobe Experience Cloud suivantes sont mises en oeuvre : [!DNL Analytics], Target et [!DNL Audience Manager]. En outre, les [!DNL Experience Cloud] services principaux suivants sont implémentés : [!DNL Adobe Experience Platform], [!UICONTROL Audiences] et [!UICONTROL Visitor ID Service].

## Quelle différence y a-t-il entre les diagrammes de wordkflow at.js 1.*x* et at.js 2.x ?

Voir [Mise à niveau d’at.js 1.x vers at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) pour plus d’informations sur les différences introduites dans la version 2.0 depuis 1.*x*.

D’un point de vu général, il y a quelques différences entre les deux versions :

* at.js 2.x n’a pas de concept de requête de mbox globale, mais plutôt une requête de chargement de page. Une requête de chargement de page peut être vue comme une requête pour récupérer le contenu qui doit être appliqué au chargement initial de la page de votre site Web.
* at.js 2.x gère les concepts appelés [!UICONTROL Views], qui sont utilisés pour les applications d’une seule page (SPA). at.js 1.*x* n’a pas conscience de ce concept.

## Diagrammes at.js 2.x

Les diagrammes suivants vous aident à comprendre le workflow d’at.js 2.x avec [!UICONTROL Views] et la manière dont cela améliore l’intégration de SPA. Pour une meilleure présentation des concepts utilisés dans at.js 2.x, voir [Implémentation d’applications monopage](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Flux Target avec at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Flux Target avec at.js 2.x"){zoomable="yes"}

| Étape | Détails |
| --- | --- |
| 1 | L’appel renvoie le [!UICONTROL Experience Cloud ID] si l’utilisateur est authentifié. Un autre appel synchronise l’ID de client. |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />at.js peut également être chargé de manière asynchrone avec en option un extrait de code pré-masquant, implémenté sur la page. |
| 3 | Une demande de chargement de page est faite, incluant tous les paramètres configurés (MCID, SDID et ID client). |
| 4 | Les scripts de profil s’exécutent, puis sont introduits dans le [!UICONTROL Profile Store]. Le Sto demande des audiences qualifiées à partir de [!UICONTROL Audience Library] (par exemple, des audiences partagées à partir de [!DNL Adobe Analytics], [!DNL Audience Manager], etc.).<br />Les attributs du client sont envoyés par lot dans le [!UICONTROL Profile Store] |
| 5 | Selon les paramètres de requête d’URL et les données de profil, [!DNL Target] décidez quelles activités et expériences renvoyer au visiteur pour la page active et les futures vues. |
| 6 | Le contenu ciblé est renvoyé à la page, comprenant, éventuellement, les valeurs de profil pour une personnalisation plus poussée.<br />Le contenu ciblé sur la page actuelle est affiché aussi rapidement que possible, sans scintillement du contenu par défaut.<br />Contenu ciblé pour les vues présentées à la suite d’actions de l’utilisateur dans une application d’une seule page cache dans le navigateur, afin qu’elles puissent être appliquées instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées `triggerView()`. |
| 7 | Les données Analytics sont envoyées aux serveurs [!UICONTROL Data Collection]. |
| 8 | Les données ciblées sont associées aux données Analytics via le SDID et sont traitées dans le stockage de rapports [!DNL Analytics].Les données <br />[!DNL Analytics] peuvent ensuite être visualisées dans les rapports [!DNL Analytics] et [!DNL Target] via (A4T). |

Désormais, partout où `triggerView()` est implémenté sur votre SPA, les actions [!UICONTROL Views] et sont récupérées dans le cache et affichées pour l’utilisateur sans appel au serveur. `triggerView()` envoie également une demande de notification au serveur dorsal de [!DNL Target] afin d’incrémenter et d’enregistrer le nombre d’impressions. Pour plus d’informations sur at.js pour les applications monopages avec vues, voir [Implémentation d’application monopage](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![ Déclencheur d’affichage at.js 2.x du flux Target](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Déclencheur d’affichage at.js 2.x du flux Target"){zoomable="yes"}

| Étape | Détails |
| --- | --- |
| 1 | `triggerView()` est appelé dans le SPA pour effectuer le rendu de [!UICONTROL View] et appliquer des actions pour modifier les éléments visuels. |
| 2 | Le contenu ciblé pour la vue est lu à partir du cache. |
| 3 | Le contenu ciblé s’affiche aussi rapidement que possible, sans scintillement du contenu par défaut. |
| 4 | La demande de notification est envoyée à [!DNL Target] [!UICONTROL Profile Store] pour compter le visiteur dans l’activité et incrémenter les mesures. |
| 5 | [!DNL Analytics] données envoyées à [!UICONTROL Data Collection Servers]. |
| 6 | Les données [!DNL Target] sont associées aux données [!DNL Analytics] via le SDID et sont traitées dans le stockage de rapports [!DNL Analytics]. Les données [!DNL Analytics] peuvent ensuite être visualisées dans [!DNL Analytics] et [!DNL Target] au moyen de rapports A4T. |

### Vidéo : diagramme architectural d’at.js 2.x

at.js 2.x améliore la prise en charge d’applications monopages par Adobe Target et s’intègre aux autres solutions d’Experience Cloud. Cette vidéo explique comment tout se connecte.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Pour plus d’informations, consultez la page [Fonctionnement d’at.js 2.x](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html?lang=fr).

## Diagramme at.js 1.x

Les diagrammes suivants vous aident à comprendre le processus d’at.js 1.x.

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Flux Target at.js 1.x](/help/dev/implement/client-side/assets/target-flow.png "Flux Target at.js 1.x"){zoomable="yes"}

| Étape | Description | L’appel | Description |
|--- |--- |--- |--- |
| 1 | L’appel renvoie l’ID d’Experience Cloud (MCID) si l’utilisateur est authentifié ; un autre appel synchronise l’ID de client. | 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document. |
| 3 | Une demande de mbox globale, incluant tous les paramètres configurés (MCID, SDID et ID de client (facultatif)), est envoyée. | 4 | Les scripts de profil s’exécutent, puis sont introduits dans le magasin de profils. Le magasin demande des audiences qualifiées auprès de la bibliothèque d’audiences (par exemple, audiences partagées depuis Adobe Analytics, Audience Manager, etc.).<br />Les attributs du client sont envoyés par lot dans le magasin de profils. |
| 5 | En fonction de l’URL, des paramètres de mbox et des données de profil, [!DNL Target] décide quelles activités et expériences renvoyer au visiteur. | 6 | Le contenu ciblé est renvoyé à la page, y compris, éventuellement, les valeurs de profil pour une personnalisation plus poussée.<br />L’expérience est affichée aussi rapidement que possible, sans scintillement du contenu par défaut. |
| 7 | Les données Analytics sont envoyées aux serveurs de collecte de données. | 8 | Les données Target sont associées aux données Analytics par l’intermédiaire du SDID et sont traitées dans le stockage de rapports Analytics.<br />Les données Analytics peuvent ensuite être visualisées dans Analytics et [!DNL Target] par l’intermédiaire des rapports [!UICONTROL Analytics for Target] (A4T). |

### Vidéo : Heures de bureau, conseils et présentation d’at.js (26 juin 2019)

Cette vidéo est un enregistrement de &quot;Heures d&#39;ouverture&quot;, une initiative menée par l&#39;équipe [!UICONTROL Adobe Customer Care].

* Avantages de l’utilisation d’at.js
* Paramètres d’at.js
* Gestion du scintillement
* Débogage d’at.js
* Problèmes connus
* FAQ

>[!VIDEO](https://video.tv.adobe.com/v/27959/?quality=12)

## Comment at.js effectue le rendu des offres avec du contenu HTML

Lors du rendu des offres avec du contenu HTML, at.js applique l’algorithme suivant :

1. Les images sont préchargées (s’il existe des balises `<img>` dans le contenu HTML).

1. Le contenu HTML est attaché au nœud DOM.

1. Les scripts intégrés sont exécutés (code inclus dans les balises `<script>`).

1. Les scripts distants sont chargés de manière asynchrone et exécutés (`<script>` balises avec les attributs `src`).

Remarques importantes :

* at.js ne fournit aucune garantie quant à l’ordre d’exécution des scripts distants, car ceux-ci sont chargés de manière asynchrone.
* Les scripts intégrés ne doivent pas avoir de dépendances sur les scripts distants, car ils sont chargés et exécutés plus tard.
