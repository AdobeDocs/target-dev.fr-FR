---
keywords: Présentation et référence, webkit, cookies, propriétaires, tiers, propriétaires, tiers, tiers, tiers, 8 $
description: Découvrez le comportement des cookies Target (cookie propriétaire, cookie tiers avec cookie propriétaire ou cookie tiers seul).
title: Où Trouver Des Informations Sur Les Cookies Target ?
feature: at.js
role: Developer
source-git-commit: 39f390a0e5eedf8c6957333759d31d96ed11b321
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 53%

---

# Cookies Target

Le comportement des cookies varie selon qu’il s’agit d’un cookie propriétaire, d’un cookie tiers avec un cookie propriétaire ou d’un cookie tiers seul.

>[!NOTE]
>
>Cette rubrique contient des informations sur `mboxSession` et `mboxPC`. Les bonnes pratiques d’implémentation recommandent de ne pas lier ni stocker d’informations sensibles aux données de cookie : `mboxSession` ou `mboxPC`.

Voir aussi [Suppression du cookie Target](/help/dev/before-implement/privacy/cookie-deleting.md).

## Quand utiliser les cookies propriétaires ou tiers

La configuration de votre site détermine le type de cookies que vous allez utiliser. Il s’avère utile de connaître le fonctionnement de Target pour bien comprendre les cookies propriétaires et tiers. Consultez [Fonctionnement d’Adobe Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) pour plus d’informations.

Il existe trois principaux cas d’utilisation des cookies :

1. Un domaine.

   Tous vos tests ont lieu dans un domaine de niveau supérieur (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, etc.).

   Approche : utilisez uniquement des cookies propriétaires (valeur par défaut).

1. Les utilisateurs passent d’un domaine à un autre et vous souhaitez effectuer un suivi et tester leur comportement sur ces domaines.

   Exemple : un utilisateur effectue des achats sur votre site mais procède à des vérifications dans des boutiques Yahoo. Trois approches (déterminez la meilleure approche avec le représentant de compte) :

   * Activez les cookies propriétaires et tiers.
   * Activez les cookies tiers uniquement (rare, mais permet de conserver le cookie mbox en dehors de votre domaine).
   * Activez uniquement les cookies propriétaires et transmettez le paramètre `mboxSession` lors de la transition entre domaines.

     Le paramètre `mboxSession` doit être transmis à une page d’entrée et référencé à partir de la bibliothèque JavaScript (SDK Web Adobe Experience Platform ou at.js). Il ne peut pas s’agir d’une page de redirection intermédiaire.

1. Vous utilisez uniquement les adbox ou les Flashbox sur un site tiers.

   Deux approches (déterminez la meilleure approche avec le représentant du compte) :

   * Activez les cookies propriétaires et tiers.

     Les cookies propriétaires et tiers sont requis pour les Flashbox et les créations dynamiques.

   * Activez uniquement les cookies tiers.

     Cette approche s’applique uniquement lorsque des mises en œuvre AdBox sont utilisées sans ciblage sur site (rare).

## Comportement des cookies propriétaires

Le cookie propriétaire est stocké dans clientdomain.com, où `clientdomain` correspond à votre domaine.

La bibliothèque JavaScript génère un `mboxSession ID` et le stocke dans le cookie Target. La première réponse mbox contient l’offre et le JavaScript permettant de stocker le `mboxPC ID` généré par l’application dans le cookie mbox.

>[!NOTE]
>
>Le cookie propriétaire AMCV_###@AdobeOrg est toujours défini avec l’identifiant visiteur Experience Cloud.

## Comportement des cookies tiers

Le cookie tiers est stocké dans clientcode.tt.omtrdc.net et le cookie propriétaire dans clientdomain.com, où `clientdomain` correspond à votre domaine.

La bibliothèque JavaScript génère un `mboxSession ID`. La première requête d’emplacement renvoie des en-têtes de réponse HTTP qui tentent de définir des cookies tiers nommés `mboxSession` et `mboxPC` et une requête de redirection est renvoyée avec un paramètre supplémentaire (`mboxXDomainCheck=true`).

Si le navigateur accepte les cookies tiers, la requête de redirection inclut ces cookies et l’offre est renvoyée.

Si le navigateur rejette les cookies tiers, la requête de redirection n’inclut pas ces cookies et le contenu par défaut s’affiche pour tous les emplacements de la page. Puisqu’aucun cookie n’est défini, le processus ci-dessus se reproduit pour chaque requête de page.

>[!NOTE]
>
>Le cookie demdex.net est défini si les cookies tiers ne sont pas bloqués.

## Comportement des cookies tiers et propriétaires

