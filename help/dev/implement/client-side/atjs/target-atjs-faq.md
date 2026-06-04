---
keywords: at.js faq, questions fréquentes sur at.js, faq, scintillement, chargeur, chargeur de page, interdomaine, taille de fichier, taille fichier, domaine x, at.js et mbox.js, x uniquement, interdomaine, safari, app à une seule page, sélecteurs manquants, sélecteurs, application à une seule page, tt.omtrdc.net, spa, Adobe Experience Manager, AEM, adresse ip, httponly, HttpOnly, secure, ip, domaine de cookie
description: Consultez les réponses aux questions fréquentes sur la bibliothèque JavaScript at [!DNL Adobe Target] js .
title: Quelles sont les questions et réponses fréquentes concernant at.js ?
feature: at.js
exl-id: 362ccc5b-8731-46c0-bc52-3e55c273e216
TQID: https://experienceleague.adobe.com/wOC67fpxKtZKP3-o-T86oA-HqySuPGebT9W5LUHuxSA
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
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 2994
ht-degree: 64%

---

# Forum aux questions sur at.js

Réponses aux questions fréquentes sur la bibliothèque JavaScript at.js [!DNL Adobe Target].

## Quels sont les avantages d’utiliser at.js au lieu de mbox.js ?

La bibliothèque at.js remplace mbox.js. La bibliothèque mbox.js n’est plus prise en charge. Cependant, pour la plupart des gens, at.js offre des avantages par rapport à mbox.js.

Entre autres avantages, at.js réduit les temps de chargement des pages pour les implémentations web, améliore la sécurité et fournit de meilleures options d’implémentation pour les applications d’une seule page.

Le diagramme suivant illustre les performances de chargement de page avec mbox.js et at.js.

(Cliquez sur l’image pour l’agrandir sur toute la largeur.)

![Diagramme de performances de page comparant mbox.js à at.js](/help/dev/implement/client-side/atjs/assets/atjs_versus_mboxjs.png "Diagramme de performances de page comparant mbox.js à at.js"){zoomable="yes"}

Comme illustré ci-dessus, avec mbox.js, le contenu de la page ne commençait à charger qu’une fois l’appel [!DNL Target] terminé. Avec at.js, le contenu de la page commence à charger dès que l’appel de [!DNL Target] est initié, sans attendre qu’il soit terminé.

## Quel est l’impact de at.js et mbox.js sur le temps chargement de la page ?

De nombreux clients et consultants souhaitent connaître l’impact d’at.js et mbox.js sur le temps de chargement des pages, en particulier dans le contexte des utilisateurs et utilisatrices nouveaux ou récurrents. Malheureusement, il est difficile de mesurer et de donner des chiffres concrets sur la manière dont at.js ou mbox.js influencent le temps de chargement des pages en raison de l’implémentation de chaque client.

Cependant, si l’API visiteur est présente sur la page, [!DNL Target] pouvez mieux comprendre comment at.js et mbox.js influencent le temps de chargement des pages.

>[!NOTE]
>
>L’API visiteur et at.js ou mbox.js n’ont un impact sur le temps de chargement des pages que lorsque vous utilisez la mbox globale (en raison de la technique de masquage du corps). Les mboxes régionales ne sont pas impactées par l’intégration de l’API visiteur.

Les sections suivantes décrivent la séquence d’actions pour les nouveaux visiteurs et les visiteurs récurrents :

### Nouveaux visiteurs

1. L’API visiteur est chargée, analysée et exécutée.
1. at.js / mbox.js est chargé, analysé, puis exécuté.
1. Si la fonction de création automatique de mbox globale est activée, la bibliothèque JavaScript de [!DNL Target] :

   * instancie l’objet visiteur ;
   * La bibliothèque [!DNL Target] tente de récupérer les données d’identifiant visiteur Experience Cloud.
   * Comme il s’agit d’un nouveau visiteur, l’API visiteur déclenche une requête inter-domaines sur demdex.net.
   * Une fois les données d’identifiant visiteur Experience Cloud récupérées, une requête à [!DNL Target] est déclenchée.

### Visiteurs récurrents

