---
keywords: implémentation, implémentation, configuration, configuration, paramètres de page
description: Obtenir des données dans [!DNL Target] à l’aide des paramètres de page.
title: Comment obtenir des données dans [!DNL Target] Utilisation des paramètres de page ?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 38%

---

# Paramètres de page

Les paramètres de page (également appelés &quot;paramètres de mbox&quot;) sont des paires nom/valeur transmises directement par le biais du code de page qui ne sont pas stockées dans le profil du visiteur en vue d’une utilisation ultérieure.

Les paramètres de page sont utiles pour envoyer des données de page à [!DNL Adobe Target] qui n’a pas besoin d’être stocké avec le profil du visiteur pour une utilisation ultérieure dans le cadre du ciblage. Ces valeurs sont utilisées pour décrire la page ou l’action effectuée par l’utilisateur sur cette page spécifique.

## Format

Les paramètres de page sont transmis [!DNL Target] via un appel au serveur en tant que paire nom/valeur de chaîne. Les noms et les valeurs de paramètre sont personnalisables (cependant, certains noms sont réservés à des utilisations spécifiques).

Voici quelques exemples de paramètres de page

* `page=productPage`

* `categoryId=homeLoans`

## Exemples de cas d’utilisation

* **Pages de produit**: envoyez des informations sur le produit spécifique consulté (cette méthode est la manière dont Recommendations fonctionne).
* **Détails de la commande**: envoyez l’identifiant de commande, orderTotal, etc. pour la collecte de commandes.
* **Affinité catégorielle**[!DNL Target] : envoyez les informations de consultation de catégorie à afin de développer la connaissance de l’affinité de l’utilisateur pour des catégories de site particulières.
* **Données tierces** : envoyez des informations provenant de sources de données tierces, telles que les fournisseurs de ciblage météo, les fournisseurs de données de compte (par exemple, DemandBase), les fournisseurs de données démographiques (par exemple, Experian), etc.

## Avantages de la méthode

Les données sont envoyées à [!DNL Target] en temps réel et peut être utilisé sur le même appel serveur que les données sur lesquelles il intervient.

## Avertissements

* Nécessite une mise à jour du code de page (directement ou par l’intermédiaire d’un système de gestion des balises).
* Si les données doivent être utilisées pour le ciblage lors d’un appel de page/serveur ultérieur, elles doivent être traduites en script de profil.
* Les caractères contenus dans les chaînes de requête doivent obligatoirement respecter les [standards de l’Internet Engineering Task Force (IETF)](https://www.ietf.org/rfc/rfc3986.txt).

  Outre les caractères mentionnés sur le site de l&#39;IETF, [!DNL Target] autorise les caractères suivants dans les chaînes de requête :

  ```< > # % " { } | \ ^ [ ] ` ``` {line-nombres=&quot;true&quot;}

  Le reste doit être encodé en URL. La norme spécifie le format suivant ( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt) ), comme illustré ci-dessous :

  ![image alternative](assets/ietf1.png)

  Ou la liste complète, pour plus de simplicité :

  ![image alternative](assets/ietf2.png)

## Exemples de code

targetPageParamsAll (ajoute les paramètres à tous les appels de mbox sur la page) :

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams (ajoute les paramètres à la mbox globale sur la page) :

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## Liens vers les informations pertinentes

Recommandations : [implémentation selon le type de page](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html)

Confirmation de commande : [suivi des conversions](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Affinité catégorielle : [affinité catégorielle](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html)
