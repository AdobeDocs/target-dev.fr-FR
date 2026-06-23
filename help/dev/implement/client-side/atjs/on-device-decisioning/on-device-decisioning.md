---
keywords: implémentation, bibliothèque javascript, js, atjs, prise de décision sur l’appareil, prise de décision sur l’appareil, at.js, sur l’appareil, sur l’appareil, implémentation0
description: Découvrez comment effectuer la [!UICONTROL prise de décision sur l’appareil] avec la bibliothèque at.js
title: Comment la prise de décision sur l’appareil fonctionne-t-elle avec la bibliothèque JavaScript at.js ?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
TQID: https://experienceleague.adobe.com/5cYQQDwAwUbKanR3Wbt7ckKnGwHvz3arqn0zjdz6SBc
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eb30f47f-d87a-400f-8f78-63ce7979ff56id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 3835
ht-degree: 4%

---

# [!UICONTROL  Prise de décision sur l’appareil ] pour at.js

À partir de la version 2.5.0, at.js offre la [!UICONTROL  prise de décision sur l’appareil ]. La [!UICONTROL prise de décision sur l’appareil] vous permet de mettre en cache vos activités [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) et [Ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) sur le navigateur afin d’effectuer une prise de décision en mémoire sans bloquer la requête réseau à l’Edge Network [!DNL Adobe Target].

>[!NOTE]
>
>La [!UICONTROL prise de décision sur l’appareil] est disponible pour les implémentations côté client et côté serveur. Cet article décrit la [!UICONTROL prise de décision sur l’appareil] pour le côté client. Pour plus d’informations sur la [!UICONTROL prise de décision sur l’appareil] pour les environnements côté serveur, consultez la documentation sur l’implémentation côté serveur [ici](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] offre également la flexibilité de fournir l’expérience la plus pertinente et la plus récente à partir de vos activités d’expérimentation et de personnalisation pilotées par le machine learning (pilotées par ML) via un appel au serveur en direct. En d’autres termes, lorsque les performances sont les plus importantes, vous pouvez choisir d’utiliser la [!UICONTROL prise de décision sur l’appareil]. Cependant, lorsque l’expérience la plus pertinente, à jour et pilotée par ML est nécessaire, un appel au serveur peut être effectué à la place.

## Quels sont les avantages de la [!UICONTROL prise de décision sur l’appareil] ?

Les avantages de la [!UICONTROL prise de décision sur l’appareil] sont les suivants :

* **Offrez des décisions et des expériences incroyablement rapides.** Le regroupement et la prise de décision sont effectués en mémoire et sur le navigateur pour éviter de bloquer les requêtes réseau.
* **Amélioration des performances des applications.** Exécutez des expériences et offrez une personnalisation à vos clients et utilisateurs sans compromettre les expériences des utilisateurs finaux.
* **Amélioration du score de qualité du site Google.** Une fois la prise de décision en mémoire, améliorez le score de qualité du site Google de votre entreprise en ligne pour la rendre plus détectable par les consommateurs.
* **En savoir plus sur l’analyse en temps réel.** Obtenez des informations sur les performances de votre activité en temps réel via les rapports [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T). A4T vous permet de faire pivoter votre stratégie aux moments critiques.

## Fonctionnalités prises en charge

Le SDK JS [!DNL Adobe Target] offre aux clients et aux clientes la possibilité de choisir entre les performances et la fraîcheur des données pour les décisions. En d’autres termes, si la diffusion du contenu personnalisé le plus pertinent et le plus attrayant via le machine learning est la plus importante pour vous, un appel au serveur en direct doit être effectué. Mais lorsque les performances sont plus critiques, une décision doit être prise sur l’appareil et en mémoire. Pour que la [!UICONTROL prise de décision sur l’appareil] fonctionne, reportez-vous à la liste des fonctionnalités prises en charge :

* Types d’activités
* Ciblage des audiences
* Méthode d&#39;allocation

