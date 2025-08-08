---
title: Hur man fyller i anpassade formulärfält i förväg
description: Använd befintliga data för att förifylla fält i ett adaptivt formulär. Användare kan förifylla grundläggande information i ett formulär genom att logga in med sina sociala profiler.
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: förifyllnadsformulär, adaptiva blanketttjänster, automatisk ifyllnad av blanketter
source-git-commit: f843a7c91c3d47610580a3787a96e7e3bd49ba09
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---

# Configuring Prefill Service in Adaptive Forms using Edge Delivery Services

Förifyllnad av formulär innebär att formulärfält automatiskt fylls i med relevanta data från externa källor så fort användaren öppnar formuläret. Genom att utnyttja information från användarprofiler, databaser, sparade utkast eller andra serverdelssystem effektiviserar förifyllningen processen och minskar behovet av manuell inmatning, minimerar antalet fel och snabbar upp ifyllandet. Detta förbättrar inte bara användarnöjdheten utan ökar också sannolikheten för att formuläret skickas in.

## Fördelar med förifyllnad av formulär

| Fördelar | Beskrivning |
|---------|-------------|
| **Snabbare slutförande** | Minskar manuell datainmatning, vilket gör att man snabbt kan fylla i blanketter |
| **Förbättrad användarupplevelse** | Forms känner sig mer personaliserat och bekvämt, särskilt för återkommande användare |
| **Högre konverteringsgrad** | Minskar antalet avhopp från formulär genom att minimera åtgärder som användaren måste utföra |
| **Minskade indatafel** | Data från betrodda källor minskar typografi och felaktiga poster |
| **Bättre datakvalitet** | Säkerställer strukturerade, korrekta och konsekventa data för backend-system |

## Hur förifyllning fungerar

I följande diagram visas den automatiska förifyllningsprocessen som inträffar när en användare öppnar ett adaptivt formulär:

