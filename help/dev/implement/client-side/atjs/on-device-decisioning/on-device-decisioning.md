---
keywords: implémentation, bibliothèque javascript, js, atjs, prise de décision sur l’appareil, prise de décision sur l’appareil, at.js, sur l’appareil, mise en oeuvre0
description: Découvrez comment effectuer [!UICONTROL prise de décision sur appareil] avec la bibliothèque at.js
title: Comment la prise de décision sur l’appareil fonctionne-t-elle avec la bibliothèque JavaScript at.js ?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '3689'
ht-degree: 12%

---

# [!UICONTROL Prise de décision sur appareil] pour at.js

À partir de la version 2.5.0, at.js propose des [!UICONTROL prise de décision sur appareil]. [!UICONTROL Prise de décision sur appareil] permet de mettre en cache votre [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) et [Ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) activités sur le navigateur pour effectuer une prise de décision en mémoire sans bloquer la demande réseau au [!DNL Adobe Target] Edge Network.

>[!NOTE]
>
>[!UICONTROL Prise de décision sur appareil] est disponible pour les mises en oeuvre côté client et côté serveur. Cet article décrit [!UICONTROL prise de décision sur appareil] pour côté client. Pour plus d’informations sur [!UICONTROL prise de décision sur appareil] pour le côté serveur, reportez-vous à la documentation de mise en oeuvre côté serveur . [here](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] offre également la flexibilité de fournir l’expérience la plus pertinente et la plus à jour de vos activités de personnalisation d’expérimentation et d’apprentissage automatique (basées sur le ML) via un appel serveur en direct. En d’autres termes, lorsque les performances sont plus importantes, vous pouvez choisir d’utiliser [!UICONTROL prise de décision sur appareil]. Cependant, lorsque l’expérience la plus pertinente, à jour et pilotée par ML est nécessaire, un appel au serveur peut être effectué à la place.

## Quels sont les avantages de [!UICONTROL prise de décision sur appareil]?

Les avantages de [!UICONTROL prise de décision sur appareil] inclure :

* **Proposez des décisions et des expériences rapides et éclatantes.** Le regroupement et la prise de décision sont effectués en mémoire et sur le navigateur afin d’éviter de bloquer les requêtes réseau.
* **Amélioration des performances de l’application.** Exécutez des expériences et personnalisez vos clients et utilisateurs sans compromettre les expériences de l’utilisateur final.
* **Amélioration du score de qualité du site Google.** Une fois la prise de décision en mémoire, améliorez le score de qualité du site Google de votre entreprise en ligne pour le rendre plus facilement détectable par les consommateurs.
* **Découvrez les analyses en temps réel.** Obtenez des informations sur les performances de votre activité en temps réel via [Analytics pour Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) création de rapports. A4T vous permet de faire pivoter votre stratégie à des moments critiques.

## Fonctionnalités prises en charge

La variable [!DNL Adobe Target] Le SDK JS offre aux clients la possibilité de choisir entre les performances et l’actualisation des données pour les décisions. En d’autres termes, si la diffusion de contenu personnalisé le plus pertinent et attrayant par le biais de l’apprentissage automatique est la plus importante pour vous, un appel au serveur en direct doit être effectué. Mais lorsque les performances sont plus critiques, une décision doit être prise sur l’appareil et en mémoire. Pour [!UICONTROL prise de décision sur appareil] pour travailler, reportez-vous à la liste des fonctionnalités prises en charge :

* Types d’activités
* Ciblage de l’audience
* Méthode d’affectation