Pour plus d’informations, voir [Fonctionnalités prises en charge pour la prise de décision [!UICONTROL  sur l’appareil]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## Comment fonctionne la [!UICONTROL prise de décision sur l’appareil] ?

Lorsque vous déployez et initialisez at.js avec la fonction [!UICONTROL prise de décision sur l’appareil] activée, un [artefact de règle](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) qui inclut votre [!UICONTROL prise de décision sur l’appareil] pour les activités, audiences et ressources A/B et XT, est téléchargé du réseau CDN Akamai le plus proche du visiteur et mis en cache localement sur le navigateur de votre visiteur. Lorsqu’une requête est effectuée à partir d’at.js pour récupérer une expérience, la décision concernant l’expérience à renvoyer est prise en mémoire, en fonction des métadonnées codées dans l’artefact de règle mis en cache.

## Méthode de prise de décision

Avec [!UICONTROL la prise de décision sur l’appareil], [!DNL Target] introduit un nouveau paramètre appelé Méthode de prise de décision. Le paramètre Méthode de prise de décision détermine la manière dont at.js diffuse vos expériences. La méthode Decisioning possède trois valeurs :

* Côté serveur uniquement
* Sur l’appareil uniquement
* Hybride

### Côté serveur uniquement

Côté serveur uniquement est la méthode de prise de décision par défaut préconfigurée lors de l’implémentation et du déploiement d’at.js 2.5.0+ sur vos propriétés web.

L’utilisation de Côté serveur uniquement comme configuration par défaut signifie que toutes les décisions sont prises sur le réseau Edge de [!DNL Target], ce qui implique un appel au serveur bloquant. Cette approche peut entraîner une latence incrémentielle, mais elle offre également des avantages significatifs, comme la possibilité d’appliquer les fonctionnalités de machine learning de [!DNL Target] qui incluent les activités [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) et [Ciblage automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html).

En outre, l’amélioration de vos expériences personnalisées à l’aide du profil utilisateur de [!DNL Target], qui est persistant entre les sessions et les canaux, peut fournir des résultats performants pour votre entreprise.

Enfin, la valeur côté serveur uniquement vous permet d’utiliser Adobe Experience Cloud et d’affiner les audiences qui peuvent être ciblées par le biais des segments Audience Manager et Adobe Analytics.

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et le réseau Edge [!DNL Adobe Target]. Ce diagramme de flux capture les nouveaux visiteurs et les visiteurs récurrents.

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Diagramme de flux côté serveur uniquement](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png "diagramme de flux côté serveur uniquement"){zoomable="yes"}

La liste suivante correspond aux nombres du diagramme :

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [service d’identités Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html ?). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />   La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de masquage préalable facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | Une requête de chargement de page est effectuée et inclut tous les paramètres configurés, tels que (ECID, ID de client, paramètres personnalisés, profil utilisateur, etc.). |
| 5 | Les scripts de profil s’exécutent, puis se propagent dans la banque de profils. <br />La banque de profils demande des audiences qualifiées à la bibliothèque d’audiences (par exemple, les audiences partagées à partir d’Adobe Analytics, de Adobe Audience Manager, etc.). <br />Les attributs du client sont envoyés à la banque de profils dans un traitement par lots. |
| 6 | Le magasin de profils est utilisé pour la qualification d’audience et le regroupement afin de filtrer les activités. |
| 7 | Le contenu qui en résulte est sélectionné une fois l’expérience déterminée à partir des activités de Live [!DNL Target]. |
| 8 | La bibliothèque at.js masque sur la page les éléments correspondants associés à l’expérience qui doit être rendue. |
| 9 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que votre visiteur puisse l’afficher. |
| 10 | La bibliothèque at.js manipule le DOM pour effectuer le rendu de l’expérience à partir du [!DNL Target] Edge Network. |
| 11 | L’expérience s’affiche pour le visiteur. |
| 12 | La page web entière se charge. |
| 13 | Les données Analytics sont envoyées aux serveurs de collecte de données. |
| 14 | Les données ciblées sont mises en correspondance avec les données Analytics via le SDID et sont traitées dans le stockage de rapports Analytics. Les données d’Analytics peuvent ensuite être affichées dans Analytics et [!DNL Target] via les rapports [!UICONTROL Analytics for Target] (A4T). |

