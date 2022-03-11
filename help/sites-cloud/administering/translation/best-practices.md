---
title: Bästa praxis för översättning
description: Lär dig mer om de effektivaste strategierna som sammanställts av Adobe tekniker och konsultteam för att hjälpa dig komma igång med översättningsprojekt.
feature: Language Copy
role: Admin
exl-id: 51b98c24-5566-4088-9010-bd39841a1633
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# Bästa praxis för översättning {#translation-best-practices}

>[!TIP]
>
>Om du är nybörjare på att översätta innehåll kan du läsa [Sites Translation Journey,](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

## Allmänt {#general}

Att skapa eller utöka en global webbnärvaro kan vara en komplex process, men med bra planering och planering kan AEM förenkla arbetet och stödja företagets globala mål.

* **Plan för global expansion** innan du implementerar din första webbplats. Att anpassa en befintlig webbplats för global täckning när webbplatsen implementerades med kort varsel är vanligtvis svårare än att planera för global expansion i början:
   * Utvärdera det aktuella läget för organisationens lokaliseringslösning. Kontrollera om du har **verktyg**, **processer** och **resurser** på plats för att stödja global expansion.
   * Var medveten om **global reglering** och **regional språkinställning**. Designa flexibla innehållsstrukturer och processer som kan hantera en föränderlig global affärsmiljö.
* Bestämma en **styrning** modell som stöder er globala verksamhet och använder AEM som MSM och användarbehörigheter för att tillämpa den valda modellen. Du kan till exempel avgöra om innehållet ska redigeras centralt och&quot;pushas&quot; eller&quot;hämtas&quot; till regioner/länder. Bestäm vilket innehåll som kan låsas upp och ändras i olika geografiska områden. Bestäm vem som ansvarar för att initiera och hantera översättningar.
* Om resurserna tillåter är det bäst att hantera översättningsaktiviteter från ett centralt team som kan utveckla expertis i de verktyg, processer och leverantörsrelationer som behövs.
* **Plan**, **prototype** och **test** er globala struktur och processer för att säkerställa att de stöder företaget och att ni har den support som krävs från intressenter i de olika geografiska områdena.

## Webbplatsstruktur {#site-structure}

* När du utformar webbplatsstrukturen börjar du med att undersöka ditt innehåll och avgör var och på vilket språk innehållet skrivs. Platsen bör vara den översta nivån på din plats.
* Det bästa sättet är att **språkbaserad struktur** med högst tre nivåer mellan den högsta utvecklingsnivån och landsinställningarna.
* Använd en namngivningskonvention för språk/land som följer **[W3C-standarder.](/help/sites-cloud/authoring/fundamentals/accessible-content.md)**
* Bestäm hur innehållet ska distribueras mellan regioner och länder. Tänk på vilka länder som delar språk. Vi rekommenderar att du skapar språkmallsidor, ett lager med oaktiverade sidor, där översatt innehåll kan granskas och ändras och sedan pushas eller dras till en landsplats där det språket delas.
* Det finns två sätt att skapa språkmallar: använda språkkopior och använda MSM/live-kopior.
   * Språkkopieringsmetoden är den som används i AEM körklara ramverk för översättningsintegrering, och därför är det enklaste sättet att komma igång. Ramverket har ett användargränssnitt som gör det till att börja med enkelt att sprida och översätta innehållsändringar från huvudspråket (t.ex. engelska) till mallsidor på överordnad språk. I takt med att projektet växer blir det dock allt viktigare att automatisera arbetsflödet för att hantera översättningen av det ökade antalet sidor och/eller språk.
   * Metoden med MSM/live-kopia kan vara ett alternativ för avancerade användningsområden, där webbplatser är större och mer komplexa. Stabil styrning och automatisering av arbetsflöden krävs från början för att hantera komplexa arvsrelationer mellan engelska och språkmallsidor och för att minska risken för att skriva över befintliga översättningar. Den här hanteringen kan utföras med hjälp av vissa översättningskontakter. Se [MSM och flerspråkiga webbplatser](/help/sites-cloud/administering/msm/best-practices.md#msm-and-multilingual-websites) för mer information.
* Om ditt överordnad språk har globala variationer är det möjligt att använda MSM för att skapa en live-kopia från den globala överordnad som ska användas för översättning. Om global redigering till exempel utförs på en amerikansk engelska-överordnad skapar du en internationell engelska-överordnad som en live-kopia och bas för översättning till andra språk.
* Använd MSM för att skapa landsplatser från översatta språkmallar och för att lansera innehåll på webbplatser som delar samma språk. Till exempel kan den franska överordnad användas på webbplatser i Frankrike, Belgien och Schweiz.
* Planera, skapa prototyper och testa först, innan implementeringen startas.

## Översättningsprocesser och metoder {#translation-processes-and-methods}

* Aktivera en **lokaliseringstjänsteleverantör (LSP)** med expertis inom översättning och tillhörande lokaliseringsverksamhet. LSP-leverantörer kan hjälpa er att skalförändra er globala verksamhet genom att tillhandahålla en rad resurser och tekniker som förbättrar effektiviteten och sparar översättningskostnader:
   * Vissa leverantörer av lågprisleverantörer är både tjänste- och teknikleverantörer. Det finns också fristående teknikleverantörer som tillåter många lågprisleverantörer att delta i deras översättningsplattformar.
   * The **AEM Translation Framework** har stöd för integrering med en mängd olika leverantörer av översättningsteknik för både maskinöversättning och mänsklig översättning.
   * Lär dig hur [integrera LSP-anslutningar i ditt AEM system](integration-framework.md) för att automatisera översättning av innehåll, eller hur du manuellt skapar, exporterar och importerar översättningsprojekt för testning och i de fall där det inte finns någon leverantör av LSP- eller översättningsteknik.
* Välj en **översättningsmetod** som bäst passar innehållet.
   * **Personlig översättning** är bäst lämpat för innehåll där meddelanden och kvalitetskrav är höga och innehållet kommer att finnas kvar på webbplatsen under en tid, till exempel marknadsföringssidor.
   * **Maskinöversättning** kan vara ett bra val för massvolymer av översättning när publiceringstiden är viktig, kvalitetsförväntningarna är avspända eller de mänskliga översättningskostnaderna är oöverkomliga. Support-kunskapsbasen och användargenererat innehåll är vanligtvis maskinöversatta.
* Använd expertis från lokaliseringsleverantörer, Adobe Consulting och systemintegratörer för att planera, skapa prototyper och testa din flerspråkiga webbplatsstruktur.