Pour plus d’informations, voir [Fonctionnalités prises en charge pour [!UICONTROL prise de décision sur appareil]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## Comment [!UICONTROL prise de décision sur appareil] travail ?

Lorsque vous déployez et initialisez at.js avec [!UICONTROL prise de décision sur appareil] activée, une [artefact de règle](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) qui inclut votre [!UICONTROL prise de décision sur appareil] Pour les activités A/B et XT, les audiences et les ressources, est téléchargé du réseau de diffusion de contenu Akamai le plus proche de votre visiteur et mis en cache localement sur le navigateur de ce dernier. Lorsqu’une demande est envoyée à partir d’at.js pour récupérer une expérience, la décision concernant l’expérience à renvoyer est prise en mémoire, en fonction des métadonnées codées dans l’artefact de règle mis en cache.

## Méthode de prise de décision

Avec [!UICONTROL prise de décision sur appareil], [!DNL Target] introduit un nouveau paramètre appelé Méthode de prise de décision. Le paramètre Méthode de prise de décision détermine la manière dont at.js diffuse vos expériences. La méthode de prise de décision comporte trois valeurs :

* Côté serveur uniquement
* Sur appareil uniquement
* Hybride

### Côté serveur uniquement

Côté serveur uniquement est la méthode de prise de décision par défaut préconfigurée lors de l’implémentation et du déploiement d’at.js 2.5.0+ sur vos propriétés web.

L’utilisation de Côté serveur uniquement comme configuration par défaut signifie que toutes les décisions sont prises sur le réseau Edge de [!DNL Target], ce qui implique un appel au serveur bloquant. Cette approche peut introduire une latence incrémentielle, mais elle offre également des avantages significatifs, comme la possibilité d’appliquer des [!DNL Target]les fonctionnalités d’apprentissage automatique qui incluent [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) et [Ciblage automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) activités.

En outre, améliorez vos expériences personnalisées en utilisant [!DNL Target]Le profil utilisateur de , qui est conservé d’une session à l’autre et sur plusieurs canaux, peut fournir de puissants résultats à votre entreprise.

Enfin, la valeur côté serveur uniquement vous permet d’utiliser Adobe Experience Cloud et d’affiner les audiences qui peuvent être ciblées par le biais des segments d’Audience Manager et d’Adobe Analytics.

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et la variable [!DNL Adobe Target] Réseau Edge. Ce diagramme de flux capture les nouveaux visiteurs et les visiteurs récurrents.

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Diagramme de flux côté serveur uniquement](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png "Diagramme de flux côté serveur uniquement"){zoomable=&quot;yes&quot;}

