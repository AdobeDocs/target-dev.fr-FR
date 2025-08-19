---
title: API de mise à jour du profil en bloc Adobe Target
description: Découvrez comment utiliser  [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] pour envoyer les données de profil de plusieurs visiteurs à afin  [!DNL Target]  les utiliser dans le ciblage.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: dae198fd8ef3fc8473ad31807c146802339b1832
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 7%

---

# [!DNL Adobe Target Bulk Profile Update API]

Le [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] vous permet de mettre à jour en bloc les profils utilisateur de plusieurs visiteurs d’un site web à l’aide d’un fichier de commandes.

À l’aide de l’[!UICONTROL Bulk Profile Update API] , vous pouvez envoyer des données de profil de visiteur détaillées sous la forme de paramètres de profil à de nombreux utilisateurs à [!DNL Target] de n’importe quelle source externe. Les sources externes peuvent inclure les systèmes de gestion de la relation client (CRM) ou de point de vente (POS), qui ne sont généralement pas disponibles sur une page web.

| Version | Exemple d’URL | Fonctionnalités |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Prise en charge de la mise à jour de profil en masse uniquement. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Créer le profil s’il est introuvable.</li><li>Mise à jour du statut par ligne.</li></ul> |

>[!NOTE]
>
>La version 2 (v2) du [!DNL Bulk Profile Update API] est la version actuelle. Toutefois, [!DNL Target] continue de prendre en charge la version 1 (v1).
>
>* Si votre implémentation de [!DNL Target] utilise [!DNL Experience Cloud ID] (ECID) comme identifiant de profil pour les visiteurs anonymes, n’utilisez pas `pcId` comme clé dans un fichier de commandes de la version 2 (v2). L’utilisation de `pcId` avec la version v2 du [!DNL Bulk Profile Update API] est réservée aux implémentations [!DNL Target] autonomes qui ne reposent pas sur l’ECID.
>
>* Si votre mise en œuvre utilise l’ECID pour l’identification du profil et que vous souhaitez utiliser `pcId` comme clé dans le fichier par lot, utilisez la version 1 (v1) de l’API.
>
>* Si votre implémentation utilise `thirdPartyId` pour l’identification de profil, utilisez la version 2 (v2) de l’API avec `thirdPartyId` comme clé.

## Avantages du [!UICONTROL Bulk Profile Update API]

* Nombre d’attributs de profil illimité.
* Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et inversement.

## Avertissements

* La taille du fichier de traitement par lot doit être inférieure à 50 Mo. En outre, le nombre total de lignes ne doit pas dépasser 500 000 lignes par téléchargement.
* Les mises à jour se produisent généralement en moins d’une heure, mais leur prise en compte peut prendre jusqu’à 24 heures.
* Le nombre de lignes que vous pouvez charger sur une période de 24 heures dans les lots suivants n’est pas limité. Cependant, le processus d’assimilation peut être ralenti pendant les heures ouvrables pour s’assurer que les autres processus s’exécutent efficacement.
* Les appels de mise à jour par lots v2 consécutifs sans appels de mbox entre les deux pour le même thirdPartyIds remplacent les propriétés mises à jour dans le premier appel de mise à jour par lots.
* [!DNL Adobe] ne garantit pas que 100 % des données de profil par lot seront intégrées et conservées dans Target et pourront donc être utilisées dans le ciblage. Dans la conception actuelle, il est possible qu’un petit pourcentage de données (jusqu’à 0,1 % des grands lots de production) ne soit pas intégré ou conservé.

## Fichier de commandes

Pour mettre à jour les données de profil en bloc, créez un fichier de commandes. Le fichier de commandes est un fichier texte dont les valeurs sont séparées par des virgules, semblable au fichier d’exemple suivant.

``` ```
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``` ```

>[!NOTE]
>
>Le paramètre `batch=` est obligatoire et doit être spécifié au début du fichier.

Vous référencez ce fichier dans l’appel POST aux serveurs [!DNL Target] pour le traiter. Lors de la création du fichier de commandes, tenez compte des points suivants :

