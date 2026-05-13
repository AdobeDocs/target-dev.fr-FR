---
title: Comprendre l’artefact de règle de prise de décision sur l’appareil
description: Découvrez comment utiliser l’artefact de règle, qui est une représentation JSON de vos activités  [!DNL Adobe Target] [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
TQID: https://experienceleague.adobe.com/mPzCK-vBYFAQnslX-8FPsBaeSiYtyxjZv76anbpHWuE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# Aperçu de l’artefact de règle

L’artefact de règle est une représentation JSON de vos activités de [!UICONTROL on-device decisioning] [!DNL Adobe Target]. Elle est générée par [!DNL Adobe Target] et propagée sur le réseau CDN Akamai afin de s’assurer qu’un artefact de règle est disponible aussi près que possible de vos utilisateurs finaux. Il contient des métadonnées qui assurent une exécution et une diffusion précises de vos activités, tout en permettant des analyses en temps réel via le suivi des événements. Les SDK [!DNL Adobe Target] peuvent être configurés de manière à permettre la gestion automatique de l’artefact de règle, grâce auquel il peut être téléchargé ou mis à jour selon un intervalle de temps spécifié par l’utilisateur. De plus, vous pouvez également conserver votre propre copie locale de l’artefact de règle à l’aide d’un système de mise en cache de la mémoire distribuée tel que [Memcached](https://memcached.org/) pour initialiser le SDK [!DNL Adobe Target], de sorte que vos serveurs sans état puissent traiter les requêtes immédiatement. Pour en savoir plus sur ces options, consultez les guides suivants :

* [Téléchargement, stockage et mise à jour automatique de l’artefact de règle via le [!DNL Adobe Target] SDK](rule-artifact-sdk.md)
* [Téléchargement, stockage et mise à jour de l’artefact de règle via la payload JSON](rule-artifact-json.md)

## Exemple d’artefact de règle

Cliquez ici pour obtenir un exemple de l’[artefact de règle](rule-artifact-example.md).

## Comment afficher l’artefact de règle pour votre client

L’activation des traces génère des informations supplémentaires à partir de [!DNL Adobe Target] en ce qui concerne l’artefact de règle, en particulier l’URL.

1. Accédez à l’interface utilisateur de Target.

   &lt;!— Insérer image-target-ui-1.png —>
   ![image alternative](assets/asset-rule-artifact-1.png)

1. Accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** et cliquez sur **[!UICONTROL Generate New Authorization Token]**.

   &lt;!— Insérer image-target-ui-2.png —>
   ![image alternative](assets/asset-rule-artifact-2.png)

1. Copiez le jeton d’autorisation nouvellement généré dans le presse-papiers et ajoutez-le à votre requête Target.

   ```javascript {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: '88f1a924-6bc5-4836-8560-2f9c86aeb36b'
     },
     execute: {
       mboxes: [{
         address: getAddress(req),
         name: "node-sdk-mbox"
       }]
   }};
   ```

1. Générez la trace de Target via le terminal pour afficher les détails sur l’artefact. L’URL est accessible via la variable `artifactLocation` .

   ```
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.bin",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
        "clientCode": "your-client-code",
      "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```
