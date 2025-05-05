---
title: Comment récupérer des recommandations avec l’API de diffusion
description: Cet article guide les développeurs à travers les étapes requises pour récupérer le contenu des recommandations à l’aide de l’API de diffusion Adobe Target.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 9b391f42-2922-48e0-ad7e-10edd6125be6
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 1%

---

# Récupération des recommandations avec l’API de diffusion

Les API Adobe Target et Adobe Target Recommendations peuvent être utilisées pour fournir des réponses aux pages web, mais peuvent également être utilisées dans des expériences non basées sur HTML, notamment les applications, les écrans, les consoles, les e-mails, les kiosques et d’autres appareils d’affichage. En d’autres termes, lorsque les bibliothèques Target et JavaScript ne peuvent pas être utilisées, l’[API de diffusion Target](/help/dev/implement/delivery-api/overview.md) permet toujours d’accéder à l’ensemble des fonctionnalités de Target pour offrir des expériences personnalisées.

>[!NOTE]
>
>Lorsque vous demandez du contenu contenant des recommandations réelles (produits ou éléments recommandés), utilisez l’API de diffusion Target.

Pour récupérer des recommandations, envoyez un appel POST de l’API de diffusion Adobe Target avec les informations contextuelles appropriées, qui peuvent inclure un identifiant utilisateur (à utiliser avec des recommandations spécifiques au profil, telles que les éléments récemment consultés de l’utilisateur), le nom de mbox approprié, les paramètres de mbox, les paramètres de profil ou d’autres attributs. La réponse inclut le paramètre entity.ids recommandé (et peut inclure d’autres données d’entité) au format JSON ou HTML, qui peut ensuite être affiché dans l’appareil.

L’[API de diffusion](/help/dev/implement/delivery-api/overview.md) pour Adobe Target expose toutes les fonctionnalités existantes fournies par une requête Target standard.

L’API de diffusion :

* Permet de récupérer des expériences ou des offres pour un emplacement et une audience de manière RESTful.
* Ne nécessite aucune authentification.
* Uniquement les publications.
* Ne traite pas les cookies ni les appels de redirection.
* Ne nécessite pas ou ne reconnaît pas de « rôles utilisateur ». Il récupère simplement du contenu ou signale des événements aux serveurs Edge de Target.

Pour utiliser l’API de diffusion afin de diffuser des expériences Target (y compris des recommandations), procédez comme suit :

1. Créez une activité Target (A/B, XT, AP ou Recommendations) à l’aide du compositeur d’après les formulaires (et non du compositeur d’expérience visuelle).
1. Utilisez l’API de diffusion pour obtenir une réponse aux requêtes générées par l’activité Target que vous venez de créer.

&lt;!— Q : Pourquoi les DEUX étapes sont-elles nécessaires pour cela ? Si vous avez défini une recommandation basée sur un formulaire pour une mbox, à quoi sert-il de faire en sorte que l’API de diffusion intervienne également pour récupérer les résultats ? Pourquoi ne pouvez-vous pas simplement laisser l’enregistrement basé sur les formulaires fournir les résultats dans l’appareil de destination...?? R : Voir le cas d’utilisation ci-dessous... c’est lorsque vous souhaitez « intercepter » les résultats en attente afin d’effectuer d’autres opérations avant d’afficher les résultats. Par exemple, des comparaisons en temps réel avec les niveaux d&#39;inventaire. —>

## Créer une recommandation à l’aide du compositeur d’expérience d’après les formulaires

Pour créer des recommandations à utiliser avec l’API de diffusion, utilisez le [compositeur basé sur les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr).

1. Tout d’abord, créez et enregistrez une conception basée sur JSON à utiliser dans votre recommandation. Pour obtenir un exemple JSON, ainsi que des informations générales sur la manière dont les réponses JSON peuvent être renvoyées lors de la configuration d’une activité basée sur des formulaires, consultez la documentation sur la [Création de conceptions de recommandations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=fr). Dans cet exemple, la conception est nommée *JSON simple.*
   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