La liste suivante correspond aux nombres du diagramme :

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [Service Adobe Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />   La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de prémasquage facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | Une requête de chargement de page est envoyée, qui inclut tous les paramètres configurés, tels que (ECID, ID de client, paramètres personnalisés, profil utilisateur, etc.). |
| 5 | Les scripts de profil s’exécutent, puis sont introduits dans le magasin de profils.<br />Le magasin de profils demande des audiences qualifiées auprès de la bibliothèque d’audiences (par exemple, audiences partagées depuis Adobe Analytics, Adobe Audience Manager, etc.).<br />Les attributs du client sont envoyés par lot dans le magasin de profils. |
| 6 | La banque de profils est utilisée pour la qualification et le regroupement des audiences afin de filtrer les activités. |
| 7 | Le contenu qui en résulte est sélectionné une fois que l’expérience est déterminée à partir de l’expérience en direct. [!DNL Target] activités. |
| 8 | La bibliothèque at.js masque les éléments correspondants sur la page associés à l’expérience qui doit être rendue. |
| 9 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que le visiteur puisse l’afficher. |
| 10 | La bibliothèque at.js manipule le DOM pour effectuer le rendu de l’expérience à partir de la variable [!DNL Target] Edge Network. |
| 11 | L’expérience est générée pour le visiteur. |
| 12 | La page web entière se charge. |
| 13 | Les données Analytics sont envoyées aux serveurs de collecte de données. |
| 14 | Les données ciblées sont associées aux données d’Analytics par l’intermédiaire du SDID et sont traitées dans le stockage de rapports d’Analytics. Il est alors possible de consulter les données Analytics dans Analytics et dans [!DNL Target] par l’intermédiaire des rapports [!UICONTROL Analytics for Target] (A4T). |

### Sur appareil uniquement

Sur l’appareil uniquement est la méthode de prise de décision qui doit être définie dans at.js 2.5.0+ lorsque [!UICONTROL prise de décision sur appareil] ne doit être utilisé que sur l’ensemble de vos pages web.

[!UICONTROL Prise de décision sur appareil] peut diffuser rapidement vos expériences et vos activités de personnalisation, car les décisions sont prises à partir d’un artefact de règles mis en cache qui contient toutes les activités pour lesquelles vous êtes éligible [!UICONTROL prise de décision sur appareil].

Pour en savoir plus sur les activités auxquelles il est admissible [!UICONTROL prise de décision sur appareil], voir [Fonctionnalités prises en charge dans [!UICONTROL prise de décision sur appareil]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

Cette méthode de prise de décision ne doit être utilisée que si les performances sont extrêmement critiques sur toutes les pages qui nécessitent des décisions de Target. En outre, gardez en tête que lorsque cette méthode de prise de décision est sélectionnée, vos activités [!DNL Target] ne remplissant pas les critères de la prise de décision sur l’appareil ne seront ni diffusées ni exécutées. La bibliothèque at.js version 2.5.0+ est configurée pour rechercher uniquement l’artefact de règles mis en cache afin de prendre des décisions.

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et le réseau de diffusion de contenu Akamai. Le réseau de diffusion de contenu Akamai met en cache l’artefact de règles pour la première visite du visiteur. Pour la première visite de page d’un nouveau visiteur, l’artefact de règles JSON doit être téléchargé à partir du réseau de diffusion de contenu Akamai pour être mis en cache localement sur le navigateur du visiteur. Une fois l’artefact de règles JSON téléchargé, la décision est prise immédiatement sans appel réseau de blocage. Le diagramme de flux suivant capture les nouveaux visiteurs.

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Diagramme de flux sur périphérique uniquement](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png "Diagramme de flux sur périphérique uniquement"){zoomable=&quot;yes&quot;}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] Les serveurs d’administration qualifient toutes les activités pour lesquelles [!UICONTROL prise de décision sur appareil], générez l’artefact de règles JSON et propagez-le au réseau de diffusion de contenu Akamai. Vos activités sont surveillées en permanence pour que les mises à jour puissent générer un nouvel artefact de règles JSON à propager sur le réseau de diffusion de contenu Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [Service Adobe Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de prémasquage facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | La bibliothèque at.js émet une requête pour récupérer l’artefact de règle JSON du réseau de diffusion de contenu Akamai le plus proche au visiteur. |
| 5 | Le réseau de diffusion de contenu Akamai répond avec l’artefact de règle JSON. |
| 6 | L’artefact de règle JSON est mis en cache localement sur le navigateur du visiteur. |
| 7 | La bibliothèque at.js interprète l’artefact de règle JSON et exécute la décision de récupérer l’expérience et masque les éléments testés. |
| 8 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que le visiteur puisse l’afficher. |
| 9 | La bibliothèque at.js manipule le modèle DOM pour effectuer le rendu de l’expérience à partir de l’artefact de règle JSON mis en cache. |
| 10 | L’expérience est générée pour le visiteur. |
| 11 | La page web entière se charge. |
| 12 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont associées aux données d’Analytics par l’intermédiaire du SDID et sont traitées dans le stockage de rapports d’Analytics. Il est alors possible de consulter les données Analytics dans Analytics et dans [!DNL Target] par l’intermédiaire des rapports [!UICONTROL Analytics for Target] (A4T). |

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et l’artefact de règle JSON mis en cache pour l’accès à la page ou la visite récurrente du visiteur. Comme l’artefact de règles JSON est déjà mis en cache et disponible sur le navigateur, la décision est prise immédiatement sans appel réseau bloquant. Ce diagramme de flux capture la navigation de page ou les visiteurs récurrents qui s’ensuivent.

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Diagramme de flux sur l’appareil uniquement pour la navigation suivante sur la page et les visites répétées](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png "Diagramme de flux sur l’appareil uniquement pour la navigation suivante sur la page et les visites répétées"){zoomable=&quot;yes&quot;}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] Les serveurs d’administration qualifient toutes les activités pour lesquelles [!UICONTROL prise de décision sur appareil], générez l’artefact de règles JSON et propagez-le au réseau de diffusion de contenu Akamai. Vos activités sont surveillées en permanence pour que les mises à jour puissent générer un nouvel artefact de règles JSON à propager sur le réseau de diffusion de contenu Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [Service Adobe Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de prémasquage facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | La bibliothèque at.js interprète l’artefact de règle JSON et exécute en mémoire la décision de récupérer l’expérience. |
| 5 | Les éléments testés sont masqués. |
| 6 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que le visiteur puisse l’afficher. |
| 7 | La bibliothèque at.js manipule le modèle DOM pour effectuer le rendu de l’expérience à partir de l’artefact de règle JSON mis en cache. |
| 8 | L’expérience est générée pour le visiteur. |
| 9 | La page web entière se charge. |
| 10 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont associées aux données d’Analytics par l’intermédiaire du SDID et sont traitées dans le stockage de rapports d’Analytics. Il est alors possible de consulter les données Analytics dans Analytics et dans [!DNL Target] par l’intermédiaire des rapports [!UICONTROL Analytics for Target] (A4T). |

### Hybride

Hybride est la méthode de prise de décision qui doit être définie dans at.js 2.5.0+ lorsque les variables [!UICONTROL prise de décision sur appareil] et les activités qui nécessitent un appel réseau à la fonction [!DNL Adobe Target] Le réseau Edge doit être exécuté.

Lorsque vous gérez les deux [!UICONTROL prise de décision sur appareil] activités et activités côté serveur, cela peut être un peu compliqué et fastidieux lorsque vous réfléchissez à la manière de déployer et de configurer [!DNL Target] sur vos pages. avec la méthode hybride comme méthode de prise de décision, [!DNL Target] sait quand il doit effectuer un appel au serveur [!DNL Adobe Target] Réseau Edge pour les activités qui nécessitent une exécution côté serveur, ainsi que le moment où exécuter uniquement les décisions sur l’appareil.

L’artefact de règles JSON comprend des métadonnées pour indiquer à at.js si une mbox est en cours d’exécution ou si une [!UICONTROL prise de décision sur appareil] activité. Cette méthode de prise de décision garantit que les activités que vous prévoyez de diffuser rapidement sont exécutées par le biais de [!UICONTROL prise de décision sur appareil] et pour les activités qui nécessitent une personnalisation plus puissante pilotée par ML, ces activités sont effectuées via l’événement [!DNL Adobe Target] Réseau Edge.

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+, le réseau de diffusion de contenu Akamai et le [!DNL Adobe Target] Réseau Edge pour un nouveau visiteur qui consulte votre page pour la première fois. Ce diagramme montre que l’artefact de règles JSON est téléchargé de manière asynchrone pendant que les décisions sont prises via la variable [!DNL Adobe Target] Réseau Edge.

Cette approche garantit que la taille de l’artefact, qui peut inclure de nombreuses activités, n’influence pas négativement la latence de la décision. Le téléchargement synchrone de l’artefact de règles JSON et la prise de la décision par la suite peuvent également avoir des effets négatifs sur la latence et peuvent être incohérents. Par conséquent, la méthode de prise de décision hybride est une recommandation recommandée pour toujours effectuer un appel côté serveur pour la décision d’un nouveau visiteur, car l’artefact de règles JSON est mis en cache en parallèle. Pour toutes les visites de page suivantes et les visites récurrentes, les décisions sont prises à partir du cache et en mémoire par le biais de l’artefact de règles JSON.

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Schéma de flux hybride pour un nouveau visiteur](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png "Schéma de flux hybride pour un nouveau visiteur"){zoomable=&quot;yes&quot;}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] Les serveurs d’administration qualifient toutes les activités pour lesquelles [!UICONTROL prise de décision sur appareil], générez l’artefact de règles JSON et propagez-le au réseau de diffusion de contenu Akamai. Vos activités sont surveillées en permanence pour que les mises à jour puissent générer un nouvel artefact de règles JSON à propager sur le réseau de diffusion de contenu Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [Service Adobe Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de prémasquage facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | Une requête de chargement de page est envoyée à la variable [!DNL Adobe Target] Edge Network, y compris tous les paramètres configurés tels que (ECID, ID de client, paramètres personnalisés, profil utilisateur, etc.) |
| 5 | En parallèle, at.js émet une requête pour récupérer l’artefact de règle JSON du réseau de diffusion de contenu Akamai le plus proche au visiteur. |
| 6 | ([!DNL Adobe Target] Edge Network) Les scripts de profil s’exécutent, puis sont introduits dans le magasin de profils. Le magasin de profils demande des audiences qualifiées auprès de la bibliothèque d’audiences (par exemple, audiences partagées depuis Adobe Analytics, Adobe Audience Manager, etc.). |
| 7 | Le réseau de diffusion de contenu Akamai répond avec l’artefact de règle JSON. |
| 8 | La banque de profils est utilisée pour la qualification et le regroupement des audiences afin de filtrer les activités. |
| 9 | Le contenu qui en résulte est sélectionné une fois que l’expérience est déterminée à partir de l’expérience en direct. [!DNL Target] activités. |
| 10 | La bibliothèque at.js masque les éléments correspondants sur la page associés à l’expérience qui doit être rendue. |
| 11 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que le visiteur puisse l’afficher. |
| 12 | La bibliothèque at.js manipule le DOM pour effectuer le rendu de l’expérience à partir de la variable [!DNL Target] Edge Network. |
| 13 | L’expérience est générée pour le visiteur. |
| 14 | La page web entière se charge. |
| 15 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont associées aux données d’Analytics par l’intermédiaire du SDID et sont traitées dans le stockage de rapports d’Analytics. Il est alors possible de consulter les données Analytics dans Analytics et dans [!DNL Target] par l’intermédiaire des rapports [!UICONTROL Analytics for Target] (A4T). |

Le diagramme suivant illustre l’interaction entre votre visiteur, le navigateur, at.js 2.5.0+ et l’artefact de règles JSON mis en cache pour une navigation de page ou une visite de retour ultérieure. Dans ce diagramme, concentrez-vous uniquement sur le cas d’utilisation où une décision sur l’appareil est prise pour la navigation ou la visite récurrente de la page suivante. Gardez à l’esprit que, selon les activités actives pour certaines pages, un appel côté serveur peut être effectué pour exécuter des décisions côté serveur.

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Diagramme de flux hybride pour la navigation suivante sur une page et les visites répétées](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png "Diagramme de flux hybride pour la navigation suivante sur une page et les visites répétées"){zoomable=&quot;yes&quot;}

