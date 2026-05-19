---
keywords: rgpd, ue, union européenne, confidentialité, faq, questions fréquentes, california consumer privacy act, ccpa, confidentialité, protection des données, opt-out, gouvernement, réglementation, rgpd5, rgpd6, rgpd7, rgpd8, rgpd9, eu0, eu1, eu2, eu3, eu4, eu5
description: Découvrez Target et le RGPD (règlement général sur la protection des données), le CCPA (California Consumer Privacy Act) et d’autres exigences internationales en matière de confidentialité.
title: Comment Target gère-t-il les réglementations relatives à la confidentialité et à la protection des données ?
feature: Privacy & Security
exl-id: 40bac3c5-8e6f-4a90-ac0c-eddce1dbe6c0
TQID: https://experienceleague.adobe.com/W-aYBengoNH5uKTcFZNHARelgAFX3-QrZixh09n0FU0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 2432
ht-degree: 61%

---

# Réglementations relatives à la confidentialité et à la protection des données

Informations sur le RGPD (règlement général sur la protection des données), le CCPA (California Consumer Privacy Act) et d’autres exigences internationales en matière de confidentialité. Découvrez comment ces réglementations affectent votre entreprise et Adobe Target.

## Présentation du règlement général sur la protection des données (RGPD)

Le 25 mai 2018, le RGPD de l’Union européenne est entré en vigueur. Pour en savoir sur ce qu’implique ce règlement pour vous, consultez le [RGPD et votre entreprise](https://business.adobe.com/fr/privacy/general-data-protection-regulation.html).

Lorsqu’Adobe fournit des logiciels et des services à une entreprise, elle agit en tant qu’entité de traitement des données pour toutes les données personnelles qu’elle traite et stocke dans le cadre de la prestation de ces services. En tant qu’entité de traitement des données, Adobe traite les données personnelles conformément aux autorisations et aux instructions de votre société (par exemple, tel qu’énoncé dans votre accord avec Adobe).

En tant que contrôleuse ou contrôleur de données, vous déterminez les données personnelles qu’Adobe traite et stocke pour vous. Si vous utilisez les solutions Adobe Experience Cloud, Adobe peut héberger des données personnelles pour vous, en fonction des solutions que vous utilisez et des informations que vous choisissez d’envoyer sur votre compte Adobe Experience Cloud. Pour obtenir une liste détaillée d’exemples, voir [Confidentialité Adobe Experience Cloud](https://www.adobe.com/fr/privacy/experience-cloud.html#collect).

Adobe Experience Cloud fournit aux responsables du traitement des données des API conformes au RGPD qui permettent d’effectuer les tâches suivantes :

* Accéder aux informations du sujet des données stockées dans Target
* Supprimer les informations du sujet des données stockées dans Target

Pour obtenir plus d’informations, voir :

* [Présentation d’Adobe Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=fr)
* [Guide de l’API Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/api/overview.html?lang=fr)
* [Présentation de l’interface utilisateur de Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=fr)

## Présentation du CCPA (California Consumer Privacy Act)

Le CCPA (California Consumer Privacy Act) accorde aux clients de Californie de nouveaux droits concernant leurs informations personnelles et impose des responsabilités en matière de protection des données à certaines entités dont les activités sont basées en Californie. Le CCPA est entré en vigueur le 1er janvier 2020.

À un niveau général, la loi accorde aux Californiens plusieurs droits principaux, notamment les droits de :

* Demander des informations (accès aux données)
* S’exclure de la vente d’informations personnelles (un droit largement défini pour s’exclure du partage d’informations avec des tiers)
* Supprimer des informations personnelles
* Être informé de la divulgation ou de la vente d’informations personnelles

Si vous vous prépariez l’année dernière pour le règlement européen sur la protection des données (RGPD), vous connaissez peut-être certains de ces droits et pouvez réutiliser une grande partie du travail déjà accompli.

>[!NOTE]
>
>L’accès et la suppression des données dans le cadre du CCPA suivent le même processus que pour le RGPD.

## Fonctionnalité de souscription (opt-in) Adobe Target et Adobe Experience Platform

Target fournit une prise en charge de la fonctionnalité de souscription par le biais des balises dans Adobe Experience Platform afin de vous aider à appliquer votre stratégie de gestion du consentement. La fonctionnalité d’opt-in permet aux clients de décider comment et à quel moment la balise Target est déclenchée. Il existe également une option via Adobe Experience Platform pour préapprouver la balise Target. Pour permettre l’utilisation de la fonctionnalité d’accord préalable dans la bibliothèque at.js de Target, vous devez utiliser `targetGlobalSettings` et ajouter le paramètre `optinEnabled=true` . Dans Adobe Experience Platform, sélectionnez « activer » dans la liste déroulante d’accord préalable RGPD dans la vue d’installation de l’extension. Voir [&#x200B; Implémentation de Target à l’aide de Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) pour plus d’informations.

L’extrait de code suivant montre comment activer le paramètre `optinEnabled=true` :

```
window.targetGlobalSettings = {
  optinEnabled: true
};
```

>[!NOTE]
>
>La fonctionnalité de souscription (opt-in) est prise en charge dans at.js version 1.7.0 et at.js 2.1.0 et versions ultérieures. Elle n’est pas prise en charge dans at.js versions 2.0.0 et 2.0.1.

L’utilisation de Adobe Experience Platform pour gérer l’opt-in est l’approche recommandée. Il existe un contrôle granulaire plus poussé dans Adobe Experience Platform. Le but est de masquer, avant le déclenchement de Target, certains éléments de votre page pouvant servir pour votre stratégie de consentement.

Lors de l’utilisation de la fonctionnalité d’opt-in, trois scénarios sont à envisager :

1. **La balise Target est préapprouvée via Adobe Experience Platform (ou la personne concernée ayant précédemment approuvé Target) :** la balise Target n’est pas conservée pour le consentement et fonctionne comme prévu.
1. **La balise Target n’a PAS été préalablement approuvée et la valeur de `bodyHidingEnabled` est FALSE :** La balise Target se déclenche seulement après que le client a donné son consentement. Avant d’avoir reçu le consentement du client, seul le contenu par défaut est disponible. Une fois le consentement reçu, Target est appelé et le contenu personnalisé est disponible pour le sujet de données (visiteur). Il est important de tenir compte du fait que seul le contenu par défaut est disponible avant la réception du consentement, et d’utiliser une stratégie appropriée à la situation. Il s’agit, par exemple, d’utiliser une splash page pour recouvrir les parties ou le contenu d’une page qui pourra être personnalisée. Ce processus permet de faire en sorte que l’expérience reste cohérente pour le titulaire de données (visiteur).
1. **La balise Target n’a PAS été préalablement approuvée et la valeur de `bodyHidingEnabled` est TRUE :** La balise Target se déclenche seulement après que le client a donné son consentement. Avant d’avoir reçu le consentement du client, seul le contenu par défaut est disponible. Cependant, comme le paramètre `bodyHidingEnabled` est défini sur « true », c’est `bodyHiddenStyle` qui définit le contenu qui est masqué jusqu’au déclenchement de la balise Target (sauf si le titulaire de données refuse l’opt-in, ce qui entraînerait l’affichage du contenu par défaut). Par défaut, le paramètre `bodyHiddenStyle` est défini sur `body { opacity:0;}`, ce qui masque la balise HTML body. Vous trouverez ci-dessous la configuration de page recommandée par Adobe : masquage de l’ensemble du corps de la page, à l’exception de la boîte de dialogue du gestionnaire de consentement, en les mettant, celle-ci et le contenu de la page, dans deux conteneurs différents. Cette configuration de Target fait en sorte que seul le conteneur du contenu de la page soit masqué. Consultez la [présentation du Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=fr ?).

   La configuration de page recommandée pour le troisième scénario est la suivante :

   ```
   <html> 
   <head> 
   //visitor, at.js 
   </head> 
   
   <body> 
   <div id = "consentManagerDialog"> 
   
   //consent manager html dialog goes here 
   </div> 
   
   <div id="pageContent"> 
   // page content goes here 
   </div> 
   
   </body> 
   </html> 
   ```

   En supposant que `bodyHiddenStyle` soit :

   ```
   #pageContent { opacity:0;}
   ```

## FAQ sur les réglementations relatives à la confidentialité et à la protection des données

Questions fréquentes sur le RGPD (règlement général sur la protection des données) de l’Union européenne, la loi CCPA (California Consumer Privacy Act) et d’autres exigences internationales en matière de confidentialité spécifiques à Target.

### Quelle est la politique d’Adobe concernant ces réglementations ?

Adobe remplit déjà ou est en train de mettre en œuvre ses obligations en tant que responsable du traitement des données. Adobe dispose d’une base solide de contrôles certifiés de sécurité et de confidentialité dès la conception et a apporté des améliorations aux produits avant l’échéance de mai 2018. Les entreprises clientes ont la responsabilité de mettre en œuvre ces améliorations et de mettre à jour les politiques et procédures nécessaires.

### Ma société, le contrôleur de données, doit-elle envoyer une requête RGPD pour chaque solution Adobe Experience Cloud qu’elle utilise ?

Non, Adobe fournit un moyen centralisé d’aider les responsables du traitement des données à répondre aux exigences du RGPD et du CCPA. Les contrôleurs de données n’ont pas besoin d’accéder directement à chaque solution.

Toutes les requêtes RGPD et CCPA à travers les solutions Experience Cloud, y compris Target, sont effectuées via une API Adobe centrale, actuellement nommée API conforme au RGPD. L’API effectue ensuite la requête à travers la suite de solutions Experience Cloud du contrôleur de données.

### Quelles informations Adobe permet-il aux clients de supprimer en réponse à une demande d’un titulaire de données/utilisateur ?

Les informations relatives à un visiteur individuel dans Target sont contenues dans le profil du visiteur Target. Target permet aux clients de supprimer toutes les données associées à un ID dans leur profil du visiteur. Pour obtenir des exemples de données de profil stockées dans Target, voir [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=fr).

Les données agrégées ou rendues anonymes (par exemple, les données des rapports) qui n’identifient pas une personne spécifique, ou les données qui ne sont pas liées à une personne spécifique (par exemple, les données en matière de contenu), ne sont pas concernées par la demande de suppression soumise par un utilisateur.

Les profils des visiteurs Target inactifs depuis 90 jours sont supprimés par défaut, sans aucune intervention nécessaire.

### Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ?

Target prend en charge les types d’ID suivants pour localiser un profil client :

| Identifiant utilisateur | Type d’ID d’espace de noms | ID d’espace de noms | Définition |
|--- |--- |--- |--- |
| Experience Cloud ID (ECID) | Standard | 4 | Adobe Experience Cloud ID, anciennement connu sous le nom d’identifiant visiteur ou Experience Cloud ID. Vous pouvez utiliser l’API JavaScript pour localiser cet ID (voir les détails ci-dessous). |
| Identifiant TnT / Identifiant du cookie (TNTID) | Standard | 9 | Identifiant cible défini comme cookie dans le navigateur du visiteur. Vous pouvez utiliser l’API JavaScript pour localiser cet ID (voir les détails ci-dessous). |
| ID tiers/ID CRM (THIRDPARTYID) | Spécifique à Target | S.O. | Si vous fournissez à Target votre logiciel de gestion de la relation client ou d’autres informations d’identification uniques pour vos clients. |

>[!NOTE]
>
>Bien que Target prenne en charge les cookies inter-domaines propriétaires et tiers, seuls les cookies Target propriétaires sont recommandés pour le RGPD et le CCPA.

### Comment Target gère-t-il la gestion du consentement ?

Le RGPD et le CCPA ne changent pas lorsque vous devez obtenir un consentement, mais c’est le cas quand il est question de la façon de l’obtenir. La stratégie de consentement de chaque client dépend de sa collecte de données et de ses pratiques d’utilisation, ainsi que de sa politique de confidentialité. La gestion du consentement n’est pas prise en charge par et ne doit pas être réalisée via Target pour le RGPD et le CCPA.

Adobe n’offre pas actuellement de solution de Gestion des consentements, mais divers outils sont en cours d’élaboration sur le marché pour répondre à certaines des nouvelles exigences. Pour de plus amples renseignements sur les outils de confidentialité en général, y compris les gestionnaires de consentement, consultez le [2017 Privacy Tech Vendor Report](https://iapp.org/media/pdf/resource_center/Tech-Vendor-Directory-1.4.1-electronic.pdf) (rapport sur les fournisseurs offrant des technologies de confidentialité) sur le site web de l’*Association internationale des professionnels de la protection de la vie privée (IAPP)*.

Target prend en charge la fonctionnalité d’accord préalable via Adobe Experience Platform pour prendre en charge votre stratégie de gestion du consentement. La fonctionnalité d’opt-in permet aux clients de décider comment et à quel moment la balise Target est déclenchée. Il existe également une option via Adobe Experience Platform pour préapprouver la balise Target. L’utilisation de Adobe Experience Platform pour gérer l’opt-in est l’approche recommandée. Il existe un contrôle granulaire plus poussé dans Adobe Experience Platform. Le but est de masquer, avant le déclenchement de Target, certains éléments de votre page pouvant servir pour votre stratégie de consentement.

Pour plus d’informations sur le RGPD, le CCPA et Adobe Experience Platform, consultez [La bibliothèque JavaScript Adobe Privacy et le RGPD](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=fr ?). Consultez également la section *Fonctionnalité de souscription (opt-in) Adobe Target et Adobe Experience Platform* ci-dessus.

### `AdobePrivacy.js` envoie-t-il des informations à l’API conforme au RGPD ?

AdobePrivacy.js n’envoie *ces informations* l’API . C’est au client de les soumettre. La bibliothèque ne fournit que les ID stockés dans le navigateur pour ce visiteur spécifique.

### Que supprime `removeIdentities` ?

`removeIdentities` *supprime uniquement* ces identités du navigateur, et cela ne dépend que de leur mise en œuvre ou non par la solution Adobe.

Par exemple, Target supprime les cookies qui stockent ses identifiants, mais Adobe Audience Manager (AAM) ne supprime pas l’identifiant demdex stocké dans un cookie tiers.

### Quelles informations doit contenir une requête RGPD ou CCPA de Target ?

Outre les exigences de Central Privacy Service, un message RGPD ou CCPA valide pour Target contient :

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            "namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            "namespace":"TNTID", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"THIRDPARTYID", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
}
```

### Quels types de réponse puis-je attendre de Target via l’API conforme au RGPD ?

| Statut de la requête | Message de la réponse Target | Scénario |
|--- |--- |--- |
| En cours de traitement | En cours de traitement | Target a reçu la requête RGPD ou CCPA et la traite. |
| Complete | Non applicable - contexte d’entreprise non applicable | L’ID IMS dans la requête RGPD ou CCPA n’est associé à aucun client Target.<br />Certaines entreprises disposent de plusieurs ID IMS. Envoyez l’identifiant IMS pour lequel Target est configuré. |
| Complete | Non applicable - contexte utilisateur introuvable | L’ID fourni dans la requête RGPD ou CCPA pour le visiteur ou le titulaire de données spécifique ne figure pas dans le magasin de profils Target.<br />Ce résultat est également retourné si vous tentez d’envoyer un type d’identifiant d’espace de noms non pris en charge par Target (voir ci-dessus les identifiants pris en charge). |
| Erreur | Message d’erreur (les détails dépendent du type d’erreur) | Erreur lors de la récupération ou de la suppression du profil du sujet de données demandé.<br />Erreur lors du chargement vers Azure pour la demande d’accès. |

### Quelle réponse Target envoie-t-il à l’API conforme au RGPD pour une demande d’accès ?

Les réponses aux demandes d’accès aux données contiennent un résumé du profil Target pour le visiteur en question. Ce retour est envoyé à l’API conforme au RGPD d’Experience Cloud, qui envoie à son tour une réponse aux contrôleurs des données.

Un exemple de réponse de l’API à Target pour la demande d’accès pourrait ressembler à ceci :

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            ~"namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            ~"namespace":"tntId", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"thirdPartyId", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
} 
```

| Champ | Description |
|--- |--- |
| jobId | Indique l’ID de tâche RGPD ou CCPA à partir de l’API Central GDPR. |
| imsOrgID | Fournit un identifiant unique pour votre entreprise. |
| espace de noms | Également appelé source de données. Voir « Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ? » dans cette rubrique. |
| type | Le type d’ID pour lequel vous avez demandé l’accès aux données en vertu du RGPD ou du CCPA. Target accepte plusieurs types d’ID, dont certains sont standard et d’autres spécifiques à Target. Voir « Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ? » dans cette rubrique. |
| value | L’ID de l’espace de noms/la source de données. Voir « Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ? » pour les valeurs acceptées. |
| integration code | Les codes d’intégration sont des noms conviviaux pour vos sources de données et vous aident à suivre vos sources de données plus facilement qu’en utilisant des ID de sources de données. |

Lorsque plusieurs valeurs sont fournies pour identifier des profils, chaque identifiant valide dispose d’un fichier de profil. Un ou plusieurs fichiers de profil sont envoyés au Blob Azure RGPD via l’API centrale RGPD, sous le format d’une réponse JSON de profil cible.

Voici un exemple de réponse JSON de profil Target :

```
{"profileAttributes": 
 
"Sample_Parameter":{"value":"Gold Loyalty Status","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"user.ReturnTimeOfDay":{"value":"44.0","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"firstSessionStart":{"value":"1523497450602","modifiedAt":"2018-04-11T21:44:10.000-04:00"}, 
 
"user.sessionCountScript":{"value":"1","modifiedAt":"2018-04-11T21:44:14.000-04:00"} 
   } 
} 
```

Le tableau suivant contient la description des champs illustratifs JSON du profil :

| Champ | Description |
|--- |--- |
| Sample_Parameter | De nombreuses informations du profil Target sont chargées ou directement fournies par le contrôleur des données. Dans cet exemple, un paramètre a été chargé dans le profil Target à l’aide de l’API de mise à jour du profil. Pour plus d’informations, voir [Méthodes pour obtenir des données dans Target](/help/dev/before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md). |
| user.ReturnTimeOfDay | Ce champ standard inclut l’heure de la journée de la dernière visite de retour d’un utilisateur ou d’une utilisatrice. |
| firstSessionStart | Ce champ standard inclut l’heure à laquelle la première session de l’utilisateur a commencé. |
| user.sessionCountScript | De nombreuses informations du profil Target sont chargées ou directement fournies par le contrôleur des données. Dans cet exemple, un script de profil incrémente le nombre de sessions que ce visiteur a effectuées sur le site du contrôleur de données. Pour plus d’informations, voir [Attributs de script de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=fr). |

>[!NOTE]
>
>À titre d’illustration, cet exemple de code est une version abrégée d’un fichier JSON de profil Target. De nombreux champs du profil Target ne sont pas standard. Les données retournées dépendent des informations figurant dans ce profil de visiteur spécifique.

### Target prend-il en charge l’obscurcissement des adresses IP ?

Target prend en charge l’obscurcissement des adresses IP si vous choisissez de l’utiliser dans le cadre de votre stratégie de mise en œuvre du RGPD ou du CCPA. Pour plus d’informations, consultez la page [Confidentialité](privacy.md#replacement-of-last-octet-of-ip-addresses).

### Dois-je faire quelque chose pour empêcher que mes données ne soient partagées ou vendues à des tiers ?

Target ne permet pas aux clients de partager ou de vendre à des tiers des données directement à partir de Target. Il n’y a donc pas d’opposition à la vente pour Target.
