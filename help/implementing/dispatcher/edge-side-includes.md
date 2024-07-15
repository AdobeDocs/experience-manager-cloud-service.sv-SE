---
title: Edge Side Includes
description: Hanterad CDN i Adobe har nu stöd för Edge Side Includes (ESI), ett markeringsspråk för dynamisk sammanställning av webbinnehåll på edge-nivå.
feature: Dispatcher
exl-id: 35093477-2788-4f69-80a9-899f43567cae
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Edge Side Includes {#edge-side-includes}

>[!NOTE]
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i det tidiga adopterprogrammet skickar du ett e-postmeddelande till `aemcs-cdn-config-adopter@adobe.com` och beskriver ditt användningsexempel.

Leveranshastigheten för innehåll drar fördel av att sidor cachelagras mycket, vilket uppnås genom att cache-rubriker ställs in med TTL-värden (high time to live). Detta kan vara en utmaning när sidor innehåller dynamiskt innehåll, som måste uppdateras ofta eller som inte kan cachas alls. Som tur är finns det strategier där den innehållande HTML-sidan kan cachas med en hög TTL-nivå och skjuta upp hämtningen av de mer dynamiska innehållsfragmenten till en senare tidpunkt, antingen via Javascript på klientsidan eller CDN. Den senare metoden är en standard som kallas Edge Side Includes (ESI), som stöds för webbplatser som återges med AEM publicering. HTML innehåller ESI-taggar som instruerar CDN att skjuta upp sidvisningen till webbläsaren tills den utvärderar dessa taggar och hämtar ytterligare, mer dynamiskt (nedre TTL) innehåll från startpunkten (eller CDN-cachen om TTL-värdet inte har gått ut).

I vissa fall kan Edge Side Includes vara användbart:

* Visa slutanvändarens namn eller annan information som är unik för slutanvändaren.
* Visa en lista över senaste information, t.ex. nyhetsartiklar eller aktiekurser.

## ESI-syntax {#esi-syntax}

ESI-syntaxen är följande om en överordnad sida `/content/page.html` innehåller ett fragment `content/snippets/mysnippet.html`.

```
<html>
  <head>
      <title>My Site</title>
  </head>
  <body>
    <div id="content">
      <esi:include src="/content/snippets/mysnippet.html" />
    </div>
  </body>
</html>
```

Mer information finns i [ESI-specifikationen](https://www.w3.org/TR/esi-lang/).

### Överväganden {#esi-syntax-considerations}

* Följande ESI-taggar stöds: include, comment, remove.
* ESI-taggar bearbetas sekventiellt i CDN i stället för samtidigt, så många ESI-taggar på en sida med låga TTL-värden kan öka fördröjningen för slutanvändarens upplevelse.
* Det maximala djupet för ESI: inkluderingsbearbetning är 5.
* Den högsta totala ESI: inkludera bearbetningsfragment är 256.


## Apache-konfiguration {#esi-apache}

Om du har sidor med ESI-taggar bör du deklarera följande egenskaper i Apache-konfigurationen:

```
<LocationMatch "/parent-pages/*content/page.html">
   # disable dispatcher compression
   SetEnv no-gzip 1
   # enable esi processing 
   Header set x-aem-esi "on"
   # enable edgeCDN compression
   Header set x-aem-compress "on"

   # typically the main page is cached at the CDN
   Header always set Cache-Control "max-age=300"
 </LocationMatch>


<LocationMatch "/content/snippets/mysnippet.html">
  SetEnv no-gzip 1

  # typically the included page is either set to a lower TTL than the parent page, or not cached at all, as these 2 commented declarations show, respectively:
  #Header always set Cache-Control "no-cache"
  #Header always set Cache-Control "max-age=50"
 </LocationMatch> 
```

De konfigurerade egenskaperna har följande beteende:

| Egenskap | Beteende |
|-----------|--------------------------|
| **no-gzip** | Om värdet är 1 överförs HTML-sidan från cache till CDN-okomprimerad. Detta är nödvändigt för ESI eftersom innehållet måste skickas till CDN okomprimerat så att CDN kan se och utvärdera ESI-taggarna.<br/><br/>Både den överordnade sidan och de inkluderade fragmenten ska ange no-gzip till 1.<br/><br/>Den här inställningen åsidosätter den komprimeringsinställning som Apache eventuellt har använt på annat sätt, baserat på begärans `Accept-Encoding` -värden. |
| **x-aem-esi** | Om värdet är &quot;on&quot; utvärderas den överordnade HTML-sidans ESI-taggar.  Som standard är rubriken inte inställd. |
| **x-aem-compress** | Om inställningen är &quot;på&quot; komprimeras innehållet från CDN till webbläsaren. Eftersom överföringen av den överordnade sidan från apache till CDN måste vara okomprimerad för att ESI ska fungera (`no-gzip` inställd på 1) kan detta minska fördröjningen.<br/><br/>Om den här rubriken inte har angetts skickas även innehåll till klienten okomprimerat när CDN hämtar innehåll från det ursprungliga innehållet. Det är därför nödvändigt att ange den här rubriken om `no-gzip` är inställd på 1 (krävs för ESI) och du vill skicka innehåll som komprimerats från CDN till webbläsaren. |

## Sling Dynamic Include {#esi-sdi}

Även om det inte krävs kan [Sling Dynamic Include](https://sling.apache.org/documentation/bundles/dynamic-includes.html) (SDI) användas för att generera ESI-fragment som tolkas vid CDN.
