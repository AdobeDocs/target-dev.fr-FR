---
keywords: Navigateurs, Conditions préalables, Conditions requises, Internet Explorer, chrome, firefox, safari, android, surface, Navigateurs0
description: Découvrez les navigateurs Internet pris  [!DNL Adobe Target]  charge pour son interface et pour la diffusion de contenu.
title: Quels Navigateurs Est [!DNL Target] Il Pris En Charge ?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: f194c6de43070443b78c9a69b4233c27d70b8858
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 23%

---

# Navigateurs pris en charge

L’application [!DNL Adobe Target] et la diffusion de contenu ont été testées sur un large éventail de navigateurs et d’appareils.

Pour obtenir des informations plus importantes sur le protocole TLS, voir [Modifications du chiffrement TLS (Transport Layer Security)](tls-transport-layer-security-encryption.md).

## Interface [!DNL Target] Standard/Premium

L’interface [!DNL Target] prend en charge les navigateurs et appareils suivants :

| Type d&#39;appareil | Version du navigateur |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome (dernier, dernier moins 1)</li><li>Mozilla Firefox (le plus récent, le plus récent moins 1)</li></ul> |
| Mac | <ul><li>Firefox (le plus récent, le plus récent moins 1)</li><li>Chrome (la plus récente, la plus récente moins 1)</li></ul> |

## Diffusion de contenu

La diffusion de contenu a été testée sur les navigateurs et les périphériques suivants :

| Type d&#39;appareil | Version du navigateur |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 et 10. Testé en mode d’émulation. **Remarque** : la diffusion de contenu sur IE 9 n’est plus prise en charge avec at.js 1.3.0 et les versions ultérieures. La diffusion de contenu sur IE 10, 11 et toutes les versions antérieures n’est plus prise en charge avec at.js 2.5.0 et les versions ultérieures.</li><li>Internet Explorer 11. **Remarque** : la diffusion de contenu sur IE 10, 11 et toutes les versions antérieures n’est plus prise en charge avec at.js 2.5.0 (et versions ultérieures).</li><li>Microsoft Edge</li><li>Chrome (la plus récente, la plus récente moins 1)</li><li>Firefox (le plus récent, le plus récent moins 1)</li></ul> |
| Mac | <ul><li>Apple Safari (la plus récente). **Remarque** : pour plus d’informations sur la façon dont Safari gère les cookies propriétaires et tiers, voir [Cookie Target](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (le plus récent, le plus récent moins 1)</li><li>Chrome (la plus récente, la plus récente moins 1)</li></ul> |
| Mobile/Tablette | <ul><li>Apple iOS (la plus récente)</li><li>Appareils et tablettes Android (Android 4 et versions ultérieures)</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

Notez ce qui suit :

* Le [!DNL Adobe Experience Platform Web SDK] est conçu pour fonctionner de manière optimale avec les dernières versions d’[!DNL Google Chrome], [!DNL Safari], [!DNL Firefox] et [!DNL Microsoft Edge Chromium]. Vous rencontrerez peut-être des problèmes pour utiliser certaines fonctionnalités sur les versions plus anciennes de ces navigateurs ou sur les navigateurs obsolètes, tels que [!DNL Internet Explorer].
* Pour les implémentations d’at.js, [!DNL Target] affiche le contenu par défaut dans les versions antérieures d’Internet Explorer et, éventuellement, dans les versions antérieures des navigateurs répertoriés ci-dessus.
* Internet Explorer traite tous les éléments inconnus (tels que les éléments personnalisés) comme un même type d’élément. Par conséquent, la diffusion ne fonctionne pas avec les éléments personnalisés.
* [!DNL Target] affiche le contenu par défaut dans les navigateurs non répertoriés ci-dessus et dans les navigateurs utilisant [mode quirks](https://en.wikipedia.org/wiki/Quirks_mode). at.js nécessite un doctype qui présente le contenu en mode standard, tel que : `<!DOCTYPE html>`
* L’infrastructure de diffusion [!DNL Adobe] est sécurisée afin de NE PAS prendre en charge les appareils et navigateurs TLS 1.0 après le 12 septembre 2018. Veuillez consulter la section [Modifications du chiffrement de TLS (Transport Layer Security)](../before-implement/tls-transport-layer-security-encryption.md) pour comprendre l’impact global de cette modification.
