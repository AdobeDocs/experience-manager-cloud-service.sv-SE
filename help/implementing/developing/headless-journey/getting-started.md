---
title: Komma igång med AEM Headless som Cloud Service
description: I den här delen av AEM Headless Developer Journey kan du läsa om AEM Headless-krav.
hide: true
hidefromtoc: true
index: false
exl-id: a39877d9-f5a1-48f0-a021-cc9849bd8ecb
source-git-commit: 83ed6295d2b29581025f5410236f2618ceb59012
workflow-type: tm+mt
source-wordcount: '3087'
ht-degree: 0%

---

# Komma igång med AEM Headless som Cloud Service {#getting-started}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](overview.md) lär du dig vad som krävs för att du ska kunna komma igång med ditt eget projekt AEM Headless.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet om den AEM headless-resan [Lär dig mer om CMS Headless Development](learn-about.md) lärde du dig den grundläggande teorin om vad ett headless CMS är och du bör nu:

* Förstå de grundläggande begreppen och terminologin för leverans av headless-innehåll
* Förstå varför och när headless krävs
* Lär dig på en hög nivå hur headless-koncept används och hur de fungerar ihop

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du kan använda AEM för att implementera en headless-lösning.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå AEM Headless i ditt projekt. När du har läst bör du:

* Förstå grunderna i AEM headless-funktioner.
* Lär känna förutsättningarna för AEM headless-funktioner.
* Tänk på AEM integrationsnivåer utan motstycke.
* Du kan definiera projektet utifrån dess omfång.

## AEM Basics {#aem-basics}

Innan du kan definiera ett headless-projekt i AEM är det viktigt att du förstår några grundläggande AEM.

### Författarinstans {#author}

