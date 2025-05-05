---
title: GraphQL Persisted Queries - aktivera cachelagring i Dispatcher
description: Dispatcher är ett cachnings- och säkerhetslager framför Adobe Experience Manager Publish-miljöer. Du kan aktivera cachelagring för beständiga frågor i AEM Headless.
feature: Headless, Dispatcher, GraphQL API
exl-id: 30a97e56-6699-41c4-a4eb-fc6236667f8f
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# GraphQL Persisted Queries - aktivera cachelagring i Dispatcher {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Om cachelagring i Dispatcher är aktiverat behövs inte [CORS-filtret](/help/headless/deployment/cross-origin-resource-sharing.md), så avsnittet kan ignoreras.

Cachelagring av beständiga frågor är inte aktiverat som standard i Dispatcher. Standardaktivering är inte möjlig eftersom kunder som använder CORS (Cross-Origin Resource Sharing) med flera ursprung måste granska och eventuellt uppdatera sin Dispatcher-konfiguration.

>[!NOTE]
>
>Dispatcher cachelagrar inte huvudet `Vary`.
>
>Cachelagring av andra CORS-relaterade rubriker kan aktiveras i Dispatcher, men kan vara otillräcklig om det finns flera CORS-ursprung.

>[!NOTE]
>
>Detaljerad dokumentation om Dispatcher finns i [Dispatcher Guide](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=sv-SE).

## Aktivera cachelagring av beständiga frågor {#enable-caching-persisted-queries}

Om du vill aktivera cachelagring av beständiga frågor definierar du Dispatcher-variabeln `CACHE_GRAPHQL_PERSISTED_QUERIES`:

1. Lägg till variabeln i Dispatcher-filen `global.vars`:

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>För att få fram individuell `ETag`-huvudberäkning för de cachelagrade beständiga frågorna (för *each*-svar som är unika) måste `FileETag Digest`-inställningen användas i den virtuella värdkonfigurationen för dispatcherns konfiguration (om den inte redan finns):
>
>```xml
><Directory />    
>   ...    
>   FileETag Digest
></Directory> 
>```

>[!NOTE]
>
>För att uppfylla [Dispatcher-kraven för dokument som kan cachas](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html?lang=sv-SE#how-does-the-dispatcher-return-documents%3F) lägger Dispatcher till suffixet `.json` i alla beständiga fråge-URL:er, så att resultatet kan cachas.
>
>Det här suffixet läggs till av en omskrivningsregel när den beständiga frågecachelagringen är aktiverad.

## CORS-konfiguration i Dispatcher {#cors-configuration-in-dispatcher}

Kunder som använder CORS-begäranden kan behöva granska och uppdatera sin CORS-konfiguration i Dispatcher.

* Rubriken `Origin` får inte skickas till AEM publicera via Dispatcher:
   * Kontrollera filen `clientheaders.any`.
* CORS-begäranden måste i stället utvärderas för tillåtna ursprung på Dispatcher-nivå. På så sätt säkerställs också att CORS-relaterade rubriker ställs in korrekt, på ett och samma ställe, i samtliga fall.
   * En sådan konfiguration bör läggas till i filen `vhost`. En exempelkonfiguration ges nedan. För enkelhetens skull har endast den korrespondensrelaterade delen angetts. Du kan anpassa den efter dina specifika användningsexempel.

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```