1. L’API visiteur est chargée, analysée et exécutée.
1. at.js / mbox.js est chargé, analysé, puis exécuté.
1. Si la fonction de création automatique de mbox globale est activée, la bibliothèque JavaScript de [!DNL Target] :

   * instancie l’objet visiteur ;
   * La bibliothèque [!DNL Target] tente de récupérer les données d’identifiant visiteur Experience Cloud.
   * l’API visiteur récupère les données du cookies ;
   * Une fois les données d’identifiant visiteur Experience Cloud récupérées, une requête à [!DNL Target] est déclenchée.

>[!NOTE]
>
>Pour les nouveaux visiteurs, si l’API visiteur est présente, [!DNL Target] devez se connecter plusieurs fois pour s’assurer que les requêtes [!DNL Target] contiennent les données d’identifiant visiteur Experience Cloud. Pour les visiteurs réguliers, [!DNL Target] se connecte uniquement à [!DNL Target] pour récupérer le contenu personnalisé.

## Pourquoi les temps de réponse semblent-ils plus lents après la mise à niveau d’une version précédente d’at.js vers la version 1.0.0 ?

Les versions 1.0.0 et ultérieures d’at.js déclenchent toutes les requêtes en parallèle. Les versions précédentes exécutent les requêtes de manière séquentielle, ce qui signifie que les requêtes sont placées en file d’attente et que [!DNL Target] attend que la première requête se termine avant de passer à la suivante.

La façon dont les versions précédentes d’at.js exécutent les requêtes est sujette au « blocage d’en-tête de ligne ». Dans at.js version 1.0.0 et ultérieure, [!DNL Target] est passé à l’exécution de demandes parallèles.

Si vous consultez la cascade de l’onglet réseau pour at.js 0.9.1, par exemple, vous verrez que la requête [!DNL Target] suivante ne démarre pas tant que la précédente n’est pas terminée. Cette séquence ne fonctionne pas avec at.js version 1.0.0 et ultérieure, où toutes les requêtes démarrent en même temps.

En termes de temps de réponse, mathématiquement, cette séquence peut se résumer comme suit :

<ul class="simplelist"> 
 <li> at.js 0.9.1 : temps de réponse de toutes les requêtes [!DNL Target] = somme des temps de réponse des requêtes </li> 
 <li> at.js 1.0.0 et versions ultérieures : temps de réponse de toutes les requêtes [!DNL Target] = maximum du temps de réponse des requêtes </li> 
</ul>

La bibliothèque at.js version 1.0.0 exécute les requêtes plus rapidement. En outre, les requêtes at.js sont asynchrones, de sorte que [!DNL Target] ne bloque pas le rendu de la page. Même si le traitement des requêtes ne prend que quelques secondes, la page rendue est toujours visible. Toutefois, certaines parties de la page sont masquées, et ce, jusqu’à ce que [!DNL Target] reçoive une réponse du Edge de [!DNL Target].

## Puis-je charger la bibliothèque [!DNL Target] de manière asynchrone ?

La version 1.0.0 d’at.js permet de charger la bibliothèque [!DNL Target] de manière asynchrone.

Pour charger at.js de manière asynchrone, procédez comme suit :

* Il est recommandé d’utiliser les balises dans Adobe Experience Platform.
* Vous pouvez également charger at.js de manière asynchrone en ajoutant l’attribut async à la balise du script qui charge at.js. Utilisez un élément semblable au suivant :

  ```
  <script src="<URL to at.js>" async></script>
  ```

* Vous pouvez également charger at.js de manière asynchrone en utilisant le code suivant :

  ```
  var script = document.createElement('script'); 
  script.async = true; 
  script.src = "<URL to at.js>"; 
  document.head.appendChild(script);
  ```

Le chargement d’at.js de manière asynchrone est un excellent moyen d’éviter de bloquer le rendu du navigateur. Cependant, cette technique peut entraîner un scintillement de la page web.

Vous pouvez éviter le scintillement à l’aide d’un extrait de code de masquage préalable qui masque la page (ou les parties spécifiées), puis la révèle après le chargement d’at.js et de la requête globale. Vous devez ajouter le fragment de code avant le chargement d’at.js.

Si vous déployez at.js par le biais d’une implémentation  asynchrone, veillez à inclure le fragment de code de masquage préalable directement sur vos pages, avant le code intégré Implémenter [!DNL Target] à l’aide de [!UICONTROL Adobe Experience Platform].

