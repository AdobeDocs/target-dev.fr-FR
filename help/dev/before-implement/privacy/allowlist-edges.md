---
keywords: implémentation, implémentation, liste autorisée, liste autorisée, liste autorisée, liste autorisée, edge, périphéries, 9 $
description: Affichez une liste d’hôtes pour vous aider à placer sur la liste autorisée des périphéries (nœuds de diffusion géographiquement répartis qui assurent un temps  [!DNL Adobe Target]  réponse optimal aux utilisateurs finaux).
title: Comment puis-je Placer sur la liste autorisée  [!DNL Target] des nœuds Edge ?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 662d415bc3c216bcd038f07dcaa0fd83f6518690
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Placer sur la liste autorisée [!DNL Target] nœuds Edge

Informations et liste à jour des hôtes pour vous aider à placer sur la liste autorisée [!DNL Adobe Target] périphéries.

Un serveur Edge est une architecture de diffusion géographiquement distribuée qui garantit un temps de réponse optimal aux utilisateurs finaux qui demandent du contenu, où qu’ils se trouvent. Chaque nœud Edge contient toutes les informations nécessaires pour répondre à la demande de contenu de l’utilisateur et pour effectuer un suivi des données d’analyse sur cette demande. Les requêtes des utilisateurs sont acheminées vers le nœud Edge le plus proche. Pour plus d’informations, voir [Le réseau Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=fr#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Vous pouvez placer sur la liste autorisée [!DNL Target] nœuds Edge, si vous le souhaitez.

>[!IMPORTANT]
>
>En plus de placer sur la liste autorisée placer sur la liste autorisée les adresses IP NAT (Network Address Translation) des adresses IP des périphéries [!DNL Target] et des adresses IP des périphéries [!DNL Target] abordées dans l’article, vous devez également tous les blocs d’adresses IP [!DNL Adobe Analytics].
>
>Pour plus d’informations, voir [Tous les blocs d’adresses IP Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=fr#all-adobe-analytics-ip-address-blocks){target=_blank} dans la documentation *Notes techniques d’Adobe Analytics*.
>
>[!DNL Adobe Target] infrastructure est en cours de mise à jour et les clients qui souhaitent utiliser des adresses IP en liste autorisée doivent utiliser les deux ensembles d’adresses IP. Si vous ne le faites pas, cela aura un impact sur les clients utilisant des implémentations côté serveur ou hybrides où les appels d’API Target pour la récupération d’expériences proviennent d’un réseau derrière un pare-feu configuré pour utiliser un place sur la liste autorisée de .

Pour garantir un accès ininterrompu aux [!DNL Target] par le biais du [!DNL Experience Edge Connector], les clients peuvent mettre à jour leurs configurations réseau afin d’autoriser le trafic vers le service proxy.

## Présentation du service de proxy

* **Point d’entrée du service** : `https://tnt-web-proxy.adobe.io`.
* **Infrastructure** : hébergé sur la plateforme [!DNL Adobe] Ethos.
* **Remarque** : ce service utilise le routage DNS basé sur la latence et ne dépend pas des adresses IP statiques.

## Cibles CNAME

Le service de proxy achemine le trafic de manière dynamique sur plusieurs régions à l’aide d’enregistrements CNAME. Voici les cibles actuelles :

| Emplacement Edge | Adresses IP sortantes |
| --- | --- |
| Région | Cible CNAME |
| Europe (eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| Est des États-Unis (us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| Est des États-Unis (us-est-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

## Entrées de place sur la liste autorisée recommandées

Pour garantir une connectivité fiable, placez sur la liste autorisée les noms d’hôtes suivants :

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## Facultatif : découverte d’adresses IP

Si vos politiques de réseau nécessitent une liste autorisée basée sur l’adresse IP, vous pouvez afficher les adresses IP publiques actuelles associées au service proxy à l’aide de cet outil :

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`