### Sur l’appareil uniquement

Sur l’appareil uniquement est la méthode de prise de décision qui doit être définie dans at.js 2.5.0+ lorsque la [!UICONTROL prise de décision sur l’appareil] doit être utilisée uniquement sur l’ensemble de vos pages web.

La [!UICONTROL prise de décision sur l’appareil] permet de diffuser vos expériences et vos activités de personnalisation à une vitesse fulgurante, car les décisions sont prises à partir d’un artefact de règles mis en cache qui contient toutes vos activités qui remplissent les critères de la [!UICONTROL prise de décision sur l’appareil].

Pour en savoir plus sur les activités qui remplissent les critères de la [!UICONTROL prise de décision sur l’appareil], voir [Fonctionnalités prises en charge dans la [!UICONTROL prise de décision sur l’appareil]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

Cette méthode de prise de décision ne doit être utilisée que si les performances sont très critiques sur toutes les pages qui nécessitent des décisions de la part de Target. En outre, gardez à l’esprit que lorsque cette méthode de prise de décision est sélectionnée, vos activités [!DNL Target] qui ne remplissent pas les critères de la [!UICONTROL prise de décision sur l’appareil] ne seront ni diffusées ni exécutées. La bibliothèque at.js version 2.5.0+ est configurée pour rechercher uniquement l’artefact de règles mis en cache afin de prendre des décisions.

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et le réseau CDN Akamai. Le réseau CDN Akamai met en cache l’artefact de règles pour la première visite du visiteur. Pour la première visite de page d’un nouveau visiteur, l’artefact de règles JSON doit être téléchargé à partir du réseau CDN Akamai pour être mis en cache localement sur le navigateur du visiteur. Une fois l’artefact de règles JSON téléchargé, la décision est prise immédiatement sans appel réseau bloquant. Le diagramme de flux suivant capture les nouveaux visiteurs.

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Diagramme de flux sur l’appareil uniquement](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png "diagramme de flux sur l’appareil uniquement"){zoomable="yes"}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] serveurs d’administration qualifient toutes vos activités éligibles à la [!UICONTROL prise de décision sur l’appareil], génèrent l’artefact de règles JSON et le propagent sur le réseau CDN Akamai. Vos activités sont surveillées en permanence à la recherche de mises à jour pour générer un nouvel artefact de règles JSON à propager sur le réseau CDN Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [service d’identités Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de masquage préalable facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | La bibliothèque at.js effectue une requête pour récupérer l’artefact de règle JSON à partir du réseau CDN Akamai le plus proche du visiteur. |
| 5 | Le réseau CDN Akamai répond avec l’artefact de règle JSON. |
| 6 | L’artefact de règle JSON est mis en cache localement sur le navigateur du visiteur. |
| 7 | La bibliothèque at.js interprète l’artefact de règle JSON et exécute la décision de récupérer l’expérience et masque les éléments testés. |
| 8 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que votre visiteur puisse l’afficher. |
| 9 | La bibliothèque at.js manipule le DOM pour effectuer le rendu de l’expérience à partir de l’artefact de règle JSON mis en cache. |
| 10 | L’expérience s’affiche pour le visiteur. |
| 11 | La page web entière se charge. |
| 12 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont mises en correspondance avec les données Analytics via le SDID et sont traitées dans le stockage de rapports Analytics. Les données d’Analytics peuvent ensuite être affichées dans Analytics et [!DNL Target] via les rapports [!UICONTROL Analytics for Target] (A4T). |

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et l’artefact de règle JSON mis en cache pour l’accès à la page suivant ou la visite récurrente du visiteur. Comme l’artefact de règles JSON est déjà mis en cache et disponible sur le navigateur, la décision est prise immédiatement sans appel réseau bloquant. Ce diagramme de flux capture la navigation ultérieure dans la page pour les visiteurs récurrents.

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Diagramme de flux sur l’appareil uniquement pour la navigation de page suivante et les visites répétées](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png "Diagramme de flux sur l’appareil uniquement pour la navigation de page suivante et les visites répétées"){zoomable="yes"}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] serveurs d’administration qualifient toutes vos activités éligibles à la [!UICONTROL prise de décision sur l’appareil], génèrent l’artefact de règles JSON et le propagent sur le réseau CDN Akamai. Vos activités sont surveillées en permanence à la recherche de mises à jour pour générer un nouvel artefact de règles JSON à propager sur le réseau CDN Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [service d’identités Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de masquage préalable facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | La bibliothèque at.js interprète l’artefact de règle JSON et exécute la décision en mémoire pour récupérer l’expérience. |
| 5 | Les éléments testés sont masqués. |
| 6 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que votre visiteur puisse l’afficher. |
| 7 | La bibliothèque at.js manipule le DOM pour effectuer le rendu de l’expérience à partir de l’artefact de règle JSON mis en cache. |
| 8 | L’expérience s’affiche pour le visiteur. |
| 9 | La page web entière se charge. |
| 10 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont mises en correspondance avec les données Analytics via le SDID et sont traitées dans le stockage de rapports Analytics. Les données d’Analytics peuvent ensuite être affichées dans Analytics et [!DNL Target] via les rapports [!UICONTROL Analytics for Target] (A4T). |

### Hybride

Hybride représente la méthode de prise de décision qui doit être définie dans at.js 2.5.0+ lorsque la [!UICONTROL prise de décision sur l’appareil] et les activités nécessitant un appel réseau au réseau Edge [!DNL Adobe Target] doivent être exécutées.

Lorsque vous gérez des activités [!UICONTROL prise de décision sur l’appareil] et côté serveur, il peut s’avérer un peu compliqué et fastidieux de réfléchir à la manière de déployer et de configurer des [!DNL Target] sur vos pages. Avec la méthode de prise de décision hybride, [!DNL Target] sait quand il doit effectuer un appel au serveur vers le réseau Edge [!DNL Adobe Target] pour les activités qui nécessitent une exécution côté serveur. Il sait également quand exécuter uniquement les décisions sur l’appareil.

L’artefact de règles JSON comprend des métadonnées qui indiquent à at.js si une mbox comporte une activité côté serveur en cours d’exécution ou une activité [!UICONTROL prise de décision sur l’appareil]. Cette méthode de prise de décision garantit que les activités que vous prévoyez de diffuser rapidement sont effectuées par le biais de la [!UICONTROL prise de décision sur l’appareil] et pour les activités qui nécessitent une personnalisation plus puissante pilotée par ML, ces activités sont effectuées via le réseau Edge [!DNL Adobe Target].

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+, le réseau CDN Akamai et [!DNL Adobe Target] Edge Network pour un nouveau visiteur qui visite votre page pour la première fois. Ce qu’il faut retenir de ce diagramme, c’est que l’artefact de règles JSON est téléchargé de manière asynchrone pendant que les décisions sont prises via le réseau Edge [!DNL Adobe Target].

Cette approche permet de s’assurer que la taille de l’artefact, qui peut inclure de nombreuses activités, n’influence pas négativement la latence de la décision. Le téléchargement synchrone de l’artefact de règles JSON et la prise de décision par la suite peuvent également avoir des effets indésirables sur la latence et peuvent être incohérents. Par conséquent, la méthode de prise de décision hybride est une recommandation de bonne pratique consistant à toujours effectuer un appel côté serveur pour la décision pour un nouveau visiteur, et comme l’artefact de règles JSON est mis en cache en parallèle. Pour les visites de page et les visites récurrentes suivantes, les décisions sont prises à partir du cache et en mémoire via l’artefact de règles JSON.

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Diagramme de flux hybride pour un nouveau visiteur](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png "Diagramme de flux hybride pour un nouveau visiteur"){zoomable="yes"}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] serveurs d’administration qualifient toutes vos activités éligibles à la [!UICONTROL prise de décision sur l’appareil], génèrent l’artefact de règles JSON et le propagent sur le réseau CDN Akamai. Vos activités sont surveillées en permanence à la recherche de mises à jour pour générer un nouvel artefact de règles JSON à propager sur le réseau CDN Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [service d’identités Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de masquage préalable facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | Une requête de chargement de page est envoyée à [!DNL Adobe Target] Edge Network, y compris tous les paramètres configurés tels que (ECID, ID de client, paramètres personnalisés, profil utilisateur, etc.). |
| 5 | En parallèle, at.js effectue une requête pour récupérer l’artefact de règle JSON à partir du réseau CDN Akamai le plus proche du visiteur. |
| 6 | ([!DNL Adobe Target] Edge Network) Les scripts de profil s’exécutent, puis sont alimentés dans la banque de profils. Le magasin de profils demande des audiences qualifiées à la bibliothèque d’audiences (par exemple, les audiences partagées depuis Adobe Analytics, Adobe Audience Manager, etc.). |
| 7 | Le réseau CDN Akamai répond avec l’artefact de règle JSON. |
| 8 | Le magasin de profils est utilisé pour la qualification d’audience et le regroupement afin de filtrer les activités. |
| 9 | Le contenu qui en résulte est sélectionné une fois l’expérience déterminée à partir des activités de Live [!DNL Target]. |
| 10 | La bibliothèque at.js masque sur la page les éléments correspondants associés à l’expérience qui doit être rendue. |
| 11 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que votre visiteur puisse l’afficher. |
| 12 | La bibliothèque at.js manipule le DOM pour effectuer le rendu de l’expérience à partir du [!DNL Target] Edge Network. |
| 13 | L’expérience s’affiche pour le visiteur. |
| 14 | La page web entière se charge. |
| 15 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont mises en correspondance avec les données Analytics via le SDID et sont traitées dans le stockage de rapports Analytics. Les données d’Analytics peuvent ensuite être affichées dans Analytics et [!DNL Target] via les rapports [!UICONTROL Analytics for Target] (A4T). |

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et l’artefact de règles JSON mis en cache pour une navigation de page ultérieure ou une visite récurrente. Dans ce diagramme, concentrez-vous uniquement sur le cas d’utilisation dans lequel une décision sur l’appareil est prise pour la navigation ultérieure sur la page ou la visite de retour. Gardez à l’esprit que, selon les activités qui sont en ligne pour certaines pages, un appel côté serveur peut être effectué pour exécuter des décisions côté serveur.

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Diagramme de flux hybride pour la navigation de page suivante et les visites répétées](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png "Diagramme de flux hybride pour la navigation de page suivante et les visites répétées"){zoomable="yes"}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] serveurs d’administration qualifient toutes vos activités éligibles à la [!UICONTROL prise de décision sur l’appareil], génèrent l’artefact de règles JSON et le propagent sur le réseau CDN Akamai. Vos activités sont surveillées en permanence à la recherche de mises à jour pour générer un nouvel artefact de règles JSON à propager sur le réseau CDN Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [service d’identités Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de masquage préalable facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | Une requête est effectuée pour récupérer une expérience. |
| 5 | La bibliothèque at.js confirme que l’artefact de règle JSON a déjà été mis en cache et exécute la décision en mémoire pour récupérer l’expérience. |
| 6 | Les éléments testés sont masqués. |
| 7 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que votre visiteur puisse l’afficher. |
| 8 | La bibliothèque at.js manipule le DOM pour effectuer le rendu de l’expérience à partir de l’artefact de règle JSON mis en cache. |
| 9 | L’expérience s’affiche pour le visiteur. |
| 10 | La page web entière se charge. |
| 11 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont mises en correspondance avec les données Analytics via le SDID et sont traitées dans le stockage de rapports Analytics. Les données d’Analytics peuvent ensuite être affichées dans Analytics et [!DNL Target] via les rapports [!UICONTROL Analytics for Target] (A4T). |

## Comment activer la [!UICONTROL prise de décision sur l’appareil] ?

La [!UICONTROL prise de décision sur l’appareil] est disponible pour tous les clients [!DNL Target] qui utilisent At.js version 2.5.0 ou ultérieure.

Pour activer la [!UICONTROL prise de décision sur l’appareil] :

>[!NOTE]
>
>Vous devez disposer du [rôle utilisateur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) Administrateur ou Approbateur pour activer ou désactiver le bouton (bascule) Prise de décision sur l’appareil.

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]**.
1. Sous **[!UICONTROL Détails du compte]**, faites glisser le bouton **[!UICONTROL Prise de décision sur l’appareil]** sur la position « activé ».

   ![[!UICONTROL Prise de décision sur l’appareil] basculer](assets/on-device-decisioning-toggle.png)

   L’option « Inclure toutes les activités qualifiées [!UICONTROL prise de décision sur l’appareil] existantes dans l’artefact » s’affiche si vous activez la [!UICONTROL prise de décision sur l’appareil].
