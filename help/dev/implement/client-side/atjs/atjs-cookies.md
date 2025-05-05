---
keywords: at.js, 2.0, 1.x, cookies
description: Détails sur la façon dont  [!DNL Adobe Target] at.js 2.x et at.js 1.x gèrent les cookies
title: Cookies at.js
feature: at.js
exl-id: 154a844a-6855-4af7-8aed-0719b4c389f5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 72%

---

# cookies at.js

Informations concernant at.js 2.x et at.js 1.comportement du cookie *x*.

## Comportement des cookies at.js 2.x

Pour at.js version 2.x (jusqu’à la version 2.10.0, mais non incluse), *seuls les cookies propriétaires sont pris en charge*. Comme pour at.js 1.*x*, le cookie propriétaire, &quot;mbox&quot;, est stocké dans `clientdomain.com`, où `clientdomain` correspond à votre domaine.

at.js génère un ID de session et le stocke dans le cookie. La première réponse contient les informations d’activité, ainsi que le `TNT` ou le `PC ID` générés par les serveurs [!DNL Target]. at.js écrit ensuite le `TNT/PC ID` dans le cookie.

Le cookie propriétaire `AMCV_###@AdobeOrg` est toujours défini par le service d’ID Experience Cloud, bien que le `ECID` soit transmis dans les requêtes [!DNL Target].

>[!NOTE]
>
>Pour at.js versions 2.10.0 et ultérieures, les cookies propriétaires et interdomaines sont pris en charge.

### Prise en charge des cookies tiers et du suivi inter-domaines.

Le suivi inter-domaines permet d’afficher les sessions sur deux sites associés, mais avec des domaines différents, dans une session unique. Vous pourriez créer une activité [!DNL Target] qui couvre `siteA.com` et `siteB.com`, et le visiteur resterait dans la même expérience en changeant de domaine. Cette fonctionnalité est liée au comportement de at.js 1.*x* tiers et comportement du cookie de première partie.

>[!NOTE]
>
>Pour at.js versions 2.10.0 et ultérieures, les cookies tiers et le suivi inter-domaines sont pris en charge.


## at.js 1.Comportement du cookie *x*

Pour at.js versions 1.*x*, le comportement du cookie varie selon qu’il s’agit d’un cookie propriétaire, d’un cookie tiers avec un cookie propriétaire ou d’un cookie tiers seul.

### Quand utiliser les cookies propriétaires ou tiers

La configuration de votre site détermine le type de cookies que vous allez utiliser. Il est utile de comprendre le fonctionnement de [!DNL Target] lorsque vous essayez de comprendre les cookies propriétaires et tiers. Pour plus d’informations, voir [Fonctionnement de  [!DNL Adobe Target] 2&rbrace; .](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html)

Il existe trois principaux cas d’utilisation des cookies :

1. Un domaine.

   L’ensemble des tests a lieu dans un domaine de niveau supérieur (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, etc.).

   Utilisez uniquement des cookies propriétaires. Il s’agit de l’utilisation par défaut.

1. Les utilisateurs passent d’un domaine à un autre et vous souhaitez effectuer un suivi et tester leur comportement sur ces domaines.

   Exemple : un utilisateur effectue des achats sur votre site mais procède à des vérifications dans des boutiques Yahoo. Trois approches (déterminez la meilleure approche avec le représentant de compte) :

   * Activez les cookies propriétaires et tiers.
   * Activez les cookies tiers uniquement (très rare, mais cela permet de conserver le cookie at.js en dehors de votre domaine).
   * Activez uniquement les cookies propriétaires et transmettez le paramètre `mboxSession` lors de la transition entre domaines.

     Le paramètre `mboxSession` doit être transmis dans une page de destination avec at.js référencé. Il ne peut pas s’agir d’une page de redirection intermédiaire.

1. Vous utilisez uniquement des adbox ou des Flashbox sur un site tiers.

   Deux approches (déterminez la meilleure approche avec le directeur du service clientèle) :

   * Activez les cookies propriétaires et tiers.

     Les cookies propriétaires et tiers sont requis pour les Flashbox et les créations dynamiques.

   * Activez uniquement les cookies tiers.

     Cette approche s’applique uniquement lorsque des mises en œuvre AdBox sont utilisées sans ciblage sur site (rare).

### Comportement du cookie propriétaire

Le cookie propriétaire est stocké dans `clientdomain.com`, où `clientdomain` correspond à votre domaine.

at.js génère un `mboxSession ID` et le stocke dans le cookie. La première réponse contient l’offre, ainsi que le JavaScript permettant de stocker dans le cookie le `mboxPC ID` généré par l’application.

>[!NOTE]
>
>Le cookie propriétaire `AMCV_###@AdobeOrg` est toujours défini avec l’identifiant visiteur Experience Cloud.

### Comportement des cookies tiers

Les cookies tiers sont stockés dans `clientcode.tt.omtrdc.net` et le cookie propriétaire dans `clientdomain.com`, où `clientdomain` correspond à votre domaine.

