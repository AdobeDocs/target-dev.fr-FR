---
keywords: versions d’at.js, versions d’at.js, application monopage, spa, interdomaines, interdomaines
description: Découvrez comment mettre à niveau at [!DNL Adobe Target] js 1.x vers at.js 2.x. Consultez les diagrammes de flux système, découvrez les nouvelles fonctions et les fonctions obsolètes, etc.
title: Comment effectuer une mise à niveau d’at.js version 1.x vers la version 2.x ?
feature: at.js
exl-id: fbfa5743-0fa5-44c6-89b3-fdee9b50e126
source-git-commit: 16132bc7a624ab4849651b183bde9b3064b4a676
workflow-type: tm+mt
source-wordcount: '2939'
ht-degree: 57%

---

# Mise à niveau à partir d’at.js 1.*x* vers at.js 2.*x*

La dernière version d’at.js [!DNL Adobe Target] propose des ensembles de fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies de nouvelle génération côté client. Cette nouvelle version vise à mettre à niveau at.js afin d’établir des interactions harmonieuses avec les applications monopages (SPA).

Voici quelques avantages liés à l’utilisation d’at.js 2.*x* qui ne sont pas disponibles dans les versions précédentes :

* La capacité à mettre en cache toutes les offres au chargement de la page afin de réduire plusieurs appels serveur à un seul appel serveur.
* Améliorez considérablement les expériences des utilisateurs finaux sur votre site. Les offres s’affichent immédiatement via le cache sans temps de latence que les appels serveur traditionnels imposent.
* Une seule ligne de code et une configuration de développeur unique pour permettre à vos spécialistes marketing de créer et d’exécuter des activités de [!UICONTROL A/B Test] et de [!UICONTROL Experience Targeting] (XT) via le compositeur d’expérience visuelle (VEC) sur vos applications d’une seule page (SPA).

## at.js 2.Diagrammes système *x*

