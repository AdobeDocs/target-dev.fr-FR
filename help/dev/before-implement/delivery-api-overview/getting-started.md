---
title: Prise en main de l’API de diffusion Adobe Target
description: Comment utiliser la variable [!UICONTROL API de diffusion Adobe Target]?
keywords: api de diffusion
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Prise en main du [!UICONTROL API de diffusion Adobe Target]

A [!UICONTROL API de diffusion Target] se présente comme suit :

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

La variable `clientCode` peut être récupéré à partir de la fonction [!DNL Target] l’interface utilisateur en accédant à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]**.

Avant d’effectuer une [!UICONTROL API de diffusion Target] appelez , procédez comme suit pour vous assurer qu’une réponse contient l’expérience appropriée pour afficher aux utilisateurs finaux :

1. Créez un [!DNL Target] activité (A/B, XT, AP ou Recommendations) utilisant la variable [Compositeur d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) ou le [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. Utilisez l’API de diffusion pour obtenir une réponse pour les mbox utilisées dans la variable [!DNL Target] activité créée à l’étape 2.
1. Présenter l’expérience au visiteur.

## Collection Postman {#postman}

Postman est une application qui permet de déclencher facilement des appels API. [Cette collection Postman](https://run.pstmn.io/button.svg) contient des exemples d’appels API de diffusion.
