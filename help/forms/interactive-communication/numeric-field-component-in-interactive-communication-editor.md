---
title: Numeriskt fältobjekt i interaktiv kommunikationsredigerare
description: Numeriskt fältobjekt i Interactive Communication Editor i AEM Forms så att författare kan samla in numeriska data från användare i ett kontrollerat format.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---


# Numeriskt fältobjekt i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Komponenten Numeriskt fält i redigeraren för interaktiv kommunikation (IC) gör att författare kan samla in numeriska data från användare i ett kontrollerat format. Oavsett om telefonnummer, PIN-koder, policy-ID:n eller ekonomiska siffror hämtas, säkerställer det här fältet att endast numeriska värden accepteras. Komponenten har också stöd för format, formatering, validering och databindning, vilket gör den oumbärlig för strukturerad kommunikation.

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/numericfield.png)

## &#x200B;2. Egenskaper

2.1 Grundläggande fält

- **Namn:** Definiera en unik identifierare för fältet, som används i datamodeller, regler och skript.

- **Bildtext:** Visa etiketten på skärmen som visas för användarna (t.ex. &quot;Kontaktnummer&quot; eller &quot;ID för anställd&quot;).

- **Värde:** Tillåt användare att ange numeriska indata, t.ex. telefonnummer, ID, kvantiteter eller monetära värden.

- **Reservera:** Ange justeringen för det numeriska värdet - vänster, höger, överst eller nederst - eller ange en anpassad position med enheter som millimeter (t.ex. 20 mm).

- **Utseende:** Ange utseendet på värderutan som Ingen, Helfylld ruta eller Understruken baserat på den önskade visuella layouten.

2.2 Typografi

Styr den visuella stilen för de numeriska tecken som anges av användaren:

- **Teckensnittsvalidering:** Använd begränsningar för att säkerställa att endast giltiga numeriska indata accepteras, t.ex. heltal, decimaler eller nummerintervall, baserat på den avsedda datatypen.

- **Teckenstorlek:** Justera storleken på den numeriska texten med punktvärden som 10 pt, 12 pt eller 20 pt för att bibehålla en konsekvent och läsbar form i hela formuläret.

2.3 Position

Styr det numeriska fältets rumsliga placering på arbetsytan.

- **X- och Y-koordinater:** Definiera exakt fältplacering.

- **Bredd och höjd (i mm):** Anger storleken på indatarutan.

2.4 Marginal

Definierar avstånd runt det numeriska fältets gräns för ren justering.

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.5 Utseende

Formaterar den numeriska inmatningsfältbehållaren så att den matchar den önskade visuella layouten:

- **Fyllning:** Ange bakgrundsfärgen för det numeriska fältet. Detta gör att det blir lättare att skilja den från andra element eller att matcha den med det övergripande temat.

- **Linje:** Lägg till kantlinjer runt det numeriska fältet med följande anpassningsbara alternativ:

- **Bredd:** Definiera kantens tjocklek så att den passar den visuella betoningen.

- **Stil:** Välj ett kantmönster - heldragen, streckad eller prickad.

- **Edge:** Markera mellan rundade eller skarpa hörn för kanten.

- **Radie:** Justera hörnrundheten med hjälp av specifika radievärden (t.ex. 4 px, 10 px) för att mjuka upp eller öka skärpan i fältets utseende.

2.6 Närvaro

Styr det numeriska fältets synlighet under körning.

- **Synligt:** Standardläge; fältet visas normalt.

- **Dolt (behåller utrymme):** Fältet är osynligt, men utrymme behålls i layouten.

2.7 Databindning

**Databindningstyp:** Ansluter det numeriska fältet till en datakälla (XML eller JSON) för integrering i realtid.

**Använd namn:** Bindar fältet till dess unika namn för enkel värdehämtning.

**Använd globala data:** Länkar fält till en delad datanod över formulär eller fragment.

**Ingen databindning:** Behåller fältet statiskt för att endast användas visuellt eller för temporära indata.

## &#x200B;3. Användning

Numeriska fält är idealiska i scenarier där bara siffror är giltiga. Exempel på vanliga användningsområden:

- Hämtar **mobilnummer, engångslösenord och PIN-koder**

- Ange **principnummer eller anställnings-ID**

- Samlar in **numeriska kvantiteter eller monetära värden**

- Aktiverar **stegbaserade nummerfält** (t.ex. räknare eller poängposter)

Författare kan placera numeriska fält i layoutbehållare eller delformulär och tillämpa validering (t.ex. begränsningar för längd, minsta eller högsta värde) för att förbättra datakvaliteten.

## &#x200B;4. Bästa praxis

- Märk numeriska fält tydligt med enheter om det behövs (t.ex.&quot;Belopp i ₹&quot;).

- Använd formatvalidering (som 10-siffriga gränser för telefonnummer) för bättre precision.

- Använd reserverade värden när fält är obligatoriska men dynamiska data kanske saknas.

- Bind numeriska fält noggrant till schemasökvägar för att stödja backend-bearbetning.

- Enhetligt utseende och typografi som överensstämmer med varumärkesriktlinjerna.

Objektet **Numeriskt fält** i redigeraren för interaktiv kommunikation är ett exakt och tillförlitligt verktyg för sifferbaserad datainsamling. Tack vare effektiva formaterings-, synlighets- och databindningsfunktioner kan du säkerställa att numeriska data är korrekt inlästa och sömlöst integrerade i digitala formulär. När formuläret är formaterat och konfigurerat på rätt sätt blir det betydligt enklare att använda formuläret och dessutom blir informationen mer korrekt.


