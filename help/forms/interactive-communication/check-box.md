---
title: Kryssrutekomponent i interaktiv kommunikationsredigerare
description: Med kryssrutekomponenten i den interaktiva kommunikationsredigeraren i AEM Forms kan du göra en eller flera binära markeringar (ja/nej, true/false).
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 636e9699-a8db-4cb0-aa9f-0602939006df
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Kryssrutekomponent i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

## &#x200B;1. Inledning

Med Check Box-komponenten i redigeraren för interaktiv kommunikation (IC) kan du göra en eller flera binära markeringar (yes/no, true/false). Det används ofta för villkor, inställningar, medgivandefält och valmöjligheter och är ett snabbt sätt att samla in boolesk information i ett kommunikationsformulär.

Kryssrutan har stöd för flexibel formatering, databindning och synlighetsregler, vilket gör den till ett lätt men kraftfullt verktyg för att utforma interaktiva, användarvänliga formulär.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/checkbox.png)

## &#x200B;2. Egenskaper

2.1 Grundläggande fält

- **Namn:** En unik identifierare som används för att referera till kryssrutan i datamodeller, regler eller skript.

- **Växla:** Tillåter att kryssrutan aktiveras/inaktiveras när användaren klickar på den. Detta kan användas i ett enstaka eller grupperat läge.

- **Bildtext:** Den beskrivande etikett som visas bredvid kryssrutan, och som vägleder användarna när det gäller vad de godkänner eller väljer.

- **Reservera:** Valfri platshållartext eller symbol visas i skrivskyddat läge eller grundläge när ingen interaktion görs.

2.2 Position

Definierar var kryssrutan placeras i layouten:

- **X- och Y-koordinater:** Ange kryssrutans plats i layoutstödrastret.

- **Höjd och bredd:** Definierar kryssrutans mått (i mm eller px), särskilt viktigt när du använder anpassade visuella format eller ikoner.

2,3 marginal

Tillåter mellanrum runt kryssrutan för layoutjusteringar:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.4 Utseende

Anger kryssrutans visuella format och dess ram:

- **Fyllning:** Kryssrutans bakgrundsfärg (när den är markerad eller omarkerad).

- **Linje:** Kryssrutans konturfärg.

- **Linjebredd:** Tjocklek på kantlinjen.

- **Stil:** Heldragen, streckad eller anpassat konturmönster.

- **Kanter:** Definierar kryssrutans hörnformat: rundade eller skarpa kanter beroende på designinställningar.

2.5 Närvaro

Anger hur och när kryssrutan visas vid körning:

- **Synlig:** Visas normalt och tar upp utrymme.

- **Dold (behåller utrymme):** Dold från gränssnittet, men layoututrymmet behålls. Användbar för villkorlig synlighet utan layoutbrytning.

2.6 Databindning

Gör att kryssrutan kan interagera med externa eller interna datakällor:

**Databindningstyp:**

**Använd namn:** Binder värdet med komponentens fältnamn.

**Använd globala data:** Ansluter till en global datamodell som delas i hela kommunikationen.

**Ingen databindning:** Kryssrutan är fristående och lagras inte i datamodellen.

&#x200B;3. Användning

Kryssrutor används ofta i scenarier som:

- **Samtyckesfält:**, t.ex. &quot;Jag accepterar villkoren&quot;

- **Användarinställningar:**, t.ex. &quot;Prenumerera på nyhetsbrev&quot;

- **Flera val:**, t.ex. &quot;Välj alla tillämpliga alternativ&quot;

- **Formulärbekräftelser:**, t.ex. &quot;Jag bekräftar att ovanstående uppgifter är korrekta&quot;

Kryssrutor kan placeras inuti stödraster eller paneler och grupperas tillsammans för bättre ordning i formulär.

&#x200B;4. Bästa praxis

- Använd tydliga, kortfattade bildtexter för att hjälpa användarna förstå vad de väljer.

- Undvik störningar genom att bara använda kryssrutor för binära indata - använd alternativknappar för exklusiva alternativ.

- Kontrollera mellanrummet med marginal- och layoutinställningar för ett rent användargränssnitt.

- Bind kryssrutorna till en meningsfull datamodellreferens när det hämtade valet behöver lagras eller bearbetas.

- Använd synlighetsregler när kryssrutorna är beroende av tidigare indata eller villkor.

Check Box-komponenten i Interactive Communication Editor är en enkel men viktig komponent för binära indata. Tack vare stödet för formatering, villkorlig närvaro och flexibel databindning spelar det en viktig roll när det gäller att förbättra interaktiviteten och användarkontrollen i smarta digitala formulär. När kryssrutorna implementeras med genomtänkta etiketter, enhetlig formatering och meningsfull dataintegrering bidrar de till en smidig och intuitiv formulärupplevelse.
