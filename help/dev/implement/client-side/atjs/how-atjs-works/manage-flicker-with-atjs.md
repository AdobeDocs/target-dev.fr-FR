---
keywords: scintillement, at.js, implémentation, asynchrone, asynchrone, synchrone, synchrone, 8 $
description: Découvrez comment at.js et  [!DNL Target]  empêchent le scintillement (le contenu par défaut s’affiche momentanément avant d’être remplacé par le contenu de l’activité) au chargement de la page ou de l’application.
title: Comment at.js gère-t-il le scintillement ?
feature: at.js
exl-id: 8aacf254-ec3d-4831-89bb-db7f163b3869
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 57%

---

# Gestion du scintillement par at.js

Informations sur la façon dont la bibliothèque JavaScript at.js [!DNL Adobe Target] empêche le scintillement lors du chargement de la page ou de l’application.

Il y a scintillement lorsque du contenu par défaut est présenté temporairement aux visiteurs avant d’être remplacé par le contenu de l’activité. Ce phénomène peut déstabiliser les visiteurs et doit donc être évité.

## Utilisation d’une mbox globale créée automatiquement

Lorsque vous activez la [Création automatique d’une Mbox globale](/help/dev/implement/client-side/atjs/global-mbox/customize-global-mbox.md) lors de la configuration d’at.js, ce dernier gère le scintillement en modifiant le paramètre d’opacité au chargement de la page. Au chargement d’at.js, le paramètre d’opacité de l’élément `<body>` est remplacé par &quot;0&quot;, ce qui rend la page initialement invisible pour les visiteurs. Après réception d’une réponse de [!DNL Target], ou si une erreur avec la requête [!DNL Target] est détectée, at.js réinitialise l’opacité sur &quot;1&quot;. Ainsi, le visiteur ne voit la page qu’une fois le contenu de vos activités appliqué.

Si vous activez le paramètre lors de la configuration de at.js, at.js définit l’opacité du style HTML BODY sur 0. Après réception d’une réponse de [!DNL Target], at.js réinitialise l’opacité de l’HTML BODY sur 1.

L’opacité définie sur 0 conserve le contenu de la page masqué pour empêcher le scintillement, mais le navigateur effectue toujours le rendu de la page et charge tous les éléments nécessaires tels que CSS, les images, etc.

Si `opacity: 0` ne fonctionne pas dans votre implémentation, vous pouvez également gérer le scintillement en personnalisant `bodyHiddenStyle` et en le définissant sur `body {visibility:hidden !important}`. Vous pouvez utiliser `body {opacity:0 !important}` ou `body {visibility:hidden !important}`, selon ce qui fonctionne le mieux dans votre situation spécifique.

L’illustration suivante présente les appels à Masquer/Afficher le corps dans at.js 1.*x* et at.js 2.x.

**at.js 2.x**

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![ Flux cible : requête de chargement de page at.js](/help/dev/implement/client-side/assets/atjs-20-flow-page-load-request.png "Flux cible : requête de chargement de page at.js"){zoomable="yes"}

**at.js 1.*x***

(Cliquez sur l’image pour agrandir l’image en largeur réelle.)

![ Flux cible : flux cible créé automatiquement : flux cible créé automatiquement : mbox globale créée automatiquement "){zoomable="yes"}] (/help/dev/implement/client-side/atjs/how-atjs-works/assets/target-flow2.png "

Pour plus d’informations sur le remplacement de `bodyHiddenStyle`, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Gestion du scintillement lors du chargement asynchrone du fichier at.js

Le chargement d’at.js de manière asynchrone est un excellent moyen d’éviter de bloquer le rendu du navigateur. Cependant, cette technique peut entraîner un scintillement de la page web.

Vous pouvez éviter le scintillement en utilisant un fragment de code de pré-masquage qui sera visible une fois les éléments d’HTML pertinents personnalisés par Target.

at.js peut être chargé de manière asynchrone, soit directement incorporé sur la page, soit via un gestionnaire de balises (Adobe Experience Platform Launch, par exemple).

Si at.js est incorporé à la page, le fragment de code doit être ajouté avant de charger at.js. Si vous chargez at.js via un gestionnaire de balises, qui est également chargé de manière asynchrone, vous devez ajouter le fragment de code avant de charger le gestionnaire de balises. Si le gestionnaire de balises est chargé de manière synchrone, le script peut être inclus dans le gestionnaire de balises avant at.js.

Le fragment de code de pré-masquage se présente comme suit :

```
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Par défaut, le fragment de code masque préalablement l’ensemble HTML BODY. Dans certains cas, vous souhaitez uniquement masquer préalablement certains éléments HTML et non la totalité de la page. Vous pouvez y parvenir en personnalisant le paramètre de style. Il peut être remplacé par un élément qui masque préalablement seulement des régions spécifiques de la page.

Par exemple, vous disposez de deux régions identifiées par les ID container-1 et container-2, alors le style peut être remplacé par ce qui suit :

```
#container-1, #container-2 {opacity: 0 !important}
```

Au lieu de la valeur par défaut :

```
body {opacity: 0 !important}
```

## Gestion du scintillement dans at.js 2.x pour triggerView()

Lorsque vous utilisez `triggerView()` pour afficher du contenu ciblé dans votre SPA, la gestion du scintillement est fournie en dehors de la zone. Cela signifie que la logique de pré-masquage ne doit pas être ajoutée manuellement. À la place, at.js 2.x pré-masque l’emplacement de votre vue avant d’appliquer le contenu ciblé.

## Gestion du scintillement avec getOffer() et applyOffer()

Comme `getOffer()` et `applyOffer()` sont des API de bas niveau, il n’y a aucun contrôle de scintillement intégré. Vous pouvez transmettre un sélecteur ou un élément HTML sous la forme d’une option à `applyOffer()`. Dans ce cas, `applyOffer()` ajoute le contenu de l’activité à cet élément spécifique. Veillez toutefois à ce que l’élément soit correctement pré-masqué avant d’appeler `getOffer()` et `applyOffer()`.

```
document.documentElement.style.opacity = "0";
 
adobe.target.getOffer({
    mbox: 'target-global-mbox',
    success: function(offer) {
        adobe.target.applyOffer({
            mbox: 'target-global-mbox',
            offer: offer
        });
 
        document.documentElement.style.opacity = "1";
    },
    error: function() {
        document.documentElement.style.opacity = "1";        
    }
});
```

## Utilisation d’une mbox régionale avec mboxCreate() dans at.js 1.x (non pris en charge dans at.js 2.x)

Si vous utilisez une implémentation de mbox régionale, vous pouvez utiliser `mboxCreate()` avec votre page configurée comme suit :

```
<div class="mboxDefault">
Some default content
</div>
<script>
mboxCreate('some-mbox');
</script>
```

Si vos pages sont correctement configurées, at.js gère le scintillement en activant/désactivant, suivant les besoins, la propriété de « visibilité » CSS de l’élément avec la classe mboxDefault.
