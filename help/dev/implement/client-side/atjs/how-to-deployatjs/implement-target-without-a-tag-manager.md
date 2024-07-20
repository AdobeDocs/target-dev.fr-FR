---
keywords: implémentation de target, implémentation, implémentation d’at.js, gestionnaire de balises, prise de décision sur les appareils, sur la prise de décision sur les appareils
description: Découvrez comment spécifier les paramètres (détails du compte, méthodes de mise en oeuvre, etc.) pour mettre en oeuvre la bibliothèque  [!DNL Adobe Target] at.js sans utiliser de gestionnaire de balises.
title: Puis-je implémenter  [!DNL Target] sans gestionnaire de balises ?
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 35%

---

# Mettre en oeuvre [!DNL Target] sans gestionnaire de balises

Informations sur l’implémentation de [!DNL Adobe Target] sans utiliser de gestionnaire de balises ou de balises dans [!DNL Adobe Experience Platform].

>[!NOTE]
>
>Les balises dans [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sont la méthode préférée pour implémenter [!DNL Target] et la bibliothèque at.js. Les informations suivantes ne s’appliquent pas lors de l’utilisation de balises dans [!DNL Adobe Experience Platform] pour implémenter [!DNL Target].

Pour accéder à la page Mise en oeuvre , cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Vous pouvez définir les paramètres suivants sur cette page :

* Détails du compte
* Méthodes de mise en oeuvre
* API de profil
* Outils de débogage
* Confidentialité

>[!NOTE]
>
>Vous pouvez remplacer les paramètres de la bibliothèque at.js au lieu de les configurer dans l’interface utilisateur [!DNL Target] Standard/Premium ou en utilisant des API REST. Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Détails du compte

Vous pouvez afficher les détails du compte suivants. Ces paramètres ne peuvent pas être modifiés.

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Client Code] | Le code client est une séquence de caractères spécifique au client souvent requise lors de l’utilisation des API [!DNL Target]. |
| [!UICONTROL IMS Organization ID] | Cet identifiant associe votre mise en oeuvre à votre compte Adobe Experience Cloud. |
| [!UICONTROL On-Device Decisioning] | Pour activer la prise de décision sur l’appareil, faites glisser la bascule vers la position &quot;activée&quot;.<p>La prise de décision sur les appareils vous permet de mettre en cache vos campagnes A/B et de ciblage d’expérience (XT) sur votre serveur et d’effectuer une prise de décision en mémoire à une latence proche de zéro. Pour plus d’informations, voir [Introduction à la prise de décision sur les appareils](../../../server-side/sdk-guides/on-device-decisioning/overview.md). |
| [!UICONTROL Include all existing on-device decisioning qualified activities in the artifact] | (Conditionnel) Cette option s’affiche si vous activez la prise de décision sur l’appareil.<p>Faites glisser le bouton d’activation vers la position &quot;Activé&quot; si vous souhaitez que toutes vos activités [!DNL Target] actives qui répondent aux critères de la prise de décision sur l’appareil soient automatiquement incluses dans l’artefact.<p>Si vous laissez ce bouton désactivé, vous devez recréer et activer toute activité de prise de décision sur l’appareil afin qu’elle soit incluse dans l’artefact de règles généré. |

## Méthodes de mise en oeuvre

Les paramètres suivants peuvent être configurés dans le panneau Méthodes de mise en oeuvre :

### Paramètres globaux

