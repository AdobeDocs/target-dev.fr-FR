---
keywords: implémentation, bibliothèque javascript, js, atjs, prise de décision sur l’appareil, prise de décision sur l’appareil, at.js, sur l’appareil, sur l’appareil, dépannage, dépannage, implémentation2
description: Découvrez comment résoudre les problèmes de [!UICONTROL prise de décision sur l’appareil] avec la bibliothèque at.js.
title: Comment résoudre les problèmes de prise de décision sur l’appareil avec la bibliothèque JavaScript at.js ?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
TQID: https://experienceleague.adobe.com/Ji3jAHC0Ek7FrVnabEEMm-KCtxJLJ5rSz4uyi6sWpiE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 281
ht-degree: 0%

---

# Résolution des problèmes [!UICONTROL prise de décision sur l’appareil] pour at.js

Effectuez les étapes suivantes pour résoudre le problème [!UICONTROL prise de décision sur l’appareil] dans [!UICONTROL Adobe Target] avec la bibliothèque JavaScript at.js :

## Étape 1 : activer le journal de la console pour at.js

L’ajout du paramètre d’URL `mboxDebug=1` permet à at.js d’imprimer des messages dans la console de votre navigateur.

Tous les messages contiennent le préfixe « AT: » pour une vue d’ensemble pratique. Pour vous assurer qu’un artefact a bien été chargé, le journal de votre console doit contenir des messages similaires à ceux-ci :

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

L’illustration suivante présente ces messages dans le journal de la console :

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Journal de console avec messages d’artefact](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Journal de console avec messages d’artefact"){zoomable="yes"}

## Étape 2 : vérifier le téléchargement de l’artefact de règle dans l’onglet Réseau de votre navigateur

Ouvrez l’onglet Réseau de votre navigateur.

Par exemple, pour ouvrir DevTools dans Google Chrome :

1. Appuyez sur Ctrl+Maj+J (Windows) ou Commande+Option+J (Mac).
1. Accédez à l’onglet Réseau .
1. Filtrez vos appels par mot-clé « rules.json » pour vous assurer que seul le fichier de règles d’artefact s’affiche.

   En outre, vous pouvez filtrer par « /delivery|rules.json/ » pour afficher tous les appels Target et règles d’artefact.json.

   ![Onglet Réseau dans Google Chrome](assets/rule-json.png)

## Étape 3 : vérifier le téléchargement de l’artefact de règle à l’aide d’événements personnalisés at.js

La bibliothèque at.js distribue deux nouveaux événements personnalisés pour prendre en charge [!UICONTROL la prise de décision sur l’appareil].

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

Vous pouvez vous abonner pour écouter ces événements personnalisés dans votre application afin d’agir en cas de réussite ou d’échec du téléchargement du fichier de règles d’artefact.

L’exemple suivant montre un exemple de code écoutant les événements de succès et d’échec du téléchargement d’artefact :

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```


