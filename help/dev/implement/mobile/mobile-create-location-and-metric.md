---
keywords: application mobile, emplacement d’application mobile, cibler une application mobile, emplacements cibles des applications mobiles, mesures de succès des applications mobiles
description: 'Affichez un exemple de code pour apprendre à créer des emplacements et des mesures de succès dans les applications iOS afin de pouvoir utiliser pour personnaliser et optimiser votre application [!DNL Adobe Target] '
title: Comment créer des emplacements et  [!DNL Target]  mesures de succès dans une application iOS ?
feature: Implement Mobile
exl-id: 755c8b26-5c60-48fc-9e7e-5e97a25edb78
TQID: https://experienceleague.adobe.com/frolzqCgdL0iz5Z3E8OaJmP6yiVq7jEYiWn6LD4bocA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 63%

---

# iOS - Création d’un emplacement [!DNL Target] et d’une mesure de succès

Pour utiliser [!DNL Target] dans votre application mobile, créez un emplacement et une mesure de succès.

>[!IMPORTANT]
>
>La prise en charge des SDK [!DNL Adobe Mobile] version 4.*x* a pris fin le 31 août 2021 et n’est plus recommandée pour les utilisateurs d’[!DNL Adobe Target] mobile.
>
>[Adobe Experience Platform SDK pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les solutions et services [!DNL Adobe Experience Cloud] dans vos applications mobiles.

Cette section comprend un exemple de code pouvant être utilisé comme modèle pour votre application. Les exemples de cette section contiennent un code pour iOS. Les mêmes modèles s’appliquent à Android. Vous trouverez la syntaxe spécifique à Android dans le guide [Android SDK 4.x pour les solutions Experience Cloud](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/target-main.html?lang=fr) .

>[!NOTE]
>
>Consultez la [Documentation mobile](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-target-methods.html?lang=fr) pour obtenir une liste de toutes les méthodes de [!DNL Target] disponibles.

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
   | `heroImage.image = [UIImage imageNamed:content];` | Par exemple : définissez le contenu et configurez le chemin d’une image principale. |

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
