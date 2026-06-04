---
title: Synchronisation des profils en temps réel pour mbox3rdPartyId
description: Découvrez comment utiliser mbox3rdPartyId avec le  [!DNL Adobe Experience Platform Web SDK].
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
exl-id: 1c5067ef-38b3-4bf1-bd39-ea0f2cbd1074
TQID: https://experienceleague.adobe.com/Ej2sYVnBD9orRTlsMQG85JJV7dvn-9gnABDa0b8uBlM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 35%

---

# Utiliser mbox3rdPartyId

Dans [!DNL Adobe Target], le `mbox3rdPartyId` représente l’identifiant visiteur de votre société. Il s’agit par exemple de l’identifiant d’abonnement pour le programme de fidélité de votre société.

Lorsqu’un visiteur se connecte au site de votre entreprise, cette dernière crée généralement un identifiant qui est associé au compte du visiteur, à sa carte de fidélité, à son numéro de membre ou à tout autre identifiant applicable de l’entreprise. [En savoir plus](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)

## Comment utiliser `mbox3rdPartyId` avec le [!DNL Platform Web SDK]

### Étape 1 : configurer le `Target Third Party ID Namespace`

Configurez le `Target Third Party ID Namespace` dans votre [flux de données](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) en utilisant l’espace de noms d’identifiant que vous souhaitez utiliser comme identifiant tiers de mbox. [En savoir plus sur les espaces de noms d’ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![Interface utilisateur d’Experience Platform affichant le champ Espace de noms de l’identifiant tiers cible.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### Étape 2 : envoyer le `mbox3rdpartyId` à [!DNL Target]

Envoyez le `mbox3rdpartyId` à [!DNL Target] dans la commande `sendEvent`, à l’aide de l’espace de noms d’identifiant que vous avez configuré à l’étape 1.
[En savoir plus sur l’envoi d’identifiants](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)

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
