---
keywords: application mobile,sdk aep,application native,vues web,natif;swift,sdk mobile adobe experience platform,sdk mobile,code natif
description: Découvrez comment mettre en œuvre  [!DNL Adobe Target]  avec dans une application native  [!DNL AEP Mobile SDK]  vues web.
title: Implémentez  [!DNL Adobe Target]  dans une application mobile qui utilise du code natif avec des vues web
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
TQID: https://experienceleague.adobe.com/JrbjPpq3ds0sl4rkMnuzF9SYk2PI4r676hHqN-Pvn78
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: d051910f-2bda-47ea-a969-6ade9fcd71f1
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 624
ht-degree: 0%

---

# Implémentez [!DNL Target] avec le [!DNL AEP Mobile SDK] dans une application native avec des vues web

Cet article partage les bonnes pratiques pour l’implémentation de [!DNL Adobe Target] dans une application mobile qui utilise du code natif avec des vues web à l’aide de l’[!DNL Adobe Experience Platform Mobile SDK] .

Cet article utilise un exemple d’application iOS utilisant le [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} et une intégration [!DNL Target] écrite dans [Swift à partir du référentiel GitHub](https://github.com/adobe/aep-sdk-app/){target=_blank}.

Dans le monde réel, votre application d’entreprise utilise probablement des vues web dans votre application mobile. Un affichage web est un conteneur qui charge une page web à l’aide d’une URL. Le conteneur est similaire à une fenêtre de navigateur sans commandes. Dans iOS, le conteneur d’affichage web fonctionne comme un navigateur Safari lors du traitement des pages web.

## Conditions préalables

Pour commencer à utiliser le [!DNL Adobe Experience Platform Mobile SDK], vous devez effectuer certaines tâches préalables.

Pour plus d’informations, voir [](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} dans la documentation [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank}.

## Synchroniser le code natif avec les vues web

Le défi de l’implémentation de [!DNL Target] dans une application native avec des vues web est que l’[!DNL Adobe Experience Platform Mobile SDK] a déjà généré tous les identifiants nécessaires au fonctionnement transparent de [!DNL Adobe] solutions. Toutefois, les identifiants ne sont pas encore visibles pour les vues web , car ils ne se trouvent pas dans l’environnement natif de la plateforme. Par conséquent, vous devez créer un pont pour transmettre certains identifiants SDK aux vues web afin que l’identité du visiteur persiste dans l’environnement web. Si vous ne le faites pas correctement, des visites sont effectuées en double, ce qui affecte vos rapports.

Heureusement, le [!DNL Adobe Experience Platform Mobile SDK] fournit une méthode pratique pour générer les paramètres [!DNL Adobe] requis pour que les vues web soient utilisées et conservées pour le même visiteur, comme illustré dans l’exemple de code suivant :

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

Pour plus d’informations sur la méthode `Identity.appendTo` et pour voir un exemple d’utilisation de la méthode, voir [Swift > Exemple](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} dans la *Documentation de Mobile SDK*.

En utilisant `Identity.appendTo`, cette URL :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

se transforme en :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Comme vous pouvez le constater, `adobe_mc` paramètre est ajouté à l’URL. Ce paramètre contient les valeurs codées pour :

* TS=1660667205 : date et heure actuelles. Cet horodatage garantit que l’affichage web ne reçoit pas de valeurs expirées.
* MCMID=69624092487065093697422606480535692677 : [!UICONTROL  Experience Cloud ID ] (ECID). Également appelé MID ou [!UICONTROL Marketing Cloud ID] requis pour [!DNL Adobe] identification des visiteurs intersolutions.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg : [!UICONTROL ID d’organisation Adobe].

L’`Identity.getUrlVariables` est une autre méthode de [!DNL Adobe Experience Platform Mobile SDK] qui renvoie une chaîne correctement formée contenant les variables d’URL [!DNL Experience Cloud Identity Service]. Pour plus d’informations, voir [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} dans la référence de l’API *Identity*.

## Transmettez l’ID de session [!DNL Target] pour une expérience de même session

Une étape supplémentaire est nécessaire pour que le parcours utilisateur [!DNL Target] fonctionne de manière transparente dans les vues native et web. Cette étape comprend l’extraction et la transmission de l’ID de session [!DNL Target] du [!DNL Adobe Experience Platform Mobile SDK] aux affichages web de l’application mobile.

Le `Target.getSessionId` extrait l’ID de session qui peut être transmis à l’URL de l’affichage web en tant que paramètre de `mboxSession` :

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Test dans les vues web

Les liens d’aperçu web sont générés sur la page [!UICONTROL Détails de l’activité] en cliquant sur le lien [[!UICONTROL AQ Adobe]](/help/dev/implement/mobile/target-mobile-preview.md) pour afficher un pop-up afin de copier chaque lien d’aperçu d’expérience, comme suit :

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Les liens d’aperçu web contiennent des paramètres de `at_preview_index` et de `at_preview_listed_activities_only` supplémentaires. Copiez ces paramètres pour créer des liens d’aperçu compatibles avec les appareils mobiles avec les paramètres de lien web.

Par exemple :

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Après avoir ouvert le lien dans un navigateur Safari iOS, votre application capture l’URL dans votre classe de `AppDelegate` comme dans l’exemple suivant :

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Maintenant que vous avez capturé tous les paramètres nécessaires dans l’application, vous pouvez les transmettre au web si nécessaire :

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

La sortie finale du lien d’affichage web peut se présenter comme suit :

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