![Processflöde för förifyllnad av formulär](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

Förifyllningsprocessen omfattar fyra huvudsteg:

1. **Användaren öppnar formuläret**: Användaren öppnar ett anpassat formulär via en URL eller navigering
1. **Identifiera data Source**: Förifyll-tjänsten avgör den konfigurerade datakällan (formulärdatamodell eller utkasttjänst)
1. **Hämta data**: Systemet hämtar relevanta användardata baserat på kontext, parametrar eller användaridentifiering
1. **Mappa och visa**: Data mappas till formulärfält med `bindRef`-egenskaper och det ifyllda formuläret visas för användaren

Denna automatiska process gör att användarna ser ett formulär som är förifyllt med relevant information, vilket avsevärt förbättrar användarupplevelsen och antalet ifyllda formulär.

## Datastruktur för förifyllning

Adaptiv Forms har stöd för två typer av fält:

- **Bundna fält**: Fält som är kopplade till en datakälla med en `bindRef` -egenskap som inte är tom
- **Obundna fält**: Fristående fält med tomma `bindRef`-värden

Datastrukturen för förifyllning omfattar:

- **afBoundData**: Innehåller data för bundna fält och paneler
- **afUnBoundData**: Innehåller data för obundna fält

Dataformatet måste överensstämma med formulärmodellen:

- **XFA-formulär**: XML-kompatibelt med XFA-mallschema
- **XML-schemaformulär**: XML matchar schemastrukturen
- **JSON-schemaformulär**: JSON-kompatibel med schemat
- **FDM-formulär (Form Data Model)**: JSON matchar FDM-strukturen
- **Schemafria formulär**: Alla fält är obundna och använder obunden XML

## Förutsättningar

Innan du konfigurerar förifyllda tjänster måste du se till att du har:

### Nödvändig konfiguration

- [GitHub-databasen har konfigurerats för Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [Adaptivt Forms-block har lagts till i ditt projekt](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [Datakällan är konfigurerad](/help/forms/configure-data-sources.md)
- [FDM (Form Data Model) har skapats](/help/forms/create-form-data-models.md)

### Åtkomstkrav

- Tillgång till AEM Forms as a Cloud Service
- Behörighet att skapa och redigera formulär
- Åtkomst till universell redigerare med obligatoriska tillägg aktiverat

>[!TIP]
>
> Du kan också redigera formulär för att integrera FDM (Form Data Model) i den universella redigeraren för att hämta data från olika backend-källor. Mer information finns i artikeln [Integrera formulär med formulärdatamodellen i den universella redigeraren](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

## Alternativ för förifyllningstjänst

Universal Editor har två alternativ för förifyllningstjänsten:

| Tjänsttyp | Syfte | Data Source | Bäst för |
|--------------|---------|-------------|----------|
| **Formulärportalutkast - förifyllning** | Återupptar delvis ifyllda formulär | Sparade utkast i Forms Portal | Fortsätter ofullständiga program |
| **Förifyll formulärdatamodell** | Fyller i fält från externa system | Backend-databaser via FDM | Autofylla användarprofildata |

### Detaljerad jämförelse

| Funktion | Förfyllnadstjänst för utkast | FDM Prefill Service |
|---------|----------------------|---------------------|
| **Autentisering** | Kräver användarinloggning för utkaståtkomst | Konfigurerbar baserat på datakälla |
| **Konfigurera komplexitet** | Minimal konfiguration | Kräver konfiguration och mappning av FDM |
| **Datatyp** | Statiska sparade data | Dynamiska data i realtid |
| **Använd skiftläge** | Återuppta sparade program | Förifyll från användarprofiler eller databaser |


## Konfigurera förifyllningstjänst för ett formulär

+++Fas 1: Konfigurera formulärdatamodell

### Steg 1: Skapa formulärdatamodell

1. Logga in på din AEM Forms as a Cloud Service-instans
1. Navigera till **Adobe Experience Manager** > **Forms** > **Dataintegreringar**
1. Välj **Skapa** > **Formulärdatamodell**
1. Välj din **Data Source-konfiguration** och välj den konfigurerade **Data Source**

   ![Skapad formulärdatamodell](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >Mer information om hur du skapar formulärdatamodeller finns i [Skapa formulärdatamodell](/help/forms/create-form-data-models.md).

### Steg 2: Konfigurera FDM-tjänster

1. Gå till **Adobe Experience Manager** > **Forms** > **Dataintegreringar**
1. Öppna formulärdatamodellen i redigeringsläge
1. Markera ett datamodellsobjekt och klicka på **Redigera egenskaper**
1. Konfigurera tjänsterna **Läs** och **Skriv** för de markerade datamodellsobjekten

   ![Konfigurera läs- och skrivtjänst](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. Konfigurera tjänstargument:

   - Klicka på redigeringsikonen för lästjänstargumentet
   - Bind argumentet till ett **användarprofilattribut**, **begärandeattribut** eller **litteralvärde**
   - Ange bindningsvärdet (t.ex. `petid` för ett registreringsformulär för ett djur)

   ![Konfigurera argument för ID för husdjur](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. Klicka på **Klar** för att spara argumentet och **Spara** för att spara FDM-filen

   >[!NOTE]
   >
   > Läs mer om hur du konfigurerar FDM-tjänster i [Arbeta med FDM (Form Data Model)](/help/forms/work-with-form-data-model.md).

+++

+++Fas 2: Skapa och konfigurera det adaptiva formuläret

### Steg 3: Skapa ett adaptivt formulär

1. Navigera till **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**
1. Välj **Skapa** > **Adaptiv Forms**
1. På fliken **Source** väljer du en Edge Delivery Services-mall:

   ![Edge Delivery Services-mall](/help/edge/assets/create-eds-forms.png)

1. Klicka på **Skapa** för att öppna guiden **Skapa formulär**
1. Ange formulärinformationen:

   - **Namn**: Ange ett beskrivande namn för formuläret
   - **Titel**: Ange en användarvänlig titel
   - **GitHub-URL**: Ange din databas-URL (t.ex. `https://github.com/wkndforms/edsforms`)

1. Klicka på **Skapa**

   ![Skapa schemabaserat formulär](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

Formuläret öppnas i den universella redigeraren för redigering.

### Steg 4: Konfigurera Source för formulärdata

1. Markera formuläret och klicka på **Egenskaper**

   ![Välj formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. Öppna fliken **Formulärmodell**
3. I listrutan **Välj från** väljer du **FDM (Form Data Model)**
4. Välj den formulärdatamodell (t.ex. PetFDM) du har skapat i listrutan

   ![Välj fliken Formulärmodell](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. Klicka på **Spara och stäng**
6. Öppna formuläret för redigering i Universal Editor

Formulärelementen från din FDM visas på fliken **Datakälla** i **Content Browser**.

### Steg 5: Lägg till databindning i formulärfält

1. Välj dataelement på fliken **Datakälla**
2. Klicka på **Lägg till** eller dra och släpp-element för att skapa formuläret

   ![Skärmbild av Universal Editor med schemabaserat formulär](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. Lägg till databindning i formulärfält:

   - Markera ett formulärfält
   - Leta reda på egenskapen **Bind Reference** i panelen **Egenskaper**
   - Välj lämplig databindningsreferens

     ![Databindning](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++fas 3: Konfigurera förifyllningstjänst

### Steg 6: Aktivera nödvändiga tillägg

Se till att dessa tillägg är aktiverade i Universell redigerare:

1. **AEM Form Properties Extension**

   - Öppna **Extension Manager** i Universal Editor
   - Aktivera tillägget **AEM-formuläregenskaper**

   ![Ikon för formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **Data Source Extension**

   - Aktivera tillägget **Datakälla** om du inte ser ikonen **Datakällor**

   ![Skärmbild av Universal Editor Extension Manager](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > Detaljerade anvisningar om hur du hanterar tillägg finns i [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

### Steg 7: Konfigurera förifyllningstjänsten

1. Öppna det adaptiva formuläret i den universella redigeraren
2. Klicka på tilläggsikonen **AEM Form Properties**

   ![Ikonen Välj formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. Klicka på fliken **Förifyll**
4. Välj **Förfyllnadstjänst för formulärdatamodell**

   ![Välj förifyllningstjänst](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. Klicka på **Spara och stäng**

+++

+++fas 4: Testa din konfiguration för förifyllning

### Steg 8: Förhandsgranska och testa

1. Gå till **Forms** > **Forms och dokument**
2. Välj ditt adaptiva formulär
3. Välj **Förhandsgranska som HTML**
4. Testa förifyllning genom att lägga till parametrar till URL:en:

   https://your-preview-url.com?<bindreferencefield>=<value>

   **Exempel:**

   https://your-preview-url.com?petid=12345

   ![Förifyll formulär](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

Formuläret ska automatiskt fyllas i med data baserat på den angivna parametern.

+++

## Exempel

### Exempel på datastrukturer för förifyllning

**JSON-exempel för FDM-baserat formulär:**

    &quot;
    
    {
    &quot;afBoundData&quot;: 
    &quot;user&quot;: 
    &quot;firstName&quot;: &quot;John&quot;,
    &quot;lastName&quot;: &quot;Doe&quot;,
    &quot;email&quot;: &quot;john.doe@example.com&quot;,
    &quot;phone&quot;: &quot;+1-555-0123&quot;
    
    },
    &quot;afUnBoundData&quot;: {
    &quot;additionalInfo&quot;: &quot;Användarinställningar inlästa&quot;
    }
    
    
    &quot;

**XML-exempel för XFA-baserat formulär:**

    &quot;
    
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?>
    &lt;afData>
    &lt;afBoundData>
    &lt;användare>
    &lt;firstName>John&lt;/firstName>
    &lt;lastName>Gör&lt;/lastName>
    &lt;email>john.doe@example.com&lt;/email>
    &lt;/user>
    &lt;/afBoundData>
    &lt;/afData>
    
    &quot;

### Exempel på förifyllda URL:er

URL-adresserna nedan är endast till för illustrationsändamål och fungerar inte som de är. Ersätt värden och parametrar med de som är relevanta för din egen miljö när du testar förifyllningsfunktioner.

**Grundläggande prefill-test:**

`https://preview.example.com/form.html?userId=12345`

**Test av flera parametrar:**

`https://preview.example.com/form.html?userId=12345&category=premium`


## Felsökning

+++Vanliga problem och lösningar

| Problem | Möjlig orsak | Lösning |
|-------|----------------|----------|
| **Formulärfält är inte förifyllda** | Fel `bindRef`-värden | Verifiera att `bindRef` matchar FDM-fältnamn exakt |
| **Dataformatfel** | Felmatchad datastruktur | Kontrollera att förifyllda data överensstämmer med formulärmodellschemat |
| **Tjänsten hittades inte** | FDM-konfigurationsproblem | Kontrollera att FDM-tjänster är korrekt konfigurerade och sparade |
| **Autentiseringsfel** | Anslutning till datakälla | Verifiera autentiseringsuppgifter och anslutning för datakälla |
| **Inläsning av partiella data** | Fältkopplingar saknas | Se till att alla obligatoriska fält har rätt databindningar |

+++

+++Felsökningssteg

1. **Verifiera FDM-konfiguration:**

   - Kontrollera om tjänsterna är korrekt konfigurerade
   - Testa FDM-tjänsterna oberoende av varandra
   - Validera anslutning till datakälla

2. **Kontrollera formulärkonfiguration:**

   - Bekräfta att formuläret är kopplat till rätt FDM
   - Verifiera värden för fält `bindRef`
   - Testa formuläret utan förifyllning först

3. **Testa dataflöde:**

   - Använd webbläsarutvecklarverktygen för att inspektera nätverksförfrågningar
   - Kontrollera JavaScript-fel i konsolen
   - Validera svarsdataformat

4. **Vanliga felmeddelanden:**

   - &quot;Det gick inte att hitta förifyllningstjänsten: Kontrollera tjänstkonfigurationen
   - &quot;Databindningen misslyckades&quot;: Verifiera noggrannheten för `bindRef`
   - &quot;Ogiltigt dataformat&quot;: Kontrollera att data matchar schema

+++

## Bästa praxis

+++Bästa praxis för konfiguration

- **Använd beskrivande namn**: Namnge dina FDM:er och tjänster tydligt
- **Validera datamcheman**: Kontrollera att datastrukturen matchar formulärkraven
- **Testa inkrementellt**: Konfigurera och testa ett fält i taget
- **Dokumentmappningar**: Håll reda på mappningar mellan fält och data

+++

+++Prestandaoptimering

- **Minimera datavolym**: Fyll endast i nödvändiga fält i förväg
- **Använd cachelagring**: Konfigurera lämplig cachelagring för data som används ofta
- **Optimera frågor**: Se till att databasfrågorna är effektiva
- **Bildskärmsprestanda**: Spåra inläsningstider för formulär med förifyllning aktiverat

+++

+++Säkerhetsfrågor

- **Verifiera indataparametrar**: Verifiera alltid URL-parametrar
- **Sanera data**: Rensa data innan du fyller i formulär i förväg
- **Implementera åtkomstkontroller**: Se till att användarna bara har tillgång till sina egna data
- **Använd HTTPS**: Använd alltid säkra anslutningar för dataöverföring

+++

+++Riktlinjer för användarupplevelser

- **Ge feedback**: Visa inläsningsindikatorer under datahämtning
- **Hantera fel smidigt**: Visa användbara felmeddelanden
- **Tillåt åsidosättningar**: Låt användare ändra förfyllda data
- **Bevara konsekvens**: Använd konsekvent förifyllning i olika formulär

+++

## Vanliga frågor

+++Hur testar jag om förifyllningen fungerar som den ska?

Förhandsgranska formuläret och lägg till förifyllningsparametrar i URL:en med följande format: `?<bindreferencefield>=<value>`. Kontrollera att fältet har en giltig `bindRef` som matchar din datastruktur. Använd utvecklingsverktygen i webbläsaren för att inspektera nätverksförfrågningar och verifiera att data hämtas på rätt sätt.

+++

+++Vilka dataformat stöds för förifyllning av Adaptive Forms?

Adaptiv Forms har stöd för flera olika format beroende på vilken formulärmodell du använder:

- **XFA-formulär**: XML matchar XFA-schemat
- **JSON-schemaformulär**: JSON-data kompatibla med schemat
- **FDM-formulär**: JSON som mappar till datamodellstrukturen
- **XML-schemaformulär**: XML matchar schemastrukturen

+++

+++Kan jag förifylla både bundna och obundna fält?

Ja, du kan förifylla båda fälttyperna. Bundna fält använder avsnittet `afBoundData` och måste matcha ditt formulärmodellschema. Obundna fält använder avsnittet `afUnBoundData` och kan innehålla ytterligare data.

+++

+++Vad ska jag göra om bara vissa fält förifylls?

Kontrollera att alla fält har rätt `bindRef`-värden som matchar din FDM exakt. Kontrollera att datakällan innehåller alla obligatoriska fält och att datastrukturen matchar formulärmodellschemat.

+++

+++Hur hanterar jag autentisering för förifyllda tjänster?

Autentiseringen beror på din datakällkonfiguration. Konfigurera autentisering i inställningarna för datakällan för FDM-baserad förifyllning. För förifyllning av utkast måste användaren vanligtvis vara inloggad för att komma åt sina sparade utkast.

+++

+++Kan jag använda flera förifyllningstjänster i ett formulär?

Du kan konfigurera en primär förifyllningstjänst per formulär. Du kan emellertid kombinera olika datakällor i en enda formulärdatamodell för att få liknande funktionalitet.

+++

## Relaterade ämnen

- [Integrera formulär med formulärdatamodellen i den universella redigeraren](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [Skapa formulärdatamodeller](/help/forms/create-form-data-models.md)
- [Arbeta med FDM (Form Data Model)](/help/forms/work-with-form-data-model.md)
- [Konfigurera datakällor](/help/forms/configure-data-sources.md)
- [Komma igång med Edge Delivery Services för AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
