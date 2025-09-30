---
title: Textfältsobjekt i interaktiv kommunikationsredigerare
description: Textfältobjekt i interaktiv kommunikationsredigerare i AEM Forms som gör det möjligt för författare att visa information som namn, adresser, kommentarer eller numeriska ID:n.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---


# Textfältsobjekt i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med textfältskomponenten i redigeraren för interaktiv kommunikation kan författare visa information som namn, adresser, kommentarer eller numeriska ID:n. Värdet som visas i textfältet är antingen fördefinierat (statiskt) eller dynamiskt ifyllt med databindning. Det stöder single line-poster, valideringsregler och flexibel formatering, vilket gör det till ett av de mest använda och mångsidiga elementen i personaliserad kommunikation.

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/textfield.png)

## &#x200B;2. Egenskaper

2.1 Grundläggande fält

- **Namn:** Definiera en unik identifierare för fältet, som används i datamodeller, regler och skript.

- **Bildtext:** Visa etiketten på skärmen som visas för användarna (t.ex. &quot;Förnamn&quot;).

- **Värde:** Visa text som namn, adresser, kommentarer eller annan information. Värdet är antingen statiskt eller härlett från databindning.

- **Reservera:** Ange justeringen av värdet, vänster, höger, upptill eller nedtill eller ange en anpassad position med enheter som millimeter (t.ex. 20 mm).

- **Utseende:** Ange utseendet på värderutan som Ingen, Helfylld ruta eller Understruken baserat på den önskade visuella layouten.

2.2 Typografi

Styr den visuella stilen för de tecken som skrivs:

- **Teckensnittsvalidering:** Använd valfria begränsningar för att validera det visade värdets format, till exempel bara alfabet, siffror eller specifika anpassade mönster.

- **Teckenstorlek:** Justera storleken på texten i fältet med punktvärden som 10 pt, 12 pt, 20 pt osv. för att säkerställa läsbarhet och justering med designstandarder.

2.3 Position

Definierar fältets placering i layouten:

- **X-/Y-koordinater**

- **Bredd och höjd** (mm, px eller %)

2.4 Marginal

Anger avstånd runt fältbehållaren:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.5 Utseende

Formaterar själva fältbehållaren:

- **Fyllning:** Ange textrutans bakgrundsfärg. Detta hjälper till att skilja på indataområden och att justera dem mot varumärkesfärger.

- **Linje:** Lägg till kantlinjer runt textrutan med följande anpassningsbara egenskaper:

- **Bredd:** Definiera kantens tjocklek.

- **Format:** Välj mellan heldragna, streckade eller prickade kantlinjeformat.

- **Edge:** Markera hörnens form, antingen rundade eller skarpa.

- **Radie:** Justera hörnkrökningen med hjälp av radievärden (t.ex. 4 px, 10 px) för ett mjukare eller mer vinkelutseende.

2.6 Närvaro

Bestämmer synlighet vid körning:

- **Synlig:** Visar och tar upp utrymme

- **Dold (behåller utrymme):** Osynlig men layoututrymme är reserverat

2.7 Databindning

Länkar textfältet till en datakälla för att visa värden dynamiskt eller statiskt i kommunikationen.

- **Databindningstyp:** Anger hur fältet ansluts till en datakälla eller ett schema.

- **Använd namn:** Binder textfältet med fältnamnet som är definierat i datamodellen eller schemat, vilket tillåter dynamisk textvisning baserat på externa data.

- **Använd globala data:** Ansluter fältet till globala data som delas i hela kommunikationen för att få en konsekvent informationsvisning.

- **Ingen databindning:** Behåller fältet olänkat från någon backend-källa. Den används för att visa statiska värden eller text som endast är avsedd för visuell kontext.

## &#x200B;3. Användning

Vanliga scenarier:

- Hämta personuppgifter (namn, adresser, telefonnummer)

- Godkänna kommentarer eller feedback (flera rader)

- Ange principnummer eller konto-ID:n

- Samla in korta numeriska värden som PIN-koder eller engångslösenord

Författare kan placera fältet i delformulär eller layoutstödraster för justering och koppla valideringsregler (längdgränser, regex-mönster) för att säkerställa ren inmatning.

## &#x200B;4. Bästa praxis

- Använd validering (obligatoriska flaggor, mönsterkontroller) för omedelbar feedback.

- Ange meningsfull reservtext för utskrift eller skrivskyddad vy.

- Håll typografin i linje med varumärkesriktlinjerna.

- Minska fältbredden på mobila layouter för att passa mindre skärmar.

- Bind direkt till datamodellen när det är möjligt för enklare underhåll.

Textfältobjektet i IC-redigeraren är en mångsidig byggsten som effektiviserar datainhämtningen. När den konfigureras noggrant, med välvald typografi, tydliga etiketter, korrekt validering och solid databindning, ger den en sömlös, användarvänlig upplevelse och tillförlitliga data för bearbetning längre fram i kedjan.


