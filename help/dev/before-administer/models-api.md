---
title: Présentation de l’API des modèles d’Adobe
description: Présentation de l’API Modèles, que les utilisateurs peuvent utiliser pour empêcher l’inclusion de fonctionnalités dans les modèles d’apprentissage automatique.
exl-id: e34b9b03-670b-4f7c-a94e-0c3cb711d8e4
feature: APIs/SDKs, Recommendations, Administration & Configuration
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 2%

---

# Présentation de l’API de modèles

L’API Modèles, également appelée API de Liste bloquée, permet aux utilisateurs d’afficher et de gérer la liste des fonctionnalités utilisées dans les modèles d’apprentissage automatique pour [!UICONTROL Automated Personalization] (AP) et [!DNL Auto-Target] (AT). Si un utilisateur souhaite exclure une fonctionnalité des modèles utilisés pour les activités AP ou AT, il peut utiliser l’API Modèles pour ajouter cette fonctionnalité à la &quot;liste bloquée&quot;.

A **[!UICONTROL liste bloquée]** définit l’ensemble des fonctionnalités qui seront exclues par [!DNL Adobe Target] de ses modèles d’apprentissage automatique. Pour plus d’informations sur les fonctionnalités, voir [Données utilisées par [!DNL Target] algorithmes d’apprentissage automatique](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/ap-data.html).

Des Listes bloquées peuvent être définies par activité (niveau d’activité) ou pour toutes les activités au sein d’une [!DNL Target] compte (niveau global).

