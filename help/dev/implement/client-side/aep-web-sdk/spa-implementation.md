---
title: Implémentation d’applications d’une seule page pour [!DNL Adobe Experience Platform Web SDK]
description: Découvrez comment créer une implémentation d’application sur une seule page (SPA) de l’ [!DNL Adobe Experience Platform Web SDK]using [!DNL Target].
keywords: target;adobe target;vues xdm;vues;applications monopages;SPA;cycle de vie SPA;côté client;AB testing;AB;Ciblage d’expérience;XT;VEC
feature: AEP Web SDK
exl-id: 17e71e47-c7cc-421a-bc9c-53f45f587449
TQID: https://experienceleague.adobe.com/Kp5fxEhLaXUNi6GOXXnET-1ueGQVLC0tPFhYzShk0cQ
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1836
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
* Une seule ligne de code et une configuration de développeur unique permettent aux marketeurs de créer et d’exécuter des activités [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] (XT) via le [!UICONTROL Compositeur d’expérience visuelle] (VEC) sur votre SPA.

## Vues XDM et applications d’une seule page

Le VEC  pour SPA tire parti d’un concept appelé [!UICONTROL Vues] : un groupe logique d’éléments visuels qui constituent ensemble une expérience SPA. Une application d’une seule page peut donc être considérée comme une transition par vues, au lieu d’URL, en fonction des interactions utilisateur. Une [!UICONTROL Vue] peut généralement représenter l’ensemble d’un site ou des éléments visuels regroupés au sein d’un site.

Pour mieux expliquer ce que sont les vues, l’exemple suivant utilise un hypothétique site d’e-commerce en ligne implémenté dans [!DNL React] pour explorer des exemples [!UICONTROL vues].

Après avoir accédé au site d&#39;accueil, une image de héros promeut une vente de Pâques ainsi que les nouveaux produits disponibles sur le site. Dans ce cas, une [!UICONTROL Vue] peut être définie pour l’ensemble de l’écran d’accueil. Cette [!UICONTROL vue] pourrait simplement s’appeler « maison ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

À mesure que le client s&#39;intéresse davantage aux produits que l&#39;entreprise vend, il décide de cliquer sur le lien **Produits**. Tout comme le site d’accueil, l’intégralité du site des produits peut être définie comme une [!UICONTROL Vue]. Cette [!UICONTROL vue] pourrait s’appeler « products-all ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, avec tous les produits affichés.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Étant donné qu&#39;une [!UICONTROL Vue] peut être définie comme un site entier ou un groupe d&#39;éléments visuels sur un site. Les quatre produits affichés sur le site des produits peuvent être regroupés et considérés comme une [!UICONTROL Vue]. Cette vue peut être nommée « produits ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, avec des exemples de produits affichés.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Lorsque le client décide de cliquer sur le bouton **Charger plus** pour explorer d’autres produits sur le site, l’URL du site web ne change pas dans ce cas. Cependant, une [!UICONTROL Vue] peut être créée ici pour représenter uniquement la deuxième ligne de produits qui s’affiche. Le nom [!UICONTROL Vue] peut être « products-page-2 ».

