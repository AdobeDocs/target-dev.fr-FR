---
keywords: implémenter, implémenter, mettre en oeuvre, mettre en whiteliste, liste blanche, liste autorisée, liste autorisée, périphérie, périphéries, 9 $
description: Affichez une liste d’hôtes pour vous aider à placer sur la liste autorisée les  [!DNL Adobe Target] périphéries (noeuds de diffusion distribués géographiquement qui assurent un temps de réponse optimal aux utilisateurs finaux).
title: Comment Placer sur la liste autorisée Les Noeuds  [!DNL Target] Edge ?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 49b6572c0d414ab304712691c97794bb0b1e3781
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Placer sur la liste autorisée [!DNL Target] noeuds de périphérie

Informations et liste actualisée des hôtes pour vous aider à placer sur la liste autorisée les [!DNL Adobe Target] périphéries.

Une périphérie est une architecture de diffusion géographiquement répartie qui assure un temps de réponse optimal pour les utilisateurs qui demandent du contenu, où qu’ils se trouvent. Chaque noeud de périphérie contient toutes les informations nécessaires pour répondre à la requête de contenu de l’utilisateur et pour effectuer le suivi des données d’analyse de cette requête. Les requêtes des utilisateurs sont acheminées vers le noeud de périphérie le plus proche. Pour plus d’informations, voir [The edge network](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Si vous le souhaitez, vous pouvez placer sur la liste autorisée [!DNL Target] noeuds périphériques.

>[!IMPORTANT]
>
>Outre le fait de placer sur la liste autorisée les adresses IP NAT (Network Address Translation) des [!DNL Target] périphéries et des [!DNL Target] edge IP addresses mentionnées dans l’article, vous devez également placer sur la liste autorisée tous les blocs d’adresses IP [!DNL Adobe Analytics].
>
>Pour plus d’informations, voir [Tous les blocs d’adresse IP Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} dans la documentation *Notes techniques Adobe Analytics*.
>
>L’infrastructure [!DNL Adobe Target] est en cours de mise à jour et les clients qui souhaitent placer sur la liste autorisée des adresses doivent utiliser les deux ensembles d’adresses IP. Sinon, les clients qui utilisent des implémentations côté serveur ou hybrides, dans lesquelles les appels d’API Target pour récupérer des expériences sont issus d’un réseau derrière un pare-feu configuré pour utiliser une liste autorisée, seront affectés.
>
>Toutes les adresses Edge4 *x* répertoriées dans les deux tableaux ci-dessous doivent être mises à jour le 9 août 2023.

## des adresses IP NAT (Network Address Translation) des [!DNL Target] périphéries

Liste des adresses IP sortantes des périphéries [!DNL Target]. Placez sur la liste autorisée ces adresses IP si vous prévoyez d’étendre [!DNL Target] à vos services.

| Emplacement Edge | Adresses IP sortantes |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<br />13.235.112.4 <br />52.66.66.192 |
| Edge42 (Tokyo) | 52.69.55.232<br />43.206.61.43 <br />13.113.73.214 |
| Edge44 (côte Est des États-Unis) | 54.164.192.223<br />52.86.86.203 <br />54.88.167.98 |
| Edge45 (côte ouest des États-Unis) | 52.40.124.129<br />54.148.219.69 <br />54.189.208.212 |
| Edge46 (Sydney) | 54.253.144.4<br />54.66.198.142 {13.211.218.51<br /> |
| Edge47 (Irlande) | 52.208.136.136<br />54.170.28.19 <br />99.80.111.82 |
| Edge48 (Singapour) | 3.1.141.36<br />18.143.112.116 <br />52.76.61.44 |

## [!DNL Target] adresses IP de périphérie

Liste des adresses IP des périphéries [!DNL Target]. Placez sur la liste autorisée ces adresses IP si vous souhaitez effectuer des appels API aux périphéries [!DNL Target].

Cette liste change souvent, car les équilibreurs de charge évoluent vers le haut ou vers le bas en fonction des profils de trafic.

| Emplacement Edge | Domaine | Adresses IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(où CLIENTCODE est votre ID client [!DNL Target]) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 15.206.104.6<br />3.109.14.178 <br />13.234.139.131 |
| Edge42 (Tokyo) | `mboxedge42.tt.omtrdc.net` | 52.194.84.34<br />3.115.158.39 <br />18.180.123.21 |
| Edge44 (côte Est des États-Unis) | `mboxedge44.tt.omtrdc.net` | 54.205.210.54<br />23.20.189.8 <br />35.169.173.155 |
| Edge45 (côte ouest des États-Unis) | `mboxedge45.tt.omtrdc.net` | 35.161.163.45<br />44.230.114.101 <br />35.161.120.22 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 3.104.142.61<br />52.62.4.152 <br />54.253.105.140 |
| Edge47 (Irlande) | `mboxedge47.tt.omtrdc.net` | 18.203.168.186<br />54.228.83.91 <br />54.217.181.83 |
| Edge48 (Singapour) | `mboxedge48.tt.omtrdc.net` | 54.179.6.70<br />13.215.150.94 <br />18.136.47.70 |

Lorsque les équilibreurs de charge détectent des modifications dans le profil de trafic, il augmente ou diminue. Le temps nécessaire à l’équilibrage de charge élastique pour l’échelle peut varier de 1 à 7 minutes, selon les modifications détectées. Lorsque les équilibreurs de charge évoluent, ils mettent à jour l’enregistrement DNS avec la nouvelle liste d’adresses IP. Pour vous assurer de tirer parti de la capacité accrue, l’équilibrage de charge élastique utilise un paramètre TTL sur l’enregistrement DNS de 60 secondes.
