---
title: Så här modellerar du innehåll
description: I den här delen av AEM Headless Developer Journey lär du dig att modellera ditt innehåll för AEM Headless-leverans med hjälp av Content Modeling med Content Fragment Models och Content Fragments.
exl-id: f052183d-18fd-4615-a81e-e45db5928fc1
source-git-commit: e592dd7a3a717259493f23943933fe3d0e71b7ab
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 0%

---

# Så här modellerar du innehåll {#model-your-content}

I den här delen av [AEM Headless Developer Journey](overview.md)kan du lära dig att modellera innehållsstrukturen. Förverkliga sedan strukturen för Adobe Experience Manager (AEM) med Content Fragments Models och Content Fragments, för återanvändning i alla kanaler.

## Story hittills {#story-so-far}

I början [Läs om CMS Headless Development](learn-about.md) innehållsleverans utan extra kostnad och varför den ska användas. Sedan [Komma igång med AEM Headless as a Cloud Service](getting-started.md) beskrivs AEM Headless i ditt eget projekt.

I det föregående dokumentet om den AEM resan utan headless [Vägen till din första upplevelse med AEM utan headless](path-to-first-experience.md)lärde du dig sedan de steg som krävs för att implementera det första projektet. Efter att ha läst den bör du:

* Förstå viktiga planeringsöverväganden vid utformningen av ditt innehåll
* Förstå stegen för att implementera headless beroende på vilka krav ni har på integreringsnivån.
* Konfigurera de verktyg och AEM som behövs.
* Lär dig de bästa sätten att göra den enkla resan smidig, hålla innehållsgenereringen effektiv och se till att innehållet levereras snabbt.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du förbereder ett eget AEM headless-projekt.

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Syfte**: Lär dig hur du modellerar innehållsstrukturen och inser sedan den strukturen med AEM Content Fragment Models och Content Fragments:
   * Lägg in koncept och terminologi för data-/innehållsmodellering.
   * Lär dig varför innehållsmodellering behövs för leverans av Headless-innehåll.
   * Lär dig hur du realiserar den här strukturen med AEM Content Fragment Models (och skapar innehåll med Content Fragments).
   * Lär dig modellera ditt innehåll. principer med grundläggande urval.

>[!NOTE]
>
>Datamodellering är ett mycket stort fält, eftersom det används vid utveckling av relationsdatabaser. Det finns många böcker och onlinekällor med information tillgängliga.
>
>Vi kommer endast att ta hänsyn till de aspekter som är intressanta när vi modellerar data för användning med AEM Headless.

## Innehållsmodellering {#content-modeling}

*Det är en stor, dålig värld där ute*.

Kanske inte, men det är verkligen en stor ***komplicerad*** världen där ute och datamodellering används för att definiera en förenklad representation av ett mycket (mycket) litet underavsnitt, med hjälp av den specifika information som behövs för ett visst ändamål.

>[!NOTE]
>
>När AEM behandlar innehåll, talar vi om datamodellering som innehållsmodellering.

Till exempel:

Det finns många skolor, men de har alla olika saker gemensamt:

* En plats
* Huvudlärare
* Många lärare
* Många icke undervisande personal
* Många elever
* Många före detta lärare
* Många före detta elever
* Många klassrum
* Många (många) böcker
* Många (många) utrustningsdelar
* Många aktiviteter utanför kurserna
* och så vidare....

Även i ett sådant litet exempel kan listan verka oändlig. Men om du bara vill att programmet ska utföra en enkel uppgift måste du begränsa informationen till de viktigaste uppgifterna.

Exempel: annonsera specialevent för alla skolor i området:

* Skolans namn
* Skolans plats
* Huvudlärare
* Typ av händelse
* Händelsedatum
* Lärare som organiserar evenemanget

### Concepts {#concepts}

Vad du vill beskriva kallas för **Enheter** - det som vi vill lagra information om.

Informationen som vi vill lagra om dem är **Attribut** (egenskaper), t.ex. namn, och lärarkvalifikationer.

Sedan finns det olika **Relationer** mellan enheterna. Till exempel har en skola bara en huvudlärare, och många lärare (och vanligtvis är huvudläraren också lärare).

Processen att analysera och definiera informationen, tillsammans med relationerna mellan dem, kallas **Innehållsmodellering**.

### Grunderna {#basics}

Du behöver ofta börja med att skapa en **Konceptuellt schema** som beskriver enheterna och deras relationer. Vanligtvis är detta en hög nivå (konceptuell).