>[!NOTE]
>
>Ces paramètres sont appliqués à toutes les bibliothèques .js [!DNL Target]. Après avoir apporté des modifications à la section Méthodes de mise en oeuvre , vous devez télécharger la bibliothèque et la mettre à jour dans votre mise en oeuvre.

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Page load enabled (Auto-create global mbox)] | Indiquez si l’appel de la mbox globale doit être incorporé dans le fichier at.js afin d’être automatiquement déclenché lors de chaque chargement de page. |
| [!UICONTROL Global mbox] | Sélectionnez un nom pour la mbox globale. Par défaut, ce nom est target-global-mbox.<p>Avec at.js, les noms de mbox peuvent contenir des caractères spéciaux, y compris des esperluettes (&amp;). |
| [!UICONTROL Timeout (seconds)] | Si [!DNL Target] ne répond pas avec du contenu dans le délai défini, l’appel au serveur expire et le contenu par défaut est affiché. Des tentatives d’appel supplémentaires sont effectuées pendant la session du visiteur. Le délai par défaut est de 5 secondes.<p>La bibliothèque at.js utilise le paramètre d’expiration défini dans `XMLHttpRequest`. Le délai d’expiration commence lorsque la requête est déclenchée et s’arrête lorsque [!DNL Target] reçoit une réponse du serveur. Pour plus d’informations, voir [XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout) sur Mozilla Developer Network.<p>Si le délai d’expiration spécifié se produit avant la réception de la réponse, le contenu par défaut s’affiche et le visiteur peut être compté comme participant à une activité, car toute collecte de données se produit sur la périphérie [!DNL Target]. Si la requête atteint le serveur [!DNL Target] Edge, le visiteur est comptabilisé.<p>Tenez compte de ce qui suit lors de la configuration du paramètre d’expiration :<ul><li>Si la valeur est trop basse, les utilisateurs risquent de voir le contenu par défaut dans la plupart des cas, bien que le visiteur puisse être comptabilisé parmi les participants à l’activité.</li><li>Si la valeur est trop élevée, les visiteurs risquent de voir des zones vierges sur votre page web ou des pages vierges si vous utilisez le masquage du contenu pendant une durée prolongée.</li></ul>Pour une meilleure compréhension du temps de réponse de mbox, consultez l’onglet Réseau dans les Outils de développement de votre navigateur. Vous pouvez également utiliser des outils de surveillance des performances web tiers, tels que Catchpoint.<p>**Remarque** : le paramètre [visitorApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout) garantit que [!DNL Target] n’attend pas trop longtemps la réponse de l’API visiteur. Ce paramètre et le paramètre Expiration de at.js décrit ici n’ont pas d’effet l’un sur l’autre. |
| [!UICONTROL Profile Lifetime] | Ce paramètre détermine la durée de stockage des profils de visiteur. Par défaut, les profils sont stockés pendant deux semaines. Ce paramètre peut être augmenté jusqu’à 90 jours.<p>Pour modifier le paramètre Durée de vie du profil, contactez le [service à la clientèle](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C). |

### Méthode de mise en oeuvre principale

>[!NOTE]
>
>[!DNL Adobe Target] prend en charge at.js 1.*x* et at.js 2.*x*. Effectuez la mise à niveau vers la mise à jour la plus récente de l’une des principales versions d’at.js pour vous assurer que vous utilisez une version prise en charge.

Pour télécharger la version d’at.js souhaitée, cliquez sur le bouton **Télécharger** approprié.

Pour modifier le paramètre at.js, cliquez sur **[!UICONTROL Edit]** en regard de la version at.js souhaitée.

>[!WARNING]
>
>Avant de modifier ces paramètres par défaut, consultez le [service à la clientèle](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C) afin de ne pas affecter votre mise en oeuvre actuelle.

Outre les paramètres décrits ci-dessus, les paramètres at.js spécifiques suivants sont également disponibles :

| Paramètre | Description |
|--- |--- |
| Cross-Domain | Pour at.js v1.*x*, indiquez si les fonctionnalités interdomaines sont `disabled` (les navigateurs définissent les cookies dans votre domaine (cookies propriétaires uniquement)), `x only` (les navigateurs définissent les cookies dans le domaine de Target uniquement), ou les deux, en sélectionnant `enabled` (les navigateurs définissent les cookies propriétaires et tiers). Pour at.js v2.10 et versions ultérieures, indiquez si les fonctionnalités interdomaines sont `enabled` (les navigateurs définissent les cookies propriétaires et tiers) ou `disabled` (les navigateurs ne définissent pas les cookies tiers). |
| En-tête de bibliothèque personnalisé | Ajoutez du code JavaScript personnalisé à inclure au haut de la bibliothèque. |
| Pied de page de bibliothèque personnalisé | Ajoutez du code JavaScript personnalisé à inclure au bas de la bibliothèque. |

### API de profil

Activez ou désactivez l’authentification pour la mise à jour des lots via l’API et générez un jeton d’authentification de profil.

Pour plus d’informations, voir [Paramètres de l’API de profil](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md).

### Outils de débogage

Générez un jeton d’autorisation pour utiliser les outils avancés de débogage [!DNL Target]. Cliquez sur **[!UICONTROL Generate New Authentication Token]**.

