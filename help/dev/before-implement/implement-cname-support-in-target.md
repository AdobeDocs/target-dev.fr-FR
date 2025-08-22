---
keywords: assistance clientèle, cname, programme de certificat, nom canonique, cookies, certificat, amc, certificat géré par adobe, digicert, validation du contrôle de domaine, dcv, assistance clientèle2
description: Travaillez avec [!UICONTROL Adobe Client Care] pour implémenter la prise en charge de CNAME (nom canonique) dans  [!DNL Adobe Target]  pour gérer les problèmes de blocage des publicités.
title: Comment utiliser CNAME dans Target ?
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: 04dfc34bcd3e7efbf73cd167334b440d42cafd1b
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---

# CNAME et Target

Instructions relatives à l’utilisation de [!DNL Adobe Client Care] pour implémenter la prise en charge de CNAME (nom canonique) dans [!DNL Adobe Target]. Utilisez CNAME pour gérer les problèmes de blocage des publicités ou les politiques de cookies liées à ITP (Intelligent Tracking Prevention). Avec CNAME, les appels sont effectués vers un domaine détenu par le client plutôt que vers un domaine détenu par Adobe.

## Demande de prise en charge CNAME dans Target

1. Déterminez la liste des noms d’hôtes dont vous avez besoin pour votre certificat SSL (voir la FAQ ci-dessous).

1. Pour chaque nom d’hôte, créez un enregistrement CNAME dans votre DNS pointant vers votre [!DNL Target] de nom d’hôte `clientcode.tt.omtrdc.net` standard.

   Par exemple, si votre code client est « cnamecustomer » et que votre nom d’hôte proposé est `target.example.com`, votre enregistrement CNAME DNS ressemble à ce qui suit :

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >L’autorité de certification d’Adobe, DigiCert, ne peut pas émettre de certificat tant que cette étape n’est pas terminée. Par conséquent, Adobe ne peut pas répondre à votre demande d’implémentation CNAME tant que cette étape n’est pas terminée.

1. [Remplissez ce formulaire](assets/FPC_Request_Form.xlsx) puis incluez-le lorsque vous [ouvrez un ticket d’assistance clientèle Adobe demandant une prise en charge CNAME](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C) :

   * Code client [!DNL Adobe Target] :
   * Noms d&#39;hôtes de certificat SSL (exemple : `target.example.com target.example.org`) :
   * Acheteur du certificat SSL (Adobe est vivement recommandé, voir la FAQ) : Adobe/client
   * Si le client achète le certificat, également appelé « Apportez votre propre certificat » (BYOC), renseignez les informations supplémentaires suivantes :
      * Organisme de certification (exemple : Société Inc) :
      * Entité organisationnelle du certificat (facultatif, exemple : Marketing) :
      * Pays du certificat (exemple : États-Unis) :
      * État/région du certificat (exemple : Californie) :
      * Ville du certificat (exemple : San José) :

1. Si Adobe achète le certificat, Adobe travaille avec DigiCert pour acheter et déployer votre certificat sur les serveurs de production Adobe.

   Si le client achète le certificat (BYOC), l’Assistance clientèle Adobe vous envoie la demande de signature de certificat (CSR). Utilisez la CSR lors de l’achat du certificat par l’intermédiaire de l’autorité de certification de votre choix. Une fois le certificat émis, envoyez une copie du certificat et des certificats intermédiaires à l’assistance clientèle d’Adobe pour déploiement.

   L’assistance clientèle Adobe vous avertit lorsque votre implémentation est prête.

1. Mettez à jour la `serverDomain` [documentation](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain) vers le nouveau nom d’hôte CNAME et définissez `overrideMboxEdgeServer` sur `false` [documentation](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver) dans votre configuration at.js.

## Questions fréquentes

Les informations suivantes répondent aux questions fréquentes sur la demande et l’implémentation de la prise en charge CNAME dans Target :

### Puis-je fournir mon propre certificat (Apporter votre propre certificat ou BYOC) ?

Vous pouvez fournir votre propre certificat. Cependant, Adobe ne recommande pas cette pratique. La gestion du cycle de vie du certificat SSL est plus facile pour Adobe et pour vous si Adobe achète et contrôle le certificat. Les certificats SSL doivent être renouvelés chaque année. Par conséquent, l’assistance clientèle Adobe doit vous contacter chaque année pour obtenir un nouveau certificat dans les délais impartis. Certains clients peuvent avoir des difficultés à produire un certificat renouvelé dans les délais impartis. Votre implémentation [!DNL Target] est compromise lorsque le certificat expire, car les navigateurs refusent les connexions.

