---
title: Comment gérer les critères personnalisés
description: Étapes requises pour utiliser les API Adobe Target afin de gérer, créer, répertorier, modifier, obtenir et supprimer des critères Adobe Target Recommendations.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 51a67a49-a92d-4377-9a9f-27116e011ab1
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Gestion des critères personnalisés

Parfois, les algorithmes fournis par Recommendations ne sont pas en mesure de faire apparaître des éléments spécifiques que vous souhaitez promouvoir. Dans ce cas, les critères personnalisés vous permettent de fournir un ensemble spécifique d’éléments recommandés pour un élément ou une catégorie clé donnée.

Pour créer des critères personnalisés, définissez et importez le mappage souhaité entre l’élément clé ou la catégorie et les éléments recommandés. Ce processus est décrit dans la [documentation sur les critères personnalisés](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=fr). Comme indiqué dans cette documentation, vous pouvez créer, modifier et supprimer des critères personnalisés via l’interface utilisateur de Target. Cependant, Target fournit également un ensemble d’API de critères personnalisés qui permettent une gestion plus détaillée de vos critères personnalisés.

>[!WARNING]
>
>Pour les critères personnalisés, effectuez toutes les actions (création, modification, suppression) pour un critère personnalisé donné à l’aide des API, ou effectuez toutes les actions (création, modification, suppression) à l’aide de l’interface utilisateur. La gestion de vos critères personnalisés par le biais d’une combinaison de l’interface utilisateur et de l’API peut entraîner des informations conflictuelles ou des résultats inattendus. Par exemple, la création d’un critère personnalisé dans l’interface utilisateur, mais sa modification via l’API, ne reflétera pas vos mises à jour dans l’interface utilisateur, même si elles seront mises à jour dans le serveur principal, comme visible via l’API.

## Création de critères personnalisés

