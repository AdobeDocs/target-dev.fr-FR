---
keywords: assistance clientèle;cname;programme de certificat;nom canonique;cookies;certificat;amc;certificat géré par adobe;digicert;validation de contrôle de domaine;dcv
description: Collaborez avec l [!DNL Adobe] assistance clientèle pour implémenter la prise en charge de CNAME (nom canonique) dans  [!DNL Adobe Target]  afin de gérer les problèmes de blocage des publicités.
title: Comment utiliser CNAME dans Target ?
feature: Privacy & Security
role: Developer
exl-id: bf533771-6d46-48ba-964c-3ad9ce9f7352
TQID: https://experienceleague.adobe.com/gTS60hypD2WGc2fJh-sUkq2-pkzt2KnM4CzSQ050L40
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1313
ht-degree: 1%

---

# CNAME et [!DNL Target]

Instructions relatives à la collaboration avec l’assistance clientèle [!DNL Adobe] pour implémenter la prise en charge CNAME (nom canonique) dans [!DNL Adobe Target]. Utilisez CNAME pour gérer les problèmes de blocage des publicités ou les politiques de cookies liées à ITP (Intelligent Tracking Prevention). Avec CNAME, les appels sont effectués vers un domaine détenu par le client plutôt que vers un domaine détenu par [!DNL Adobe].

## Demande de prise en charge CNAME dans [!DNL Target]