La liste suivante correspond aux nombres du diagramme :

>[!NOTE]
>
>[!DNL Adobe Target] Les serveurs d’administration qualifient toutes les activités pour lesquelles [!UICONTROL prise de décision sur appareil], générez l’artefact de règles JSON et propagez-le au réseau de diffusion de contenu Akamai. Vos activités sont surveillées en permanence pour que les mises à jour puissent générer un nouvel artefact de règles JSON à propager sur le réseau de diffusion de contenu Akamai.

| Étape | Description |
| --- | --- |
| 1 | L’identifiant visiteur Experience Cloud est récupéré à partir du [Service Adobe Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<br />La bibliothèque at.js peut également être chargée de manière asynchrone avec un fragment de code de prémasquage facultatif implémenté sur la page. |
| 3 | La bibliothèque at.js masque le corps pour éviter le scintillement. |
| 4 | Une demande est envoyée pour récupérer une expérience. |
| 5 | La bibliothèque at.js confirme que l’artefact de règle JSON a déjà été mis en cache et exécute en mémoire la décision de récupérer l’expérience. |
| 6 | Les éléments testés sont masqués. |
| 7 | La bibliothèque at.js affiche le corps afin que le reste de la page puisse être chargé pour que le visiteur puisse l’afficher. |
| 8 | La bibliothèque at.js manipule le modèle DOM pour effectuer le rendu de l’expérience à partir de l’artefact de règle JSON mis en cache. |
| 9 | L’expérience est générée pour le visiteur. |
| 10 | La page web entière se charge. |
| 11 | Les données Analytics sont envoyées aux serveurs de collecte de données. Les données ciblées sont associées aux données d’Analytics par l’intermédiaire du SDID et sont traitées dans le stockage de rapports d’Analytics. Il est alors possible de consulter les données Analytics dans Analytics et dans [!DNL Target] par l’intermédiaire des rapports [!UICONTROL Analytics for Target] (A4T). |

## Comment activer [!UICONTROL prise de décision sur appareil]?

[!UICONTROL Prise de décision sur appareil] est disponible pour tous [!DNL Target] clients qui utilisent at.js 2.5.0+.

Pour activer [!UICONTROL prise de décision sur appareil]:

>[!NOTE]
>
>Vous devez avoir l’administrateur ou l’approbateur [rôle utilisateur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) pour activer ou désactiver le bouton activer/désactiver de la prise de décision sur le périphérique.

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]**.
1. Sous **[!UICONTROL Détails du compte]**, faites glisser le curseur **[!UICONTROL Prise de décision sur appareil]** basculez sur la position &quot;activé&quot;.

   ![[!UICONTROL Prise de décision sur appareil] basculer](assets/on-device-decisioning-toggle.png)

   &quot;Inclure tous les éléments existants [!UICONTROL prise de décision sur appareil] l’option activités qualifiées dans l’artefact s’affiche si vous activez [!UICONTROL prise de décision sur appareil].
