---
keywords: mbox globale, implémentation d’at.js
description: En savoir plus sur la mbox globale dans l [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] implémentation.
title: Qu’est-ce qu’une mbox globale ?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
TQID: https://experienceleague.adobe.com/MXEGvHHY8tFMfS6bMHcZYaG9mZtOWEkuODKH24JifZI
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
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 61%

---

# Présentation de la mbox globale

Informations sur la mbox globale, un nom utilisé pour faire référence à l’appel au serveur unique effectué en haut de chaque page web dans votre implémentation [!DNL Adobe Target].

Par défaut, la mbox globale est nommée `target-global-mbox`. Si nécessaire, vous pouvez la renommer pour votre compte.

Il existe plusieurs différences entre une mbox ordinaire (mbox non globale) et la mbox globale, notamment :

| mbox ordinaire | mbox globale |
|--- |--- |
| Généralement, une mbox ordinaire encapsule le contenu à l’aide d’une balise `<DIV>`. | La mbox globale est « vide » et n’encapsule aucun contenu. |
| Le contenu d’une seule activité peut être distribué dans une mbox ordinaire. | Le contenu de plusieurs activités peut être distribué dans une réponse à une mbox globale. |

Si plusieurs activités sont diffusées via la mbox globale ou plusieurs mbox standard, Target [détermine la priorité](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) selon laquelle la ou les activités sont diffusées sur une page web.

D’autres données au niveau de la page peuvent être envoyées à [!DNL Target] avec la mbox globale, en utilisant la fonction `[!UICONTROL targetPageParams]`. Ceci est similaire à la fonctionnalité du paramètre de mbox. Pour plus d’informations, veuillez consulter la section [Transfert de paramètres vers une mbox globale](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
