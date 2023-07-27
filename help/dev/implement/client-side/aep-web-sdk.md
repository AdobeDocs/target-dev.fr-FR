---
keywords: SDK web Adobe Experience Platform, sdk web aep, sdk web, sdk, adobe experience cloud, réseau Edge de la plateforme, réseau Edge d’adobe experience platform, réseau Edge, réseau Edge aep, SDK Web Adobe Experience Platform0
description: Découvrez comment utiliser le [!UICONTROL SDK Web Adobe Experience Platform] pour interagir avec les différents services de la variable [!UICONTROL Adobe Experience Cloud] par le biais du [!UICONTROL AEP Edge Network].
title: Comment mettre en oeuvre avec le [!UICONTROL SDK Web Experience Platform]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 12%

---

# [!UICONTROL SDK web Adobe Experience Platform]

[!UICONTROL SDK Web Adobe Experience Platform] (SDK Web AEP) est une bibliothèque JavaScript côté client qui permet aux clients de [!UICONTROL Adobe Experience Cloud] pour interagir avec les différents services de la variable [!DNL Adobe Experience Cloud] (y compris [!DNL Target]) par l’intermédiaire de la variable [!UICONTROL Adobe Experience Platform Edge Network]. Outre la bibliothèque JavaScript, il existe une [!UICONTROL Adobe Experience Platform] extension pour faciliter les configurations de votre SDK Web.

Pour plus d’informations, voir les liens suivants dans la section *[!UICONTROL SDK Web Adobe Experience Platform]* help:

* Pour obtenir des informations complètes : [Présentation [!UICONTROL SDK Web Adobe Experience Platform]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=fr)
* Pour plus d’informations spécifiques à [!DNL Target]: [[!DNL Target] Présentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=fr)

## Tutoriels

Les tutoriels suivants vous aident dans votre mise en oeuvre :

### Mise en oeuvre [!DNL Adobe Experience Cloud] avec [!DNL Platform Web SDK]

Découvrez comment implémenter [!DNL Experience Cloud] applications utilisant [!DNL Adobe Experience Platform Web SDK] avec [ce tutoriel](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). Pour plus d’informations spécifiques à [!DNL Target], consultez la section du tutoriel intitulée [Configuration [!DNL Target] avec SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrer [!DNL Target] depuis at.js 2.*x* to [!DNL Platform Web SDK]

Découvrez comment migrer votre [!DNL Target] implémentation à partir d’at.js 2.*x* à la fonction [!DNL Adobe Experience Platform Web SDK] avec [ce tutoriel](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=fr).

## Documentation recommandée

En plus de la variable [!UICONTROL SDK Web Platform] documentation mentionnée ci-dessus, les rubriques de ce guide contiennent également des informations spécifiques à la [!UICONTROL SDK Web Platform] en ce qui concerne [!DNL Target] fonctions et fonctionnalités.

| Fonctionnalité | Description/Lien |
| --- | --- |
| [QA d’activité](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Utilisation d’URL AQ dans [!DNL Target] pour effectuer une AQ d’activité de bout en bout simple avec des liens d’aperçu qui ne changent jamais, un ciblage d’audience facultatif et une création de rapports d’AQ qui restent segmentés à partir des données d’activité actives. L’AQ des activités vous permet de tester entièrement votre [!DNL Target] activités avant de les lancer en direct.<p>Voir [Compatibilité du mode AQ de la bibliothèque JavaScript Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) et [URL d’aperçu](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics pour Target] (A4T) est une intégration intersolutions qui vous permet de créer des activités basées sur des [!DNL Analytics] mesures de conversion et segments d’audience. Cette intégration A4T vous permet d’utiliser les rapports Analytics pour étudier vos résultats.<p>Voir [Types d’activité pris en charge](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) et [Étapes de mise en oeuvre d’une mise en oeuvre SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Audiences](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Audiences dans [!DNL Target] déterminer qui voit le contenu et les expériences dans une activité ciblée ;<p>Voir [Utilisation de la liste Audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) et [Combinaison de plusieurs audiences](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Création dʼaudiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=fr) | Les audiences créées dans [!DNL Adobe Experience Platform] fournissent des données clientes plus riches et permettent d’offrir une personnalisation plus poussée.<p>Voir [Utilisation des audiences de Adobe Experience Platform](https://experienceleague.adobe.com/docs/?lang=frtarget/using/audiences/create-audiences/audiences.html#aep). |
| [Décisions d’offre](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Ajoutez les décisions d’offre créées dans [!DNL Adobe Journey Optimizer] to [!DNL Target] activités (test A/B manuel ou ciblage d’expérience) afin de déterminer et de proposer la meilleure offre à vos visiteurs sur le web et les appareils mobiles. |
| [FAQ sur les offres de redirection - A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Les offres de redirection provoquent la redirection des navigateurs des visiteurs vers une nouvelle page.<p>Voir [La variable [!UICONTROL SDK Web Adobe Experience Platform] prendre en charge les offres de redirection pour A4T ?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Les jetons de réponse vous permettent d’envoyer [!DNL Target] des données vers des Google Analytics et d’autres intégrations tierces.<p>Voir [Envoi de données à des Google Analytics via le SDK Web Platform](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) pour voir un exemple de code montrant comment effectuer cette tâche. |
| [Implémentation d’applications d’une seule page](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) dans le *[!UICONTROL SDK Web Platform] aperçu* guide. | [!UICONTROL SDK Web Adobe Experience Platform] fournit des fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies côté client de nouvelle génération, telles que les applications d’une seule page (SPA). |
| [Modifications du chiffrement de TLS (Transport Layer Security)](../../before-implement/tls-transport-layer-security-encryption.md) | TLS (Transport Layer Security) vous aide à maintenir les normes de sécurité les plus élevées et à promouvoir la sécurité des données client. |
