---
keywords: mbox globale, implémentation d’at.js
description: Découvrez la mbox globale dans [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] implémentation.
title: Qu’est-ce qu’une mbox globale ?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 73%

---

# Présentation de la mbox globale

Informations sur la mbox globale, nom désignant l’appel de serveur effectué en haut de chaque page web dans votre mise en œuvre [!DNL Adobe Target].

Par défaut, la mbox globale est nommée `target-global-mbox`. Si nécessaire, vous pouvez la renommer pour votre compte.

Il existe plusieurs différences entre une mbox ordinaire (mbox non globale) et la mbox globale, notamment :

| mbox ordinaire | mbox globale |
|--- |--- |
| Généralement, une mbox ordinaire encapsule le contenu à l’aide d’une balise `<DIV>`. | La mbox globale est « vide » et n’encapsule aucun contenu. |
| Le contenu d’une seule activité peut être distribué dans une mbox ordinaire. | Le contenu de plusieurs activités peut être distribué dans une réponse à une mbox globale. |

Si plusieurs activités sont diffusées via la mbox globale ou via plusieurs mbox ordinaires, Target [détermine la priorité](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) par laquelle l’activité (ou les activités) sont diffusées sur une page web.

D’autres données au niveau de la page peuvent être envoyées à [!DNL Target] avec la mbox globale, en utilisant la fonction `[!UICONTROL targetPageParams]`. Ceci est similaire à la fonctionnalité du paramètre de mbox. Pour plus d’informations, veuillez consulter la section [Transfert de paramètres vers une mbox globale](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