1. (Conditionnel) Faites glisser le bouton (bascule) sur la position « activé » si vous souhaitez que toutes vos activités Live [!DNL Target] qui remplissent les critères de la [!UICONTROL prise de décision sur l’appareil] soient automatiquement incluses dans l’artefact.

   Si vous désactivez cette option, vous devez recréer et activer toutes les activités [!UICONTROL prise de décision sur l’appareil] pour les inclure dans l’artefact de règles généré. En d’autres termes, toute activité à l’état actif avant d’activer le bouton (bascule) Prise de décision sur l’appareil n’est pas incluse dans l’artefact de règles.

Après avoir activé le bouton (bascule) Prise de décision sur l’appareil, [!DNL Target] commence à générer et à propager des artefacts [de règle](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) pour votre client.

>[!WARNING]
>
>Assurez-vous d’activer le bouton avant d’initialiser le SDK [!DNL Adobe Target] pour utiliser [!UICONTROL la prise de décision sur l’appareil]. Les artefacts de règles doivent d’abord générer et se propager sur les réseaux CDN Akamai pour que la [!UICONTROL prise de décision sur l’appareil] fonctionne. La propagation peut prendre entre cinq et dix minutes pour que le premier artefact de règle génère et se propage sur le réseau CDN Akamai.

## Comment configurer at.js 2.5.0+ pour utiliser la [!UICONTROL prise de décision sur l’appareil] ?

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]**.
1. Sous **[!UICONTROL Méthodes d’implémentation]** > **[!UICONTROL Méthode d’implémentation principale]**, cliquez sur **[!UICONTROL Modifier]** en regard de votre version d’at.js (doit être at.js 2.5.0 ou une version ultérieure).

   ![Modifier les paramètres de la méthode d’implémentation principale](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >Avant de modifier ces paramètres par défaut, contactez l’assistance clientèle pour éviter d’affecter votre implémentation actuelle.

1. Sélectionnez la méthode de prise de décision souhaitée :

   * Côté serveur uniquement
   * Sur l’appareil uniquement
   * Hybride

   ![Panneau Modifier les paramètres at.js](assets/global-settings.png)

### Paramètres globaux

Vous pouvez configurer une méthode de prise de décision par défaut pour toutes les décisions [!DNL Target]. Les différentes méthodes de prise de décision sont Côté serveur uniquement, Sur l’appareil uniquement et Hybride. La méthode de prise de décision sélectionnée dans l’interface utilisateur de [!DNL Target] est configurée dans `window.targetGlobalSettings` sous le champ `decisioningMethod` . En savoir plus sur les `decisioningMethod` dans [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

```javascript {line-numbers="true"}
<head> 
    <script type="text/javascript">

        window.targetGlobalSettings = { 
            clientCode: "yourClientCodeHere", 
            imsOrgId: "imsOrgId@AdobeOrg", 
            decisioningMethod: "on-device"

        }; 
    </script>

    <script type="text/javascript" src="at.js"></script> 
</head>
```

### Paramètre personnalisé

Si vous définissez la `decisioningMethod` dans `window.targetGlobalSettings`, mais souhaitez remplacer le `decisioningMethod` de chaque décision de [!DNL Adobe Target] en fonction de votre cas d’utilisation, vous pouvez effectuer cette procédure en spécifiant `decisioningMethod` dans l’appel [getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) d’At.js2.5.0+.

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
});
```

>[!NOTE]
>
>Pour utiliser « sur l’appareil » ou « hybride » comme méthode de prise de décision dans l’appel getOffers(), assurez-vous que le paramètre global a `decisioningMethod` « sur l’appareil » ou « hybride ». La bibliothèque at.js version 2.5.0+ doit savoir si l’artefact de règles JSON doit être téléchargé et mis en cache immédiatement après le chargement sur la page. Si la méthode de prise de décision pour le paramètre global est définie sur « côté serveur » et que la méthode de prise de décision « sur l’appareil » ou « hybride » est transmise dans l’appel getOffers() , at.js 2.5.0+ ne met pas en cache l’artefact de règle JSON pour exécuter vos décisions sur l’appareil.

### TTL du cache d’artefacts

Target représente vos activités qui remplissent les critères de la [!UICONTROL prise de décision sur l’appareil] en tant qu’artefact composé de métadonnées, de règles et de conditions. Cet artefact est mis en cache sur le réseau CDN Akamai. Lors de la première visite de votre utilisateur, le navigateur de l’utilisateur télécharge et met en cache l’artefact qui représente vos activités de [!UICONTROL prise de décision sur l’appareil].

Lors des visites ultérieures de votre site, le navigateur vérifie automatiquement s’il doit télécharger une version plus récente de l’artefact. Ce contrôle ajoute de la latence. La durée de vie du cache d’artefacts définit le nombre de minutes pendant lesquelles vous ne souhaitez pas que le navigateur recherche un artefact mis à jour depuis le dernier téléchargement réussi. Plus la période est longue, meilleures sont les performances. Plus la période est courte, meilleure est la fraîcheur des données, mais au prix d’une latence supplémentaire.

## Comment savoir si une activité est éligible [!UICONTROL prise de décision sur l’appareil] ?

Une fois que vous avez créé une activité [!UICONTROL prise de décision sur l’appareil] éligible, un libellé qui indique Prise de décision sur l’appareil éligible est visible dans la page Aperçu de l’activité.

![Libellé Éligible de la prise de décision sur l’appareil sur la page Aperçu de l’activité.](assets/on-device-decisioning-eligible-label.png)

Ce libellé ne signifie pas que l’activité sera toujours diffusée via la [!UICONTROL prise de décision sur l’appareil]. Ce n’est que lorsque at.js 2.5.0+ est configuré pour utiliser la [!UICONTROL prise de décision sur l’appareil] que cette activité sera exécutée sur l’appareil. Si at.js 2.5.0+ n’est pas configuré pour utiliser sur l’appareil, cette activité sera toujours diffusée via un appel au serveur effectué à partir d’at.js.

Vous pouvez filtrer toutes les activités éligibles [!UICONTROL prise de décision sur l’appareil] sur la page Activités à l’aide du filtre Éligible pour la prise de décision sur l’appareil .

![Filtre Éligible pour la prise de décision sur l’appareil sur la page Activités.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>Après la création et l’activation d’une activité éligible pour la [!UICONTROL prise de décision sur l’appareil], il peut s’écouler entre cinq et dix minutes avant qu’elle ne soit incluse dans l’artefact de règles généré et propagé au point de présence du réseau CDN Akamai.

## Résumé des étapes permettant de s’assurer que mes activités [!UICONTROL prise de décision sur l’appareil] sont diffusées via At.js 2.5.0+?

1. Accédez à l’interface utilisateur de [!DNL Adobe Target] et accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]** pour activer le bouton (bascule) **[!UICONTROL Prise de décision sur l’appareil]**.
1. Activez le bouton **[!UICONTROL Inclure toutes les activités qualifiées [!UICONTROL prise de décision sur l’appareil] existantes dans l’artefact »]**.

   La première génération d’artefact de règles JSON peut prendre jusqu’à 10 minutes.

1. Créez et activez un [type d’activité pris en charge par la [!UICONTROL prise de décision sur l’appareil]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md) et vérifiez qu’il est éligible à la [!UICONTROL prise de décision sur l’appareil].
1. Définissez la **[!UICONTROL Méthode de prise de décision]** sur **[!UICONTROL « Hybride »]** ou **[!UICONTROL « Sur l’appareil uniquement »]** via l’interface utilisateur des paramètres at.js.
1. Téléchargez et déployez At.js 2.5.0+ sur vos pages.

