---
keywords: Mise en œuvre, mbox.js sans JavaScript, redirecteur, coûts par clic, recettes par clic
description: Découvrez comment utiliser les redirecteurs dans les implémentations d’e-mail, de la même manière que vous utilisez une mbox dans vos  [!DNL Adobe Target] .
title: Comment puis-je travailler avec un redirecteur ?
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
TQID: https://experienceleague.adobe.com/3SUsZl1y9tk97sWgdB3iB7wrAXNb2LfN3hObJM14caE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 689
ht-degree: 63%

---

# Fonctionnement avec un redirecteur

L’utilisation d’un redirecteur s’apparente à celle d’une mbox dans vos tests.

Les redirecteurs sont créés avec une URL de redirecteur spéciale qui charge une mbox Redirecteur dans votre compte L’utilisation de ce redirecteur s’apparente à celle d’une mbox dans vos tests. Envoyez l’URL du redirecteur à votre réseau publicitaire en tant que lien de destination de l’annonce.

Utilisez le redirecteur pour effectuer les opérations suivantes :

* Assurer le suivi des clics à partir de vos publicités jusqu’à votre site.
* Créer un rapport centralisé unique pour effectuer le suivi des clics sur les publicités affichées sur plusieurs réseaux publicitaires.
* Modifier les destinations des publicités.

  Par exemple, une même bannière pointe vers votre page d’accueil, votre page de catégories et votre page de produits.

* Déterminer quelle page d’entrée entraîne le plus de conversions.

Pour plus d’informations sur la configuration appropriée, voir [Implémentations non basées sur JavaScript](/help/dev/implement/email/overview.md).

## Création d’un redirecteur

Pour pouvoir utiliser un redirecteur, vous devez le créer.

1. Déterminez les variations de destination de l’annonce, y compris la destination par défaut.
1. Créez l’URL de redirecteur.

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * Où `yourclientcode` est le code client de votre société. Le code client de votre entreprise est en minuscules et ne comporte pas de caractères spéciaux.

     Votre code client est disponible en haut de la page **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** de l’interface [!DNL Target].

   * `redirectorlink_456` est le nom de la mbox Redirecteur qui s’affiche dans votre compte pour être utilisée dans des campagnes et des tests.

     Les redirecteurs fonctionnent différemment des autres mbox, mais leur apparence est identique à celle de toute autre mbox de votre compte. Nommez le redirecteur de manière à pouvoir le différencier facilement des mbox de type standard de votre compte.  Pour respecter les bonnes pratiques, commencez le nom de la mbox par redirectorlink.

   * Où `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm` est la destination par défaut.

     Elle doit être en codage URL et il doit s’agir d’une référence absolue. Vous pouvez utiliser la [Référence de codage d’URL d’](https://www.w3schools.com/tags/ref_urlencode.asp) pour coder rapidement vos URL.

   >[!WARNING]
   >
   >Notez qu’avec Redirector, vous pouvez être exposé à un risque de vulnérabilité de redirection ouverte. Pour éviter l’utilisation non autorisée de liens de redirection par des tiers, Adobe recommande d’utiliser des « hôtes autorisés » pour placer sur la liste autorisée les domaines d’URL de redirection par défaut. [!DNL Target] utilise des hôtes pour placer sur la liste autorisée les domaines vers lesquels vous souhaitez autoriser les redirections. Pour plus d’informations, consultez [Création de Listes autorisées qui spécifient les hôtes autorisés à envoyer des appels de mbox à [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=fr#allowlist) dans *Hôtes*.

1. Validez le redirecteur.
   1. *Bonne pratique en matière de sécurité* : assurez-vous que le domaine utilisé dans le redirecteur est bien placé sur la liste autorisée, comme indiqué ci-dessus. Si vous utilisez un domaine qui n’est pas placé sur la liste autorisée, Adobe bloquera tous les appels vers ce domaine afin d’empêcher des acteurs malveillants d’utiliser le redirecteur pour rediriger vers des domaines potentiellement malveillants.
   2. Insérez l’URL du redirecteur dans un navigateur et procédez à l’actualisation.
   3. Connectez-vous à votre compte, actualisez votre liste de mbox et vérifiez que le nouveau redirecteur est répertorié en tant que mbox.
1. Si vous testez différentes destinations pour une même publicité, créez des [offres de redirection](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html?lang=fr) pour chaque version.
1. Créez la campagne.

   Consultez les [Implémentations non basées sur JavaScript](/help/dev/implement/email/overview.md) pour connaître la configuration appropriée permettant d’atteindre vos objectifs.
1. Effectuez une AQ sur la campagne.

   Créez une page factice avec une `<a href>` contenant l’URL de redirection. Exemple :

   ```
   <a href=https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=
   
   redirectorlink_456&mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2F​usualdestination%2Ehtm>
   ```

1. Vérifiez que toutes les expériences, le contenu par défaut et les rapports fonctionnent comme prévu sur tous les types de navigateur et ce, dans tous vos environnements.

   >[!NOTE]
   >
   >Les redirecteurs ne sont pas pris en charge par la méthode Aperçu de l’offre ou Rechercher les mbox. Prévisualisez les expériences directement dans un navigateur. En outre, `mboxDebug` ne fonctionne pas avec les redirecteurs.

1. Envoyez l’URL complète du redirecteur à votre réseau d’affichage publicitaire en tant que destination de l’annonce.

## Utilisez un redirecteur pour transmettre les coûts par clic et les revenus par clic

Informations sur l’utilisation d’un redirecteur pour transmettre des coûts par clic et des recettes par clic.

### Transmission des coûts par clic

Utilisez un redirecteur pour transmettre les coûts par clic.

>[!NOTE]
>
>Il est recommandé de déterminer la valeur de coût à l’aide de la mesure d’engagement **[!UICONTROL Score per visit]**.

Ajoutez `&mboxPageValue=-value` à l’URL. Nous attirons votre attention sur la valeur négative.

Exemple : pour un coût par clic de 0,10 cent :

```
https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=redirectorlink_456
&mboxPageValue=-0.1&mboxDefault=​https://www.yourcompany.com/usualdestination.htm
```

### Transmission des recettes par clic

Utilisez un redirecteur pour transmettre les recettes par clic.

>[!NOTE]
>
>Une bonne pratique consiste à déterminer la valeur du chiffre d’affaires à l’aide de la mesure d’engagement **[!UICONTROL Score per visit]**.

Ajoutez `&mboxPageValue=value` à l’URL.

Exemple : pour un coût par clic de 0,10 cent :

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