Pour créer des critères personnalisés à l’aide de l’ [ API Créer des critères personnalisés](https://developer.adobe.com/target/administer/recommendations-api/#operation/createCriteriaCustom), la syntaxe est la suivante :

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Les critères personnalisés créés à l’aide de l’API Créer des critères personnalisés, comme décrit dans cet exercice, s’affichent dans l’interface utilisateur, où ils sont conservés. Vous ne pourrez pas les modifier ni les supprimer de l’interface utilisateur. Vous pouvez les modifier ou les supprimer **via l’API**, mais dans les deux cas, elles continueront à apparaître dans l’interface utilisateur de Target. Pour conserver l’option de modification ou de suppression de l’interface utilisateur, créez les critères personnalisés à l’aide de l’interface utilisateur selon [la documentation](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=fr), plutôt que d’utiliser l’API Créer des critères personnalisés.

Suivez les étapes ci-après seulement lorsque vous avez lu l’avertissement ci-dessus et que vous êtes à l’aise avec la création de critères personnalisés qui ne peuvent pas être supprimés par la suite de l’interface utilisateur.

1. Vérifiez que `TENANT_ID` et `API_KEY` pour **[!UICONTROL Create custom criteria]** font référence aux variables d’environnement Postman établies précédemment. Utilisez l’image ci-dessous pour la comparaison.

   ![CreateCustomCrit1](assets/CreateCustomCriteria1.png)

1. Ajoutez votre fichier JSON **Body** en tant que **raw** qui définit l’emplacement de votre fichier CSV de critères personnalisés. Utilisez l’exemple fourni dans la documentation [Créer une API de critères personnalisés](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom) comme modèle, fournissant vos `environmentId` et d’autres valeurs si nécessaire. Pour cet exemple, nous utilisons LAST_PURCHASED comme clé.

   ![CreateCustomCritère2](assets/CreateCustomCriteria2.png)

1. Envoyez la requête et observez la réponse, qui contient les détails des critères personnalisés que vous venez de créer.

   ![CreateCustomCritère3](assets/CreateCustomCriteria3.png)

1. Pour vérifier que vos critères personnalisés ont été créés, accédez dans Adobe Target à **[!UICONTROL Recommendations > Criteria]** et recherchez vos critères par nom, ou utilisez l’ **[!UICONTROL List Custom Criteria API]** à l’étape suivante.

   ![CreateCustomCritère4](assets/CreateCustomCriteria4.png)

Dans ce cas, nous avons une erreur. Examinons l’erreur en examinant de plus près les critères personnalisés, à l’aide de **[!UICONTROL List Custom Criteria API]**.

## Liste des critères personnalisés

Pour récupérer une liste de tous vos critères personnalisés avec des détails pour chacun d’eux, utilisez l’ [ API Liste de critères personnalisés](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom). La syntaxe est la suivante :

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Vérifiez `TENANT_ID` et `API_KEY` comme auparavant, puis envoyez la demande. Dans la réponse, notez l’identifiant de critère personnalisé, ainsi que les détails concernant le message d’erreur mentionné précédemment.
   ![ListCustomCritère](assets/ListCustomCriteria.png)

Dans ce cas, l’erreur s’est produite car les informations du serveur sont incorrectes, ce qui signifie que Target ne peut pas accéder au fichier CSV contenant la définition de critères personnalisés. Modifions les critères personnalisés pour corriger ce problème.

## Modifier des critères personnalisés

Pour modifier les détails d’une définition de critère personnalisée, utilisez l’ [API Modifier des critères personnalisés](https://developer.adobe.com/target/administer/recommendations-api/#operation/updateCriteriaCustom). La syntaxe est la suivante :

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Vérifiez `TENANT_ID` et `API_KEY`, comme auparavant.
   ![EditCustomCrit1](assets/EditCustomCriteria1.png)

1. Indiquez l’identifiant du critère personnalisé (unique) que vous souhaitez modifier.
   ![EditCustomCritère2](assets/EditCustomCriteria2.png)

1. Dans le corps, fournissez le JSON mis à jour avec les informations correctes du serveur. (Pour cette étape, spécifiez l’accès FTP à un serveur auquel vous pouvez accéder.)
   ![EditCustomCritère3](assets/EditCustomCriteria3.png)

1. Envoyez la requête et notez la réponse.
   ![EditCustomCrit4](assets/EditCustomCriteria4.png)

Vérifiez le succès des critères personnalisés mis à jour, à l’aide de **[!UICONTROL Get Custom Criteria API]**.

## Obtenir des critères personnalisés

Pour afficher les détails des critères personnalisés pour un critère personnalisé spécifique, utilisez l’ [API Obtenir des critères personnalisés](https://developer.adobe.com/target/administer/recommendations-api/#operation/getCriteriaCustom). La syntaxe est la suivante :

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Indiquez l’identifiant du critère personnalisé dont vous souhaitez obtenir les détails. Envoyez la requête et passez en revue la réponse.
   ![GetCustomCritères.png](assets/GetCustomCriteria.png)
1. Vérifiez la réussite. (Dans notre cas, vérifiez qu’il n’y a pas d’autres erreurs FTP.)
   ![GetCustomCrit1.png](assets/GetCustomCriteria1.png)
1. (Facultatif) Vérifiez que la mise à jour s’affiche avec précision dans l’interface utilisateur.
   ![GetCustomCrit2.png](assets/GetCustomCriteria2.png)

## Suppression de critères personnalisés

À l’aide de l’ID de critère mentionné précédemment, supprimez vos critères personnalisés à l’aide de l’API [Supprimer les critères personnalisés](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteCriteriaCustom). La syntaxe est la suivante :

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Indiquez l’identifiant du critère personnalisé (unique) que vous souhaitez supprimer. Cliquez sur **[!UICONTROL Send]**.
   ![DeleteCustomCrit1](assets/DeleteCustomCriteria1.png)

1. Vérifiez que les critères ont été supprimés à l’aide de l’option Obtenir des critères personnalisés.
   ![DeleteCustomCrit2](assets/DeleteCustomCriteria2.png)
Dans ce cas, l’erreur 404 attendue indique que les critères supprimés sont introuvables.

>[!NOTE]
>
>Pour rappel, les critères ne seront pas supprimés de l’interface utilisateur de Target même s’ils ont été supprimés, car ils ont été créés à l’aide de l’API Créer des critères personnalisés .

Félicitations ! Vous pouvez désormais créer, répertorier, modifier, supprimer et obtenir des détails sur des critères personnalisés à l’aide de l’API Recommendations. Dans la section suivante, vous utiliserez l’API de diffusion Target pour récupérer les recommandations.

&lt;!— [Suite : &quot;Récupérer Recommendations avec l’API de diffusion côté serveur&quot; >](fetch-recs-server-side-delivery-api.md) —>