Le cookie tiers est stocké dans clientcode.tt.omtrdc.net et le cookie propriétaire dans clientdomain.com, où `clientdomain` correspond à votre domaine.

La bibliothèque JavaScript génère un `mboxSession ID`. La première requête d’emplacement renvoie des en-têtes de réponse HTTP qui tentent de définir des cookies tiers nommés `mboxSession` et `mboxPC` et une requête de redirection est renvoyée avec un paramètre supplémentaire (`mboxXDomainCheck=true`).

Si le navigateur accepte les cookies tiers, la requête de redirection inclut ces cookies et l’offre est renvoyée.

Certains navigateurs rejettent les cookies tiers. Dans ce cas, le cookie propriétaire continue de fonctionner. Target tente de définir le cookie tiers. S’il ne le peut pas, Target peut uniquement effectuer le suivi sur le domaine spécifique du client. Le suivi inter-domaines ne fonctionne pas si le cookie tiers est bloqué, à moins que `mboxSession` ne soit annexé au lien qui traverse les domaines. Dans ce cas, un autre cookie propriétaire est défini et synchronisé avec le cookie propriétaire du domaine précédent.

## Configuration des cookies

Le cookie s’accompagne de plusieurs paramètres par défaut. Vous pouvez modifier ces paramètres si nécessaire, à l’exception de la durée du cookie. Consultez le représentant de votre compte lorsque vous modifiez les paramètres du cookie.

| Paramètre | Informations |
|--- |--- |
| Nom du cookie | mbox. |
| Domaine du cookie | Niveaux secondaire et supérieur des domaines à partir desquels vous publiez le contenu. Comme il est diffusé à partir du domaine de votre entreprise, le cookie est un cookie propriétaire.<br />Exemple : `mycompany.com`. |
| Domaine du serveur | `clientcode.tt.omtrdc.net`, à l’aide du code client de votre compte. |
| Durée du cookie | Le cookie reste dans le navigateur du visiteur deux semaines à compter de la dernière connexion. Vous ne pouvez pas modifier la durée des cookies. |
| Stratégie P3P | Le cookie est publié avec une stratégie P3P, comme requis par le paramètre par défaut de la plupart des navigateurs. Une stratégie P3P indique à un navigateur qui diffuse le cookie et comment les informations sont utilisées. |

Le cookie conserve différentes valeurs afin de gérer la manière dont vos visiteurs expérimentent les campagnes :

| Valeur | Définition |
|--- |--- |
| session ID | ID unique pour une session utilisateur. Par défaut, cet identifiant dure 30 minutes. |
| pc ID | Identifiant semi-permanent pour le navigateur d’un visiteur. Dure 14 jours. |
| check | Valeur de test unique déterminant si un visiteur prend en charge les cookies. Définie chaque fois qu’un visiteur demande une page. |
| disable | Défini si le temps de chargement d’un visiteur dépasse le délai configuré dans le fichier de bibliothèque JavaScript. Par défaut, cette valeur dure une heure. |

## Impact sur Target pour les visiteurs Safari suite aux modifications de suivi du WebKit Apple

**Comment fonctionne le suivi Adobe Target ?**

| Cookies | Détails |
|--- |--- |
| Domaines propriétaires | Mise en oeuvre standard pour les clients Target. Les cookies « mbox » sont définis dans le domaine du client. |
| Suivi tiers | Le suivi tiers est important pour les cas d’utilisation de publicité et de ciblage dans Target et dans Adobe Audience Manager (AAM). Le suivi tiers nécessite des techniques de script intersite. Target utilise deux cookies, « mboxSession » et « mboxPC », définis dans le domaine `clientcode.tt.omtrd.net`. |

**Quelle est l’approche d’Apple ?**

Extrait d’Apple :

« Intelligent Tracking Prevention (Prévention intelligente du suivi) est une nouvelle fonctionnalité WebKit qui réduit le suivi des sites en limitant davantage les cookies et les autres données du site Web. »

« C’est ce qu’on appelle un suivi intersite. Le cookie utilisé par `example-tracker.com` s’appelle un cookie tiers. Lors de nos tests, nous avons identifié des sites Web populaires avec plus de 70 trackers, qui collectaient tous en silence des données sur les utilisateurs. »

