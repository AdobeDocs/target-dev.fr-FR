---
keywords: rgpd, eu, union européenne, confidentialité, faq, questions fréquentes, california consumer privacy act, ccpa, confidentialité, protection des données, opt-out, gouvernement, réglementation, gdpr5, gdpr6, gdpr7, gdpr8, gdpr9, eu0, eu1, eu2, eu3, eu4, eu5, eu5
description: Découvrez Target et le Règlement général sur la protection des données (RGPD) de l’Union européenne, la loi CCPA (California Consumer Privacy Act) et d’autres exigences en matière de confidentialité.
title: Comment Target gère-t-il les réglementations sur la confidentialité et la protection des données ?
feature: Privacy & Security
exl-id: 40bac3c5-8e6f-4a90-ac0c-eddce1dbe6c0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2374'
ht-degree: 64%

---

# Réglementations relatives à la confidentialité et à la protection des données

Informations sur le RGPD (règlement général sur la protection des données), le CCPA (California Consumer Privacy Act) et d’autres exigences internationales en matière de confidentialité. Découvrez comment ces réglementations affectent votre entreprise et Adobe Target.

## Présentation du règlement général sur la protection des données (RGPD) 

Le 25 mai 2018, le RGPD de l’Union européenne est entré en vigueur. Pour en savoir sur ce qu’implique ce règlement pour vous, consultez le [RGPD et votre entreprise](https://business.adobe.com/fr/privacy/general-data-protection-regulation.html).

Lorsqu’Adobe fournit des logiciels et des services à une entreprise, elle agit en tant qu’entité de traitement des données pour toutes les données personnelles qu’elle traite et stocke dans le cadre de la prestation de ces services. En tant qu’entité de traitement des données, Adobe traite les données personnelles conformément aux autorisations et aux instructions de votre société (par exemple, tel qu’énoncé dans votre accord avec Adobe).

En tant que contrôleuse ou contrôleur de données, vous déterminez les données personnelles qu’Adobe traite et stocke pour vous. Si vous utilisez les solutions Adobe Experience Cloud, Adobe peut héberger des données personnelles pour vous, en fonction des solutions que vous utilisez et des informations que vous choisissez d’envoyer sur votre compte Adobe Experience Cloud. Pour obtenir une liste détaillée d’exemples, voir [Confidentialité Adobe Experience Cloud](https://www.adobe.com/fr/privacy/experience-cloud.html#collect).

Adobe Experience Cloud fournit des API conformes au RGPD aux responsables du traitement des données qui leur permettent d’effectuer les tâches suivantes :

* Accéder aux informations du sujet des données stockées dans Target
* Supprimer les informations du sujet des données stockées dans Target

Pour obtenir plus d’informations, voir :

* [Adobe Privacy Service - Aperçu](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=fr)
* [Guide de l’API Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/api/overview.html?lang=fr)
* [Présentation de l’interface utilisateur de Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=fr)

## Présentation du CCPA (California Consumer Privacy Act)

Le CCPA (California Consumer Privacy Act) accorde aux clients de Californie de nouveaux droits concernant leurs informations personnelles et impose des responsabilités en matière de protection des données à certaines entités dont les activités sont basées en Californie. Le CCPA est entré en vigueur le 1er janvier 2020.

À un niveau général, la loi accorde aux Californiens plusieurs droits principaux, notamment les droits de :

* Demander des informations (accès aux données)
* S’exclure de la vente d’informations personnelles (un droit largement défini pour s’exclure du partage d’informations avec des tiers)
* Supprimer des informations personnelles
* Être informé de la divulgation ou de la vente d’informations personnelles

Si vous étiez occupé à vous préparer à la loi européenne sur la protection de la vie privée (RGPD) l&#39;an dernier, certains de ces droits pourraient vous être familiers et une grande partie du travail que vous avez accompli peut être réorientée.

>[!NOTE]
>
>L’accès et la suppression des données dans le cadre du CCPA suivent le même processus que pour le RGPD.

## Inclusion dans Adobe Target et Adobe Experience Platform

Target fournit la prise en charge de la fonctionnalité d’opt-in par le biais de balises dans Adobe Experience Platform afin de vous aider à prendre en charge votre stratégie de gestion des consentements. La fonctionnalité d’opt-in permet aux clients de décider comment et à quel moment la balise Target est déclenchée. Il existe également une option via Adobe Experience Platform permettant d’approuver à l’avance la balise Target. Pour activer la possibilité d’utiliser Opt-in dans la bibliothèque Target at.js, utilisez `targetGlobalSettings` et ajoutez le `optinEnabled=true` . Dans Adobe Experience Platform, sélectionnez &quot;activer&quot; dans la liste déroulante d’inscription RGPD dans la vue d’installation de l’extension. Voir [Mise en oeuvre de Target avec Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) pour plus d’informations.

L’extrait de code suivant montre comment activer le paramètre `optinEnabled=true` :

```
window.targetGlobalSettings = {
  optinEnabled: true
};
```

>[!NOTE]
>
>La fonctionnalité de souscription (opt-in) est prise en charge dans at.js version 1.7.0 et at.js 2.1.0 et versions ultérieures. Elle n’est pas prise en charge dans at.js versions 2.0.0 et 2.0.1.

Il est recommandé d’utiliser Adobe Experience Platform pour gérer les souscriptions (opt-in). Il existe un contrôle granulaire plus poussé dans Adobe Experience Platform pour masquer certains éléments de votre page avant le déclenchement de Target, qui sont utiles dans le cadre de votre stratégie de consentement.

Lors de l’utilisation de la fonctionnalité d’opt-in, trois scénarios sont à envisager :

1. **La balise Target est préalablement approuvée via Adobe Experience Platform (ou la personne concernée a préalablement approuvé Target) :** La balise Target n’est pas conservée pour le consentement et les fonctions comme prévu.
1. **La balise Target n’a PAS été préalablement approuvée et la valeur de `bodyHidingEnabled` est FALSE :** La balise Target se déclenche seulement après que le client a donné son consentement. Avant d’avoir reçu le consentement du client, seul le contenu par défaut est disponible. Une fois le consentement reçu, Target est appelé et le contenu personnalisé est disponible pour le sujet de données (visiteur). Il est important de tenir compte du fait que seul le contenu par défaut est disponible avant la réception du consentement, et d’utiliser une stratégie appropriée à la situation. Il s’agit, par exemple, d’utiliser une splash page pour recouvrir les parties ou le contenu d’une page qui pourra être personnalisée. Ce processus permet de faire en sorte que l’expérience reste cohérente pour le titulaire de données (visiteur).
1. **La balise Target n’a PAS été préalablement approuvée et la valeur de `bodyHidingEnabled` est TRUE :** La balise Target se déclenche seulement après que le client a donné son consentement. Avant d’avoir reçu le consentement du client, seul le contenu par défaut est disponible. Cependant, comme le paramètre `bodyHidingEnabled` est défini sur « true », c’est `bodyHiddenStyle` qui définit le contenu qui est masqué jusqu’au déclenchement de la balise Target (sauf si le titulaire de données refuse l’opt-in, ce qui entraînerait l’affichage du contenu par défaut). Par défaut, le paramètre `bodyHiddenStyle` est défini sur `body { opacity:0;}`, ce qui masque la balise HTML body. Vous trouverez ci-dessous la configuration de page recommandée par Adobe : masquage de l’ensemble du corps de la page, à l’exception de la boîte de dialogue du gestionnaire de consentement, en les mettant, celle-ci et le contenu de la page, dans deux conteneurs différents. Cette configuration de Target fait en sorte que seul le conteneur du contenu de la page soit masqué. Consultez la [présentation du Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=fr?).

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

### Quelle est la politique Adobe de ces réglementations ?

Adobe remplit déjà ou est en train de mettre en oeuvre ses obligations en tant qu’entité de traitement des données. Adobe dispose d’une base solide de contrôles certifiés de sécurité et de confidentialité dès la conception et a apporté des améliorations aux produits avant l’échéance de mai 2018. Les entreprises clientes ont la responsabilité de mettre en œuvre ces améliorations et de mettre à jour les politiques et procédures nécessaires.

### Mon entreprise, le contrôleur de données, doit-elle envoyer une demande RGPD ou CCPA à chaque solution Adobe Experience Cloud qu’elle utilise ?

Non, Adobe fournit un moyen central d’aider les contrôleurs de données à répondre aux exigences du RGPD et du CCPA. Les contrôleurs de données n’ont pas besoin d’accéder directement à chaque solution.

Toutes les demandes RGPD et CCPA à travers les solutions Experience Cloud, y compris Target, passent par une API Adobe centrale, actuellement appelée API relative au RGPD. L’API effectue ensuite la demande dans la suite de solutions Experience Cloud du contrôleur de données.

### Quelles informations Adobe permet-il aux clients de supprimer en réponse à une demande d’un sujet des données/utilisateur ?

Les informations relatives à un visiteur individuel dans Target sont contenues dans le profil du visiteur Target. Target permet aux clients de supprimer toutes les données associées à un identifiant dans leur profil de visiteur. Pour obtenir des exemples de données de profil stockées par Target, voir [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

Les données agrégées ou rendues anonymes (par exemple, les données des rapports) qui n’identifient pas une personne spécifique, ou les données qui ne sont pas liées à une personne spécifique (par exemple, les données en matière de contenu), ne sont pas concernées par la demande de suppression soumise par un utilisateur.

Les profils des visiteurs Target inactifs depuis 90 jours sont supprimés par défaut, sans aucune intervention nécessaire.

### Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ?

Target prend en charge les types d’ID suivants pour localiser un profil client :

| Identifiant utilisateur | Type d’ID d’espace de noms | ID d’espace de noms | Définition |
|--- |--- |--- |--- |
| Experience Cloud ID (ECID) | Standard | 4 | Adobe Experience Cloud ID anciennement connu sous le nom d’ID de visiteur ou d’Experience Cloud ID. Vous pouvez utiliser l’API JavaScript pour localiser cet ID (voir les détails ci-dessous). |
| ID TNT/ID de cookie(TNTID) | Standard | 9 | Identifiant de la cible défini comme cookie dans le navigateur du visiteur. Vous pouvez utiliser l’API JavaScript pour localiser cet ID (voir les détails ci-dessous). |
| ID tiers/ID de gestion de la relation client  (THIRDPARTYID) | Spécifique à Target | S.O. | Si vous fournissez à Target votre logiciel de gestion de la relation client ou d’autres informations d’identification uniques pour vos clients. |

>[!NOTE]
>
>Bien que Target prenne en charge les cookies interdomaines propriétaires et tiers, seuls les cookies propriétaires de Target sont recommandés pour le RGPD et le CCPA.

### Comment  Target traite-t-il la gestion des consentements ?

Le RGPD et le CCPA ne changent pas lorsque vous devez obtenir un consentement, mais c’est le cas quand il est question de la façon de l’obtenir. La stratégie de consentement de chaque client dépend de sa collecte de données et de ses pratiques d’utilisation, ainsi que de sa politique de confidentialité. La gestion du consentement n’est pas prise en charge par et ne doit pas être réalisée via Target pour le RGPD et le CCPA.

Adobe n’offre pas actuellement de solution de Gestion des consentements, mais divers outils sont en cours d’élaboration sur le marché pour répondre à certaines des nouvelles exigences. Pour de plus amples renseignements sur les outils de confidentialité en général, y compris les gestionnaires de consentement, consultez le [2017 Privacy Tech Vendor Report](https://iapp.org/media/pdf/resource_center/Tech-Vendor-Directory-1.4.1-electronic.pdf) (rapport sur les fournisseurs offrant des technologies de confidentialité) sur le site web de l’*Association internationale des professionnels de la protection de la vie privée (IAPP)*.

Target fournit la prise en charge de la fonctionnalité d’opt-in via Adobe Experience Platform pour prendre en charge votre stratégie de gestion des consentements. La fonctionnalité d’opt-in permet aux clients de décider comment et à quel moment la balise Target est déclenchée. Il existe également une option via Adobe Experience Platform permettant d’approuver à l’avance la balise Target. Il est recommandé d’utiliser Adobe Experience Platform pour gérer les souscriptions (opt-in). Il existe un contrôle granulaire plus poussé dans Adobe Experience Platform afin de masquer, avant le déclenchement de Target, certains éléments de votre page pouvant s’avérer utiles dans le cadre de votre stratégie de consentement.

Pour plus d’informations sur le RGPD, le CCPA et Adobe Experience Platform, voir [Bibliothèque JavaScript Adobe Privacy et RGPD](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=fr?). Consultez également la section *Fonctionnalité de souscription (opt-in) Adobe Target et Adobe Experience Platform* ci-dessus.

### `AdobePrivacy.js` envoie-t-il des informations à l’API conforme au RGPD ?

AdobePrivacy.js n’envoie *pas* ces informations à l’API. C’est au client de les soumettre. La bibliothèque ne fournit que les ID stockés dans le navigateur pour ce visiteur spécifique.

### Que supprime `removeIdentities` ?

`removeIdentities` *supprime uniquement* ces identités du navigateur, et cela ne dépend que de leur mise en œuvre ou non par la solution Adobe.

Par exemple, Target supprime les cookies qui stockent ses ID, mais Adobe Audience Manager (AAM) ne supprime pas l’ID demdex stocké dans un cookie tiers.

### Quelles informations doivent être incluses dans une requête RGPD ou CCPA Target ?

Outre les exigences du Privacy Service central, un message RGPD ou CCPA valide pour Target contient :

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
| Traitement | Traitement | Target a reçu la requête RGPD ou CCPA et la traite. |
| Complete | Non applicable - contexte d’entreprise non applicable | L’ID IMS dans la requête RGPD ou CCPA n’est associé à aucun client Target.<br />Certaines entreprises disposent de plusieurs ID IMS. Envoyez l’identifiant IMS dans lequel Target est configuré. |
| Complete | Non applicable - contexte utilisateur introuvable | L’ID fourni dans la requête RGPD ou CCPA pour le visiteur ou le titulaire de données spécifique ne figure pas dans le magasin de profils Target.<br />Ce résultat est également renvoyé si vous tentez d’envoyer un type d’ID d’espace de noms non pris en charge par Target (voir ci-dessus les ID pris en charge). |
| Erreur | Message d’erreur (les détails dépendent du type d’erreur) | Erreur lors de la récupération ou de la suppression du profil du sujet de données demandé.<br />Erreur lors du chargement vers Azure pour la demande d’accès. |

### Quelle réponse Target envoie-t-il à l’API conforme au RGPD pour une demande d’accès ?

Les réponses aux demandes d’accès aux données contiennent un résumé du profil Target pour le visiteur en question. Ce retour est envoyé à l’API Experience Cloud relative au RGPD, qui à son tour envoie une réponse aux responsables du traitement des données.

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
| jobId | Indique l’ID de tâche RGPD ou CCPA à partir de l’API centrale relative au RGPD. |
| imsOrgID | Fournit un identifiant unique pour votre entreprise. |
| espace de noms | Également appelé source de données. Voir « Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ? » dans cette rubrique. |
| type | Le type d’ID pour lequel vous avez demandé l’accès aux données en vertu du RGPD ou du CCPA. Target accepte plusieurs types d’ID, dont certains sont standard et d’autres spécifiques à Target. Voir « Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ? » dans cette rubrique. |
| value | L’ID de l’espace de noms/la source de données. Voir « Quels ID sont pris en charge pour aider les clients à remplir une demande d’accès et de suppression en vertu du RGPD ou du CCPA pour Target ? » pour les valeurs acceptées. |
| integration code | Les codes d’intégration sont des noms conviviaux pour vos sources de données et vous aident à suivre vos sources de données plus facilement qu’en utilisant des ID de sources de données. |

Lorsque plusieurs valeurs sont fournies pour identifier des profils, chaque identifiant valide dispose d’un fichier de profil. Un ou plusieurs fichiers de profil sont envoyés au Azure Blob RGPD via l’API centrale RGPD, au format de la réponse JSON du profil Target.

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
| user.ReturnTimeOfDay | Ce champ standard inclut l’heure de la dernière visite récurrente d’un utilisateur. |
| firstSessionStart | Ce champ standard inclut l’heure de début de la première session de l’utilisateur. |
| user.sessionCountScript | De nombreuses informations du profil Target sont chargées ou directement fournies par le contrôleur des données. Dans cet exemple, un script de profil augmente le nombre de sessions que ce visiteur a effectuées sur le site du contrôleur de données. Pour plus d’informations, voir [Attributs de script de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html). |

>[!NOTE]
>
>Cet exemple de code est une version abrégée d’un profil Target au format JSON pour illustration. De nombreux champs du profil Target ne sont pas standard. Les données retournées dépendent des informations figurant dans ce profil de visiteur spécifique.

### Target prend-il en charge l’obscurcissement des adresses IP ?

Target prend en charge l’obscurcissement des adresses IP si vous choisissez de l’utiliser dans le cadre de votre stratégie de mise en oeuvre du RGPD ou du CCPA. Pour plus d’informations, consultez la page [Confidentialité](privacy.md/#replacement-of-last-octet-of-ip-addresses).

### Dois-je faire quelque chose pour empêcher que mes données ne soient partagées ou vendues à des tiers ?

Target ne permet pas aux clients de partager ou de vendre des données directement de Target à des tiers. Il n’y a donc pas d’exclusion de la vente pour Target.
