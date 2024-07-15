---
title: Bästa praxis för översättning
description: Lär dig mer om de effektivaste strategierna som sammanställts av Adobe tekniker och konsultteam för att hjälpa dig komma igång med översättningsprojekt.
feature: Language Copy
role: Admin
exl-id: 51b98c24-5566-4088-9010-bd39841a1633
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---

# Bästa praxis för översättning {#translation-best-practices}

>[!TIP]
>
>Om du inte är van vid att översätta innehåll läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md), som är en guidad väg genom att översätta ditt AEM Sites-innehåll med hjälp av AEM kraftfulla översättningsverktyg, som är idealisk för dem som saknar AEM eller översättningsupplevelse.

## Allmänt {#general}

Att skapa eller utöka en global webbnärvaro kan vara en komplex process, men med bra planering och planering kan AEM förenkla arbetet och stödja företagets globala mål.

* **Planera för global expansion** innan du implementerar din första plats. Att anpassa en befintlig webbplats för global täckning när webbplatsen implementerades med kort varsel är vanligtvis svårare än att planera för global expansion i början:
   * Utvärdera det aktuella läget för organisationens mognad för lokalisering. Avgör om du har **verktygen**, **processerna** och **resurserna** på plats som stöd för global expansion.
   * Observera **globala regler** och **regionala språkinställningar**. Designa flexibla innehållsstrukturer och processer som kan hantera en föränderlig global affärsmiljö.
* Identifiera en **styrningsmodell** som stöder den globala verksamheten och använd AEM som MSM och användarbehörigheter för att framtvinga den valda modellen. Ta till exempel reda på om innehållet skrivs centralt och&quot;push&quot; eller&quot;pull&quot; till regioner/länder. Bestäm vilket innehåll som kan låsas upp och ändras i olika geografiska områden. Bestäm vem som ansvarar för att initiera och hantera översättningar.
* Om resurserna tillåter är det bäst att hantera översättningsaktiviteter från ett centralt team som kan utveckla expertis i de verktyg, processer och leverantörsrelationer som behövs.
* **Planera**, **prototyp** och **testa** din globala struktur och processer för att se till att de stöder företaget och att du har den support som krävs från intressenter i de olika geografiska områdena.

## Webbplatsstruktur {#site-structure}

* När du utformar webbplatsstrukturen börjar du med att undersöka ditt innehåll och avgör var och på vilket språk innehållet skrivs. Platsen bör vara den översta nivån på din plats.
* Det bästa sättet är en **språkbaserad struktur** med högst tre nivåer mellan den översta utvecklingsnivån och landsplatser.
* Använd en namngivningskonvention för språk/land som följer **[W3C-standarden](/help/sites-cloud/authoring/page-editor/accessible-content.md)**.
* Bestäm hur innehållet ska distribueras mellan regioner och länder. Tänk på vilka länder som delar språk. Vi rekommenderar att du skapar språkmallsidor, ett lager med oaktiverade sidor, där översatt innehåll kan granskas och ändras och sedan pushas eller dras till en landsplats där det språket delas.
* Det finns två sätt att skapa språkmallar: använda språkkopior och använda MSM/live-kopior.
   * Det är språkversionen som används för att AEM ett körklart ramverk för översättningsintegrering, och därför är det enklaste sättet att komma igång. Ramverket har ett användargränssnitt som gör det till att börja med enkelt att sprida och översätta innehållsändringar från huvudspråket (till exempel engelska) till språkmallsidor. I takt med att projektet växer blir det dock allt viktigare att automatisera arbetsflödet för att hantera översättningen av det ökade antalet sidor och/eller språk.
   * Metoden med MSM/live-kopia kan vara ett alternativ för avancerade användningsområden, där webbplatser är större och mer komplexa. Stabil styrning och automatisering av arbetsflöden krävs från början för att hantera komplexa arvsrelationer mellan engelska och språkmallsidor och för att minska risken för att skriva över befintliga översättningar. Den här hanteringen kan utföras med hjälp av vissa översättningskontakter. Mer information finns i [MSM och flerspråkiga platser](/help/sites-cloud/administering/msm/best-practices.md#msm-and-multilingual-websites).
* Om huvudspråket har globala variationer är ett alternativ att använda MSM för att skapa en live-kopia från den globala mallsidan för översättning. Om global redigering till exempel utförs i en amerikansk engelsk master skapar du en internationell engelsk master som en live-kopia och bas för översättning till andra språk.
* Använd MSM för att skapa landsplatser från översatta språkmallar och för att lansera innehåll på webbplatser som delar samma språk. Den franska huvudpersonen kan till exempel läggas ut på webbplatser i Frankrike, Belgien och Schweiz.
* Planera, skapa prototyper och testa först, innan implementeringen startas.

## Översättningsprocesser och metoder {#translation-processes-and-methods}

* Engagera en **lokaliseringstjänstleverantör (LSP)** med expertis inom översättning och relaterade lokaliseringsaktiviteter. LSP-leverantörer kan hjälpa er att skalförändra er globala verksamhet genom att tillhandahålla en rad resurser och tekniker som förbättrar effektiviteten och sparar översättningskostnader:
   * Vissa leverantörer av lågprisleverantörer är både tjänste- och teknikleverantörer. Det finns också fristående teknikleverantörer som tillåter många lågprisleverantörer att delta i deras översättningsplattformar.
   * **AEM Translation Framework** har stöd för integrering med flera olika översättningsteknikleverantörer för både maskinöversättning och mänsklig översättning.
   * Lär dig hur du [integrerar LSP-anslutningar i ditt AEM](integration-framework.md) för att automatisera innehållsöversättning, eller hur du manuellt skapar, exporterar och importerar översättningsprojekt för testning och i de fall där det inte finns någon leverantör av LSP- eller översättningsteknik.
* Välj den **översättningsmetod** som bäst passar innehållet.
   * **Personlig översättning** passar bäst för innehåll där meddelanden och kvalitetskrav är höga och där innehållet kommer att finnas kvar en tid på webbplatsen, till exempel marknadsföringssidor.
   * **Maskinöversättning** kan vara ett bra val för massvolymer av översättning när tiden för publicering är viktig, kvalitetsförväntningarna är avspända eller personalens översättningskostnader är oöverkomliga. Support-kunskapsbasen och användargenererat innehåll är vanligtvis maskinöversatta.
* Använd expertis från lokaliseringsleverantörer, Adobe Consulting och systemintegratörer för att planera, ta fram prototyper och testa din flerspråkiga webbplatsstruktur.