Les diagrammes suivants vous aident à comprendre le workflow d’at.js 2.*x* avec des vues et comment cela améliore l’intégration de la SPA. Pour une meilleure introduction des concepts utilisés dans at.js 2.*x*, voir [Implémentation d’applications d’une seule page](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Flux cible avec at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Flux cible avec at.js 2.x"){zoomable="yes"}

| L’appel | Détails |
| --- | --- |
| 1 | L’appel renvoie le [!UICONTROL Experience Cloud ID] si l’utilisateur est authentifié. Un autre appel synchronise l’ID de client. |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document.<P>at.js peut également être chargé de manière asynchrone avec une option de masquage préalable d’un fragment de code implémentée sur la page. |
| 3 | Une demande de chargement de page est faite, incluant tous les paramètres configurés (MCID, SDID et ID client). |
| 4 | Les scripts de profil s’exécutent, puis sont introduits dans le magasin de profils. Le magasin demande des audiences qualifiées à la bibliothèque d’audiences (par exemple, les audiences partagées depuis [!DNL Adobe Analytics], [!DNL Audience Manager], etc.).<P>Les attributs du client sont envoyés par lot dans le magasin de profils. |
| 5 | Selon les paramètres de requête d’URL et les données de profil, [!DNL Target] décidez quelles activités et expériences renvoyer au visiteur pour la page active et les futures vues. |
| 6 | Le contenu ciblé est renvoyé à la page, comprenant, éventuellement, les valeurs de profil pour une personnalisation plus poussée.<P>Le contenu ciblé sur la page active est révélé le plus rapidement possible sans scintillement du contenu par défaut.<P>Contenu ciblé pour les vues présentées à la suite d’actions de l’utilisateur dans une SPA mise en cache dans le navigateur, afin qu’elles puissent être appliquées instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées via `triggerView()`. |
| 7 | Les données [!UICONTROL Analytics] sont envoyées aux serveurs de collecte de données. |
| 8 | Les données ciblées sont mises en correspondance avec les données [!UICONTROL Analytics] via le SDID et sont traitées dans le stockage des rapports [!UICONTROL Analytics].<P>[!UICONTROL Analytics] données peuvent ensuite être affichées dans [!UICONTROL Analytics] et [!DNL Target] via les rapports [!UICONTROL Analytics for Target] (A4T). |

Désormais, où que soit implémenté `triggerView()` sur votre application d’une seule page, les vues et actions sont récupérées depuis le cache et présentées à l’utilisateur sans appel au serveur. `triggerView()` envoie également une demande de notification au serveur principal [!DNL Target] afin d’incrémenter et d’enregistrer le nombre d’impressions.

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Flux cible at.js 2.Flux *x* triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target at.js 2.*x* triggerView"){zoomable="yes"}

| L’appel | Détails |
| --- | --- |
| 1 | `triggerView()` est appelée dans l’application d’une seule page pour afficher les vues et appliquer les actions pour modifier les éléments visuels. |
| 2 | Le contenu ciblé pour la vue est lu à partir du cache. |
| 3 | Le contenu ciblé s’affiche aussi rapidement que possible, sans scintillement du contenu par défaut. |
| 4 | La demande de notification est envoyée au magasin de profils [!DNL Target] pour compter le visiteur dans l’activité et incrémenter les mesures. |
| 5 | [!UICONTROL Analytics] les données envoyées aux serveurs de collecte de données. |
| 6 | [!DNL Target] données sont mises en correspondance avec les données [!UICONTROL Analytics] via le SDID et sont traitées dans le stockage de rapports [!UICONTROL Analytics]. [!UICONTROL Analytics] données peuvent ensuite être affichées dans [!UICONTROL Analytics] et [!DNL Target] via les rapports A4T. |

## Déployer at.js 2.*x*

Déployer at.js 2.*x* via les balises dans l’extension [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md).

>[!NOTE]
>
>La méthode recommandée consiste à déployer at.js à l’aide de balises dans [!DNL Adobe Experience Platform].
>
>Ou
>
>Téléchargez manuellement at.js 2.*x* à l’aide de l’interface utilisateur [!DNL Target] et déployez-la à l’aide de la méthode [ de votre choix](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md).

## Fonctions d’at.js obsolètes

Plusieurs fonctions ont été abandonnées dans at.js 2.*x*.

>[!WARNING]
>
>Si ces fonctions obsolètes sont toujours utilisées sur votre site lorsqu’at.js 2.*x* est déployé, des avertissements s’affichent dans la console. L’approche recommandée lors de la mise à niveau consiste à tester le déploiement d’at.js 2.*x* dans un environnement d’évaluation, veillez à parcourir chaque avertissement consigné dans la console et à traduire les fonctions obsolètes en nouvelles fonctions introduites dans at.js 2.*x*.

Les fonctions obsolètes et leurs contreparties sont présentées ci-après. Pour obtenir la liste complète des fonctions, voir [Fonctions at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).

>[!NOTE]
>
>at.js 2.*x* ne prémasque plus automatiquement `mboxDefault` éléments marqués. Les clients doivent donc s’adapter manuellement à la logique pré-masquée, soit sur le site, soit via un gestionnaire de balises.

### mboxCreate(mbox,params)

**Description** :

Exécute une requête et applique l’offre au DIV le plus proche avec le nom de classe `mboxDefault`.

**Exemple** :

```html {line-numbers="true"}
<div class="mboxDefault">
  default content to replace by offer
</div>
<script>
  mboxCreate('mboxName','param1=value1','param2=value2');
</script>
```

**Équivalent at.js 2.*x***

Une alternative à `mboxCreate(mbox, params)` est `getOffer()` et `applyOffer()`.

**Exemple** :

```html {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  var el = document.currentScript.previousElementSibling;
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2"
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: el,
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      el.style.visibility = "visible";
    }
  });
</script> 
```

### mboxDefine() et mboxUpdate()

**Description** :

Crée un mappage interne entre un élément et le nom d’une mbox, mais n’exécute pas la demande. Utilisé conjointement avec `mboxUpdate()`, qui exécute la requête et applique l’offre à l’élément identifié par le nodeld dans `mboxDefine()`. Cette fonction peut être également utilisée pour mettre à jour une mbox initiée par `mboxCreate`.

**Exemple** :

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"></div>
<script>
 mboxDefine('someId','mboxName','param1=value1','param2=value2');
 mboxUpdate('mboxName','param3=value3','param4=value4');
</script>
```

**Équivalent at.js 2.*x*** :

Une alternative à `mboxDefine()` et `mboxUpdate`, est `getOffer()` et `applyOffer()`, avec l’option de sélecteur utilisée dans `applyOffer()`. Cette approche permet de mapper l’offre à un élément à l’aide d’un sélecteur CSS, et pas seulement avec un identifiant.

**Exemple** :

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2",
      param3: "value3",
      param4: "value4" 
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: "#someId",
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      var el = document.getElementById("someId");
      el.style.visibility = "visible";
    }
  });
</script>
```

### adobe.target.registerExtension()

**Description** :

Propose une méthode standard pour enregistrer une extension spécifique.

Ce paramètre n’est plus pris en charge et ne doit pas être utilisé.

## Résumé des fonctions at.js obsolètes, nouvelles et prises en charge dans 2.*x*

| Méthode | Pris en charge ? | Nouveau ? | Obsolète ?<P>(Le contenu par défaut s’affiche) |
| --- | --- | --- | --- |
| `getOffer()` | Oui |  |  |
| `getOffers()` |  | Oui |  |
| `applyOffer()` | Oui |  |  |
| `applyOffers()` |  | Oui |  |
| `triggerView()` |  | Oui |  |
| `trackEvent()` | Oui |  |  |
| `mboxCreate()` |  |  | Oui |
| `mboxDefine()`<P>`mboxUpdate()` |  |  | Oui |
| `targetGlobalSettings()` | Oui |  |  |
| `Data Providers` | Oui |  |  |
| `targetPageParams()` | Oui |  |  |
| `targetPageParamsAll()` | Oui |  |  |
| `registerExtension()` |  |  | Oui |
| `At.js Custom Events` | Oui |  |  |

## Limites et légendes

Gardez à l’esprit les limites et légendes suivantes :

### Suivi des conversions

Les clients qui utilisent `mboxCreate()` le suivi de conversion doivent utiliser `trackEvent()` ou `getOffer()`.

### Présentation des offres

Clients qui ne remplacent `mboxCreate()` pas les `getOffer()` offres ou `applyOffer()` ne les risquent pas.

### Peut-on utiliser at.js 2.*x* sur certaines pages pendant que at.js 1.*x* est sur d’autres pages ?

Oui, le profil du visiteur est conservé sur plusieurs pages à l’aide de différentes versions et bibliothèques. Le format de cookie est identique.

### Nouvelle utilisation de l’API dans at.js 2.*x*

at.js 2.*x* utilise une nouvelle API, que nous appelons l’API de diffusion. Pour déboguer si at.js appelle correctement le serveur Edge de [!DNL Target], vous pouvez filtrer l’onglet Réseau des outils de développement de votre navigateur par « diffusion », « `tt.omtrdc.net` » ou votre code client. Vous remarquerez également que [!DNL Target] envoie une charge utile JSON plutôt que des paires clé-valeur.

### [!DNL Target] mbox globale n’est plus utilisée

Dans at.js 2.*x*, vous ne voyez plus « `target-global-mbox` » de manière visible dans les appels réseau. Au lieu de cela, nous avons remplacé la syntaxe « `target-global-mbox` » par « `execute > pageLoad` » dans la payload JSON envoyée aux serveurs [!DNL Target], comme illustré ci-dessous :

```json {line-numbers="true"}
{
  "id": {
    // ...
  },
  "context": {
    "channel": "web",
    // ...
  },
  "execute": {
    "pageLoad": {}
  }
}
```

Essentiellement, le concept de mbox globale a été introduit pour faire savoir à [!DNL Target] si les offres et le contenu doivent être récupérés au chargement de la page. Cela a donc été plus explicite dans notre nouvelle version.

### Le nom de la mbox globale dans at.js est-il plus volumineux ?

Les clients peuvent spécifier un nom de mbox global via **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit at.js Settings]**. Ce paramètre est utilisé par les [!DNL Target] serveurs Edge pour convertir exécuter > pageload en nom de mbox globale, qui apparaît dans [!DNL Target] l’interface utilisateur. Ainsi, les clients peuvent continuer à utiliser les API côté serveur, le compositeur basé sur les formulaires, les scripts de profil et créer des audiences à l’aide du nom de mbox globale. Nous vous recommandons vivement de vous assurer que le même nom de mbox globale est configuré sur la page **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]** également, au cas où vous auriez encore des pages utilisant at.js 1.*x*, comme illustré ci-dessous.

