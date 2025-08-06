---
title: Synchronisation des profils en temps réel pour mbox3rdPartyId
description: Découvrez comment utiliser mbox3rdPartyId avec le  [!DNL Adobe Experience Platform Web SDK].
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
source-git-commit: 27759841c8d6a4ac4cc72e735f1dc6512c71aea5
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 16%

---

# Qu’est-ce que mbox3rdPartyId ?

Dans [!DNL Adobe Target], le `mbox3rdPartyId` représente l’identifiant visiteur de votre société. Il s’agit par exemple de l’identifiant d’abonnement pour le programme de fidélité de votre société.

Lorsqu’un visiteur se connecte au site d’une entreprise, l’entreprise crée généralement un identifiant lié au compte du visiteur, à la carte de fidélité, au numéro d’abonnement ou à d’autres identifiants applicables de cette entreprise. [En savoir plus](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=fr#)

## Comment utiliser `mbox3rdPartyId` avec le [!DNL Platform Web SDK]

### Étape 1 : configurer le `Target Third Party ID Namespace`

Configurez le `Target Third Party ID Namespace` dans votre [flux de données](https://experienceleague.adobe.com/fr/docs/experience-platform/datastreams/overview) en utilisant l’espace de noms d’identifiant que vous souhaitez utiliser comme identifiant tiers de mbox. [En savoir plus sur les espaces de noms d’ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

![Interface utilisateur d’Experience Platform affichant le champ Espace de noms de l’identifiant tiers cible.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### Étape 2 : envoyer le `mbox3rdpartyId` à [!DNL Target]

Envoyez le `mbox3rdpartyId` à [!DNL Target] dans la commande `sendEvent`, à l’aide de l’espace de noms d’identifiant que vous avez configuré à l’étape 1.
[En savoir plus sur l’envoi d’identifiants](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
