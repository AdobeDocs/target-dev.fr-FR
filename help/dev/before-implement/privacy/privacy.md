---
keywords: confidentialité, adresse ip, géosegmentation, opt-out, opt-out, opt-out, confidentialité des données, réglementations gouvernementales, gdpr, ccpa, confidentialité, informations d’identification personnelles, PII
description: Découvrez comment  [!DNL Adobe Target] est conforme aux lois applicables sur la confidentialité des données, notamment la collecte et le traitement des adresses IP, des informations d’identification personnelles et des instructions d’exclusion.
title: Comment Target gère-t-il les problèmes de confidentialité, y compris les informations d’identification personnelles ?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: 88bde40aa6dfb96e1d53e4db6ba5547d38dbbb99
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 43%

---

# Confidentialité

Les paramètres et les processus d’[!DNL Adobe Target] vous permettent d’utiliser [!DNL Target] conformément aux lois applicables en matière de confidentialité des données.

## Collecte d’adresses IP et d’informations d’identification personnelle (PII)

L’adresse IP d’un visiteur de votre site Web est transmise à un centre de traitement de données Adobe. Selon la configuration réseau du visiteur, l’adresse IP ne représente pas nécessairement l’adresse IP de l’ordinateur du visiteur. Il peut par exemple s’agir de l’adresse IP externe d’un pare-feu NAT (traduction d’adresses réseau), d’un proxy HTTP ou d’une passerelle Internet.

>[!IMPORTANT]
>
>[!DNL Target] ne stocke aucune adresse IP de l’utilisateur ni aucune information d’identification personnelle (PII). Les adresses IP ne sont utilisées que par [!DNL Target] pendant la session (en mémoire, jamais conservée).

## Remplacement du dernier octet des adresses IP

Adobe a développé un paramètre de &quot;confidentialité par conception&quot; que les utilisateurs peuvent activer pour l’Adobe [!DNL Target]. Lorsqu&#39;il est activé, l&#39;Adobe [!DNL Target] obscurcit immédiatement le dernier octet (la dernière partie) de l&#39;adresse IP au moment de la collecte de l&#39;adresse IP. Cette anonymisation a lieu avant le traitement des adresses IP et avant la géolocalisation facultative de l’adresse IP.

Si cette fonction est activée, l’adresse IP est suffisamment anonyme pour ne plus être identifiable en tant qu’information personnelle. Par conséquent, [!DNL Target] peut être utilisé conformément aux lois sur la confidentialité des données dans les pays qui n’autorisent pas la collecte d’informations personnelles. L’obtention d’informations sur les villes sera considérablement entravée par l’obscurcissement de l’adresse IP, tandis que l’obtention des informations sur les régions et les pays ne sera que légèrement entravée.

Les paramètres suivants sont disponibles dans l’interface utilisateur de [!DNL Target] en accédant à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** :

* [!UICONTROL Last octet obfuscation] : [!DNL Target] masque le dernier octet de l’adresse IP.
* [!UICONTROL Entire IP obfuscation] : [!DNL Target] masque l’adresse IP entière.
* [!UICONTROL None] : [!DNL Target] ne masque aucune partie de l’adresse IP.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] reçoit l’adresse IP complète et l’obscurcit (s’il est défini sur le dernier octet ou l’IP entière) comme spécifié. [!DNL Target] contient ensuite l’adresse IP obscurcie en mémoire uniquement pendant la session en cours.

### Obscurcissement de l’adresse IP au niveau du flux de données lors de l’utilisation de [!DNL Adobe Experience Platform Web SDK] {#aep}

Lors de l’utilisation de [!DNL Platform Web SDK] (version 23.4 ou ultérieure), le paramètre d’obscurcissement de l’adresse IP au niveau du flux de données est prioritaire sur toute option d’obscurcissement de l’adresse IP définie dans [!DNL Target]. Par exemple, si l’option d’obscurcissement de l’adresse IP au niveau du flux de données est définie sur [!UICONTROL Full] et que l’option d’obscurcissement de l’adresse IP [!DNL Target] est définie sur [!UICONTROL Last octet obfuscation], [!DNL Target] reçoit une adresse IP entièrement obscurcie.

Pour plus d’informations, voir [!UICONTROL IP Obfuscation] dans [Configuration d’un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=fr){target=_blank} dans le *[!DNL Adobe Experience Platfrom]Guide des flux de données*.

## Géosegmentation

Si vous activez le remplacement du dernier octet de l’adresse IP, les valeurs restantes de l’adresse IP peuvent être analysées à l’aide de rapports dans [!DNL Target]. Si le dernier octet de l’adresse IP n’a pas été obscurci, l’adresse IP complète peut être analysée dans [!DNL Target]. Vous pouvez utiliser la fonctionnalité de géosegmentation pour dessiner l’emplacement du visiteur par zone géographique. Les données de géosegmentation sont alors détaillées au niveau des villes ou des codes postaux uniquement, mais pas au niveau individuel.

Si les adresses IP sont entièrement obscurcies, la géosegmentation et le géociblage ne sont pas disponible.

## Lien d’exclusion

Vous pouvez ajouter un lien d’exclusion à vos sites pour permettre aux visiteurs de s’exclure de tout comptage et diffusion de contenu.

1. Ajoutez le lien suivant sur votre site :

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Conditionnel) Si vous utilisez CNAME, le lien doit contenir le paramètre &quot;client=`clientcode`&quot;, par exemple :
   `https://my.cname.domain/optout?client=clientcode`.

1. Remplacez `clientcode` par votre code client et ajoutez le texte ou l’image à lier à l’URL d’exclusion.

Les visiteurs qui cliquent sur ce client ne sont pas inclus dans les requêtes de mbox appelées à partir de leur session de navigation tant qu’ils ne suppriment par leurs cookies ou pendant une durée de 2 ans, le premier événement prévalant. Ce lien définit un cookie, appelé `disableClient`, pour le visiteur dans le domaine `clientcode.tt.omtrdc.net`.

Même si vous utilisez une implémentation avec cookies propriétaires, l’exclusion par défaut est définie par l’intermédiaire d’un cookie tiers. Si le client utilise uniquement un cookie propriétaire, [!DNL Target] vérifie si un cookie d’exclusion est défini.

## Réglementations relatives à la confidentialité et à la protection des données

Pour plus d’informations sur le Règlement général sur la protection des données (RGPD) de l’Union européenne, le California Consumer Privacy Act (CCPA) et d’autres exigences internationales en matière de protection des données, voir [Réglementations relatives à la confidentialité et à la protection des données](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) et sur la manière dont ces réglementations affectent votre organisation et [!DNL Target].

## Collecte de données d’utilisation des fonctionnalités

Les données d’utilisation des fonctionnalités individuelles sont collectées à des fins d’Adobe interne afin d’identifier si les fonctionnalités [!DNL Target] fonctionnent comme prévu ou pour identifier celles qui sont sous-utilisées. Plusieurs mesures de latence sont collectées pour aider à résoudre les problèmes de performances. Les données personnelles ne sont pas collectées.

Vous pouvez exclure les données d’utilisation des rapports dans nos SDK en définissant `telemetryEnabled` sur false dans les options d’initialisation du client. Pour plus d’informations, consultez la section [telemetryEnabled dans targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
