---
keywords: email, adbox, adbox, adbox d’image de courrier électronique
description: Découvrez comment utiliser [!DNL Adobe Target] pour tester dynamiquement des images dans un email, et même modifier ces images à la volée lorsqu’une personne ouvre l’email.
title: Comment tester une adbox d’image de courrier électronique ?
feature: Implement Email
exl-id: 4512741a-567f-41bb-9721-3e1c4f5302e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 84%

---

# Test d’une adbox d’image de courrier électronique

Testez dynamiquement les images dans un courrier électronique et changez instantanément ces images lorsqu’une personne ouvre son courrier.

Des redirecteurs peuvent être utilisés dans les messages électroniques afin d’effectuer le suivi des clics et de contrôler dynamiquement la page d’entrée sur laquelle arrivent les utilisateurs.

Le test des images de courrier électronique s’effectue en utilisant des versions modifiées d’adbox. Étant donné que les clients de messagerie n’autorisent pas la définition de cookies, un identifiant unique doit être généré pour chaque message électronique. Ce numéro est ajouté à l’URL de l’adbox et à tout redirecteur utilisé dans le message électronique pour effectuer le suivi des clics à partir du message électronique.

>[!NOTE]
>
>Bien que [!DNL Target] peut techniquement fournir une optimisation d’image au moment de l’ouverture, chaque client de messagerie gère la mise en cache différemment, de sorte que la réussite varie. Quel que soit le fournisseur de services de messagerie utilisé, le client de messagerie utilisé par l’utilisateur final pour ouvrir le courrier électronique (application Gmail, Outlook, Hotmail, etc.) détermine si l’image est réellement récupérée lors de l’ouverture. Par exemple, Gmail met en cache la plupart des éléments, de sorte que l’image que l’utilisateur final voit dépend du moment auquel Gmail choisit d’appeler et de mettre en cache l’image.

**Exemple de code pour l’adbox d’une image de message électronique :**

```
<img src="https://{clientcode}.tt.omtrdc.net/m2/​{clientcode}/ubox/​image?
mbox={email_header}&
mboxDefault=​{http%3A%2F%2Fwww.domain.com%2Fheader.jpg}&
mboxXDomain=disabled&
mboxSession={123456}&
mboxPC={123456}" border=:"0"/>
```

Les valeurs ci-dessous vous sont spécifiques :

| Valeur | Description |
|--- |--- |
| clientcode | Code client de votre entreprise. Vous le trouverez dans le fichier at.js sous la forme `clientCode='yourclientcode'`. Toutes les lettres sont en minuscules et aucun caractère spécial n’est autorisé. |
| image | Type d’offre. Il s’agit toujours de « image » pour les annonces graphiques et de « page » pour les redirecteurs. |
| email_header | Nom de l’adbox. |
| `mboxDefault=http%3A%2F%2Fwww.domain.com%2Fheader.jpg` | Requis. Remplacez l’URL par le contenu par défaut approprié pour votre adbox. Ce contenu doit être en codage URL et il doit s’agir d’une référence absolue. |
| `mboxXDomain=disabled` | Indique à [!DNL Target] de ne pas essayer de définir un cookie. |
| `mboxSession=123456` et `mboxPC=123456` | Deux valeurs requises par [!DNL Target] pour fusionner le profil de cet utilisateur avec son profil existant sur votre site. 123456 est l’identifiant unique généré par courrier électronique. Insérez dynamiquement cette valeur dans chaque URL de redirecteur et d’adbox. Ce nombre doit être unique pour chaque courrier électronique envoyé à chaque personne. Si un courrier électronique hebdomadaire est envoyé à 1 000 personnes, 1 000 identifiants uniques doivent être générés.<br />L’identificateur unique par courrier électronique doit être affecté aux éléments mboxSession et mboxPC dans chaque adbox et URL de redirecteur. Le format recommandé pour cet identifiant est horodatage-NNNNN, où NNNNN est un nombre aléatoire à 5 chiffres, mais le format alphanumérique fonctionne. Certains services de publipostage et tous les langages de programmation peuvent générer cet identifiant unique. |