<!-- To get started with the Models API in order to create and manage your blocklist, download the Postman Collection [here](https://git.corp.adobe.com/target/ml-configuration-management-service/tree/nextRelease/rest_api_library). Note this is an Adobe internal link. Need to publish this publicly if want to share with customers. -->

## Spécification de l’API de modèles

Affichage de la spécification de l’API de modèles [here](../administer/models-api/models-api-overview.md).

## Conditions préalables

Pour utiliser l’API Modèles, vous devez configurer l’authentification à l’aide du [Console Adobe Developer](https://developer.adobe.com/console/home), comme vous le feriez avec le [API d’administration de Target](../administer/admin-api/admin-api-overview-new.md). Pour plus d’informations, voir [Configuration de l’authentification](../before-administer/configure-authentication.md).

## Directives d’utilisation de l’API de modèles

Gestion des listes bloquées

[**Étape 1 :**](#step1) Affichage de la liste des fonctionnalités d’une activité

[**Étape 2 :**](#step2) Vérifier la liste bloquée de l’activité

[**Étape 3 :**](#step3) Ajout de fonctionnalités à la liste bloquée de l’activité

[**Étape 4 :**](#step4) (Facultatif) Débloquer

[**Étape 5 :**](#step5) (Facultatif) Gestion de la liste bloquée globale


## Étape 1 : afficher la liste des fonctionnalités d’une activité {#step1}

Avant de placer sur la liste bloquée une fonctionnalité, consultez la liste des fonctionnalités actuellement incluses dans les modèles de cette activité.

>[!BEGINTABS]

>[!TAB Demande]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/<campaignId>
```

>[!TAB Réponse]

```json {line-numbers="true"}
{
    "features": [
        {
            "externalName": "Visitor Profile - Total Visits to Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Total Visits",
            "internalName": "SES_TOTAL_SESSIONS",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Pages Seen Before Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Activity Lifetime Time on Site",
            "internalName": "SES_TOTAL_TIME",
            "type": "CONTINUOUS"
        }
    ],
    "reportParameters": {
        "clientCode": <tenant>,
        "campaignId": <campaignId>
    }
}
```

>[!ENDTABS]

<!-- JUDY: Update codeblock above once you have the complete Response. -->

Dans l’exemple illustré ici, l’utilisateur vérifie la liste des fonctionnalités utilisées dans le modèle pour l’activité dont l’ID d’activité est 260840.

![Étape 1](assets/models-api-step-1.png)

>[!NOTE]
>
>Pour trouver l’ID d’activité de votre activité, accédez à la Liste des activités dans la [!DNL Target] Interface utilisateur. Cliquez sur l’activité qui vous intéresse. L’ID d’activité s’affiche dans le corps de la page d’aperçu des activités qui en résulte, ainsi qu’à la fin de l’URL de cette page.

La variable **[!UICONTROL externalName]** est un nom convivial d’une fonctionnalité. Il est créé par [!DNL Target], et il est possible que cette valeur change au fil du temps. Les utilisateurs peuvent afficher ces noms conviviaux dans la variable [Rapport Informations sur la personnalisation](https://experienceleague.adobe.com/docs/target/using/reports/insights/personalization-insights-reports.html).

La variable **[!UICONTROL internalName]** est l’identifiant réel de la fonctionnalité. Il est également créé par [!DNL Target], mais il ne peut pas être modifié. Il s’agit de la valeur à référencer pour identifier la ou les fonctionnalités que vous souhaitez placer sur la liste bloquée.

Notez que pour que la liste de fonctionnalités soit renseignée avec des valeurs (c’est-à-dire, pour qu’elle ne soit pas nulle), une activité :

1. Posséder le statut = En direct ou avoir été activé précédemment
1. L’exécution doit avoir été suffisamment longue pour qu’il y ait une activité de campagne, de sorte que le modèle comporte des données à exécuter.

## Etape 2 : Vérifier la liste bloquée de l&#39;activité {#step2}

Affichez ensuite la liste bloquée. En d’autres termes, vérifiez quelles fonctionnalités, le cas échéant, sont actuellement bloquées pour être incluses dans les modèles de cette activité.

>[!ERROR]
>
>Notez que `/blockList/` est sensible à la casse dans la requête.

>[!BEGINTABS]

>[!TAB Demande]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>
```

>[!TAB Réponse]

```json {line-numbers="true"}

```

>[!ENDTABS]

Dans l’exemple illustré ici, l’utilisateur vérifie la liste des fonctionnalités bloquées pour l’activité dont l’ID d’activité est 260840. Les résultats sont vides, ce qui signifie que cette activité ne comporte actuellement aucune fonctionnalité placée sur la liste bloquée.

![Étape 2](assets/models-api-step-2.png)

>[!NOTE]
>
>Vous pouvez voir des résultats vides comme celui-ci, la première fois que vous vérifiez la liste bloquée complète, avant d’y ajouter des fonctionnalités. Cependant, une fois que vous avez ajouté (et par la suite supprimé) des fonctionnalités d’une liste bloquée, vous pouvez voir des résultats légèrement différents, dans lesquels un tableau de fonctionnalités placées sur la liste bloquée vide est renvoyé. Poursuivez la lecture pour voir un exemple de cela dans [Étape 4](#step4).

## Étape 3 : Ajout de fonctionnalités à la liste bloquée de l’activité {#step3}

Pour ajouter des fonctionnalités à la liste bloquée, remplacez la requête de GET par PUT, puis modifiez le corps de la requête pour spécifier la variable `blockedFeatureSources` ou `blockedFeatures` selon vos besoins.

* Le corps de la requête nécessite : `blockedFeatures` ou `blockedFeatureSources`. Les deux peuvent être inclus.
* Renseigner `blockedFeatures` avec des valeurs identifiées à partir de `internalName`. Voir [Étape 1](#step1).
* Renseigner `blockedFeatureSources` avec les valeurs du tableau ci-dessous.

Notez que `blockedFeatureSources` indique d’où provient une fonctionnalité. Pour placer sur la liste bloquée, ils servent de groupes ou de catégories de fonctionnalités, ce qui permet aux utilisateurs de bloquer simultanément des ensembles complets de fonctionnalités. Les valeurs de `blockedFeatureSources` correspond aux premiers caractères de l’identifiant d’une fonction (`blockedFeatures` ou `internalName` ) ; ils peuvent donc être également considérés comme des &quot;préfixes de fonctionnalités&quot;.

### Tableau de `blockedFeatureSources` values {#table}

| Préfixe | Description |
| --- | --- |
| BOX | Paramètre de mbox |
| URL | Personnalisé - Paramètre d’URL |
| ENV | Environnement |
| SES | Profil du visiteur |
| GEO | Emplacement géographique |
| PRO | Personnalisé - Profil |
| SEG | Personnalisé - Segment de création de rapports |
| AAM | Personnalisé - Segment Experience Cloud |
| MOB | Mobile |
| CRS | Personnalisé - Attributs du client |
| UPA | Personnalisé - Attribut de profil RT-CDP |
| IAC | Centres d’intérêt du visiteur |  |

>[!BEGINTABS]

>[!TAB Demande]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": ["AAM"],
    "blockedFeatures": ["SES_PREVIOUS_VISIT_COUNT", "SES_TOTAL_SESSIONS"]
}
```

>[!TAB Réponse]

```json {line-numbers="true"}
{
    "blockedFeatures": [
            "SES_PREVIOUS_VISIT_COUNT",
            "SES_TOTAL_SESSIONS"
        ],
    "blockedFeatureSources": [
            "AAM"
        ]
}
```

>[!ENDTABS]

Dans l’exemple illustré ici, l’utilisateur bloque deux fonctionnalités : `SES_PREVIOUS_VISIT_COUNT` et `SES_TOTAL_SESSIONS`, qu’ils ont précédemment identifié en interrogeant la liste complète des fonctionnalités de l’activité dont l’ID d’activité est 260480, comme décrit dans la section [Étape 1](#step1). Elles bloquent également toutes les fonctionnalités provenant des segments Experience Cloud, ce qui se fait en bloquant les fonctionnalités avec le préfixe &quot;AAM&quot;, comme décrit dans la section [table](#table) ci-dessus.

![Étape 3](assets/models-api-step-3.png)

Notez qu’après avoir placé sur la liste bloquée une fonction, il est recommandé de vérifier la liste bloquée mise à jour en procédant comme suit : [Étape 2](#step2) à nouveau (GET de la liste bloquée). Vérifiez que les résultats s’affichent comme prévu (vérifiez que les résultats incluent les fonctionnalités ajoutées à partir de la dernière requête de PUT).

## Étape 4 : (facultative) Débloquer {#step4}

Pour débloquer toutes les fonctionnalités placées sur la liste bloquée, effacez les valeurs de `blockedFeatureSources` ou `blockedFeatures`.

>[!BEGINTABS]

>[!TAB Demande]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": [],
    "blockedFeatures": []
}
```

>[!TAB Réponse]

```json {line-numbers="true"}
{
    "blockedFeatures": [],
    "blockedFeatureSources": []
}
```

>[!ENDTABS]

Dans l’exemple illustré ici, l’utilisateur efface sa liste bloquée pour l’activité dont l’ID d’activité est 260840. Notez que la réponse confirme les tableaux vides pour les fonctionnalités bloquées et leurs sources—`blockedFeatureSources` et `blockedFeatures`, respectivement.

![Étape 4](assets/models-api-step-4.png)

Comme toujours, après avoir modifié la liste bloquée, il est recommandé d’effectuer les opérations suivantes : [Étape 2](#step2) à nouveau (GET de la liste bloquée pour vérifier que la liste inclut des fonctionnalités comme prévu). Dans l’exemple illustré ici, l’utilisateur vérifie que sa liste bloquée est désormais vide.

![Étape 4b](assets/models-api-step-4b.png)

Question : Comment puis-je supprimer une partie, mais pas toutes, d’une liste bloquée ?

Réponse : pour supprimer un sous-ensemble distinct de fonctionnalités placées sur la liste bloquée d’une liste bloquée multifonction, les utilisateurs peuvent simplement envoyer la liste mise à jour des fonctionnalités qu’ils souhaitent bloquer. [requête de liste bloquée](#step3), plutôt que d’effacer la liste bloquée entière et de rajouter les fonctionnalités souhaitées. En d’autres termes, envoyez la liste des fonctionnalités mises à jour (comme illustré dans la section [Étape 3](#step3)), en veillant à exclure de la liste bloquée les fonctionnalités que vous souhaitez &quot;supprimer&quot;.

## Étape 5 : (facultative) Gestion de la liste bloquée globale {#step5}

Les exemples ci-dessus étaient tous dans le contexte d’une seule activité. Vous pouvez également bloquer des fonctionnalités pour toutes les activités sur un client donné (client), au lieu d’avoir à spécifier la liste bloquée de chaque activité individuellement. Pour effectuer une liste bloquée globale, utilisez la méthode `/blockList/global` appelez, au lieu de `blockList/<campaignId>`.

>[!BEGINTABS]

>[!TAB Demande]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/global

{
    "blockedFeatureSources": ["AAM", "PRO", "ENV"],
    "blockedFeatures": ["AAM_FEATURE_1", "AAM_FEATURE_2"]
}
```

>[!TAB Réponse]

```json {line-numbers="true"}
{
    "blockedFeatures": [
        "AAM_FEATURE_1",
        "AAM_FEATURE_2"
    ],
    "blockedFeatureSources": [
        "AAM",
        "PRO",
        "ENV"
    ]
}
```

>[!ENDTABS]

Dans l’exemple de requête illustré ci-dessus, l’utilisateur bloque deux fonctionnalités, &quot;AAM_FEATURE_1&quot; et &quot;AAM_FEATURE_2&quot;, pour toutes les activités de la requête. [!DNL Target] compte . Cela signifie que, quelle que soit l’activité, &quot;AAM_FEATURE_1&quot; et &quot;AAM_FEATURE_2&quot; ne seront pas inclus dans les modèles d’apprentissage automatique pour ce compte. En outre, l’utilisateur bloque également globalement toutes les fonctionnalités dont le préfixe est &quot;AAM&quot;, &quot;PRO&quot; ou &quot;ENV&quot;.

Question : L’exemple de code ci-dessus n’est-il pas redondant ?

Réponse : Oui. Il est redondant de bloquer les fonctionnalités avec des valeurs commençant par &quot;AAM&quot;, tout en bloquant également toutes les fonctionnalités dont la source est &quot;AAM&quot;. Par conséquent, toutes les fonctionnalités provenant d’AAM (segments Experience Cloud) seront bloquées. Par conséquent, si l’objectif est de bloquer toutes les fonctionnalités des segments Experience Cloud, la spécification individuelle de certaines fonctionnalités commençant par &quot;AAM&quot; n’est pas nécessaire, dans l’exemple ci-dessus.

Étape finale : que ce soit au niveau de l’activité ou global, il est recommandé de vérifier votre liste bloquée après l’avoir modifiée, afin de vous assurer qu’elle contient les valeurs attendues. Pour ce faire, modifiez la variable `PUT` à `GET`.

L’exemple de réponse illustré ci-dessous indique : [!DNL Target] bloque deux fonctions individuelles, plus toutes celles provenant de &quot;AAM&quot;, &quot;PRO&quot; et &quot;ENV&quot;.

![Étape 5](assets/models-api-step-5.png)
