---
keywords: implémentation, implémentation, configuration, configuration, paramètre de page
description: Récupérez des données dans  [!DNL Target]  à l’aide d’attributs de profil internes à la page.
title: Comment obtenir des données dans  [!DNL Target] à l’aide des attributs de profil internes à la page ?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 43%

---

# Attributs de profil sur la page

Les attributs de profil internes à la page dans [!DNL Adobe Target] (également appelés &quot;attributs de profil internes à la mbox&quot;) sont des paires nom/valeur transmises directement par le code de page qui sont stockées dans le profil du visiteur en vue d’une utilisation ultérieure.

Les attributs de profil internes à la page permettent d’enregistrer les données spécifiques à l’utilisateur dans le profil de Target pour un ciblage et une segmentation ultérieurs.

## Format

Les attributs de profil internes à la page sont transmis à [!DNL Target] via un appel au serveur sous la forme d’une paire nom/valeur de chaîne avec le préfixe &quot;profile&quot;. .

Les noms et les valeurs d’attribut sont personnalisables (cependant, certains noms sont réservés à des utilisations spécifiques).

Voici quelques exemples sur les attributs de profil internes à la page :

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## Exemples de cas d’utilisation

* **Informations de connexion** : partagez des données non personnelles avec des informations d’identification personnelles sur [!DNL Target] en fonction de la connexion de l’utilisateur. Il peut s’agir de l’état de l’adhésion, de l’historique des commandes, etc.
* **Informations de boutique** : déterminez quelle est la boutique de prédilection de cet utilisateur.
* **Interactions précédentes** : effectuez le suivi des activités précédentes de l’utilisateur sur le site afin d’informer la personnalisation ultérieure.

## Avantages de la méthode

Les données sont envoyées à [!DNL Target] en temps réel et peuvent être utilisées sur le même appel serveur que celui sur lequel les données entrent.

## Avertissements

Nécessite des mises à jour du code de page (directement ou par l’intermédiaire d’un système de gestion des balises).

Les attributs et valeurs sont visibles dans les appels au serveur, ce qui signifie qu’un visiteur peut les voir. Si vous partagez des informations telles que des plages de crédits ou d’autres informations potentiellement privées, cette méthode n’est peut-être pas la meilleure méthode.

## Exemples de code

targetPageParamsAll (ajoute les attributs à tous les appels de mbox sur la page) :

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams (ajoute les attributs à la mbox globale sur la page) :

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

Attributs dans le code mboxCreate :

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## Liens vers les informations pertinentes

[Attributs de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)

[Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html)