Si vous déployez at.js par le biais d’une implémentation synchrone de la gestion dynamique des balises, le fragment de code prémasqué peut être ajouté au moyen d’une règle de chargement de page déclenchée en haut de la page.

Pour plus d’informations, voir [Comment at.js gère le scintillement](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## Est-ce qu’at.js est compatible avec l’intégration [!DNL Adobe Experience Manager] (Experience Manager) ?

[!DNL Adobe Experience Manager] 6.2 avec FP-11577 (ou version ultérieure) prend désormais en charge les implémentations d’at.js avec son intégration [!UICONTROL Adobe Target Cloud Services].

## Comment empêcher le scintillement au chargement des pages avec at.js ?

[!DNL Target] offre plusieurs moyens d’empêcher le scintillement au chargement de la page. Pour plus d’informations, voir [Prévention du scintillement avec at.js](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## Quelle est la taille de fichier d’at.js ?

Le fichier at.js fait environ 109 Ko une fois téléchargé. Cependant, comme la plupart des serveurs compressent automatiquement les fichiers pour les rendre plus légers, at.js ne fait plus que 34 Ko environ une fois compressé (avec GZIP ou une autre méthode) sur votre serveur et chargé lorsque des utilisateurs visitent votre site web. Les paramètres de compression du serveur sur lequel vous avez installé at.js déterminent sa taille réelle après compression.

## Pourquoi le fichier at.js est-il plus volumineux que le fichier mbox.js ?

Les implémentations d’at.js utilisent une seule bibliothèque ( at.js), tandis que celles de mbox.js utilisent deux bibliothèques ( mbox.js et target.js). Il serait donc préférable donc de comparer at.js à mbox.js *et* `target.js`. En comparant les tailles compressées des deux versions, at.js version 1.2 fait 34 Ko et mbox.js version 63 fait 26,2 Ko. «

Le fichier at.js est plus volumineux, car il effectue beaucoup plus d’analyses DOM que le fichier mbox.js, du fait que le fichier at.js doit interpréter les données « brutes » qu’il récupère dans la réponse JSON. mbox.js utilisait `document.write()` et toute l’analyse était effectuée par le navigateur.

Malgré une taille de fichier plus importante, nos tests démontrent que les pages se chargent plus rapidement avec at.js qu’avec mbox.js. En outre, at.js offre une sécurité accrue, car il ne charge pas de fichiers supplémentaires de manière dynamique ni n’utilise `document.write`.

## at.js inclut-il jQuery ? Puis-je supprimer cette partie du fichier at.js si jQuery figure déjà dans mon site web ?

Actuellement, at.js utilise des parties de jQuery ; c’est pourquoi l’avis de licence MIT s’affiche en haut du fichier at.js. jQuery n’est pas exposé et n’interfère pas avec la bibliothèque jQuery déjà présente sur votre page, qui peut être d’une autre version. Il n’est pas possible de supprimer le code jQuery dans at.js.

## at.js prend-il en charge Safari et un interdomaine défini sur x-uniquement ?

Non, si le suivi inter-domaines est défini sur x-uniquement et que les cookies tiers sont désactivés dans Safari, mbox.js et at.js définissent un cookie désactivé et aucune requête de mbox n’est exécutée pour le domaine de ce client spécifique.

Pour prendre en charge les visiteurs Safari, il est préférable d’avoir un X-Domain « désactivé » (définit uniquement un cookie propriétaire) ou « activé » (définit uniquement un cookie propriétaire sur Safari, ainsi que des cookies propriétaires et tiers sur les autres navigateurs).

## Puis-je utiliser le compositeur d’expérience visuelle [!UICONTROL VEC] de Target dans mes applications monopages ?

Oui, vous pouvez utiliser le VEC pour votre SPA si vous utilisez at.js 2.x. Pour plus d’informations, voir [&#x200B; Compositeur d’expérience visuelle monopage (SPA)](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html?lang=fr).

## Puis-je utiliser le débogueur Adobe Experience Cloud avec les implémentations d’at.js ?

Oui. Vous pouvez également utiliser mboxTrace à des fins de débogage ou les outils de développement de votre navigateur pour inspecter les demandes de réseau, en filtrant sur « mbox » pour isoler les appels mbox.

## Puis-je utiliser des caractères spéciaux dans les noms mbox avec at.js ?

Oui, comme avec mbox.js.

## Pourquoi mes mbox ne se déclenchent-elles pas sur mes pages web ?

Les clients de [!DNL Target] utilisent parfois des instances basées sur le cloud avec [!DNL Target] à des fins de test ou de preuve de concept. Ces domaines, et de nombreux autres, font partie de la [liste des suffixes publics](https://publicsuffix.org/list/public_suffix_list.dat).

Les navigateurs modernes n’enregistrent pas les cookies si vous utilisez ces domaines, sauf si vous personnalisez le paramètre `cookieDomain` à l’aide de targetGlobalSettings(). Pour plus d’informations, voir [Utilisation d’instances basées sur Cloud avec [!DNL Target]](/help/dev/implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md).

## Les adresses IP peuvent-elles être utilisées comme domaine de cookie lors de l’utilisation d’at.js ?

Assurez-vous que vous utilisez la [version at.js 1.2 ou ultérieure](/help/dev/implement/client-side/atjs/target-atjs-versions.md). Adobe vous recommande toutefois vivement de rester à jour avec la dernière version.

>[!NOTE]
>
>Remarque : Les exemples suivants ne sont pas nécessaires si vous utilisez la version 1.2 ou ultérieure d’at.js.

Remarque : En fonction de votre utilisation de [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md), vous devrez peut-être apporter des modifications supplémentaires au code après le téléchargement d’at.js. Par exemple, si vous avez besoin de paramètres légèrement différents pour vos mises en œuvre [!DNL Target] sur plusieurs sites web et que vous ne parvenez pas à définir ces paramètres dynamiquement à l’aide d’un code JavaScript personnalisé, effectuez ces personnalisations manuellement après avoir téléchargé le fichier et avant de le transférer vers le site web correspondant.

Les exemples suivants permettent d’utiliser la fonction `targetGlobalSettings()` d’at.js pour insérer un fragment de code permettant de prendre en charge les adresses IP.

Cet exemple concerne une adresse IP unique :

```
if (window.location.hostname === '123.456.78.9') { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

Cet exemple concerne une plage d’adresses IP :

```
if (/^123\.456\.78\..*/g.test(window.location.hostname)) { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

## Pourquoi des messages d’avertissement du type « Actions avec sélecteurs manquants » s’affichent-ils ?

Ces messages ne sont pas liés à la fonctionnalité at.js. La bibliothèque at.js tente de signaler tout ce qui est introuvable dans le DOM.

L’affichage de ce message d’avertissement peut s’expliquer par les causes suivantes :

* La page est créée dynamiquement et at.js ne parvient pas à trouver l’élément.
* La page est créée lentement (en raison de la lenteur du réseau) et at.js ne parvient pas à trouver le sélecteur dans le DOM.
* La structure de la page sur laquelle s’exécute l’activité a été modifiée. Si vous rouvrez l’activité dans le compositeur d’expérience visuelle (VEC), un message d’avertissement s’affiche. Mettez à jour l’activité afin que tous les éléments nécessaires soient détectés.
* La page sous-jacente fait partie d’une application monopage (SPA) ou la page contient des éléments qui apparaissent plus bas dans la page et le « mécanisme d’interrogation des sélecteurs » d’at.js ne parvient pas à trouver ces éléments. Augmenter le `selectorsPollingTimeout` peut aider. Pour plus d’informations, voir [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* Les mesures de suivi des clics tentent de s’ajouter à chaque page, indépendamment de l’URL à laquelle elles ont été configurées. Bien que sans danger, cette situation entraîne l’affichage répété de ces messages.

  Pour de meilleurs résultats, téléchargez et utilisez la [dernière version d’at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md). Pour plus d’informations sur le téléchargement d’at.js, reportez-vous à la section  [!DNL Target]  Télécharger at.js à l’aide de l’interface[&#128279;](how-to-deployatjs/implement-target-without-a-tag-manager.md#download-atjs-using-the-target-interface) de l’article [*Comment déployer at.js* > *Implémenter [!DNL Target] sans gestionnaire de balises*](how-to-deployatjs/implement-target-without-a-tag-manager.md).

## À quoi correspond le domaine tt.omtrdc.net auquel les appels au serveur de [!DNL Target] sont adressés ?

tt.omtrdc.net est le nom de domaine du réseau Adobe EDGE utilisé pour recevoir tous les appels au serveur pour [!DNL Target].

## Pourquoi at.js n’utilise-t-il pas toujours les indicateurs de cookie HttpOnly et Secure ?

HttpOnly ne peut être défini que via un code côté serveur. [!DNL Target]Les cookies, tels que mbox, étant créés et enregistrés via le code JavaScript, ne peut pas utiliser l’indicateur de [!DNL Target] cookie HttpOnly. [!DNL Target] utilise la définition HttpOnly pour les cookies tiers définis du côté serveur lorsque le suivi inter-domaines est activé.

Secure ne peut être défini que via JavaScript lorsque la page a été chargée via HTTPS. Si la page se charge initialement via HTTP, JavaScript ne peut pas définir cet indicateur. En outre, si l’indicateur Secure est utilisé, le cookie est disponible uniquement sur les pages HTTPS. Pour les pages chargées via HTTPS, [!DNL Target] définit les attributs Secure et SameSite=None.

Pour garantir le suivi correct des utilisateurs par [!DNL Target] et parce que les cookies sont générés côté client, [!DNL Target] n’utilise aucun de ces indicateurs, sauf dans les situations mentionnées ci-dessus.

## Comment at.js gère-t-il les problèmes de sécurité tels que les attaques XSS et MITM ?

La communication avec le réseau Edge d’Adobe, activé par at.js, se produit uniquement via HTTPS tant que l’option `secureOnly` est définie sur true dans la fonction targetGlobalSettings() ([targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)), sinon at.js est autorisé à basculer entre HTTP et HTTPS en fonction du protocole de la page.

Les en-têtes suivants sont appliqués par défaut :
* HTTP Strict Transport Security (HSTS)
* Protection X-XSS
* X Options de type de contenu
* Politique-Référent

Tous les en-têtes déjà utilisés dans les pages clientes peuvent être appliqués. Une façon courante de le faire est d’utiliser « l’autorisation d’en-tête de requête HTTP ». L’assistance clientèle d’Adobe peut vous conseiller sur les bonnes méthodes et pratiques.

De plus, les requêtes envoyées à Adobe Edge Network sont publiques (dans la mesure où elles sont conçues pour être effectuées à partir des navigateurs des visiteurs) et ne contiennent pas de détails de visiteur visibles (elles contiennent uniquement un identifiant visiteur). Ces requêtes fournissent des expériences aux visiteurs et visiteuses et contiennent des détails sur ce qu’un visiteur ou une visiteuse doit voir sur la page.

Notez que pour les jetons de réponse et les ID de session transmis dans ces requêtes :

* Ils effectuent le suivi des sessions de communication
* Ils sont composés de caractères aléatoires
* Les ID de session sont valides pendant 30 minutes
* Les jetons de réponse peuvent être désactivés ([jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr)).
* Elles ne sont utiles que dans l’environnement des solutions Adobe.

Il est prévu que l’en-tête `Access-Control-Allow-Origin` avec la valeur « * » s’affiche dans les requêtes at.js, car elles sont publiques, l’authentification n’est pas requise et le réseau Edge d’Adobe doit être accessible à partir de n’importe quel domaine via des appels JavaScript.

Cependant, la politique de sécurité du contenu (CSP) doit être appliquée à la page. Pour plus d’informations sur les exigences de la CSP pour at.js, consultez [Politique de sécurité du contenu](/help/dev/before-implement/privacy/content-security-policy.md) et [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## À quelle fréquence la bibliothèque at.js déclenche-t-elle une demande de réseau ?

Toutes les prises de décision de [!DNL Target] se font côté serveur. Cela signifie que at.js déclenche une demande de réseau à chaque rechargement de page, ou qu’une API publique de at.js est appelée.

## Dans le meilleur des cas, peut-on espérer que l’utilisateur ne subisse pas d’effets visibles liés au masquage, au remplacement et à l’affichage de contenu lors du chargement d’une page ?

at.js tente d’éviter le masquage préalable de l’ensemble HTML BODY ou autres éléments DOM pendant une période prolongée, mais cela dépend des conditions du réseau et de la configuration des activités. at.js fournit [des paramètres](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) pouvant être utilisés pour personnaliser BODY en masquant le style CSS. Par exemple, au lieu de masquer entièrement l’ensemble HTML BODY, vous pouvez pré-masquer certaines parties de la page. On s’attend à ce que ces parties contiennent des éléments DOM à « personnaliser ».

## Quelle est le déroulement des événements dans une situation type, dans laquelle un utilisateur est admissible pour une activité ?

La requête at.js est une requête `XMLHttpRequest` asynchrone. Les étapes exécutées sont donc les suivantes :

1. La page charge.
1. at.js pré-masque l’ensemble HTML BODY. Il existe un paramètre qui permet de pré-masquer un conteneur plutôt que l’ensemble HTML BODY.
1. La bibliothèque at.js déclenche une demande.
1. Une fois la réponse de [!DNL Target] reçue, [!DNL Target] extrait les sélecteurs CSS.
1. Grâce aux sélecteurs CSS, [!DNL Target] crée des balises de style pour pré-masquer les éléments DOM qui seront personnalisés.
1. Le style de pré-masquage de l’ensemble HTML BODY est supprimé.
1. [!DNL Target] lance l’interrogation pour les éléments DOM.
1. Si un élément DOM est trouvé, [!DNL Target] apporte des modifications au modèle DOM et le STYLE de pré-masquage de l’élément est supprimé.
1. Si Target ne trouve pas d’élément DOM, un délai d’expiration global supprime le masquage des éléments afin d’éviter de faire face à une page endommagée.

## À quelle fréquence le contenu des pages est-il complétement chargé et visible lorsqu’at.js finit par supprimer le masquage de l’élément modifié par l’activité ?

Dans le cas ci-dessus, à quelle fréquence le contenu des pages est-il complétement chargé et visible lorsqu’at.js finit par supprimer le masquage de l’élément modifié par l’activité ? Autrement dit, la page est entièrement visible, excepté le contenu de l’activité, qui apparaît légèrement après le reste du contenu.

at.js ne bloque pas le rendu de la page. L’utilisateur peut apercevoir certaines zones vides dans la page, représentant les éléments personnalisés par [!DNL Target]. Si le contenu qui doit être appliqué contient peu d’actifs distants, tels que des scripts et des images, tout devrait être rendu rapidement.

## Quel serait l’impact d’une page entièrement en cache dans le cas ci-dessus ? Le contenu de l’activité aurait-il plus de chance d’être visible une fois le reste du contenu de la page chargé ?

Si une page est mise en cache sur un réseau CDN proche de l’emplacement géographique de l’utilisateur, mais loin du serveur Edge de [!DNL Target], le délai risque d’être un peu plus long. Les serveurs Edge de [!DNL Target] sont bien répartis autour du globe, ce n’est donc pas un problème la plupart du temps.

## Est-il possible que la bannière principale s’affiche, puis change après un court instant ?

Dans le cas suivant :

Le délai d’expiration de [!DNL Target] est de cinq secondes. Un utilisateur charge une page qui a une activité afin de personnaliser une image principale. at.js envoie une requête pour déterminer s’il faut appliquer une activité, mais dans un premier temps, ne reçoit pas de réponse. On considère que l’utilisateur consulte le contenu de l’image principale, car [!DNL Target] n’a pas envoyé de réponse pour savoir si oui ou non une activité y est associée. Au bout de quatre secondes, [!DNL Target] envoie une réponse avec le contenu de l’activité.

À ce stade, est-il possible d’afficher la version alternative ? Donc, après les quatre secondes, l’image principale a pu changer et l’utilisateur a pu remarquer ce changement ?

Initialement, l’élément DOM de l’image principale est masqué. Une fois la réponse de [!DNL Target] reçue, at.js apporte les modifications aux éléments DOM, comme le changement d’image, et affiche l’image principale personnalisée.

## Quel doctype HTML at.js requiert-il ?

at.js requiert le doctype HTML 5.

Cette syntaxe est la suivante :

`<!DOCTYPE html>`

Le doctype HTML 5 garantit le chargement de la page en mode standard. Lors du chargement en mode quirks, certaines API JS dont le fichier at.js dépend sont désactivées. [!DNL Target] désactive at.js en mode quirks.

## at.js fonctionne-t-il dans un environnement d’application ionique ?

Cette implémentation n’a jamais été testée, car at.js n’était pas destiné à fonctionner dans un environnement non web. [!DNL Adobe] recommande ses [&#x200B; SDK pour les implémentations mobiles](/help/dev/implement/mobile/overview.md).
