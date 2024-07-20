---
keywords: application mobile,sdk aep,application native,vues web,natif;swift,sdk mobile adobe experience platform,sdk mobile,code natif
description: Découvrez comment implémenter  [!DNL Adobe Target] avec  [!DNL AEP Mobile SDK]  dans une application native avec des vues web.
title: Implémenter  [!DNL Adobe Target]  dans une application mobile qui utilise du code natif avec des vues web
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Mettre en oeuvre [!DNL Target] avec [!DNL AEP Mobile SDK] dans une application native avec des vues web

Cet article partage les bonnes pratiques pour implémenter [!DNL Adobe Target] dans une application mobile qui utilise du code natif avec des vues web à l’aide de [!DNL Adobe Experience Platform Mobile SDK].

Cet article utilise un exemple d’application iOS à l’aide de [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} et d’une intégration [!DNL Target] écrite dans [Swift à partir du référentiel GitHub](https://github.com/adobe/aep-sdk-app/){target=_blank}.

Dans le monde réel, votre application d’entreprise utilise probablement des vues web dans votre application mobile. Un affichage web est un conteneur qui charge une page web à l’aide d’une URL. Le conteneur est similaire à une fenêtre de navigateur sans contrôle. Dans iOS, le conteneur d’affichage web fonctionne comme un navigateur Safari lors du traitement des pages web.

## Conditions préalables

Pour commencer à utiliser [!DNL Adobe Experience Platform Mobile SDK], vous devez effectuer certaines tâches préalables requises.

Pour plus d’informations, voir [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} dans la documentation [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank}.

## Synchronisation du code natif avec les vues web

La difficulté lors de l&#39;implémentation de [!DNL Target] dans une application native avec des vues web est que [!DNL Adobe Experience Platform Mobile SDK] a déjà généré tous les identifiants nécessaires au bon fonctionnement des solutions [!DNL Adobe]. Toutefois, les identifiants ne sont pas encore visibles par les vues web, car ces identifiants ne se trouvent pas dans l’environnement natif de la plateforme. Par conséquent, vous devez créer un pont pour transmettre certains identifiants SDK aux vues web afin que l’identité du visiteur persiste dans l’environnement web. Si vous ne le faites pas correctement, il en résulte des visites en double, ce qui affecte vos rapports.

Heureusement, [!DNL Adobe Experience Platform Mobile SDK] fournit une méthode pratique pour générer les paramètres [!DNL Adobe] requis pour que les vues web soient consommées et conservées pour le même visiteur, comme illustré dans l’exemple de code suivant :

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

Pour plus d’informations sur la méthode `Identity.appendTo` et pour voir un exemple d’utilisation de la méthode, voir [Swift > Exemple](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} dans la *documentation du SDK mobile*.

En utilisant `Identity.appendTo`, cette URL :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

se transforme en :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Comme vous pouvez le constater, un paramètre `adobe_mc` est ajouté à l’URL. Ce paramètre contient des valeurs codées pour :

* TS=1660667205 : horodatage actuel. Cet horodatage permet de s’assurer que l’affichage web ne reçoit pas les valeurs expirées.
* MCMID=69624092487065093697422606480535692677 : [!UICONTROL Experience Cloud ID] (ECID). Également appelé MID ou [!UICONTROL Marketing Cloud ID] requis pour l’identification des visiteurs [!DNL Adobe] inter-solutions.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg : [!UICONTROL Adobe Organization ID].

`Identity.getUrlVariables` est une autre méthode [!DNL Adobe Experience Platform Mobile SDK] qui renvoie une chaîne correctement formée contenant les variables d’URL [!DNL Experience Cloud Identity Service]. Pour plus d’informations, voir [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} dans la *référence de l’API Identity*.

## Transmettez l’ID de session [!DNL Target] pour une expérience de même session

Une étape supplémentaire est nécessaire pour que le parcours d’utilisateurs [!DNL Target] fonctionne parfaitement sur les vues natives et web. Cette étape consiste à extraire et à transmettre l’ID de session [!DNL Target] de [!DNL Adobe Experience Platform Mobile SDK] aux vues web de l’application mobile.

`Target.getSessionId` extrait l’ID de session qui peut être transmis à l’URL de l’affichage web en tant que paramètre `mboxSession` :

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Test dans les vues web

Les liens d’aperçu web sont générés sur la page [!UICONTROL Activity detail] en cliquant sur le lien [[!UICONTROL Adobe QA]](/help/dev/implement/mobile/target-mobile-preview.md) pour afficher une fenêtre contextuelle permettant de copier chaque lien d’aperçu d’expérience, comme suit :

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Les liens d’aperçu web contiennent des paramètres `at_preview_index` et `at_preview_listed_activities_only` supplémentaires. Copiez ces paramètres pour créer des liens d’aperçu compatibles avec les mobiles avec des paramètres de lien web.

Par exemple :

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Après avoir ouvert le lien dans un navigateur Safari iOS, votre application capture l’URL dans votre classe `AppDelegate` comme dans l’exemple suivant :

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
