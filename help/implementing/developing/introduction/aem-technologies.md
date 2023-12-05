---
title: AEM Technical Foundations
description: En översikt över den tekniska grunden för AEM, inklusive hur AEM är strukturerad och grundläggande tekniker som JCR, Sling och OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '2130'
ht-degree: 0%

---

# AEM Technical Foundations {#aem-technical-foundations}

AEM är en stabil plattform som bygger på beprövade, skalbara och flexibla tekniker. Det här dokumentet ger en detaljerad översikt över de olika delar som AEM består av och är avsett som ett tekniskt tillägg för en AEM som utvecklar en hel hög. Den är inte avsedd som en guide för att komma igång. Om du inte är van vid att AEM utveckling, se [Getting Started Developing AEM Sites - WKND Tutorial](develop-wknd-tutorial.md) som ett första steg.

>[!TIP]
>
>Innan du tar dig in i AEM kärnteknik rekommenderar Adobe att du slutför [Getting Started Developing AEM Sites - WKND Tutorial.](develop-wknd-tutorial.md)

## Grundläggande {#fundamentals}

Som ett modernt innehållshanteringssystem bygger AEM på standardwebbtekniker:

* Request-response-cykeln (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

Det underliggande lagret för innehåll och affärslogik bygger på Java™-teknologier:

* JCR
* Sling
* OSGi

## Java™ Content Repository {#java-content-repository}

Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), anger ett leverantörsoberoende och implementeringsoberoende sätt att få åtkomst till innehåll dubbelriktat på en detaljnivå i en innehållsdatabas. Specifikationsledaren innehas av Adobe Research (Schweiz) AG.

The [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) paket, `javax.jcr.*` används för direkt åtkomst och hantering av databasinnehåll.

AEM bygger på en JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/) är en implementering av ett skalbart och högpresterande hierarkiskt innehållslager som kan användas som grund för moderna webbplatser i världsklass och andra krävande innehållsprogram, som uppfyller JCR-standarden.

Jackrabbit Oak (även kallad Oak) är implementeringen av den JCR-standard som AEM bygger på.

## Bearbetning av försäljningsbegäran {#sling-request-processing}

