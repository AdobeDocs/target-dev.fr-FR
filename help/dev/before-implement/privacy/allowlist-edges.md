---
keywords: implémenter, implémenter, liste autorisée, liste autorisée, liste autorisée, liste autorisée, périphérie, périphéries, 9 $
description: Affichage d’une liste d’hôtes pour vous aider à placer sur la liste autorisée [!DNL Adobe Target] périphéries (noeuds de diffusion distribués géographiquement qui garantissent un temps de réponse optimal pour les utilisateurs finaux).
title: Comment Placer sur la liste autorisée [!DNL Target] Noeuds Edge ?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 3f4147d521b1fb3ee12e879e52a48d459f6b24b9
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 6%

---

# Liste autorisée [!DNL Target] noeuds périphériques

Informations et liste actualisée des hôtes pour vous aider à placer sur la liste autorisée [!DNL Adobe Target] arêtes.

Une périphérie est une architecture de diffusion géographiquement répartie qui assure un temps de réponse optimal pour les utilisateurs qui demandent du contenu, où qu’ils se trouvent. Chaque noeud de périphérie contient toutes les informations nécessaires pour répondre à la requête de contenu de l’utilisateur et pour effectuer le suivi des données d’analyse de cette requête. Les requêtes des utilisateurs sont acheminées vers le noeud de périphérie le plus proche. Pour plus d’informations, voir [Réseau Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Vous pouvez placer sur la liste autorisée [!DNL Target] noeuds Edge, le cas échéant.

>[!IMPORTANT]
>
>En plus de placer sur la liste autorisée la traduction des adresses IP NAT (Network Address Translation) de [!DNL Target] arêtes [!DNL Target] Les adresses IP Edge mentionnées dans l’article doivent également placer sur la liste autorisée toutes les [!DNL Adobe Analytics] Blocs d’adresses IP.
>
>Pour plus d’informations, voir [Tous les blocs d’adresses IP Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} dans le *Notes techniques d’Adobe Analytics* la documentation.
>
>[!DNL Adobe Target] L’infrastructure est en cours de mise à jour et les clients qui souhaitent placer sur la liste autorisée des adresses doivent utiliser les deux ensembles d’adresses IP. Sinon, les clients qui utilisent des implémentations côté serveur ou hybrides, dans lesquelles les appels d’API Target pour récupérer des expériences sont issus d’un réseau derrière un pare-feu configuré pour utiliser une liste autorisée, seront affectés.
>
>All Edge4 *x* Les adresses répertoriées dans les deux tableaux ci-dessous doivent être mises à jour le 9 août 2023.

## Traduction d’adresses réseau (NAT) des adresses IP de [!DNL Target] edge

Liste des adresses IP sortantes de [!DNL Target] arêtes. Placez sur la liste autorisée ces adresses IP si vous envisagez d’utiliser [!DNL Target] contactez vos services.

| Emplacement Edge | Adresses IP sortantes |
| --- | --- |
| Edge31 (Mumbai) | 13.126.131.246<br />13.234.229.8 |
| Edge32 (Tokyo) | 3.115.154.28<br />3.115.227.146 |
| Edge34 (côte Est des États-Unis) | 34.232.149.249<br />52.21.139.93 |
| Edge35 (côte ouest des États-Unis) | 52.10.11.139<br />44.231.171.161 |
| Edge36 (Sydney) | 13.237.227.20<br />13.210.93.142 |
| Edge37 (Irlande) | 54.72.21.68<br />52.208.139.19 |
| Edge38 (Singapour) | 18.141.132.96<br />54.179.187.167 |
| Edge41 (Mumbai) | 3.6.2.221<br />13.235.112.4 <br />52.66.66.192 |
| Edge42 (Tokyo) | 52.69.55.232<br />43.206.61.43 <br />13.113.73.214 |
| Edge44 (côte Est des États-Unis) | 54.164.192.223<br />52.86.86.203 <br />54.88.167.98 |
| Edge45 (côte ouest des États-Unis) | 52.40.124.129<br />54.148.219.69 <br />54.189.208.212 |
| Edge46 (Sydney) | 54.253.144.4<br />54.66.198.142 <br />13.211.218.51 |
| Edge47 (Irlande) | 52.208.136.136<br />54.170.28.19 <br />99.80.111.82 |
| Edge48 (Singapour) | 3.1.141.36<br />18.143.112.116 <br />52.76.61.44 |

## [!DNL Target] adresses IP Edge

Liste des adresses IP de [!DNL Target] arêtes. Placez sur la liste autorisée ces adresses IP si vous souhaitez effectuer des appels d’API vers [!DNL Target] arêtes.

Cette liste change souvent, car les équilibreurs de charge évoluent vers le haut ou vers le bas en fonction des profils de trafic.

| Emplacement Edge | Domaine | Adresses IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(où CLIENTCODE est votre [!DNL Target] ID client) |  |
| Edge31 (Mumbai) | `mboxedge31.tt.omtrdc.net` | 13.235.211.15<br />35.154.193.2<br />35.154.53.50<br />15.206.4.195<br />13.234.45.112<br />3.7.14.31<br />3.7.182.1<br />52.66.52.225<br />3.6.64.110<br />65.0.222.85<br />65.1.67.35<br />43.205.52.220 |
| Edge32 (Tokyo) | `mboxedge32.tt.omtrdc.net` | 3.112.121.190<br />54.65.158.134<br />52.199.9.11<br />54.95.35.22<br />52.68.152.188<br />52.196.181.152<br />54.150.112.230<br />52.198.235.210 |
| Edge34 (côte Est des États-Unis) | `mboxedge34.tt.omtrdc.net` | 44.195.255.231<br />52.207.142.243<br />52.54.50.225<br />35.169.35.160<br />52.71.135.138<br />35.169.227.120<br />23.22.33.42<br />52.54.152.40<br />54.243.116.94<br />3.233.250.116<br />50.16.29.53<br />54.86.98.238<br />44.210.41.177<br />3.211.200.163<br />54.210.15.1<br />34.199.251.113 |
| Edge35 (côte ouest des États-Unis) | `mboxedge35.tt.omtrdc.net` | 44.238.17.94<br />52.27.37.224<br />52.89.178.205<br />52.24.182.215<br />44.241.83.238<br />52.24.177.17<br />35.165.241.91<br />52.36.84.148<br />52.40.70.235<br />52.11.244.25<br />35.83.17.210<br />52.42.219.24<br />54.218.0.208<br />34.218.165.70<br />44.239.131.209<br />52.37.121.114<br />35.164.96.150<br />52.40.11.173<br />52.32.91.22<br />35.82.102.174<br />50.112.233.80<br />44.241.57.139<br />44.233.4.154<br />54.69.42.127<br />34.211.73.73<br />54.148.130.206<br />44.238.29.100<br />44.228.116.36<br />52.40.119.218<br />52.25.253.33 |
| Edge36 (Sydney) | `mboxedge36.tt.omtrdc.net` | 54.206.232.103<br />54.206.183.241<br />3.24.158.129<br />54.253.0.242 |
| Edge37 (Irlande) | `mboxedge37.tt.omtrdc.net` | 54.77.63.43<br />63.35.113.29<br />63.34.224.124<br />54.246.171.67<br />99.80.163.253<br />34.253.167.75<br />52.211.90.101<br />54.246.201.164<br />34.249.148.170<br />54.76.19.168<br />52.209.9.253 |
| Edge38 (Singapour) | `mboxedge38.tt.omtrdc.net` | 52.220.75.199<br />52.221.116.71 |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 15.206.104.6<br />3.109.14.178 <br />13.234.139.131 |
| Edge42 (Tokyo) | `mboxedge42.tt.omtrdc.net` | 52.194.84.34<br />3.115.158.39 <br />18.180.123.21 |
| Edge44 (côte Est des États-Unis) | `mboxedge44.tt.omtrdc.net` | 54.205.210.54<br />23.20.189.8 <br />35.169.173.155 |
| Edge45 (côte ouest des États-Unis) | `mboxedge45.tt.omtrdc.net` | 35.161.163.45<br />44.230.114.101 <br />35.161.120.22 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 3.104.142.61<br />52.62.4.152 <br />54.253.105.140 |
| Edge47 (Irlande) | `mboxedge47.tt.omtrdc.net` | 18.203.168.186<br />54.228.83.91 <br />54.217.181.83 |
| Edge48 (Singapour) | `mboxedge48.tt.omtrdc.net` | 54.179.6.70<br />13.215.150.94 <br />18.136.47.70 |

Lorsque les équilibreurs de charge détectent des modifications dans le profil de trafic, il augmente ou diminue. Le temps nécessaire à l’équilibrage de charge élastique pour l’échelle peut varier de 1 à 7 minutes, selon les modifications détectées. Lorsque les équilibreurs de charge évoluent, ils mettent à jour l’enregistrement DNS avec la nouvelle liste d’adresses IP. Pour vous assurer de tirer parti de la capacité accrue, l’équilibrage de charge élastique utilise un paramètre TTL sur l’enregistrement DNS de 60 secondes.
