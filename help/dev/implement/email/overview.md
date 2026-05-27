---
keywords: Implémentation, at.js non javascript, adbox, redirecteur, mbox
description: Découvrez comment mettre en œuvre  [!DNL Adobe Target]  scénarios autres que JavaScript, tels que l’utilisation d’une AdBox ou d’un redirecteur.
title: Comment mettre en œuvre  [!DNL Target]  pour les e-mails ?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
TQID: https://experienceleague.adobe.com/NeITIa97pW-yiB6EB-ajqRuBgp9mx-uzdwlREdgotj8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e9001ce2-5245-4a8e-8601-dd958009072f
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 441
ht-degree: 62%

---

# E-mail : implémentation de [!DNL Target]

Informations sur l’implémentation de [!DNL Target] dans des scénarios autres que JavaScript, comme l’utilisation d’une AdBox ou d’un redirecteur.

Vous pouvez effectuer le suivi des visites sur vos annonces ainsi que de tout autre contenu hors site. Vous pouvez également identifier le même utilisateur, que ce soit sur votre site ou en dehors de celui-ci, et lui garantir une expérience web cohérente. En utilisant une seule URL, l’AdBox permet de tester sans JavaScript ni at.js.

Un AdBox est utile pour les sites qui n’ont pas at.js, comme les affiliés. Si votre activité nécessite du contenu publicitaire dynamique (vous devez, par exemple, afficher un produit dans l’annonce qui a été abandonné dans le panier), vous ne pouvez pas utiliser une AdBox.

Les annonces AdBox et le redirecteur peuvent être utilisés avec n’importe quel type d’activité. Le tableau suivant compare le redirecteur et adbox, et indique dans quels cas les utiliser :

| | Objectif | Conditions d’utilisation | Structure de l’URL | Type d’offre | Contenu de l’offre |
|--- |--- |--- |--- |--- |--- |
| AdBox | Renvoie différentes images à l’annonce | Permet de modifier le contenu d’une annonce | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | Offre de redirection | URL d’une image |
| Redirecteur | Redirige un visiteur vers une autre page Web | Permet de modifier la page d’entrée d’une annonce | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | Offre de redirection | URL d’une page |

## Bonnes pratiques en matière de sécurité

Notez qu’avec Redirector, vous pouvez être exposé à un risque de vulnérabilité de redirection ouverte. Pour éviter l’utilisation non autorisée de liens de redirection par des tiers, nous vous recommandons d’utiliser des « hôtes autorisés » pour placer sur la liste autorisée les domaines d’URL de redirection par défaut. [!DNL Target] utilise des hôtes pour placer sur la liste autorisée les domaines vers lesquels vous souhaitez autoriser les redirections. Pour plus d’informations, consultez [Création de Listes autorisées qui spécifient les hôtes autorisés à envoyer des appels de mbox à [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) dans *Hôtes*.

## Contraintes

* Absence de délai d’expiration côté client, contrairement aux mbox standard. Si la [!DNL Target] est complètement arrêtée, les visiteurs et visiteuses de la publicité ne verront pas de contenu, pas même par défaut.
* Les cookies tiers sont utilisés pour effectuer le suivi des visites. Si les PCId sont différents, le profil tiers du visiteur est par défaut fusionné avec tout profil propriétaire existant.
* Pour utiliser des cookies propriétaires sur l’AdBox proprement dite, vous devez transmettre la session mBox dans l’URL. Pour cela, contactez le représentant du compte.
* Pour utiliser des cookies propriétaires afin d’effectuer le suivi des clics publicitaires, vous devez transmettre la session mbox dans l’URL. Pour cela, contactez le représentant du compte.
* Pour utiliser plusieurs AdBox sur la même page, vous devez transmettre la session mbox dans l’URL. Pour cela, contactez le représentant du compte. Une AdBox et un lien Redirecteur peuvent coexister sur la même page (car le redirecteur se situe, en réalité, sur une deuxième page).