at.js génère une `mboxSession ID`. La première requête d’emplacement renvoie des en-têtes de réponse HTTP qui tentent de définir des cookies tiers nommés `mboxSession` et `mboxPC` et une requête de redirection est renvoyée avec un paramètre supplémentaire (`mboxXDomainCheck=true`).

Si le navigateur accepte les cookies tiers, la requête de redirection inclut ces cookies et l’offre est renvoyée.

Si le navigateur rejette les cookies tiers, la requête de redirection n’inclut pas ces cookies et le contenu par défaut s’affiche pour tous les emplacements de la page. Puisqu’aucun cookie n’est défini, le processus ci-dessus se reproduit pour chaque requête de page.

### Comportement des cookies tiers et propriétaires

Les cookies tiers sont stockés dans `clientcode.tt.omtrdc.net` et le cookie propriétaire dans `clientdomain.com`, où `clientdomain` correspond à votre domaine.

at.js génère une `mboxSession ID`. La première requête d’emplacement renvoie des en-têtes de réponse HTTP qui tentent de définir des cookies tiers nommés `mboxSession` et `mboxPC` et une requête de redirection est renvoyée avec un paramètre supplémentaire (`mboxXDomainCheck=true`).

Si le navigateur accepte les cookies tiers, la requête de redirection inclut ces cookies et l’offre est renvoyée.

Certains navigateurs rejettent les cookies tiers. Dans ce cas, le cookie propriétaire continue de fonctionner. [!DNL Target] tente de définir le cookie tiers. S’il n’y parvient pas, [!DNL Target] ne peut qu’effectuer un suivi sur le domaine spécifique du client. Le suivi inter-domaines ne fonctionne pas si les cookies tiers sont bloqués, sauf si `mboxSession` est annexé au lien qui traverse les domaines. Dans ce cas, un autre cookie propriétaire est défini et synchronisé avec le cookie propriétaire du domaine précédent.

## Paramétrage des cookies

Le cookie s’accompagne de plusieurs paramètres par défaut. Vous pouvez modifier ces paramètres, si nécessaire, à l’exception de la durée des cookies. Consultez le représentant de votre compte lorsque vous modifiez les paramètres du cookie.

| Paramètre | Informations |
|--- |--- |
| Nom du cookie | mbox. |
| Domaine du cookie | Niveaux secondaire et supérieur des domaines à partir desquels vous publiez le contenu. Il s’agit d’un cookie propriétaire, puisqu’il est diffusé à partir du domaine de votre société. Exemple : `mycompany.com`. |
| Domaine du serveur | `clientcode.tt.omtrdc.net`, à l’aide du code client de votre compte. |
| Durée du cookie | Le cookie reste sur le navigateur du visiteur deux ans après sa dernière connexion.<P>Le paramètre `deviceIdLifetime` peut être remplacé dans [at.js version 2.3.1 ou ultérieure](../atjs/target-atjs-versions.md). Pour plus d’informations, voir [targetGlobalSettings()](../../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md). |
| Stratégie P3P | Le cookie est publié avec une stratégie P3P, comme requis par le paramètre par défaut de la plupart des navigateurs. Une stratégie P3P indique à un navigateur qui publie le cookie et comment sont utilisées les informations. |

Le cookie conserve certaines valeurs afin de gérer la façon dont les visiteurs expérimentent les campagnes :

| Valeur | Définition |
|--- |--- |
| session ID | ID unique pour une session utilisateur. Dure 30 minutes par défaut. |
| pc ID | Identifiant semi-permanent pour le navigateur d’un visiteur. Dure 14 jours. |
| check | Valeur de test unique déterminant si un visiteur prend en charge les cookies. Définie chaque fois qu’un visiteur demande une page. |
| disable | Défini si le temps de chargement d’un visiteur dépasse le délai configuré dans le SDK Web Adobe Experience Platform ou le fichier at.js. Dure 1 heure par défaut. |

## Impact sur [!DNL Target] pour les visiteurs Safari suite aux modifications de suivi du WebKit Apple

Gardez à l’esprit les éléments suivants :

### Comment fonctionne le suivi [!DNL Adobe Target] ?

| Cookies | Détails |
|--- |--- |
| Domaines propriétaires | Il s’agit de l’implémentation standard pour les clients [!DNL Target].  Les cookies « mbox » sont définis dans le domaine du client. |
| Suivi tiers | Le suivi tiers est important pour les cas pratiques de publicité et de ciblage dans [!DNL Target] et dans [!DNL Adobe Audience Manager] (AAM).  Le suivi tiers nécessite des techniques de script de site à site. [!DNL Target] utilise deux cookies, &quot;mboxSession&quot; et &quot;mboxPC&quot; définis dans le domaine `clientcode.tt.omtrd.net`. |

### Quelle est l’approche d’Apple ?

Extrait d’Apple :

« Intelligent Tracking Prevention (Prévention intelligente du suivi) est une nouvelle fonctionnalité WebKit qui réduit le suivi des sites en limitant davantage les cookies et les autres données du site Web. »

« C’est ce qu’on appelle un suivi intersite. Le cookie utilisé par `example-tracker.com` s’appelle un cookie tiers. Lors de nos tests, nous avons identifié des sites Web populaires avec plus de 70 trackers, qui collectaient tous en silence des données sur les utilisateurs. »