* La première ligne du fichier doit spécifier les en-têtes de colonne.
* Le premier en-tête doit être un `pcId` ou un `thirdPartyId`. Le [!UICONTROL Marketing Cloud visitor ID] n’est pas pris en charge. [!UICONTROL pcId] est un visitorID généré par [!DNL Target]. `thirdPartyId` est un identifiant spécifié par l’application cliente et transmis à [!DNL Target] par le biais d’un appel de mbox, selon les `mbox3rdPartyId`. Il faut l&#39;appeler ici `thirdPartyId`.
* Pour des raisons de sécurité, les paramètres et valeurs que vous spécifiez dans le fichier par lot doivent être encodés en URL à l’aide d’UTF-8. Les paramètres et les valeurs peuvent être transférés vers d’autres nœuds Edge pour traitement via des requêtes HTTP.
* Les paramètres doivent être au format `paramName` uniquement. Les paramètres s’affichent dans [!DNL Target] sous la forme `profile.paramName`.
* Si vous utilisez [!UICONTROL Bulk Profile Update API] v2, il n’est pas nécessaire de spécifier toutes les valeurs de paramètre pour chaque `pcId`. Les profils sont créés pour tout `pcId` ou `mbox3rdPartyId` introuvable dans [!DNL Target]. Si vous utilisez v1, les profils ne sont pas créés pour les pcIds ou mbox3rdPartyIds manquants.
* La taille du fichier de traitement par lot doit être inférieure à 50 Mo. En outre, le nombre total de lignes ne doit pas dépasser 500 000. Cette limite permet de s’assurer que les serveurs ne sont pas submergés par un trop grand nombre de requêtes.
* Vous pouvez envoyer plusieurs fichiers. Cependant, la somme totale des lignes de tous les fichiers que vous envoyez au cours d’une journée ne doit pas dépasser un million pour chaque client.
* Le nombre d’attributs que vous pouvez charger n’est pas limité. Cependant, la taille totale des données de profil externes, qui comprennent les attributs du client, l’API de profil, les paramètres de profil In-Mbox et la sortie de script de profil, ne doit pas dépasser 64 Ko.
* Les paramètres et les valeurs sont sensibles à la casse.

## Requête HTTP POST

Envoyez une requête HTTP POST aux serveurs Edge de [!DNL Target] pour traiter le fichier. Voici un exemple de requête HTTP POST pour le fichier batch.txt à l’aide de la commande curl :

``` ```
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``` ```

Où :

BATCH.TXT est le nom du fichier. CLIENTCODE est le code client [!DNL Target].

Si vous ne connaissez pas votre code client, dans l’interface utilisateur [!DNL Target], cliquez sur **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. Le code client s’affiche dans la section [!UICONTROL Account Details] .

### Inspecter la réponse

L’API Profiles renvoie le statut d’envoi du lot à traiter, ainsi qu’un lien sous « batchStatus » vers une autre URL qui indique le statut global du traitement par lots spécifique.

### Exemple de réponse d’API

Le code suivant extrait est un exemple de réponse de l’API Profiles :

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

En cas d’erreur, la réponse contient `success=false` et un message détaillé correspondant.

### Réponse par défaut au statut du lot

Une réponse par défaut réussie lorsque l’utilisateur clique sur le lien URL `batchStatus` ci-dessus ressemble à ce qui suit :

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Les valeurs attendues pour les champs de statut sont les suivantes :

| État | Détails |
| --- | --- |
| [!UICONTROL complete] | La demande de mise à jour du lot de profils a été effectuée avec succès. |
| [!UICONTROL incomplete] | La demande de mise à jour par lots de profils est toujours en cours de traitement et n’est pas terminée. |
| [!UICONTROL stuck] | La demande de mise à jour par lots du profil est bloquée et n’a pas pu être terminée. |

### Réponse détaillée d’URL de statut du lot

Une réponse plus détaillée peut être récupérée en transmettant un `showDetails=true` de paramètre à l’URL `batchStatus` ci-dessus.

Par exemple :

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### Réponse détaillée

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```