![Modification de la boîte de dialogue at.js](../assets/modify-atjs.png)

et

![Mbox globale personnalisée](../assets/custom-global-mbox.png)

### Le paramètre de mbox globale de création automatique doit-il être activé pour at.js 2 ?*x* ?

Dans la plupart des cas, oui. Ce paramètre indique à at.js 2.*x* pour déclencher une requête sur les serveurs edge de [!DNL Target] au chargement de la page. La mbox globale étant traduite pour exécuter > pageload, ce paramètre doit être activé si vous souhaitez déclencher une requête au chargement de la page.

### Les activités du compositeur d’expérience visuelle existantes continueront-elles de fonctionner, même si le nom de la mbox globale cible n’est pas spécifié à partir d’at.js 2 ?*x* ?

Oui, car exécuter > pageload est traité sur le [!DNL Target] serveur principal comme `target-global-mbox`.

### Si mes activités basées sur des formulaires sont ciblées sur `target-global-mbox`, ces activités continueront-elles à fonctionner ?

Oui, car exécuter > pageload est traité sur les [!DNL Target] serveurs Edge comme `target-global-mbox`.

### at.js pris en charge et non pris en charge 2.Paramètres *x*

| Paramètre | Pris en charge ? |
| --- | --- |
| X-Domaine | Non |
| Créer automatiquement la mbox globale | Oui |
| Nom de mbox globale | Oui |