| Approche | Détails |
|--- |--- |
| Intelligent Tracking Prevention (Prévention intelligente du suivi) | Pour en savoir plus, reportez-vous à la section [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) sur le site du navigateur Web Open Source, WebKit. |
| Cookies | Comment Safari traite les cookies :<ul><li>Les cookies tiers qui ne se trouvent pas dans un domaine auquel l’utilisateur accède directement ne sont jamais enregistrés. Ce comportement n’est pas neuf. Les cookies tiers ne sont déjà plus pris en charge dans Safari.</li><li>Les cookies tiers définis dans un domaine auquel l’utilisateur accède directement sont effacés après 24 heures.</li><li>Les cookies tiers sont effacés après 30 jours si le domaine propriétaire est classé comme suivant les utilisateurs de site en site. Ce problème peut concerner les grandes entreprises qui envoient les utilisateurs vers différents domaines en ligne. Apple n’a pas précisé clairement comment ces domaines seront classés, ou comment un domaine peut déterminer s’ils sont classés comme suivant les utilisateurs de site en site.</li></ul> |
| L’apprentissage automatique pour identifier les domaines intersites | Extrait d’Apple :<P>Machine Learning Classifier : modèle d’apprentissage automatique utilisé pour classer les domaines régis par le contrôle privé afin de pouvoir suivre l’utilisateur de site en site, en fonction des statistiques collectées. Sur les différentes statistiques recueillies, trois vecteurs se sont avérés avoir un signal fort pour la classification en fonction des pratiques de suivi actuelles : sous-ressource sous le nombre de domaines uniques, sous-trame sous le nombre de domaines uniques et nombre de domaines uniques redirigés. Toute la collecte et la classification des données se produisent sur le périphérique.<P>Cependant, si l’utilisateur interagit avec example.com comme domaine supérieur, souvent appelé domaine propriétaire, la prévention intelligente du suivi considère qu’il s’agit d’un signal que l’utilisateur est intéressé par le site web et ajuste temporairement son comportement comme illustré dans cette chronologie :<P>Si l’utilisateur a interagi avec example.com au cours des dernières 24 heures, ses cookies seront disponibles lorsque `example.com` est un tiers. Cela me permet de « me connecter avec mon compte X sur les scénarios de connexion Y. »<ul><li>Les domaines visités comme domaines de haut niveau ne seront pas affectés. Des sites comme OKTA, par exemple.</li><li>Identifie les domaines qui sont des sous-domaines ou des sous-cadres de la page active sur plusieurs domaines uniques.</li></ul> |

### Comment Adobe sera-t-il affecté ?

| Fonctionnalités affectées | Détails |
|--- |--- |
| Prise en charge de l’exclusion | La fonction de suivi du WebKit d’Apple modifie la prise en charge de l’exclusion.<P>L’exclusion de [!DNL Target] utilise un cookie dans le domaine `clientcode.tt.omtrdc.net`. Pour plus d’informations, consultez la section [Confidentialité](/help/dev/before-implement/privacy/privacy.md)<P>[!DNL Target] prend en charge deux exclusions :<ul><li>une par client (le client gère le lien d’exclusion) ;</li><li>Un par Adobe qui exclut l’utilisateur de toutes les fonctionnalités [!DNL Target] pour tous les clients.</li></ul>Ces deux méthodes utilisent le cookie tiers. |
| [!DNL Target] activités | Les clients peuvent choisir leur [durée de vie du profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) pour leurs comptes [!DNL Target] (jusqu’à 90 jours). Le problème est que si la durée de vie du profil du compte est supérieure à 30 jours et que le cookie propriétaire est purgé car le domaine du client a été marqué comme suivant les utilisateurs sur plusieurs sites, le comportement des visiteurs Safari sera affecté dans les zones suivantes de [!DNL Target] :<P>**[!DNL Target]Rapports** : si un utilisateur Safari entre dans une activité, revient après 30 jours, puis convertit, cet utilisateur compte comme deux visiteurs et une conversion.<P>Ce comportement est le même pour les activités utilisant [!DNL Analytics] comme source de création de rapports (A4T).<P>**Profil et appartenance à une activité** :<ul><li>Les données du profil sont effacées lorsque le cookie propriétaire expire.</li><li>L’appartenance à une activité est effacée lorsque le cookie propriétaire expire.</li><li> [!DNL Target] ne fonctionne pas dans Safari pour les comptes qui utilisent une implémentation de cookies tiers ou une implémentation de cookies propriétaires et tiers. Notez que ce comportement n’est pas récent. Cela fait un certain temps déjà que Safari n’autorise plus les cookies tiers.</li></ul><P>**Suggestions** : s’il existe un risque que le domaine du client soit marqué comme un suivi des visiteurs d’une session à l’autre, il est plus prudent de définir la durée de vie du profil sur 30 jours ou moins dans [!DNL Target]. Ceci garantit que les utilisateurs seront suivis de la même manière dans Safari et tous les autres navigateurs. |
