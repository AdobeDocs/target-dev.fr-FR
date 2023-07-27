---
keywords: implémentation, bibliothèque javascript, js, atjs, prise de décision sur l’appareil, prise de décision sur l’appareil, at.js, sur l’appareil, résolution des problèmes, mise en oeuvre2
description: Découvrez comment résoudre les problèmes [!UICONTROL prise de décision sur appareil] avec la bibliothèque at.js.
title: Comment résoudre les problèmes liés à la prise de décision sur les périphériques avec la bibliothèque JavaScript at.js ?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Dépannage [!UICONTROL prise de décision sur appareil] pour at.js

Procédez comme suit pour résoudre les problèmes [!UICONTROL prise de décision sur appareil] in [!UICONTROL Adobe Target] avec la bibliothèque JavaScript at.js :

## Étape 1 : activation du journal de la console pour at.js

Ajout du paramètre d’URL `mboxDebug=1` permet à at.js d’imprimer les messages dans la console du navigateur.

Tous les messages contiennent un préfixe &quot;AT:&quot; pour une présentation pratique. Pour vous assurer qu’un artefact a bien été chargé, le journal de votre console doit contenir des messages similaires à ceux-ci :

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

L’illustration suivante présente ces messages dans le journal de la console :

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![Journal de la console avec des messages d’artefact](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Journal de la console avec des messages d’artefact"){zoomable=&quot;yes&quot;}

## Étape 2 : vérification du téléchargement de l’artefact de règle dans l’onglet Réseau de votre navigateur

Ouvrez l’onglet Réseau de votre navigateur.

Par exemple, pour ouvrir DevTools dans Google Chrome :

1. Appuyez sur Ctrl+Maj+J (Windows) ou Commande+Option+J (Mac).
1. Accédez à l’onglet Réseau.
1. Filtrez vos appels par mot-clé &quot;rules.json&quot; pour vous assurer que seul le fichier de règles d’artefact s’affiche.

   En outre, vous pouvez filtrer par &quot;/delivery|rules.json/&quot; pour afficher tous les appels Target et artefact rules.json.

   ![Onglet Réseau dans Google Chrome](assets/rule-json.png)

## Étape 3 : vérification du téléchargement des artefacts de règle à l’aide des événements personnalisés at.js

La bibliothèque at.js distribue deux nouveaux événements personnalisés pour prendre en charge [!UICONTROL prise de décision sur appareil].

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

Vous pouvez vous abonner pour écouter ces événements personnalisés dans votre application afin d’agir en cas de succès ou d’échec du téléchargement du fichier de règles d’artefact.

L’exemple suivant illustre un exemple de code écoutant les événements de succès et d’échec de téléchargement d’artefact :

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```