| Approche | Détails |
|--- |--- |
| Intelligent Tracking Prevention (Prévention intelligente du suivi) | Pour en savoir plus, reportez-vous à la section [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) sur le site du navigateur Web Open Source, WebKit. |
| Cookies | Comment Safari traite les cookies :<ul><li>Les cookies tiers qui ne se trouvent pas dans un domaine auquel l’utilisateur accède directement ne sont jamais enregistrés. Ce comportement n’est pas neuf. Les cookies tiers ne sont déjà plus pris en charge dans Safari.</li><li>Les cookies tiers définis dans un domaine auquel l’utilisateur accède directement sont effacés après 24 heures.</li><li>Les cookies tiers sont effacés après 30 jours si le domaine propriétaire est classé comme suivant les utilisateurs de site en site. Ce problème peut concerner les grandes entreprises qui envoient les utilisateurs vers différents domaines en ligne. Apple n’a pas précisé clairement comment ces domaines sont classés, ni comment un domaine peut déterminer s’ils ont été classés comme suivant les utilisateurs sur plusieurs sites.</li></ul> |
| L’apprentissage automatique pour identifier les domaines intersites | À partir d’Apple :<br />Machine Learning Classifier : un modèle d’apprentissage automatique est utilisé pour classer les domaines régis par le contrôle privé afin de suivre l’utilisateur de site en site, en fonction des statistiques collectées. Sur les différentes statistiques recueillies, trois vecteurs se sont avérés avoir un signal fort pour la classification en fonction des pratiques de suivi actuelles : sous-ressource sous le nombre de domaines uniques, sous-trame sous le nombre de domaines uniques et nombre de domaines uniques redirigés. Toute la collecte et la classification des données se produisent sur le périphérique.<br />Cependant, si l’utilisateur interagit avec `example.com` en tant que domaine supérieur, souvent appelé domaine propriétaire, la prévention intelligente du suivi considère qu’il s’agit d’un signal que l’utilisateur est intéressé par le site web et ajuste temporairement son comportement comme illustré dans cette chronologie :<br />Si l’utilisateur a interagi avec `example.com` au cours des dernières 24 heures, ses cookies sont disponibles lorsque `example.com` est un tiers. Cette pratique autorise les scénarios de connexion &quot;Se connecter avec mon compte X sur Y&quot;.<ul><li>Les domaines visités en tant que domaine de niveau supérieur ne sont pas affectés. Des sites comme OKTA, par exemple.</li><li>Identifie les domaines qui sont des sous-domaines ou des sous-cadres de la page active sur plusieurs domaines uniques.</li></ul> |

**Comment l’Adobe est-il affecté ?**

| Fonctionnalités affectées | Détails |
|--- |--- |
| Prise en charge de l’exclusion | La fonction de suivi du WebKit d’Apple modifie la prise en charge de l’exclusion.<br />La fonction d’exclusion de Target utilise un cookie dans le domaine `clientcode.tt.omtrdc.net`. Pour plus d’informations, consultez la section [Confidentialité](/help/dev/before-implement/privacy/privacy.md)<br />Target prend en charge deux exclusions :<ul><li>une par client (le client gère le lien d’exclusion) ;</li><li>une via Adobe qui exclut l’utilisateur de toutes les fonctionnalités Target pour tous les clients.</li></ul>Ces deux méthodes utilisent le cookie tiers. |
| Activités Target | Les clients peuvent choisir la [durée de vie du profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) pour leurs comptes Target (jusqu’à 90 jours). Le problème est que si la durée de vie du profil du compte est supérieure à 30 jours et que le cookie propriétaire est purgé parce que le domaine du client a été marqué comme suivant les utilisateurs sur plusieurs sites, le comportement des visiteurs Safari est affecté dans les zones suivantes de Target :<br />**[!UICONTROL Target reports]**: Si un utilisateur Safari entre dans une activité, revient après 30 jours, puis effectue une conversion, cet utilisateur compte comme deux visiteurs et une conversion.<br />Ce comportement est le même pour les activités utilisant Analytics comme source de création de rapports (A4T).<br />**[!UICONTROL Profile & activity membership]** :<ul><li>Les données du profil sont effacées lorsque le cookie propriétaire expire.</li><li>L’appartenance à une activité est effacée lorsque le cookie propriétaire expire.</li><li> Target ne fonctionne pas dans Safari pour les comptes qui utilisent une implémentation de cookies tiers ou une implémentation de cookies tiers et de cookies propriétaires. Ce comportement n’est pas neuf. Safari n’a pas autorisé les cookies tiers pendant un certain temps.</li></ul><br />**[!UICONTROL Suggestions]**: s’il existe un risque que le domaine du client soit marqué comme un suivi des visiteurs d’une session à l’autre, il est plus prudent de définir la durée de vie du profil sur 30 jours ou moins dans Target. Cette limite garantit que les utilisateurs sont suivis de la même manière dans Safari et dans tous les autres navigateurs. |
