---
title: Frågeguiden för Experience Modernization Agent
description: I den här guiden får du tips om hur du kan få en effektiv fråga om Experience Modernization Agent och hur dess kunskaper fungerar.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: e2a9c55644c0d9542f6a299f0df30a3dfd4a55de
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 0%

---


# Frågeguiden för Experience Modernization Agent {#prompting-guide}

Agenten för upplevelsemodernisering väljer automatiskt lämplig kompetens baserat på önskemål om naturliga språk. I den här guiden får du tips på hur du kan få en effektiv fråga och beskriver vad kunskaperna gör.

## Allmänna tips {#general-tips}

### Vissa färdigheter är beroende av resultat från andra färdigheter. {#dependency}

* Eftersom bulkimport behöver den importinfrastruktur som sidmigreringen skapar, måste du migrera minst en sida innan du kör bulkimport.
* Eftersom block-CSS refererar till globala designtoken slutför du den platsomfattande designen innan du formaterar enskilda block.

### AI följer strukturerade arbetsflöden och kommer att ställa klargörande frågor när det behövs mer information. {#workflows}

* Lita på processen och svara på dessa kvalificerande frågor när de kommer fram.
* Försök inte att läsa in alla krav i den inledande uppmaningen.

### Skapa markeringsfiler i projektet för att dokumentera projektspecifika regler, riktlinjer, designbeslut eller begränsningar. {#markdown-files}

* Dessa markeringsfiler (t.ex. INSTRUCTIONS.md, CONTEXT.md) kan innehålla namnkonventioner för filer, regler för innehållsmappning eller varumärkesriktlinjer.
* När du startar en ny konversation ber du agenten att&quot;värma upp genom att läsa projektdokumentationen&quot; så att den läser in det här sammanhanget innan du fortsätter med uppgifter.

### Agentens kontextfönster är inte oändligt. {#limited-window}

* Vid långa konversationer kan tidigare instruktioner vara komprimerade eller glömda.
* Om agenten verkar ha förlorat sitt sammanhang kan du antingen påminna den om de viktigaste punkterna eller rensa chatten och börja om med en snabbguide för att läsa projektdokumentationen.

### Använd iterativa instruktioner för att förfina resultatet. {#iterate}

* Om något inte ser bra ut (t.ex. fel bakgrundsfärg i ett block) ber du agenten att åtgärda det specifika problemet i stället för att börja om från början.

## Kompetens för att skapa och migrera webbplatser {#site-migration}

Webbplatsmoderniseringsagenten har många färdigheter för att skapa nya Edge Delivery Services-webbplatser och migrera befintliga webbplatser. Alla nya webbplatser eller migreringsprojekt på Edge Delivery bör utnyttja dessa kunskaper.

### Migrera en webbplats eller sida till AEM {#migrate-a-site}

Använd denna uppmaning när du migrerar innehåll från en befintlig webbplats till Edge Delivery Services.

#### Exempelfrågor {#example-migrate}

* &quot;Migrera den här sidan: `https://example.com/about`
* &quot;Migrera dessa sidor: URL1, URL2, URL3&quot;

#### Vad du ska veta {#wtk-migrate}

* Migreringen följer ett arbetsflöde i sju steg:
   1. Agenten klipper ut källsidan.
   1. Det identifierar avsnittsstrukturen.
   1. Den utför redigeringsanalyser.
   1. Innehållet mappas till blockvarianter.
   1. Den genererar kod.
   1. Det skapar importinfrastruktur.
   1. Resultatet förhandsgranskas.
* Agenten analyserar sidor med hjälp av en hierarki på två nivåer:
   * Först identifieras avsnittsgränser (bakgrundsändringar, mellanrumsskift)
   * Sedan identifieras innehållssekvenser i varje avsnitt.
