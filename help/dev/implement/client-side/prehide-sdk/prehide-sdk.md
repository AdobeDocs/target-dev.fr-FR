---
keywords: prémasquer SDK, scintillement, anti-scintillement, prémasquage, pré-masquage, alliage, at.js, implémentation, consentement, CMP, placement de script, en ligne, externe, sélection SDK
description: Découvrez comment intégrer la fonction  [!DNL Adobe Target] Prehide SDK pour éliminer le flash de contenu non personnalisé (scintillement) lors du chargement de la page. Le SDK fonctionne avec Adobe Alloy (Web SDK) et at.js.
title: Aperçu du guide d’intégration de SDK
feature: Implementation
hide: true
source-git-commit: 2f7a53b667990474dfab7ca66a8ea93d2e946548
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Prévisualisation du guide d’intégration de SDK

Une minuscule bibliothèque JavaScript synchrone qui empêche le scintillement visuel provoqué par [!DNL Adobe Target] personnalisation réécrivant une page en cours de rendu. Ajoutez une balise de `<script>` intégrée en haut de l’`<head>` pour que la page s’affiche uniquement lorsque le contenu personnalisé est prêt ou que le minuteur de sécurité se déclenche.

## Étapes d’intégration {#integration-steps}

1. Téléchargez le lot.

   Utilisez l’interface utilisateur de Scintillement Manager pour télécharger `prehide.min.js`. Le fichier est préconfiguré avec votre code client et le délai d’expiration de la protection. Aucun bloc de `PrehideConfig` n’est donc nécessaire.

