---
title: Bästa metoder för SEO- och URL-hantering för Adobe Experience Manager as a Cloud Service
description: Bästa metoder för SEO- och URL-hantering för Adobe Experience Manager as a Cloud Service
translation-type: tm+mt
source-git-commit: d1e789527bed9e846dfc265c757889fcd96feaf5
workflow-type: tm+mt
source-wordcount: '3124'
ht-degree: 100%

---


# Bästa metoder för SEO- och URL-hantering för Adobe Experience Manager as a Cloud Service{#seo-and-url-management-best-practices-for-aem}

Sökmotoroptimering (SEO) har blivit en viktig fråga för många marknadsförare. Därför måste SEO-frågor hanteras i många Adobe Experience Manager (AEM) as a Cloud Service-projekt.

I det här dokumentet beskrivs först några [SEO-metodtips](#seo-best-practices) och rekommendationer för hur du kan använda dem på en AEM as a Cloud Service-implementering. Sedan får du en närmare titt på några av de mer [komplexa implementeringsstegen](#aem-configurations) som togs upp i det första avsnittet.

## SEO-metodtips {#seo-best-practices}

I det här avsnittet beskrivs några allmänna SEO-metodtips.

### URL:er {#urls}

Det finns vissa allmänt vedertagna bästa metoder för URL:er.

Ställ följande fråga när du utvärderar URL:er i ett AEM-projekt:

*”Skulle en användare kunna beskriva vad sidan är om han/hon bara kunde se URL:en och inget av sidans innehåll?”*

Om svaret är ja är det troligt att URL:en är lämplig för en sökmotor.

Här följer några allmänna tips om hur du skapar URL:er för SEO:

* Använd bindestreck för att avgränsa ord.

   * Namnge sidor med bindestreck (-) som avgränsare.
   * Undvik att använda kamelnotation, understreck och mellanslag.

* Undvik att använda frågeparametrar när det är möjligt. Begränsa dem till två eller färre om de behövs.

   * Använd katalogstrukturen för att ange informationsarkitekturen, om en sådan finns.
   * Om en katalogstruktur inte är ett alternativ bör du använda Sling-väljare i URL:en i stället för frågesträngar. Du kan även göra sidorna cachelagringsbara för dispatchern med hjälp av Sling-väljare, utöver SEO-värdet som de ger.

* Ju enklare en URL är att läsa, desto bättre – nyckelord i URL:en ökar värdet.

   * När du använder väljare på en sida är det bäst att använda väljare som har ett semantiskt värde.
   * Om en användare inte kan läsa URL:en kan inte en sökmotor heller göra det.
   * Till exempel:

      `mybrand.com/products/product-detail.product-category.product-name.html`
är att föredra framför 
`mybrand.com/products/product-detail.1234.html`

* Undvik underdomäner när det är möjligt eftersom sökmotorer behandlar dem som andra enheter, vilket fragmenterar webbplatsens SEO-värde.

   * Använd i stället undersökvägar på första nivån. Använd till exempel `www.mybrand.com/es/home.html` istället för `es.mybrand.com/home.html`.

   * Planera innehållshierarkin så att den matchar hur innehållet kommer att presenteras, enligt den här riktlinjen.

* URL:ens nyckelordseffektivitet minskar ju längre URL:en är och nyckelordets position ökar. Med andra ord är kortare bättre.

   * Använd tekniker och funktioner för förkortning av URL:er från AEM för att ta bort onödiga URL-delar.
   * Till exempel är `mybrand.com/en/myPage.html` att föredra framför `mybrand.com/content/my-brand/en/myPage.html`.

* Använd kanoniska URL:er.

   * Använd en `rel=canonical`-tagg på sidan när en URL kan hanteras från olika sökvägar, eller med olika parametrar eller väljare.

   * Den kan inkluderas i koden för AEM-mallen.

* Matcha URL:er med sidtitlar när det är möjligt.

   * Innehållsförfattare bör uppmuntras att följa den här metoden.

* Stöd skiftlägesokänslighet i URL-begäranden.

   * Konfigurera dispatchern att skriva om alla inkommande begäranden som gemener.
   * Utbilda innehållsförfattarna att skapa alla sidor med gemener.

* Se till att varje sida bara hanteras från ett protokoll.

   * Ibland hanteras webbplatser över `http` tills en användare når en sida med t.ex. ett utchecknings- eller inloggningsformulär, då sidan växlar till `https`. Om användaren kan återvända till `http`-sidor och komma åt dem via `https`, spåras de som två separata sidor vid länkning från den här sidan.

   * Google föredrar för närvarande `https`-sidor framför `http`-sidor. Därför gör det, för det mesta, att allas liv blir lättare om hela webbplatsen hanteras över `https`.

### Serverkonfiguration {#server-configuration}

Följ följande steg för serverkonfigurationen för att se till att endast rätt innehåll crawlas:

* Använd en `robots.txt`-fil för att blockera crawlning av innehåll som inte ska indexeras.

   * Blockera **all** crawlning i testmiljöer.

* Implementera 301-omdirigeringar när du startar en ny webbplats med uppdaterade URL:er, för att säkerställa att din befintliga SEO-rankning inte går förlorad.
* Inkludera en favoritikonbild för webbplatsen.
* Implementera en XML-webbplatskarta som gör det enklare för sökmotorer att crawla innehållet. Se till att du inkluderar en mobilwebbplatskarta för mobiler och/eller responsiva webbplatser.

## AEM-konfigurationer {#aem-configurations}

I det här avsnittet beskrivs de implementeringssteg som krävs för att konfigurera AEM för att följa dessa SEO-rekommendationer.

### Använda Sling-väljare {#using-sling-selectors}

Tidigare var användning av frågeparametrar den allmänt accepterade metoden när ett företagswebbprogram byggdes.

Trenden under de senaste åren har varit att ta bort dessa i ett försök att göra webbadresserna enklare att läsa. På många plattformar innebär det att omdirigeringar implementeras på webbservern eller innehållsleveransnätverket (CDN) – men Sling gör det enklare. Sling-väljare:

* gör webbadresser enklare att läsa
* gör att du kan cachelagra sidorna på dispatchern och förbättrar ofta säkerheten
* gör att du kan adressera innehållet direkt, i stället för att ha en allmän servlet som hämtar innehållet. Det här ger dig fördelarna med åtkomstkontrollistor som du tillämpar på databasen och filter som du tillämpar på dispatchern.

#### Använda väljare för servletar {#using-selectors-for-servlets}

AEM ger oss två alternativ när vi skriver servletar:

* **bin**-servletar
* **Sling**-servletar

Följande exempel visar hur du registrerar servletar som följer båda dessa mönster samt fördelarna med att använda Sling-servletar.

#### Bin-servletar (en nivå ned) {#bin-servlets-one-level-down}

**Bin**-servletar följer mönstret som många utvecklare är vana vid från J2EE-programmering. Servleten registreras på en viss sökväg, som för AEM vanligtvis finns under `/bin`, och du extraherar de nödvändiga parametrarna från frågesträngen.

SCR-anteckningen för den här typen av servlet skulle se ut ungefär så här:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Sedan extraherar du parametrarna från frågesträngen via objektet `SlingHttpServletRequest` som finns i metoden `doGet`. Till exempel:

```
String myParam = req.getParameter("myParam");
```

Den URL som skapas skulle se ut ungefär så här:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Några saker att ha i åtanke:

* Själva URL:en förlorar SEO-värde. Användare som har åtkomst till webbplatsen, inklusive sökmotorer, får inga semantiska värden från URL:en eftersom URL:en representerar en programmatisk sökväg och inte innehållshierarkin.
* Närvaron av frågeparametrar i URL:en innebär det att dispatchern inte kan cachelagra svaret.
* Om du vill skydda servleten måste du implementera en egen anpassad säkerhetslogik i den.
* Dispatchern måste konfigureras (med försiktighet) för att visa `/bin/myApp/myServlet`. Att helt enkelt visa `/bin` ger åtkomst till vissa servletar som inte ska vara öppna för webbplatsens besökare.

#### Sling-servletar (en nivå ned) {#sling-servlets-one-level-down}

Med **Sling**-servletar kan du registrera en servlet på motsatt sätt. I stället för att adressera en servlet och ange det innehåll som du vill att servleten ska återge baserat på frågeparametrarna, kan du adressera det innehåll som du vill ha och ange den servlet som ska återge innehållet baserat på Sling-väljare.

SCR-anteckningen för den här typen av servlet skulle se ut ungefär så här:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

I det här fallet är den resurs som URL:en adresserar (en instans av resursen `myPageType`) automatiskt tillgänglig i servleten. För att få åtkomst till den ska du anropa:

```
Resource myPage = req.getResource();
```

Den URL som skapas skulle se ut ungefär så här:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

Fördelarna med det här tillvägagångssätt är:

* Du kan baka in SEO-värdet, som genereras av semantiken i webbplatshierarkin och sidnamnet.
* Eftersom det inte finns några frågeparametrar kan dispatchern cachelagra svaret. Uppdateringar som görs på den adresserade webbplatsen kommer dessutom att göra cacheminnet ogiltigt när sidan aktiveras.
* Alla åtkomstkontrollistor som tillämpas på `/content/my-brand/my-page` aktiveras när en användare försöker få åtkomst till den här servleten.
* Dispatchern kommer redan att vara konfigurerad för att hantera det här innehållet som en funktion för att betjäna webbplatsen. Ingen ytterligare konfiguration krävs.

### URL-omskrivning {#url-rewriting}

I AEM lagras alla webbplatser under `/content/my-brand/my-content`. Det kan vara användbart för databashantering, men det är inte nödvändigtvis så du vill att dina kunder ska se din webbplats och det kan strida mot SEO-riktlinjen som förespråkar att URL:er ska hållas så korta som möjligt. Dessutom kan du betjäna flera webbplatser från samma AEM-instans och från olika domännamn.

I det här avsnittet beskrivs alternativen i AEM som används för att hantera URL:erna och hur de kan presenteras för användarna på ett mer läsbart och SEO-vänligt sätt.

#### Alternativa URL:er {#vanity-urls}

Om en författare vill att en sida ska vara tillgänglig från en andra plats i marknadsföringssyfte, kan det vara användbart att definiera alternativa URL:er, sida för sida, för AEM. Om du vill lägga till en alternativ URL för en sida ska du gå till den i konsolen **Webbplatser** och redigerar sidegenskaperna. Det finns ett avsnitt där du kan lägga till alternativa URL:er längst ned på fliken **Grundläggande**. Tänk på att sidans SEO-värde fragmenteras om sidan är tillgänglig via mer än en URL. Du kan dock undvika det här problemet genom att lägga till en kanonisk URL-tagg på sidan.

#### Lokaliserade sidnamn {#localized-page-names}

Du kanske vill visa lokaliserade sidnamn för användare av översatt innehåll. Till exempel:

* I stället för att en spansk användare går till:
   `www.mydomain.com/es/home.html`

* Vore det bättre om URL:en var:
   `www.mydomain.com/es/casa.html`.

Utmaningen med att lokalisera sidans namn är att många av de lokaliseringsverktyg som är tillgängliga på AEM-plattformen kräver att sidnamnen matchar för alla språk för att innehållet ska kunna synkroniseras.

Egenskapen `sling:alias` gör att du både kan äta kakan och ha den kvar. Du kan lägga till `sling:alias` som en egenskap för alla resurser för att tillåta att ett aliasnamn används för resursen. I föregående exempel skulle du få:

* En sida i JCR:
   `…/es/home`

* Lägg sedan till en egenskap till den:
   `sling:alias` = `casa`

På så sätt kan AEM-översättningsverktyg som Multi Site Manager fortsätta att upprätthålla relationen mellan:

* `/en/home`

* `/es/home`

Samtidigt som slutanvändarna kan visa sidnamnen på olika språk.

>[!NOTE]
>
>Egenskapen `sling:alias` kan anges med [aliasegenskapen vid redigering av sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced).

#### /etc/map {#etc-map}

I en vanlig AEM-installation:

* för OSGi-konfigurationen
   **Apache Sling Resource Resolver Factory**
( 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* egenskapen
   **Mappningsplats** ( `resource.resolver.map.location`)

* blir som standard `/etc/map`.

Mappningsdefinitioner kan läggas till på den här platsen för att mappa inkommande begäranden, skriva om URL:er på sidorna i AEM, eller både och.

Om du vill skapa en ny mappning ska du skapa en ny `sling:Mapping`-nod på den här platsen under `/http` eller `/https`. Baserat på egenskaperna `sling:match` och `sling:internalRedirect` som har angetts för den här noden dirigerar AEM om all trafik för den matchade URL:en till det värde som har angetts i egenskapen `internalRedirect`.

Det här är den metod som beskrivs i den officiella AEM- och Sling-dokumentationen, men det stöd för reguljära uttryck som tillhandahålls av implementeringen är begränsat i omfattning jämfört med de alternativ som är tillgängliga om `SlingResourceResolver` används direkt. Implementering av mappningar på det här sättet kan dessutom leda till problem med cachelagring av ogiltighetsposter.

Här är ett exempel på hur problemet uppstår:

1. En användare besöker webbplatsen och begär `https://www.mydomain.com/my-page.html`
1. Dispatchern vidarebefordrar begäran till publiceringsservern.
1. Publiceringsservern skickar begäran till `/content/my-brand/my-page` med `/etc/map` och återger sidan.

1. Dispatchern cachelagrar svaret på `/my-page.html` och returnerar svaret till användaren.
1. En innehållsförfattare gör en ändring på sidan och aktiverar den.
1. Dispatcherns rensningsagent skickar en begäran om ogiltigförklaring för `/content/my-brand/my-page`**.** Det gamla innehållet förblir cachelagrat och kommer att vara inaktivt eftersom dispatchern inte har någon sida cachelagrad på den här sökvägen.

Det finns sätt att konfigurera anpassade rensningsregler för dispatcher som mappar den kortare URL:en till den längre URL:en för cachelagring av ogiltighetsposter.

Det finns dock ett enklare sätt att hantera det här på:

1. **SlingResourceResolver-regler**

   Du kan konfigurera Sling Resource Resolver med webbkonsolen (till exempel localhost:4502/system/console/configMgr):

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   Vi rekommenderar att du skapar de mappningar som krävs för att korta ned URL:er som reguljära uttryck och sedan definierar konfigurationerna under en OSGi-konfigurationsnod, `config.publish`, som ingår i bygget.

   I stället för att definiera mappningarna i `/etc/map` kan de tilldelas direkt till egenskapen **URL-mappningar** ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   I det här enkla exemplet tar du bort `/content/my-brand/` från början av alla URL:er där den finns.

   Det konverterar en URL:

   * från `/content/my-brand/my-page.html`
   * till bara `/my-page.html`

   Vilket är i linje med rekommendationen att hålla URL:erna så korta som möjligt.

1. **Mappa URL-utdata på sidor**

   När du har definierat mappningarna i Apache Sling Resource Resolver måste du använda mappningarna i dina komponenter för att se till att de URL:er som du skapar på sidorna är korta och tydliga. Du kan göra det med Mappningsfunktionen i `ResourceResolver`.

   Om du till exempel implementerade en anpassad navigeringskomponent som listar de underordnade sidorna för den aktuella sidan kan du använda mappningsmetoden så här:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

Hittills har du implementerat mappningar tillsammans med logiken i dina komponenter för att använda mappningarna när du skriver URL:er på våra sidor.

Den sista biten i pusslet är att hantera de förkortade URL:erna när de kommer till dispatchern, och det är nu som `mod_rewrite` kommer in i bilden. Den största fördelen med att använda `mod_rewrite` är att URL:erna mappas tillbaka till de långa versionerna *innan* de skickas till dispatchermodulen. Det innebär att dispatchern begär den långa URL:en från publiceringsservern och cachelagrar den därefter. Alla begäranden om rensning av dispatchern som kommer in från publiceringsservern kan därför göra det här innehållet ogiltigt.

Om du vill implementera den här reglerna kan du lägga till `RewriteRule`-element under den virtuella värden i Apache HTTP Server-konfigurationen. Om du vill utöka de förkortade URL:erna från det tidigare exemplet kan du implementera en regel som ser ut så här:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Kanoniska URL-taggar {#canonical-url-tags}

Kanoniska URL-taggar är länktaggar som placeras i ett HTML-dokuments sidhuvud för att klargöra hur sökmotorer ska hantera en sida när innehållet indexeras. Fördelen som de ger är att de säkerställer att (olika versioner av) en sida indexeras som samma sida även när sidans URL kan innehålla skillnader.

Om en webbplats till exempel har en utskriftsvänlig version av en sida skulle en sökmotor kunna indexera sidan separat från den vanliga versionen av sidan. Den kanoniska taggen anger för sökmotorn att de är samma sida.

Exempel:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

Båda skulle använda följande tagg i sidans sidhuvud:

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

`href` kan vara relativt eller absolut. Koden bör inkluderas i sidmarkeringen för att fastställa sidans kanoniska URL och returnera den här taggen.

### Konfigurera dispatchern för skiftlägesokänslighet {#configuring-the-dispatcher-for-case-insensitivity}

Den bästa metoden är att skicka alla sidor med gemener. Du vill däremot inte att en användare som får åtkomst till webbplatsen med URL med versaler får en 404-felkod. Därför rekommenderar Adobe att du lägger till en omskrivningsregel i Apache HTTP Server-konfigurationen för att mappa alla inkommande URL:er till gemener. Dessutom måste innehållsförfattarna få utbildning i hur de skapar sidor med namn i gemener.

Lägg till följande i `vhost`-konfigurationen om du vill konfigurera Apache för att tvinga all inkommande trafik till gemener:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Lägg dessutom till följande längst upp i filen `htaccess`:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementera robots.txt för att skydda utvecklingsmiljöer {#implementing-robots-txt-to-protect-development-environments}

Sökmotorer *bör* kontrollera om det finns en `robots.txt`-fil i webbplatsroten innan de crawlar webbplatsen. Det bör understrykas att även om stora sökmotorer som Google, Yahoo och Bing gör det, så gör inte vissa utländska sökmotorer det.

Det enklaste sättet att blockera åtkomst till hela webbplatsen är att placera en fil med namnet `robots.txt` i webbplatsroten med följande innehåll:

```xml
User-agent: *
Disallow: /
```

I en aktiv miljö kan du även välja att inte tillåta specifika sökvägar som du inte vill indexera.

Något att tänka på när `robots.txt`-filen placeras i webbplatsroten är att begäranden om rensning av dispatchern kan ta bort filen och URL-mappningar kommer troligtvis att placera webbplatsroten på en annan plats än `DOCROOT`, enligt Apache HTTP Server-konfigurationen. Därför är det vanligt att placera den här filen på författarinstansen i webbplatsroten och replikera den till publiceringsinstansen.

### Bygga en XML-webbplatskarta på AEM {#building-an-xml-sitemap-on-aem}

Crawlers använder XML-webbplatskartor för att bättre förstå webbplatsernas struktur. Det är en vedertagen bästa metod, även om det inte finns någon garanti för att en webbplatskarta kommer att ge en förbättrad SEO-rankning. Du kan underhålla en XML-fil manuellt på webbservern och använda den som en webbplatskarta, men vi rekommenderar att du genererar webbplatskartan programmatiskt, vilket säkerställer att webbplatskartan automatiskt återspeglar ändringarna när författare skapar nytt innehåll.

Om du vill skapa en webbplatskarta programmatiskt registrerar du en Sling-servlet som lyssnar efter ett `sitemap.xml`-anrop. Servleten kan sedan använda resursen som tillhandahålls via servletens API för att titta på den aktuella sidan och dess underordnade sidor, och skapa XML. XML-filen cachelagras sedan i dispatchern. Den här platsen bör refereras till i egenskapen för webbplatskartan för filen `robots.txt`. Dessutom måste en anpassad rensningsregel implementeras för att säkerställa att filen rensas när en ny sida aktiveras.

>[!NOTE]
>
>Du kan registrera en Sling-servlet för att lyssna efter väljaren `sitemap` med tillägget `xml`. Det gör att servleten bearbetar begäran varje gång en URL begärs som slutar med:
>    `/<path-to>/page.sitemap.xml`
>Du kan sedan hämta den begärda resursen från begäran och generera en webbplatskarta från den punkten i innehållsträdet med API:erna för JCR.
>Den här typen av metod ger en fördel när du har flera webbplatser som hanteras från samma instans. En begäran till `/content/siteA.sitemap.xml` genererar en webbplatskarta för `siteA`, medan en begäran till `/content/siteB.sitemap.xml` genererar en webbplatskarta för `siteB` utan att du behöver skriva ytterligare kod.

### Skapa 301-omdirigeringar för äldre URL:er {#creating-redirects-for-legacy-urls}

När du startar en webbplats med en ny struktur är det av två skäl viktigt att implementera och testa 301-omdirigeringar i Apache HTTP Server:

* De äldre URL:erna har byggt upp ett SEO-värde över tid. Genom att implementera en omdirigering kan sökmotorn tillämpa det värdet på den nya URL:en.
* Webbplatsens användare kan ha skapat bokmärken på de gamla sidorna. Genom att implementera omdirigeringar kan du vara säker på att användarna skickas vidare till de sidor på den nya webbplatsen som mest liknar de sidor som de försöker ta sig till på den gamla webbplatsen.

Anvisningar för hur 301-omdirigeringar implementeras och information om ett verktyg som kan användas för att testa att omdirigeringarna fungerar som väntat finns i följande avsnitt.

## Ytterligare resurser {#additional-resources}

Mer information finns i följande resurser:

<!--
* [Resource Mapping](/help/sites-deploying/resource-mapping.md)
-->

* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
