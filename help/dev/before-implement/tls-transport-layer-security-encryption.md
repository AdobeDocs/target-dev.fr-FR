---
keywords: tls, tls 1.0, transport layer security, encryption, tls 1.1, tls 1.2
description: Découvrez comment  [!DNL Target] utilise le protocole TLS (Transport Layer Security) pour maintenir les normes de sécurité les plus élevées et promouvoir la sécurité de vos données client.
title: Comment  [!DNL Target] utilise-t-il TLS pour assurer la sécurité ?
feature: Privacy & Security
exl-id: f5ea2272-27ab-49c9-b096-b15dd277d4e5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 49%

---

# Modifications du chiffrement de TLS (Transport Layer Security)

Informations sur les modifications apportées à la manière dont [!DNL Adobe] et [!DNL Adobe Target] utilisent TLS (Transport Layer Security) pour maintenir les normes de sécurité les plus élevées et promouvoir la sécurité des données client.

Transport Layer Security (TLS) est le protocole de sécurité le plus répandu utilisé aujourd’hui pour les navigateurs web et autres applications exigeant que les données soient échangées en toute sécurité sur un réseau. Adobe applique des normes de conformité de sécurité qui exigent la fin de vie des protocoles plus anciens et impose l’utilisation de TLS 1.2 afin d’avoir la version la plus récente et la plus sécurisée en usage.

>[!WARNING]
>
>À compter du 1er mars 2020, [!DNL Target] ne prendra plus en charge le chiffrement TLS 1.1 pour le compositeur d’expérience visuelle (VEC), le compositeur d’expérience avancé (EEC), la diffusion d’activité, les API, etc. Mettez à niveau vers TLS 1.2 pour éviter tout problème.

Cette modification ne devrait pas avoir de répercussions importantes sur les données des clients ou le compte rendu des performances.

## Compositeur d’expérience visuelle (VEC) avec Compositeur d’expérience avancé activé

TLS 1.2 est la valeur par défaut à partir du 1er mars 2020 et TLS 1.1 ne sera plus pris en charge.

Adobe fera passer les clients de manière progressive à TLS 1.2. Pour ceux dont les domaines sont déjà conformes à la version 1.2, nous les déplacerons vers TLS 1.2 sans que vous ayez à apporter une modification. La plupart des domaines de clients prennent déjà en charge TLS 1.2. Cependant, si votre domaine ne prend pas en charge TLS 1.2, nous conserverons ces domaines sur TLS 1.1 comme aujourd’hui (jusqu’à mars 2020).

Aucun problème ne devrait se poser pendant cette phase de migration. Si le VEC a arrêté de charger un site qui fonctionnait auparavant, [ouvrez un ticket d’assistance clientèle](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C) en citant cette migration comme une cause possible.

Si, cependant, vous êtes l’un de ces clients qui sont sur TSL 1.1 sans prendre en charge TLS 1.2, alors vous devez planifier le déplacement de vos domaines/infrastructure vers TLS 1.2. Nous continuerons à prendre en charge le protocole TLS 1.1 jusqu’au lundi 1 mars 2020. À compter du 1er mars 2020, [!DNL Target] ne prendra plus en charge le protocole TLS 1.1 à utiliser pour le VEC via la fonctionnalité du compositeur d’expérience avancé.

Bien que nous recommandions fortement à tout le monde de travailler avec TLS 1.2 à l’avenir, si vous êtes un nouveau client, mais que vous ne prenez *PAS* en charge TLS 1.2, veuillez contacter l’assistance clientèle pour l’informer que vous devez être sur TLS 1.1 pour le Compositeur d’expérience avancé. Cependant, veuillez prévoir de passer à TLS 1.2, car la prise en charge ne sera plus disponible d’ici le lundi 1 mars 2020.

## Diffusion d’activité

À compter du 1er mars 2020, les serveurs [!DNL Target] ne prendront plus en charge TLS 1.1. Avec cette modification, les serveurs [!DNL Target] n’accepteront plus les demandes des visiteurs disposant d’appareils ou de navigateurs web plus anciens qui ne prennent pas en charge TLS 1.2 (ou version ultérieure). De ce fait, les appareils et navigateurs plus anciens prenant uniquement en charge TLS 1.1 (ou prenant en charge TLS 1.1 par défaut) ne recevront pas de contenu d’activité d’Adobe Target. Le contenu par défaut du site sera rendu.

Certains des anciens appareils et navigateurs qui seront affectés incluent :

* Google Chrome (Chrome pour Android) versions 29 et antérieures
* Opera Browser (Opera Mobile) versions 12.17 et antérieures
* Mozilla Firefox (Firefox pour Mobile) versions 26 et antérieures
* Android 4.3 et versions antérieures
* Internet Explorer 8-10 sous Windows 7 et versions antérieures
* Internet Explorer 10 sous Windows Phone 8.0
* Safari 6.0.4/OS X 10.8.4 et versions antérieures.

Lorsque vous planifiez ce changement, tenez compte de ce qui suit (notez que l’échéance du lundi 1 mars 2020 a une incidence sur tous ces éléments) :

* Vous devez vous assurer que votre site par défaut est prêt à être utilisé avec les appareils et navigateurs conformes.
* Gardez à l’esprit que le nombre de visiteurs dans vos rapports [!DNL Target] peut potentiellement voir une baisse insignifiante du nombre de visiteurs.
* Vous devrez peut-être modifier les audiences créées spécifiquement pour cibler les appareils ou navigateurs plus anciens qui ne prennent pas en charge TLS 1.2. La diffusion vers ces appareils et navigateurs ne fonctionnera plus.

