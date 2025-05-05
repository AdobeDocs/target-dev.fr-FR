---
title: Gestion des déploiements pour les tests de fonctionnalités
description: Découvrez comment gérer les déploiements pour les tests de fonctionnalités à l’aide de [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Gestion des déploiements pour les tests de fonctionnalités

## Résumé des étapes

1. Activer [!UICONTROL on-device decisioning] pour votre organisation
1. Créer une activité [!UICONTROL A/B Test]
1. Définition de votre fonction et des paramètres de déploiement
1. Mise en oeuvre et rendu de la fonctionnalité dans votre application
1. Mise en oeuvre du suivi des événements dans votre application
1. Activation de votre activité A/B
1. Ajuster le déploiement et l’affectation du trafic selon les besoins

## 1. Activez [!UICONTROL on-device decisioning] pour votre organisation.

L’activation de la prise de décision sur l’appareil garantit qu’une activité A/B est exécutée à une latence proche de zéro. Pour activer cette fonction, accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** dans [!DNL Adobe Target] et activez le bouton d’activation/désactivation de **[!UICONTROL On-Device Decisioning]**.

![alt image](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Vous devez disposer du rôle d’administrateur ou d’approbateur [utilisateur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=fr) pour activer ou désactiver le bouton d’activation/désactivation de [!UICONTROL On-Device Decisioning].

Après avoir activé le bouton d’activation [!UICONTROL On-Device Decisioning], [!DNL Adobe Target] commence à générer des *artefacts de règle* pour votre client.

## 2. Créer une activité [!UICONTROL A/B Test]

1. Dans [!DNL Adobe Target], accédez à la page **[!UICONTROL Activities]**, puis sélectionnez **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**.

   ![alt image](assets/asset-ab.png)

1. Dans le modal **[!UICONTROL Create A/B Test Activity]**, laissez l’option **[!UICONTROL Web]** par défaut sélectionnée (1), sélectionnez **[!UICONTROL Form]** comme compositeur d’expérience (2), sélectionnez **[!UICONTROL Default Workspace]** avec **[!UICONTROL No Property Restrictions]** (3), puis cliquez sur **[!UICONTROL Next]** (4).

   ![alt image](assets/asset-form.png)

## 3. Définissez les paramètres de votre fonction et de déploiement.

À l’étape **[!UICONTROL Experiences]** de la création de l’activité, donnez un nom à votre activité (1). Saisissez le nom de l’emplacement (2) dans votre application où vous souhaitez gérer les déploiements de votre fonction. Par exemple, `ondevice-rollout` ou `homepage-addtocart-rollout` sont des noms d’emplacement indiquant les destinations de gestion des déploiements de fonctionnalités. Dans l’exemple ci-dessous, `ondevice-rollout` est l’emplacement défini pour l’expérience A. Vous pouvez éventuellement ajouter des ajustements d’audience (4) pour limiter la qualification à l’activité.

![alt image](assets/asset-location-rollout.png)

1. Dans la section **[!UICONTROL Content]** de la même page, sélectionnez **[!UICONTROL Create JSON Offer]** dans la liste déroulante (1) comme indiqué.

   ![alt image](assets/asset-offer.png)

1. Dans la zone de texte **[!UICONTROL JSON Data]** qui s’affiche, saisissez la variable d’indicateur de fonctionnalité pour la fonctionnalité que vous avez l’intention de déployer avec cette activité dans l’expérience A (1), à l’aide d’un objet JSON valide (2).

   ![alt image](assets/asset-json-a-rollout.png)

1. Cliquez sur **[!UICONTROL Next]** (1) pour passer à l’étape **[!UICONTROL Targeting]** de la création de l’activité.

   ![alt image](assets/asset-next-2-t-rollout.png)

1. À l’étape **[!UICONTROL Targeting]** , conservez l’audience **[!UICONTROL All Visitors]** (1), pour plus de simplicité. Mais ajustez l’affectation du trafic (2) à 10 %. Cette option limite la fonctionnalité à seulement 10 % des visiteurs de votre site. Cliquez sur Suivant (3) pour passer à l’étape **[!UICONTROL Goals & Settings]**.

   ![alt image](assets/asset-next-2-g-rollout.png)

1. À l’étape **[!UICONTROL Goals & Settings]** , choisissez **[!UICONTROL Adobe Target]** (1) comme **[!UICONTROL Reporting Source]** pour afficher les résultats de votre activité dans l’interface utilisateur de [!DNL Adobe Target].

1. Sélectionnez un **[!UICONTROL Goal Metric]** pour mesurer l’activité. Dans cet exemple, une conversion réussie dépend de l’achat ou non d’un élément par l’utilisateur, comme indiqué par l’accès ou non de l’utilisateur à l’emplacement orderConfirm (2).

1. Cliquez sur **[!UICONTROL Save & Close]** (3) pour enregistrer l’activité.

   ![alt image](assets/asset-conv-rollout.png)

## 4. Implémentez et effectuez le rendu de la fonctionnalité dans votre application.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
targetClient.getAttributes(["ondevice-rollout"]).then(function(attributes) {
      const featureFlags = attributes.asObject("ondevice-rollout");

      // Your flag variables are now available in the featureFlags object variable.
      //If you failed to qualify for the Activity, you will have an empty object.
      console.log(featureFlags);
    });
```

>[!TAB Java]

```java {line-numbers="true"}
    Attributes attrs = targetJavaClient.getAttributes(targetDeliveryRequest, "ondevice-rollout");
    Map<String, Object> featureFlags = attrs.toMboxMap("ondevice-rollout");
​
    // Your flag variables are now available in the featureFlags object variable.
    //If you failed to qualify for the Activity, you will have an empty object.
    System.out.println(featureFlags);
```

>[!ENDTABS]

## 5. Implémentation du suivi des événements dans votre application

Après avoir rendu la variable d’indicateur de fonctionnalité disponible dans l’application, vous pouvez l’utiliser pour activer toute fonctionnalité qui fait déjà partie de votre application. Si un visiteur ne remplit pas les critères de l’activité, cela signifie qu’il n’a pas été inclus dans le compartiment de 10 % défini comme audience.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

if(featureFlags.enable == "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}

// alternatively, the getValue method could be used on the Attributes object.

if(attributes.getValue("ondevice-rollout", "enable") === "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}
```

>[!TAB Java]

```java {line-numbers="true"}
//... Code removed for brevity
​
if("yes".equals(String.valueOf(featureFlags.get("enable")))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
​
// alternatively, the getString method could be used on the Attributes object.
​
if("yes".equals(attrs.getString("ondevice-rollout", "enable"))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
```

>[!ENDTABS]

## 6. Activez votre activité de déploiement.

![alt image](assets/asset-activate-rollout.png)

## 7. Ajustez le déploiement et l’affectation du trafic selon les besoins

Une fois que vous avez activé votre activité, modifiez-la à tout moment afin d’augmenter ou de diminuer l’affectation du trafic, le cas échéant.

Augmentation de l’affectation du trafic de 10 % à 50 % en raison du succès du déploiement initial.

![alt image](assets/asset-adjust-rollout.png)
