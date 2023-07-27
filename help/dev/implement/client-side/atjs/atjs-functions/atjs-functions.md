---
keywords: at.js, fonctions, bibliothèque JavaScript
description: Affichez la liste des fonctions pouvant être utilisées avec les versions 1.x et 2.x de la bibliothèque JavaScript at.js dans [!DNL Adobe Target].
title: Quelles fonctions puis-je utiliser avec at.js ?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 73%

---

# Fonctions d’at.js

Liste des fonctions pouvant être utilisées avec la fonction [!DNL Adobe Target] Bibliothèque JavaScript at.js. Cliquez sur les liens de la colonne Fonction pour plus d’informations et d’exemples.

| Fonction | Détails |
| --- | --- | 
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | Cette fonction déclenche une requête pour obtenir une [!DNL Target] offre. Utilisez avec `adobe.target.applyOffer()` pour traiter la réponse ou utilisez votre propre gestion de succès. |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | Cette fonction permet de récupérer plusieurs offres en transmettant plusieurs mbox. De plus, plusieurs offres peuvent être extraites pour toutes les vues des activités actives.<P>**Remarque :** cette fonction a été introduite avec at.js 2.x. Cette fonction n’est pas disponible pour at.js version 1.*x*. |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | Cette fonction permet d’appliquer le contenu de la réponse. |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | Cette fonction vous permet d’appliquer plusieurs offres récupérées par [!UICONTROL adobe.target.getOffers()].<P>**Remarque :** cette fonction a été introduite avec at.js 2.x. Cette fonction n’est pas disponible pour at.js version 1.*x*. |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | Cette fonction peut être appelée à chaque chargement d’une nouvelle page ou lorsqu’un composant fait l’objet d’un nouveau rendu sur une page.<P> Cette fonction doit être implémentée pour les applications d’une seule page (SPA) afin d’utiliser la fonction [!UICONTROL Compositeur d’expérience visuelle] (VEC) à créer [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] (XT). |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | Cette fonction déclenche une demande pour signaler les actions de l’utilisateur, telles que les clics et les conversions. Elle ne déclenche pas la diffusion d’activités dans le cadre de la réponse. |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | Exécute une requête et applique l’offre au DIV le plus proche avec le nom de la classe mboxDefault.<P>**Remarque :** Cette fonction est disponible pour at.js versions 1.*x* uniquement. Cette fonction a été abandonnée avec la version d’at.js 2.x. Cette fonction renvoie le contenu par défaut s’il est utilisé avec at.js 2.x. |
| [[!UICONTROL mboxDefine(options)] et [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | Définissent et mettent à jour une mbox.<P>**Remarque :** Cette fonction est disponible pour at.js versions 1.*x* uniquement. Cette fonction a été abandonnée avec la version d’at.js 2.x. Cette fonction renvoie le contenu par défaut s’il est utilisé avec at.js 2.x. |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | Vous pouvez remplacer les paramètres de la bibliothèque at.js à l’aide de la fonction `[!UICONTROL targetGlobalSettings()]`, plutôt que de les configurer dans la variable [!DNL Target Standard/Premium] IU ou à l’aide des API REST.<ul><li>Fournisseurs de données : ce paramètre permet aux clients de collecter des données auprès de fournisseurs de données tiers tels que Demandbase, BlueKai ou des services personnalisés, et de les transmettre à Target sous forme de paramètres mbox dans la requête globale mbox.</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | Cette méthode permet de joindre des paramètres à la mbox globale depuis l’extérieur du code de demande. |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | Cette méthode permet de joindre des paramètres à toutes les mbox à l’extérieur du code de demande. |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | Propose une méthode standard pour enregistrer une extension spécifique.<P>**Remarque :** Cette fonction est disponible pour at.js versions 1.*x* uniquement. Cette fonction a été abandonnée avec la version d’at.js 2.x. Cette fonction renvoie le contenu par défaut s’il est utilisé avec at.js 2.x. |
| [[!UICONTROL événements personnalisés at.js]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | Les événements personnalisés at.js indiquent quand une requête ou une offre de mbox échoue ou réussit. |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | Cette fonction envoie une notification à [!DNL Target] edge lorsqu’une expérience est générée sans utiliser `[!UICONTROL adobe.target.applyOffer()]` ou `[!UICONTROL adobe.target.applyOffers()]`.<P>**Remarque** : Cette fonction a été introduite dans at.js 2.1.0 et sera disponible pour toutes les versions ultérieures à 2.1.0. |
