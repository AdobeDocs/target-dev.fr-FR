---
title: Implémentation d’applications d’une seule page pour [!DNL Adobe Experience Platform Web SDK]
description: Découvrez comment créer une implémentation d’application sur une seule page (SPA) de l’ [!DNL Adobe Experience Platform Web SDK]using [!DNL Target].
keywords: target;adobe target;vues xdm;vues;applications monopages;SPA;cycle de vie SPA;côté client;AB testing;AB;Ciblage d’expérience;XT;VEC
feature: AEP Web SDK
source-git-commit: 9a2c35b2d150638fbda00be866f84d2a6faa4300
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 2%

---


# Implémentation d’applications d’une seule page

[!DNL Adobe Experience Platform Web SDK] fournit des fonctionnalités riches qui permettent à votre entreprise d’exécuter de la personnalisation sur des technologies côté client de nouvelle génération, telles que les applications d’une seule page (SPA).

Les sites web traditionnels utilisaient des modèles de navigation « page à page », également appelés applications multi-pages. Dans ces sites web, les conceptions sont étroitement liées aux URL et le déplacement entre les pages nécessite un chargement complet de la page.

Les applications web modernes, telles que les applications d’une seule page, ont plutôt adopté un modèle qui propulse l’utilisation rapide du rendu de l’interface utilisateur du navigateur, qui est souvent indépendant des rechargements de page. Ces expériences sont déclenchées par les interactions des clients, telles que les défilements, les clics et les mouvements de curseur. À mesure que les paradigmes du web moderne ont évolué, la pertinence des événements génériques traditionnels, tels que le chargement d’une page, pour déployer la personnalisation et l’expérimentation ne fonctionne plus.

![Diagramme présentant le cycle de vie des SPA par rapport au cycle de vie traditionnel des pages.](/help/dev/implement/client-side/aep-web-sdk/assets/spa-vs-traditional-lifecycle.png)

## Avantages de la [!DNL Experience Platform Web SDK] pour les SPA

Voici quelques avantages liés à l’utilisation de [!DNL Adobe Experience Platform Web SDK] pour vos applications monopages :

* Capacité à mettre en cache toutes les offres au chargement de la page afin de passer de plusieurs appels serveur à un seul appel serveur.
* Améliorez l’expérience utilisateur sur votre site, car les offres sont affichées immédiatement via le cache sans le délai introduit par les appels au serveur traditionnels.
* Une seule ligne de code et une configuration de développeur unique permettent aux marketeurs de créer et d’exécuter des activités de [!UICONTROL A/B Test] et de [!UICONTROL Experience Targeting] (XT) via le [!UICONTROL Visual Experience Composer] (VEC) sur votre SPA.

## Vues XDM et applications d’une seule page

Le compositeur d’expérience visuelle [!UICONTROL Adobe Target] pour les SPA tire parti d’un concept appelé [!UICONTROL Views] : un groupe logique d’éléments visuels qui constituent ensemble une expérience SPA. Une application d’une seule page peut donc être considérée comme une transition par vues, au lieu d’URL, en fonction des interactions utilisateur. Un [!UICONTROL View] peut généralement représenter l’ensemble d’un site ou des éléments visuels regroupés au sein d’un site.

Pour mieux expliquer ce que sont les vues, l’exemple suivant utilise un hypothétique site d’e-commerce en ligne implémenté dans [!DNL React] pour explorer des exemples de [!UICONTROL Views].

Après avoir accédé au site d&#39;accueil, une image de héros promeut une vente de Pâques ainsi que les nouveaux produits disponibles sur le site. Dans ce cas, une [!UICONTROL View] peut être définie pour l’ensemble de l’écran d’accueil. Ce [!UICONTROL View] pourrait simplement s&#39;appeler « chez soi ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

À mesure que le client s&#39;intéresse davantage aux produits que l&#39;entreprise vend, il décide de cliquer sur le lien **Produits**. Tout comme le site d’accueil , l’intégralité du site produits peut être définie comme un [!UICONTROL View]. Ce [!UICONTROL View] pourrait être nommé « products-all ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, avec tous les produits affichés.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Puisqu’un [!UICONTROL View] peut être défini comme un site entier ou un groupe d’éléments visuels sur un site. Les quatre produits présentés sur le site des produits pourraient être regroupés et considérés comme des [!UICONTROL View]. Cette vue peut être nommée « produits ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, avec des exemples de produits affichés.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Lorsque le client décide de cliquer sur le bouton **Charger plus** pour explorer d’autres produits sur le site, l’URL du site web ne change pas dans ce cas. Cependant, un [!UICONTROL View] peut être créé ici pour représenter uniquement la deuxième ligne de produits qui s’affiche. Le nom du [!UICONTROL View] peut être « products-page-2 ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, avec des exemples de produits affichés sur une page supplémentaire.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