1. Insérez-le en ligne tout en haut de la `<head>`.

   Collez le contenu de `prehide.min.js` directement à l’intérieur d’une balise `<script>` intégrée en tant que premier enfant de `<head>`. Voir [Intégré ou externe](#inline-vs-external) pour connaître les raisons pour lesquelles la mise en ligne est préférable.

   ```html
   <!-- 1. Prehide SDK: must be FIRST in <head> and BEFORE any Adobe SDK -->
   <script>
     // paste the contents of prehide.min.js here
   </script>
   
   <!-- 2. Then load Alloy.js OR at.js -->
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Facultatif) Ajoutez un bloc de configuration d’exécution.

   Obligatoire uniquement si vous auto-hébergez le lot sans le télécharger via l’interface utilisateur ou si vous devez remplacer le choix SDK. Placez le bloc de configuration avant le script de prévisualisation :

   ```html
   <script>
     window.PrehideConfig = {
       sdk: "alloy"            // or "atjs" (defaults to "alloy")
     };
   </script>
   <script> /* prehide.min.js inline contents */ </script>
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Facultatif) Congédiez le consentement.

   Si votre mise en œuvre utilise une plateforme de gestion du consentement (CMP), appelez le `window.Prehide.setConsent(...)` dès que l’état du consentement est connu. Voir [&#x200B; Gestion du consentement &#x200B;](#consent-management).

1. Vérifiez.

   Ouvrez DevTools et vérifiez que `<style id="alloy-prehiding">` (ou `at-body-style` pour at.js) apparaît dans `<head>` sur la première peinture et est supprimé une fois le SDK terminé. Exécutez `window.Prehide.getState()` dans la console pour inspecter l’état d’exécution.

## Où placer le script {#script-placement}

>[!IMPORTANT]
>
>Le SDK de prévisualisation doit s’exécuter avant Alloy/at.js. Si Alloy se charge en premier, la page affiche du contenu non personnalisé, puis effectue un nouveau rendu. C’est exactement le scintillement que ce SDK est conçu pour éviter.
></br>>N’ajoutez pas de `async` ni de `defer` à la balise de script Prehide SDK. Une exécution synchrone est requise afin que la règle de masquage soit injectée avant que le navigateur ne commence à afficher la page.

Le SDK de prémasquage doit apparaître plus tôt dans le document que le SDK de [!DNL Adobe Target] qui le supprime. L&#39;ordre de chargement est non négociable :

```html
<!doctype html>
<html>
<head>
  <!-- ① Prehide SDK FIRST. Inline. Synchronous. No async/defer. -->
  <script> /* prehide.min.js inline contents */ </script>

  <!-- ② Alloy or at.js loads next -->
  <script src="https://cdn.alloy.adobe.com/alloy.min.js"></script>

  <!-- ③ Then everything else: meta, css, third-party tags, ... -->
  <link rel="stylesheet" href="main.css">
</head>
<body> ... your page ... </body>
</html>
```

## Inline ou externe {#inline-vs-external}

Il existe deux manières d’inclure `prehide.min.js` :

| Méthode | Exemple | Remarques |
| --- | --- | --- |
| En ligne (préféré) | `<script>/* full contents of prehide.min.js pasted directly into the page */</script>` | Zéro aller-retour réseau. Le SDK s’exécute avant tout autre rendu. |
| Externe (uniquement si la mise en ligne est impossible) | `<script src="/static/prehide.min.js"></script>` | Introduit une requête réseau de blocage avant le premier rendu. Même avec le HTTP/2 et la mise en cache Edge, cela coûte généralement entre 30 et 80 ms. |

### Pourquoi privilégier la mise en ligne

>[!TIP]
>
>Intégrez le lot directement dans `<script>...</script>` dans votre modèle HTML. Traitez-le comme un bloc CSS critique : petit, en ligne et toujours tout en haut.

* Aucune récupération bloquant le rendu. L’objectif du SDK Prehide est d’injecter des règles de masquage *avant* le premier rendu. Un `<script src>` externe ajoute un aller-retour réseau exactement dans cette fenêtre critique.
* Aucun nouveau mode d’échec. Un fichier externe peut 404, expirer ou être bloqué par un bloqueur de publicités. Une copie en ligne ne le peut pas.
* Le lot est petit (~6 Ko). La mise en ligne coûte moins cher qu’un favicon classique et aucun avantage de mise en cache n’est suffisamment important pour l’emporter sur l’aller-retour supplémentaire au premier rendu.
* Compatible avec le cache. Lorsqu’il est intégré dans la réponse d’HTML, le SDK est mis en cache avec le reste du document par votre couche de mise en cache existante (cache CDN ou HTTP du navigateur).
* Offre groupée spécifique au client. Le fichier téléchargé contient votre code client au moment du téléchargement. La mise en ligne permet de s’assurer que chaque visiteur reçoit le lot personnalisé approprié sans demande supplémentaire.

## Configuration {#configuration}

Le SDK accepte la configuration de deux sources, par ordre de priorité. Il lit ce qui est disponible en premier.

### `window.PrehideConfig` d’exécution (intégration manuelle)

Pour les lots auto-hébergés ou non modifiés, déclarez un objet config avant l’exécution du script de prévisualisation :

```html
<script>
  window.PrehideConfig = {
    sdk: "alloy"             // optional: "alloy" (default) or "atjs"
  };
</script>
```

| Champ | Type | Requis | Description |
| --- | --- | --- | --- |
| `sdk` | `"alloy"` \| `"atjs"` | Non | SDK Adobe chargé sur la page. Voir la sélection [&#128279;](#sdk-selection). |

## SDK selection {#sdk-selection}

[!DNL Adobe Target] propose deux SDK de diffusion : Alloy (le SDK Web moderne) et at.js (la bibliothèque classique). Chaque recherche un élément de `<style>` *différent* `id` une fois la personnalisation terminée et le supprime pour afficher la page. Le SDK Prehide doit injecter la `id` correspondante ; sinon la page reste masquée jusqu’au déclenchement du minuteur de sécurité.

| valeur `sdk` | ID de balise de style injecté | Supprimé par | Quand l’utiliser |
| --- | --- | --- | --- |
| `"alloy"` *(par défaut)* | `<style id="alloy-prehiding">` | Alloy SDK sur personalize-complete | Vous chargez Alloy / Adobe Web SDK sur cette page. |
| `"atjs"` | `<style id="at-body-style">` | at.js sur personalize-complete | Vous chargez la bibliothèque at.js classique sur cette page. |

>[!NOTE]
>
>Pour le SDK at.js, seules les versions 2.x et ultérieures sont prises en charge.

### Comment le définir

```html
<!-- For at.js -->
<script>
  window.PrehideConfig = { sdk: "atjs" };
</script>
<script> /* prehide.min.js inline */ </script>
<script src="https://cdn.adobe.com/.../at.js"></script>
```

>[!WARNING]
>
>Avertissement de non-correspondance. La définition de `sdk: "alloy"` lors du chargement d’at.js (ou inversement) signifie que le SDK ne trouvera pas l’élément de prévisualisation à supprimer. Le minuteur de garde finira par révéler la page, mais les visiteurs verront une fenêtre masquée plus longue. Définissez toujours `sdk` pour correspondre à la bibliothèque que vous chargez.

Les valeurs inconnues ou manquantes reviennent à `"alloy"`, de sorte que les intégrations Alloy existantes continuent à fonctionner sans modification de configuration.

## Gestion du consentement {#consent-management}

>[!NOTE]
>
>* La valeur de consentement n’est jamais stockée sur `window`. Seule la fonction est exposée. L’état interne reste privé pour le SDK.
>* Les transitions de `"out"` à `"in"` ne masquent pas à nouveau la page, car le masquage à nouveau du contenu entièrement rendu entraînerait des perturbations visuelles.
>* `setConsent` peut être appelé plusieurs fois dans une seule page vue. Chaque appel remplace l’état précédent.

Le SDK Prehide comprend une API basée sur le consentement pour se coordonner avec votre CMP. Son utilisation est facultative. Si `setConsent` n’est jamais appelé, le SDK se comporte comme une intégration standard sans consentement.

### Surface API

```js
// Single function call. Pass a status string.
window.Prehide.setConsent("pending");  // banner shown, awaiting decision
window.Prehide.setConsent("in");       // user accepted personalization
window.Prehide.setConsent("out");      // user declined personalization

// Read-only debug snapshot.
window.Prehide.getState();
// → { sdk, version, consentStatus, consentApiUsed,
//      rulesResolved, hasSelectorsToGuard, guardTimeout }
```

### Fonction de chaque statut

| L’appel | Effet sur le minuteur de garde | Effet sur le contenu masqué |
| --- | --- | --- |
| `setConsent("pending")` | Le minuteur actif est effacé. Aucune sécurité ne doit afficher les incendies jusqu&#39;à ce que le consentement soit résolu. | Les sélecteurs restent masqués indéfiniment. |
| `setConsent("in")` | Effacé, puis redémarré avec la temporisation configurée. Attend que les règles soient résolues si elles ne l’ont pas encore fait. | Le contenu reste masqué jusqu’à ce que le SDK se personnalise ou que le minuteur de garde se déclenche. |
| `setConsent("out")` | Effacé. La page est immédiatement affichée. | La page s’affiche immédiatement. Les règles qui sont résolues ultérieurement ne *masquent pas* nouveau le contenu. |
| *(jamais appelé)* | Le minuteur par défaut s’exécute à partir de `init()` pour la durée configurée. | Le contenu reste masqué jusqu’à ce que le SDK se personnalise ou que le minuteur de garde se déclenche. (Mode hérité rétrocompatible.) |

### Modèle recommandé : phase en attente explicite

1. Dès que votre CMP affiche l’interface utilisateur de consentement, appelez `setConsent("pending")`. Cela efface le minuteur de sécurité afin que la page reste masquée pendant que le visiteur se décide, évitant ainsi un flash de contenu non personnalisé derrière la bannière.

   ```js
   window.Prehide.setConsent("pending");
   ```

1. Lorsque le visiteur accepte la personnalisation, appelez `setConsent("in")`. Le minuteur de garde redémarre et Alloy/at.js prend le relais, affichant la page une fois la personnalisation appliquée.

   ```js
   window.Prehide.setConsent("in");
   ```

1. Lorsque le visiteur refuse la personnalisation, appelez `setConsent("out")`. La page apparaît immédiatement et reste visible. Les règles de réseau CDN qui sont résolues ultérieurement ne le masqueront pas à nouveau.

   ```js
   window.Prehide.setConsent("out");
   ```

### Exemple : intégration de style OneTrust

```js
// Called once OneTrust has rendered its banner.
function onOneTrustReady() {
  // Pause the guard timer while the banner is visible.
  window.Prehide.setConsent("pending");

  OneTrust.OnConsentChanged(function (event) {
    if (event.consentedToTargeting) {
      window.Prehide.setConsent("in");
    } else {
      window.Prehide.setConsent("out");
    }
  });
}
```

### Exemple : TCF / style IAB

```js
// Optional: pause the guard while UI is up.
window.Prehide.setConsent("pending");

// Your CMP eventually emits the final TC string.
function onTcData(tcData) {
  const hasTargetConsent = /* derive from tcData */;
  window.Prehide.setConsent(hasTargetConsent ? "in" : "out");
}
```

