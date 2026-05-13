---
keywords: implémentation, implémentation, configuration, configuration, paramètre de page
description: Transformez les données en  [!DNL Target]  à l’aide des attributs de profil sur la page.
title: Comment puis-je importer des données dans à l [!DNL Target] aide des attributs de profil sur la page ?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
TQID: https://experienceleague.adobe.com/jXWNNl7HfrR03tEoMz7KApX3onc1Zc44IAuXy4QF2tU
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 311
ht-degree: 40%

---

# Attributs de profil sur la page

Les attributs de profil sur la page dans [!DNL Adobe Target] (également appelés « attributs de profil sur la mbox ») sont des paires nom/valeur transmises directement par le biais du code de page qui sont stockées dans le profil du visiteur pour une utilisation ultérieure.

Les attributs de profil internes à la page permettent d’enregistrer les données spécifiques à l’utilisateur dans le profil de Target pour un ciblage et une segmentation ultérieurs.

## Format

Les attributs de profil sur la page sont transmis à [!DNL Target] via un appel au serveur sous la forme d’une paire nom/valeur de chaîne avec le préfixe « profile ». .

Les noms et les valeurs d’attribut sont personnalisables (cependant, certains noms sont réservés à des utilisations spécifiques).

Voici quelques exemples d’attributs de profil sur la page :

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## Exemples de cas d’utilisation

* **Informations de connexion** : partagez des données autres que les informations d’identification personnelle avec [!DNL Target] en fonction de la connexion de l’utilisateur. Ces données peuvent être le statut d’abonnement, l’historique des commandes, etc.
* **Informations de boutique** : déterminez quelle est la boutique de prédilection de cet utilisateur.
* **Interactions précédentes** : effectuez le suivi des activités précédentes de l’utilisateur sur le site afin d’informer la personnalisation ultérieure.

## Avantages de la méthode

Les données sont envoyées à [!DNL Target] en temps réel et peuvent être utilisées lors de l’appel au serveur à partir duquel les données entrent.

## Avertissements

Nécessite des mises à jour du code de page (directement ou par l’intermédiaire d’un système de gestion des balises).

Les attributs et valeurs sont visibles dans les appels au serveur, ce qui signifie qu’un visiteur peut les voir. Si vous partagez des informations telles que les plages de crédit ou d’autres informations potentiellement privées, cette méthode peut ne pas être la meilleure.

## Exemples de code

targetPageParamsAll (ajoute les attributs à tous les appels de mbox sur la page) :

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams (ajoute les attributs à la mbox globale sur la page) :

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

Attributs dans le code mboxCreate :

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## Liens vers des informations pertinentes

[Attributs de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)

[Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html)
