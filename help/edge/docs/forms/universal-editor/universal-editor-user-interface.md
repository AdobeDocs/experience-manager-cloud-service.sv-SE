---
title: Navigera i det universella redigeringsgränssnittet för AEM Forms
description: Använd det universella redigeringsgränssnittet för att skapa AEM Forms med Edge Delivery Services. Lär dig de verktyg, genvägar och arbetsflöden du behöver för att skapa formulär effektivt med den här omfattande gränssnittshandboken.
keywords: universell redigerare, AEM-formulär, edge delivery services, interface guide, formulärredigering, WYSIWYG editor, verktyg för formulärframtagning, navigering i användargränssnittet
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 0f372f4ddc0ff323a3beedacc84a8a59de8e6d2a
workflow-type: tm+mt
source-wordcount: '2376'
ht-degree: 0%

---


# Navigera i det universella redigeringsgränssnittet för AEM Forms

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) har ett visuellt gränssnitt för att skapa AEM Forms med Edge Delivery Services. Det ger en **What You See Is What You Get (WYSIWYG)**-upplevelse som visar exakt hur formulären kommer att se ut för användarna.

![Gränssnittsöversikt för Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

Den här guiden hjälper dig att förstå gränssnittet för att skapa formulär effektivt. Vare sig du är nybörjare eller erfaren utvecklare kommer den här guiden att hjälpa dig att:

**Lär dig viktiga färdigheter:**

- Navigera säkert och effektivt i gränssnittet
- Använd lämpliga verktyg för att skapa vanliga formulär
- Arbeta effektivare med kortkommandon
- Felsöka vanliga gränssnittsproblem

**Huvudnyckelarbetsflöden:**

- Konfigurera arbetsytan för optimal produktivitet
- Skapa blanketter från idé till publicering
- Testa och förhandsgranska formulär på olika enheter
- Samarbeta med teammedlemmar i formulärprojekt



## Komma igång snabbt

**Första gången du använder:** Börja med [Grundläggande verktyg](#essential-tools-for-form-building) för att lära dig de huvudfunktioner du använder oftast.

**Erfarna användare:** Hoppa till [Avancerade funktioner](#advanced-features-and-integrations) för specialiserade verktyg och integreringar.

**Snabbreferens:** Använd avsnitten [Gränssnittsöversikt](#interface-overview) och [Kortkommandon](#keyboard-shortcuts) för snabba sökningar.

>[!NOTE]
>
> Har du inte använt formulärredigering tidigare? I [Komma igång med Edge Delivery Services för AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) finns stegvisa anvisningar för hur du skapar formulär.

## Gränssnittsöversikt

Gränssnittet för Universell redigering är indelat i fyra huvudområden, där vart och ett är utformat för specifika uppgifter:

![Gränssnittslayout för Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **Område** | **Syfte** | **Primär användning** |
|----------|-------------|----------------|
| **[A: Experience Cloud Header](#experience-cloud-header)** | Navigering och kontohantering | Växla mellan Adobe verktyg, få tillgång till hjälp, hantera meddelanden |
| **[B: Verktygsfältet Universal Editor](#universal-editor-toolbar)** | Formulärredigering och publicering | Skapa, redigera, förhandsgranska och publicera formulär |
| **[C: Egenskapspanelen](#properties-panel)** | Komponentkonfiguration | Konfigurera formulärfält, hantera innehållsstruktur, komma åt avancerade funktioner |
| **[D: Arbetsytan i redigeraren](#editor-canvas)** | Skapa visuellt formulär | Lägga till komponenter, ordna layout, se förhandsvisning i realtid |

**Gränssnittsflöde:** De flesta användare arbetar primärt i **arbetsytan i redigeraren** (D) och **egenskapspanelen** (C), med **verktygsfältet** (B) för åtgärder som förhandsgranskning och publicering.

## Grundläggande verktyg för formulärkonstruktion

Börja här om du inte har använt den universella redigeraren tidigare. Det här är de verktyg du kommer att använda för de flesta formulärbyggarbetsmoment:

### **1. Arbetsytan i redigeraren - ditt huvudsakliga Workspace**

På arbetsytan i **redigeraren** kan du skapa dina formulär visuellt. Det visar exakt hur formuläret kommer att se ut för användarna.

![Arbetsytan i redigeraren](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Nyckelåtgärder:**

- **Lägg till komponenter** genom att klicka på knappen **Lägg till** på egenskapspanelen
- **Markera element** genom att klicka direkt på dem på arbetsytan
- **Se ändringar i realtid** när du konfigurerar komponenter
- **Testa interaktioner** i förhandsgranskningsläge

### **2. Egenskapspanelen - Konfigurera dina komponenter**

På **egenskapspanelen** (höger sida) kan du anpassa markerade komponenter och hantera formulärstrukturen.

![Egenskapspanelen](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**Grundläggande funktioner:**

- **Egenskapsläge** (`d` genväg) - Konfigurera valda komponentinställningar
- **Innehållsträd** (`f` genväg) - Navigera i formulärstrukturen
- **Lägg till komponenter** (`a` genväg) - Infoga nya formulärfält
- **Komponentåtgärder** - Duplicera eller ta bort markerade element

### **3. Grundläggande om verktygsfält - Förhandsgranska och publicera**

Verktygsfältet **Universal Editor** innehåller viktiga åtgärder för att testa och publicera formulär.

![Verktygsfältet Universal Editor](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**Nödvändiga verktyg:**

- **Förhandsgranskningsläge** (`p` genväg) - Testa formuläret så som användarna ser det
- **Responsivt läge** - Kontrollera hur formuläret ser ut på mobila enheter
- **Öppna sida** (`o` genväg) - Visa formulär på en ny flik
- **Publicera** - Gör formuläret tillgängligt för användare

### **4. Snabbstartarbetsflöde**

**För ditt första formulär:**

1. **Lägg till en adaptiv formulärkomponent** - Infoga `Adaptive Form`-komponenten i ett avsnitt.
2. **Börja bygga** - Lägg till komponenter med knappen **Lägg till** (`a`)
3. **Konfigurera fält** - Välj komponenter och använd **egenskapsläget** (`d`)
4. **Testa formuläret** - Använd **förhandsgranskningsläge** (`p`) för att interagera med formuläret
5. **Kontrollera mobilvyn** - Växla till **responsivt läge** för mobiltestning
6. **Publicera** - Klicka på **Publicera** när du är klar

>[!NOTE]
>
> Mer information om hur du skapar formulär i Universal Editor finns i [Skapa och publicera anpassad Forms med Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md).

**Kontrollpunkter för validering:**

- Kan du lägga till och konfigurera formulärfält?
- Fungerar förhandsvisningsläget korrekt?
- Är alla obligatoriska fält korrekt konfigurerade?
- Visas formuläret bra på mobila enheter?

## Experience Cloud Header

**Experience Cloud Header** innehåller verktyg för navigering och kontohantering. De flesta formulärbyggare använder det ibland för att växla mellan Adobe-verktyg eller för att få tillgång till hjälp.

![Experience Cloud Header](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**Nyckelelement:**

| **Element** | **Syfte** | **När ska du använda** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | Navigera till andra Adobe-verktyg | Växla mellan sajter, Assets, Forms |
| **Organisation** | Växla mellan organisationer | Åtkomstscenarier för flera organisationer |
| **Hjälp** | Få tillgång till dokumentation och support | När du behöver hjälp eller vill lämna feedback |
| **Meddelanden** | Visa tilldelade uppgifter och aviseringar | Kontrollerar arbetsflödesstatus |
| **Lösningar** | Snabb åtkomst till andra Adobe-lösningar | Växla mellan olika Adobe-produkter |
| **Användarprofil** | Kontoinställningar och utloggning | Hantera konton eller byta användare |

**De vanligaste användningsområdena:**

- **Hämtar hjälp** - Klicka på hjälpikonen om du vill ha mer information och support
- **Byta organisation** - Använd listrutan Organisation om du har åtkomst till flera organisationer

## Verktygsfältet Universell redigerare

**Verktygsfältet för den universella redigeraren** innehåller dina primära redigerings- och publiceringsverktyg för formulär. Dessa är ordnade efter användningsfrekvens och typiskt arbetsflöde.

![Verktygsfältet Universal Editor](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **Dagliga arbetsflödesverktyg**

**De här verktygen används i de flesta sessioner för att skapa formulär:**

#### **Förhandsgranskningsläge** (`p` genväg)

**Syfte:** Testa formuläret exakt så som användarna kommer att uppleva det\
**När du ska använda:** Innan du publicerar, efter att ha gjort ändringar, för att testa formulärfunktionen

![Förhandsgranskningsläge](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**Bästa praxis:** Förhandsgranska efter varje större ändring för att fånga upp problem tidigt.

#### **Responsivt läge**

**Syfte:** Kontrollera hur formuläret visas på mobila enheter\
**När ska du använda:** Efter att formuläret har skapats, före publicering

![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**Bästa praxis:** Testa alltid mobilvyn - många användare kommer åt formulär på telefoner.

#### **Öppna sida** (`o` genväg)

**Syfte:** Visa formuläret på en ny flik utan redigeringsgränssnittet\
**När ska du använda:** För helskärmstestning, dela med intressenter för granskning

![Öppna sida](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **Publicera**

**Syfte:** Gör formuläret tillgängligt för användare och live\
**När du ska använda:** Efter grundlig testning i förhandsgransknings- och svarsläge

![Publicera](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**Checklista för validering före publicering:**

- Formuläret har testats i förhandsgranskningsläge
- Mobilsvar har verifierats
- Alla obligatoriska fält har konfigurerats
- Skicka funktionsmakron som fungerar korrekt

### **Navigeringsverktyg**

#### **Hemknapp**

**Syfte:** Återgå till startsidan för Universal Editor\
**När:** Startar arbete i ett annat formulär

![Hemknapp](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **Platsfält** (`l` genväg)

**Syfte:** Navigera direkt till valfritt formulär via URL\
**När ska du använda:** Växla snabbt mellan specifika formulär

![Platsfält](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **Avancerade konfigurationsverktyg**

**Dessa verktyg används för specifika scenarier eller avancerade inställningar:**

#### **AEM-formuläregenskaper**

**Syfte:** Konfigurera inställningar på formulärnivå som FDM (Form Data Model), konfigurera skicka-åtgärder och publiceringsdatum\
**När ska användas:** Konfigurera dataintegreringar, schemalägga publicering

![Formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![Guiden Formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

Panelen Formuläregenskaper innehåller följande avsnitt:

- **Skicka**: Definiera vad som ska hända när en användare skickar formuläret. Välj bland flera olika inlämningsåtgärder, som att skicka data via e-post, skicka till SharePoint, använda en formulärdatamodell eller integrera med tjänster som Adobe Experience Platform eller Microsoft Power Automate. En fullständig lista över de överföringsåtgärder som stöds finns i artikeln [Skicka åtgärd](/help/edge/docs/forms/universal-editor/submit-action.md).

- **Förifyll**: Konfigurera hur formulärfält fylls i automatiskt innan användaren interagerar med formuläret. Du kan ansluta till datakällor som en FDM (Form Data Model) eller använda URL-parametrar för att fylla i fält i förväg, förbättra användarupplevelsen och minska manuell inmatning. Mer information finns i artikeln [Prefill Service](/help/edge/docs/forms/universal-editor/prefill-form.md).

- **Tack**: Anpassa vad användarna ser när de har skickat in formuläret. Du kan visa ett bekräftelsemeddelande eller dirigera om dem till en annan webbsida, vilket ger ett smidigt och professionellt resultat. Mer information om hur du konfigurerar ett tackmeddelande för formulär finns i artikeln [Konfigurera tackmeddelande](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md).

#### **Regelredigeraren** (tidig åtkomst)

**Syfte:** Lägg till dynamiska beteenden, valideringar och villkorlig logik\
**När:** Skapa interaktiva formulär med komplex affärslogik

![Regelredigeraren](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **Mer information:** Mer information finns i [Regelredigerarhandboken](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

#### **Inställningar för autentiseringshuvud**

**Syfte:** Ange anpassade autentiseringsrubriker för utvecklingstestning\
**När:** Lokal utveckling med formulär som krävs för autentisering ska användas

![Autentiseringshuvuden](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **Ytterligare alternativ** (Ellips-menyn)

**Syfte:** Få åtkomst till mindre vanliga åtgärder som att avpublicera\
**När:** tar formulär offline och använder avancerade alternativ

![Ytterligare alternativ](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## Egenskapspanelen

**Egenskapspanelen** (höger sida) är ditt kontrollcenter för att skapa och konfigurera formulär. Det ändras baserat på vad du väljer och innehåller olika verktyg för olika uppgifter.

![Egenskapspanelen](/help/edge/docs/forms/universal-editor/assets/text-properties-ue.png)

### **Bygg kärnformulärverktyg**

**De här verktygen är viktiga när du vill skapa och ordna formulär:**

#### **Lägg till komponenter** (`a` genväg)

**Syfte:** Infoga nya formulärfält och element\
**Så här fungerar det:** Visar tillgängliga komponenter för den valda behållaren

![Lägg till komponenter](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**Vanliga komponenter:**

- Textinmatning, E-post, Telefonfält
- Listruta, alternativknappar, kryssrutor
- Filöverföring, datumväljare
- Paneler och avsnitt för organisationen

#### **Egenskapsläge** (`d` genväg)

**Syfte:** Konfigurera inställningar för valda komponenter\
**När du ska använda:** När du har lagt till en komponent för att anpassa dess beteende

![Egenskapsläge](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**Nyckelinställningar:**

- Field labels and placeholder text
- Valideringsregler (obligatoriskt, format, längd)
- Standardvärden och hjälptext
- Regler för villkorlig synlighet

#### **Innehållsträd** (`f` genväg)

**Syfte:** Navigera och organisera formulärstrukturen\
**När:** Komplexa formulär med flera avsnitt ska användas, hitta specifika komponenter

![Innehållsträd](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**Fördelar:**

- Snabb navigering till valfri komponent
- Visuell formulärhierarki
- Enkel omsortering av element

#### **Komponentåtgärder**

**Syfte:** Hantera befintliga komponenter\
**Tillgängliga åtgärder:**

- **Duplicera** - Kopiera komponenter snabbt ![Duplicera](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **Ta bort** - Ta bort komponenter (ingen bekräftelsefråga) ![Ta bort](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **Avancerade funktioner och integreringar**

**De här verktygen möjliggör avancerad formulärfunktion:**

+++Dataintegrering

#### **Data Source**

**Syfte:** Koppla formulär till datasystem\
**När:** Forms ska användas som behöver läsa/skriva till databaser eller externa tjänster

![Data Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**Funktioner:**

- Konfiguration av formulärdatamodell (FDM)
- Dynamisk datainsamling
- Inlämning till externa system

+++

+++AI-verktyg

#### **Generera variationer**

**Syfte:** Använd AI för att skapa olika versioner av formulärinnehåll\
**När du ska använda:** Experimentera med olika texter, layouter och metoder

    ![Generera variationer](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**Mer information:** [Guiden Generera variationer](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **Innehållsutkast**

**Syfte:** Skapa och spara preliminära textversioner\
**När du ska använda:** Upprepar formulärkopieringen och sparar alternativ för text

![Innehållsutkast](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++Testning och optimering

#### **A/B-testning**

**Syfte:** Jämför formulärvariationer för att optimera prestanda\
**När:** Optimerar konverteringsgrader, testar olika designer

![A/B-testning](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **Experimentation**

**Syfte:** Kör kontrollerade tester på formulärdesign\
**När:** Datadriven formuläroptimering ska användas, användarupplevelsetestning

    ![Experimentation](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Collaboration Tools

#### **Aktivitetshantering**

**Syfte:** Organisera teamarbetsflödet för formulärprojekt\
**När:** Formulärutveckling för flera personer, projektspårning

![Aktivitetshantering](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **Personalization**

**Syfte:** Kontakta Adobe Experience Platform för skräddarsydda upplevelser\
**När ska användas:** Skapa anpassade formulär baserade på användardata

    ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## Arbetsyta för redigerare

**Arbetsytan i redigeraren** är huvudarbetsytan där du visuellt skapar formulär. Det visar exakt hur formuläret kommer att se ut för användarna och ger realtidsfeedback när du gör ändringar.

![Arbetsytan i redigeraren](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Nyckelfunktioner:**

- **WYSIWYG-redigering** - Se ändringarna direkt när du gör dem
- **Direktinteraktion** - Klicka på en komponent för att markera och redigera den
- **Förhandsvisning i realtid** - Växla till förhandsgranskningsläge om du vill testa funktionen
- **Responsiv skärm** - Växla mellan enhetsvisningar för att kontrollera mobilkompatibilitet

**God praxis:**

- **Börja med struktur** - Lägg till huvudavsnitt före detaljerade komponenter
- **Testa ofta** - Använd förhandsvisningsläget regelbundet för att fånga upp problem tidigt
- **Tänk mobilt först** - Kontrollera responsivt läge under hela designprocessen

## Kortkommandon

Använd kortkommandona för att skapa formulär snabbare och effektivare:

| **Kortkommando** | **Åtgärd** | **När ska du använda** |
|--------------|------------|----------------|
| `a` | Öppna komponentlista | Lägga till nya formulärfält |
| `d` | Öppna komponentegenskaper | Konfigurera markerade element |
| `f` | Växla innehållsträd | Navigera i komplexa formulär |
| `p` | Växla förhandsvisningsläge | Testa formulärfunktioner |
| `o` | Öppna formulär på en ny flik | Helskärmstestning |
| `l` | Fokuseringsfält | Byta till olika formulär |

**Pro Tip:** Använd dessa kortkommandon i kombination - markera till exempel en komponent, tryck på `d` för att konfigurera den och sedan på `p` för att testa ändringarna.

## Vanliga arbetsflöden

### **Skapar ditt första formulär**

1. **Lägg till struktur** - Använd `a` för att lägga till en panel för formuläravsnitt
2. **Lägg till fält** - Infoga textindata, e-post och andra komponenter
3. **Konfigurera egenskaper** - Markera varje fält och tryck på `d` för att ange etiketter och validering
4. **Testa funktioner** - Tryck på `p` om du vill förhandsgranska och testa formuläret
5. **Kontrollera mobilvy** - Använd responsivt läge för att verifiera mobilvisning
6. **Publicera** - Klicka på Publicera när du vill publicera

### **Redigerar befintlig Forms**

1. **Navigera i strukturen** - Använd innehållsträdet (`f`) för att snabbt hitta komponenter
2. **Markera och ändra** - Klicka på komponenter direkt eller använd innehållsträdet
3. **Testa ändringar** - Förhandsgranska (`p`) efter varje viktig ändring
4. **Verifiera arbetsflöde** - Testa hela formulärflödet innan du publicerar om

### **Samarbeta med team**

1. **Använd aktivitetshantering** - Tilldela specifika formuläravsnitt till gruppmedlemmar
2. **Dela för granskning** - Använd Öppna sida (`o`) om du vill dela rena förhandsvisningar
3. **Testa tillsammans** - Använd förhandsgranskningsläge för samarbetstestsessioner
4. **Spåra förlopp** - Kontrollera meddelanden om aktivitetsuppdateringar

## Felsökning av vanliga problem

### **Gränssnittsproblem**

+++Gränssnittselement läses inte in

**Problem:** Verktygsfältsknappar, egenskapspanelen eller andra gränssnittselement visas inte

**Lösningar:**

- **Uppdatera sidan** - en enkel webbläsaruppdatering löser ofta inläsningsproblem
- **Kontrollera webbläsarkompatibilitet** - Använd Chrome, Firefox eller Safari
- **Rensa webbläsarcache** - Ta bort cachelagrade filer som kan vara inaktuella
- **Verifiera behörigheter** - Kontrollera att du har rätt åtkomst för att redigera formulär

+++

+++Komponenter svarar inte

**Problem:** Det går inte att välja komponenter eller så uppdateras inte egenskapspanelen

**Lösningar:**

- **Klicka direkt på komponenter** - Undvik att klicka på tomma områden
- **Använd innehållsträdet** - Tryck på `f` och välj komponenter från trädet
- **Kontrollera om det finns överlappande element** - Vissa komponenter kan blockera andra
- **Läs in formuläret igen** - Använd platsfältet (`l`) för att läsa in det aktuella formuläret igen

+++

+++Problem med förhandsgranskningsläge

**Problem:** Förhandsgranskningsläget fungerar inte som det ska eller så visas fel

**Lösningar:**

- **Kontrollera formulärvalidering** - Kontrollera att alla obligatoriska fält är korrekt konfigurerade
- **Testa i redigeringsläge först** - Kontrollera att komponenterna fungerar innan du förhandsgranskar
- **Rensa webbläsarcache** - cachelagrade skript kan störa förhandsgranskningen
- **Kontrollera komponentkonfigurationen** - Kontrollera inställningar för egenskapsläge för fel

+++

## Bästa tillvägagångssätt för effektiv formulärkonstruktion

### **Organisationstips**

- **Använd beskrivande namn** - Etikettera komponenter tydligt i egenskapsläget
- **Gruppera relaterade fält** - Använd paneler för att ordna formuläravsnitt logiskt
- **Planera innan du skapar** - Skissa formulärstrukturen innan du startar
- **Behåll det enkelt** - Undvik överväldigande användare med för många fält

### **Användarupplevelse**

- **Testa ofta** - Använd förhandsgranskningsläget efter varje större ändring
- **Tänk som användare** - Överväg att fylla i hela formuläret
- **Ange tydliga etiketter** - Gör fälten tydliga för användarna
- **Lägg till hjälptext** - Använd hjälptext för komplexa fält

### **Prestandaoptimering**

- **Minimera komponenter** - Använd endast nödvändiga formulärfält
- **Optimera bilder** - Komprimera alla bilder som används i formulär
- **Testa på mobilen** - Säkerställ goda prestanda på långsammare mobilanslutningar
- **Verifiera tidigt** - Ställ in korrekt validering för att förhindra överföringsfel

## Nästa steg

Nu när du förstår gränssnittet i Universal Editor:

1. **Öva med ett enkelt formulär** - Börja med grundläggande fält för att få bekväm användning
2. **Utforska avancerade funktioner** - Prova AI-baserade verktyg och integreringar när det passar
3. **Lär dig att skapa formulär** - Se [Starthandboken](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **Huvudregelredigerare** - Lägg till dynamiska beteenden med [regelredigerarhandboken](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)

**Kom ihåg:** Den universella redigeraren är utformad för att göra formulärskapandet intuitivt. Börja med grunderna och utforska de avancerade funktionerna i takt med att behoven växer.