### Prise en charge du suivi inter-domaines dans at.js 2.x

Le suivi inter-domaines permet de regrouper les visiteurs dans différents domaines. Un nouveau cookie devant être créé pour chaque domaine, il est difficile de suivre les visiteurs lorsqu’ils passent d’un domaine à l’autre. Pour effectuer le suivi inter-domaines, [!DNL Target] utilise un cookie tiers pour suivre les visiteurs entre les domaines. Vous pouvez ainsi créer une activité [!DNL Target] qui s’étend sur `siteA.com` et `siteB.com` et les visiteurs restent dans la même expérience lorsqu’ils naviguent sur des domaines uniques. Cette fonctionnalité est liée au comportement des cookies tiers et propriétaires d’[!DNL Target].

>[!NOTE]
>
>Le suivi inter-domaines est pris en charge à partir d’at.js 2.10, mais n’est pas pris en charge par défaut dans at.js 2.*x* antérieur à 2.10. Le suivi inter-domaines est pris en charge dans at.js 2.*x* via la bibliothèque Experience Cloud ID (ECID) v4.3.0+.

En [!DNL Target], le cookie tiers est stocké dans `<CLIENTCODE>.tt.omtrdc.net`. Le cookie propriétaire est stocké dans `clientdomain.com`. Première requête de renvoi des en-têtes de réponse HTTP qui tentent de définir des cookies tiers nommés `mboxSession` et `mboxPC` tandis qu’une requête de redirection est renvoyée avec un paramètre supplémentaire (`mboxXDomainCheck=true`). Si le navigateur accepte les cookies tiers, la requête de redirection inclut ces cookies et l’expérience est renvoyée. Ce processus est possible car nous utilisons la méthode HTTP GET.

