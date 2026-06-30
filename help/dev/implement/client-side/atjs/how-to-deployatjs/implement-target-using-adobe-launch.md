---
keywords: implémentation, implémentation, implémentation, adobe launch, launch, race, redirection, experience platform launch, platform launch, balises, adobe platform, implémentation2
description: Découvrez comment implémenter la bibliothèque at [!DNL Adobe Target] js à l’aide de  [!DNL Adobe Experience Platform], la méthode recommandée pour implémenter Target.
title: Comment puis-je implémenter  [!DNL Target]  avec  [!DNL Adobe Experience Platform] ?
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
TQID: https://experienceleague.adobe.com/5dXJlXYYvlu5sskrNED2j55SNmeggtWTb1jLgXRXAEo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 61%

---

# Implémentation de [!DNL Target] à l’aide d’[!DNL Adobe Experience Platform]

Les balises dans [!DNL Adobe Experience Platform] représentent la nouvelle génération de fonctionnalités de gestion des balises proposées par [!DNL Adobe]. Les balises offrent aux clients un moyen simple de déployer et gérer les balises d’analyse, de marketing et de publicité nécessaires pour proposer des expériences client pertinentes.

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans [!DNL Adobe Experience Platform]. Plusieurs modifications terminologiques ont par conséquent été déployées dans la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html ?) suivant pour obtenir une référence consolidée des modifications terminologiques.

Le tableau suivant répertorie les différentes sources fournissant plus d’informations :

| Ressource | Détails |
|--- |--- |
| [Ajouter Adobe Target](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html?lang=fr#implement-solutions) | Ce tutoriel fournit des instructions détaillées relatives à l’implémentation de [!DNL Target] dans un site web avec des balises dans [!DNL Adobe Experience Platform]. Les rubriques incluent l’ajout de la bibliothèque JavaScript at.js, le déclenchement de la mbox globale, l’ajout de paramètres et l’intégration à d’autres solutions. Cet article fait partie d’un tutoriel plus vaste qui vous explique comment implémenter Adobe Experience Platform et d’autres solutions Adobe Experience Cloud. |
| [Guide de démarrage rapide](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=fr) | Informations sur le déploiement et la gestion des balises d’analyse, de marketing et de publicité nécessaires pour proposer des expériences client pertinentes. |
| [Présentation de l’extension Adobe  [!DNL Target] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=fr) | Informations sur l’implémentation de [!DNL Target] avec [!DNL Adobe Experience Platform]. |

## Avantages de l’implémentation d’at.js à l’aide de l’extension [!DNL Target]

Les avantages suivants s’appliquent uniquement si vous utilisez les balises dans [!DNL Adobe Experience Platform] pour implémenter at.js. Pour cette raison, Adobe vous recommande vivement d’utiliser les balises dans [!DNL Adobe Experience Platform] plutôt qu’une implémentation manuelle d’at.js.

* **Résout la condition de concurrence [!DNL Adobe Analytics] et [!DNL Target] :** comme l’appel [!DNL Analytics] peut être déclenché avant l’appel [!DNL Target], l’appel [!DNL Target] n’est pas associé à l’appel [!DNL Analytics]. Ce séquencement peut entraîner des données incorrectes. L’extension [!DNL Target] garantit que l’appel de la balise [!DNL Analytics] attend la fin de l’appel [!DNL Target], réussi ou non. L’utilisation de balises dans [!DNL Adobe Experience Platform] résout l’incohérence des données que les clients peuvent rencontrer lors de l’implémentation manuelle.

  >[!NOTE]
  >
  >Utilisez l’action Envoyer la balise dans l’extension [!DNL Adobe Analytics] afin que l’appel [!DNL Analytics] attende l’appel [!DNL Target]. Si vous appelez directement `s.t()` ou `s.tl()` à l’aide d’un code personnalisé, les appels [!DNL Analytics] n’attendent pas la fin des appels [!DNL Target].

* **Empêche une gestion incorrecte des offres de redirection :** si la page contient des [!DNL Target] et des [!DNL Analytics] et qu’une offre de redirection est en cours d’exécution par Target, il peut arriver que le dispositif de suivi des [!DNL Analytics] déclenche une requête alors qu’il ne devrait pas (car l’utilisateur est redirigé vers une autre URL). Si vous implémentez [!DNL Target] et [!DNL Analytics] au moyen de balises dans [!DNL Adobe Experience Platform], vous ne rencontrerez pas ce problème. À l’aide des balises dans [!DNL Adobe Experience Platform], [!DNL Target] donne l’ordre à [!DNL Analytics] d’abandonner la requête de balise [!DNL Analytics].


