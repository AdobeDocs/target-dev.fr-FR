---
keywords: Mise en oeuvre, at.js sans JavaScript, adbox, redirecteur, mbox
description: Découvrez comment implémenter  [!DNL Adobe Target] dans des scénarios non JavaScript, tels que l’utilisation d’une adbox ou d’un redirecteur.
title: Comment mettre en oeuvre  [!DNL Target] pour la messagerie ?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 63%

---

# Email : implémentation [!DNL Target]

Informations sur l’implémentation de [!DNL Target] dans des scénarios autres que JavaScript, comme l’utilisation d’une adbox ou d’un redirecteur.

Vous pouvez effectuer le suivi des visites sur vos annonces ainsi que de tout autre contenu hors site. Vous pouvez également identifier le même utilisateur, que ce soit sur votre site ou en dehors de celui-ci, et lui garantir une expérience web cohérente. Avec une seule URL, l’AdBox permet de réaliser des tests sans JavaScript ni at.js.

Une AdBox est utile pour les sites qui ne disposent pas d’at.js, tels que les affiliés. Si votre activité nécessite du contenu publicitaire dynamique (vous devez, par exemple, afficher un produit dans l’annonce qui a été abandonné dans le panier), vous ne pouvez pas utiliser une AdBox.

Les annonces AdBox et le redirecteur peuvent être utilisés avec n’importe quel type d’activité. Le tableau suivant compare le redirecteur et adbox, et indique dans quels cas les utiliser :

| | Objectif | Conditions d’utilisation | Structure de l’URL | Type d’offre | Contenu de l’offre |
|--- |--- |--- |--- |--- |--- |
| AdBox | Renvoie différentes images à l’annonce | Permet de modifier le contenu d’une annonce | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | Offre de redirection | URL d’une image |
| Redirecteur | Redirige un visiteur vers une autre page Web | Permet de modifier la page d’entrée d’une annonce | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | Offre de redirection | URL d’une page |

## Bonnes pratiques relatives à la sécurité

Notez qu’avec Redirecteur, vous pouvez être exposé à un risque de vulnérabilité de redirection ouverte. Pour éviter l’utilisation non autorisée de liens de redirection par des tiers, nous vous recommandons d’utiliser des &quot;hôtes autorisés&quot; pour placer sur la liste autorisée les domaines d’URL de redirection par défaut. [!DNL Target] utilise des hôtes pour placer sur la liste autorisée des domaines auxquels vous souhaitez autoriser des redirections. Pour plus d’informations, voir [Création de Listes autorisées qui spécifient les hôtes autorisés à envoyer des appels de mbox à [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=fr#allowlist) dans *Hôtes*.

## Contraintes

* Absence de délai d’expiration côté client, contrairement aux mbox standard. Si [!DNL Target] est complètement hors service, le contenu n’est pas visible pour les visiteurs de l’annonce, pas même le contenu par défaut.
* Les cookies tiers sont utilisés pour effectuer le suivi des visites. Si les PCId sont différents, le profil tiers du visiteur est par défaut fusionné avec tout profil propriétaire existant.
* Pour utiliser des cookies propriétaires sur l’AdBox proprement dite, vous devez transmettre la session mBox dans l’URL. Pour cela, contactez le représentant du compte.
* Pour utiliser des cookies propriétaires afin d’effectuer le suivi des clics publicitaires, vous devez transmettre la session mbox dans l’URL. Pour cela, contactez le représentant du compte.
* Pour utiliser plusieurs AdBox sur la même page, vous devez transmettre la session mbox dans l’URL. Pour cela, contactez le représentant du compte. Une AdBox et un lien Redirecteur peuvent coexister sur la même page (car le redirecteur se situe, en réalité, sur une deuxième page).