Le client décide d&#39;acheter quelques produits sur le site et passe à l&#39;écran de passage en caisse. Sur le site de passage en caisse, le client a la possibilité de choisir entre une livraison normale ou une livraison express. Un [!UICONTROL View] peut être n’importe quel groupe d’éléments visuels sur un site. Par conséquent, un [!UICONTROL View] peut être créé pour les préférences de diffusion et appelé « Préférences de diffusion ».

![Exemple d’image d’une page de passage en caisse d’application monopage dans une fenêtre de navigateur.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

Le concept de [!UICONTROL Views] peut être étendu bien au-delà de ce scénario. Ces scénarios ne sont que quelques exemples de [!UICONTROL Views] qui peuvent être définis sur un site.

## [!UICONTROL XDM Views] d’implémentation

[!UICONTROL XDM Views] peut être utilisé dans [!DNL Target] pour permettre aux marketeurs d’exécuter des tests A/B et XT sur des SPA via [!UICONTROL Visual Experience Composer]. Pour ce faire, les étapes suivantes doivent être effectuées afin de terminer une configuration de développeur ponctuelle :

1. Installez [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Déterminez toutes les [!UICONTROL XDM Views] de votre application monopage que vous souhaitez personnaliser.
3. Après avoir défini la [!UICONTROL XDM Views], pour diffuser des activités A/B ou XT VEC, implémentez la fonction `sendEvent()` avec `renderDecisions` définie sur `true` et la [!UICONTROL XDM View] correspondante dans votre application d’une seule page. Le [!UICONTROL XDM View] doit être transmis en `xdm.web.webPageDetails.viewName`. Cette étape permet aux spécialistes du marketing d’exploiter le [!UICONTROL Visual Experience Composer] pour lancer des tests A/B et XT pour ces XDM.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>Lors du premier appel `sendEvent()`, toutes les [!UICONTROL XDM Views] qui doivent être rendues à l’utilisateur final sont récupérées et mises en cache. Les appels `sendEvent()` suivants avec [!UICONTROL XDM Views] transmis sont lus à partir du cache et rendus sans appel au serveur.

## Exemples de fonctions `sendEvent()`

Cette section présente trois exemples montrant comment appeler la fonction `sendEvent()` dans React pour une hypothétique SPA d’e-commerce.

### Exemple 1 : page d’accueil du test A/B

L’équipe marketing souhaite exécuter des tests A/B sur l’ensemble de la page d’accueil.

![Exemple d’image d’une application monopage dans une fenêtre de navigateur.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-1.png)

Pour exécuter des tests A/B sur l’ensemble du site d’accueil, `sendEvent()` devez être appelé avec le `viewName` XDM défini sur `home` :

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Exemple 2 : produits personnalisés

L’équipe marketing souhaite personnaliser la deuxième ligne de produits en modifiant la couleur du libellé de prix en rouge après qu’un utilisateur ou une utilisatrice clique sur **Charger plus**.

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, affichant des offres personnalisées.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Exemple 3 : préférences de diffusion des tests A/B

L’équipe marketing souhaite effectuer un test A/B pour voir si la couleur du bouton qui passe du bleu au rouge lorsque l’option **Diffusion express** est sélectionnée. L&#39;équipe pense que cette modification peut augmenter les conversions (plutôt que de garder la couleur bleue du bouton pour les deux options de diffusion).

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, avec test A/B.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-3.png)

Pour personnaliser le contenu du site en fonction de la préférence de diffusion sélectionnée, vous pouvez créer un [!UICONTROL View] pour chaque préférence de diffusion. Lorsque l’option **Diffusion normale** est sélectionnée, le [!UICONTROL View] peut être nommé « passage en caisse normal ». Si l’option **Diffusion express** est sélectionnée, le [!UICONTROL View] peut être nommé « passage en caisse express ».

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Utilisation de l’[!UICONTROL Visual Experience Composer] pour une SPA

Une fois la définition de vos [!UICONTROL XDM Views] et les `sendEvent()` implémentées avec celles [!UICONTROL XDM Views] transmises, le compositeur d’expérience visuelle peut détecter ces [!UICONTROL Views] et permettre aux utilisateurs de créer des actions et des modifications pour les activités A/B ou XT.

>[!NOTE]
>
>Pour utiliser le VEC pour votre SPA, vous devez installer et activer l’extension d’assistance du VEC [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension).

### panneau [!UICONTROL Modifications]

Le panneau [!UICONTROL Modifications] capture les actions créées pour une [!UICONTROL View] spécifique. Toutes les actions d’une [!UICONTROL View] sont regroupées sous cette [!UICONTROL View].

### Actions

Cliquez sur une action pour mettre en surbrillance l’élément sur le site où cette action est appliquée. Chaque action du compositeur d’expérience visuelle créée sous un [!UICONTROL View] possède les icônes suivantes : **Informations**, **Modifier**, **Cloner**, **Déplacer** et **Supprimer**. Ces icônes sont expliquées plus en détail dans le tableau ci-dessous.

| Icône | Description |
|---|---|
| Informations | Affiche les détails de cette action. |
| Modifier | Permet de modifier directement les propriétés de cette action. |
| Dupliquer | Clonez l’action sur une ou plusieurs [!UICONTROL Views] qui existent dans le panneau de [!UICONTROL Modifications] ou sur une ou plusieurs [!UICONTROL Views] que vous avez parcourues et auxquelles vous avez accédé dans le compositeur d’expérience visuelle. L’action n’a pas nécessairement à exister dans le panneau [!UICONTROL Modifications].<br/><br/>**Remarque :** une fois une opération de clonage effectuée, vous devez accéder au [!UICONTROL View] dans le VEC via [!UICONTROL Browse] pour voir si l’action clonée était une opération valide. Si l’action ne peut pas être appliquée au [!UICONTROL View], une erreur s’affiche. |
| Déplacer | Déplace l’action vers un [!UICONTROL Page Load Event] ou tout autre [!UICONTROL View] existant déjà dans le panneau [!UICONTROL Modifications].<br/><br/>**Événement de chargement de page :** toutes les actions correspondant à l’événement de chargement de page sont appliquées au chargement initial de la page de votre application web. <br/><br/>**Remarque :** une fois l’opération de déplacement effectuée, vous devez accéder au [!UICONTROL View] dans le compositeur d’expérience visuelle via [!UICONTROL Browse] pour vérifier si le déplacement était une opération valide. Si l’action ne peut pas être appliquée au [!UICONTROL View], une erreur s’affiche. |
| Supprimer | Supprime l’action. |

## Utilisation du compositeur d’expérience visuelle (VEC) pour les SPA

Cette section présente trois exemples d’utilisation de l’[!UICONTROL Visual Experience Composer] pour créer des actions et des modifications pour les activités A/B ou XT.

### Exemple 1 : mise à jour de la vue « accueil »

Plus tôt dans cet article, un [!UICONTROL View] nommé « home » a été défini pour l’ensemble du site d’accueil. L’équipe marketing souhaite maintenant mettre à jour la vue d’accueil des manières suivantes :

* Remplacez les boutons **Ajouter au panier** et **Comme** par une teinte bleue plus claire. Cette modification doit se produire lors du chargement de la page, car elle implique de modifier les composants de l’en-tête .
* Remplacez le libellé **Derniers produits pour 2026** par **Produits les plus chauds pour 2026** et modifiez la couleur du texte en violet.

Pour effectuer ces mises à jour dans le compositeur d’expérience visuelle, sélectionnez **Composer** et appliquez ces modifications à la vue « accueil ».

![Exemple de page du compositeur d’expérience visuelle.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Exemple 2 : modification des libellés de produit

Pour l’[!UICONTROL View] « products-page-2 », l’équipe marketing souhaite remplacer le libellé **Price** par **Prix de vente** et modifier la couleur du libellé en rouge.

Pour effectuer ces mises à jour dans le VEC, les étapes suivantes sont requises :

1. Sélectionnez **Parcourir** dans le VEC.
2. Sélectionnez **Produits** dans la barre de navigation supérieure du site.
3. Sélectionnez **Charger plus** une fois pour afficher la deuxième ligne de produits.
4. Sélectionnez **Composer** dans le VEC.
5. Appliquez des actions pour modifier le libellé de texte en **Prix de vente** et la couleur en rouge.

![Exemple de page du compositeur d’expérience visuelle avec des libellés de produit.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Exemple 3 : personnalisation du style des préférences de diffusion

[!UICONTROL Views] peut être défini à un niveau granulaire, comme un état ou une option d’un bouton radio. Plus tôt dans cet article, [!UICONTROL Views] ont été définis pour les préférences de diffusion, « checkout-normal » et « checkout-express ». L’équipe marketing souhaite modifier la couleur du bouton en rouge pour la vue « passage en caisse express ».

Pour effectuer ces mises à jour dans le VEC, les étapes suivantes sont requises :

1. Sélectionnez **Parcourir** dans le VEC.
2. Ajouter des produits au panier sur le site.
3. Sélectionnez l’icône du panier dans le coin supérieur droit du site.
4. Sélectionnez **Extraire votre commande**.
5. Sélectionnez le bouton radio **Diffusion express** sous **Préférences de diffusion**.
6. Sélectionnez **Composer** dans le VEC.
7. Remplacez la couleur du bouton **Pay** par le rouge.

>[!NOTE]
>
>Le [!UICONTROL View] « checkout-express » n’apparaît pas dans le panneau [!UICONTROL Modifications] tant que le bouton radio **Diffusion express** n’est pas sélectionné. Cela est dû au fait que la fonction `sendEvent()` est exécutée lorsque le bouton radio **Diffusion express** est sélectionné. Par conséquent, le compositeur d’expérience visuelle ne prend pas en compte le [!UICONTROL View] « checkout-express » tant que le bouton radio n’est pas sélectionné.

![Compositeur d’expérience visuelle affichant le sélecteur des préférences de diffusion.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