1. Dans Target, accédez à **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Recommendations]**, puis sélectionnez **[!UICONTROL Form]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

1. Sélectionnez une propriété, puis cliquez sur **[!UICONTROL Next]**.
1. Définissez l’emplacement où vous souhaitez que les utilisateurs reçoivent la réponse de la recommandation. L’exemple ci-dessous utilise un emplacement nommé *api_charter*. Sélectionnez votre conception basée sur JSON, créée précédemment, nommée *JSON simple.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
1. Enregistrez et activez la recommandation. Cela produira des résultats. [Une fois les résultats prêts](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=fr) vous pouvez utiliser l’API de diffusion pour les récupérer.

## Utilisation de l’API de diffusion

La syntaxe de l’[API de diffusion](/help/dev/implement/delivery-api/overview.md) est la suivante :

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Notez que le code client est obligatoire. Pour rappel, vous trouverez peut-être votre code client dans Adobe Target en accédant à **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**. Notez la valeur **Code client** dans la section **Jeton API Recommendations**.
   ![code-client.png](assets/client-code.png)
1. Une fois que vous disposez de votre code client, créez votre appel API de diffusion. L’exemple ci-dessous commence par la **[!UICONTROL Web Batched Mboxes Delivery API Call]** fournie dans la [collection Postman de l’API de diffusion](../../implement/delivery-api/overview.md/#section/Getting-Started/Postman-Collection), qui permet d’apporter des modifications pertinentes. Par exemple :
   * les objets **browser** et **address** ont été supprimés de la **Body**, car ils ne sont pas nécessaires pour les cas d’utilisation non HTML
   * *api_charter* est répertorié comme nom d’emplacement dans cet exemple
   * entity.id est spécifié, car cette recommandation est basée sur la similarité de contenu, qui nécessite la transmission d’une clé d’élément active à Target.

     ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
N’oubliez pas de configurer correctement vos paramètres de requête. Par exemple, veillez à spécifier `{{CLIENT_CODE}}` si nécessaire. &lt;!— Q : Dans la syntaxe d’appel mise à jour, entity.id est répertorié en tant que profileParameter au lieu d’un mboxParameter comme dans les versions plus anciennes. —> &lt;!— Q : Ancienne image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Ancien texte d’accompagnement : « Notez que cette recommandation est basée sur des produits Content Similary basés sur entity.id envoyés via mboxParameters. » —>
     ![code-client3](assets/client-code3.png)
1. Envoyez la demande. Cette opération s’exécute à l’emplacement *api_charter*, où s’exécute une recommandation active, définie avec votre conception JSON et qui génère une liste des entités recommandées.
1. Recevez une réponse basée sur la conception JSON.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
La réponse inclut l’identifiant de clé, ainsi que les identifiants d’entité des entités recommandées.

Ainsi, l’utilisation de l’API de diffusion avec Recommendations permet d’effectuer des étapes supplémentaires avant d’afficher les recommandations au visiteur sur un appareil non HTML. Par exemple, vous pouvez utiliser la réponse de l’API de diffusion pour effectuer une recherche en temps réel supplémentaire des détails des attributs de l’entité (inventaire, prix, évaluation, etc.) à partir d’un autre système (une plateforme CMS, PIM ou eCommerce, par exemple), avant d’afficher les résultats finaux.

En utilisant l’approche décrite dans ce guide, vous pouvez obtenir n’importe quelle application pour exploiter la réponse de Target et fournir des recommandations personnalisées.

## Exemple de mises en œuvre

Les ressources suivantes fournissent des exemples de diverses implémentations non axées sur HTML. Gardez à l’esprit que chaque mise en œuvre sera unique, en raison du système et des appareils impliqués.

| Ressource | Détails |
| --- | --- |
| [Configuration de l’extension Target dans Experience Platform Launch et implémentation des API Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/) | Suivez les étapes de configuration de l’extension Target dans Experience Platform Launch, d’ajout de l’extension Target à votre application et d’implémentation des API Target pour demander des activités, prérécupérer des offres et passer en mode Aperçu visuel. |
| [Client Adobe Target Node](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | SDK open source Node.js de Target version 1.0 |
| [Présentation côté serveur](../../implement/server-side/server-side-overview.md) | Informations sur les API de diffusion côté serveur d’Adobe Target, les API de diffusion par lots côté serveur, le SDK Node.js et les API Recommendations d’Adobe Target. |
| [Recommandations de contenu Adobe Campaign dans un e-mail](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog qui décrit comment tirer parti des recommandations de contenu dans les e-mails via Adobe Target et Adobe I/O Runtime dans Adobe Campaign. |

## Gestion de la configuration de Recommendations à l’aide des API

La plupart du temps, les recommandations sont configurées dans l’interface utilisateur d’Adobe Target, puis utilisées ou accessibles via les API Target, pour des raisons telles que celles mentionnées dans les sections ci-dessus. Cette coordination interface utilisateur-API est courante. Cependant, il arrive que les utilisateurs souhaitent effectuer toutes les actions par le biais d’API, à la fois la configuration et l’utilisation des résultats. Bien que cela soit beaucoup moins courant, les utilisateurs peuvent absolument configurer, exécuter *et exploiter* résultats des recommandations entièrement à l’aide des API.

Dans une [section précédente](manage-catalog.md) nous avons appris à gérer les entités Adobe Target Recommendations et à les diffuser côté serveur. De même, le [Adobe Developer Console](https://developer.adobe.com/console/home) vous permet de gérer les critères, les promotions, les collections et les modèles de conception sans avoir à vous connecter à Adobe Target. Vous trouverez une liste complète de toutes les API Recommendations [ici](https://developer.adobe.com/target/administer/recommendations-api/), mais voici un résumé à titre de référence.

| Ressource | Détails |
| --- | --- |
| [Collections](https://developer.adobe.com/target/administer/recommendations-api/#tag/Collections) | Répertorier, créer, obtenir, modifier et supprimer des collections |
| [Critères](https://developer.adobe.com/target/administer/recommendations-api/#tag/Criteria) | Répertoriez et obtenez des critères. |
| [Conceptions](https://developer.adobe.com/target/administer/recommendations-api/#tag/Designs) | Répertorier, créer, obtenir, modifier, supprimer et valider des conceptions. |
| [ Entités ](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities) | Enregistrer, supprimer et obtenir des entités. |
| [Promotions ](https://developer.adobe.com/target/administer/recommendations-api/#tag/Promotions) | Répertorier, créer, obtenir, modifier et supprimer des promotions. |
| [Critères de catégorie](https://developer.adobe.com/target/administer/recommendations-api/#tag/Category-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères de catégorie. |
| [Critères personnalisés](https://developer.adobe.com/target/administer/recommendations-api/#tag/Custom-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères personnalisés. |
| [Critères d’élément](https://developer.adobe.com/target/administer/recommendations-api/#tag/Item-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères d’élément. |
| [Critères de popularité](https://developer.adobe.com/target/administer/recommendations-api/#tag/Popularity-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères de popularité. |
| [Critères d’attribut de profil](https://developer.adobe.com/target/administer/recommendations-api/#tag/Profile-Attribute-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères d’attribut de profil. |
| [ Critères récents ](https://developer.adobe.com/target/administer/recommendations-api/#tag/Recent-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères récents. |
| [Critères de séquence](https://developer.adobe.com/target/administer/recommendations-api/#tag/Sequence-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères de séquence. |

## Documentation de référence

* [Documentation sur l’API de diffusion Adobe Target](/help/dev/implement/delivery-api/overview.md)
* [Intégration de Recommendations dans la messagerie électronique](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html?lang=fr)

## Résumé et révision

Félicitations ! En complétant ce guide, vous avez appris à :
* [Gérer votre catalogue à l’aide de l’API Recommendations](manage-catalog.md)
* [Gestion des critères personnalisés à l’aide de l’API Recommendations](manage-custom-criteria.md)
* [Utilisation de l’API de diffusion avec Recommendations](fetch-recs-server-side-delivery-api.md)
