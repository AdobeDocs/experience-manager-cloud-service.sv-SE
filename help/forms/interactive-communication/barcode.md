---
title: Streckkodskomponent i Interactive Communication Editor
description: Med streckkodskomponenten i Interactive Communication Editor i AEM Forms kan man visuellt representera kodade data i kommunikationsmallar.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: b44cc569-00a1-4a66-ae25-3d672cf5fc12
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Streckkodskomponent i Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

## &#x200B;1. Inledning

Med streckkodskomponenten i Interactive Communication Editor kan man visuellt presentera kodade data i kommunikationsmallar. Detta är särskilt användbart för program som omfattar spårning, identifiering, fakturering eller automatisering. Den här komponenten har stöd för olika streckkodsstandarder som Code 128, QR med flera, och erbjuder flexibla alternativ för format, positionering och databindning som passar många olika affärsbehov.

Oavsett om du skapar kundfakturor, etiketter eller medlemskort förenklar streckkodskomponenten processen genom att bädda in maskinläsbara data direkt i dokumentet.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/barcode.png)

## &#x200B;2. Egenskaper

Komponenten Barcode innehåller en omfattande uppsättning konfigurerbara alternativ som styr dess beteende och utseende:

2.1 Grundläggande fält

**Namn:** En unik identifierare för streckkoden. Den används för att referera till komponenten i datamodeller och regeluppsättningar.

**Plats:** Anger var streckkodstexten visas i förhållande till streckkodssymbolen.

**Alternativ:**

- **Ingen:** Döljer texten.

- **Ovanför:** Visar texten ovanför streckkoden.

- **Nedan:** Visar texten nedanför streckkoden.

- **Ovanför inbäddat:** Bäddar in texten i streckkodens övre del.

- **Under inbäddad:** Bäddar in texten i streckkodens nedre område.

- **Typ:** Anger streckkodsstandarden (t.ex. Code 128, Code 39, QR Code).

- **Standard:** Ett fördefinierat värde som visas om inga data anges.

- **Datalängd:** Anger det förväntade eller maximala antalet tecken som streckkoden kan innehålla.

- **Kontrollsumma:** Validerar streckkodsdata för precision.

   - **Alternativ:**

      - **Ingen:** Ingen kontrollsummevalidering.

      - **Auto:** Beräknar kontrollsumma automatiskt baserat på typ.

- **Bredd/smalt förhållande:** Definierar den relativa bredden på de breda staplarna till de smala (används i vissa 1D-streckkoder).

2.2 Plats

Avgör var streckkoden visas i relation till innehållet:

- **Ingen:** Ingen ytterligare placering.

- **Ovanför:** Placerar streckkoden ovanför det relaterade innehållet.

- **Nedan:** Placerar streckkoden nedanför innehållet.

- **Ovanför inbäddat:** Streckkoden är inbäddad och flyter ovanför innehållet.

- **Nedanför inbäddat:** Inbäddat under innehåll.

2.3 Position

Definierar den exakta placeringen av streckkoden i layouten:

- **X- och Y-koordinater:** Placera streckkoden i formuläret med millimeterenheter.

- **Höjd och bredd:** Ange streckkodens fysiska mått.

2.4 Marginal

Lägger till avstånd runt streckkoden för bättre visuell separation:

- Överkant

- Nederkant

- Vänster

- Höger

Marginalerna gör layouten mer enhetlig och lättläst.

2.5 Utseende

Anpassa streckkodens visuella stil:

- **Fyllning:** Streckkodsområdets bakgrundsfärg.

- **Linje:** Kantfärg.

- **Bredd:** Definierar streckkodslinjernas tjocklek.

- **Stil:** Välj bland förinställningar som platt, kantlinje eller förhöjd.

- **Kanter:** Avgör mellan rundade eller skarpa hörn för streckkodsrutan.

2.6 Närvaro

Anger om streckkoden visas eller döljs vid körning:

- **Synlig:** Streckkoden visas i det slutliga resultatet.

- **Dolt:** Utrymmet är reserverat men streckkoden visas inte.

2.7 Databindning

Databindning: Ansluter streckkoden till en serverdelsdatamodell (XML eller JSON). Detta garanterar att streckkoden dynamiskt återspeglar unika data per dokumentinstans, som ett order-ID eller spårningsnummer.

## &#x200B;3. Användning

Streckkodskomponenten är särskilt användbar när man automatiserar processer som bygger på inskannade data. Den kan läggas till i kommunikationsmallar som:

- Fakturor (för kundreferens och betalningar för snabbsökning)

- Leveransetiketter (för paketspårning)

- Medlemskap eller förmånskort (för skanningsbaserad identifiering)

- Kuponger och kuponger (för validering vid inköpstillfället)

Författare kan bädda in streckkoden i layoutbehållare och formatera den enligt varumärket eller dokumenttemat.

## &#x200B;4. Bästa praxis

- Använd en lämplig streckkodstyp för användningsfallet, t.ex. QR-kod för URL:er, Code 128 för alfanumeriska ID:n.

- Validera streckkodens läsbarhet genom att skriva ut testversioner och skanna dem.

- Säkerställ dataintegriteten med alternativet checksum om streckkodsstandarden stöder det.

- Välj läsbara storlekar och linjebredder för att undvika skanningsproblem.

- Behåll lämpliga marginaler för att förhindra bortfall vid utskrift.

Streckkodskomponenten i Interactive Communication editor gör det möjligt för dokumentförfattare att överbrygga klyftan mellan digitala och fysiska system. När det implementeras effektivt förbättras automatiseringen, användarbekvämligheten förbättras och integrationen med skannerenheter och arbetsflöden underlättas.
