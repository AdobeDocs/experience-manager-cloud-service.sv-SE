---
title: Hur bäddar jag in anpassningsbara formulär på en extern webbsida?
description: Lär dig bädda in en adaptiv Forms på en webbplats.
topic-tags: author
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 00b8cd79-bf2d-4001-b2d6-1b020c868008
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Bädda in anpassningsbara formulär på en extern webbsida{#embed-adaptive-form-in-external-web-page}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Du kan [bädda in anpassningsbara formulär på en AEM Sites-sida](/help/forms/embed-adaptive-form-aem-sites.md) eller en webbsida som ligger på AEM. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att stanna kvar i sitt sammanhang för andra element på webbsidan och interagera med formuläret samtidigt.

## Förutsättningar {#prerequisites}

Utför följande steg innan du bäddar in ett anpassat formulär på en extern webbplats

* Publicera det adaptiva formulär som ska bäddas in i Publish-instansen av AEM Forms Server.
* Skapa eller identifiera en webbsida på webbplatsen där du kan lägga upp det adaptiva formuläret. Kontrollera att webbsidan kan [läsa jQuery-filer från ett CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) eller har en lokal kopia av jQuery inbäddad. jQuery krävs för att återge ett anpassat formulär.
* När AEM och webbsidan finns på olika domäner utför du stegen som anges i avsnittet, [göra det möjligt för AEM Forms att skicka adaptiva formulär till en domänövergripande webbplats](#cross-site).

## Bädda in anpassat formulär {#embed-adaptive-form}

Du kan bädda in ett anpassat formulär genom att infoga några rader med JavaScript på webbsidan. API:t i koden skickar en HTTP-begäran till AEM för adaptiva formulärresurser och injicerar det adaptiva formuläret i den angivna formulärbehållaren.

Så här bäddar du in det anpassade formuläret:

1. Skapa en webbsida på webbplatsen med följande kod:

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the path of the adaptive form
           // For Example: /content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. I den inbäddade koden:

   * Ändra värdet för *options.path* variabel med sökvägen till den publicerings-URL som används i det adaptiva formuläret. Om AEM körs på en kontextsökväg kontrollerar du att URL:en innehåller kontextsökvägen. Ange alltid det fullständiga namnet på det adaptiva formuläret inklusive tillägget. Koden ovan och adaptiv kod finns till exempel på samma AEM Forms Server så att exemplet använder kontextsökvägen för adaptiv form `/content/forms/af/locbasic.html`.
   * Ersätt *options.dataRef* med attribut att skicka med URL:en. Du kan använda dataref-variabeln för att [förifylla ett anpassat formulär](/help/forms/prepopulate-adaptive-form-fields.md).
   * Ersätt *options.themePath* med sökvägen till ett annat tema än det som har konfigurerats i det adaptiva formuläret. Du kan också ange temats sökväg med hjälp av attributet request.
   * CSS_Selector är CSS-väljaren för den formulärbehållare där det adaptiva formuläret är inbäddat. Klassen .customafsection css är till exempel CSS-väljaren i exemplet ovan.

Det anpassningsbara formuläret är inbäddat på webbsidan. Observera följande i den inbäddade adaptiva formen:

* Sidhuvudet och sidfoten i det ursprungliga adaptiva formuläret inkluderas inte i det inbäddade formuläret.
* Utkast och inskickade formulär finns på fliken Utkast och inskickningar i Forms Portal.
* Den Skicka-åtgärd som är konfigurerad i det ursprungliga adaptiva formuläret behålls i det inbäddade formuläret.
* Anpassningsbara formulärregler behålls och fungerar fullt ut i det inbäddade formuläret.
* Upplevelsemål- och A/B-tester som konfigurerats i det ursprungliga adaptiva formuläret fungerar inte i det inbäddade formuläret.
* Om Adobe Analytics har konfigurerats på originalformuläret hämtas analysdata av Adobe Analytics-servern. Den finns dock inte i Forms analysrapport.

## Exempel på topologi {#sample-topology}

Den externa webbsidan som bäddar in det adaptiva formuläret skickar begäranden till AEM server, som vanligtvis ligger bakom brandväggen i ett privat nätverk. För att säkerställa att förfrågningarna dirigeras säkert till AEM bör du konfigurera en omvänd proxyserver.

Vi ska titta på ett exempel på hur du kan konfigurera en omvänd Apache 2.4-proxyserver utan en Dispatcher. I det här exemplet är du värd för AEM server med `/forms` kontextbana och karta `/forms` för den omvända proxyn. Alla förfrågningar om `/forms` på Apache-servern dirigeras till AEM. Den här topologin hjälper till att minska antalet regler i Dispatcher-lagret som alla begäranden som föregås av `/forms` till AEM.

1. Öppna `httpd.conf` konfigurationsfilen och avkommentera följande kodrader. Du kan också lägga till de här kodraderna i filen.

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Ställ in proxyregler genom att lägga till följande kodrader i `httpd-proxy.conf` konfigurationsfil.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Ersätt `[AEM_Instance]` med den AEM serverns publicerings-URL i reglerna.

Om du inte monterar AEM på en kontextbana är proxyreglerna i Apache-lagret som följer:

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>Om du konfigurerar någon annan topologi måste du lägga till överförings-, förifyllnings- och andra URL-adresser till tillåtelselista i Dispatcher-lagret.

## God praxis {#best-practices}

Tänk på följande när du bäddar in ett anpassat formulär på en webbsida:

* Kontrollera att formateringsreglerna som definieras i webbsidans CSS inte är i konflikt med formulärobjektets CSS. För att undvika konflikterna kan du återanvända webbsidans CSS i det adaptiva formulärtemat med hjälp av AEM klientbibliotek. Mer information om hur du använder klientbiblioteket i adaptiva formulärteman finns i [Teman i AEM Forms](/help/forms/themes.md).
* Låt formulärbehållaren på webbsidan använda hela fönsterbredden. Det ser till att CSS-reglerna som konfigurerats för mobila enheter fungerar utan ändringar. Om formulärbehållaren inte får hela fönsterbredden måste du skriva anpassad CSS för att formuläret ska kunna anpassas till olika mobila enheter.
* Använd `[getData](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/GuideBridge.html)` API för att hämta XML- eller JSON-representationen av formulärdata i klienten.
* Använd `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/GuideBridge.html)` API för att ta bort det adaptiva formuläret från HTML DOM.
* Ange huvudet för åtkomstkontrollens ursprung när du skickar ett svar från en AEM server.

## Möjliggör för AEM Forms att skicka adaptiva formulär till en domänövergripande webbplats {#cross-site}

1. Vid AEM publiceringsinstans går du till AEM Web Console Configuration Manager på `https://'[server]:[port]'/system/console/configMgr`.
1. Leta reda på och öppna **Apache Sling Referer-filter** konfiguration.
1. I fältet Tillåtna värdar anger du den domän där webbsidan finns. Det gör att värddatorn kan göra POST-förfrågningar till AEM. Du kan också använda reguljära uttryck för att ange en serie externa programdomäner.

>[!MORELIKETHIS]
>
>* [Bädda in anpassningsbara formulär baserade på kärnkomponenter på en extern webbsida](/help/forms/embed-adaptive-form-core-components-external-web-page.md)
