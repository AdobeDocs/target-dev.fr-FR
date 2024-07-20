---
keywords: SDK web Adobe Experience Platform, sdk web aep, sdk web, sdk, adobe experience cloud, réseau Edge de la plateforme, réseau Edge d’adobe experience platform, réseau Edge, réseau Edge aep, SDK Web Adobe Experience Platform0
description: Découvrez comment utiliser le [!UICONTROL Adobe Experience Platform Web SDK] pour interagir avec les différents services dans le [!UICONTROL Adobe Experience Cloud] par le [!UICONTROL AEP Edge Network].
title: Comment mettre en oeuvre avec le [!UICONTROL Experience Platform Web SDK] ?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (SDK Web AEP) est une bibliothèque JavaScript côté client qui permet aux clients de [!UICONTROL Adobe Experience Cloud] d’interagir avec les différents services de [!DNL Adobe Experience Cloud] (y compris [!DNL Target]) par l’intermédiaire de [!UICONTROL Adobe Experience Platform Edge Network]. Outre la bibliothèque JavaScript, il existe une extension [!UICONTROL Adobe Experience Platform] pour vous aider à configurer vos SDK Web.

Pour plus d’informations, voir les liens suivants dans l’aide de *[!UICONTROL Adobe Experience Platform Web SDK]* :

* Pour obtenir des informations complètes : [What is [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=fr)
* Pour plus d’informations spécifiques à [!DNL Target] : [[!DNL Target] Présentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=fr)

## Tutoriels

Les tutoriels suivants vous aident dans votre mise en oeuvre :

### Mise en oeuvre de [!DNL Adobe Experience Cloud] avec [!DNL Platform Web SDK]

Découvrez comment mettre en oeuvre des applications [!DNL Experience Cloud] à l’aide de [!DNL Adobe Experience Platform Web SDK] avec [ce tutoriel](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). Pour plus d’informations sur [!DNL Target], consultez la section de tutoriel intitulée [Configuration [!DNL Target]  avec le SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrez [!DNL Target] depuis at.js 2.*x* à [!DNL Platform Web SDK]

Découvrez comment migrer votre implémentation [!DNL Target] depuis at.js 2.*x* vers [!DNL Adobe Experience Platform Web SDK] avec [ce tutoriel](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=fr).

## Documentation recommandée

Outre la documentation [!UICONTROL Platform Web SDK] mentionnée ci-dessus, les rubriques de ce guide contiennent également des informations spécifiques à [!UICONTROL Platform Web SDK] en ce qui concerne les fonctionnalités de [!DNL Target].

| Fonctionnalité | Description/Lien |
| --- | --- |
| [QA d’activité](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Utilisez les URL AQ dans [!DNL Target] pour effectuer une AQ d’activité de bout en bout simple avec des liens d’aperçu qui ne changent jamais, un ciblage d’audience facultatif et une création de rapports d’AQ qui restent segmentés à partir des données d’activité actives. L’AQ d’activité vous permet de tester entièrement vos activités [!DNL Target] avant de les lancer en direct.<p>Voir [Compatibilité du mode AQ de la bibliothèque Target JavaScript](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) et [Prévisualiser les URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics for Target] (A4T) est une intégration intersolutions permettant de créer des activités basées sur les mesures de conversion d’[!DNL Analytics] ainsi que sur les segments d’audience. L’intégration A4T vous permet d’utiliser des rapports Analytics pour examiner vos résultats.<p>Voir [Types d’activité pris en charge](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) et [Étapes de mise en oeuvre pour une mise en oeuvre du SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Audiences](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Les audiences de [!DNL Target] déterminent qui voit le contenu et les expériences dans une activité ciblée.<p>Voir [Utilisation de la liste d’audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) et [Combinaison de plusieurs audiences](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Création dʼaudiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=fr) | L’utilisation d’audiences créées dans [!DNL Adobe Experience Platform] fournit des données client plus riches qui permettent une personnalisation plus impactée.<p>Voir [Utilisation d’audiences de Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [Offer Decisions](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Ajoutez les décisions d’offre créées dans [!DNL Adobe Journey Optimizer] aux activités [!DNL Target] (test A/B manuel ou ciblage d’expérience) afin de déterminer et de proposer la meilleure offre qui s’offre aux visiteurs sur le web et sur mobile. |
| [FAQ sur les offres de redirection - A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Les offres de redirection provoquent la redirection des navigateurs des visiteurs vers une nouvelle page.<p>Voir [Le [!UICONTROL Adobe Experience Platform Web SDK] prend-il en charge les offres de redirection pour A4T ?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Les jetons de réponse vous permettent d’envoyer [!DNL Target] données à des Google Analytics et à d’autres intégrations tierces.<p>Voir [Envoi de données à des Google Analytics via le SDK Web Platform](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) pour voir un exemple de code sur la manière d’accomplir cette tâche. |
| [Implémentation d’applications d’une seule page](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) dans le guide *[!UICONTROL Platform Web SDK]overview*. | [!UICONTROL Adobe Experience Platform Web SDK] fournit des fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies côté client de nouvelle génération, telles que les applications d’une seule page (SPA). |
| [Modifications du chiffrement de TLS (Transport Layer Security)](../../before-implement/tls-transport-layer-security-encryption.md) | TLS (Transport Layer Security) vous aide à maintenir les normes de sécurité les plus élevées et à promouvoir la sécurité des données client. |
