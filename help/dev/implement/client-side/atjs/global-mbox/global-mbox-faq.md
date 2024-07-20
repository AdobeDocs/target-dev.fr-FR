---
keywords: dépannage, questions fréquentes, FAQ, forum aux questions, globale, mbox globale
description: Lisez les questions fréquentes et les réponses sur les mbox globales Adobe [!DNL Target] .
title: Questions fréquentes à propos de la mbox globale
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 39%

---

# Questions fréquentes relatives aux mbox globales

Liste des questions fréquentes (FAQ) relatives aux mbox globales.

## Puis-je avoir plusieurs mbox globales si mon compte [!DNL Target] est défini sur plusieurs domaines ?

Une seule mbox globale est prise en charge pour l’ensemble du compte.

Vous pouvez limiter l’exécution des activités en ajoutant des règles d’URL à ces dernières. Pour plus d’informations, voir [Inclure la même expérience sur des pages similaires](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

Vous pouvez également transmettre un paramètre sur la page à l’aide de [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md), puis sélectionner ces paramètres dans la section &quot;Configurer l’URL&quot; dans le [!UICONTROL Visual Experience Composer] (VEC) ou en ajoutant les paramètres comme &quot;ajustements&quot; dans le [!UICONTROL Form-Based Experience Composer].

## Comment puis-je transmettre des données de recettes à une mbox globale [!DNL Target] ?

Pour collecter les recettes et commander des informations sur target-global-mbox, les &quot;paramètres mbox&quot; doivent être envoyés à [!DNL Target]. Ces paramètres sont des paires nom/valeur utilisées pour envoyer plus d’informations à [!DNL Target]. [!DNL Target] recherche automatiquement ces paramètres (noms réservés) pour renseigner les données de recettes.

Pour le `orderConfirmPage`, vous devez transmettre `orderTotal`, `orderId` et `productPurchasedId`.

Ces paramètres doivent être envoyés à target-global-mbox via `targetPageParams()`. Pour plus d’informations, veuillez consulter la section [Transfert de paramètres vers une mbox globale](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

Vous souhaiterez également ajouter un ciblage à l’élément de conversion afin que [!DNL Target] ne comptabilise que les conversions sur target-global-mbox lorsque la page de confirmation de commande a été affichée, comme illustré ci-dessous :

![alt image](assets/revenue1.png)

La section Pages du site illustrée ci-dessus comporte les sélections suivantes : Page actuelle, URL, contient, orderconfirm.

![alt image](assets/revenue2.png)

Les options de l’illustration ci-dessus incluent les paramètres suivants :

* **Que souhaitez-vous mesurer avec cette activité ? :** Recettes
* **Affichage par défaut pour les rapports :** Recettes par visiteur (RPV)
* **Quelle action a été entreprise par votre audience pour indiquer que votre objectif a été atteint ?** A affiché une mbox, target-global-mbox
