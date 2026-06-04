---
keywords: dépannage, questions fréquentes, FAQ, forum aux questions, globale, mbox globale
description: 'Consultez les questions fréquentes (FAQ) relatives aux mbox globales dAdobe. [!DNL Target] '
title: Quelles sont les questions fréquentes sur la mbox globale ?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
TQID: https://experienceleague.adobe.com/bxsjCqSQpp6M20StzZtMBrfxjJCKgPEPfS2OlBUP00A
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# Questions fréquentes relatives aux mbox globales

Liste des questions fréquentes (FAQ) relatives aux mbox globales.

## Puis-je avoir plusieurs mbox globales si mon compte [!DNL Target] est défini sur plusieurs domaines ?

Une seule mbox globale est prise en charge pour l’ensemble du compte.

Vous pouvez limiter l’exécution des activités en ajoutant des règles d’URL à ces dernières. Pour plus d’informations, voir [Inclure la même expérience sur des pages similaires](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

Vous pouvez également transmettre un paramètre sur la page à l’aide de [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md), puis sélectionner ces paramètres dans la section « Configurer l’URL » du [!UICONTROL Compositeur d’expérience visuelle] (VEC) ou en ajoutant les paramètres en tant que « affinements » dans le [!UICONTROL Compositeur d’expérience d’après les formulaires].

## Comment transmettre les données de chiffre d’affaires sur une mbox globale [!DNL Target] ?

Pour collecter les informations de chiffre d’affaires et de commande sur la target-global-mbox, les « paramètres de mbox » doivent être envoyés à [!DNL Target]. Ces paramètres sont des paires nom/valeur utilisées pour envoyer plus d’informations à [!DNL Target]. [!DNL Target] recherche automatiquement ces paramètres (noms réservés) pour renseigner les données de chiffre d’affaires.

Pour la `orderConfirmPage`, vous devez transmettre `orderTotal`, `orderId` et `productPurchasedId`.

Ces paramètres doivent être envoyés à target-global-mbox via `targetPageParams()`. Pour plus d’informations, veuillez consulter la section [Transfert de paramètres vers une mbox globale](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

Vous souhaiterez également ajouter le ciblage à l’élément de conversion afin que [!DNL Target] ne compte les conversions sur target-global-mbox que lorsque la page de confirmation de commande a été consultée, comme illustré ci-dessous :

![image alternative](assets/revenue1.png)

La section Pages du site illustrée ci-dessus comporte les sélections suivantes : Page actuelle, URL, contient, orderconfirm.

![image alternative](assets/revenue2.png)

Les options de l’illustration ci-dessus incluent les paramètres suivants :

* **Que souhaitez-vous mesurer avec cette activité ? :** Recettes
* **Affichage par défaut pour les rapports :** Recettes par visiteur (RPV)
* **Quelle action a été entreprise par votre audience pour indiquer que votre objectif a été atteint ?** mbox affichée : target-global-mbox
