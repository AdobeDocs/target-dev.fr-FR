---
keywords: implémentation, implémentation, liste autorisée, liste autorisée, liste autorisée, liste autorisée, edge, périphéries, 9 $
description: Affichez une liste d’hôtes pour vous aider à placer sur la liste autorisée des périphéries (nœuds de diffusion géographiquement répartis qui assurent un temps  [!DNL Adobe Target]  réponse optimal aux utilisateurs finaux).
title: Comment puis-je Placer sur la liste autorisée  [!DNL Target] des nœuds Edge ?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 275c3fabdcaf3152d7d6161f3c325e54c840c805
workflow-type: tm+mt
source-wordcount: '563'
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
>
>Toutes les adresses Edge4 *x* répertoriées dans les deux tableaux ci-dessous doivent être mises à jour le 9 août 2023.

## Adresses IP NAT (Network Address Translation) des périphéries [!DNL Target]

Liste des adresses IP sortantes des périphéries [!DNL Target]. Placez sur la liste autorisée ces adresses IP si vous prévoyez de [!DNL Target] à vos services.

| Emplacement Edge | Adresses IP sortantes |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<P>13.235.112.4 <P>52.66.66.192 |
| Edge42 (Tokyo) | 52.69.55.232<P>43.206.61.43 <P>13.113.73.214 |
| Edge44 (côte Est des États-Unis) | 54.164.192.223<P>52.86.86.203 <P>54.88.167.98 |
| Edge45 (côte ouest des États-Unis) | 52.40.124.129<P>54.148.219.69 <P>54.189.208.212 |
| Edge46 (Sydney) | 54.253.144.4<P>54.66.198.142 <P>13.211.218.51 |
| Edge47 (Irlande) | 52.208.136.136<P>54.170.28.19 <P>99.80.111.82 |
| Edge48 (Singapour) | 3.1.141.36<P>18.143.112.116 <P>52.76.61.44 |

## Adresses IP Edge de [!DNL Target]

Liste des adresses IP des périphéries du [!DNL Target]. Placez sur la liste autorisée ces adresses IP si vous souhaitez effectuer des appels API vers les périphéries [!DNL Target].

Cette liste change souvent, car les équilibreurs de charge sont mis à l’échelle en fonction des profils de trafic.

| Emplacement Edge | Domaine | Adresses IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(où CLIENTCODE est votre identifiant client [!DNL Target]) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52.66.66.192<P>13.235.112.4 |
| Edge42 (Tokyo) | `mboxedge42.tt.omtrdc.net` | 43.206.61.43<P>13.113.73.214<P>52.69.55.232 |
| Edge44 (côte Est des États-Unis) | `mboxedge44.tt.omtrdc.net` | 54.88.167.98<P>54.164.192.223<P>52.86.86.203 |
| Edge45 (côte ouest des États-Unis) | `mboxedge45.tt.omtrdc.net` | 52.40.124.129<P>54.148.219.69<P>54.189.208.212 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 54.66.198.142<P>54.253.144.4<P>13.211.218.51 |
| Edge47 (Irlande) | `mboxedge47.tt.omtrdc.net` | 54.170.28.19<P>52.208.136.136<P>99.80.111.82 |
| Edge48 (Singapour) | `mboxedge48.tt.omtrdc.net` | 52.76.61.44<P>3.1.141.36<P>18.143.112.116 |

Lorsque les équilibreurs de charge détectent des modifications dans le profil de trafic, ils sont mis à l’échelle vers le haut ou vers le bas. Le temps nécessaire pour que l&#39;équilibrage de charge élastique soit mis à l&#39;échelle peut aller de 1 à 7 minutes, selon les changements détectés. Lorsque les répartiteurs de charge se mettent à l’échelle, ils mettent à jour l’enregistrement DNS avec la nouvelle liste d’adresses IP. Pour vous assurer de tirer parti de cette capacité accrue, l’équilibrage de charge élastique utilise un paramètre de durée de vie sur l’enregistrement DNS de 60 secondes.

## Placer sur la liste autorisée Configuration requise pour le service de proxy [!DNL Target]

Pour garantir un accès ininterrompu aux [!DNL Target] par le biais du [!DNL Experience Edge Connector] (EEC), les clients peuvent avoir besoin de mettre à jour leurs configurations réseau pour autoriser le trafic vers le service proxy.

### Présentation du service de proxy

* **Point d’entrée du service** : `https://tnt-web-proxy.adobe.io`.
* **Infrastructure** : hébergé sur la plateforme [!DNL Adobe] Ethos.
* **Remarque** : ce service utilise le routage DNS basé sur la latence et ne dépend pas des adresses IP statiques.

### Cibles CNAME

Le service de proxy achemine le trafic de manière dynamique sur plusieurs régions à l’aide d’enregistrements CNAME. Voici les cibles actuelles :

| Emplacement Edge | Adresses IP sortantes |
| --- | --- |
| Région | Cible CNAME |
| Europe (eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| Est des États-Unis (us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| Est des États-Unis (us-est-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

### Entrées de place sur la liste autorisée recommandées

Pour garantir une connectivité fiable, placez sur la liste autorisée les noms d’hôtes suivants :

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

### Facultatif : découverte d’adresses IP

Si vos politiques de réseau nécessitent une liste autorisée basée sur l’adresse IP, vous pouvez afficher les adresses IP publiques actuelles associées au service proxy à l’aide de cet outil :

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`