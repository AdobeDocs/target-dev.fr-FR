---
user-guide-title: Guide du développeur d’Adobe Target
breadcrumb-title: Guide du développeur de Target
user-guide-description: Découvrez comment personnaliser l’expérience de vos clients afin de maximiser les recettes de vos sites web et mobiles, de vos applications, de vos médias sociaux et de vos autres canaux numériques.
source-git-commit: 54647001c4e5dc5ce208430c7fea103a720b0980
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 45%

---


# Guide du développeur d’Adobe Target {#developer}

+ [Guide du développeur d’Adobe Target](overview.md)
+ Prise en main {#implementation}
   + Avant l’implémentation {#before-implement}
      + [Avant l’implémentation](before-implement/considerations-before-you-implement-target.md)
      + [Préparation à la mise en œuvre de Target](before-implement/prepare-to-implement-target.md)
   + Confidentialité et sécurité {#privacy}
      + [Vue d’ensemble de la confidentialité](before-implement/privacy/privacy.md)
      + [Réglementations relatives à la confidentialité et à la protection des données](before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)
      + [Cookies Target](before-implement/privacy/cookie-behavior.md)
      + [Suppression du cookie Target](before-implement/privacy/cookie-deleting.md)
      + [Impact de l’obsolescence des cookies tiers sur Target (at.js)](/help/dev/before-implement/privacy/third-party-cookie-deprecation.md)
      + [Politiques de cookie Google Chrome samesite](before-implement/privacy/google-chrome-samesite-cookie-policies.md)
      + [ITP (Intelligent Tracking Prevention) 2.x d’Apple](before-implement/privacy/apple-itp-2x.md)
      + [Directives relatives aux CSP (Content Security Policy, politique de sécurité du contenu)](before-implement/privacy/content-security-policy.md)
      + [Ajout des nœuds Edge de Target sur liste autorisée](before-implement/privacy/allowlist-edges.md)
   + Méthodes de transfert de données dans Target {#methods}
      + [Présentation des méthodes](before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)
      + [Paramètres de page](before-implement/methods-to-get-data-into-target/page-parameters.md)
      + [Attributs de profil sur la page](before-implement/methods-to-get-data-into-target/in-page-profile-attributes.md)
      + [Attributs de profil de script](before-implement/methods-to-get-data-into-target/script-profile-attributes.md)
      + [Fournisseurs de données](before-implement/methods-to-get-data-into-target/data-providers.md)
      + [API de mise à jour des profils en masse](before-implement/methods-to-get-data-into-target/bulk-profile-update-api.md)
      + [API de mise à jour de profil unique](before-implement/methods-to-get-data-into-target/single-profile-update-api.md)
      + [Attributs du client](before-implement/methods-to-get-data-into-target/customer-attributes.md)
      + [Paramètres de l’API de profil](before-implement/methods-to-get-data-into-target/profile-api-settings.md)
   + [Présentation de la sécurité de Target](before-implement/target-security-overview.md)
   + [Navigateurs pris en charge](before-implement/supported-browsers.md)
   + [Modifications du chiffrement de TLS (Transport Layer Security)](before-implement/tls-transport-layer-security-encryption.md)
   + [CNAME et Adobe Target](before-implement/implement-cname-support-in-target.md)
+ Mise en oeuvre côté client {#client-side}
   + [Aperçu : implémentation de Target pour le web côté client](implement/client-side/overview.md)
   + [Mise en oeuvre du SDK Web Adobe Experience Platform - Aperçu](implement/client-side/aep-web-sdk.md)
   + Implémentation d’at.js {#at-js-implementation}
      + [Présentation d’at.js](implement/client-side/atjs/how-atjs-works/overview.md)
      + Fonctionnement d’at.js {#at-js}
         + [Présentation du fichier at.js](implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
         + [Gestion du scintillement par at.js](implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
         + [Intégrations d’at.js](implement/client-side/atjs/how-atjs-works/target-atjs-integrations.md)
      + Déploiement d’at.js {#deploy-at-js}
         + [Déploiement d’at.js](implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)
         + [Implémentation de Target à l’aide d’Adobe Experience Platform](implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)
         + [Mise en œuvre de Target sans gestionnaire de balises](implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)
         + [Mise en œuvre de Target avec Dynamic Tag Management (DTM)](implement/client-side/atjs/how-to-deployatjs/implement-target-using-dtm.md)
         + [Implémentation de Target pour les applications monopages (SPA)](implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)
      + Prise de décision sur l’appareil {#on-device-decisioning}
         + [Présentation de la prise de décision sur l’appareil](implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md)
         + [Fonctionnalités prises en charge](implement/client-side/atjs/on-device-decisioning/supported-features.md)
         + [Artefact de règle](implement/client-side/atjs/on-device-decisioning/rule-artifact.md)
         + [Résolution des problèmes](implement/client-side/atjs/on-device-decisioning/troubleshooting-on-device-decisioning.md)
      + Fonctions d’at.js {#functions-overview}
         + [Présentation des fonctions at.js](implement/client-side/atjs/atjs-functions/atjs-functions.md)
         + [adobe.target.getOffer()](implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)
         + [adobe.target.getOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
         + [adobe.target.applyOffer()](implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)
         + [adobe.target.applyOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)
         + [adobe.target.triggerView() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)
         + [adobe.target.trackEvent()](implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
         + [mboxCreate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)
         + [targetGlobalSettings()](implement/client-side/atjs/atjs-functions/targetglobalsettings.md)
         + [mboxDefine () et mboxUpdate () - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)
         + [targetPageParams()](implement/client-side/atjs/atjs-functions/targetpageparams.md)
         + [targetPageParamsAll()](implement/client-side/atjs/atjs-functions/targetpageparamsall.md)
         + [registerExtension () - at.js 1.x](implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)
         + [sendNotifications() - at.js 2.1](implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)
         + [événements personnalisés at.js](implement/client-side/atjs/atjs-functions/atjs-custom-events.md)
         + [Déboguer at.js à l’aide du débogueur Adobe Experience Cloud](implement/client-side/target-debugging-atjs/target-debugging-atjs.md)
         + [Utilisation d’instances basées sur le cloud avec Target](implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)
      + [Questions fréquentes sur at.js](implement/client-side/atjs/target-atjs-faq.md)
      + [Informations détaillées sur les versions du fichier at.js](implement/client-side/atjs/target-atjs-versions.md)
      + [Mise à niveau d’at.js 1.x vers at.js 2.x](implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)
      + [cookies at.js](implement/client-side/atjs/atjs-cookies.md)
   + [Conseils sur l’agent utilisateur et le client](implement/client-side/atjs/user-agent-and-client-hints.md)
   + Présentation de la mbox globale {#global-mbox}
      + [Présentation de la mbox globale](implement/client-side/atjs/global-mbox/global-mbox-overview.md)
      + [Personnalisation d’une mbox globale](implement/client-side/atjs/global-mbox/customize-global-mbox.md)
      + [Utilisation d’une mbox globale à partir d’une implémentation héritée](implement/client-side/atjs/global-mbox/mbox-global-target-standard.md)
      + [Transfert de paramètres vers une mbox globale](implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)
      + [Questions fréquentes relatives aux mboxes globales](implement/client-side/atjs/global-mbox/global-mbox-faq.md)
+ Mise en oeuvre côté serveur {#server-side}
   + [Aperçu de l’implémentation de Target côté serveur](implement/server-side/server-side-overview.md)
   + [Prise en main des SDK Target](implement/server-side/sdk-guides/getting-started/getting-started.md)
   + [Exemples d’applications](implement/server-side/sdk-guides/sample-apps/sample-apps.md)
   + [Transition des API héritées de Target vers Adobe I/O](implement/server-side/transition-from-target-classic-apis.md)
   + Principes fondamentaux {#core-principles}
      + [Présentation des principes de base](implement/server-side/sdk-guides/core-principles/overview.md)
      + [Identifiant utilisateur et regroupement](implement/server-side/sdk-guides/core-principles/user-identification-and-bucketing.md)
      + [Ciblage de l’audience](implement/server-side/sdk-guides/core-principles/audience-targeting.md)
      + [Suivi des événements](implement/server-side/sdk-guides/core-principles/event-tracking.md)
      + [Autorisations et propriétés des utilisateurs](implement/server-side/sdk-guides/core-principles/user-permissions-and-properties.md)
   + Intégration {#integration}
      + [Présentation de l’intégration](implement/server-side/sdk-guides/integration-with-experience-cloud/overview.md)
      + [Service d’ID Experience Cloud (ECID)](implement/server-side/sdk-guides/integration-with-experience-cloud/ecid.md)
      + [Rapports Analytics for Target (A4T)](implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md)
      + [Segments AAM](implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md)
   + Prise de décision sur appareil {#on-device-decisioning}
      + [Présentation de la prise de décision sur l’appareil](implement/server-side/sdk-guides/on-device-decisioning/overview.md)
      + Artefact de règle {#rule-artifact}
         + [Aperçu de l’artefact de règle](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)
         + [Téléchargement via le SDK Adobe Target](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-sdk.md)
         + [Téléchargement via la payload JSON](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-json.md)
         + [Exemple d’artefact de règle](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-example.md)
      + [Exécution de tests A/B avec des indicateurs de fonctionnalité](implement/server-side/sdk-guides/on-device-decisioning/execute-ab-tests-with-feature-flags.md)
      + [Exécution de tests de fonctionnalités avec des attributs](implement/server-side/sdk-guides/on-device-decisioning/execute-feature-tests-with-attributes.md)
      + [Gestion des déploiements pour les tests de fonctionnalités](implement/server-side/sdk-guides/on-device-decisioning/manage-rollouts-for-feature-tests.md)
      + [Personnalisation de la diffusion](implement/server-side/sdk-guides/on-device-decisioning/deliver-personalization.md)
      + [Présentation des fonctionnalités prises en charge](implement/server-side/sdk-guides/on-device-decisioning/supported-features.md)
      + [Dépannage de la prise de décision sur appareil](implement/server-side/sdk-guides/on-device-decisioning/troubleshooting.md)
      + [Bonnes pratiques](implement/server-side/sdk-guides/best-practices/best-practices.md)
   + Référence du SDK Node.js {#node-js}
      + [Présentation du SDK Node.js](implement/server-side/node-js/overview.md)
      + [Installation du SDK Node.js](implement/server-side/node-js/install-sdk.md)
      + [Initialisation du SDK Node.js](implement/server-side/node-js/initialize-sdk.md)
      + [Obtention d’offres (Node.js)](implement/server-side/node-js/get-offers.md)
      + [Obtention d’attributs (Node.js)](implement/server-side/node-js/get-attributes.md)
      + [Envoi de notifications (Node.js)](implement/server-side/node-js/send-notifications.md)
      + [Événements SDK (Node.js)](implement/server-side/node-js/sdk-events.md)
      + [Enregistreur (Node.js)](implement/server-side/node-js/logger.md)
      + [Configuration du proxy (Node.js)](implement/server-side/node-js/proxy-configuration.md)
   + Référence du SDK Java {#java}
      + [Présentation du SDK Java](implement/server-side/java/overview.md)
      + [Installation du SDK Java](implement/server-side/java/install-sdk.md)
      + [Initialisation du SDK Java](implement/server-side/java/initialize-sdk.md)
      + [Obtention d’offres (Java)](implement/server-side/java/get-offers.md)
      + [Obtenir des attributs (Java)](implement/server-side/java/get-attributes.md)
      + [Envoi de notifications (Java)](implement/server-side/java/send-notifications.md)
      + [Événements SDK (Java)](implement/server-side/java/sdk-events.md)
      + [Enregistreur (Java)](implement/server-side/java/logger.md)
      + [Requêtes asynchrones (Java)](implement/server-side/java/asynchronous-requests.md)
      + [Configuration du proxy (Java)](implement/server-side/java/proxy-configuration.md)
      + [Configuration client HTTP personnalisée (Java)](implement/server-side/java/custom-http-client.md)
      + [Méthodes d’utilitaire (Java)](implement/server-side/java/utility-methods.md)
   + Référence du SDK .NET {#net}
      + [Présentation du SDK .NET](implement/server-side/net/overview.md)
      + [Installation du SDK .Net](implement/server-side/net/install-sdk.md)
      + [Initialisation du SDK .NET](implement/server-side/net/initialize-sdk.md)
      + [Obtention d’offres (.NET)](implement/server-side/net/get-offers.md)
      + [Obtention des attributs (.NET)](implement/server-side/net/get-attributes.md)
      + [Envoi de notifications (.NET)](implement/server-side/net/send-notifications.md)
      + [Événements SDK (.NET)](implement/server-side/net/sdk-events.md)
      + [Requêtes asynchrones (.NET)](implement/server-side/net/asynchronous-requests.md)
   + Référence du SDK Python {#python}
      + [Présentation du SDK Python](implement/server-side/python/overview.md)
      + [Installation du SDK Python](implement/server-side/python/install-sdk.md)
      + [Initialisation du SDK Python](implement/server-side/python/initialize-sdk.md)
      + [Obtention d’offres (Python)](implement/server-side/python/get-offers.md)
      + [Obtenir des attributs (Python)](implement/server-side/python/get-attributes.md)
      + [Envoyer des notifications (Python)](implement/server-side/python/send-notifications.md)
      + [Événements SDK (Python)](implement/server-side/python/sdk-events.md)
      + [Requêtes asynchrones (Python)](implement/server-side/python/asynchronous-requests.md)
      + [Enregistreur (Python)](implement/server-side/python/logger.md)
+ [Implémentation hybride](implement/hybrid/hybrid-overview.md)
+ [Implémentation Recommendations](implement/recommendations/recommendations.md)
+ Mise en oeuvre des applications mobiles {#mobile-apps}
   + [Target pour les applications mobiles](implement/mobile/overview.md)
   + [Aperçu de Target Mobile](implement/mobile/target-mobile-preview.md)
   + [Utilisation du service de localisation](implement/mobile/use-location-service.md)
   + [FAQ sur Target pour les applications mobiles](implement/mobile/mobile-faq.md)
   + [Mise en oeuvre de Target avec le SDK AEP Mobile dans une application native avec des vues web](/help/dev/implement/mobile/native-app.md)
+ Implémentation par email {#implement-email}
   + [Message électronique : implémentation de Target](implement/email/overview.md)
   + [Création d’une adbox pour une image](implement/email/testing-content-with-the-adbox.md)
   + [Test d’une adbox d’image de courrier électronique](implement/email/testing-email-image-adbox.md)
   + [Fonctionnement avec un redirecteur](implement/email/working-with-redirectors.md)
+ Guides d’API {#api}
   + [Présentation de l’API Target](/help/dev/before-administer/target-api-overview.md)
   + [Configuration de l’authentification pour les API Target](/help/dev/before-administer/configure-authentication.md)
   + Guide de l’API de diffusion {#delivery-api}
      + [Présentation de l’API de diffusion](/help/dev/implement/delivery-api/overview.md)
      + [SDK pour interagir avec l’API de diffusion](/help/dev/before-implement/delivery-api-overview/sdks.md)
      + [Prise en main](/help/dev/before-implement/delivery-api-overview/getting-started.md)
      + [Autorisations utilisateur (Premium)](/help/dev/before-implement/delivery-api-overview/user-permissions.md)
      + [Identification des visiteurs](/help/dev/before-implement/delivery-api-overview/identifying-visitors.md)
      + [Diffusion unique ou par lots](/help/dev/before-implement/delivery-api-overview/single-or-batch.md)
      + [Prérécupération](/help/dev/before-implement/delivery-api-overview/prefetch.md)
      + [Notifications](/help/dev/before-implement/delivery-api-overview/notifications.md)
      + [Intégration à Experience Cloud](before-implement/delivery-api-overview/integration.md)
      + [Considérations et limites connues](/help/dev/before-implement/delivery-api-overview/known-limitations.md)
      + [Conseils au client](/help/dev/before-implement/delivery-api-overview/client-hints.md)
      + [API de diffusion](/help/dev/implement/delivery-api/delivery-api.md)
   + API d’administration {#admin-api}
      + [API d’administration - Aperçu](before-administer/admin-api-overview/admin-api-overview.md)
      + [API d’administration Adobe Target](/help/dev/administer/admin-api/admin-api-overview-new.md)
   + API de profil {#profile-apis}
      + [Présentation de l’API Profiles](/help/dev/administer/profile-api/profiles-api.md)
      + [Récupération de profils](/help/dev/administer/profile-api/profile-fetch.md)
      + [Mettre à jour les profils](/help/dev/administer/profile-api/profile-api-overview.md)
      + [API de mise à jour de profil unique](/help/dev/administer/profile-api/profile-single-api.md)
      + [API de mise à jour des profils en masse](/help/dev/administer/profile-api/profile-bulk-api.md)
   + [API de création de rapports](/help/dev/administer/reporting-api/reporting-api.md)
   + API RECOMMENDATIONS {#recommendations-api}
      + [Présentation de l’API Recommendations](before-administer/recs-api/overview.md)
      + [Gestion de votre catalogue avec les API](before-administer/recs-api/manage-catalog.md)
      + [Gestion des critères personnalisés](before-administer/recs-api/manage-custom-criteria.md)
      + [Utilisation de l’API de diffusion avec Recommendations](before-administer/recs-api/fetch-recs-server-side-delivery-api.md)
      + [API RECOMMENDATIONS](/help/dev/administer/recommendations-api/recommendations-api.md)
   + API de modèles {#models-api}
      + [Présentation de l’API Modèles (Liste bloquée)](before-administer/models-api.md)
      + [API de modèles](/help/dev/administer/models-api/models-api-overview.md)
   + [API ADOBE ADMIN CONSOLE](/help/dev/before-implement/delivery-api-overview/adobe-console-api.md)
   + [API du serveur réseau Adobe Experience Platform Edge](/help/dev/before-implement/delivery-api-overview/aep-edge-network-server-api.md)
+ Modèles de mise en oeuvre {#implementation-patterns}
   + [Présentation des modèles d’implémentation](/help/dev/patterns/pattern-overview.md)
   + Modèle de mise en oeuvre Recommendations à l’aide d’at.js {#atjs}
      + [Modèle de mise en oeuvre Recommendations à l’aide de la présentation d’at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md)
      + [Initialisation des SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
      + [Configuration de la collecte de données](/help/dev/patterns/recs-atjs/data-collection.md)
      + [Rendu d’expériences](/help/dev/patterns/recs-atjs/render-experiences.md)
      + [Notifier Target](/help/dev/patterns/recs-atjs/notify-target.md)


