---
keywords: Adobe Experience Platform Web SDK, sdk web aep, sdk web, sdk, adobe experience cloud, platform edge network, adobe experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: Découvrez comment utiliser l’[!UICONTROL Adobe Experience Platform Web SDK] pour interagir avec les différents services de l’[!UICONTROL Adobe Experience Cloud] via l’[!UICONTROL AEP Edge Network].
title: Comment effectuer une implémentation avec le [!UICONTROL Experience Platform Web SDK] ?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: ac03d5d15875ab4945b07b3e95037ce9ecde1044
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) est une bibliothèque JavaScript côté client qui permet aux clients de [!UICONTROL Adobe Experience Cloud] d’interagir avec les différents services de la [!DNL Adobe Experience Cloud] (y compris [!DNL Target]) via [!UICONTROL Adobe Experience Platform Edge Network]. Outre la bibliothèque JavaScript, il existe une extension [!UICONTROL Adobe Experience Platform] pour vous aider à configurer votre SDK Web.

Pour plus d’informations, consultez les liens suivants dans l’aide de *[!UICONTROL Adobe Experience Platform Web SDK]* :

* Pour obtenir des informations complètes : [Qu’est-ce que [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=fr)
* Pour plus d’informations spécifiques à [!DNL Target] : [[!DNL Target] Présentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=fr)

## Tutoriels

Les tutoriels suivants vous aident à mettre en œuvre :

### Implémentation de [!DNL Adobe Experience Cloud] avec [!DNL Platform Web SDK]

Découvrez comment implémenter des applications [!DNL Experience Cloud] à l’aide de [!DNL Adobe Experience Platform Web SDK] avec [ce tutoriel](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). Pour plus d’informations spécifiques à [!DNL Target], consultez la section du tutoriel intitulée [Configuration d [!DNL Target] avec Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migration de [!DNL Target] à partir d’at.js 2.*x* à [!DNL Platform Web SDK]

Découvrez comment migrer votre implémentation [!DNL Target] à partir d’at.js 2.*x* au [!DNL Adobe Experience Platform Web SDK] avec [ce tutoriel](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=fr).

## Documentation recommandée

Outre la documentation [!UICONTROL Platform Web SDK] mentionnée ci-dessus, les rubriques de ce guide contiennent également des informations spécifiques au [!UICONTROL Platform Web SDK] en ce qui concerne [!DNL Target] fonctionnalités.

| Fonctionnalité | Description/Lien |
| --- | --- |
| [QA d’activité](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Utilisez les URL d’assurance qualité dans [!DNL Target] pour effectuer facilement une assurance qualité de bout en bout de l’activité avec des liens d’aperçu qui ne changent jamais, un ciblage d’audience facultatif et un compte rendu des performances d’assurance qualité qui reste segmenté à partir des données d’activité en direct. Le QA d’activité vous permet de tester entièrement vos activités [!DNL Target] avant de les lancer en direct.<p>Consultez les sections [Compatibilité du mode AQ de la bibliothèque JavaScript Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) et [Aperçu des URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics for Target] (A4T) est une intégration intersolutions permettant de créer des activités basées sur les mesures de conversion d’[!DNL Analytics] ainsi que sur les segments d’audience. L’intégration A4T vous permet d’utiliser les rapports Analytics pour examiner vos résultats.<p>Voir [Types d’activité pris en charge](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) et [Étapes d’implémentation pour une implémentation de Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Audiences](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Les audiences dans [!DNL Target] déterminent qui peut voir le contenu et les expériences d’une activité ciblée.<p>Voir [Utilisation de la liste Audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) et [Combinaison de plusieurs audiences](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Création dʼaudiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=fr) | Les audiences créées dans [!DNL Adobe Experience Platform] fournissent des données client plus riches et permettent d’offrir une personnalisation plus poussée.<p>Voir [Utilisation des audiences de Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [Décisions d’offre](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Ajoutez les décisions d’offre créées en [!DNL Adobe Journey Optimizer] aux activités [!DNL Target] (test A/B manuel ou ciblage d’expérience) pour déterminer et diffuser la meilleure offre pour vos visiteurs sur le web et les appareils mobiles. |
| [FAQ sur les offres de redirection - A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Les offres de redirection entraînent la redirection par les navigateurs des visiteurs vers une nouvelle page.<p>Voir [Le [!UICONTROL Adobe Experience Platform Web SDK] prend-il en charge les offres de redirection pour A4T ?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Les jetons de réponse vous permettent d’envoyer des données [!DNL Target] à Google Analytics et à d’autres intégrations tierces.<p>Consultez [Envoi de données à Google Analytics via Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) pour voir un exemple de code illustrant comment accomplir cette tâche. |
| [Implémentation d’applications d’une seule page](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) dans le guide *[!UICONTROL Platform Web SDK]présentation* . | [!UICONTROL Adobe Experience Platform Web SDK] fournit des fonctionnalités riches qui permettent à votre entreprise d’exécuter de la personnalisation sur des technologies côté client de nouvelle génération, telles que les applications d’une seule page (SPA). |
| [Modifications du chiffrement de TLS (Transport Layer Security)](/help/dev/before-implement/tls-transport-layer-security-encryption.md) | TLS (Transport Layer Security) vous aide à maintenir les normes de sécurité les plus élevées et à promouvoir la sécurité des données client. |