När detta är stabilt kan du omvandla modellerna till en **Logiskt schema** som beskriver enheterna, tillsammans med attributen, och relationerna. På den här nivån bör du noggrant granska definitionerna för att undvika duplicering och optimera designen.

>[!NOTE]
>
>Ibland sammanfogas dessa två steg, ofta beroende på hur komplicerat ditt scenario är.

Behöver du till exempel separata enheter för `Head Teacher` och `Teacher`eller bara ytterligare ett attribut på `Teacher` modell?

### Säkerställer dataintegritet {#data-integrity}

Dataintegritet krävs för att garantera innehållets exakthet och enhetlighet under hela dess livscykel. Detta innefattar att säkerställa att innehållsförfattare enkelt kan förstå vad de ska lagra var - så följande är viktiga:

* en tydlig struktur
* en struktur som är så kortfattad som möjligt (utan att offra noggrannheten)
* validering av enskilda fält
* vid behov begränsa innehållet i specifika fält till vad som är meningsfullt

### Eliminera redundans {#data-redundancy}

Dataredundans inträffar när samma information lagras två gånger i innehållsstrukturen. Detta bör undvikas eftersom det kan leda till missförstånd när innehållet skapas och fel vid frågor. för att inte tala om missbruk av lagringsutrymme.

### Optimering och prestanda {#optimization-and-performance}

Genom att optimera strukturen kan du förbättra prestandan, både när det gäller att skapa innehåll och fråga.

Allt är en balansakt, men att skapa en struktur som är för komplex, eller som har för många nivåer, kan:

* Var förvirrande för författare som skapar innehållet.

* Påverka prestandan allvarligt om frågan måste få åtkomst till flera kapslade (refererade) innehållsfragment för att hämta nödvändigt innehåll.

## Innehållsmodellering för AEM Headless {#content-modeling-for-aem-headless}

Datamodellering är en uppsättning etablerade tekniker som ofta används vid utvecklade relationsdatabaser, så vad innebär innehållsmodellering för AEM Headless?

### Varför? {#why}

För att ditt program ska kunna begära och ta emot nödvändigt innehåll från AEM på ett konsekvent och effektivt sätt måste det här innehållet struktureras.

Detta innebär att din ansökan i förväg vet vilken form av svar det är och därför hur den ska behandlas. Detta är mycket enklare än att ta emot frihandsinnehåll, som måste analyseras för att avgöra vad det innehåller och därför hur det kan användas.

### Introduktion till Hur? {#how}

AEM använder Content Fragments för att tillhandahålla de strukturer som behövs för Headless-leverans av ditt innehåll till dina program.

Innehållsmodellens struktur är:

* som realiseras av definitionen av din innehållsfragmentmodell,
* används som bas för de innehållsfragment som används för att generera innehåll.

>[!NOTE]
>
>Modellerna för innehållsfragment används också som bas för AEM GraphQL-scheman, som används för att hämta ditt innehåll - mer om det i en senare session.

Begäranden om ditt innehåll görs med AEM GraphQL API, en anpassad implementering av standard-API:t GraphQL. Med AEM GraphQL API kan du utföra (komplexa) frågor på dina innehållsfragment, där varje fråga anpassas efter en viss modelltyp.

Det returnerade innehållet kan sedan användas av dina program.

## Skapa strukturen med Content Fragment Models {#create-structure-content-fragment-models}

I Content Fragment Models finns olika mekanismer som gör att du kan definiera innehållets struktur.

En innehållsfragmentmodell beskriver en enhet.

>[!NOTE]
>Du måste aktivera funktionen för innehållsfragment i konfigurationsläsaren så att du kan skapa nya modeller.

>[!TIP]
>
>Modellen bör namnges så att innehållsförfattaren vet vilken modell som ska väljas när ett innehållsfragment skapas.

Inom en modell:

1. **Datatyper** gör att du kan definiera de enskilda attributen.
Definiera till exempel fältet som innehåller en lärares namn som **Text** och deras tjänsteår som **Nummer**.
1. Datatyperna **Innehållsreferens** och **Fragmentreferens** gör att du kan skapa relationer till annat innehåll i AEM.
1. The **Fragmentreferens** datatypen gör att du kan realisera flera strukturnivåer genom att kapsla dina innehållsfragment (enligt modelltypen). Detta är viktigt för er innehållsmodellering.

Till exempel:
![Innehållsmodellering med innehållsfragment](assets/headless-modeling-01.png "Innehållsmodellering med innehållsfragment")

### Datatyper {#data-types}

AEM innehåller följande datatyper som du kan använda för att modellera ditt innehåll:

