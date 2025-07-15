---
title: Förstå universell redigerare - responsivt läge
description: I den här artikeln beskrivs hur du förhandsgranskar formulär med olika emulatorer i den universella redigeraren för att se hur de ser ut och känns under utvecklingen.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 0%

---


# Responsivt läge i WYSIWYG Authoring

<span class="preview"> Det här är en förhandsversion som är tillgänglig via vår <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">förhandsversion </a>. </span>

## Introduktion till responsiv Forms

I dagens värld med flera enheter måste dina formulär se bra ut och fungera bra på skärmar av alla storlekar - från datorskärmar till smarttelefoner. Med det responsiva läget i Universal Editor kan du göra detta genom att förhandsgranska och testa formulären i olika enhetsstorlekar under utvecklingsprocessen.

Med [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) kan du skapa formulär som automatiskt anpassar sig till olika skärmstorlekar, vilket ger en optimal användarupplevelse oavsett vilken enhet som används.

## Förhandsgranska Forms i responsivt läge för olika enheter

Den universella redigeraren har en **emulatorikon** som finns i skärmens övre högra hörn. Du kan förhandsgranska sidor i olika enhetsstorlekar och testa hur responsiv design fungerar för att få en bättre användarupplevelse.

Så här förhandsgranskar du ett formulär i svarsläge:

1. Öppna formuläret i Universell redigerare för redigering.
2. Klicka på ikonen ![Emulator som visar en enhetsförhandsvisningssymbol](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} i verktygsfältet.
3. Välj ett enhetsformat:
   - Skrivbord (standard)
   - Tablet
   - Mobil
   - Anpassad (ange bredd och höjd)

