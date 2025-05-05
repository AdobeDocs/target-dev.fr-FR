---
keywords: stratégie de sécurité du contenu, csp, at.js, liste blanche, liste autorisée, scintillement, pré-masquage, prémasquage, masquage, stratégie de sécurité du contenu, iFrame, iframe
description: Découvrez les directives CSP (Content Security Policy) que vous devez ajouter lors de l’utilisation de  [!DNL Adobe Target].
title: Comment  [!DNL Target]  gère-t-il les politiques de sécurité du contenu (CSP) ?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 28%

---

# Directives relatives aux politiques de sécurité du contenu (CSP)

Si vous utilisez la [stratégie de sécurité du contenu](https://fr.wikipedia.org/wiki/Content_Security_Policy) (CSP) pour votre implémentation [!DNL Adobe Target], vous devez ajouter les directives CSP suivantes lors de l’utilisation de [at.js 2.1 ou version ultérieure](../../implement/client-side/atjs/target-atjs-versions.md) :

* `connect-src` avec `*.tt.omtrdc.net` placé sur la liste autorisée. Nécessaire pour autoriser la requête réseau à [!DNL Target] edge.
* `style-src unsafe-inline`. Obligatoire pour le prémasquage et le contrôle du scintillement.
* `script-src unsafe-inline`. Obligatoire pour autoriser l’exécution de JavaScript qui peut faire partie d’une offre HTML.

## Questions fréquentes

Consultez les questions fréquentes suivantes au sujet des politiques de sécurité :

### Les politiques CORS (Cross Origin Resource Sharing) et les politiques Flash Cross-domain présentent-elles des problèmes de sécurité ?

La méthode recommandée pour mettre en œuvre la politique CORS consiste à autoriser l’accès aux seules origines approuvées qui le nécessitent via une liste autorisée de domaines approuvés. Il en va de même pour la politique Flash Cross-domain. Certains clients [!DNL Target] s’inquiètent de l’utilisation de caractères génériques pour les domaines dans Target. Le problème est que si un utilisateur est connecté à une application et qu’il visite un domaine autorisé par la stratégie, tout contenu malveillant s’exécutant sur ce domaine peut potentiellement récupérer du contenu sensible de l’application et effectuer des actions dans le contexte de sécurité de l’utilisateur connecté. Cette situation est généralement appelée Cross-Site Request Forgery (CSRF).

Toutefois, dans une implémentation de [!DNL Target], ces stratégies ne doivent pas représenter un problème de sécurité.

« adobe.tt.omtrdc.net » est un domaine détenu par Adobe. [!DNL Adobe Target] est un outil de test et de personnalisation. Il est prévu que [!DNL Target] puisse recevoir et traiter des requêtes provenant de n’importe où sans nécessiter d’authentification. Ces requêtes contiennent des paires clé/valeur utilisées pour les tests A/B, les recommandations ou la personnalisation du contenu.

Adobe ne stocke pas d’informations d’identification personnelle ni d’autres informations sensibles sur les serveurs Edge [!DNL Adobe Target], vers lesquels pointe &quot;adobe.tt.omtrdc.net&quot;.

Il est prévu que [!DNL Target] soit accessible depuis n’importe quel domaine via des appels JavaScript. La seule façon d’autoriser cet accès consiste à appliquer &quot;Access-Control-Allow-Origin&quot; avec un caractère générique.

### Comment puis-je autoriser ou empêcher mon site d’être incorporé en tant qu’iFrame sous des domaines étrangers ?

Pour permettre au [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr){target=_blank} (VEC) d’incorporer votre site web dans un iFrame, la CSP (si elle est définie) doit être modifiée dans le paramètre de votre serveur web. Les domaines [!DNL Adobe] doivent être mis en liste blanche et configurés.

Pour des raisons de sécurité, vous pouvez empêcher votre site d’être incorporé en tant qu’iFrame sous des domaines étrangers.

Les sections suivantes expliquent comment autoriser ou empêcher le compositeur d’expérience visuelle d’incorporer votre site dans un iFrame.

#### Autorisation du VEC à incorporer votre site dans un iFrame

La solution la plus simple pour permettre au VEC d’incorporer votre site web dans un iFrame est d’autoriser `*.adobe.com`, qui est le caractère générique le plus large.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Comme dans l’illustration suivante (cliquez pour agrandir) :


![CSP avec le caractère générique le plus large](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Vous pouvez uniquement autoriser le service [!DNL Adobe] réel. Ce scénario peut être réalisé en utilisant `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Comme dans l’illustration suivante (cliquez pour agrandir) :

![CSP avec application de portée Experience Cloud](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

L’accès le plus restrictif au compte d’une entreprise peut être obtenu en utilisant `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`, où `<Client Code>` représente votre code client spécifique.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Comme dans l’illustration suivante (cliquez pour agrandir) :

![CSP avec clientcode scoped](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Si [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) est implémenté, il doit également être déverrouillé.
>
>Par exemple :
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Empêcher le VEC d’incorporer votre site dans un iFrame

Pour empêcher le compositeur d’expérience visuelle d’incorporer votre site dans un iFrame, vous pouvez restreindre à &quot;vous&quot; uniquement.

Par exemple :

`Content-Security-Policy: frame-ancestors 'self'`

Comme illustré ci-dessous (cliquez pour agrandir) :

![Erreur CSP](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

Le message d&#39;erreur suivant s&#39;affiche :

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

