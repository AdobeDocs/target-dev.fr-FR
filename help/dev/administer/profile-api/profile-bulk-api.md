---
title: API de mise à jour du profil en bloc d’Adobe Target
description: Découvrez comment utiliser [!DNL Adobe Target] [!UICONTROL API de mise à jour des profils en masse] pour envoyer des données de profil de plusieurs visiteurs à [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 43f4fb8345a77ccb0e112fe196e7e0944cc468c9
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 9%

---

# [!DNL Adobe Target Bulk Profile Update API]

La variable [!DNL Adobe Target] [!UICONTROL API de mise à jour des profils en masse] permet de mettre à jour les profils utilisateur de plusieurs visiteurs d’un site web en masse à l’aide d’un fichier de commandes.

En utilisant la variable [!UICONTROL API de mise à jour des profils en masse], vous pouvez facilement envoyer des données détaillées sur le profil du visiteur sous la forme de paramètres de profil à de nombreux utilisateurs. [!DNL Target] de n’importe quelle source externe. Les sources externes peuvent inclure des systèmes de gestion de la relation client (CRM) ou de point de vente (POS), qui ne sont généralement pas disponibles sur une page web.

| Version | Exemple d’URL | Fonctionnalités |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate` | Prise en charge de la mise à jour des profils en masse uniquement. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Créez un profil s’il est introuvable.</li><li>Mise à jour de l’état par ligne.</li></ul> |

>[!NOTE]
>
>Version 2 (v2) du [!UICONTROL API de mise à jour des profils en masse] est la version actuelle. Cependant, [!DNL Target] prend toujours en charge la version 1 (v1).

## Avantages de l’API de mise à jour du profil en bloc

* Nombre d’attributs de profil illimité.
* Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et de la manière inverse.

## Avertissements

* La taille du fichier de traitement par lot doit être inférieure à 50 Mo. En outre, le nombre total de lignes ne doit pas dépasser 500 000 lignes par téléchargement.
* Le nombre de lignes que vous pouvez transférer sur une période de 24 heures dans les lots suivants n’est pas limité. Cependant, le processus d’assimilation peut être ralenti pendant les heures ouvrables pour s’assurer que les autres processus s’exécutent efficacement.
* Les appels de mise à jour de lots v2 consécutifs sans appels de mbox intermédiaires pour le même thirdPartyIds remplacent les propriétés mises à jour lors du premier appel de mise à jour de lots.

## Fichier batch

Pour mettre à jour les données de profil en bloc, créez un fichier de commandes. Le fichier de commandes est un fichier texte dont les valeurs sont séparées par des virgules, comme dans l’exemple de fichier suivant.

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

Vous référencez ce fichier dans l’appel du POST à [!DNL Target] serveurs pour traiter le fichier. Lors de la création du fichier de commandes, tenez compte des points suivants :

* La première ligne du fichier doit spécifier les en-têtes de colonne.
* Le premier en-tête doit être un `pcId` ou `thirdPartyId`. La variable [!UICONTROL Identifiant visiteur Marketing Cloud] n’est pas prise en charge. [!UICONTROL pcId] est un [!DNL Target]visitorID généré. `thirdPartyId` est un identifiant spécifié par l’application cliente, qui est transmis à [!DNL Target] par le biais d’un appel de mbox comme `mbox3rdPartyId`. Il doit être appelé ici `thirdPartyId`.
* Pour des raisons de sécurité, les paramètres et valeurs que vous spécifiez dans le fichier de lot doivent être codés au format URL à l’aide du codage UTF-8. Les paramètres et valeurs peuvent être transférés vers d’autres noeuds périphériques pour traitement via des requêtes HTTP.
* Les paramètres doivent être au format `paramName` uniquement. Les paramètres affichés dans [!DNL Target] as `profile.paramName`.
* Si vous utilisez [!UICONTROL API de mise à jour des profils en masse] v2, vous n’avez pas besoin de spécifier toutes les valeurs de paramètre pour chaque `pcId`. Les profils sont créés pour tous les `pcId` ou `mbox3rdPartyId` qui est introuvable dans [!DNL Target]. Si vous utilisez la version 1, les profils ne sont pas créés pour les pcIds manquants ou mbox3rdPartyIds.
* La taille du fichier de traitement par lot doit être inférieure à 50 Mo. En outre, le nombre total de lignes ne doit pas dépasser 500 000. Cette limite garantit que les serveurs ne sont pas inondés de requêtes trop nombreuses.
* Vous pouvez envoyer plusieurs fichiers. Cependant, la somme totale des lignes de tous les fichiers que vous envoyez par jour ne doit pas dépasser un million pour chaque client.
* Le nombre d’attributs que vous chargez n’est pas limité. Toutefois, la taille globale d’un profil, y compris les données système, ne doit pas dépasser 2 000 Ko. [!DNL Adobe] recommande d’utiliser moins de 1 000 Ko de stockage pour les attributs de profil.
* Les paramètres et les valeurs sont sensibles à la casse.

## requête de POST HTTP

Envoyez une requête de POST HTTP à [!DNL Target] serveurs Edge pour traiter le fichier. Voici un exemple de requête de POST HTTP pour le fichier batch.txt à l’aide de la commande curl :

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate
``````

Où :

BATCH.TXT est le nom du fichier. CLIENTCODE est la variable [!DNL Target] code client.

Si vous ne connaissez pas votre code client, dans la variable [!DNL Target] clic sur l’interface utilisateur **[!UICONTROL Administration]** > **[!UICONTROL Implémentation]**. Le code client s’affiche dans la variable [!UICONTROL Détails du compte] .

### Inspect de la réponse

v2 renvoie un état de profil par profil et v1 renvoie uniquement l’état global. La réponse comprend un lien vers une autre URL qui comporte le message de réussite profil par profil.

### Exemple de réponse

```
true http://mboxedge19.tt.omtrdc.net/m2/demo/v2/profile/batchStatus?batchId=demo-1845664501&m2Node=00 Batch submitted for processing
```

En cas d’erreur, la réponse contient `success=false` et un message d’erreur détaillé.

Une réponse réussie ressemble à ce qui suit :

``````
demo-1845664501 1436187396849-250353.03_03 success 2403081156529-351655.03_03 success 2403081156529-351656.03_03 success 1436187396849-250351.01_00 success 
``````

Les valeurs attendues pour les champs d’état sont les suivantes :

**success**: le profil a été mis à jour. Si le profil est introuvable, l’un d’eux a été créé avec les valeurs du lot.
**error**: le profil n’a pas été mis à jour ou créé en raison d’un échec, d’une exception ou d’une perte de message.
**en attente**: le profil n’a pas encore été mis à jour ou créé.


