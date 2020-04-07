---
title: Bästa praxis för SEO- och URL-hantering för Adobe Experience Manager som en molntjänst
seo-title: Bästa praxis för SEO- och URL-hantering för Adobe Experience Manager som en molntjänst
translation-type: tm+mt
source-git-commit: 70e76205e82b491fa77f65cd4257a79dda17b882

---


# Bästa praxis för SEO- och URL-hantering för Adobe Experience Manager som en molntjänst{#seo-and-url-management-best-practices-for-aem}

SEO (Search Engine Optimization) har blivit en viktig fråga för många marknadsförare. Därför måste SEO-problem hanteras i många Adobe Experience Manager (AEM) som ett molnserviceprojekt.

I det här dokumentet beskrivs först några [SEO-metodtips](#seo-best-practices) och rekommendationer för hur du kan uppnå dessa på en AEM som en molntjänst-implementering. Sedan går det djupare in i några av de mer [komplexa implementeringssteg](#aem-configurations) som togs upp i det första avsnittet.

## SEO Best Practices {#seo-best-practices}

I det här avsnittet beskrivs några allmänna SEO-metoder.

### URL:er {#urls}

Det finns vissa allmänt vedertagna bästa metoder när det gäller URL-adresser.

I ditt AEM-projekt kan du fråga dig följande när du utvärderar dina URL:er:

&quot;Om en användare skulle se den här URL:en och inget av innehållet på sidan, kunde de då beskriva vad sidan var?&quot;

Om svaret är ja är det troligt att URL:en fungerar bra för en sökmotor.

Här följer några allmänna tips om hur du skapar URL:er för SEO:

* Använd bindestreck för att avgränsa ord.

   * Namnge sidor med bindestreck (-) som avgränsare.
   * Undvik att använda kamelcase, understreck och mellanslag.

* Undvik att använda frågeparametrar när det är möjligt. Vid behov kan du begränsa dem till två eller färre.

   * Använd katalogstrukturen för att ange informationsarkitektur, om sådan finns.
   * Om en katalogstruktur inte är ett alternativ bör du använda delningsväljare i URL:en i stället för frågesträngar. Förutom SEO-värdet som de anger, kan du även göra sidorna tillgängliga för avsändaren med hjälp av snedväljare.

* Ju mer läsbar en URL är, desto bättre. om det finns nyckelord i URL:en ökar värdet.

   * När du använder väljare på en sida är det bäst att använda väljare som har ett semantiskt värde.
   * Om en användare inte kan läsa din URL-adress kan inte en sökmotor heller göra det.
   * Exempel:
      `mybrand.com/products/product-detail.product-category.product-name.html`
är att föredra att `mybrand.com/products/product-detail.1234.html`

* Undvik underdomäner när det är möjligt, eftersom sökmotorer behandlar dem som olika enheter och fragmenterar SEO-värdet för webbplatsen.

   * Använd i stället undersökvägar på första nivån. Använd till exempel i stället för `es.mybrand.com/home.html``www.mybrand.com/es/home.html`.

   * Planera din innehållshierarki så att den matchar hur innehållet presenteras, enligt den här riktlinjen.

* Nyckelordseffektiviteten i URL:er minskar allt eftersom längden på URL:en och nyckelordets position ökar. Med andra ord är kortare bättre.

   * Använd tekniker och funktioner för förkortning av URL:er från AEM för att ta bort onödiga URL-delar.
   * Det `mybrand.com/en/myPage.html` är till exempel att föredra framför `mybrand.com/content/my-brand/en/myPage.html`.

* Använd kanoniska URL:er.

   * När en URL kan hanteras från olika sökvägar eller med olika parametrar eller väljare måste du använda en `rel=canonical` -tagg på sidan.

   * Detta kan inkluderas i koden för AEM-mallen.

* Matcha URL:er med sidtitlar när det är möjligt.

   * Innehållsförfattare bör uppmuntras att följa denna praxis.

* Stöd för skiftlägeskänslighet i URL-begäranden.

   * Konfigurera dispatchern att skriva om alla inkommande begäranden som gemener.
   * Utbilda innehållsförfattare och skapa alla sidor med gemener.

* Se till att varje sida bara hanteras från ett protokoll.

   * Ibland serveras webbplatser `http` tills en användare når en sida med t.ex. ett utchecknings- eller inloggningsformulär, där användaren växlar till `https`. När användaren länkar från den här sidan och kan gå tillbaka till `http` sidor och komma åt dem via `https`dem, spåras de som två separata sidor.

   * Google föredrar för närvarande `https` sidor framför `http` dem. Därför gör det ofta att allas liv blir lättare att serva hela webbplatsen över `https`.

### Serverkonfiguration {#server-configuration}

När det gäller serverkonfigurationen kan du utföra följande steg för att se till att endast rätt innehåll crawlas:

* Använd en `robots.txt` fil för att blockera crawlning av innehåll som inte ska indexeras.

   * Blockera **all** crawlning i testmiljöer.

* När du startar en ny webbplats med uppdaterade URL:er implementerar du 301 omdirigeringar för att säkerställa att din befintliga SEO-rankning inte går förlorad.
* Ta med en favoritikonbild för din webbplats.
* Implementera en XML-webbplatskarta som gör det enklare för sökmotorer att crawla ditt innehåll. Se till att du inkluderar en mobilsajtkarta för mobiler och/eller responsiva sajter.

## AEM-konfigurationer {#aem-configurations}

I det här avsnittet beskrivs de implementeringssteg som krävs för att konfigurera AEM för att följa dessa SEO-rekommendationer.

### Använda delningsväljare {#using-sling-selectors}

Tidigare var användningen av frågeparametrar den allmänt accepterade metoden när ett företagswebbprogram skapades.

Trenden under de senaste åren har varit att ta bort dessa i ett försök att göra webbadresserna mer läsbara. På många plattformar innebär detta implementering av omdirigeringar på webbservern eller CDN (Content Delivery Network), men Sling gör detta enkelt. Sling-väljare:

* Förbättra läsbarheten för webbadresser.
* Gör att du kan cachelagra sidorna i dispatchern och ofta förbättra säkerheten.
* Gör att du kan adressera innehållet direkt, i stället för att ha en allmän server som hämtar innehåll. Detta ger dig de fördelar med åtkomstkontrollistor som du tillämpar på din databas och filter som du tillämpar på dispatchern.

#### Använda väljare för servrar {#using-selectors-for-servlets}

AEM ger oss två alternativ när vi skriver servlets:

* **bin** servlets
* **Sling** servlets

I följande exempel visas hur du registrerar servrar som följer båda dessa mönster samt fördelarna med att använda Sling-servrar.

#### Fackservrar (en nivå ned) {#bin-servlets-one-level-down}

**Bin** -servlets följer mönstret som många utvecklare är vana vid från J2EE-programmering. Servern registreras på en viss sökväg, som i fallet AEM vanligtvis finns under `/bin`, och du extraherar de begärda parametrarna från frågesträngen.

SCR-anteckningen för den här typen av servlet skulle se ut ungefär så här:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Sedan extraherar du parametrarna från frågesträngen via objektet som `SlingHttpServletRequest` finns i `doGet` metoden. till exempel:

```
String myParam = req.getParameter("myParam");
```

Den URL som skapas skulle se ut ungefär så här:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Det finns några saker att tänka på:

* Själva URL-adressen förlorar SEO-värde. Användare som har åtkomst till webbplatsen, inklusive sökmotorer, får inga semantiska värden från URL-adressen eftersom URL-adressen representerar en programmatisk sökväg och inte innehållshierarkin.
* Om det finns frågeparametrar i URL:en innebär det att avsändaren inte kan cachelagra svaret.
* Om du vill skydda den här servern måste du implementera din egen anpassade säkerhetslogik i servermodulen.
* Dispatcharen måste konfigureras (med försiktighet) för att kunna visas `/bin/myApp/myServlet`. Bara exponering `/bin` ger åtkomst till vissa servrar som inte ska vara öppna för besökare på webbplatsen.

#### Sling-serverlets (en nivå ned) {#sling-servlets-one-level-down}

**Med SSLING** -servlets kan du registrera din servlet på motsatt sätt. I stället för att adressera en servlet och ange det innehåll som du vill att serverleten ska återge baserat på frågeparametrarna, kan du adressera det innehåll som du vill ha och ange den serverlet som ska återge innehållet baserat på delningsväljare.

SCR-anteckningen för den här typen av servlet skulle se ut ungefär så här:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

I det här fallet är den resurs som URL-adressen (en instans av `myPageType` resursen) automatiskt tillgänglig i serverutrymmet. Ring:

```
Resource myPage = req.getResource();
```

Den URL som skapas skulle se ut ungefär så här:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

Fördelarna med detta tillvägagångssätt är:

* Du kan baka i SEO-värdet, som genereras av semantiken i platshierarkin och sidnamnet.
* Eftersom det inte finns några frågeparametrar kan avsändaren cachelagra svaret. Uppdateringar som görs på den adresserade sidan kommer dessutom att göra cacheminnet ogiltigt när sidan aktiveras.
* Alla åtkomstkontrollistor som tillämpas på `/content/my-brand/my-page` aktiveras när en användare försöker få åtkomst till den här servern.
* Dispatcharen kommer redan att konfigureras för att hantera det här innehållet som en funktion för att skicka webbplatsen. Ingen ytterligare konfiguration krävs.

### URL-omskrivning {#url-rewriting}

I AEM lagras alla dina webbsidor under `/content/my-brand/my-content`. Detta kan vara användbart när det gäller databasdatahantering, men det är inte nödvändigtvis så du vill att dina kunder ska se din webbplats och det kan strida mot SEO-vägledningen för att hålla URL:erna så korta som möjligt. Dessutom kan du betjäna flera webbplatser från samma AEM-instans och från olika domännamn.

I det här avsnittet beskrivs alternativen i AEM för att hantera dessa URL:er och presentera dem för användarna på ett mer läsbart och SEO-vänligt sätt.

#### Vanity URLs {#vanity-urls}

Om en författare vill att en sida ska vara tillgänglig från en andra plats i kampanjsyfte, kan det vara bra att definiera AEM-adressernas vanlighetsadresser, sida för sida. Om du vill lägga till en huvud-URL för en sida går du till den i **webbplatskonsolen** och redigerar sidegenskaperna. Längst ned på fliken **Grundläggande** , visas ett avsnitt där du kan lägga till egna URL:er. Tänk på att om sidan är tillgänglig via mer än en URL fragmenteras SEO-värdet för sidan, så en kanonisk URL-tagg bör läggas till på sidan för att undvika det här problemet.

#### Lokaliserade sidnamn {#localized-page-names}

Du kanske vill visa lokaliserade sidnamn för användare av översatt innehåll. Exempel:

* I stället för att låta en spansk användare navigera till:
   `www.mydomain.com/es/home.html`

* Det vore bättre om URL:en var:
   `www.mydomain.com/es/casa.html`.

Utmaningen med att lokalisera sidans namn är att många av de lokaliseringsverktyg som är tillgängliga på AEM-plattformen kräver att sidnamnen matchar olika språk för att innehållet ska kunna synkroniseras.

Med den här `sling:alias` egenskapen kan du också äta tårtan. `sling:alias` kan läggas till som en egenskap för alla resurser för att tillåta ett aliasnamn för resursen. I föregående exempel skulle du ha:

* En sida i JCR på:
   `…/es/home`

* Lägg sedan till en egenskap i den:
   `sling:alias` = `casa`

På så sätt kan AEM-översättningsverktyg som Multi-site Manager fortsätta att upprätthålla relationen mellan:

* `/en/home`

* `/es/home`

Samtidigt som slutanvändarna kan interagera med sidnamnet på sina modersmål.

>[!NOTE]
>
>Du kan ange `sling:alias` egenskapen [Alias när du redigerar Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced).

#### /etc/map {#etc-map}

I en vanlig AEM-installation:

* för OSGi-konfigurationen
   **Apache Sling Resource Resolver Factory**( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* egenskapen
   **Mappningsplats** ( `resource.resolver.map.location`)

* blir som standard `/etc/map`.

Mappningsdefinitioner kan läggas till på den här platsen för att mappa inkommande begäranden, skriva om URL:er på sidor i AEM eller båda.

Om du vill skapa en ny mappning skapar du en ny `sling:Mapping` nod på den här platsen under `/http` eller `/https`. Baserat på de `sling:match` - och `sling:internalRedirect` -egenskaper som har angetts för den här noden dirigerar AEM om all trafik för den matchade URL:en till det värde som har angetts i `internalRedirect` egenskapen.

Detta är den metod som beskrivs i den officiella AEM- och Sling-dokumentationen, men det reguljära uttrycksstöd som tillhandahålls av implementeringen är begränsat i omfattning jämfört med de alternativ som är tillgängliga för oss genom att använda `SlingResourceResolver` direkt. Implementering av mappningar på det här sättet kan dessutom leda till problem med invalidering av dispatchercache.

Här är ett exempel på hur det här problemet inträffar:

1. En användare besöker er webbplats och begär `https://www.mydomain.com/my-page.html`
1. Avsändaren vidarebefordrar denna begäran till publiceringsservern.
1. Med `/etc/map`kan publiceringsservern lösa denna begäran till `/content/my-brand/my-page` och återge sidan.

1. Avsändaren cachelagrar svaret vid `/my-page.html` och returnerar svaret till användaren.
1. En innehållsförfattare gör en ändring på den här sidan och aktiverar den.
1. Dispatcherns rensningsagent skickar en begäran om ogiltigförklaring för `/content/my-brand/my-page`**.**Eftersom dispatchern inte har någon sida cachelagrad på den här sökvägen, förblir det gamla innehållet cachelagrat och kommer att vara inaktivt.

Det finns sätt att konfigurera anpassade regler för utskickstömning som mappar den kortare URL:en till den längre URL:en för att cacheogiltigförklaras.

Det finns dock ett enklare sätt att hantera detta:

1. **SlingResourceResolver-regler**

   Med webbkonsolen (till exempel localhost:4502/system/console/configMgr) kan du konfigurera Sling Resource Resolver:

   * **Apache Sling Resource Resolver Factory**
      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   Vi rekommenderar att du skapar de mappningar som krävs för att korta ned URL:er som reguljära uttryck och sedan definierar dessa konfigurationer under en OsgiConfignode, `config.publish`som ingår i ditt bygge.

   I stället för att definiera dina mappningar i `/etc/map`kan de tilldelas direkt till egenskapen **URL Mappings** ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   I det här enkla exemplet tar du bort `/content/my-brand/` från början av en URL där den finns.

   Detta skulle konvertera en URL:

   * from `/content/my-brand/my-page.html`
   * till bara `/my-page.html`
   Detta är i linje med den rekommenderade metoden att hålla URL-adresserna så korta som möjligt.

1. **Mappa URL-utdata på sidor**

   När du har definierat dina mappningar i Resurslösaren för Apache Sling måste du använda dessa mappningar i dina komponenter för att se till att de URL-adresser du skapar på sidorna är korta och tydliga. Du kan göra detta med hjälp av kartfunktionen i `ResourceResolver`.

   Om du till exempel implementerade en anpassad navigeringskomponent som listar de underordnade sidorna för den aktuella sidan kan du använda mappningsmetoden så här:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

Hittills har du implementerat mappningar tillsammans med logiken i dina komponenter för att använda dessa mappningar när du skriver ut URL:er på våra sidor.

Det sista i pusslet är att hantera dessa förkortade URL:er när de kommer in i dispatchern, där det `mod_rewrite` kommer in på lek. Den största fördelen med att använda `mod_rewrite` är att URL-adresserna mappas tillbaka till deras långa formulär *innan* de skickas till dispatchermodulen. Det innebär att avsändaren begär den långa URL:en från publiceringsservern och cachelagrar den därefter. Alla begäranden om rensning av dispatcher som kommer in från publiceringsservern kan därför göra det här innehållet ogiltigt.

Om du vill implementera dessa regler kan du lägga till `RewriteRule` element under den virtuella värden i Apache HTTP Server-konfigurationen. Om du vill utöka de förkortade URL:erna från det tidigare exemplet kan du implementera en regel som ser ut så här:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Kanoniska URL-taggar {#canonical-url-tags}

Kanoniska URL-taggar är länktaggar som placeras i ett HTML-dokuments huvud för att klargöra hur sökmotorer ska hantera en sida när innehållet indexeras. Fördelen med det är att se till att en sida indexeras som samma (olika versioner av) även när URL:en till sidan kan innehålla skillnader.

Om en webbplats till exempel ska erbjuda en utskriftsvänlig version av en sida, kan en sökmotor indexera den här sidan separat från den vanliga versionen av sidan. Den kanoniska taggen anger för sökmotorn att de är samma.

Exempel:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

Båda lägger till följande tagg i sidhuvudet:

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

Värdet `href` kan vara relativt eller absolut. Koden bör inkluderas i sidmarkeringen för att fastställa sidans kanoniska URL och returnera den här taggen.

### Konfigurera dispatchern för skiftlägeskänslighet {#configuring-the-dispatcher-for-case-insensitivity}

Det bästa sättet är att skicka alla sidor med gemener. Du vill dock inte att en användare ska få en 404-siffra när han/hon kommer till webbplatsen med versaler i sin URL. Därför rekommenderar Adobe att du lägger till en omskrivningsregel i Apache HTTP Server-konfigurationen för att mappa alla inkommande URL:er till gemener. Dessutom måste skribenterna utbildas för att kunna skapa sidor med gemener.

Om du vill konfigurera Apache att tvinga all inkommande trafik till gemener lägger du till följande i `vhost` konfigurationen:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Lägg dessutom till följande längst upp i `htaccess` filen:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementera robots.txt för att skydda utvecklingsmiljöer {#implementing-robots-txt-to-protect-development-environments}

Sökmotorer *bör* kontrollera om det finns en `robots.txt` fil i webbplatsens rot innan du crawlar webbplatsen. Det bör understrykas här, för även om stora sökmotorer som Google, Yahoo och Bing alla respekterar detta, så gör inte vissa utländska sökmotorer det.

Det enklaste sättet att blockera åtkomst till hela platsen är att placera en fil med namnet `robots.txt` i platsroten med följande innehåll:

```xml
User-agent: *
Disallow: /
```

I en aktiv miljö kan du också välja att inte tillåta vissa sökvägar som du inte vill indexera.

Det kavé som uppstår när filen placeras i platsroten är att begäranden om tömning av dispatcher kan ta bort filen och URL-mappningar troligtvis placerar platsroten på en annan plats än den `robots.txt` `DOCROOT` som definieras i Apache HTTP Server-konfigurationen. Därför är det vanligt att placera den här filen på författarinstansen i platsroten och replikera den till publiceringsinstansen.

### Bygga en XML-webbplatskarta på AEM {#building-an-xml-sitemap-on-aem}

Crawler använder XML-platskartor för att bättre förstå webbplatsernas struktur. Även om det inte finns någon garanti för att en platskarta kommer att leda till förbättrad SEO-rankning är det en överenskommen bästa praxis. Du kan manuellt underhålla en XML-fil på webbservern och använda den som platskarta, men du rekommenderas att generera platskartan programmatiskt, vilket säkerställer att platskartan automatiskt återspeglar ändringarna när författare skapar nytt innehåll.

Om du vill skapa en webbplatskarta programmatiskt registrerar du en Sling Servlet som lyssnar efter ett `sitemap.xml` samtal. Servern kan sedan använda resursen som tillhandahålls via serverletens API för att titta på den aktuella sidan och dess underordnade sidor, och skriva ut XML. XML-innehållet cachelagras sedan i dispatchern. Den här platsen bör refereras i platskartegenskapen för `robots.txt` filen. Dessutom måste en anpassad justeringsregel implementeras för att säkerställa att filen rensas när en ny sida aktiveras.

>[!NOTE]
>
>Du kan registrera en Sling Servlet för att lyssna efter väljaren `sitemap` med tillägget `xml`. Detta gör att servern bearbetar begäran när som helst när en URL begärs som slutar i:
>    `/<path-to>/page.sitemap.xml`
Du kan sedan hämta den begärda resursen från begäran och generera en platskarta från den punkten i innehållsträdet med JCR-API:erna.
Fördelen med en sådan här metod är när du har flera webbplatser från samma instans. En begäran att `/content/siteA.sitemap.xml` generera en platskarta för `siteA` medan en begäran om `/content/siteB.sitemap.xml` skulle generera en platskarta `siteB` utan att behöva skriva ytterligare kod.

### Skapa 301 omdirigeringar för äldre URL:er {#creating-redirects-for-legacy-urls}

När du startar en webbplats med en ny struktur är det av två skäl viktigt att implementera och testa 301-omdirigeringar i Apache HTTP Server:

* De gamla URL:erna har byggt upp SEO-värdet över tiden. Genom att implementera en omdirigering kan sökmotorn tillämpa det här värdet på den nya URL:en.
* Användare av din webbplats kan ha skapat bokmärken på dessa sidor. Genom att implementera omdirigeringar kan du vara säker på att dirigera användaren till den sida på den nya webbplatsen som mest liknar den plats där han/hon försöker ta sig till den gamla webbplatsen.

Se till att du läser avsnittet med ytterligare resurser som följer för instruktioner om hur 301 omdirigeringar implementeras, samt ett verktyg som testar att omdirigeringarna fungerar som väntat.

## Additional Resources {#additional-resources}

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