1. (Conditionnel) Faites glisser le bouton d’activation sur la position &quot;Activé&quot; si vous souhaitez que tout votre contenu soit actif [!DNL Target] activités qui remplissent les critères [!UICONTROL prise de décision sur appareil] à inclure automatiquement dans l’artefact.

   Si vous laissez ce bouton désactivé, vous devez recréer et activer tout [!UICONTROL prise de décision sur appareil] activités pour qu’elles soient incluses dans l’artefact de règles généré. En d’autres termes, toute activité à l’état actif avant d’activer le bouton bascule de prise de décision sur l’appareil n’est pas incluse dans l’artefact de règles.

Après avoir activé le bouton activer/désactiver de la prise de décision sur le périphérique, [!DNL Target] commence à générer et à propager [artefacts de règle](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) pour votre client.

>[!WARNING]
>
>Assurez-vous d’activer le bouton bascule avant d’initialiser le [!DNL Adobe Target] SDK à utiliser [!UICONTROL prise de décision sur appareil]. Les artefacts de règle doivent d’abord être générés et propagés aux réseaux de diffusion de contenu Akamai pour [!UICONTROL prise de décision sur appareil] au travail. La propagation peut prendre entre cinq et dix minutes pour que le premier artefact de règle soit généré et propagé vers le réseau de diffusion de contenu Akamai.

