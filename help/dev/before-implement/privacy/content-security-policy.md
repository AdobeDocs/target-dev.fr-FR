---
keywords: politique de sécurité du contenu, csp, at.js, liste blanche,, scintillement, pré-masquage, pré-masquage, prémasquage, politique de sécurité du contenu, iFrame, iframe
description: Découvrez les directives de la politique de sécurité du contenu (CSP) que vous devez ajouter lors de l’utilisation de  [!DNL Adobe Target].
title: Comment  [!DNL Target]  gère-t-il les politiques de sécurité du contenu (CSP) ?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
TQID: https://experienceleague.adobe.com/gGNgYyblw6-D-RiHBtzAtrOOdhVOsIzYQ-HhkhCtyuI
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 28%

---

# Directives relatives aux politiques de sécurité du contenu (CSP)

Si vous utilisez la [&#x200B; politique de sécurité du contenu &#x200B;](https://fr.wikipedia.org/wiki/Content_Security_Policy) (CSP) pour votre mise en œuvre [!DNL Adobe Target], vous devez ajouter les directives CSP suivantes lors de l’utilisation d’[at.js 2.1 ou version ultérieure &#x200B;](../../implement/client-side/atjs/target-atjs-versions.md) :

* `connect-src` avec `*.tt.omtrdc.net` placé sur la liste autorisée. Nécessaire pour autoriser la requête réseau à [!DNL Target] edge.
* `style-src unsafe-inline`. Obligatoire pour le prémasquage et le contrôle du scintillement.
* `script-src unsafe-inline`. Obligatoire pour autoriser l’exécution de JavaScript qui peut faire partie d’une offre HTML.

## Questions fréquentes

Consultez les questions fréquentes suivantes au sujet des politiques de sécurité :

### Les politiques CORS (Cross Origin Resource Sharing) et les politiques Flash Cross-domain présentent-elles des problèmes de sécurité ?

La méthode recommandée pour mettre en œuvre la politique CORS consiste à autoriser l’accès aux seules origines approuvées qui le nécessitent via une liste autorisée de domaines approuvés. Il en va de même pour la politique Flash Cross-domain. Certains clients [!DNL Target] s’inquiètent de l’utilisation de caractères génériques pour les domaines dans Target. Si un utilisateur est connecté à une application et qu’il visite un domaine autorisé par la politique, tout contenu malveillant exécuté sur ce domaine peut potentiellement récupérer du contenu sensible dans l’application et effectuer des actions dans le contexte de sécurité de l’utilisateur connecté. Cette situation est généralement appelée attaque CSRF (Cross-site request forgery).

Dans une implémentation [!DNL Target], cependant, ces politiques ne doivent pas représenter un problème de sécurité.

« adobe.tt.omtrdc.net » est un domaine détenu par Adobe. [!DNL Adobe Target] est un outil de test et de personnalisation. Il est prévu que [!DNL Target] puisse recevoir et traiter des requêtes provenant de n’importe où sans nécessiter d’authentification. Ces requêtes contiennent des paires clé/valeur utilisées pour les tests A/B, les recommandations ou la personnalisation du contenu.

Adobe ne stocke pas les informations d’identification personnelle (PII) ni d’autres informations sensibles sur les serveurs Edge de [!DNL Adobe Target], vers lesquels pointe « adobe.tt.omtrdc.net ».

Il est prévu que [!DNL Target] soit accessible depuis n’importe quel domaine via des appels JavaScript. La seule façon d’autoriser cet accès consiste à appliquer « Access-Control-Allow-Origin » avec un caractère générique.

### Comment puis-je autoriser ou empêcher l’incorporation de mon site en tant qu’iFrame sous des domaines étrangers ?

Pour permettre au [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr){target=_blank} (VEC) d’incorporer votre site web dans un iFrame, la CSP (si elle est définie) doit être modifiée dans les paramètres de votre serveur web. Les domaines [!DNL Adobe] doivent être whitelistés et configurés.

Pour des raisons de sécurité, vous souhaiterez peut-être empêcher l’incorporation de votre site en tant qu’iFrame sous des domaines étrangers.

Les sections suivantes expliquent comment autoriser ou empêcher le VEC d’incorporer votre site dans un iFrame.

#### Autoriser le compositeur d’expérience visuelle à incorporer votre site dans un iFrame

La solution la plus simple pour permettre au compositeur d’expérience visuelle d’incorporer votre site web dans un iFrame consiste à autoriser `*.adobe.com`, qui est le caractère générique le plus large.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Comme dans l’illustration suivante (cliquez pour agrandir) :


![CSP avec le caractère générique le plus large](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Vous souhaiterez peut-être autoriser uniquement le service [!DNL Adobe] réel. Ce scénario peut être réalisé à l’aide de `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Comme dans l’illustration suivante (cliquez pour agrandir) :

![CSP avec étendue ExperienceCloud](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

L’accès le plus restrictif au compte d’une entreprise peut être obtenu en utilisant `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`, où `<Client Code>` représente votre code client spécifique.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Comme dans l’illustration suivante (cliquez pour agrandir) :

![CSP avec code client défini](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Si vous avez implémenté [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md), il doit également être déverrouillé.
>
>Par exemple :
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Empêcher le compositeur d’expérience visuelle d’incorporer votre site dans un iFrame

Pour empêcher le compositeur d’expérience visuelle d’incorporer votre site dans un iFrame, vous pouvez vous limiter à « self » uniquement.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self'`

Comme illustré ci-dessous (cliquez pour agrandir) :

![Erreur CSP](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

Le message d’erreur suivant s’affiche :

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

