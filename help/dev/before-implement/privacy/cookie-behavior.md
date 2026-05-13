---
keywords: Présentation et référence, webkit, cookies, propriétaires, tiers, propriétaires, tiers, tiers,
description: Découvrez le comportement  [!DNL Target]  cookies (cookie propriétaire, cookie tiers avec cookie propriétaire ou cookie tiers seul).
title: Où Puis-Je Trouver Des Informations Sur Les Cookies  [!DNL Target]  ?
feature: at.js
exl-id: d44e02ce-8920-4130-bcad-699ca77c0dad
TQID: https://experienceleague.adobe.com/Uc9Gb06t9DIkvBvLQJ9ZhopE8pyJovjyrQdsUmFD9-o
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1692
ht-degree: 49%

---

# [!DNL Target] des cookies

Le comportement des cookies varie selon qu’il s’agit d’un cookie propriétaire, d’un cookie tiers avec un cookie propriétaire ou d’un cookie tiers seul.

>[!NOTE]
>
>Pour plus d’informations sur les différents cookies utilisés par [!DNL Target], voir [[!DNL Adobe Target] cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-target.html?lang=fr){target=_blank} dans le *Guide des composants de l’interface centrale d’Experience Cloud*.
>
>Cette rubrique contient des informations sur `mboxSession` et `mboxPC`. Les bonnes pratiques d’implémentation recommandent de ne pas lier ni stocker d’informations sensibles avec les données de cookie : `mboxSession` ou `mboxPC`.

Voir aussi [Supprimer le [!DNL Target] cookie](cookie-deleting.md).

## Quand utiliser des cookies propriétaires ou tiers ?

La configuration de votre site détermine le type de cookies que vous allez utiliser. Il est utile de comprendre comment fonctionne [!DNL Target] lorsque vous essayez de comprendre les cookies propriétaires et tiers. Pour plus d’informations [!DNL Adobe] [!DNL Target] consultez la section [ Fonctionnement ](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) .

Il existe trois principaux cas d’utilisation des cookies :

1. Un domaine.

   Tous vos tests se déroulent dans un domaine de niveau supérieur (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, etc.).

   Approche : utilisez uniquement des cookies propriétaires (valeur par défaut).

1. Les utilisateurs passent d’un domaine à un autre et vous souhaitez effectuer un suivi et tester leur comportement sur ces domaines.

   Exemple : un utilisateur effectue des achats sur votre site mais procède à des vérifications dans des boutiques Yahoo. Trois approches (déterminez la meilleure approche avec le représentant de compte) :

   * Activez les cookies propriétaires et tiers.
   * Activez uniquement les tiers (rare, mais qui a l’avantage de garder le cookie de mbox hors de votre domaine).
   * Activez uniquement les cookies propriétaires et transmettez le paramètre `mboxSession` lors de la transition entre domaines.

     Le paramètre `mboxSession` doit être transmis à une page de destination et référencé à partir de la bibliothèque JavaScript (Adobe Experience Platform Web SDK ou at.js). Il ne peut pas s’agir d’une page de redirection intermédiaire.

1. Vous utilisez uniquement les adbox ou les Flashbox sur un site tiers.

   Deux approches (travaillez avec votre représentant de compte pour déterminer la meilleure approche) :

   * Activez les cookies propriétaires et tiers.

     Les cookies propriétaires et tiers sont requis pour les Flashbox et les créations dynamiques.

   * Activez uniquement les cookies tiers.

     Cette approche s’applique uniquement lorsque des mises en œuvre AdBox sont utilisées sans ciblage sur site (rare).

## Comportement du cookie propriétaire

Le cookie propriétaire est stocké dans clientdomain.com, où `clientdomain` est votre domaine.

La bibliothèque JavaScript génère un `mboxSession ID` et le stocke dans le cookie [!DNL Target]. La première réponse de mbox contient l’offre et le JavaScript pour stocker les `mboxPC ID` générés par l’application, dans le cookie de mbox.

>[!NOTE]
>
>Le cookie propriétaire AMCV_##@AdobeOrg est toujours défini avec l’identifiant visiteur Experience Cloud.

## Comportement des cookies tiers

Le cookie tiers est stocké dans clientcode.tt.omtrdc.net et le cookie propriétaire est stocké dans clientdomain.com, où `clientdomain` est votre domaine.

La bibliothèque JavaScript génère un `mboxSession ID`. La première requête d’emplacement renvoie des en-têtes de réponse HTTP qui tentent de définir des cookies tiers nommés `mboxSession` et `mboxPC` et une requête de redirection est renvoyée avec un paramètre supplémentaire (`mboxXDomainCheck=true`).

Si le navigateur accepte les cookies tiers, la requête de redirection inclut ces cookies et l’offre est renvoyée.