* Redigeringsanalysen följer [David&#39;s Model.](https://www.aem.live/docs/davidsmodel)
   * för varje innehållssekvens kontrolleras först&quot;Kan en författare skapa detta med vanlig typning?&quot;
   * Standardinnehåll (rubriker, stycken, listor, textbundna bilder) är att föredra framför block.
* Agenten försöker återanvända befintliga block från databasens blockbibliotek innan nya skapas.
   * När innehåll inte kan mappas till ett befintligt block skapas nya blockvarianter.
   * Du kan fråga efter ändringar, begära nya varianter eller justera mappningar interaktivt.
* Blockvarianter spåras med metadata.
   * När du migrerar flera sidor läser agenten in befintliga anpassade varianter först och återanvänder dem när formateringen matchar (tröskelvärde på 70 % likhet baserat på syfte, färger, typografi, mellanrum, layout).
* Sidhuvud, navigering och sidfot tas inte med vid sidmigrering. Dessa hanteras av särskilda färdigheter.
* Varje migrering skapar importinfrastruktur (sidmallar, blockparser, transformatorer) för framtida bulkimport.

### Massimport {#bulk-import}

Använd den här uppmaningen om du vill importera många sidor i samma mall efter att ha slutfört en [inledande enkelsidig migrering.](#migrate-a-site)

#### Exempelfrågor {#example-prompts-bulk-import}

* &quot;Kör bulkimporten på dessa sidor: URL1, URL2, URL3.&quot;
* &quot;Kör bulkimport på alla produktsidor.&quot;
* &quot;Importera följande bloggsidor gruppvis: URL1, URL2.&quot;

#### Vad du ska veta {#wtk-bulk-import}

* Massimport är beroende av importinfrastruktur som skapats under en tidigare migrering av en sida.
   * Detta inkluderar sidmallar (avsnittsstruktur), transformerare (platsomfattande DOM-rensning) och parsrar (blockspecifik HTML till tabellkonvertering).
* Du måste migrera minst en representativ sida per mall innan bulkimporten kan köras.
* Vid massimport återanvänds den struktur och de mappningar som skapades vid migrering av en sida.
   * Det ger inga fördelar med helt nya mallar.
* Omvandlare arbetar på hela DOM före och efter parsning. Parsorer fungerar på den enskilda blocknivån.
* Alla parsrar valideras innan bulkimporten kan fortsätta.
* En mall motsvarar en bulkimportkonfiguration.
   * Det går inte att blanda mallar i en enda körning.

#### Normalt arbetsflöde {#typical-workflow}

Det rekommenderade arbetsflödet är iterativt: validera först i en liten uppsättning och skala sedan upp.

1. **Kör en enkelsidig migrering först.** - Migrera en representativ sida för mallen som du planerar att importera gruppvis.
   * Detta skapar den importinfrastruktur som krävs.
1. **Kör bulkimporten på en liten uppsättning sidor.** - Be agenten att köra bulkimporten och ange en kort lista med URL:er som följer samma mall.
1. **Granska och förfina resultaten.** - Granska de importerade sidorna.
   * Om något ser felaktigt ut ber du agenten att justera parsrar, transformatorer eller importlogik.
1. **Skala upp.** - När resultatet ser korrekt ut ska du ange en fullständig lista över URL-adresser.
   * Agenten återanvänder samma importlogik och kör bulkimport i stor skala.

### Klipper ut webbsidor {#scraping-webpages}

Använd den här uppmaningen för att extrahera innehåll, metadata och bilder från en käll-URL för analys eller migrering.

#### Exempelfrågor {#example-scraping}

* &quot;Rätta till den här sidan för analys: `https://example.com`&quot;
* &quot;Hämta innehåll från `https://example.com/product`&quot;

#### Vad du ska veta {#wtk-scraping}

* Den här uppmaningen anropas vanligtvis automatiskt som det första steget i sidmigreringen.
* Innehåll som döljs via CSS hämtas också om de finns i DOM.
* Lazyfyllda bilder och renderat innehåll på klientsidan hanteras genom att bläddra igenom sidan i Chromium utan rubrik och låta skript köras.
* WebP-/AVIF/SVG-bilder konverteras till PNG för kompatibilitet.
* Metadata extraheras med titel, beskrivning, Open Graph-taggar, JSON-LD-strukturerade data, kanoniska URL:er.
* Bilder i DOM är fasta.
   * background-image konverteras till img.
   * Bildelement är uppackade
   * src
   * Relativa URL:er konverteras till absoluta
   * Textbundna SVG konverteras till img-filer.
* Sanitifierade dokumentsökvägar genereras (gemener utan tillägget `.html`).
* Följande utdata produceras:
   * `screenshot.png`
   * `cleaned.html` (inga skript/format)
   * `metadata.json`
   * Mappen `images/` med lokala kopior
* Användare kan fråga om skärmbildsdimensioner och begära specifika enhetsstorlekar (mobil, dator) för att extrahera innehåll.
* Genom att extrahera innehåll vid flera brytpunkter förlängs bearbetningstiden.

### Designmigrering {#design-migration}

Använd den här uppmaningen för att extrahera och tillämpa visuell design från en källwebbplats på Edge Delivery Services.

#### Exempelfrågor {#example-design}

* &quot;Migrera designen från `https://example.com`&quot;
* &quot;Extrahera designtoken&quot;
* &quot;Stila hjälteblocket&quot;

#### Vad du ska veta {#wtk-design}

* Designmigreringen har två faser:
   1. Fas 1 (hela platsen) extraherar följande till `styles/styles.css`:
      * Global färgpalett och dekorfärger
      * Typografisystem (teckensnitt, storlekar, vikter)
      * Mellanrumssystem (utfyllnad, marginaler, mellanrum)
      * Sektionsbakgrund (ljusa, mörka, färgade)
      * Grundkomponentformat (knappar, länkar, bilder)
      * Utdata till
   1. Fas 2 migrerar enskilda blockformat och skapar blockspecifik CSS i `/blocks/{name}/{name}.css`.
* Blockformatering (fas 2) kräver att platsomfattande design (fas 1) är klar först.
   * Det globala designsystemet innehåller anpassade CSS-egenskaper som blockerar referenser.
* Beräknad tid:
   * Fas 1: 5-10 minuter
   * Fas 2: 10-15 minuter
* Tvetydiga begäranden om att slutföra migreringen (båda faserna) ska vara standard.

### Blockera kritisk {#block-critique}

Använd den här uppmaningen för att validera och förfina enskilda migrerade block och säkerställa visuell precision mot den ursprungliga webbplatsen.

#### Exempelfrågor {#example-block-critique}

* &quot;Kritique hero block&quot;
* &quot;Validera blockera anpassade kort&quot;

#### Vad du ska veta {#wtk-block-critique}

* Blockkritiker jämför ett migrerat block med dess ursprungliga källa och tillämpar upprepade CSS-korrigeringar tills en visuell likhet på 85 % uppnås eller tre iterationer slutförs.
* Kompetensen kräver att blocket har skapats av sidmigrering först.
* En blockkritik följer ett arbetsflöde i sex steg:
   1. Det hämtar originalblocket från källsidan med en XPath-väljare.
   1. Den initierar kritikersessionen.
   1. Den inspekterar originalblocket (skärmbilder, format, HTML).
   1. Den inspekterar det migrerade blocket.
   1. Den jämför element och genererar en likhetspoäng med CSS-korrigeringar.
   1. Korrigeringar och kontroller utförs tills målet på 85 % har uppnåtts.
* Varje upprepning visar en komplett kritikerrapport med alla skillnader, tillämpar alla CSS-korrigeringar (som prioriteras efter visuell effekt), verifierar i förhandsgranskning, inspekterar om och visar förbättringsmått.
* Använd blockkritiken när [designmigreringen](#design-migration) har slutförts.

### Page Critique {#page-critique}

Använd den här uppmaningen för att validera hela migrerade sidor för att få en helsidig visuell återgivning av originalwebbplatsen.

#### Exempelfrågor {#example-page-critique}

* &quot;Kritisera om-sidan&quot;
* &quot;Verifiera den migrerade sidan mot `https://example.com/about`&quot;

#### Vad du ska veta {#wtk-page-critique}

* Sidkritiker utför en helsidig visuell jämförelse mellan den ursprungliga sidan och den migrerade sidan. Den itererar tills ett 85-procentigt likhetsmål uppnås eller tre iterationer slutförs.
* En sidkritiker har ett arbetsflöde i fem steg:
   1. Initierar en kritisk session.
   1. Den undersöker alla element på originalsidan.
   1. Den undersöker alla element på den migrerade sidan.
   1. Den jämför och genererar en likhetspoäng med prioriterade CSS-korrigeringar.
   1. Korrigeringar och kontroller utförs tills målet på 85 % har uppnåtts.
* En sidkritiker behöver källsidans URL och den migrerade sökvägen (t.ex.&quot;/about&quot;) som indata.
* Använd sidkritiker när du validerar övergripande sidåtergivning eller validerar flera block samtidigt.
* [Använd blockkritik](#block-critique) för fokuserad validering av specifika komponenter.
* Följande arbetsflöde rekommenderas:
   1. Migrera en sida.
   1. Tillämpa en design.
   1. Köra en blockkritik på nyckelblock
   1. Kör ålderskritik för fullständig validering.

### Migrering av Figma Block {#figma-block-migration}

Använd den här uppmaningen för att migrera ett block från Figma-design till Edge Delivery Services.

Observera att du måste ställa in din Figma-information i [Experience Modernization Console](/help/ai-in-aem/agents/brand-experience/modernization/console.md) för att kunna använda den här uppmaningen.

#### Exempelfrågor {#example-figma}

* &quot;Migrera blocket `https://figma.com/design/{fileKey}?node-id={nodeId}` till Edge Delivery Services&quot;
* &quot;Migrera `{blockName}` från `https://figma.com/file/{fileKey}` till Edge Delivery Services&quot;

#### Vad du ska veta {#wtk-figma}

* Den här kompetensen migrerar ett block i taget, inte hela sidor eller fullständiga Figma-filer.
* Bästa resultat:
   * Markera det specifika block som du vill migrera i Figma och kopiera länken (med `node-id`) eller namnet.
   * Ange parametern `node-id` i URL:en för att ange det exakta blocket som mål.
* När du kör den här kompetensen utförs följande steg automatiskt i värdmiljön:
   1. **Identifiering av blockstruktur** - Agenten läser Figma-noden för att förstå lager och komponenter.
   1. **Global style extraction** - Agenten hämtar färger, typografi och mellanrum till `styles/styles.css` som anpassade CSS-egenskaper (designtoken).
   1. **Blockspecifik formatskapande** - Agenten skapar ytterligare anpassade CSS-egenskaper som är specifika för det block som migreras.
   1. **Mappning till befintliga block** - Agenten identifierar det närmaste matchande blocket i projektets blockbibliotek och skapar en anpassad variant.
   1. **CSS-generering** - Agenten skriver format som refererar till de extraherade anpassade CSS-egenskaperna, vilket ger en konsekvent design.
   1. **Resurshämtning** - Agenten sparar bilder och ikoner från Figma till värdmiljöns arbetsyta.
   1. **Edge Delivery Services-innehållsgenerering** - Agenten skapar markeringsfilen efter EDS-blockstrukturen
   1. **Utdatavalidering** - Agenten förhandsgranskar resultatet och utför visuell jämförelse med den ursprungliga Figma-designen.
* Kunskapen läser först metadata (steg 1) för att förstå strukturen, och extraherar sedan detaljerad designkontext (steg 2-5).
   * Detta stegvisa tillvägagångssätt förhindrar problem med stora eller komplexa Figma-filer.
* Den här kompetensen sätter stilar först.
   * Alla format extraheras som anpassade CSS-egenskaper (designvariabler) innan CSS skrivs.
   * Detta garanterar att det migrerade blocket följer ditt designsystem.
* Kommandot kräver Figma-URL (med `fileKey` och valfri `node-id`) eller en Figma-filnyckel direkt som indata.

### Navigeringsinställningar {#navigation-setup}

Använd den här uppmaningen för att konfigurera eller migrera webbplatsnavigering.

#### Exempelfrågor {#example-navigation}

* &quot;Konfigurera navigering från `https://example.com`&quot;
* &quot;Åtgärda navigeringsmenyn&quot;

#### Vad du ska veta {#wtk-navigation}

* Edge Delivery Services-navigering tvingar fram en struktur med tre avsnitt (påtvingad av `header.js`):
   1. **Varumärke** (avsnitt 1): Länk för logotyp och primärt varumärke
   1. **Avsnitt** (avsnitt 2): Huvudnavigeringsmeny med valfria listrutor
   1. **Verktyg** (avsnitt 3): Verktygslänkar (prenumeration, inloggning, kundvagn)
* Navigeringsinnehållet finns i `nav.md` i rotkatalogen.
* Avsnitt avgränsas med (`---`) markörer.
* Fet objekt (`**Text**`) med kapslade listor skapar listrutor.
* Länkar i navigering kan återges som knappar på grund av dokumentredigeringens automatiska radbrytningsbeteende.
   * Rubrikblocket innehåller kod för att ta bort knappklasser från navigeringslänkar.

## Funktioner för blockutveckling {#block-development-capabilities}

Dessa uppmaningar används för att skapa och utveckla block, vilket ger ett kontinuerligt värde utöver att skapa eller migrera den initiala webbplatsen.

### Blockutveckling {#block-development}

Använd den här uppmaningen för att skapa nya eller ändra befintliga block.

#### Exempelfrågor {#example-block-development}

* &quot;Skapa ett block för vittnesmål&quot;
* &quot;Lägg till en videobakgrundsvariant i hjälteblocket&quot;

#### Vad du ska veta {#wtk-block-development}

* Medlet följer innehållsstyrd utveckling (CDD), en obligatorisk process för all Edge Delivery Services-utveckling.
   * Den frågar om innehållsmodeller och testar innehåll innan den skriver kod.
* CDD-filosofin är att författaren måste komma innan utvecklaren behöver det.
   * Innehållsmodellerna måste vara intuitiva för författarna, även om det innebär mer komplex dekorationskod.
* När du skapar testinnehåll först får du:
   * Omedelbar testkapacitet
   * PR-valideringslänkar för PSI-kontroller
   * Livedokumentation för författare
   * Identifiering av kantfall som inte kan hanteras med kod först
* Agenten söker efter liknande block i [Blocksamling](https://www.aem.live/developer/block-collection) och [Blockera grupp](https://www.aem.live/developer/block-party/) innan den implementerar för att hitta mönster och återanvändbar kod.
* Hoppa endast över CDD för triviala CSS-förbättringar (men identifiera fortfarande testinnehåll för validering).

### Innehållsmodellering {#content-modeling}

Använd den här uppmaningen för att utforma tabellstrukturen som författare arbetar med när de skapar blockinnehåll.

#### Exempelfrågor {#example-modeling}

* &quot;Designa en innehållsmodell för ett vittnesmål&quot;
* &quot;Vilken är den bästa innehållsmodellen för karusellen?&quot;

#### Vad du ska veta {#wtk-modeling}

* Edge Delivery Services har fyra typer av kanoniska modeller:
   * **Fristående:** distinkta visuella/berättande element (hjälte, blockquote)
      * En tabell med blockinnehåll
   * **Samling:** Upprepat halvstrukturerat innehåll (kort, karusell)
      * Tabell med upprepat radmönster
   * **Konfiguration:** API-drivet eller dynamiskt innehåll där config-kontroller visas (blogglista, sökresultat)
      * Tabell med nyckelvärdeskonfigurationsrader.
   * **Automatiskt blockerad:** Komplexa strukturer som författare skapar som avsnitt/standardinnehåll och sedan omformas (flikar, YouTube-inbäddade)
* Det finns en gräns på fyra celler per rad.
   * Gruppera relaterade element i celler.
* Använd blockvarianter framför config-celler för formatskillnader.
* [Följ Postels lag](https://en.wikipedia.org/wiki/Robustness_principle): Var flexibel när det gäller indatastrukturen.
   * Ett hjälteblock ska fungera oavsett om innehållet finns i en cell, delas över två celler eller i separata rader.
* Den här kompetensen anropas vanligtvis automatiskt av innehållsdriven utveckling när block skapas.

### Söka efter referensblock {#reference-blocks}

Använd den här uppmaningen för att söka efter befintliga implementeringar som ska användas som startpunkter.

#### Exempelfrågor {#example-reference}

* &quot;Hitta block som liknar en pristabell&quot;
* &quot;Vilka block finns det för vittnesmål?&quot;
* &quot;Search Block Party for a tab implementation&quot;

#### Vad du ska veta {#wtk-reference}

* [Blocksamlingen](https://www.aem.live/developer/block-collection) underhålls av Adobe och kontrolleras för bästa praxis, utmärkt innehållsmodellering, höga prestanda och tillgänglighet.
   * Den är begränsad till vanliga block. Börja här.
* [Blockgruppen](https://www.aem.live/developer/block-party/) är communitydriven och erbjuder en bredare variation, bland annat experimentella metoder.
   * Det innehåller även plugin-program för sidospark, verktyg för bygge (webpack, vite, sass) och integreringar.
   * Används när blocksamlingen inte har det du behöver.
* Tänk på alternativa namn när du söker
   * Vanliga frågor = dragspelspanel
   * Galleri = karusell/bildspel
   * Navigering = meny/rubrik
* Blockparten returnerar endast godkända/förvaltade poster.

### Söker dokumentation {#searching-documentation}

Här hittar du information om Edge Delivery Services funktioner eller implementeringsvägledning.

#### Exempelfrågor {#example-documentation}

* &quot;Hur implementerar jag lazy loading i Edge Delivery Services?&quot;
* &quot;Sök i dokumenten efter metadata för avsnitt&quot;

#### Vad du ska veta {#wtk-documentation}

* Den söker igenom dokumentationen för [aem.live](https://aem.live) (dokument och blogginlägg) specifikt.
* Använd specifika nyckelord (&quot;blockdekoration&quot;,&quot;sidespark plugin&quot;,&quot;metadata&quot;) i stället för generiska termer (&quot;aem&quot;,&quot;website&quot;,&quot;How to build&quot;).
* För kodexempel och referensimplementeringar använder du&quot;find reference blocks&quot; i stället.
* De tio mest relevanta resultaten returneras som standard.

### Testning {#testing}

Använd den här uppmaningen för att validera kodändringar innan du öppnar en pull-begäran.

#### Exempelfrågor {#example-testing}

* &quot;Testa det nya kortblocket&quot;
* &quot;Kör testerna innan jag öppnar en PR&quot;

#### Vad du ska veta {#wtk-testing}

* Testningen följer en &quot;value vs. cost&quot;-filosofi där du skapar och underhåller tester när deras värde överstiger kostnaden.
   * **Innehavartester** (enhetstester) är för logiktunga verktyg, databearbetning och API-integreringar. Dessa är snabba, enkla att underhålla och fångar upp regressioner i återanvänd kod.
   * **Throwaway-tester** (webbläsartester) är för DOM-omvandlingar och visuell validering. Använd för att validera implementeringen, ta skärmdumpar för PR-granskning och sedan ta bort dem.
* Throwaway-tester går in `test/tmp/` och testar innehåll i `drafts/tmp/` (båda gitignored).
* Innan du öppnar en PR ska du se till att
   * Befintliga tester godkänns
   * Enhetstester skrivs för ny logik
   * Valideringen av webbläsaren är klar
   * Alla varianter testas
   * Responsiv funktion har verifierats
   * Linting pass

### Felsökning {#debugging}

Använd den här uppmaningen för att felsöka problem med block, bilder, CSS eller förhandsgranskning.

#### Exempelfrågor {#example-debugging}

* &quot;Felsök varför bilder visas som om :error&quot;
* &quot;Åtgärda hjälteblocket som inte återges&quot;
* &quot;Varför visas inte mina ändringar i förhandsgranskningen?&quot;

#### Vad du ska veta {#wtk-debugging}

* Vanliga problem har kända mönster:
   * **Bilder som visar &quot;about:error&quot;**: `createOptimizedPicture`-anrop saknas vanligtvis i block-JS, eller anropas före DOM-omstrukturering
   * **Blocken återger inte**: Kontrollera blocknamnsformatet i markeringen och verifiera att blocket har både `.js` och `.css` filer i `blocks/`.
   * **CSS läses inte in**: Kontrollera filsökvägar, verifiera att CSS-filen finns och kontrollera fliken Nätverk i webbläsaren.
   * **Ändringar visas inte**: Kodsynkronisering tar 3-5 sekunder. Prova att uppdatera (Ctrl+Skift+R).
* Agenten kontrollerar varje lager systematiskt:
   1. Source-filer
   1. Återgivna utdata
   1. Blockera kod
   1. Webbläsarkonsol
* Agenten kan kontrollera lokala förhandsvisningar på `http://localhost:3000`.
