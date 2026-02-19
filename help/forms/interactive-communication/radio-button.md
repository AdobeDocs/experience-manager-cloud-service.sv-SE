---
title: Alternativknappskomponent i interaktiv kommunikationsredigerare
description: Med Radio Button Component (Alternativknappskomponent) i Interactive Communication Editor i AEM Forms kan författare visa en uppsättning ömsesidigt uteslutande alternativ för användare, vilket innebär att endast ett alternativ kan väljas åt gången.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: fe1608f0-8d93-4b89-9dd9-849339b0a175
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Alternativknappskomponent i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

## &#x200B;1. Inledning

Med komponenten **Alternativknapp** i redigeraren för interaktiv kommunikation (IC) kan författare visa en uppsättning ömsesidigt uteslutande alternativ för användare, vilket innebär att endast ett alternativ kan väljas åt gången. Detta gör det idealiskt för användningsområden som Ja/Nej-frågor, genusval, klassificeringsnivåer eller fördefinierade kategorisvsvar.
Alternativknappar är intuitiva, enkla att konfigurera och kan bindas till backend-datamodeller för smidig datainhämtning och integrering.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/radio.png)

## &#x200B;2. Egenskaper

Komponenten Radio Button innehåller flera konfigurerbara egenskaper:

2.1. Grundläggande fält

- **Namn:** En unik identifierare för fältet. Det används för referenser inom datamodeller, regler och affärslogik.

- **Växla:** Gör det möjligt att definiera varje valbart alternativ i knappgruppen. Varje alternativknapp representerar ett möjligt värde.

- **Bildtext:** Etiketten som är associerad med alternativknappsgruppen som vägleder användaren.

- **Reservera:** Valfritt reservvärde om ingen markering görs eller databindning är tom.

2.2. Position

Beskrivning: Styr den rumsliga placeringen av alternativknappsgruppen i layouten.

**Inställningar:**

- **X- och Y-koordinater**

- **Höjd och bredd** (definieras i mm eller % för responsiv layout)

2.3. Marginal

Definiera avstånd runt textrutan:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.4 Närvaro

- **Beskrivning:** Anger synligheten för alternativknappskomponenten vid körning.

- **Alternativ:**

   - **Synlig:** Visas för användare och tar upp utrymme.

   - **Dold (behåller utrymme):** Visas inte men behåller layoutavståndet.



2.5. Databindning

- **Beskrivning:** Ansluter alternativknappsgruppen till en datamodell för att hämta det valda alternativet.

- **Bindningstyper:**

   - **Använd namn:** Använder det tilldelade fältnamnet som referens för bindning.

   - **Använd globala data:** Binder fältet till en global datamodell eller ett schemaelement.

   - **Ingen databindning:** Alternativknappsmarkeringen är inte knuten till någon datakälla. Den används endast för gränssnittsbeteenden.

## &#x200B;3. Användning

Alternativknappskomponenten är väl lämpad för scenarier där användarna bara får välja ett värde i en lista. Exempel på användningsområden är:

- Välja en föredragen kommunikationsmetod (e-post/telefon/SMS)

- Bekräfta binära beslut (Ja/Nej)

- Välj bland begränsade alternativ (t.ex. kön, civilstånd)

- Ange nöjdhetsnivåer eller avtalsskalor (t.ex. Ogilla/Neutral/Godkänn)

Författare kan gruppera relaterade alternativknappar tillsammans och placera dem i layoutbehållare för enhetlig justering. Etiketter kan placeras textbundet eller ovanför knapparna beroende på visuella designkrav.

## &#x200B;4. Bästa praxis

- Begränsa antalet alternativ till 5 eller färre för att undvika att överbelasta användaren.

- Använd tydliga och kortfattade bildtexter för att beskriva vad användaren väljer.

- Välj det vanligaste eller säkraste alternativet om det behövs.

- Undvik att använda alternativknappar när användare ska kunna välja mer än ett alternativ, använd kryssrutor i stället.

- Bind alternativknappar direkt till schemanoder vid integrering med backend-datamodeller.

- Använd konsekvent mellanrum och justering för bättre visuell skärpa, särskilt i mobilanpassade layouter.

Alternativknappskomponenten i redigeraren för interaktiv kommunikation är en grundläggande indatakomponent som ger ett rent, strukturerat beslutsfattande för slutanvändarna. När den konfigureras med tydliga etiketter, genomtänkta mellanrum och databindning säkerställer den tillförlitlig datainsamling och en smidigare användarupplevelse för formulär, undersökningar och arbetsflöden för introduktion.