Si le navigateur rejette les cookies tiers, la requête de redirection n’inclut pas ces cookies et le contenu par défaut s’affiche pour tous les emplacements de la page. Puisqu’aucun cookie n’est défini, le processus ci-dessus se reproduit pour chaque requête de page.

>[!NOTE]
>
>Le cookie demdex.net est défini si les cookies tiers ne sont pas bloqués.

## Comportement des cookies tiers et propriétaires

Le cookie tiers est stocké dans clientcode.tt.omtrdc.net et le cookie propriétaire est stocké dans clientdomain.com, où `clientdomain` est votre domaine.

La bibliothèque JavaScript génère un `mboxSession ID`. La première requête d’emplacement renvoie des en-têtes de réponse HTTP qui tentent de définir des cookies tiers nommés `mboxSession` et `mboxPC` et une requête de redirection est renvoyée avec un paramètre supplémentaire (`mboxXDomainCheck=true`).

Si le navigateur accepte les cookies tiers, la requête de redirection inclut ces cookies et l’offre est renvoyée.

Certains navigateurs rejettent les cookies tiers. Dans ce cas, le cookie propriétaire continue de fonctionner. [!DNL Target] tente de définir le cookie tiers. S’il n’y parvient pas, [!DNL Target] ne peut qu’effectuer un suivi sur le domaine spécifique du client. Le suivi inter-domaines ne fonctionne pas si le cookie tiers est bloqué, sauf si le `mboxSession` est ajouté dans le lien qui traverse les domaines. Dans ce cas, un autre cookie propriétaire est défini et synchronisé avec le cookie propriétaire du domaine précédent.

## Paramétrage des cookies

Le cookie s’accompagne de plusieurs paramètres par défaut. Si nécessaire, vous pouvez modifier ces paramètres, à l’exception de la durée des cookies. Consultez le représentant de votre compte lorsque vous modifiez les paramètres du cookie.

| Paramètre | Informations |
|--- |--- |
| Nom du cookie | mbox. |
| Domaine du cookie | Niveaux secondaire et supérieur des domaines à partir desquels vous publiez le contenu. Étant donné qu’il est diffusé à partir du domaine de votre entreprise, le cookie est un cookie propriétaire.<br />Exemple : `mycompany.com`. |
| Domaine du serveur | `clientcode.tt.omtrdc.net`, à l’aide du code client de votre compte. |
| Durée du cookie | Le cookie reste sur le navigateur du visiteur deux semaines après la dernière connexion. Vous ne pouvez pas modifier la durée des cookies. |
| Stratégie P3P | Le cookie est publié avec une stratégie P3P, comme requis par le paramètre par défaut de la plupart des navigateurs. Une politique P3P indique à un navigateur qui diffuse le cookie et comment les informations sont utilisées. |

Le cookie conserve différentes valeurs pour gérer la manière dont vos visiteurs expérimentent les campagnes :

| Valeur | Définition |
|--- |--- |
| session ID | ID unique pour une session utilisateur. Par défaut, cet identifiant dure 30 minutes. |
| pc ID | Identifiant semi-permanent pour le navigateur d’un visiteur. Dure 14 jours. |
| check | Valeur de test unique déterminant si un visiteur prend en charge les cookies. Définie chaque fois qu’un visiteur demande une page. |
| disable | Défini si le temps de chargement d’un visiteur dépasse le délai configuré dans le fichier de bibliothèque JavaScript. Par défaut, cette valeur dure une heure. |

## Impact sur le [!DNL Target] des visiteurs Safari en raison des modifications du suivi WebKit Apple

**Comment fonctionne [!DNL Target] suivi ?**

| Cookies | Détails |
|--- |--- |
| Domaines propriétaires | Implémentation standard pour les clients [!DNL Target]. Les cookies « mbox » sont définis dans le domaine du client. |
| Suivi tiers | Le suivi tiers est important pour les cas d’utilisation de publicité et de ciblage dans [!DNL Target] et dans [!DNL Adobe Audience Manager] (AAM). Le suivi tiers nécessite des techniques de script de site à site. [!DNL Target] utilise deux cookies, « mboxSession » et « mboxPC » définis dans le domaine `clientcode.tt.omtrd.net`. |

**Quelle est l’approche d’Apple ?**

Extrait d’Apple :

« Intelligent Tracking Prevention (Prévention intelligente du suivi) est une nouvelle fonctionnalité WebKit qui réduit le suivi des sites en limitant davantage les cookies et les autres données du site Web. »

« C’est ce qu’on appelle un suivi intersite. Le cookie utilisé par `example-tracker.com` s’appelle un cookie tiers. Lors de nos tests, nous avons identifié des sites Web populaires avec plus de 70 trackers, qui collectaient tous en silence des données sur les utilisateurs. »

