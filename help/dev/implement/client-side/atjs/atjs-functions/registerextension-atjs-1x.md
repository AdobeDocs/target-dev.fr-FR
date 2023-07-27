---
keywords: registerExtension, registerExtension, registerExtension, at.js, fonctions, fonction, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, timeout, registerExtension2
description: Utilisez la variable [!UICONTROL registerExtension()] pour la fonction [!DNL Adobe Target] Bibliothèque JavaScript at.js pour enregistrer une extension spécifique. (at.js 1.x)
title: Comment utiliser la variable [!UICONTROL registerExtension()] Fonction ?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 76%

---

# [!UICONTROL registerExtension()] - at.js 1.x

Propose une méthode standard pour enregistrer une extension spécifique.

>[!NOTE]
>
>Cette fonction est disponible pour at.js versions 1.*x* uniquement. Cette fonction a été abandonnée avec la version d’at.js 2.*x*. Cette fonction renvoie le contenu par défaut s’il est utilisé avec at.js 2.x.

Le paramètre options est obligatoire et possède la structure suivante :

| Clé | Type | Requis | Description |
|--- |--- |--- |--- |
| name | Chaîne | Oui | Nom de l’extension. |
| modules | Tableau[Chaîne] | Oui | Tableau de chaînes représentant les noms de modules demandés. |
| s’inscrire | Fonction | Oui | Fonction utilisée pour initialiser et créer l’extension. Cette fonction reçoit les arguments sur la base du tableau de modules. |

Remarques :

* Si l’un des paramètres n’est pas fourni, une exception est déclenchée.
* Si le tableau de modules est vide, une exception est déclenchée.

Pour en savoir plus et consulter des exemples sur la manière d’utiliser `[!UICONTROL registerExtension]`, visitez la page [Extensions Target atjs d’Adobe Experience Cloud](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) sur GitHub.

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