Toutefois, dans at.js 2.*x*, le GET HTTP n’est pas utilisé. Au lieu de cela, la requête HTTP POST est utilisée via at.js 2.*x* pour envoyer des payloads JSON aux serveurs [!DNL Target] Edge. L’utilisation de la requête HTTP POST signifie que la requête de redirection visant à vérifier si un navigateur prend en charge les cookies tiers sera interrompue. Cela est dû au fait que les requêtes HTTP GET sont des transactions idempotentes, tandis que HTTP POST est non idempotent et ne doit pas être répété arbitrairement. Par conséquent, le suivi inter-domaines dans at.js 2.*x* (antérieur à la version 2.10) n’est pas pris en charge prêt à l’emploi. Seul at.js 1.*x* assure la prise en charge par défaut du suivi inter-domaines.

Pour utiliser le suivi inter-domaines pour at.js v2.10 ou une version ultérieure, vous pouvez effectuer l’une des opérations suivantes :

1. Installez la bibliothèque [ECID v4.3.0+](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=fr) conjointement avec at.js 2.*x*. Le but de la bibliothèque ECID est de gérer les ID persistants utilisés pour identifier un visiteur et ce même entre les domaines. Après avoir installé la bibliothèque ECID v4.3.0+ et at.js 2.*x*, vous pouvez créer des activités qui s’étendent sur des domaines uniques et effectuer le suivi des utilisateurs. Il est important de noter que cette fonctionnalité ne fonctionne qu’après l’expiration de la session.

1. Au lieu d’installer la bibliothèque ECID, si vous disposez d’at.js version 2.10 ou ultérieure, vous pouvez activer le paramètre interdomaines dans l’interface utilisateur [!DNL Target] dans **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. (Vous pouvez également définir l’option _crossDomain_ sur _enabled_ dans le code at.js.)

Pour utiliser le suivi inter-domaines pour les versions d’at.js v2.*x* avant la version 2.10, vous pouvez implémenter l’option #1 ci-dessus (installer la bibliothèque ECID).

### La création automatique de la mbox globale est prise en charge

Ce paramètre indique à at.js 2.*x* pour déclencher une requête sur les serveurs Edge de [!DNL Target] au chargement de la page. Etant donné que la mbox globale est convertie pour exécuter > pageLoad, et que cela est interprété par les serveurs Edge [!DNL Target], les clients doivent activer cette fonction s’ils souhaitent déclencher une requête au moment du chargement de la page.

### Le nom de la mbox globale est pris en charge

Les clients peuvent spécifier un nom de mbox global via **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]**. Ce paramètre est utilisé par les serveurs Edge [!DNL Target] pour convertir exécuter > pageLoad en nom de la mbox globale saisi. Cela permet aux clients de continuer à utiliser les API côté serveur, le compositeur basé sur les formulaires, les scripts de profil et de créer les audiences qui ciblent la mbox globale.

### Les événements personnalisés at.js ci-dessous sont-ils applicables à `triggerView()` ou n’est-ce que pour `applyOffer()` ou `applyOffers()` ?

* `adobe.target.event.CONTENT_RENDERING_FAILED`
* `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`
* `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`
* `adobe.target.event.CONTENT_RENDERING_REDIRECT`

Oui, les événements personnalisés at.js s’appliquent à `triggerView()` également.

### Elle indique que lorsque j’appelle `triggerView()` avec &amp;lbrace;`"page" : "true"`&amp;rbrace;, une notification est envoyée au serveur principal [!DNL Target] et l’impression est augmentée. Cela entraîne-t-il également l’exécution des scripts de profil ?

