---
keywords: Navigateurs, conditions préalables, exigences, internet explorer, chrome, firefox, safari, android, surface, navigateurs0
description: Découvrez quels navigateurs Internet  [!DNL Adobe Target]  prennent en charge pour son interface et pour la diffusion de contenu.
title: Quels Navigateurs  [!DNL Target] prend-il en charge ?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 26%

---

# Navigateurs pris en charge

L’application [!DNL Adobe Target] et la diffusion de contenu ont été testées sur un large éventail de navigateurs et d’appareils.

Pour plus d’informations importantes sur TLS, voir [Modifications du chiffrement de TLS (Transport Layer Security)](tls-transport-layer-security-encryption.md).

## [!DNL Target] Interface Standard/Premium

L’interface [!DNL Target] prend en charge les navigateurs et les périphériques suivants :

| Type d&#39;appareil | Version du navigateur |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome (dernière version, dernière version moins 1)</li><li>Mozilla Firefox (dernière version, dernière version moins 1)</li></ul> |
| Mac | <ul><li>Firefox (dernière version, dernière version moins 1)</li><li>Chrome (dernière version, dernière version moins 1)</li></ul> |

## Diffusion de contenu

La diffusion de contenu a été testée sur les navigateurs et les périphériques suivants :

| Type d&#39;appareil | Version du navigateur |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 et 10. Testé en mode d’émulation. **Remarque** : La diffusion de contenu sur IE 9 n’est plus prise en charge avec at.js 1.3.0 (et versions ultérieures). La diffusion de contenu sur IE 10, 11 et toutes les versions antérieures n’est plus prise en charge avec at.js 2.5.0 (et versions ultérieures).</li><li>Internet Explorer 11. **Remarque** : La diffusion de contenu sur IE 10, 11 et toutes les versions antérieures n’est plus prise en charge avec at.js 2.5.0 (et versions ultérieures).</li><li>Microsoft Edge</li><li>Chrome (dernière version, dernière version moins 1)</li><li>Firefox (dernière version, dernière version moins 1)</li></ul> |
| Mac | <ul><li>Apple Safari (dernière version). **Remarque** : Pour plus d’informations sur la manière dont Safari traite les cookies propriétaires et tiers, voir [Cookie Target](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (dernière version, dernière version moins 1)</li><li>Chrome (dernière version, dernière version moins 1)</li></ul> |
| Mobile/Tablette | <ul><li>Apple iOS (dernière version)</li><li>Appareils et tablettes Android (Android 4 et versions ultérieures)</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

Notez les points suivants :

* Pour les implémentations d’at.js, [!DNL Target] affiche le contenu par défaut dans les versions antérieures d’Internet Explorer, ainsi que éventuellement dans les versions antérieures des navigateurs susmentionnés.
* Internet Explorer traite tous les éléments inconnus (tels que les éléments personnalisés) comme un même type d’élément. Par conséquent, la diffusion ne fonctionne pas avec les éléments personnalisés.
* [!DNL Target] affiche le contenu par défaut dans les navigateurs non répertoriés ci-dessus et dans les navigateurs utilisant le [mode quirks](https://en.wikipedia.org/wiki/Quirks_mode). at.js nécessite un doctype qui présente le contenu en mode standard, tel que : `<!DOCTYPE html>`
* [!DNL Adobe] L’infrastructure de diffusion est sécurisée pour NE PAS prendre en charge les appareils et navigateurs TLS 1.0 après le 12 septembre 2018. Veuillez consulter la section [Modifications du chiffrement de TLS (Transport Layer Security)](../before-implement/tls-transport-layer-security-encryption.md) pour comprendre l’impact global de cette modification.