AEM byggs med [Sling](https://sling.apache.org/index.html), ett ramverk för webbapplikationer som bygger på REST-principer och som enkelt utvecklar innehållsorienterade applikationer. Sling använder en JCR-databas, som Apache Jackrabbit Oak, som datalager. Sling har bidragit till Apache Software Foundation - mer information finns på Apache.

### Introduktion till Sling {#introduction-to-sling}

Med Sling är den typ av innehåll som ska återges inte den första bearbetningen. Det viktigaste är i stället om URL:en tolkas till ett innehållsobjekt för vilket ett skript sedan kan hittas för att utföra återgivningen. Den här processen ger utmärkt stöd för webbinnehållsförfattare att skapa sidor som enkelt kan anpassas efter deras behov.

Fördelarna med den här flexibiliteten är uppenbara i program med många olika innehållselement eller när du behöver sidor som enkelt kan anpassas. Detta gäller särskilt när man implementerar ett system för hantering av webbinnehåll, t.ex. AEM.

Se [Sling på 15 minuter](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) för de första stegen för att utveckla med Sling.

I följande diagram förklaras Sling-skriptupplösningen. Den visar hur du hämtar från HTTP-begäran till innehållsnoden, från innehållsnod till resurstyp, från resurstyp till skript och vilka skriptvariabler som är tillgängliga.

![Om Apache Sling-skriptupplösningen](assets/sling-cheatsheet-01.png)

I följande diagram förklaras de dolda, men kraftfulla, frågeparametrarna som du kan använda med `SlingPostServlet`, standardhanteraren för alla POSTER. Hanteraren ger dig oändliga alternativ för att skapa, ändra, ta bort, kopiera och flytta noder i databasen.

![Använda SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling är innehållscentrerat {#sling-is-content-centric}

Sling är *innehållscentrerad*. Det innebär att bearbetningen är inriktad på innehållet eftersom varje HTTP-begäran mappas till innehåll i form av en JCR-resurs (en databasnod):

* Det första målet är den resurs (JCR-nod) som innehåller innehållet
* För det andra finns representationen, eller skriptet, från resursegenskaperna med vissa delar av begäran (till exempel väljare och/eller tillägg)

### RESTful Sling {#restful-sling}

På grund av sin innehållsorienterade filosofi implementerar Sling en REST-orienterad server och har därmed ett nytt koncept i ramverk för webbapplikationer. Fördelarna är:

* RESTful, inte bara på ytan; resurser och representationer är korrekt modellerade inuti servern
* Tar bort en eller flera datamodeller
   * Andra content management-ramverk kan kräva URL-struktur, affärsobjekt och DB-schema för att komma åt en resurs.
   * Sling förminskar det till: URL = resource = JCR-struktur

### URL-disposition {#url-decomposition}

Vid Sling styrs bearbetningen av URL:en för användarförfrågningen. Den definierar det innehåll som ska visas med lämpliga skript och information extraheras från URL:en.

Analyserar följande URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Du kan dela upp den i dess sammansatta delar:

| protocol | värd |  | innehållsbana | väljare | extension |  | suffix |  | parametrar |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocol** - HTTPS
* **värd** - Webbplatsens domän
* **innehållsbana** - Sökväg som anger det innehåll som ska återges och som används med tillägget. I det här exemplet innebär det att `tools/spy.html`
* **väljare** - Används för alternativa metoder för återgivning av innehållet. I det här exemplet används en utskriftsvänlig version i A4-format
* **extension** - Innehållsformat; anger även vilket skript som ska användas för återgivning
* **suffix** - Kan användas för att ange ytterligare information
* **parametrar** - Alla parametrar som krävs för dynamiskt innehåll

#### Från URL till innehåll och skript {#from-url-to-content-and-scripts}

Använda principerna för URL-nedbrytning:

* Mappningen använder innehållssökvägen som extraherats från begäran för att hitta resursen.
* När rätt resurs hittas extraheras sling-resurstypen och används för att hitta skriptet som ska användas för återgivning av innehållet.

Följande bild visar vilken mekanism som används, vilket beskrivs mer ingående i följande avsnitt.

![URL-mappningsmekanism](assets/url-mapping.png)

Med Sling anger du vilket skript som ska återge en viss enhet (genom att ange `sling:resourceType` i JCR-noden). Den här mekanismen ger mer frihet än en där skriptet får åtkomst till datatabellerna (som en SQL-sats i ett PHP-skript skulle göra) eftersom en resurs kan ha flera renderingar.

#### Mappa begäranden till resurser {#mapping-requests-to-resources}

Begäran är uppdelad och nödvändig information extraheras. Databasen genomsöks efter den begärda resursen (innehållsnod):

* First Sling kontrollerar om det finns en nod på den plats som anges i begäran, till exempel `../content/corporate/jobs/developer.html`
* Om ingen nod hittas tas tillägget bort och sökningen upprepas, till exempel `../content/corporate/jobs/developer`
* Om ingen nod hittas returnerar Sling http-koden 404 (Hittades inte).

Med Sling kan även andra saker än JCR-noder vara resurser, men den här funktionen är en avancerad funktion.

### Hitta skriptet {#locating-the-script}

När rätt resurs (innehållsnod) finns, **slingresurstyp** extraheras. Den här sökvägen hittar det skript som ska användas för återgivning av innehållet.

Sökvägen som anges av `sling:resourceType` kan antingen vara:

* Absolut
* Relativt till en konfigurationsparameter

>[!TIP]
>
>Relativa sökvägar rekommenderas av Adobe när de ökar portabiliteten.

Alla Sling-skript lagras i undermappar till båda `/apps` (mutable, user scripts) eller `/libs` (ej ändringsbart, systemskript), som söks igenom i den här ordningen.

Några andra punkter att notera är:

* När metoden (GET, POST) krävs, anges den med versaler som enligt HTTP-specifikationen, till exempel `jobs.POST.esp`
* Olika skriptmotorer stöds, men de vanliga, rekommenderade skripten är HTML och JavaScript.

Listan över skriptmotorer som stöds av den angivna AEM finns på Felix Management Console ( `http://<host>:<port>/system/console/slingscripting`).

Använda föregående exempel om `sling:resourceType` är `hr/jobs` sedan för:

* GET/HEAD och URL:er som slutar på `.html` (standardtyper för begäran, standardformat)
   * Skriptet är `/apps/hr/jobs/jobs.esp`; sista delen av `sling:resourceType` används för att ange filnamnet.
* Begäranden om POST (alla begärandetyper utom GET/HEAD, metodnamnet måste vara versaler)
   * POST används i skriptnamnet.
   * Skriptet är `/apps/hr/jobs/jobs.POST.esp`.
* URL-adresser i andra format, slutar inte med `.html`
   * Exempel: `../content/corporate/jobs/developer.pdf`
   * Skriptet är `/apps/hr/jobs/jobs.pdf.esp`; suffixet läggs till i skriptnamnet.
* URL:er med väljare
   * Väljare kan användas för att visa samma innehåll i ett alternativt format. Till exempel en utskriftsvänlig version, ett RSS-flöde eller en sammanfattning.
   * Om du tittar på en utskriftsvänlig version där väljaren kan vara `print`; som i `../content/corporate/jobs/developer.print.html`
   * Skriptet är `/apps/hr/jobs/jobs.print.esp`; väljaren läggs till i skriptnamnet.
* Om nej, `sling:resourceType` definieras sedan:
   * Innehållssökvägen används för att söka efter ett lämpligt skript (om den sökvägsbaserade `ResourceTypeProvider` är aktivt).
   * Skriptet för `../content/corporate/jobs/developer.html` skulle generera en sökning i `/apps/content/corporate/jobs/`.
   * Den primära nodtypen används.
* Om inget skript hittas alls används standardskriptet.
   * Standardåtergivningen stöds som oformaterad text (`.txt`), HTML (`.html`) och JSON (`.json`), som alla innehåller en lista med nodens egenskaper (lämpligt formaterade). Standardåtergivningen för tillägget `.res`, eller begäranden utan ett tillägg till en begäran, är att resursen (där det är möjligt) ska tas bort.
* För http-felhantering (kod 403 eller 404) söker Sling efter ett skript på antingen:
   * Platsen `/apps/sling/servlet/errorhandler` för anpassade skript
   * Eller platsen för standardskriptet `/libs/sling/servlet/errorhandler/404.jsp`

Om flera skript gäller för en viss begäran väljs det skript som matchar bäst. Ju mer specifik en matchning är, desto bättre blir den; med andra ord matchar väljaren bättre, oavsett vilket tillägg eller metodnamn som används i begäran.

Ta till exempel en begäran om åtkomst till resursen

* `/content/corporate/jobs/developer.print.a4.html`

Av typ

* `sling:resourceType="hr/jobs"`

Anta att du har följande lista med skript på rätt plats:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Sedan är ordningen (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Förutom resurstyperna (definieras primärt av `sling:resourceType` ) finns också resursens supertyp. Den här typen anges av `sling:resourceSuperType` -egenskap. De här supertyperna beaktas också när du försöker hitta ett skript. Fördelen med resurssupertyper är att de kan utgöra en hierarki av resurser där standardresurstypen är `sling/servlet/default` (används av standardservletarna) är roten.

Resursens överordnade typ kan definieras på två sätt:

* av `sling:resourceSuperType` resursens egenskap.
* av `sling:resourceSuperType` egenskapen för noden som `sling:resourceType` punkter.

Till exempel:

* `/`
   * `a`
   * `b`
      * `sling:resourceSuperType = a`
   * `c`
      * `sling:resourceSuperType = b`
   * `x`
      * `sling:resourceType = c`
   * `y`
      * `sling:resourceType = c`
      * `sling:resourceSuperType = a`

Typhierarkin för:

* `/x`
   * Är `[ c, b, a, <default>]`
* Med `/y`
   * Hierarkin är `[ c, a, <default>]`

Orsaken är att `/y` har `sling:resourceSuperType` egendom, medan `/x` inte och dess supertyp tas därför från sin resurstyp.

#### Sling Scripts kan inte anropas direkt {#sling-scripts-cannot-be-called-directly}

I Sling kan skript inte anropas direkt eftersom det skulle bryta det strikta begreppet med en REST-server. Du skulle blanda resurser och representationer.

Om du anropar representationen (skriptet) direkt döljer du resursen i skriptet, så att ramverket (Sling) inte längre vet om det. Därför förlorar du vissa funktioner:

* Automatisk hantering av andra http-metoder än GET, inklusive:
   * POST, PUT, DELETE som hanteras med en Sing-standardimplementering
   * The `POST.jsp` skript `sling:resourceType` plats
* Kodarkitekturen är inte längre så ren eller så tydligt strukturerad som den ska vara; av största vikt för storskalig utveckling

### Sling API {#sling-api}

Använder Sling API-paketet, `org.apache.sling.*`och taggbibliotek.

### referera till befintliga element med sling:include {#referencing-existing-elements-using-sling-include}

En sista sak är behovet av att referera till befintliga element i skripten.

Mer komplicerade skript (sammanfoga skript) har åtkomst till flera resurser (t.ex. navigering, sidospalt, sidfot, element i en lista) och gör det genom att inkludera *resurs*.

I det här fallet kan du använda `sling:include("/<path>/<resource>")` -kommando. Den innehåller effektivt definitionen av den refererade resursen.

## OSGi {#osgi}

OSGi (Open Services Gateway Initiative) definierar en arkitektur för utveckling och driftsättning av modulära program och bibliotek (kallas även Dynamic Module System för Java™). Med OSGi-behållare kan du dela in programmet i enskilda moduler (är jar-filer med ytterligare metainformation och kallas buntar i OSGi-terminologi) och hantera korsberoenden mellan dem med:

* Tjänster som implementeras i behållaren
* Ett kontrakt mellan behållaren och programmet

Dessa tjänster och kontrakt utgör en arkitektur som gör att enskilda element dynamiskt kan identifiera varandra för samarbete.

Ett OSGi-ramverk ger dig dynamisk inläsning/borttagning, konfiguration och kontroll av dessa paket - utan att du behöver starta om.

>[!NOTE]
>
>Fullständig information om OSGi-teknik finns på [OSGi-webbplats](https://www.osgi.org).
>
>På sidan Grundläggande utbildning finns en samling presentationer och självstudiekurser.

Med den här arkitekturen kan du utöka Sling med programspecifika moduler. Sling, och därmed AEM, använder [Apache Felix](https://felix.apache.org/documentation/index.html) implementering av OSGi. De är båda samlingar av OSGi-paket som körs i ett OSGi-ramverk.

Med den här funktionen kan du utföra följande åtgärder på alla paket i installationen:

* Installera
* Starta
* Stoppa
* Uppdatera
* Avinstallera
* Se den senaste statusen
* Mer information om specifika paket, till exempel symboliskt namn, version och plats

Se [Konfigurera OSGi för AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) för mer information.

## Struktur i databasen {#structure-within-the-repository}

I följande lista visas en översikt över strukturen som du ser i databasen.

* `/apps` - Programrelaterade; innehåller komponentdefinitioner som är specifika för din webbplats. Komponenterna som du utvecklar kan baseras på de färdiga komponenterna som finns på `/libs/core/wcm/components`.
* `/content` - Innehåll som skapats för din webbplats.
* `/etc`
* `/home` - Användar- och gruppinformation.
* `/libs` - Bibliotek och definitioner som hör till kärnan i AEM. Undermapparna i `/libs` som representerar de färdiga AEM. Innehållet i `/libs` får inte ändras. Funktioner som är specifika för din webbplats bör göras under `/apps`.
* `/tmp` - Tillfälligt arbetsområde.
* `/var` - Filer som ändras och uppdateras av systemet, till exempel granskningsloggar, statistik, händelsehantering.

>[!CAUTION]
>
>Den här strukturen, eller de filer som finns i den, bör ändras med försiktighet. Se till att du är helt medveten om konsekvenserna av de ändringar du gör.
>
>Ändra ingenting i dialogrutan `/libs` bana. Kopiera objektet från för konfiguration och andra ändringar `/libs` till `/apps` och göra ändringar i `/apps`.
