---
keywords: application mobile, emplacement d’application mobile, cibler une application mobile, emplacements cibles des applications mobiles, mesures de succès des applications mobiles
description: Affichez un exemple de code pour vous aider à apprendre à créer des emplacements et des mesures de succès dans les applications iOS afin que vous puissiez utiliser  [!DNL Adobe Target] pour personnaliser et optimiser votre application.
title: Comment créer [!DNL Target] des emplacements et des mesures de succès dans une application iOS ?
feature: Implement Mobile
exl-id: 755c8b26-5c60-48fc-9e7e-5e97a25edb78
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 66%

---

# iOS : créez un emplacement [!DNL Target] et une mesure de succès.

Pour utiliser [!DNL Target] dans votre application mobile, créez un emplacement et une mesure de succès.

>[!IMPORTANT]
>
>Prise en charge de la version 4 de [!DNL Adobe Mobile].Les SDK *x* ont pris fin le 31 août 2021 et ne sont plus recommandés pour les utilisateurs mobiles [!DNL Adobe Target].
>
>Le [SDK Adobe Experience Platform pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les services et solutions [!DNL Adobe Experience Cloud] de vos applications mobiles.

Cette section comprend un exemple de code pouvant être utilisé comme modèle pour votre application. Les exemples de cette section contiennent un code pour iOS. Les mêmes modèles s’appliquent à Android. La syntaxe spécifique à Android est disponible dans le guide [Android SDK 4.x pour solutions Experience Cloud](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/target-main.html) .

>[!NOTE]
>
>Pour obtenir la liste de toutes les méthodes [!DNL Target] disponibles, reportez-vous à la [documentation mobile](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-target-methods.html) .

Pour créer un emplacement [!DNL Target] dans votre application et effectuer une requête, il existe deux méthodes principales :

* `targetCreateRequestWithName`
* `targetLoadRequest`

1. Créez un emplacement [!DNL Target].

   Voici un exemple d’appel permettant de créer une requête :

   ```
   // make your request 
   ADBTargetLocationRequest *myRequest = [ADBMobile targetCreateRequestWithName:@"heroBanner" 
                                                    defaultContent:@"default.png" 
                                                    parameters:nil];
   ```

   | Paramètre | Description |
   |---|---|
   | `ADBTargetLocationRequest *myRequest` | Remplacez `myRequest` par le nom de votre `targetLocation` dans l’application. |
   | `targetCreateRequestWithName:@"heroBanner"` | Remplacez `heroBanner` par le nom de votre `targetLocation` dans Target. Il s’agit du même nom que celui de la mbox. Cette bannière à forte identification apparaît dans l’interface de Target. |
   | `defaultContent:@"default.png"` | Remplacez `default.png` par la valeur utilisée par l’application lorsque Target ne répond pas. |
   | `parameters:nil` | Précisez le profil ou les paramètres mbox. Obtenez des informations complémentaires dans la section « Diffusion de données personnalisées ». |

   Voici un exemple d’appel permettant de charger la requête :

   ```
   // load your request 
   [ADBMobile targetLoadRequest:myRequest callback:^(NSString *content) { 
                                        // do something with content 
                                        heroImage.image = [UIImage imageNamed:content]; 
   }];
   ```

   | Paramètre | Description |
   |---|---|
   | `targetLoadRequest:myRequest` | Remplacez `myRequest` par le nom de votre `targetLocation` dans l’application. |
   | `NSString *content` | Remplacez le contenu par le contenu actuel provenant d’Adobe. La chaîne peut être au format XML, JSON ou brut. Utilisez cette section du code pour définir les variables, configurer les chemins des images, afficher les commandes de flux, les points de transaction ou toute autre action de votre choix. Target rendra le contenu saisi au niveau de l’interface utilisateur exactement au même format. |
   | `heroImage.image = [UIImage imageNamed:content];` | Par exemple : définissez le contenu et configurez le chemin d’une image à forte identification. |

1. Création d’une mesure de succès.

   La méthode `targetCreateOrderConfirmRequestWithName` peut être utilisée pour suivre une mesure de conversion/succès dans votre application.

   ```
   ADBTargetLocationRequest *req = [ADBMobile targetCreateOrderConfirmRequestWithName: "orderConfirm" 
                                              orderId: orderId 
                                              orderTotal: @"39.95" 
                                              productPurchasedId: _galleryItem.title 
                                              parameters: nil]; 
   [ADBMobile targetLoadRequest: req callback: nil];
   ```

   | Paramètre | Description |
   |---|---|
   | `orderId` | Remplacez cette valeur par une variable dynamique qui représente un ID de commande unique. |
   | `@"39.95"` | Remplacez cette valeur par une variable dynamique qui représente un total de commande unique. |
   | `_galleryItem.title` | Remplacez cette valeur par une variable dynamique qui représente une liste de produits achetés, délimités par des virgules. |
   | `parameters: nil` | Dictionnaire facultatif des paramètres supplémentaires. |

1. Création de l’application.

   Une fois votre emplacement cible créé et le balisage d’une mesure de succès effectué, créez un test A/B. L’activité peut être créée en utilisant le compositeur d’expérience d’après les formulaires.