![Générer un nouveau jeton d’authentification](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### Confidentialité

Ces paramètres vous permettent d’utiliser [!DNL Target] conformément aux lois applicables sur la confidentialité des données.

Sélectionnez un paramètre dans la liste déroulante Obscurcir l’adresse IP du visiteur :

* Obscurcissement du dernier octet
* Obscurcissement d’IP complet
* None

Pour plus d’informations, consultez la page [Confidentialité](/help/dev/before-implement/privacy/privacy.md).

>[!NOTE]
>
>L’option Prise en charge du navigateur hérité était disponible dans les versions 0.9.3 et antérieures d’ at.js . Cette option a été supprimée de la version 0.9.4 d’at.js. Pour obtenir une liste des navigateurs pris en charge par at.js, voir [Navigateurs pris en charge](/help/dev/before-implement/supported-browsers.md).<p>Les navigateurs hérités sont d’anciens navigateurs qui ne prennent pas entièrement en charge le partage des ressources cross-origin (CORS). Ces navigateurs comprennent Internet Explorer (versions antérieures à la version 11) et Safari (versions 6 et antérieures). Si la prise en charge du navigateur hérité a été désactivée, [!DNL Target] n’a pas diffusé de contenu ni comptabilisé les visiteurs dans les rapports sur ces navigateurs. Si cette option a été activée, il est recommandé d’effectuer une assurance qualité sur les navigateurs plus anciens afin de garantir une bonne expérience client.

## Téléchargement d’at.js

Instructions pour télécharger la bibliothèque à l’aide de l’interface [!DNL Target] ou de l’API de téléchargement.

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) est la méthode préférée pour implémenter [!DNL Target] et la bibliothèque at.js. Les informations suivantes ne s’appliquent pas lors de l’utilisation de balises dans [!DNL Adobe Experience Platform] pour implémenter [!DNL Target].
>
>[!DNL Adobe Target] prend en charge at.js 1.*x* et at.js 2.*x*. Effectuez une mise à niveau vers la mise à jour la plus récente de l’une des versions majeures d’at.js pour vous assurer que vous utilisez une version prise en charge. Pour en savoir plus sur le contenu de chaque version, voir [Informations détaillées sur les versions d’at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Télécharger at.js à l’aide de l’interface [!DNL Target]

Pour télécharger at.js depuis l’interface [!DNL Target] :

1. Cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Dans la section Méthodes d’implémentation , cliquez sur le bouton **[!UICONTROL Download]** en regard de la version at.js souhaitée.

### Télécharger at.js à l’aide de l’API de téléchargement [!DNL Target]

Pour télécharger at.js à l’aide de l’API, procédez comme suit :

1. Obtenez votre code client.

   Votre code client est disponible en haut de la page **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** de l’interface [!DNL Target].

1. Obtenez votre numéro d’administrateur.

   Chargez cette URL :

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   Remplacez `client code` par le code client de l’étape 1.

   Le résultat du chargement de cette URL doit ressembler à l’exemple suivant :

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   Dans cet exemple, le numéro d’administrateur est 6.

1. Téléchargez at.js.

   Chargez cette URL avec la structure suivante. Le chargement de cette URL démarre le téléchargement de votre fichier at.js personnalisé.

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * Remplacez `admin number` par votre numéro d’administrateur.
   * Remplacez `client code` par le code client de l’étape 1.
   * Remplacez `version number` par le numéro de version at.js souhaité (par exemple, 2.2).

>[!WARNING]
>
>L’équipe [!DNL Target] gère deux versions seulement d’at.js : la version actuelle et la version la plus récente avant celle-ci. Mettez à niveau at.js si nécessaire pour vous assurer que vous utilisez une version prise en charge. Pour en savoir plus sur le contenu de chaque version, voir [Informations détaillées sur les versions d’at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

## Implémentation d’at.js

Vous devez implémenter at.js à `<head>` l’élément de chaque page de votre site web.

Une implémentation classique de [!DNL Target] n’utilisant pas de gestionnaire de balises, comme les balises dans [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) ressemble à ceci :

```
<!doctype html> 
<html> 
<head> 
    <meta charset="utf-8"> 
    <title>Title of the Page</title> 
    <!--Preconnect and DNS-Prefetch to improve page load time--> 
    <link rel="preconnect" href="//<client code>.tt.omtrdc.net"> 
    <link rel="dns-prefetch" href="//<client code>.tt.omtrdc.net"> 
    <!--/Preconnect and DNS-Prefetch--> 
    <!--Data Layer to enable rich data collection and targeting--> 
    <script> 
        var digitalData = { 
            "page": { 
                "pageInfo": { 
                    "pageName": "Home" 
                } 
            } 
        }; 
    </script> 
    <!--/Data Layer--> 
    <!-- targetPageParams(), targetPageParamsAll(), Data Providers or targetGlobalSettings() functions to enrich the visitor profile or modify the library settings--> 
    <script> 
        targetPageParams = function() { 
            return { 
                "a": 1, 
                "b": 2, 
                "pageName": digitalData.page.pageInfo.pageName, 
                "profile": { 
                    "age": 26, 
                    "country": { 
                        "city": "San Francisco" 
                    } 
                } 
            }; 
        }; 
    </script> 
    <!--/targetPageParams()--> 
 
    <!--jQuery or other helper libraries should be implemented before at.js if you would like to use their methods in Target--> 
    <script src="jquery-3.3.1.min.js"></script> 
    <!--/jQuery--> 
    <!--Target's JavaScript SDK, at.js--> 
    <script src="at.js"></script> 
    <!--/at.js--> 
</head>
<body> 
    The default content of the page 
</body> 
</html>
```

Tenez compte des remarques importantes suivantes :

* Le Doctype HTML5 (par exemple, `<!doctype html>`) doit être utilisé. Les doctypes non pris en charge ou plus anciens peuvent empêcher [!DNL Target] d’effectuer une requête.
* Les options de préconnexion et de prérécupération peuvent aider vos pages web à charger plus rapidement. Si vous utilisez ces configurations, assurez-vous de remplacer `<client code>` par votre propre code client, que vous pouvez obtenir sur la page **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** .
* Si vous possédez une couche de données, l’idéal est d’en définir le plus possible dans la section `<head>`de vos pages, et ce avant le chargement d’at.js. Cet emplacement offre la possibilité maximale d’utiliser ces informations dans [!DNL Target] pour la personnalisation.
* Les fonctions spéciales [!DNL Target], telles que `targetPageParams()`, `targetPageParamsAll()`, les fournisseurs de données et `targetGlobalSettings()`, doivent être définies après la couche de données et avant le chargement d’at.js. Vous pouvez également enregistrer ces fonctions dans la section En-tête de bibliothèque de la page Modifier les paramètres at.js et les enregistrer dans la bibliothèque at.js elle-même. Pour plus d’informations sur ces fonctions, voir [Fonctions at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).
* Si vous utilisez des bibliothèques d’assistance JavaScript, telles que jQuery, incluez-les avant [!DNL Target] afin que vous puissiez utiliser leur syntaxe et leurs méthodes lors de la création d’expériences [!DNL Target].
* Incluez at.js dans la section `<head>` de vos pages.

## Suivi des conversions

La mbox de confirmation de commande enregistre des détails sur les commandes passées sur votre site, puis rend possible la création de rapports en fonction des recettes et des commandes. Elle contribue également aux algorithmes de recommandation, tels que « Les personnes qui ont acheté le produit x ont également acheté le produit y ».

>[!NOTE]
>
>Si les utilisateurs effectuent des achats sur votre site web, Adobe recommande de mettre en oeuvre une mbox de confirmation de commande, même si vous utilisez Analytics for [!DNL Target] (A4T) pour vos rapports.

1. Sur votre page des détails de la commande, insérez un script de mbox en respectant le modèle ci-dessous.
1. Remplacez les MOTS EN LETTRES MAJUSCULES par des valeurs dynamiques ou statiques issues de votre catalogue.

   >[!TIP]
   >
   >Vous pouvez également transmettre des informations de commande dans n’importe quelle mbox (il n’est pas nécessaire de le nommer `orderConfirmPage`). Vous pouvez également transmettre les informations de la commande dans plusieurs mbox au sein de la même campagne.

   ```
   <script type="text/javascript"> 
   adobe.target.trackEvent({ 
       "mbox": "orderConfirmPage", 
       "params":{  
           "orderId": "ORDER ID FROM YOUR ORDER PAGE",  
           "orderTotal": "ORDER TOTAL FROM YOUR ORDER PAGE",  
           "productPurchasedId": "PRODUCT ID FROM YOUR ORDER PAGE, PRODUCT ID2, PRODUCT ID3"  
       } 
   }); 
   </script> 
   ```

>[!NOTE]
>
>Dans la mbox de confirmation de commande, utilisez des virgules de séparation pour séparer plusieurs ID de produit.

La mbox de confirmation de commande utilise les paramètres suivants :

| Paramètre | Description |
|--- |--- |
| orderId | Valeur unique identifiant une commande pour la comptabilisation de la conversion.<p>L’`orderId` doit être unique. Les commandes en double ne sont pas prises en compte dans les rapports. |
| orderTotal | Valeur monétaire de l’achat.<p>N’indiquez pas le symbole de la devise. Utilisez un point décimal (pas une virgule) pour indiquer les valeurs décimales. |
| productPurchasedId (facultatif) | Liste des ID de produit achetés dans la commande séparés par des virgules.<p>Ces ID produit s’affichent dans le rapport d’audit pour étayer les analyses de rapports supplémentaires. |
