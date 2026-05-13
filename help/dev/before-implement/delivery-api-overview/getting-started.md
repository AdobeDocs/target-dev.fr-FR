---
title: Prise en main de l’API de diffusion Adobe Target
description: Comment utiliser le [!UICONTROL Adobe Target Delivery API] ?
keywords: API de diffusion
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/DC-YVq6VfAaqMU1utmIMw73gzp4PIJgQjaS0a8FQEO4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 116
ht-degree: 1%

---

# Prise en main du [!UICONTROL Adobe Target Delivery API]

Un appel [!UICONTROL Target Delivery API] ressemble à ceci :

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

Le `clientCode` peut être récupéré à partir de l’interface utilisateur de [!DNL Target] en accédant à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Avant d’effectuer un appel [!UICONTROL Target Delivery API], procédez comme suit pour vous assurer qu’une réponse contient l’expérience pertinente à montrer aux utilisateurs finaux :

1. Créez une activité de [!DNL Target] (A/B, XT, AP ou Recommendations) à l’aide du [compositeur basé sur les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr) ou du [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr).
1. Utilisez l’API de diffusion pour obtenir une réponse pour les mbox utilisées dans l’activité de [!DNL Target] créée à l’étape 2.
1. Présentez l’expérience au visiteur.