Lorsqu’un appel de pré-récupération est effectué au [!DNL Target] principal, les scripts de profil sont exécutés. Ensuite, les données de profil impactées seront chiffrées et retransmises côté client. Après l’appel de `triggerView()` avec `{"page": "true"}`, une notification est envoyée avec les données de profil chiffrées. C’est alors que l’arrière-plan [!DNL Target] déchiffrera les données de profil et les stockera dans les bases de données.

### Devons-nous ajouter un prémasquage du code avant d’appeler `triggerView()` pour gérer le scintillement ?

Non, il n’est pas nécessaire d’ajouter un prémasquage du code avant d’appeler `triggerView()`. at.js 2.*x* gère la logique de pré-masquage et de scintillement avant que la vue ne soit affichée et appliquée.

### Quel at.js 1.Les paramètres *x* de création d’audiences ne sont pas pris en charge dans at.js 2.*x* ?

Les paramètres at.js 1.x suivants ne sont *PAS* actuellement pris en charge pour la création d’audiences lors de l’utilisation d’at.js 2.*x* :

* browserHeight
* browserWidth
* browserTimeOffset
* screenHeight
* screenWidth
* screenOrientation
* colorDepth
* devicePixelRatio
* vst.* paramètres (voir ci-dessous)

### at.js 2.*x* ne prend pas en charge la création d’audiences à l’aide de paramètres.* paramètres

Clients sur at.js 1.*x* ont pu utiliser vst.* Paramètres de mbox pour créer des audiences. Il s’agissait d’un effet secondaire inattendu de la méthode d’at.js 1.*x* a envoyé les paramètres de mbox au serveur principal [!DNL Target]. Après la migration vers at.js 2.*x*, vous ne pouvez plus créer d’audiences à l’aide de ces paramètres, car at.js 2.*x* envoie les paramètres de mbox différemment.

## Compatibilité at.js

Les tableaux suivants décrivent at.js. compatibilité 2.*x* avec différents types d’activités, intégrations, fonctionnalités et fonctions at.js ;

### Types d’activités

| Type | Pris en charge ? |
| --- | --- |
| [!UICONTROL A/B Test] | Oui |
| [!UICONTROL Auto-Allocate] | Oui |
| [!UICONTROL Auto-Target] | Oui |
| [!UICONTROL Experience Targeting] | Oui |
| [!UICONTROL Multivariate Test] | Oui |
| [!UICONTROL Automated Personalization] | Oui |
| [!DNL Recommendations] | Oui |

>[!NOTE]
>
>Les activités [!UICONTROL Auto-Target] sont prises en charge par at.js 2.*x* et le compositeur d’expérience visuelle lorsque toutes les modifications sont appliquées au `Page Load Event`. Lorsque des modifications sont ajoutées à des vues spécifiques, seules les activités [!UICONTROL A/B Test], [!UICONTROL Auto-Allocate] et [!UICONTROL Experience Targeting] (XT) sont prises en charge.

### Intégrations

