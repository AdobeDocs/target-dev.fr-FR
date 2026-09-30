---
keywords: application mobile, envoi de données d’application mobile, données utilisateur personnalisées mobiles, données personnalisées d’application mobile
description: Découvrez comment envoyer des informations supplémentaires sur l’emplacement ou l’utilisateur à [!DNL Adobe Target] en tant que paires nom-valeur pour vous aider à créer des audiences personnalisées.
title: Comment envoyer des données utilisateur personnalisées dans une application iOS ?
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: d051910f-2bda-47ea-a969-6ade9fcd71f1
    internal-label: Implement mobile
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 55%
---
# iOS - Envoi de données utilisateur personnalisées

Vous pouvez envoyer des informations supplémentaires sur l’emplacement ou l’utilisateur à [!DNL Target] en tant que paires nom-valeur.

>[!IMPORTANT]
>
>La prise en charge des SDK [!DNL Adobe Mobile] version 4.*x* a pris fin le 31 août 2021 et n’est plus recommandée pour les utilisateurs d’[!DNL Adobe Target] mobile.
>
>[Adobe Experience Platform SDK pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les solutions et services [!DNL Adobe Experience Cloud] dans vos applications mobiles.

Ces informations peuvent être utilisées pour créer des audiences personnalisées (par exemple, utilisateurs disposant de plus de 25 000 miles) et créer des rapports.

Vous pouvez envoyer deux types de paramètres avec un appel [!DNL Target] :

* **paramètres de mbox** : les paramètres de mbox ne sont pas persistants entre les sessions.
* **Paramètres de profil** : les paramètres de profil sont stockés dans la banque de profils du visiteur et sont persistants entre les sessions. Les paramètres de mbox ne sont pas conservés. Tandis que certaines clés sont réservées, les paramètres de profil et mbox peuvent être des paires personnalisées de type clé-valeur.

Bien que certaines clés soient réservées, les paramètres de profil et mbox peuvent contenir des paires clé-valeur personnalisées.

1. Création d’un dictionnaire.

   Créez tout d’abord un dictionnaire avec les valeurs que vous envoyez pour transmettre à [!DNL Target]. Pour des questions pratiques, ajoutez ces éléments à la méthode `welcomeMessageCampaign` de manière à ne pas devoir vous soucier de la portée.

   Vous trouverez ci-dessous un exemple de dictionnaire. Vous pouvez le copier et le coller dans la méthode `(void)welcomeMessageCampaign`. Les valeurs des clés telles que `userLevel` et `userMiles` sont codées en dur pour cet exemple. En règle générale, vous transférez les variables correspondantes.

   ```
   NSDictionary *targetParams = [[NSDictionary alloc] initWithObjectsAndKeys: 
                                 @"platinum",@"userLevel", 
                                 @26500,@"userMiles", 
                                 @"1067007",@"entity.id", 
                                 @"dealsapp.qa", @"host", 
                                 @"fashion",@"entity.categoryId", 
                                 @"millenial", @"profile.persona", 
                                 @"cohort_5", @"profile.cohort", 
                                 nil];
   ```

   * Les clés contenant un préfixe de profil (par exemple : `profile.persona`) sont stockées au niveau du profil d’utilisateur.

     Ces attributs de profil peuvent être utilisés pour différentes activités et différents canaux.

   * Les clés ne contenant aucun préfixe (par exemple : `userMiles`) sont des paramètres mbox.

     Ces paramètres sont disponibles uniquement lors de la session.

   * Les clés contenant un préfixe d’entité (par exemple : `entity.category.id`) sont utilisées pour des recommandations de produits.

1. Vérification des données.
   1. Dans l’application `didFinishLaunchingWithOptions`, décommentez ou ajoutez `[ADBMobile setDebugLogging:YES];`.

      Cette action imprime les journaux de débogage détaillés.
   1. Création de l’application.
   1. Vérifiez que les paramètres ont été transférés vers l’appel cible.

      Recherchez le nom de votre emplacement cible dans la console de débogage. Vous remarquerez un appel vers `YOUR-CLIENT-CODE.tt.omtrdc.net` contenant l’ensemble des paramètres que vous venez de transférer.

      (Cliquez sur l’image pour l’agrandir sur toute la largeur.)

      ![Emplacement cible dans la console &#x200B;](/help/dev/implement/mobile/assets/mobile-debug.png " débogageEmplacement cible dans la console de débogage"){zoomable="yes"}

   Vous pouvez créer des audiences et restreindre ou cibler l’affichage du contenu à l’aide de ces paramètres dans [!DNL Target].