1. Déterminez la liste des noms d’hôtes dont vous avez besoin pour votre certificat SSL (voir la FAQ ci-dessous).
1. [Remplissez ce formulaire](/help/dev/implement/assets/FPC_Request_Form.xlsx) et incluez-le lorsque vous [ouvrez un ticket d’assistance clientèle demandant une prise en charge  [!DNL Adobe]  CNAME](https://experienceleague.adobe.com/en/docs/target/using/cmp-resources-and-contact-information#reference_ACA3391A00EF467B87930A450050077C) :

   * Code client [!DNL Adobe Target] :
   * Noms d&#39;hôtes de certificat SSL (exemple : `target.example.com target.example.org`) :
   * Acheteur du certificat SSL ([!DNL Adobe] est vivement recommandé, voir la FAQ) : Adobe/client
   * Si le client achète le certificat, également appelé « Apportez votre propre certificat » (BYOC), renseignez les informations supplémentaires suivantes :

      * Organisme de certification (exemple : Société Inc) :
      * Entité organisationnelle du certificat (facultatif, exemple : Marketing) :
      * Pays du certificat (exemple : États-Unis) :
      * État/région du certificat (exemple : Californie) :
      * Ville du certificat (exemple : San José) :

1. Pour chaque demande de nom d’hôte, Adobe crée l’implémentation et vous renvoie un nom d’enregistrement CNAME à créer, qui contient une chaîne aléatoire avec le suffixe `tt.omtrdc.net`

   Par exemple, si vous avez effectué une demande de `target.example.com`, nous vous renverrons un CNAME sous la forme d’un `abcdefgh.tt.omtrdc.net`. Votre enregistrement CNAME DNS doit ressembler à ce qui suit :

   ```
   target.example.com.  IN  CNAME  abcdefgh.tt.omtrdc.net.
   ```

   >[!IMPORTANT]
   >
   >L&#39;autorité de certification de [!DNL Adobe], DigiCert, ne peut pas émettre de certificat tant que cette étape n&#39;est pas terminée. Par conséquent, [!DNL Adobe] ne pouvez pas répondre à votre demande d’implémentation CNAME tant que cette étape n’est pas terminée.

1. Si [!DNL Adobe] achetez le certificat, [!DNL Adobe] travaille avec DigiCert pour acheter et déployer votre certificat sur les serveurs de production de [!DNL Adobe].

   Si le client achète le certificat (BYOC), [!DNL Adobe] service clientèle vous envoie la demande de signature de certificat (CSR). Utilisez la CSR lors de l’achat du certificat par l’intermédiaire de l’autorité de certification de votre choix. Une fois le certificat émis, envoyez une copie du certificat et des certificats intermédiaires à l’assistance clientèle [!DNL Adobe] pour déploiement.

   Le service clientèle [!DNL Adobe] vous avertit lorsque votre implémentation est prête.

1. Mettez à jour le `serverDomain` ([documentation](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverDomain)) sur le nouveau nom d’hôte CNAME et définissez `overrideMboxEdgeServer` sur `false` ([documentation](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver)) dans votre configuration at.js.

## Questions fréquentes

Les informations suivantes répondent aux questions fréquentes sur la demande et l’implémentation de la prise en charge CNAME dans [!DNL Target] :

### Puis-je fournir mon propre certificat (Apporter votre propre certificat ou BYOC) ?

Vous pouvez fournir votre propre certificat. Toutefois, [!DNL Adobe] déconseillons vivement cette pratique. La gestion du cycle de vie du certificat SSL est plus facile pour [!DNL Adobe] et pour vous, si [!DNL Adobe] achète et contrôle le certificat. La durée de vie des certificats SSL sera seulement plus courte (voir la section suivante à propos de la durée de vie des certificats). Par conséquent, [!DNL Adobe] Service à la clientèle doit communiquer avec vous à chaque fois pour obtenir un nouveau certificat en temps opportun. Cela s’avérera problématique lorsque la durée de vie du certificat sera réduite à seulement 47 jours. Votre implémentation [!DNL Target] est compromise lorsque le certificat expire, car les navigateurs refusent les connexions.

>[!IMPORTANT]
>
>Si vous demandez une implémentation CNAME [!DNL Target] apportez votre propre certificat, vous êtes responsable de fournir des certificats renouvelés à l’assistance clientèle [!DNL Adobe] chaque fois qu’ils expirent. Le fait de laisser votre certificat CNAME expirer avant que [!DNL Adobe] puissiez déployer un certificat renouvelé entraîne une panne de votre implémentation [!DNL Target] spécifique.

### Combien de temps avant l’expiration de mon nouveau certificat SSL ?

La durée de vie de tous les certificats sera réduite dans le cadre d’une initiative majeure des autorités de certification. Pour DigiCert, le fournisseur de certificats de [!DNL Adobe], le planning suivant sera appliqué :

Jusqu’au 15 mars 2026, la durée de vie maximale d’un certificat TLS est de 398 jours.
Depuis le 15 mars 2026, la durée de vie maximale d’un certificat TLS est de 200 jours.
Depuis le 15 mars 2027, la durée de vie maximale d’un certificat TLS est de 100 jours.
Depuis le 15 mars 2029, la durée de vie maximale d’un certificat TLS est de 47 jours.
Pour plus d’informations, consultez l’article de [ DigiCert sur la réduction de la durée de vie des certificats](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)

### Quels noms d’hôtes dois-je choisir ? Combien de noms d’hôtes par domaine dois-je choisir ?

[!DNL Target] implémentations CNAME ne nécessitent qu’un seul nom d’hôte par domaine sur le certificat SSL et dans le DNS du client. [!DNL Adobe] recommande un nom d’hôte par domaine. Certains clients nécessitent plus de noms d’hôtes par domaine pour leurs propres besoins (test lors de l’évaluation, par exemple), ce qui est pris en charge.

La plupart des clients choisissent un nom d’hôte tel que `target.example.com`. [!DNL Adobe] recommande de suivre cette pratique, mais le choix vous appartient en fin de compte. Ne demandez pas un nom d’hôte d’un enregistrement DNS existant. Cela entraîne un conflit et retarde la résolution de votre requête CNAME [!DNL Target].

### J’ai déjà une implémentation CNAME pour [!DNL Adobe Analytics], puis-je utiliser le même certificat ou nom d’hôte ?

Non, [!DNL Target] nécessite un nom d’hôte et un certificat distincts.

### Mon implémentation actuelle d’[!DNL Target] est-elle affectée par ITP 2.x ?

La version 2.3 d’Apple Intelligent Tracking Prevention (ITP) a introduit sa fonctionnalité de limitation du cloaking CNAME, qui permet de détecter les implémentations CNAME [!DNL Adobe Target] et de réduire l’expiration du cookie à sept jours. Actuellement, [!DNL Target] ne dispose d’aucune solution pour l’atténuation du cloaking CNAME d’ITP. Pour plus d’informations sur ITP, voir [ITP (Intelligent Tracking Prevention) 2.x](/help/dev/before-implement/privacy/apple-itp-2x.md) d’Apple.

### À quel type d’interruption de service puis-je m’attendre lorsque mon implémentation CNAME est déployée ?

Le déploiement du certificat n’entraîne aucune interruption de service (y compris les renouvellements de certificat).

Cependant, une fois que vous avez remplacé le nom d’hôte dans votre code d’implémentation [!DNL Target] (`serverDomain` dans at.js) par le nouveau nom d’hôte CNAME (`target.example.com`), les navigateurs web traitent les visiteurs récurrents comme de nouveaux visiteurs. Les données de profil des visiteurs récurrents sont perdues, car le cookie précédent est inaccessible sous l’ancien nom d’hôte (`clientcode.tt.omtrdc.net`). Le cookie précédent est inaccessible en raison des modèles de sécurité du navigateur. Cette interruption ne se produit qu’au moment du basculement initial vers le nouveau CNAME. Les renouvellements de certificat n’ont pas le même effet, car le nom d’hôte ne change pas.

### Quel type de clé et algorithme de signature de certificat est utilisé pour mon implémentation CNAME ?

Tous les certificats sont RSA SHA-256 et les clés sont RSA 2048 bits, par défaut. Les tailles de clé supérieures à 2 048 bits doivent être demandées explicitement via l’assistance clientèle.

### Comment puis-je vérifier que mon implémentation CNAME est prête pour le trafic ?

Utilisez l’ensemble de commandes suivant (dans le terminal de ligne de commande macOS ou Linux, en utilisant bash et curl >=7.49) :

1. Copiez et collez cette fonction bash dans votre terminal ou collez-la dans votre fichier de script de démarrage bash (généralement `~/.bash_profile` ou `~/.bashrc`) afin qu’elle soit disponible dans toutes les sessions de terminal :

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

1. Collez cette commande (en remplaçant `target.example.com` par votre nom d’hôte) :

   ```
   adobeTargetCnameValidation target.example.com
   ```

   Si l’implémentation est prête, vous voyez une sortie comme ci-dessous. La partie importante est que toutes les lignes d’état de validation affichent `✅` plutôt que `🚫`. Chaque partition CNAME Edge de [!DNL Target] doit afficher `CN=target.example.com`, qui correspond au nom d’hôte principal sur le certificat demandé (les noms d’hôte SAN supplémentaires sur le certificat ne sont pas imprimés dans cette sortie).

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

>[!NOTE]
>
>Si cette commande de validation échoue lors de la validation DNS, mais que vous avez déjà effectué les modifications DNS nécessaires, vous devrez peut-être attendre que vos mises à jour DNS se propagent complètement. Les enregistrements DNS sont associés à une [durée de vie)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) qui détermine le délai d’expiration du cache pour les réponses DNS de ces enregistrements. Par conséquent, il se peut que vous deviez attendre au moins aussi longtemps que vos TTL. Vous pouvez utiliser la commande `dig target.example.com` ou [la boîte à outils G Suite](https://toolbox.googleapps.com/apps/dig/#CNAME) pour rechercher vos TTL spécifiques. Pour vérifier la propagation DNS dans le monde entier, consultez [whatsmydns.net](https://whatsmydns.net/#CNAME).

### Comment utiliser un lien d’exclusion avec CNAME ?

Si vous utilisez CNAME, le lien d’opt-out doit contenir le paramètre « client=`clientcode` », par exemple :
`https://my.cname.domain/optout?client=clientcode`.

Remplacez `clientcode` par votre code client, puis ajoutez le texte ou l’image à lier à l’[URL d’exclusion](/help/dev/before-implement/privacy/privacy.md).

## Limites connues

* Le mode assurance qualité n’est pas contigu lorsque vous disposez de CNAME et d’at.js 1.x, car il est basé sur un cookie tiers. La solution consiste à ajouter les paramètres d’aperçu à chaque URL à laquelle vous accédez. Le mode assurance qualité est contigu lorsque vous disposez de CNAME et d’at.js 2.x.
* Lors de l’utilisation de CNAME, il est plus probable que la taille de l’en-tête du cookie pour les appels [!DNL Target] augmente. [!DNL Adobe] recommande de conserver la taille du cookie inférieure à 8 Ko.