>[!WARNING]
>
>Si vous demandez une implémentation CNAME [!DNL Target] apportez votre propre certificat, vous êtes responsable de fournir des certificats renouvelés à l’assistance clientèle d’Adobe chaque année. Le fait de laisser votre certificat CNAME expirer avant qu’Adobe puisse déployer un certificat renouvelé entraîne une panne de votre implémentation [!DNL Target] spécifique.

### Combien de temps avant l’expiration de mon nouveau certificat SSL ?

Tous les certificats achetés par Adobe sont valides pendant un an. Pour plus d’informations, consultez l’article de [DigiCert sur les certificats d’un an](https://www.digicert.com/blog/position-on-1-year-certificates).

### Quels noms d’hôtes dois-je choisir ? Combien de noms d’hôtes par domaine dois-je choisir ?

Les implémentations CNAME de Target ne nécessitent qu’un seul nom d’hôte par domaine sur le certificat SSL et dans le DNS du client. Adobe recommande un nom d’hôte par domaine. Certains clients nécessitent plus de noms d’hôtes par domaine pour leurs propres besoins (test lors de l’évaluation, par exemple), ce qui est pris en charge.

La plupart des clients choisissent un nom d’hôte tel que `target.example.com`. Adobe recommande de suivre cette pratique, mais le choix vous appartient en fin de compte. Ne demandez pas un nom d’hôte d’un enregistrement DNS existant. Cela entraîne un conflit et retarde la résolution de votre requête CNAME [!DNL Target].

### J’ai déjà une implémentation CNAME pour Adobe Analytics, puis-je utiliser le même certificat ou nom d’hôte ?

Non, [!DNL Target] nécessite un nom d’hôte et un certificat distincts.

### Mon implémentation actuelle d’[!DNL Target] est-elle affectée par ITP 2.x ?

La version 2.3 d’Apple Intelligent Tracking Prevention (ITP) a introduit sa fonctionnalité de limitation du cloaking CNAME, qui permet de détecter les implémentations CNAME [!DNL Target] et de réduire l’expiration du cookie à sept jours. Actuellement, [!DNL Target] ne dispose d’aucune solution pour l’atténuation du cloaking CNAME d’ITP. Pour plus d’informations sur ITP, voir [ITP (Intelligent Tracking Prevention) 2.x](../before-implement/privacy/apple-itp-2x.md) d’Apple.

### À quel type d’interruption de service puis-je m’attendre lorsque mon implémentation CNAME est déployée ?

Le déploiement du certificat n’entraîne aucune interruption de service (y compris les renouvellements de certificat).

Cependant, une fois que vous avez remplacé le nom d’hôte dans votre code d’implémentation [!DNL Target] (`serverDomain` dans at.js) par le nouveau nom d’hôte CNAME (`target.example.com`), les navigateurs web traitent les visiteurs récurrents comme de nouveaux visiteurs. Les données de profil des visiteurs récurrents sont perdues, car le cookie précédent est inaccessible sous l’ancien nom d’hôte (`clientcode.tt.omtrdc.net`). Le cookie précédent est inaccessible en raison des modèles de sécurité du navigateur. Cette interruption ne se produit qu’au moment du basculement initial vers le nouveau CNAME. Les renouvellements de certificat n’ont pas le même effet, car le nom d’hôte ne change pas.

### Quel type de clé et algorithme de signature de certificat est utilisé pour mon implémentation CNAME ?

Tous les certificats sont RSA SHA-256 et les clés sont RSA 2048 bits, par défaut. Les tailles de clé supérieures à 2 048 bits doivent être demandées explicitement via [!UICONTROL Customer Care].

### Comment puis-je vérifier que mon implémentation CNAME est prête pour le trafic ?

Utilisez l’ensemble de commandes suivant (dans le terminal de ligne de commande macOS ou Linux, en utilisant bash et curl >=7.49) :

1. Copiez et collez cette fonction bash dans votre terminal ou collez-la dans votre fichier de script de démarrage bash (généralement `~/.bash_profile` ou `~/.bashrc`) afin qu’elle soit disponible dans toutes les sessions de terminal :

   +++Afficher les détails

   ```
   function adobeTargetCnameValidation {
     local hostname="$1"
   
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="41 42 44 45 46 47 48"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local poolDomain="pool.data.adobedc.net"
     local shards=5
     local shardsFoundCount=0
     local shardsFound=""
     local shardsFoundOutput=""
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2)"
     local curlVersionRequired=7.49
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local cnameExists=""
     local endToEndTestSucceeded=""
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local currShard="${region}-${poolDomain}"
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         shardsFound+=" $currShard"
   
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundCount=$((shardsFoundCount+1))
           shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
         else
           shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
         fi
   
         shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
   
         if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
         fi
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
   
     local dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
       fi
     fi
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
           if [ -n "$cnameExists" ]; then
             echo
           else
             echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
               "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
           fi
           endToEndTestSucceeded=true
         else
           echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
             "unexpected response from $url -- "
           if [ -n "$cnameExists" ]; then
             echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
           else
             echo "the required DNS CNAME record is missing, see above"
           fi
         fi
       else
         echo -n "$failure $hostname FAILED TLS validation for region $region -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
             "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
           echo ""
           echo "$horizontalRule"
           echo "$curlResult" | sed 's/^/    /g'
           echo "$horizontalRule"
           echo ""
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     done
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, see SSL Shopper:"
         echo ""
         echo "    $info  $sslShopperUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       echo ""
     fi
   
     echo
     echo "$horizontalRule"
     echo
   }
   ```

   +++

1. Collez cette commande (en remplaçant `target.example.com` par votre nom d’hôte) :

   ```adobeTargetCnameValidation target.example.com```

   Si l’implémentation est prête, vous voyez une sortie comme ci-dessous. La partie importante est que toutes les lignes d’état de validation affichent `✅` plutôt que `🚫`. Chaque partition CNAME Edge de Target doit afficher `CN=target.example.com`, qui correspond au nom d&#39;hôte principal sur le certificat demandé (les noms d&#39;hôtes SAN supplémentaires sur le certificat ne sont pas imprimés dans cette sortie).

   +++Afficher les détails

   ```
   $ adobeTargetCnameValidation target.example.com
   
   ==========================================================
   
   Adobe Target CNAME implementation validation for hostname target.example.com:
   ✅ target.example.com passes DNS CNAME validation
   ✅ target.example.com passes TLS and HTTP response validation for region IRL1
   ✅ target.example.com passes TLS and HTTP response validation for region IND1
   ✅ target.example.com passes TLS and HTTP response validation for region SIN
   ✅ target.example.com passes TLS and HTTP response validation for region OR
   ✅ target.example.com passes TLS and HTTP response validation for region SYD
   ✅ target.example.com passes TLS and HTTP response validation for region VA
   ✅ target.example.com passes TLS and HTTP response validation for region TYO
   ✅ target.example.com passes shard validation for the following 7 edge shards:
   
   ===== ✅ target.example.com [edge shard: IRL1-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: IND1-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: SIN-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: OR-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: SYD-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: VA-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: TYO-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ==========================================================  
   
   For additional TLS/SSL validation, see SSL Shopper:
   
       🔎  https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com  
   
   To check DNS propagation around the world, see whatsmydns.net:
   
       🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
       🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com 
   ```

+++

>[!NOTE]
>
>Si cette commande de validation échoue lors de la validation DNS, mais que vous avez déjà effectué les modifications DNS nécessaires, vous devrez peut-être attendre que vos mises à jour DNS se propagent complètement. Les enregistrements DNS sont associés à une [durée de vie)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) qui détermine le délai d’expiration du cache pour les réponses DNS de ces enregistrements. Par conséquent, il se peut que vous deviez attendre au moins aussi longtemps que vos TTL. Vous pouvez utiliser la commande `dig target.example.com` ou [la boîte à outils G Suite](https://toolbox.googleapps.com/apps/dig/#CNAME) pour rechercher vos TTL spécifiques. Pour vérifier la propagation DNS dans le monde entier, consultez [whatsmydns.net](https://whatsmydns.net/#CNAME).

### Comment utiliser un lien d’exclusion avec CNAME ?

Si vous utilisez CNAME, le lien d’opt-out doit contenir le paramètre « client=`clientcode` », par exemple :
`https://my.cname.domain/optout?client=clientcode`.

Remplacez `clientcode` par votre code client, puis ajoutez le texte ou l’image à lier à l’[URL d’exclusion](privacy/privacy.md).

## Limites connues

* Le mode assurance qualité n’est pas contigu lorsque vous disposez de CNAME et d’at.js 1.x, car il est basé sur un cookie tiers. La solution consiste à ajouter les paramètres d’aperçu à chaque URL à laquelle vous accédez. Le mode assurance qualité est contigu lorsque vous disposez de CNAME et d’at.js 2.x.
* Lors de l’utilisation de CNAME, il est plus probable que la taille de l’en-tête du cookie pour les appels [!DNL Target] augmente. Adobe recommande de conserver la taille du cookie inférieure à 8 Ko.