![Skärmbild av Universal Editor med alternativ för responsivt läge för olika enheter](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

Du kan också använda ikonen **Skärmrotator** för att växla mellan stående och liggande orientering när du förhandsgranskar på en surfplatta eller mobila enheter.

Universal Editor har olika emulatorer för att förhandsgranska formulär på olika enheter. I tabellen nedan listas de tillgängliga emulatortyperna tillsammans med motsvarande enhetsbeteckning:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Typ av emulator</th>
        <th style="width: 80%">Enhetsbild</th>
    </tr>
    <tr>
        <td style="width: 20%">Skrivbord</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Skrivbordsvy av ett formulär med helbreddslayout" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tablet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Surfplattevy av ett formulär med medelstor layout med justerade komponenter" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Mobil</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Mobil vy av ett formulär med tunn layout med staplade komponenter" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Egen enhet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Anpassad enhetsvy för ett formulär med användardefinierade dimensioner" style="width: auto; height: auto"></td>
    </tr>
</table>

## Layoutfunktioner

Med Universal Editor kan du skapa lättanvända formulär som ger användarna dynamiska upplevelser. Formulärlayouten styr hur objekt och komponenter visas i ett formulär.

Universal Editor har stöd för följande typer av layouter för formulär:

- [Panellayout](#panel-layout)
- [Guidelayout](#wizard-layout)
- [Dragspelslayout](#accordion-layout)

### Panellayout

Panelayout är användbart när du vill ordna relaterade fält på ett sätt som gör det enklare att navigera och hitta motsvarande innehåll. Panelayouten ordnar formulärkomponenter inom distinkta avsnitt eller paneler i formulär.

![Panellayout som visar flera distinkta avsnitt i ett formulär](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Exempel:** Ett jobbansökningsformulär kan använda paneler för att separera personlig information, utbildning, arbetsupplevelse och referenser till distinkta avsnitt.

**Responsivt beteende:** På mindre skärmar staplas panelerna vanligtvis lodrätt, vilket bevarar deras distinkta grupperingar samtidigt som de justeras till den smalare bredden.

Du kan använda [panelkomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) för att lägga till panellayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar olika egenskaper för panelkomponenten finns i artikeln [panelkomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Guidelayout

Med guidelayouten kan du förenkla ett komplext formulär genom att dela upp det i distinkta steg. Varje steg representerar en annan del av processen och användarna navigerar genom stegen sekventiellt, ofta med knapparna **Nästa** och **Bakåt** . Du kan använda guidelayouten för att skapa ett formulär som innehåller flera avsnitt eller steg.

![Guidelayout med ett flerstegsformulär med navigeringskontroller](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Exempel:** Ett formulär för försäkringsanspråk kan använda en guide för att vägleda användarna genom att tillhandahålla incidentinformation, överföra bevis, ange personlig information och granska överföringen.

**Responsivt beteende:** På mobila enheter behåller guiden sin stegvisa strategi, men justerar innehållet i varje steg för att passa den smalare skärmen, ofta staplade element som skulle visas sida vid sida på större skärmar.

Du kan använda [guidekomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) för att lägga till guidelayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för guidekomponenten finns i artikeln [wizard component](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Dragspelets layout

Dragspelslayouten visar innehåll i komprimerbara avsnitt eller paneler i ett adaptivt formulär. När ett avsnitt är expanderat visas innehållet i det, medan andra avsnitt förblir komprimerade. Den här layouten är idealisk för att visa stora mängder information i ett kompakt format.

![Dragspelslayout som visar expanderbara avsnitt i ett formulär](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Exempel:** Ett produktkonfigurationsformulär kan använda dragspelsavsnitt för Grundläggande alternativ, Avancerade funktioner, Tillbehör och Betalningsplaner, vilket gör att användarna kan fokusera på en aspekt i taget.

**Responsivt beteende:** Dragspel fungerar särskilt bra på mobila enheter eftersom de på ett naturligt sätt sparar vertikalt utrymme genom att endast visa det utökade innehållsavsnittet, vilket gör dem idealiska för mindre skärmar.

Du kan använda [dragspelskomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) för att lägga till dragspelslayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för dragspelskomponenten finns i artikeln om [dragspelskomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### Hur väljer man rätt layout?

Det är viktigt att välja rätt layout för att optimera användarupplevelsen och formulärfunktionerna. Tabellen hjälper dig att förstå de olika layoutalternativen som finns och hjälper dig att välja den lämpligaste layouten baserat på dina specifika behov och användningsexempel:

| Funktion | Panellayout | Guidelayout | Dragspelets layout |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Syfte** | Grupperar relaterat innehåll i distinkta avsnitt | Hjälper användarna genom en flerstegsprocess eller ett formulär | Ordnar innehållet i komprimerbara avsnitt |
| **Struktur** | Distinkta avsnitt | Sekventiella steg/sidor | Komprimerbara paneler/avsnitt |
| **Navigering** | Klicka på panelrubrikerna för att navigera | - Framåt: Nästa-knappen <br>- Bakåt: Bakåt-knappen <br> - Valfria hoppsteg | Klicka på rubriker för att expandera/komprimera avsnitt |
| **Användarupplevelse** | Organiserar stora mängder innehåll på ett hanterbart sätt | Stegvisa anvisningar som minskar överväldigande | Komprimerad vy med expanderade/komprimerade avsnitt |
| **Använd skiftläge** | Komplexa formulär med kategoriserade avsnitt | Konfigurera processer, komplexa formulär | Vanliga frågor, inställningsmenyer, avsnitt med detaljerat innehåll |
| **Bäst för mobilen** | Måttlig - paneler staplas lodrätt | Bra - fokusera bara på det aktuella steget | Utmärkt - sparar utrymme med komprimerbara avsnitt |

## Best Practices for Responsive Forms

Följ dessa standarder för att vara säker på att formulären ger bästa möjliga upplevelse på alla enheter:

1. **Designa för mobilen först:** Börja med att designa formuläret för mobila enheter och förbättra det sedan för större skärmar. Det här arbetssättet garanterar att kärnfunktionerna fungerar på de minsta skärmarna.

2. **Använd lämpliga fälttyper:** Välj fälttyper som fungerar bra på enheter med pekskärm:
   - Använd listrutor i stället för alternativknappar när det finns många alternativ
   - Använd datumväljare utformade för pekrörelser
   - Se till att knappar och knappmål är minst 44px x 44px

3. **Förenkla för mindre skärmar:**
   - Visa färre fält per rad på mobila enheter
   - Överväg att dölja valfria fält bakom ett&quot;Visa mer&quot;-alternativ
   - Dela upp komplexa formulär i fler steg på mobilen

4. **Testa noggrant:** Testa alltid formulären på de faktiska enheterna eller använd emulatorläget i Universal Editor för att säkerställa att de fungerar som de ska oavsett skärmstorlek.

5. **Överväg inläsningstider:** Optimera bildstorlekar och minimera nödvändiga resurser, särskilt för mobila användare som har långsammare anslutningar.

## Felsökning av responsiv Forms

| Problem | Möjlig orsak | Lösning |
|-------|---------------|----------|
| Formuläret ser ut att vara avstängt på mobila enheter | Inställningar för fast bredd eller spillproblem | Använd relativa enheter (%, rem) i stället för pixlar, och kontrollera om det finns spillning:dolda egenskaper |
| Touchelement som är svåra att interagera med | Pekmålen är för små eller för nära varandra | Öka knappens/inmatningsstorleken till minst 44px x 44px och lägg till mer utrymme mellan interaktiva element |
| Innehållsspill på små skärmar | Inga responsiva regler för mindre visningsrutor | Lägg till mediefrågor eller responsiva klasser för att justera layouten för olika skärmstorlekar |
| Formuläret är för långsamt på mobila enheter | Stora bilder eller stora skript | Optimera bilder, minimera JavaScript och överväga lazy loading av icke-kritiska element |
| Olika utseenden mellan emulatorn och riktiga enheter | Webbläsarspecifik återgivning eller enhetsvariationer | Testa på faktiska enheter när det är möjligt, inte bara emulatorer |

## Se även

{#see-more-eds-forms}