| Type | Pris en charge ? |
| --- | --- |
| [!UICONTROL Analytics for Target] (A4T) | Oui |
| Audiences | Oui |
| Attributs du client | Oui |
| Fragments d’expérience AEM | Oui |
| [Extension ](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) | Oui |
| Débogueur | Oui |
| Auditeur | Les règles n’ont pas encore été mises à jour pour at.js 2.*x* |
| Prise en charge de l’Opt-in pour le [RGPD](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) | Cette fonctionnalité est prise en charge dans [at.js version 2.1.0](/help/dev/implement/client-side/atjs/target-atjs-versions.md#atjs-version-210-june-3-2019) ou ultérieure. |
| Personalization amélioré d’AEM optimisé par [!DNL Adobe Target] | Non |

### Fonctionnalités

| Fonctionnalité | Pris en charge ? |
| --- | --- |
| X-Domaine | Non |
| Propriétés / Espaces de travail | Oui |
| Liens d’assurance qualité | Oui |
| Compositeur d’expérience d’après les formulaires | Oui |
| Compositeur d’expérience visuelle (VEC) | Oui |
| Code personnalisé | Oui |
| [Jetons de réponse](#response-tokens) | Oui |
| Suivi des clics | Oui |
| Diffusion multi-activité | Oui |
| targetGlobalSettings | Oui (mais pas x-domaine) |
| Méthodes at.js | Tout est pris en charge, sauf<P>`mboxCreate()`<P>`mboxUpdate()`<P>`mboxDefine()`<P>qui affiche le contenu par défaut. |

### Paramètres de chaîne de requête

| Paramètre | Pris en charge ? |
| --- | --- |
| `?mboxDisable` | Oui |
| `?mboxDisable` | Oui |
| `?mboxTrace` | Oui |
| `?mboxSession` | Non |
| `?mboxOverride.browserIp` | Oui |

## Jetons de réponse

at.js 2.*x*, tout comme at.js 1.*x*, utilise l’événement personnalisé `at-request-succeeded` pour les jetons de réponse de surface. Pour des exemples de code utilisant l’événement `at-request-succeeded` personnalisé, voir [Jetons réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html).

## Paramètres at.js 1.Paramètres *x* pour at.js 2.Mappage de la payload *x*

Cette section décrit les mappages entre at.js 1.*x* et at.js 2.*x*.

Avant de passer à la correspondance des paramètres, les points d’entrée que ces versions de bibliothèque utilisent ont changé :

* at.js 1.*x* - `http://<client code>.tt.omtrdc.net/m2/<client code>/mbox/json`
* at.js 2.*x* - `http://<client code>.tt.omtrdc.net/rest/v1/delivery`

Une autre différence majeure réside dans le fait que :

* at.js 1.*x* - Le code client fait partie du chemin d’accès
* at.js 2.*x* - Le code client est envoyé en tant que paramètre de chaîne de requête, tel que :
  `http://<client code>.tt.omtrdc.net/rest/v1/delivery?client=democlient`

Les sections suivantes répertorient chaque at.js 1.Paramètre *x*, sa description et le 2 correspondant.Payload JSON *x* (le cas échéant) :

### at_property

(at.js 1.*x* paramètre)

Utilisé pour [les permissions utilisateur d’entreprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=fr).

```json {line-numbers="true"}
{
  ....
  "property": {
    "token": "1213213123122313121"
  }
  ....
}
```

### mboxHost

(at.js 1.*x* paramètre)

Domaine de la page sur laquelle s’exécute la bibliothèque [!DNL Target].

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "host": "test.com"
    }
  }
}
```

### webGLRenderer

(at.js 1.*x* paramètre)

Fonctionnalités du rendu WEB GL du navigateur. Ce mécanisme est utilisé par notre mécanisme de détection d’appareil pour déterminer si l’appareil du visiteur est un ordinateur, un iPhone, un appareil Android, etc.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "webGLRenderer": "AMD Radeon Pro 560X OpenGL Engine"
    }
  }
}
```

### mboxURL

(at.js 1.*x* paramètre)

URL de la page.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "url": "http://test.com"
    }
  }
}
```

### mboxReferrer

(at.js 1.*x* paramètre)

Référent de la page.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "referringUrl": "http://google.com"
    }
  }
}
```

### mbox (nom) est égal à mbox globale

(at.js 1.*x* paramètre)

