---
keywords: apple, ITP, prévention intelligente du suivi, experience cloud id, ecid, itp
description: Découvrez  [!DNL Adobe Target]  et l’impact de l’initiative ITP (Intelligent Tracking Prevention) d’Apple qui vise à protéger la confidentialité des utilisateurs de Safari.
title: Comment gère [!DNL Target] t-il la prise en charge d’Apple ITP ?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 30%

---

# ITP (Intelligent Tracking Prevention) 2.x d’Apple

La prévention intelligente du suivi (ITP) est une initiative d’Apple visant à protéger la confidentialité des utilisateurs de Safari. La première version d’ITP, qui date de 2017, concernait l’utilisation des cookies tiers. En fait, Apple bloquait entièrement les cookies tiers, ce qui gênait les entreprises technologiques et marketing, car ceux-ci servent généralement au suivi des visiteurs et à la collecte des données des visiteurs. Maintenant, Apple souhaite limiter l’utilisation des cookies propriétaires dans Safari.

Ces versions d’ITP comprennent les restrictions suivantes :

| Version | Détails |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Limite à sept jours le délai d’expiration des cookies côté client qui sont placés sur le navigateur à l’aide de l’API `document.cookie`.<br />Publié le 21 février 2019. |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Réduit de façon drastique la limite de délai d’expiration de sept jours à un jour.<br />Publié le 24 avril 2019. |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | Élimination de plusieurs solutions de contournement, telles que l’utilisation de localStorage ou de l’`Document.referrer property` JavaScript.<br />Publié Le 23 Septembre 2019.<br />Fonctionnalité de défense de masquage CNAME pour ITP publiée dans Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 et iPadOS 14. Tous les cookies créés par une réponse HTTP tierce voilée par un CNAME expireront dans sept jours.<br />Annoncé le 12 novembre 2020. |

## Quel est l’impact pour moi en tant que client [!DNL Target] ?

Target fournit des bibliothèques JavaScript que vous pouvez déployer sur vos pages afin que [!DNL Target] puissiez offrir une personnalisation en temps réel à vos visiteurs. Il existe trois bibliothèques [!DNL Target] JavaScript at.js 1.*x*, at.js 2.*x*, les [!DNL Adobe Experience Cloud Web SDK] qui placent des cookies [!DNL Target] côté client sur les navigateurs de vos visiteurs via l’API `document.cookie`. Par conséquent, les cookies [!DNL Target] sont affectés par les versions ITP 2.1, 2.2 et 2.3 d’Apple et expireront après sept jours (avec ITP 2.1) et après un jour (avec ITP 2.2 et ITP 2.3).

Apple ITP 2.x a un impact sur le [!DNL Target] dans les domaines suivants :

| Impact | Détails |
| --- | --- |
| Augmentation éventuelle du nombre de visiteurs uniques | En raison de la définition de la fenêtre d’expiration sur sept jours (avec ITP 2.1) et un jour (avec ITP 2.2 et ITP 2.3), vous pouvez constater une augmentation du nombre de visiteurs uniques provenant des navigateurs Safari. Si vos visiteurs revisitent votre domaine après sept jours (ITP 2.1) ou un jour (ITP 2.2 et ITP 2.3), [!DNL Target] est forcé de placer un nouveau cookie [!DNL Target] sur votre domaine à la place du cookie expiré. Le nouveau cookie [!DNL Target] convertit un utilisateur en nouveau visiteur unique, même s’il s’agit d’un même utilisateur. |
| Diminution des périodes de recherche pour les activités [!DNL Target] | La période de recherche des profils de visiteur des activités [!DNL Target]peut être réduite pour la prise de décision. Les cookies [!DNL Target] sont utilisés pour identifier un visiteur et stocker les attributs de profil utilisateur en vue de la personnalisation. Étant donné que les cookies [!DNL Target] peuvent expirer sur Safari après sept jours (ITP 2.1) ou un jour (ITP 2.2 et 2.3), les données de profil utilisateur liées au cookie [!DNL Target] purgé ne peuvent pas être utilisées pour la prise de décision. |
| Scripts de profil basés sur 3rdPartyID | En raison de la définition de la fenêtre d’expiration sur sept jours (avec ITP 2.1) et un jour (avec ITP 2.2 et ITP 2.3), les [scripts de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html) basés sur le cookie 3rdPartyID cesseront de fonctionner à l’expiration. |
| URL d’AQ/d’aperçu des appareils iOS | En raison de la définition de la fenêtre d’expiration sur sept jours (avec ITP 2.1) et un jour (avec ITP 2.2 et ITP 2.3), les [URL d’AQ/de prévisualisation](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) cesseront de fonctionner à l’expiration, car les URL sont basées sur le cookie 3rdPartyID. |

## Mon implémentation actuelle de [!DNL Target] est-elle impactée ?

Si vous utilisez la bibliothèque Experience Cloud ID (ECID) en plus de la bibliothèque [!DNL Target] JavaScript, votre implémentation sera affectée des manières répertoriées dans cet article : [Impact d’ITP 2.1 de Safari sur les clients Adobe Experience Cloud et Experience Platform](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