| Approche | Détails |
|--- |--- |
| Intelligent Tracking Prevention (Prévention intelligente du suivi) | Pour en savoir plus, reportez-vous à la section [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) sur le site du navigateur Web Open Source, WebKit. |
| Cookies | Comment Safari traite les cookies :<ul><li>Les cookies tiers qui ne se trouvent pas dans un domaine auquel l’utilisateur accède directement ne sont jamais enregistrés. Ce comportement n’est pas neuf. Les cookies tiers ne sont déjà plus pris en charge dans Safari.</li><li>Les cookies tiers définis dans un domaine auquel l’utilisateur accède directement sont effacés après 24 heures.</li><li>Les cookies tiers sont effacés après 30 jours si le domaine propriétaire est classé comme suivant les utilisateurs de site en site. Ce problème peut concerner les grandes entreprises qui envoient les utilisateurs vers différents domaines en ligne. Apple n’a pas indiqué clairement comment ces domaines sont classés exactement, ni comment un domaine peut déterminer s’ils ont été classés comme utilisateurs du suivi sur plusieurs sites.</li></ul> |
| L’apprentissage automatique pour identifier les domaines intersites | Dans Apple:<br />Machine Learning Classifier : un modèle de machine learning est utilisé pour classer les principaux domaines contrôlés de manière privée qui peuvent suivre l’utilisateur sur plusieurs sites, en fonction des statistiques collectées. Sur les différentes statistiques recueillies, trois vecteurs se sont avérés avoir un signal fort pour la classification en fonction des pratiques de suivi actuelles : sous-ressource sous le nombre de domaines uniques, sous-trame sous le nombre de domaines uniques et nombre de domaines uniques redirigés. Toutes les collectes et classifications de données se font sur l’appareil.<br />Cependant, si l’utilisateur interagit avec `example.com` en tant que domaine principal, souvent appelé domaine propriétaire, la prévention intelligente du suivi le considère comme un signal indiquant que l’utilisateur s’intéresse au site web et ajuste temporairement son comportement comme illustré dans cette chronologie :<br />Si l’utilisateur a interagi avec `example.com` au cours des dernières 24 heures, ses cookies sont disponibles lorsque `example.com` est un tiers. Cette pratique autorise les scénarios de connexion « Se connecter avec mon compte X sur Y ».<ul><li>Les domaines visités en tant que domaine de niveau supérieur ne sont pas affectés. Des sites comme OKTA, par exemple.</li><li>Identifie les domaines qui sont des sous-domaines ou des sous-cadres de la page active sur plusieurs domaines uniques.</li></ul> |

**Comment cela affecte-t-[!DNL Adobe] ?**

| Fonctionnalités affectées | Détails |
|--- |--- |
| Prise en charge de l’exclusion | La fonction de suivi du WebKit d’Apple modifie la prise en charge de l’exclusion.<br />La fonction d’exclusion de Target utilise un cookie dans le domaine `clientcode.tt.omtrdc.net`. Pour plus d’informations, voir [Confidentialité](privacy.md).<br />Target prend en charge deux désinscriptions :<ul><li>une par client (le client gère le lien d’exclusion) ;</li><li>Un via [!DNL Adobe] qui exclut l’utilisateur de toutes les fonctionnalités [!DNL Target] pour tous les clients.</li></ul>Ces deux méthodes utilisent le cookie tiers. |
| Activités Target | Les clients peuvent choisir leur [durée de vie du profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) pour leurs comptes [!DNL Target] (jusqu’à 90 jours). Le problème est que si la durée de vie du profil du compte est supérieure à 30 jours et que le cookie propriétaire est purgé, car le domaine du client a été marqué comme effectuant le suivi des utilisateurs sur plusieurs sites, le comportement des visiteurs Safari est affecté dans les zones suivantes des rapports Target:<br />**Target** : si un utilisateur Safari entre dans une activité, la revient après 30 jours, puis effectue une conversion, cet utilisateur compte comme deux visiteurs et une conversion.<br />Ce comportement est identique pour les activités utilisant Analytics comme source de création de rapports (A4T).<br />**Profil et appartenance à une activité** :<ul><li>Les données du profil sont effacées lorsque le cookie propriétaire expire.</li><li>L’appartenance à une activité est effacée lorsque le cookie propriétaire expire.</li><li> [!DNL Target] ne fonctionne pas dans Safari pour les comptes utilisant une implémentation de cookies tiers ou une implémentation de cookies propriétaires et tiers. Ce comportement n’est pas neuf. Safari n’autorise pas les cookies tiers depuis un certain temps.</li></ul><br />**Suggestions** : si vous craignez que le domaine client ne soit marqué comme un seul domaine de suivi des visiteurs sur plusieurs sessions, il est préférable de définir la durée de vie du profil sur 30 jours ou moins dans Target. Cette limite garantit que les utilisateurs sont suivis de la même manière dans Safari et tous les autres navigateurs. |