L’API de diffusion n’a plus de concept de mbox globale. Dans la charge utile JSON, vous devez utiliser `execute > pageLoad`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "execute": {
    "pageLoad": {
       "parameters": ....
       "profileParameters": ...
       .....
    }
  }
}
```

### mbox (nom) n’est *pas* égale à la mbox globale

(at.js 1.*x* paramètre)

Pour utiliser un nom de mbox, transmettez-le `execute > mboxes`. Une mbox requiert un index et un nom.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "execute": {
    "mboxes": [{
       "index": 0,
       "name": "some-mbox",
       "parameters": ....
       "profileParameters": ...
       .....
    }]
  }
}
```

### mboxId

(at.js 1.*x* paramètre)

N’est plus utilisée.

### mboxCount

(at.js 1.*x* paramètre)

N’est plus utilisée.

### mboxRid

(at.js 1.*x* paramètre)

ID de requête utilisé par les systèmes en aval pour faciliter le débogage.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "requestId": "2412234442342"
  ....
}
```

### mboxTime

(at.js 1.*x* paramètre)

N’est plus utilisée.

### mboxSession

(at.js 1.*x* paramètre)

L’ID de session est envoyé en tant que paramètre de chaîne de requête (`sessionId`) au point d’entrée de l’API de diffusion.

### mboxPC

(at.js 1.*x* paramètre)

L’identifiant TNT est transmis `id > tntId`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "id": {
    "tntId": "ca5ddd7e33504c58b70d45d0368bcc70.21_3"
  }
  ....
}
```

### mboxMCGVID

(at.js 1.*x* paramètre)

L’identifiant visiteur Experience Cloud est transmis `id > marketingCloudVisitorId`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "id": {
    "marketingCloudVisitorId": "797110122341429343505"
  }
  ....
}
```

### `vst.aaaa.id` et `vst.aaaa.authState`

(at.js 1.*x* paramètres)

Les identifiants de client doivent `id > customerIds`être transmis.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "id": {
    "customerIds": [{
       "id": "1232131",
       "integrationCode": "aaaa",
       "authenticatedState": "....."
     }]
  }
  ....
}
```

### mbox3rdPartyId

(at.js 1.*x* paramètre)

ID tiers du client utilisé pour lier différents ID de [!DNL Target].

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "id": {
    "thirdPartyId": "1232312323123"
  }
  ....
}
```

### mboxMCSDID

(at.js 1.*x* paramètre)

SDID, également appelé identifiant de données supplémentaires. Doit être transmis `experienceCloud > analytics > supplementalDataId`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "supplementalDataId": "1212321132123131"
    }
  }
  ....
}
```

### vst.trk

(at.js 1.*x* paramètre)

Serveur de suivi [!UICONTROL Analytics]. Doit être transmis `experienceCloud > analytics > trackingServer`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServer": "analytics.test.com"
    }
  }
  ....
}
```

### vst.trks

(at.js 1.*x* paramètre)

Serveur de suivi Analytics sécurisé. Doit être transmis `experienceCloud > analytics > trackingServerSecure`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServerSecure": "secure-analytics.test.com"
    }
  }
  ....
}
```

### mboxMCGLH

(at.js 1.*x* paramètre)

Conseil d’emplacement d’Audience Manager. Doit être transmis `experienceCloud > audienceManager > locationHint`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "locationHint": 9
    }
  }
  ....
}
```

### mboxAAMB

(at.js 1.*x* paramètre)

Blob Audience Manager. Doit être transmis `experienceCloud > audienceManager > blob`.

at.js 2.Payload JSON *x* :

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "blob": "2142342343242342"
    }
  }
  ....
}
```

### mboxVersion

(at.js 1.*x* paramètre)

La version est envoyée en tant que paramètre de chaîne de requête via le paramètre de version.

## Vidéo de formation : at.js 2.Schéma architectural *x* ![Badge d’aperçu](../../assets/overview.png)

at.js 2.*x* améliore la prise en charge des SPA par Adobe [!DNL Target] et s’intègre à d’autres solutions Experience Cloud. Cette vidéo explique comment tout se connecte.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Voir [Comprendre comment at.js 2.*x* fonctionne](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html) pour plus d’informations.

