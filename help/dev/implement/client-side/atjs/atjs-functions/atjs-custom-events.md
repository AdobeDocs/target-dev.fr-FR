---
keywords: événements personnalisés, at.js, échec de la requête, succès de la requête, échec du rendu du contenu, succès du rendu du contenu, bibliothèque chargée, début de la requête, début du rendu du contenu, aucune offre de rendu du contenu, redirection du rendu du contenu, événements personnalisés2
description: Utilisez des événements personnalisés pour que la bibliothèque JavaScript at [!DNL Adobe Target] js soit avertie en cas d’échec ou de succès d’une requête ou d’une offre de mbox.
title: Comment utiliser les événements personnalisés at.js ?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
TQID: https://experienceleague.adobe.com/gCjLJ-XBlMe-GE-gaTJ2wHkn1jmal6Ftbs1GDb0zURA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 661
ht-degree: 70%

---

# événements personnalisés at.js

Informations sur `at.js custom events`, qui permet de savoir quand une requête ou une offre mbox échoue ou réussit.

Historiquement, mbox.js (désormais obsolète) ne laissait pas les autres codes JavaScript exécutés sur la page savoir ce qui se passe en arrière-plan. Avec l’évolution d’at.js, nous avions une opportunité unique de résoudre ce problème.

Nos clients nous ont ainsi indiqué qu’ils souhaiteraient être informés dans différentes situations, notamment lorsque :

* Une requête mbox a échoué en raison du délai d’attente, d’un code d’état erroné, d’une erreur d’analyse JSON, etc.
* Une requête mbox a réussi.
* Le rendu d’une offre a échoué en raison d’un élément mbox d’encapsulage manquant, d’un sélecteur introuvable, etc.
* Le rendu d’une offre a réussi. Des modifications ont été appliquées au modèle DOM.

Les événements prédéfinis ont une structure qui vous permet d’extraire les données requises en fonction du type d’événement.

Pour s’assurer que des événements peuvent être utilisés dans différents scénarios, les événements personnalisés ont un objet de charge utile affecté à la propriété Détail de l’objet d’événement (transféré au gestionnaire). De plus, pour éviter de transférer des chaînes comme noms d’événements, les événements sont exposés sous la forme de constantes par le biais de l’espace de noms `adobe.target.event`.

## Structure

| Clé | Type | Description |
|--- |--- |--- |
| type | Chaîne | Il existe plusieurs scénarios dans lesquels vous pouvez souhaiter être notifié afin de faciliter les activités de traçage, de débogage et de personnalisation de l’interaction avec at.js.<p>Chacun des événements personnalisés ci-dessous comporte deux formats : une « constante » et une « valeur de chaîne ».<ul><li>**Constantes** : précédées de `adobe.target.event.`, présentées en majuscules et contenant des traits de soulignement. Pour vous abonner à des événements personnalisés *après* le chargement d’at.js, mais *avant* que la réponse mbox n’ait été reçue, utilisez le format de la constante.</li><li>**Valeurs de chaîne** : en minuscules avec des tirets. Pour vous abonner à des événements personnalisés *avant* le chargement d’at.js, utilisez la valeur de chaîne.</li></ul>**Échec de la demande**<p>Constante : `adobe.target.event.REQUEST_FAILED`<p>Valeur de chaîne : `at-request-failed`<p>Description : une requête mbox a échoué en raison du délai d’attente, d’un code d’état erroné, d’une erreur d’analyse JSON, etc.<p>**Succès de la demande**<p>Constante : `adobe.target.event.REQUEST_SUCCEEDED`<p>Valeur de chaîne : `at-request-succeeded`<p>Description : une requête mbox a réussi.<p>**Échec de rendu du contenu**<p>Constante : `adobe.target.event.CONTENT_RENDERING_FAILED`<p>Valeur de chaîne : `at-content-rendering-failed`<p>Description : le rendu d’une offre a échoué en raison d’un élément mbox d’encapsulage manquant, d’un sélecteur introuvable, etc.<p>**Succès du rendu du contenu**<p>Constante : `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>Valeur de chaîne : `at-content-rendering-succeeded`<p>Description : le rendu d’une offre a réussi. Des modifications ont été appliquées au modèle DOM.<p>**Bibliothèque chargée**<p>Constante : `adobe.target.event.LIBRARY_LOADED`<p>Valeur de chaîne : `at-library-loaded`<p>Description : cet événement est idéal pour suivre le moment où at.js a été entièrement chargé. Vous pouvez utiliser cet événement pour personnaliser l’exécution globale de mbox. Vous pouvez également l’utiliser pour désactiver la mbox globale, puis écouter cet événement de manière à en différer le déclenchement.<p>**Début de la requête**<p>Constante : `adobe.target.event.REQUEST_START`<p>Valeur de chaîne : `at-request-start`<p>Description : cet événement est déclenché avant l’exécution d’une requête HTTP. Vous pouvez utiliser cet événement pour effectuer des mesures de performances à l’aide de l’API de temporisation de ressources.<p>**Début du rendu du contenu**<p>Constante : `adobe.target.event.CONTENT_RENDERING_START`<p>Valeur de chaîne : `at-content-rendering-start`<p>Description : cet événement est déclenché avant le début de l’interrogation du sélecteur et le rendu du contenu sur la page. Vous pouvez utiliser cet événement pour effectuer le suivi de la progression du rendu du contenu.<p>**Aucune offre rendue par le contenu**<p>Constante : `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>Valeur de chaîne : `at-content-rendering-no-offers`<p>Description : cet événement est déclenché lorsqu’aucune offre n’est renvoyée.<p>**Redirection du rendu du contenu**<p>Constante : `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>Valeur de chaîne : `at-content-rendering-redirect`<p>Description : cet événement est déclenché lorsqu’une offre est une redirection et que [!DNL Target] redirige vers une autre URL. |
| mbox | Chaîne | nom de mbox |
| message | Chaîne | Contient une description explicite indiquant ce qui s’est passé, le message d’erreur, etc. |
| Suivi | Objet | Contient `sessionId` et `deviceId`. Dans certains cas, `deviceId` peut être absent si [!DNL Target] n’est pas parvenu à le récupérer dans le serveur Edge. |
| type | Chaîne | **Artefact de prise de décision sur l’appareil réussi**<p>Constante :<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>Valeur de chaîne : `artifactDownloadSucceeded`<p>Description : appelé lorsque l’artefact de prise de décision sur l’appareil est téléchargé avec succès.<p>**Échec de l’artefact de prise de décision sur l’appareil**<p>Constante : `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>Valeur de chaîne : `artifactDownloadFailed`<p>Description : appelé lorsque le téléchargement de l’artefact de prise de décision sur l’appareil a échoué. |

## Utilisation

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## Vidéo de formation : jetons de réponse et événements personnalisés at.js ![Badge du tutoriel](../../../assets/tutorial.png)

Regardez la vidéo suivante pour découvrir comment utiliser les jetons de réponse et les événements personnalisés at.js pour partager des informations de profil de [!DNL Target] vers des systèmes tiers.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)


