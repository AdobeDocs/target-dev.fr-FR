---
keywords: adobe.target.getOffer, getOffer, getoffer, get offer, at.js, fonctions, fonction, 8 $
description: Utilisez la fonction [!UICONTROL adobe.target.getOffer()] et ses options pour la bibliothèque  [!DNL Adobe Target] at.js pour déclencher les demandes d’obtention d’une offre  [!DNL Target] .
title: Comment utiliser la fonction [!UICONTROL adobe.target.getOffer()] ?
feature: at.js
exl-id: 7b917d42-06e8-4838-a09d-0c4872c9beaa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 81%

---

# [!DNL adobe.target.getOffer(options)]

Cette fonction déclenche une requête pour obtenir une offre [!DNL Target].

Utilisez avec `[!UICONTROL adobe.target.applyOffer()]` pour traiter la réponse ou utilisez votre propre gestion de succès. Le paramètre options est obligatoire et possède la structure suivante :

| Clé | Type | Requis | Description |
|--- |--- |--- |--- |
| mbox | Chaîne | Oui | Nom de mbox |
| params | Objet | Non | Paramètres mbox. Objet de paires clé-valeur qui possède la structure suivante :<P>`{ "param1": "value1", "param2": "value2"}` |
| success | Fonction | Oui | Rappel à exécuter lors de l’obtention d’une réponse du serveur. La fonction de rappel de succès reçoit un seul paramètre qui représente un tableau des objets d’offre. Voici un exemple de rappel de succès :<P>`function handleSuccess(response){......}`<P>Pour plus d’informations, voir les réponses ci-dessous. |
| error | Fonction | Oui | Rappel à exécuter lors d’une erreur. Quelques cas sont considérés comme des erreurs :<ul><li>Le code d’état HTTP est différent de 200 OK.</li><li>La réponse ne peut pas être analysée. Par exemple, le code JSON a été mal créé ou du code HTML a été utilisé à la place de JSON.</li><li>La réponse contient la clé error. Par exemple, une exception a été levée à la périphérie car une demande n’a pas pu être correctement traitée. Un message d’erreur peut être généré lorsqu’une mbox est bloquée et qu’il est impossible de récupérer le contenu correspondant, etc. La fonction de rappel d’erreur reçoit deux paramètres : status et error. Voici un exemple de rappel d’erreur : `function handleError(status, error){......}`</li></ul>Pour plus d’informations, voir les réponses d’erreur ci-dessous. |
| timeout | Nombre | Non | Délai d’attente exprimé en secondes. Si cette valeur n’est pas spécifiée, le délai d’attente par défaut d’at.js est utilisé.<P>Le délai d’expiration par défaut peut être défini à partir de l’interface utilisateur [!DNL Target] sous [!UICONTROL Administration] > [!UICONTROL Implementation]. |

## Exemples

Ajout de paramètres avec [!UICONTROL getOffer()] et utilisation de [!UICONTROL applyOffer()] pour la gestion de succès :

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

Ajout de paramètres et de paramètres de profil avec [!UICONTROL getOffer()] et utilisation de [!UICONTROL applyOffer()] pour la gestion de succès :

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2, 
     "profile.age": 27, 
     "profile.gender": "male" 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

Utilisation d’un délai d’expiration personnalisé et d’une gestion de succès personnalisée avec [!UICONTROL getOffer()] :

« YOUR_OWN_CUSTOM_HANDLING_FUNCTION » est un espace réservé pour une fonction définie par le client.

```javascript {line-numbers="true"}
adobe.target.getOffer({     
  "mbox": "target-global-mbox",   
  "success": function(offer) { 
    YOUR_OWN_CUSTOM_HANDLING_FUNCTION(offer);   
  }, 
  "error": function(status, error) {                 
    console.log('Error', status, error);   
  },   
  "timeout": 2000 
});
```

## Réponses

Le paramètre de la réponse transféré au rappel de succès correspondra à un tableau d’actions. Une action est un objet qui a généralement le format suivant :

| Nom | Type | Description |
|--- |--- |--- |
| action | Chaîne | Type d’action à appliquer à l’élément identifié. |
| selector | Chaîne | Représente un sélecteur de fichier sizzle. |
| cssSelector | Chaîne | Sélecteur de modèle DOM natif, utilisé pour le prémasquage des éléments. |
| content | Chaîne | Le contenu à appliquer à l’élément identifié. |

## Exemple

```javascript {line-numbers="true"}
{ 
    "sessionId": "1444512212156-384616", 
    "tntId": "1444512212156-384616.17_35", 
    "offers": [{ 
        "plugins": ["<script type=\"text/javascript\">\r\n/*mboxHighlight+ (1of2) v1 ==> Response Plugin*/\r\nwindow.ttMETA=(typeof(window.ttMETA)!='undefined')?window.ttMETA:[];window.ttMETA.push({'mbox':'target-global-mbox','campaign':'at: redirect ootb','experience':'Experience B','offer':'/at_redirect_ootb/experiences/1/pages/0/1442082890250'});window.ttMBX=function(x){var mbxList=[];for(i=0;i<ttMETA.length;i++){if(ttMETA[i].mbox==x.getName()){mbxList.push(ttMETA[i])}}return mbxList[x.getId()]}\r\n</script>"], 
        "actions": { 
            "content": [{ 
                "passMboxSession": false, 
                "selector": "body", 
                "action": "redirect", 
                "url": "https://example.com/04.html", 
                "includeAllUrlParameters": true 
            }] 
        } 
    }] 
}
```

## Réponses d’erreur

Les paramètres status et error transmis au rappel d’erreur possèdent le format suivant :

| Nom | Type | Description |
|--- |--- |--- |
| status | Chaîne | Représente l’état d’erreur. Ce paramètre peut avoir les valeurs suivantes :<ul><li>timeout : indique que la demande a expiré.</li><li>parseerror : indique que l’erreur n’a pas pu être analysée, par exemple, si nous recevons le code HTML ou un texte brut au lieu du code JSON.</li><li>error : indique une erreur générale, telle que la réception d’un état HTTP différent de 200 OK</li></ul> |
| error | Chaîne | Contient des données supplémentaires telles qu’un message d’exception ou tout autre élément utile pour la résolution des problèmes. |