![Exemple d’image d’une application monopage dans une fenêtre de navigateur, avec des exemples de produits affichés sur une page supplémentaire.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

Le client décide d&#39;acheter quelques produits sur le site et passe à l&#39;écran de passage en caisse. Sur le site de passage en caisse, le client a la possibilité de choisir entre une livraison normale ou une livraison express. Un [!UICONTROL Affichage] peut être n’importe quel groupe d’éléments visuels sur un site. Par conséquent, un [!UICONTROL Affichage] peut être créé pour les préférences de diffusion et appelé « Préférences de diffusion ».

![Exemple d’image d’une page de passage en caisse d’application monopage dans une fenêtre de navigateur.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

Le concept de [!UICONTROL Vues] peut être étendu bien au-delà de ce scénario. Ces scénarios ne sont que quelques exemples de [!UICONTROL vues] qui peuvent être définies sur un site.

## Implémentation [!UICONTROL vues XDM]

[!UICONTROL Les vues XDM] peuvent être utilisées dans [!DNL Target] pour permettre aux spécialistes du marketing d’exécuter des tests A/B et XT sur des SPA via le [!UICONTROL compositeur d’expérience visuelle]. Pour ce faire, les étapes suivantes doivent être effectuées afin de terminer une configuration de développeur ponctuelle :

1. Installez [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Déterminez toutes les [!UICONTROL vues XDM] de votre application monopage que vous souhaitez personnaliser.
3. Après avoir défini les [!UICONTROL vues XDM], pour diffuser des activités A/B ou XT VEC, implémentez la fonction `sendEvent()` avec `renderDecisions` définie sur `true` et la [!UICONTROL vue XDM] correspondante dans votre application d’une seule page. La [!UICONTROL vue XDM] doit être transmise en `xdm.web.webPageDetails.viewName`. Cette étape permet aux professionnels du marketing de tirer parti du [!UICONTROL compositeur d’expérience visuelle] pour lancer des tests A/B et XT pour ces XDM.

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
>Lors du premier appel `sendEvent()`, toutes les [!UICONTROL vues XDM] qui doivent être rendues à l’utilisateur final sont récupérées et mises en cache. Les appels `sendEvent()` suivants transmis avec les vues [!UICONTROL XDM] sont lus à partir du cache et rendus sans appel au serveur.

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

Pour personnaliser le contenu du site en fonction de la préférence de diffusion sélectionnée, vous pouvez créer une [!UICONTROL Vue] pour chaque préférence de diffusion. Lorsque **Diffusion normale** est sélectionné, le [!UICONTROL Affichage] peut être nommé « passage en caisse normal ». Si **Diffusion express** est sélectionné, le [!UICONTROL Affichage] peut être nommé « passage en caisse express ».

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

## Utilisation du [!UICONTROL compositeur d’expérience visuelle] pour une SPA

Une fois que vous avez défini vos [!UICONTROL vues XDM] et implémenté `sendEvent()` avec ces [!UICONTROL vues XDM] transmises, le compositeur d’expérience visuelle est en mesure de détecter ces [!UICONTROL vues] et de permettre aux utilisateurs de créer des actions et des modifications pour les activités A/B ou XT.

>[!NOTE]
>
>Pour utiliser le VEC pour votre SPA, vous devez installer et activer l’extension d’assistance du VEC [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension).

### Panneau [!UICONTROL Modifications]

Le panneau [!UICONTROL Modifications] capture les actions créées pour une [!UICONTROL Vue] spécifique. Toutes les actions d’une [!UICONTROL Vue] sont regroupées sous cette [!UICONTROL Vue].

### Actions

Cliquez sur une action pour mettre en surbrillance l’élément sur le site où cette action est appliquée. Chaque action du compositeur d’expérience visuelle créée sous une [!UICONTROL Vue] comporte les icônes suivantes : **Informations**, **Modifier**, **Cloner**, **Déplacer** et **Supprimer**. Ces icônes sont expliquées plus en détail dans le tableau ci-dessous.

| Icône | Description |
|---|---|
| Informations | Affiche les détails de cette action. |
| Modifier | Permet de modifier directement les propriétés de cette action. |
| Dupliquer | Clonez l’action sur une ou plusieurs [!UICONTROL Vues] qui existent dans le panneau [!UICONTROL Modifications] ou sur une ou plusieurs [!UICONTROL Vues] que vous avez parcourues et auxquelles vous avez accédé dans le compositeur d’expérience visuelle. L’action n’a pas nécessairement à exister dans le panneau [!UICONTROL Modifications].<br/><br/>**Remarque :** une fois l’opération de clonage effectuée, vous devez accéder à la [!UICONTROL Vue] dans le VEC via [!UICONTROL Parcourir] pour voir si l’action clonée était une opération valide. Si l’action ne peut pas être appliquée à la [!UICONTROL Vue], une erreur s’affiche. |
| Déplacer | Déplace l’action vers un [!UICONTROL Événement de chargement de page] ou tout autre [!UICONTROL Vue] existant déjà dans le panneau [!UICONTROL Modifications].<br/><br/>**Événement de chargement de page :** toutes les actions correspondant à l’événement de chargement de page sont appliquées au chargement initial de la page de votre application web. <br/><br/>**Remarque :** une fois une opération de déplacement effectuée, vous devez accéder à la [!UICONTROL Vue] dans le compositeur d’expérience visuelle via [!UICONTROL Parcourir] pour vérifier si le déplacement était une opération valide. Si l’action ne peut pas être appliquée à la [!UICONTROL Vue], une erreur s’affiche. |
| Supprimer | Supprime l’action. |

## Utilisation du compositeur d’expérience visuelle (VEC) pour les SPA

Cette section présente trois exemples d’utilisation du [!UICONTROL compositeur d’expérience visuelle] pour créer des actions et des modifications pour les activités A/B ou XT.

### Exemple 1 : mise à jour de la vue « accueil »

Plus tôt dans cet article, une [!UICONTROL Vue] nommée « accueil » a été définie pour l’ensemble du site d’accueil. L’équipe marketing souhaite maintenant mettre à jour la vue d’accueil des manières suivantes :

* Remplacez les boutons **Ajouter au panier** et **Comme** par une teinte bleue plus claire. Cette modification doit se produire lors du chargement de la page, car elle implique de modifier les composants de l’en-tête .
* Remplacez le libellé **Derniers produits pour 2026** par **Produits les plus chauds pour 2026** et modifiez la couleur du texte en violet.

Pour effectuer ces mises à jour dans le compositeur d’expérience visuelle, sélectionnez **Composer** et appliquez ces modifications à la vue « accueil ».

![Exemple de page du compositeur d’expérience visuelle.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Exemple 2 : modification des libellés de produit

Pour l’[!UICONTROL Affichage] « products-page-2 », l’équipe marketing souhaite remplacer le libellé **Prix** par **Prix de vente** et modifier la couleur du libellé en rouge.

Pour effectuer ces mises à jour dans le VEC, les étapes suivantes sont requises :

1. Sélectionnez **Parcourir** dans le VEC.
2. Sélectionnez **Produits** dans la barre de navigation supérieure du site.
3. Sélectionnez **Charger plus** une fois pour afficher la deuxième ligne de produits.
4. Sélectionnez **Composer** dans le VEC.
5. Appliquez des actions pour modifier le libellé de texte en **Prix de vente** et la couleur en rouge.

![Exemple de page du compositeur d’expérience visuelle avec des libellés de produit.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Exemple 3 : personnalisation du style des préférences de diffusion

Les [!UICONTROL vues] peuvent être définies à un niveau granulaire, par exemple un état ou une option d’un bouton radio. Plus tôt dans cet article [!UICONTROL Vues] ont été définies pour les préférences de diffusion : « checkout-normal » et « checkout-express ». L’équipe marketing souhaite modifier la couleur du bouton en rouge pour la vue « passage en caisse express ».

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
>Le bouton radio « passage en caisse express » [!UICONTROL Affichage] n’apparaît pas dans le panneau [!UICONTROL Modifications] tant que le bouton radio **Diffusion express** n’est pas sélectionné. Cela est dû au fait que la fonction `sendEvent()` est exécutée lorsque le bouton radio **Diffusion express** est sélectionné. Par conséquent, le compositeur d’expérience visuelle ne prend pas en compte le bouton « passage en caisse express » [!UICONTROL Affichage] tant que le bouton radio n’est pas sélectionné.

![Compositeur d’expérience visuelle affichant le sélecteur des préférences de diffusion.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