## Comment configurer at.js 2.5.0+ pour utiliser [!UICONTROL prise de décision sur appareil]?

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]**.
1. Sous **[!UICONTROL Méthodes de mise en oeuvre]** > **[!UICONTROL Méthode de mise en oeuvre principale]**, cliquez sur **[!UICONTROL Modifier]** en regard de votre version d’at.js (doit être at.js 2.5.0 ou version ultérieure).

   ![Modification des paramètres de la méthode d’implémentation principale](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >Avant de modifier ces paramètres par défaut, consultez le service à la clientèle pour éviter d’affecter votre mise en oeuvre actuelle.

1. Sélectionnez la méthode de prise de décision souhaitée :

   * Côté serveur uniquement
   * Sur appareil uniquement
   * Hybride

   ![Modification du panneau des paramètres at.js](assets/global-settings.png)

### Paramètres globaux

Vous pouvez configurer une méthode de prise de décision par défaut pour l’ensemble des [!DNL Target] décisions. Les différentes méthodes de prise de décision sont côté serveur uniquement, on-device uniquement et hybride. La méthode de prise de décision sélectionnée dans [!DNL Target] L’interface utilisateur est configurée dans `window.targetGlobalSettings` sous le `decisioningMethod` champ . En savoir plus sur les `decisioningMethod` in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

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

Si vous définissez la variable `decisioningMethod` in `window.targetGlobalSettings`, mais souhaitez remplacer la variable `decisioningMethod` pour chaque [!DNL Adobe Target] selon votre cas d’utilisation, vous pouvez effectuer cette procédure en spécifiant `decisioningMethod` dans at.js2.5.0+ [getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) appelez .

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
>Pour utiliser &quot;sur l’appareil&quot; ou &quot;hybride&quot; comme méthode de prise de décision dans l’appel getOffers() , assurez-vous que le paramètre global comporte `decisioningMethod` comme &quot;sur l’appareil&quot; ou &quot;hybride&quot;. La bibliothèque at.js version 2.5.0+ doit savoir si l’artefact des règles JSON doit être téléchargé et mis en cache immédiatement après le chargement sur la page. Si la méthode de prise de décision pour le paramètre global est définie sur &quot;côté serveur&quot; et que la méthode de prise de décision &quot;on-device&quot; ou &quot;hybride&quot; est transmise à l’appel getOffers(), at.js 2.5.0+ n’aurait pas l’artefact de règle JSON mis en cache pour exécuter vos décisions sur l’appareil.

### TTL du cache d’artefacts

Target représente vos activités qui remplissent les critères [!UICONTROL prise de décision sur appareil] comme artefact constitué de métadonnées, de règles et de conditions. Cet artefact est mis en cache sur le réseau de diffusion de contenu Akamai. Lors de la première visite de votre utilisateur, le navigateur de l’utilisateur télécharge et met en cache l’artefact qui représente votre [!UICONTROL prise de décision sur appareil] activités.

Lors des visites suivantes sur votre site, le navigateur vérifie automatiquement s’il doit télécharger une version plus récente de l’artefact. Cette vérification ajoute une latence. La durée de vie (TTL) du cache des artefacts définit le nombre de minutes pendant lesquelles le navigateur ne doit pas rechercher un artefact mis à jour depuis le dernier téléchargement réussi. Plus la période est longue, meilleures sont les performances. Plus la période est courte, plus l’actualisation des données est importante, mais au prix d’une latence supplémentaire.

## Comment savoir si une activité est [!UICONTROL prise de décision sur appareil] éligible ?

Après avoir créé une activité qui est [!UICONTROL prise de décision sur appareil] éligible, un libellé qui indique Prise de décision sur l’appareil éligible, est visible dans la page Aperçu de l’activité.

![Prise de décision sur l’appareil Libellé éligible sur la page Aperçu de l’activité.](assets/on-device-decisioning-eligible-label.png)

Ce libellé ne signifie pas que l&#39;activité sera toujours diffusée via [!UICONTROL prise de décision sur appareil]. Uniquement lorsque at.js 2.5.0+ est configuré pour utiliser [!UICONTROL prise de décision sur appareil] Cette activité sera exécutée sur l’appareil. Si at.js 2.5.0+ n’est pas configuré pour utiliser sur l’appareil, cette activité sera toujours diffusée via un appel au serveur effectué à partir d’at.js.

Vous pouvez filtrer toutes les activités qui [!UICONTROL prise de décision sur appareil] éligible sur la page Activités via le filtre éligible Prise de décision sur périphérique .

![Prise de décision sur l’appareil Filtre éligible sur la page Activités.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>Après avoir créé et activé une activité qui est [!UICONTROL prise de décision sur appareil] éligible, il peut s’écouler entre cinq et dix minutes avant qu’il ne soit inclus dans l’artefact de règles généré et propagé vers le point de présence du réseau de diffusion de contenu Akamai.

## Résumé des étapes pour garantir mon [!UICONTROL prise de décision sur appareil] Les activités sont diffusées via at.js 2.5.0+?

1. Accédez au [!DNL Adobe Target] et accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Détails du compte]** pour activer la variable **[!UICONTROL Prise de décision sur appareil]** bascule.
1. Activez la variable **[!UICONTROL &quot;Inclure toutes les [!UICONTROL prise de décision sur appareil] activités qualifiées dans l’artefact&quot;]** bascule.

   La première génération d’artefact de règles JSON peut prendre jusqu’à 10 minutes.

1. Créez et activez un [type d’activité pris en charge par [!UICONTROL prise de décision sur appareil]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md), et vérifiez qu’il s’agit de [!UICONTROL prise de décision sur appareil] éligible.
1. Définissez la variable **[!UICONTROL Méthode de prise de décision]** à **[!UICONTROL &quot;Hybride&quot;]** ou **[!UICONTROL &quot;Sur appareil uniquement&quot;]** via l’interface utilisateur des paramètres at.js.
1. Téléchargez et déployez at.js 2.5.0+ sur vos pages.
