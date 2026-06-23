---
keywords: registerExtension, registerextension, register extension, at.js, functions, function, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, timeout, registerExtension2
description: Utilisez la fonction [!UICONTROL registerExtension()] pour la bibliothèque JavaScript at [!DNL Adobe Target] js afin d’enregistrer une extension spécifique. (at.js 1.x)
title: Comment utiliser la fonction [!UICONTROL registerExtension()] ?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
TQID: https://experienceleague.adobe.com/qTWubp0dNesN-8vsooz8pdbjfSw1W1ktm-0bG6YRzJw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 62%

---

# [!UICONTROL registerExtension()] - at.js 1.x

Propose une méthode standard pour enregistrer une extension spécifique.

>[!NOTE]
>
>Cette fonction est disponible uniquement pour les versions 1.*x* d’at.js. Cette fonction a été abandonnée avec la publication d’at.js 2.*x*. Cette fonction renvoie le contenu par défaut s’il est utilisé avec at.js 2.x.

Le paramètre options est obligatoire et possède la structure suivante :

| Clé | Type | Requis | Description |
|--- |--- |--- |--- |
| name | Chaîne | Oui | Nom de l’extension. |
| modules | Tableau[Chaîne] | Oui | Tableau de chaînes représentant les noms de modules demandés. |
| s’inscrire | Fonction | Oui | Fonction utilisée pour initialiser et créer l’extension. Cette fonction reçoit les arguments sur la base du tableau de modules. |

Remarques :

* Si l’un des paramètres n’est pas fourni, une exception est déclenchée.
* Si le tableau de modules est vide, une exception est déclenchée.

Pour plus d’informations et d’exemples sur l’utilisation de `[!UICONTROL registerExtension]`, consultez la page [Extensions atjs Adobe Experience Cloud Target](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) sur GitHub.

## Méthodes de module Paramètres

| Clé | Type | Description |
|--- |--- |--- |
| clientCode | Chaîne | Code client |
| serverDomain | Chaîne | Domaine du serveur Edge |
| globalMboxName | Chaîne | [!DNL Target] nom de mbox globale |
| globalMboxAutoCreate | Booléen | Indique si la création automatique est activée ou non. |
| timeout | Nombre | Délai d’attente de requête |

## Méthodes de module Enregistreur

| Clé | Type | Description |
|--- |--- |--- |
| log | Fonction | Enregistre la liste de variables des arguments dans la console du navigateur, le cas échéant. Cette fonction est activée uniquement lorsque `mboxDebug=true` est passé à l’URL. |
| error | Fonction | Enregistre la liste de variables des arguments dans la console du navigateur. Cette fonction est activée uniquement en cas d’erreurs importantes, comme le délai d’expiration réseau atteint, un nœud HTML introuvable, etc. |

