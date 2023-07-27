---
keywords: confidentialité, adresse ip, géosegmentation, opt-out, opt-out, opt-out, confidentialité des données, réglementations gouvernementales, gdpr, ccpa, confidentialité, informations d’identification personnelles, PII
description: Découvrez comment [!DNL Adobe Target] se conforme aux lois sur la confidentialité des données en vigueur, notamment à la collecte et au traitement des adresses IP, des informations d’identification personnelles et des instructions d’exclusion.
title: Comment Target gère-t-il les problèmes de confidentialité, y compris les informations d’identification personnelles ?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 58%

---

# Confidentialité

Les paramètres et les processus d’[!DNL Adobe Target] vous permettent d’utiliser [!DNL Target] conformément aux lois applicables en matière de confidentialité des données.

## Collecte d’adresses IP et d’informations d’identification personnelle (PII)

L’adresse IP d’un visiteur de votre site Web est transmise à un centre de traitement de données Adobe. Selon la configuration réseau du visiteur, l’adresse IP ne représente pas nécessairement l’adresse IP de l’ordinateur du visiteur. Il peut par exemple s’agir de l’adresse IP externe d’un pare-feu NAT (traduction d’adresses réseau), d’un proxy HTTP ou d’une passerelle Internet.

>[!IMPORTANT]
>
>[!DNL Target] ne stocke aucune adresse IP de l’utilisateur ni aucune information personnelle identifiable. Les adresses IP ne sont utilisées que par [!DNL Target] pendant la session (en mémoire, jamais conservée).

## Remplacement du dernier octet des adresses IP

Adobe a développé un paramètre de &quot;confidentialité par conception&quot; que les utilisateurs peuvent activer pour Adobe [!DNL Target]. Lorsqu’elle est activée, Adobe [!DNL Target] obscurcit immédiatement le dernier octet (la dernière partie) de l’adresse IP au moment de la collecte de l’adresse IP. Cette anonymisation a lieu avant le traitement des adresses IP et avant la géolocalisation facultative de l’adresse IP.

Si cette fonction est activée, l’adresse IP est suffisamment anonyme pour ne plus être identifiable en tant qu’information personnelle. Par conséquent, [!DNL Target] peuvent être utilisées conformément aux lois sur la confidentialité des données dans les pays qui n’autorisent pas la collecte d’informations personnelles. L’obtention d’informations sur les villes sera considérablement entravée par l’obscurcissement de l’adresse IP, tandis que l’obtention des informations sur les régions et les pays ne sera que légèrement entravée.

Les paramètres suivants sont disponibles dans la variable [!DNL Target] l’interface utilisateur en accédant à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]**:

* [!UICONTROL Obscurcissement du dernier octet]: [!DNL Target] masque le dernier octet de l’adresse IP.
* [!UICONTROL Obscurcissement d’IP complet]: [!DNL Target] masque l’adresse IP entière.
* [!UICONTROL Aucun]: [!DNL Target] ne masque aucune partie de l’adresse IP.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] reçoit l’adresse IP complète et l’obscurcit (s’il est défini sur le dernier octet ou l’adresse IP complète) comme spécifié. [!DNL Target] contient ensuite l’adresse IP obscurcie uniquement en mémoire pendant la session en cours.

## Géosegmentation

Si vous activez le remplacement du dernier octet de l’adresse IP, les valeurs restantes de l’adresse IP peuvent être analysées à l’aide des rapports dans [!DNL Target]. Si le dernier octet de l’adresse IP n’a pas été obscurci, l’adresse IP complète peut être analysée dans [!DNL Target]. Vous pouvez utiliser la fonctionnalité de géosegmentation pour dessiner l’emplacement du visiteur par zone géographique. Les données de géosegmentation sont alors détaillées au niveau des villes ou des codes postaux uniquement, mais pas au niveau individuel.

Si les adresses IP sont entièrement obscurcies, la géosegmentation et le géociblage ne sont pas disponible.

## Lien d’exclusion

Vous pouvez ajouter un lien d’exclusion à vos sites pour permettre aux visiteurs de s’exclure de tout comptage et diffusion de contenu.

1. Ajoutez le lien suivant sur votre site :

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Conditionnel) Si vous utilisez CNAME, le lien doit contenir &quot;client=`clientcode` par exemple :
   `https://my.cname.domain/optout?client=clientcode`.

1. Remplacez `clientcode` par votre code client et ajoutez le texte ou l’image à lier à l’URL d’exclusion.

Les visiteurs qui cliquent sur ce client ne sont pas inclus dans les requêtes de mbox appelées à partir de leur session de navigation tant qu’ils ne suppriment par leurs cookies ou pendant une durée de 2 ans, le premier événement prévalant. Ce lien définit un cookie, appelé `disableClient`, pour le visiteur dans le domaine `clientcode.tt.omtrdc.net`.

Même si vous utilisez une implémentation avec cookies propriétaires, l’exclusion par défaut est définie par l’intermédiaire d’un cookie tiers. Si le client utilise uniquement un cookie propriétaire, [!DNL Target] vérifie si un cookie d’exclusion est défini.

## Réglementations relatives à la confidentialité et à la protection des données

Consultez les [réglementations relatives à la confidentialité et à la protection des données](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) pour plus d’informations sur le RGPD (règlement général sur la protection des données), le CCPA (California Consumer Privacy Act) et d’autres exigences internationales en matière de confidentialité, ainsi que sur l’impact de ces réglementations sur votre entreprise et sur [!DNL Target].

## Collecte de données d’utilisation des fonctionnalités

Les données d’utilisation des fonctionnalités individuelles sont collectées à des fins d’Adobe interne pour déterminer si [!DNL Target] Les fonctions se comportent comme prévu ou pour identifier les fonctions qui sont sous-utilisées. Plusieurs mesures de latence sont collectées pour aider à résoudre les problèmes de performances. Les données personnelles ne sont pas collectées.

Vous pouvez exclure les données d’utilisation des rapports dans nos SDK en définissant `telemetryEnabled` sur false dans les options d’initialisation du client. Pour plus d’informations, consultez la section [telemetryEnabled dans targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