Pour plus d’informations sur les navigateurs pris en charge et leurs versions, voir [Navigateurs pris en charge](supported-browsers.md).

## [!DNL Adobe Target] API

À compter du 1er mars 2020, les API [!DNL Target] ne prendront plus en charge le chiffrement TLS 1.1. Les clients qui accèdent à l’API doivent vérifier qu’ils ne seront pas affectés.

* Les clients API utilisant Java 7 avec les paramètres par défaut devront être modifiés pour prendre en charge TLS 1.2. Pour plus d’informations, voir &quot; [Modification de la version par défaut du protocole TLS pour les points de terminaison clients : TLS 1.0 à TLS 1.2](https://www.java.com/en/configure_crypto.html)&quot; sur le site web Java.
* Les clients d’API utilisant Java 8 ne devraient pas être affectés, étant donné que TLS 1.2 est la configuration par défaut.
* Les clients API utilisant d’autres structures devront contacter leurs fournisseurs pour plus de détails sur la prise en charge de TLS 1.2.

## Accès aux interfaces de solutions Experience Cloud

Comme l’interface [!DNL Target] Standard/Premium nécessite déjà un [navigateur Web moderne](supported-browsers.md), nous ne prévoyons pas de problèmes. Si vous ne parvenez pas à vous connecter à Target, mettez à niveau votre navigateur vers la version la plus récente.

## Comment vérifier quelle version de TLS votre navigateur utilise

Pour vérifier la version TLS de votre site web à l’aide de Google Chrome :

1. Ouvrez le site web concerné dans Chrome.
1. Dans le menu Chrome (les trois points alignés verticalement), cliquez sur Autres outils > Outils de développement.

   ![Chrome Developer Tools](assets/chrome-developer-tools.png)

1. Ouvrez l’onglet Sécurité , puis examinez les informations de version TLS sous Connexion :

   ![Détails de la version TLS](assets/chrome-tls-version.png)

>[!NOTE]
>
>Ces instructions sont à jour à compter de la publication et peuvent faire l’objet de modifications. Une recherche rapide sur Internet devrait vous aider si ces instructions changent. D’autres navigateurs ont des étapes similaires.

## Comportement attendu des navigateurs prenant en charge les versions de TLS antérieures à 1.2

Cette section décrit ce à quoi s’attendre avec les navigateurs qui prennent en charge les versions de TLS antérieures à la version 1.2 uniquement lors de l’utilisation d’une implémentation d’at.js. À des fins de comparaison, cette section décrit également ce à quoi s’attendre avec les navigateurs qui prennent en charge TLS 1.2.

### Points de terminaison centraux

| [!DNL Target] Mise en oeuvre de JavaScript | Détails |
|--- |--- |
| at.js | Avec TLS 1.0 ou TLS 1.1 activé :<ul><li>Lors de l’utilisation des outils de développement du navigateur, « 200 OK » s’affiche sur l’onglet réseau. Cela indique le succès de la requête.</li><li>Le message « Impossible d’établir une connexion sécurisée. » s’affiche. Ce message indique que les paramètres de sécurité TLS du site sont peut-être obsolètes ou risqués.</li><li>Aucune erreur ne s’affiche dans la console.</li></ul>Avec TLS 1.2 activé :<ul><li>Téléchargement du fichier at.js.</li></ul> |

### Points de terminaison Edge

| [!DNL Target] Mise en oeuvre de JavaScript | Détails |
|--- |--- |
| SDK Web Adobe Experience Platform | Avec TLS 1.0 ou TLS 1.1 activé :<ul><li>Lors de l’utilisation des outils de développement du navigateur, « 200 OK » s’affiche sur l’onglet réseau. Cela indique le succès de la requête.</li><li>Le message « Impossible d’établir une connexion sécurisée. » s’affiche. Ce message indique que les paramètres de sécurité TLS du site sont peut-être obsolètes ou risqués.</li><li>Aucune erreur ne s’affiche dans la console.</li><li>Le contenu par défaut est présenté.</li></ul>Avec TLS 1.2 activé :<ul><li>Le contenu des offres est présenté.</li></ul> |
| at.js | Avec TLS 1.0 ou TLS 1.1 activé :<ul><li>Lors de l’utilisation des outils de développement du navigateur, « 200 OK » s’affiche sur l’onglet réseau. Cela indique le succès de la requête.</li><li>Le message « Impossible d’établir une connexion sécurisée. » s’affiche. Ce message indique que les paramètres de sécurité TLS du site sont peut-être obsolètes ou risqués.</li><li>Aucune erreur ne s’affiche dans la console.</li><li>Le contenu par défaut est présenté.</li></ul>Avec TLS 1.2 activé :<ul><li>Le contenu des offres est présenté.</li></ul> |

### Activité ciblée avec une audience de version de navigateur (Internet Explorer, versions 6, 7 ou 8)

Les audiences ne fonctionnent plus.

| [!DNL Target] Mise en oeuvre de JavaScript | Détails |
|--- |--- |
| SDK Web Adobe Experience Platform | Le SDK Platform n’est pas pris en charge sur les versions d’Internet Explorer antérieures à la version 10. |
| at.js | at.js n’est pas pris en charge par les versions antérieures à Internet Explorer 10. |
