---
keywords: implémentation, implémentation, configuration, configuration, paramètres de page
description: Transférez des données dans à l [!DNL Target] aide des paramètres de page.
title: Comment puis-je importer des données dans à l [!DNL Target] aide des paramètres de page ?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
TQID: https://experienceleague.adobe.com/CYhZOFnli-DmREOOZGE2aGNn3x7BJ7uwGA2vfwUSnOk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: f6df325aff4a2eb9321b86778d102737493e63bb
workflow-type: tm+mt
source-wordcount: 397
ht-degree: 31%

---

# Paramètres de page

Les paramètres de page (également appelés « paramètres de mbox ») sont des paires nom/valeur transmises directement par le biais du code de page, qui ne sont pas stockées dans le profil du visiteur pour une utilisation ultérieure.

Les paramètres de page sont utiles pour envoyer des données de page à des [!DNL Adobe Target] qui n’ont pas besoin d’être stockées avec le profil du visiteur pour une utilisation ultérieure de ciblage. Ces valeurs sont utilisées pour décrire la page ou l’action effectuée par l’utilisateur sur cette page spécifique.

## Format

Les paramètres de page sont transmis à [!DNL Target] via un appel au serveur sous la forme d’une paire nom/valeur de chaîne. Les noms et les valeurs de paramètre sont personnalisables (cependant, certains noms sont réservés à des utilisations spécifiques).

Voici quelques exemples de paramètres de page

* `page=productPage`

* `categoryId=homeLoans`

## Exemples de cas d’utilisation

* **Pages produit** : envoyez des informations sur le produit spécifique consulté (cette méthode décrit le fonctionnement de Recommendations).
* **Détails de la commande** : envoyez l’ID de commande, orderTotal, etc. pour la collecte des commandes.
* **Affinité catégorielle** : envoyez des informations consultées par catégorie aux [!DNL Target] pour acquérir des connaissances sur l’affinité de l’utilisateur ou de l’utilisatrice avec des catégories de site spécifiques
* **Données tierces** : envoyez des informations provenant de sources de données tierces, telles que les fournisseurs de ciblage météo, les fournisseurs de données de compte (par exemple, DemandBase), les fournisseurs de données démographiques (par exemple, Experian), etc.

## Avantages de la méthode

Les données sont envoyées à [!DNL Target] en temps réel et peuvent être utilisées sur le même serveur pour appeler les données dans lesquelles elles arrivent.

## Avertissements

* Nécessite une mise à jour du code de page (directement ou par l’intermédiaire d’un système de gestion des balises).
* Si les données doivent être utilisées pour le ciblage lors d’un appel page/serveur suivant, elles doivent être traduites en script de profil.
* Les chaînes de requête ne peuvent contenir que des caractères conformément à la norme [Internet Engineering Task Force (IETF)](https://www.ietf.org/rfc/rfc3986.txt) .

  En plus des caractères mentionnés sur le site de l’IETF, [!DNL Target] autorise les caractères suivants dans les chaînes de requête :

  `< > # % " { } | \ ^ [ ] `

  Le reste doit être encodé en URL. La norme spécifie le format suivant ( [&#128279;](https://www.ietf.org/rfc/rfc1738.txt) ), comme illustré ci-dessous :

  ![image alternative](assets/ietf1.png)

  Ou la liste complète, pour plus de simplicité :

  ![image alternative](assets/ietf2.png)

## Exemples de code

targetPageParamsAll (ajoute les paramètres à tous les appels de mbox sur la page) :

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams (ajoute les paramètres à la mbox globale sur la page) :

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## Liens vers des informations pertinentes

Recommandations : [implémentation selon le type de page](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=fr)

Confirmation de commande : [suivi des conversions](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Affinité catégorielle : [affinité catégorielle](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=fr)
