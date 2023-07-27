---
title: Présentation de l’artefact de règle de prise de décision sur l’appareil
description: Découvrez comment utiliser l’artefact de règle, qui est une représentation JSON de votre [!DNL Adobe Target] [!UICONTROL prise de décision sur appareil] activités.
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Aperçu de l’artefact de règle

L’artefact de règle est une représentation JSON de votre [!DNL Adobe Target] [!UICONTROL prise de décision sur appareil] activités. Il est généré par [!DNL Adobe Target] et propagé vers le réseau de diffusion de contenu Akamai pour s’assurer qu’un artefact de règle est disponible aussi près que possible de vos utilisateurs finaux. Il contient des métadonnées qui assurent une exécution et une diffusion précises de vos activités, tout en permettant des analyses en temps réel via le suivi des événements. La variable [!DNL Adobe Target] Les SDK peuvent être configurés de manière à permettre la gestion automatique de l’artefact de règle, par lequel il peut être téléchargé ou mis à jour selon un intervalle de temps défini par l’utilisateur. De plus, vous pouvez également gérer votre propre copie locale de l’artefact de règle à l’aide d’un système de mise en cache de mémoire distribuée, comme [Mis en cache](https://memcached.org/) pour initialiser la variable [!DNL Adobe Target] SDK, de sorte que vos serveurs sans état puissent traiter immédiatement les requêtes. Pour en savoir plus sur ces options, consultez les guides suivants :

* [Téléchargement, stockage et mise à jour automatique de l’artefact de règle via le [!DNL Adobe Target] SDK](rule-artifact-sdk.md)
* [Téléchargement, stockage et mise à jour de l’artefact de règle via la charge utile JSON](rule-artifact-json.md)

## Exemple d’artefact de règle

Cliquez ici pour consulter un exemple du [artefact de règle](rule-artifact-example.md).

## Affichage de l’artefact de règle pour votre client

L’activation des traces génère des informations supplémentaires à partir de [!DNL Adobe Target] en ce qui concerne l’artefact de règle, en particulier l’URL.

1. Accédez à l’interface utilisateur de Target.

   &lt;!— Insérer image-target-ui-1.png —>
   ![image alternative](assets/asset-rule-artifact-1.png)

1. Accédez à **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]** et cliquez sur **[!UICONTROL Générer un nouveau jeton d’autorisation]**.

   &lt;!— Insérer image-target-ui-2.png —>
   ![image alternative](assets/asset-rule-artifact-2.png)

1. Copiez le jeton d’autorisation nouvellement généré dans le Presse-papiers et ajoutez-le à votre requête Target.

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

1. Sortez Target Trace via le terminal pour afficher les détails sur l’artefact. L&#39;URL est accessible à partir de la `artifactLocation` Variable .

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