* Enkelradig text
* Flerradstext
* Siffra
* Boolesk
* Datum och tid
* Uppräkning
* Taggar
* Innehållsreferens
* Fragmentreferens
* JSON-objekt

### Referenser och kapslat innehåll {#references-nested-content}

Två datatyper ger referenser till innehåll utanför ett visst fragment:

* **Innehållsreferens**
Detta ger en enkel referens till annat innehåll av valfri typ.
Du kan till exempel referera till en bild på en viss plats.

* **Fragmentreferens**
Detta innehåller referenser till andra innehållsfragment.
Den här typen av referens används för att skapa kapslat innehåll, vilket introducerar de relationer som behövs för att modellera innehållet.
Datatypen kan konfigureras så att fragmentförfattare kan:
   * Redigera det refererade fragmentet direkt.
   * Skapa ett nytt innehållsfragment, baserat på lämplig modell

### Skapa modeller för innehållsfragment {#creating-content-fragment-models}

Först måste du aktivera Content Fragment Models för platsen. Detta görs i Configuration Browser. under Verktyg -> Allmänt -> Konfigurationsläsaren. Du kan antingen välja att konfigurera den globala posten eller skapa en ny konfiguration. Till exempel:

![Definiera konfiguration](assets/cfm-configuration.png)

>[!NOTE]
>
>Se Ytterligare resurser - Innehållsfragment i Configuration Browser

Sedan kan du skapa modellerna för innehållsfragment och definiera strukturen. Detta kan du göra under Verktyg -> Resurser -> Modeller för innehållsfragment. Till exempel:

![Content Fragment Model](assets/cfm-model.png)

>[!NOTE]
>
>Se Ytterligare resurser - modeller för innehållsfragment.

## Använda modellen för att skapa innehåll med innehållsfragment {#use-content-to-author-content}

Innehållsfragment baseras alltid på en innehållsfragmentmodell. Modellen innehåller strukturen, fragmentet innehåller innehållet.

### Välja lämplig modell {#select-model}

Det första steget till att skapa innehåll är att skapa ett innehållsfragment. Detta görs med Skapa -> Innehållsfragment i den obligatoriska mappen under Resurser -> Filer. Guiden vägleder dig genom stegen.

Ett innehållsfragment baseras på en viss innehållsfragmentmodell som du väljer som första steg i skapandet.

### Skapa och redigera strukturerat innehåll {#create-edit-structured-content}

När fragmentet har skapats kan du öppna det i Content Fragment Editor. Här kan du:

* Redigera innehållet i normalt läge eller helskärmsläge.
* Formatera innehållet som antingen Fullständig text, Oformaterad text eller Markering.
* Skapa och hantera variationer av ert innehåll.
* Associera innehåll.
* Redigera metadata.
* Visa trädstrukturen.
* Förhandsgranska JSON-representationen.

### Skapa innehållsfragment {#creating-content-fragments}

När du har valt lämplig modell öppnas ett innehållsfragment för redigering i redigeraren för innehållsfragment:

![Innehållsfragmentsredigerare](assets/cfm-editor.png)

>[!NOTE]
>
>Se Ytterligare resurser - Arbeta med innehållsfragment.

## Komma igång med några exempel {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

En grundläggande struktur som exempel finns i Struktur för exempelinnehållsfragment.

## What&#39;s Next {#whats-next}

Nu när du har lärt dig att utforma strukturen och skapa innehåll som är beroende av den, är nästa steg att [Lär dig hur du använder GraphQL-frågor för att komma åt och hämta innehåll i innehållsfragment](access-your-content.md). Detta kommer att presentera och diskutera GraphQL och sedan titta på några exempelfrågor för att se hur saker och ting fungerar i praktiken.

## Ytterligare resurser {#additional-resources}

* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md) - den första sidan för innehållsfragment
   * [Innehållsfragment i konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md) - aktivera funktionen för innehållsfragment i konfigurationsläsaren
   * [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) - skapa och redigera modeller för innehållsfragment
   * [Hantera innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md) - skapa och skriva innehållsfragment, den här sidan leder dig till andra detaljerade avsnitt
* [AEM GraphQL-scheman](access-your-content.md) - hur GraphQL realiserar modeller
* [Strukturen för exempelinnehållsfragment](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)
* [Komma igång med AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) - En kort videosjälvstudiekurs med en översikt över hur du använder AEM headless-funktioner, inklusive innehållsmodellering och GraphQL
   * [Grundläggande om GraphQL-modellering](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html) - Lär dig hur du definierar och använder innehållsfragment i Adobe Experience Manager (AEM) för GraphQL.