AEM består av en författarinstans och en [publiceringsinstans](#publish) som fungerar tillsammans för att skapa, hantera och publicera ditt innehåll.

Innehållet börjar på författarinstansen. Här skapar du innehåll för innehållsförfattare. I författarmiljön finns olika verktyg som författare kan använda för att skapa, ordna och återanvända sitt innehåll.

### Publiceringsinstans {#publish}

När innehållet har skapats i författarinstansen måste det publiceras för att vara tillgängligt för andra tjänster att använda. En publiceringsinstans innehåller allt innehåll som har publicerats.

### Replikering {#replication}

Replikering innebär att överföra innehåll från författarinstansen till publiceringsinstansen. Detta görs automatiskt av AEM när en författare eller annan användare med lämplig behörighet publicerar innehåll.

### Sammanfattning av AEM {#aem-basics-summary}

På den enklaste nivån krävs följande steg för att skapa digitala upplevelser i AEM:

1. Dina innehållsförfattare skapar ditt headless-innehåll i författarinstansen.
1. När innehållet är klart replikeras det till publiceringsinstansen.
1. API:er kan sedan anropas för att hämta det här innehållet.

AEM Headless bygger vidare på denna tekniska grund med kraftfulla verktyg för att hantera headless-innehåll, som [beskrivs i nästa avsnitt.](#aem-headless-basics)

## AEM Headless Basics {#aem-headless-basics}

De headless-funktionerna i AEM bygger på några viktiga funktioner. Dessa kommer att förklaras i detalj i senare delar av resan. Det är nu bara viktigt att veta vad de gör och vad de kallas.

### Modeller för innehållsfragment {#content-fragment-models}

Modeller för innehållsfragment definierar strukturen för data och innehåll som du skapar och hanterar i AEM. De fungerar som en sorts ställningar för ert innehåll. När du väljer att skapa innehåll väljer författarna bland de modeller för innehållsfragment som du definierar, som vägleder dem när de skapar innehåll.

### Innehållsfragment {#content-fragments}

Med Content Fragments kan du utforma, skapa, strukturera och publicera sidoberoende innehåll. Med dem kan du förbereda innehåll som är klart för användning på flera platser och i flera kanaler.

Innehållsfragment innehåller strukturerat innehåll och kan levereras i JSON-format.

### API:er för GraphQL och REST {#apis}

AEM erbjuder två kraftfulla API:er för att ändra ert innehåll utan problem.

* Med GraphQL API kan du skapa begäranden om åtkomst till och leverans av innehållsfragment.
* Med Assets REST API kan du skapa och ändra innehållsfragment (och andra resurser).

Du kommer att lära dig mer om dessa API:er och hur du använder dem i en senare del av den AEM resan utan headless. Eller se [avsnittet ](#additional-resources) om du vill ha mer information.

## Headless Integration Levels {#integration-levels}

AEM stöder både den fullständiga headless-modellen och den traditionella fullstacksmodellen eller headful-modellen i ett CMS-system. AEM erbjuder inte bara dessa två exklusiva alternativ, utan även möjligheten att stödja hybridmodeller som kombinerar fördelarna med båda, vilket ger unik flexibilitet för ditt headless-projekt.

För att du ska få en förståelse för headless-koncept fokuserar den här AEM Headless Developer Journey på den rena headless-modellen så att du kommer igång så fort som möjligt utan att behöva skriva någon kod i AEM.

Du bör dock vara medveten om de extra hybridmöjligheterna som är öppna för dig när du väl förstår AEM headless-funktioner. Vi har utformat de här fallen nedan för din kännedom. När resan är över kommer du att få en mer detaljerad introduktion till dessa koncept om en sådan flexibilitet krävs för ditt projekt.

### Du har redan en extern förbrukning av headless-innehåll som ett program på en sida (SPA). {#already-have-a-spa}

Låt oss anta att ditt grundläggande krav är åtminstone att leverera innehåll från AEM till en befintlig, extern tjänst.

#### Nivå 1: Integrering av innehållsfragment - traditionell Headless-modell {#level-1}

Den här integreringsnivån är den traditionella headless-modellen och gör det möjligt för innehållsförfattarna att skapa innehåll i AEM och leverera det helhjärtat till valfritt antal externa tjänster med GraphQL eller redigera dem från externa tjänster med Assets API. Ingen kodning krävs i AEM.

I den här modellen används AEM bara för att skapa och leverera innehåll med hjälp av AEM innehållsfragment. Återgivning och interaktion med innehållet delegeras till det uppladdande externa programmet, ofta ett ensidigt program (SPA).

#### Nivå 2: Bädda in SPA i AEM - hybridmodell {#level-2}

Den här integreringsnivån bygger på den första nivån, men tillåter även att det externa programmet (SPA) bäddas in i AEM så att innehållsförfattarna kan visa innehållet i det externa programmet i AEM. Programmet har även stöd för begränsad redigering av det externa programmet i AEM.

Den här nivån har fördelen att innehållsförfattare kan skapa innehåll på ett flexibelt sätt i AEM med sitt innehåll som presenteras i sitt sammanhang med en inbäddad extern SPA, samtidigt som innehållet levereras utan problem.

#### Nivå 3: Bädda in och aktivera SPA fullständigt i AEM - hybridmodell {#level-3}

Denna nivå av integration bygger på nivå två genom att göra det möjligt att redigera det mesta innehållet i det externa SPA i AEM.

### Du har ännu inte någon extern konsument av det Headless-innehåll som ett program med en enda sida (SPA). {#do-not-have-a-spa}

Om målet är att skapa en ny SPA som använder innehåll från AEM i bakgrunden kan du använda funktioner som Content Fragments för att hantera ditt headless-innehåll och även skapa en SPA med AEM SPA Editor-ramverket.

Med SPA Editor konsumerar SPA inte bara innehåll från AEM, utan kan även redigeras i AEM av innehållsförfattarna, vilket ger dig både flexibiliteten med headless-leverans och kontextredigering inom AEM.

## Krav och krav {#requirements-prerequisites}

Det finns ett antal krav innan du börjar AEM headless-projektet.

### Kunskap {#knowledge}

* GraphQL
* Utvecklingserfarenhet som skapar SPA med React- eller Angular-ramverk
* Grundläggande AEM att skapa innehållsfragment och använda redigeraren

### Verktyg {#tools}

* Sandlådeåtkomst för testning av driftsättning av ditt projekt
* Lokal utvecklingsinstans för datamodellering och -testning
* Befintliga externa SPA eller andra kunder av ditt AEM innehåll utan huvud

## Definiera ditt projekt {#defining-your-project}

För varje framgångsrikt projekt är det viktigt att tydligt definiera inte bara projektets krav utan även roller och ansvar.

### Omfång {#scope}

Det är mycket viktigt att ha ett tydligt definierat utrymme för projektet. Omfattningen informerar acceptanskriterier och gör det möjligt att fastställa en definition av slutfört.

Den första frågan du måste ställa dig själv är &quot;Vad försöker jag uppnå med AEM Headless?&quot; Svaret bör i allmänhet vara att du har eller kommer att ha i framtiden ett upplevelseprogram som du har skapat med dina egna utvecklingsverktyg som inte finns i kombination med AEM. Det här upplevelseprogrammet kan vara en mobilapp, en webbplats eller någon annan kundupplevelseapplikation som vänder sig till slutanvändaren. Målet med AEM Headless är att mata in ditt upplevelseprogram med innehåll som skapas, lagras och hanteras i AEM med avancerade API:er som anropar AEM Headless för att hämta innehåll eller till och med fullständigt CRUD-innehåll direkt från ditt upplevelseprogram. Om detta inte är vad du vill göra, vill du förmodligen [gå tillbaka till AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) och hitta det avsnitt som passar bättre för det du vill åstadkomma.

### Roller och ansvar {#roles-responsibilities}

Rollerna för enskilda projekt varierar, men viktiga faktorer att tänka på när det gäller innehållet i AEM headless-utveckling är:

* [Administratör](#administrator)
* [Innehållsförfattare](#content-author)
* [Content Modeler](#content-modeler)
* [Developer](#developer)

#### Administratör {#administrator}

Administratören ansvarar för systemets grundkonfiguration och konfiguration. Administratören kommer till exempel att konfigurera din organisation i användarhanteringssystemet Adobe, som hänvisas till Identity Management System (IMS). Administratören blir den första användaren i organisationen som får en e-postinbjudan från Adobe när din organisation har skapats av Adobe i IMS. Administratören kan logga in på IMS och lägga till användare från andra profiler.

När användarna har konfigurerats av administratören får de behörighet att komma åt alla AEM resurser för att utföra sitt arbete som medarbetare på att leverera upplevelseprogrammet med AEM Headless.

Administratören ska vara den användare som konfigurerar AEM och förbereder körningsmiljön så att [innehållsförfattare](#content-author) kan skapa och uppdatera innehåll, och [utvecklare](#developer) kan använda API:er som hämtar eller ändrar innehåll för sina upplevelseprogram.

#### Innehållsförfattare {#content-author}

Innehållsförfattare skapar och hanterar innehåll som levereras utan problem av AEM. Innehållsförfattare använder AEM funktioner som Content Fragments och Assets Console för att hantera sitt innehåll.

Innehållsförfattare bör ha följande i åtanke:

#### Plan för lokalisering {#localization}

Planera för översättning och lokalisering i början av projektet. Överväg&quot;Internationalization Project Manager&quot; som en separat person vars ansvar är att definiera vilket innehåll som ska översättas och vad som inte ska översättas och vilket översatt innehåll som ska kunna ändras av regionala eller lokala innehållsproducenter.

Skapa en plan för vilken innehållslokalisering du behöver.

* Behöver ni bara olika språk eller språk för att anpassa er till regionala särdrag?
* Behöver multimediematerial som bilder och videor vara olika för olika språkområden?

Var tydlig med ditt arbetsflöde för innehållsuppdatering. Vilken godkännandeprocess behöver systemet stödja? Kan AEM arbetsflöden utnyttjas för att automatisera denna process?

Observera att din [innehållshierarki](#content-hierarchy) kan utnyttjas för att underlätta lokaliseringen.

Mer information om AEM arbetsflöden och lokaliseringsverktyg finns i avsnittet [ytterligare resurser](#additional-resources).

##### Utnyttja innehållshierarkin {#content-hierarchy}

Mapphierarkin kan hantera två viktiga problem när det gäller innehållshantering:

* [Lokalisering](#localization)  - AEM hanterar lokalisering av innehåll genom att behålla kopior av innehåll i språkspecifika mappar.
* Organisation - Mappar används för att definiera en innehållshierarki som krävs för lokaliseringsbehov och för att logiskt hantera innehållsfragment.

AEM ger en mycket flexibel innehållsstruktur och en hierarki kan vara godtyckligt stor. Det är dock viktigt att komma ihåg att alla ändringar i mappstrukturen kan få oönskade konsekvenser för befintliga frågor som [är beroende av innehållssökvägen.](#developer) En väldefinierad hierarki som är tydligt angiven i förväg kan därför vara mycket användbar för era innehållsförfattare.

Mappar kan även begränsas till att endast tillåta vissa typer av innehåll (baserat på modeller för innehållsfragment). Det rekommenderas i allmänhet att du alltid uttryckligen anger vilka modeller som tillåts för alla mappar i hierarkin. Ange tillåtet innehåll för en viss mapp:

* Förhindrar att innehållsförfattare skapar innehåll som inte tillhör mappen.
* Optimerar processen för att skapa innehåll genom att filtrera de innehållstyper som tillåts i mappen under skapandet så att endast giltiga typer av innehåll visas.

Genom att skapa en lämplig innehållsstruktur blir det enklare att samordna redigering av headless-innehåll i olika kanaler för att maximera återanvändningen av innehållet. Genom att utnyttja innehåll i flera kanaler blir innehållsproduktionen effektivare och ändringshanteringen effektivare.

##### Upprätta praktiska namnkonventioner {#naming-conventions}

Namn på innehållsfragment måste vara beskrivande för innehållsförfattare. AEM hanterar på ett genomskinligt sätt flytning och/eller trunkering av de namn som används i ID:n på databasnivå. Därför bör de logiska namn som tillhandahålls av innehållsförfattarna alltid vara läsbara och representera innehållet.

* Felaktigt namn: `cta_btn_1`
* Bra namn: `Call To Action Button`

I avsnittet [ytterligare resurser](#additional-resources) finns mer information om namnkonventioner AEM sidor.

##### Öka inte innehållets kapsling {#content-nesting}

[Innehållsfragmenteranvänds ](#content-fragments) i AEM för att skapa innehåll utan rubrik. AEM har stöd för upp till tio nivåer av innehållkapsling för innehållsfragment. Det är dock viktigt att komma ihåg att AEM måste tolka varje referens som definieras i det överordnade innehållsfragmentet iterativt och sedan kontrollera om det finns några underordnade referenser i alla jämställda. De här åtgärderna kan snabbt bli ett prestandaproblem.

Som en allmän tumregel får inte Content Fragment-referenser kapslas över fem nivåer.

#### Innehållsmodelleraren {#content-modeler}

Innehållsmodellerarna analyserar kraven för de data som behöver levereras utan problem och definierar strukturen för dessa data. Dessa strukturer kallas [Content Fragment Models](#content-fragment-models) i AEM. Modeller för innehållsfragment används som bas för de innehållsfragment som innehållsförfattarna skapar.

Ett användbart sätt att definiera modeller för innehållsfragment är att skapa modeller som mappar till UX-komponenterna i de program som ska använda innehållet.

Eftersom innehållsförfattarna interagerar med modellerna kontinuerligt när de skapar nytt innehåll kan man genom att anpassa modellerna till användargränssnittet visualisera den digitala upplevelsen. Om du går ett steg längre kan du tilldela ikoner till de modeller för innehållsfragment som representerar UX-elementet så att författarna intuitivt kan välja rätt modell baserat på visuella tecken.

#### Utvecklare {#developer}

Utvecklarna ansvarar för att sammanfoga det material som skapas direkt AEM till konsumenten, som ofta kan vara ett ensidigt program (SPA), ett progressivt webbprogram (PWA), en webbshop eller en annan tjänst som inte är AEM.

GraphQL fungerar som ett&quot;glimt&quot; mellan AEM och konsumenterna av headless-innehåll. GraphQL är det språk som AEM efter nödvändigt innehåll.

Utvecklare bör tänka på några grundläggande rekommendationer när de planerar sina frågor:

* Frågor ska inte förlita sig på en fast sökväg (`ByPath`) för att hämta innehållsfragment.
   * [Innehållsförfattare har fullständig kontroll över ](#content-hierarchy) innehållsfragmenthierarkin och kan göra ändringar som skulle bryta en sådan fråga.
   * Frågor ska i stället välja om innehållsfragmentmodellreferenser med dynamiska frågeparametrar ska filtrera resultaten för att generera önskad nyttolast.
* Använd alltid beständiga frågor i AEM för bästa frågeprestanda. Dessa diskuteras senare under resan.
* GraphQL är utformat för att vara deklarativ enligt motto&quot;Fråga efter exakt det du behöver och få exakt det&quot;. Det innebär att du alltid undviker `select *`-typfrågor som du kan skapa i en relationsdatabas när du skapar GraphQL-frågor.

För en [vanlig headless-implementering med AEM](#level-1) behöver utvecklaren ingen kodkunskap om AEM.

### Prestandakrav {#performance-requirements}

För att ett projekt ska lyckas måste prestanda beaktas innan något innehåll skapas.

Ni måste förstå era kunders/besökares förväntningar och design för dem. Ange servicenivåmål (SLO) och mät dem för att förstå om du uppfyller användarens förväntningar.

#### Trafikmönster {#traffic-patterns}

Att förstå trafik- och trafikmönster börjar med att samla det ni vet från det förflutna och sedan projicera till den förväntade tillväxten under de närmaste åren. Några av de viktigaste variablerna att tänka på:

* Hur många API-anrop per timme/dag/månad förväntar du dig och finns det risk för kryddor och säsongsvariation?
* Hur många olika innehållsförfattare finns det?
* Hur många innehållsförfattare tror du kommer att arbeta samtidigt?
* Hur ofta uppdateras innehållet?
* Hur många innehållsmodeller behövs?
* Hur många förekomster av modeller behövs?

#### Uppdateringsfrekvens {#update-frequency}

Oftast har olika avsnitt av upplevelser olika frekvens för innehållsuppdateringar. Det är viktigt att du förstår detta för att kunna finjustera CDN och cachekonfigurationer. Detta är också viktigt för [innehållsmodellerarna](#content-modeler) när de utformar modeller för ditt innehåll. Fundera:

* Måste vissa typer av innehåll förfalla efter en viss period?
* Finns det element som är användarspecifika och därför inte kan cachas?

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey ska du:

* Förstå grunderna i AEM headless-funktioner.
* Lär känna förutsättningarna för AEM headless-funktioner.
* Tänk på AEM integrationsnivåer utan motstycke.
* Du kan definiera projektet utifrån dess omfång.

Du bör fortsätta din AEM resa utan att ta hjälp av rubriker nästa gång du granskar dokumentet [Vägen till din första upplevelse med AEM Headless](path-to-first-experience.md) där du får lära dig hur du ställer in nödvändiga verktyg och hur du börjar fundera på att modellera data i AEM.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-utvecklingsresan genom att granska dokumentet [Vägen till din första upplevelse med AEM Headless,](path-to-first-experience.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta den headless-resan.

* [An Introduction to the Architecture of Adobe Experience Manager as a Cloud Service](/help/core-concepts/architecture.md)  - Understanding AEM as a Cloud Services structure
* [AEM Headless Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  - Använd dessa praktiska självstudiekurser för att utforska hur du kan använda de olika alternativen för att leverera innehåll till headless endpoints med AEM och välja vad som är rätt för dig.
* [Headless Content Management Using GraphQL APIs](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - Följ den här kursen för en översikt över GraphQL API som implementerats i AEM. Autentisering via AdobeID krävs.
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  - Det här GitHub-projektet innehåller exempelprogram som AEM GraphQL API:er.
* [Authoring Concepts](/help/sites-cloud/authoring/getting-started/concepts.md)  - Teknisk dokumentation för redigeringsmiljön i AEM inklusive information om författarpubliceringskonfigurationen
* [Publicera sidor](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) - Teknisk dokumentation för publicering av innehåll på AEM
* [Namngivningskonventioner](/help/implementing/developing/introduction/naming-conventions.md)  - Teknisk dokumentation av namngivningsbegränsningar i AEM
* [Multi Site Manager och Translation](/help/sites-cloud/administering/msm-and-translation.md)  - Teknisk dokumentation om AEM kraftfulla översättningsfunktioner
* [AEM arbetsflöden](/help/sites-cloud/authoring/workflows/overview.md)  - Teknisk dokumentation om hur du automatiserar arbetsflöden i AEM
* [Content Fragments](/help/assets/content-fragments/content-fragments.md)  - Technical documentation for Content Fragments.
* [Modeller](/help/assets/content-fragments/content-fragments-models.md)  för innehållsfragment - teknisk dokumentation för modeller av innehållsfragment.
* [GraphQL Technical Documentation](https://graphql.org)  - GraphQL-definitionen (extern länk)
* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) - Teknisk dokumentation som förklarar hur du skapar begäranden om åtkomst och leverans av innehållsfragment
* [Resurser REST API](/help/assets/content-fragments/assets-api-content-fragments.md)  - Teknisk dokumentation som förklarar hur du skapar och ändrar innehållsfragment (och andra resurser)
* [Beständiga frågor](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching)  - Teknisk dokumentation om beständiga frågor i AEM
* [Headless and Headless in AEM](/help/implementing/developing/headful-headless.md) - A complete describing the headless integration levels available in AEM
