---
keywords: confidentialité, adresse ip, géosegmentation, opt-out, opt-out, confidentialité des données, réglementations gouvernementales, réglementations, rgpd, ccpa, confidentialité, informations d’identification personnelle, PII
description: Découvrez comment  [!DNL Adobe Target]  conforme aux lois applicables en matière de confidentialité des données, y compris la collecte et le traitement des adresses IP, des PII et des instructions d’exclusion.
title: Comment Target gère-t-il les problèmes de confidentialité, y compris les informations d’identification personnelles ?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
TQID: https://experienceleague.adobe.com/lEllQscRLJ1I-5mu3r2TyoxYfaOb2nLHVQzG9YnL0ig
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d095671a-1355-40aa-8b5f-06c33c68080bid: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 814
ht-degree: 43%

---

# Confidentialité

Les paramètres et les processus d’[!DNL Adobe Target] vous permettent d’utiliser [!DNL Target] conformément aux lois applicables en matière de confidentialité des données.

## Collecte d’adresses IP et d’informations d’identification personnelle

L’adresse IP d’un visiteur de votre site Web est transmise à un centre de traitement de données Adobe. Selon la configuration réseau du visiteur, l’adresse IP ne représente pas nécessairement l’adresse IP de l’ordinateur du visiteur. Il peut par exemple s’agir de l’adresse IP externe d’un pare-feu NAT (traduction d’adresses réseau), d’un proxy HTTP ou d’une passerelle Internet.

>[!IMPORTANT]
>
>[!DNL Target] ne stocke aucune adresse IP de l’utilisateur ni aucune information d’identification personnelle (PII). Les adresses IP sont utilisées uniquement par les [!DNL Target] pendant la session (en mémoire, jamais conservées).

## Remplacement du dernier octet des adresses IP

Adobe a développé un paramètre de confidentialité dès la conception que les utilisateurs peuvent activer pour Adobe [!DNL Target]. Lorsqu’il est activé, Adobe [!DNL Target] obscurcit immédiatement le dernier octet (la dernière partie) de l’adresse IP au moment où l’adresse IP est collectée. Cette anonymisation a lieu avant le traitement des adresses IP et avant la géolocalisation facultative de l’adresse IP.

Si cette fonction est activée, l’adresse IP est suffisamment anonyme pour ne plus être identifiable en tant qu’information personnelle. Par conséquent, [!DNL Target] peut être utilisé conformément aux lois sur la confidentialité des données dans les pays qui ne permettent pas la collecte d’informations personnelles. L’obtention d’informations sur les villes sera considérablement entravée par l’obscurcissement de l’adresse IP, tandis que l’obtention des informations sur les régions et les pays ne sera que légèrement entravée.

Les paramètres suivants sont disponibles dans l’interface utilisateur de [!DNL Target] en accédant à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** :

* [!UICONTROL Obfuscation du dernier octet] : [!DNL Target] masque le dernier octet de l’adresse IP.
* [!UICONTROL Obfuscation de l’intégralité de l’adresse IP] : [!DNL Target] masque l’intégralité de l’adresse IP.
* [!UICONTROL Aucune] : [!DNL Target] ne masque aucune partie de l’adresse IP.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] reçoit l’adresse IP complète et l’obscurcit (si défini sur « Dernier octet » ou « IP entière ») comme indiqué. [!DNL Target] conserve alors l’adresse IP obscurcie en mémoire uniquement pendant la session en cours.

### Obfuscation des adresses IP au niveau du flux de données lors de l’utilisation de l’[!DNL Adobe Experience Platform Web SDK] {#aep}

Lors de l’utilisation de l’[!DNL Platform Web SDK] (version 23.4 ou ultérieure), le paramètre d’obscurcissement de l’adresse IP au niveau du train de données est prioritaire sur toute option d’obscurcissement d’adresse IP définie dans [!DNL Target]. Par exemple, si l’option d’obscurcissement de l’adresse IP au niveau du train de données est définie sur [!UICONTROL Complet] et l’option d’obscurcissement de l’adresse IP [!DNL Target] sur [!UICONTROL Obfuscation du dernier octet], [!DNL Target] reçoit une adresse IP entièrement obscurcie.

Pour plus d’informations, voir [!UICONTROL Obscurcissement d’IP] dans [Configurer un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=fr){target=_blank} dans le guide des flux de données *[!DNL Adobe Experience Platfrom]*.

## Géosegmentation

Si vous activez le remplacement du dernier octet de l’adresse IP, les valeurs restantes de l’adresse IP peuvent être analysées à l’aide des rapports dans [!DNL Target]. Si le dernier octet de l’adresse IP n’a pas été obscurci, l’adresse IP complète peut être analysée en [!DNL Target]. Vous pouvez utiliser la fonctionnalité de géosegmentation pour dessiner l’emplacement du visiteur par zone géographique. Les données de géosegmentation sont alors détaillées au niveau des villes ou des codes postaux uniquement, mais pas au niveau individuel.

Si les adresses IP sont entièrement obscurcies, la géosegmentation et le géociblage ne sont pas disponible.

## Lien d’exclusion

Vous pouvez ajouter un lien d’exclusion à vos sites pour permettre aux visiteurs de s’exclure de tout comptage et diffusion de contenu.

1. Ajoutez le lien suivant sur votre site :

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Conditionnel) Si vous utilisez CNAME, le lien doit contenir le paramètre « client=`clientcode` » par exemple :
   `https://my.cname.domain/optout?client=clientcode`.

1. Remplacez `clientcode` par votre code client et ajoutez le texte ou l’image à lier à l’URL d’exclusion.

Les visiteurs qui cliquent sur ce client ne sont pas inclus dans les requêtes de mbox appelées à partir de leur session de navigation tant qu’ils ne suppriment par leurs cookies ou pendant une durée de 2 ans, le premier événement prévalant. Ce lien définit un cookie, appelé `disableClient`, pour le visiteur dans le domaine `clientcode.tt.omtrdc.net`.

Même si vous utilisez une implémentation avec cookies propriétaires, l’exclusion par défaut est définie par l’intermédiaire d’un cookie tiers. Si le client utilise uniquement un cookie propriétaire, [!DNL Target] vérifie si un cookie d’exclusion est défini.

## Réglementations relatives à la confidentialité et à la protection des données

Consultez [Règlements relatifs à la confidentialité et à la protection des données](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) pour plus d’informations sur le RGPD (règlement général sur la protection des données), le CCPA (California Consumer Privacy Act) et d’autres exigences internationales en matière de confidentialité, ainsi que sur l’impact de ces règlements sur votre organisation et vos [!DNL Target].

## Collecte de données d’utilisation des fonctionnalités

Les données individuelles d’utilisation des fonctionnalités sont collectées à des fins d’Adobe interne, afin de déterminer si [!DNL Target] fonctionnalités s’exécutent comme prévu ou d’identifier celles qui sont sous-utilisées. Plusieurs mesures de latence sont collectées pour aider à résoudre les problèmes de performances. Les données personnelles ne sont pas collectées.

Vous pouvez exclure les données d’utilisation des rapports dans nos SDK en définissant `telemetryEnabled` sur false dans les options d’initialisation du client. Pour plus d’informations, consultez la section [telemetryEnabled dans targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
