---
keywords: application mobile,sdk aep,application native,vues web,natif;swift,sdk mobile adobe experience platform,sdk mobile,code natif
description: Découvrez comment implémenter [!DNL Adobe Target] avec la propriété [!DNL AEP Mobile SDK] dans une application native avec des vues web.
title: Mise en oeuvre [!DNL Adobe Target] dans une application mobile qui utilise du code natif avec des vues web ;
feature: Implement Mobile
role: Developer
source-git-commit: c0fda36cb5472d71438c47b8b484716003da4214
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# Mise en oeuvre [!DNL Target] avec la propriété [!DNL AEP Mobile SDK] dans une application native avec des vues web

Cet article présente les bonnes pratiques pour la mise en oeuvre de [!DNL Adobe Target] dans une application mobile qui utilise du code natif avec des vues web à l’aide de la variable [!DNL Adobe Experience Platform Mobile SDK].

Cet article utilise un exemple d’application iOS à l’aide de la fonction [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

Dans le monde réel, votre application d’entreprise utilise probablement des vues web dans votre application mobile. Un affichage web est un conteneur qui charge une page web à l’aide d’une URL. Le conteneur est similaire à une fenêtre de navigateur sans contrôle. Dans iOS, le conteneur d’affichage web fonctionne comme un navigateur Safari lors du traitement des pages web.

## Conditions préalables

Pour commencer à utiliser la méthode [!DNL Adobe Experience Platform Mobile SDK], vous devez effectuer certaines tâches prérequises.

Pour plus d’informations, voir [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} la documentation.

## Synchronisation du code natif avec les vues web

Le défi de la mise en oeuvre [!DNL Target] dans une application native avec des vues web est que la variable [!DNL Adobe Experience Platform Mobile SDK] a déjà généré tous les identifiants nécessaires pour [!DNL Adobe] pour travailler en toute transparence. Toutefois, les identifiants ne sont pas encore visibles par les vues web, car ces identifiants ne se trouvent pas dans l’environnement natif de la plateforme. Par conséquent, vous devez créer un pont pour transmettre certains identifiants SDK aux vues web afin que l’identité du visiteur persiste dans l’environnement web. Si vous ne le faites pas correctement, il en résulte des visites en double, ce qui affecte vos rapports.

Heureusement, le [!DNL Adobe Experience Platform Mobile SDK] fournit une méthode pratique pour générer des [!DNL Adobe] paramètres requis pour que les vues web consomment et persistent pour le même visiteur, comme illustré dans l’exemple de code suivant :

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

Pour plus d’informations sur la variable `Identity.appendTo` et pour voir un exemple d’utilisation de la méthode, voir [Swift > Exemple](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} dans le *Documentation du SDK Mobile*.

Utilisation `Identity.appendTo`, cette URL :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

se transforme en :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Comme vous pouvez le voir, il y a `adobe_mc` ajouté à l’URL. Ce paramètre contient des valeurs codées pour :

* TS=1660667205 : horodatage actuel. Cet horodatage permet de s’assurer que l’affichage web ne reçoit pas les valeurs expirées.
* MCMID=69624092487065093697422606480535692677 : la variable [!UICONTROL Identifiant Experience Cloud] (ECID). Également appelé MID ou [!UICONTROL ID de Marketing Cloud] requis pour [!DNL Adobe] identification des visiteurs inter-solutions.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: [!UICONTROL ID d’organisation Adobe].

La variable `Identity.getUrlVariables` est une alternative ; [!DNL Adobe Experience Platform Mobile SDK] qui renvoie une chaîne correctement formée contenant la variable [!DNL Experience Cloud Identity Service] Variables d’URL. Pour plus d’informations, voir [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} dans le *Référence de l’API Identity*.

## Transmettez la variable [!DNL Target] ID de session pour une expérience de même session

Une étape supplémentaire est nécessaire pour que la variable [!DNL Target] le parcours utilisateur fonctionne de manière transparente sur les vues natives et web. Cette étape comprend l’extraction et la transmission [!DNL Target] ID de session de la [!DNL Adobe Experience Platform Mobile SDK] aux vues web de l’application mobile.

La variable `Target.getSessionId` extrait l’ID de session qui peut être transmis à l’URL de l’affichage web sous la forme d’une `mboxSession` parameter:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Test dans les vues web

Les liens d&#39;aperçu Web sont générés sur la variable [!UICONTROL Détails de l’activité] en cliquant sur la [[!UICONTROL AQ d’Adobe] link](/help/dev/implement/mobile/target-mobile-preview.md) pour afficher une fenêtre contextuelle afin de copier chaque lien d’aperçu d’expérience, comme suit :

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Les liens d’aperçu web contiennent des liens supplémentaires `at_preview_index` et `at_preview_listed_activities_only` paramètres. Copiez ces paramètres pour créer des liens d’aperçu compatibles avec les mobiles avec des paramètres de lien web.

Par exemple :

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Après avoir ouvert le lien dans un navigateur Safari iOS, votre application capture l’URL dans votre `AppDelegate` , comme dans l’exemple suivant :

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Maintenant que vous avez capturé tous les paramètres nécessaires dans l’application, vous pouvez les transmettre sur le web si nécessaire :

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

La sortie finale du lien d’affichage web peut se présenter comme suit :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
