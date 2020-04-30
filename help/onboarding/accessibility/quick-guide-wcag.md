---
title: En snabbguide till WCAG 2.1
seo-title: En snabbguide till WCAG 2.1
translation-type: tm+mt
source-git-commit: 921334705578626ac0ea75765496d4f379bb00fc

---


# En snabbguide till WCAG 2.1{#quick-guide-to-wcag}

Adobe Experience Manager (AEM) as a Cloud Service har utvecklats för att maximera kompatibiliteten med riktlinjerna för tillgängligt webbinnehåll.

The [Web Content Accessibility Guidelines (WCAG) version 2.1](https://www.w3.org/TR/WCAG/) are a set of internationally recognized guidelines developed by the [World Wide Web Consortium (W3C)](https://www.w3.org/) under their [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/).

WCAG 2.1 består av en uppsättning teknikoberoende riktlinjer och framgångskriterier för att göra webbinnehåll tillgängligt för och användbart för personer med funktionshinder. De ger råd till webbinnehållsförfattare, designers och utvecklare som ser till att de resurser de producerar är så tillgängliga som möjligt för så många människor som möjligt, oavsett vilka funktionshinder de har, t.ex. synnedsättning, hörselnedsättning, inlärningssvårigheter, åldersrelaterade begränsningar med mera.

Om du till exempel beskriver en bild (eller annat innehåll som inte är text) genom att använda attributet `alt` i HTML blir det till stor fördel för personer som är blinda eller har nedsatt syn. Textbeskrivningen i attributet `alt` kan antingen konverteras till tal eller överföras till elektroniska, uppdateringsbara blindskriftsskärmar. 

Dessutom kan WCAG 2.1 leda till fördelar för andra mottagare, inklusive personer som kan begränsas beroende på en viss *situation*. Det kan vara personer som på grund av omständigheter som surfteknik, nätverksanslutningshastighet eller surfmiljö kan uppleva hinder som liknar de personer med funktionshinder har.

Med Adobe Experience Manager kan författare och/eller webbplatsägare skapa webbinnehåll som uppfyller relevanta framgångskriterier för WCAG 2.1 nivå A och nivå AA.

Därför är det viktigt att förstå syftet med WCAG 2.1 och hur riktlinjerna är upplagda för att förstå webbtillgänglighet och hur riktlinjerna kan hjälpa till att skapa tillgängligt webbinnehåll.

Syftet med WCAG 2.1 är att tillhandahålla riktlinjer som:

* Är **teknikoberoende:**
Det vill säga riktlinjer som kan tillämpas på en rad olika format för webbinnehåll, inte bara HTML. WCAG 2.1 kan alltså omfatta innehåll som genereras som eller tillhandahålls i PDF, Flash, JavaScript och andra befintliga och framtida webbtekniker. <!-- This aims to address a recognized weakness of WCAG 1.0, in that it was focused on HTML at the expense of other web content formats. -->

* Kan **testas:**
Varje riktlinje är skriven på ett sådant sätt att den kan testas objektivt för att säkerställa att en allmän grupp tillgänglighetsexperter håller med om att riktlinjen har följts. En av utmaningarna med riktlinjerna för tillgänglighet är att vissa kan testas tekniskt medan andra kräver en mänsklig bedömning för att avgöra om riktlinjerna har följts eller inte. <!-- WCAG 2.1 has been written with the aim of reducing the subjectivity that was present in some of the WCAG 1.0 guidelines and checkpoints. -->

* Stödjer **prioriterad och sammanhangsbaserad implementering:**
   <!-- As with WCAG 1.0, --> WCAG 2.1 guidelines are given priorities, relating to the likely impact of not following a guideline on a particular group of users with disabilities. This allows authors to make an informed decision on the most important guidelines for their particular situation. In addition, the concept of *accessibility supported* is introduced. This allows authors to make decisions on how best to use web technologies that may not have full accessibility support, or may require users to have specific assistive technologies and/or browsers in order to benefit from accessibility features.

Dessa mål har i hög grad påverkat strukturen i WCAG 2.1.

>[!NOTE]
>
>Det går inte att skapa en webbplats som tar hänsyn till alla tänkbara funktionshinder eller persontyper. Syftet med WCAG 2.1 är att hjälpa webbförfattare att skapa webbplatser som så långt det rimligen är möjligt är tillgängliga under vissa förhållanden.

<!--
>[!NOTE]
>
>If you are familiar with WCAG 1.0, you will notice some changes in WCAG 2.1. These relate to scope, organization and aim.
-->

## Struktur {#structure}

WCAG 2.1 är strukturerat på ett sätt som introducerar begrepp för att skapa tillgängligt webbinnehåll på ett gradvis mer detaljerat sätt. Det kan ge intryck av att WCAG 2.1 är en mycket komplex uppsättning sammanlänkade dokument, men målet är att (stegvis) tillhandahålla mer detaljerad information när författarna behöver den, i stället för att tillhandahålla allt i ett mycket stort dokument.

WCAG 2.1 består av fyra huvudprinciper för hjälpmedelsanpassad design, som ibland kallas för akronymen **POUR**. Dessa är:

1. **Perceivable**: Kan en användare känna av webbinnehållet i fråga?
1. **Operable**: Kan en användare navigera, mata in data eller på annat sätt interagera med webbinnehållet?
1. **Understandable**: Kan en användare bearbeta och förstå det webbinnehåll som presenteras?
1. **Robust**: Är webbinnehållet tillgängligt på det sätt som avses för en mängd olika webbläsarmiljöer, inklusive äldre och kommande webbläsarmiljöer?

För att förtydliga:
* Varje **princip** består av en eller flera **riktlinjer**.

* Riktlinjerna är skrivna som instruktioner som antingen är positiva (gör det här…) eller negativa (gör inte det här…).
* Riktlinjerna är numrerade från 1.1 till 4.1 där den första siffran motsvarar den överordnade principen.
* Varje riktlinje består av ett eller flera **framgångskriterier**.
* Framgångskriterier skrivs som programsatser, antingen `True` eller `False` för en given webbsida.
* Framgångskriterier kan innehålla antingen/eller-alternativ eller undantag för situationer då framgångskriterierna inte behöver uppfyllas.
* Framgångskriterierna är numrerade enligt den överordnade riktlinjen och principen, från 1.1.1 till 4.1.1. De har också ett kort namn som sammanfattar syftet med kriteriet för enklare referens. Framgångskriterium 1.1.1 är till exempel ett alternativ som inte är text.
* Framgångskriterierna inkluderar en lista med relaterade **tekniker** (beskrivs nedan).

## Stödresurser {#supporting-resources}

Förutom WCAG 2.1-huvudkomponenterna som principer, riktlinjer och framgångskriterier finns det en rad stöddokument. Vissa av dem ger specifika råd om hur man uppfyller vissa aspekter av riktlinjerna, andra är mer allmänna referenser som hjälper webbförfattare, designers och utvecklare att förstå och använda WCAG 2.1 så effektivt som möjligt.

WCAG 2.1 är ett stabilt dokument och kommer inte att ändras, men de flesta av stödresurserna är dynamiska dokument som kommer att förändras och växa med tiden allt eftersom nya tekniker utvecklas och nya exempel upptäcks på hur webbtillgänglighet kan uppnås.

### WCAG 2.1-resurser {#wcag-resources}

Denna förteckning är inte avsedd att vara uttömmande, utan innehåller en introduktion till de tillgängliga resurserna:
* [En översikt över alla WCAG-relaterade dokument](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [En sammanfattning av de olika dokumenten](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [New in WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [A Quick Reference Guide for How to Meet WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [WCAG 2 Frequently Asked Questions](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### What is New in WCAG 2.1 {#what-is-new}

[What&#39;s New in WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) ger värdefull information om delta mellan WCAG samt version 2.0 och WCAG 2.1.

Avsnittet [WCAG 2.0 and 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) beskriver förhållandet mellan dem ytterligare.

### Techniques for WCAG 2.1 {#techniques-for-wcag}

Techniques for WCAG 2.1 finns på sidan [Techniques for WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/).

**Tekniker** utgör nivån under framgångskriterierna i WCAG 2.1-hierarkin. De klassas av WAI som informativa, inte normativa. En specifik teknik behöver alltså inte följas för att en resurs ska uppfylla kraven i WCAG 2.1.

Eftersom tekniker är mycket mer specifika än framgångskriterier avser de vanligtvis en viss teknologi eller innehållstyp (t.ex. HTML eller video) eller en situation (t.ex. e-handel eller e-utbildningsprogramvara). Du kan tänka på tekniker som beprövade exempel på hur specifika riktlinjer och framgångskriterier kan uppfyllas, därför är de till stor hjälp för författare och utvecklare som arbetar i särskilda sammanhang.

Du kan komma åt tekniker:

* Via samlingar (tekniker kan vara allmänna eller relaterade till en viss teknik eller ett visst format som HTML, CSS eller skript på klientsidan) eller
* Via relaterade framgångskriterier. Tekniker kan gälla mer än ett framgångskriterium.

Varje teknik har ett unikt nummer som refererar till dess samling. En av ARIA-teknikerna är till exempel *Technique ARIA2: Identifying required fields with the &quot;required&quot; property*.

Tekniker kan vara tillräckliga, rådgivande eller felaktiga:

* En *tillräcklig teknik* är en teknik som, om den följs, kommer att vara tillräcklig för att uppfylla ett visst framgångkriterium.
* En *rådgivande teknik* är en teknik som, om den följs, kommer att ha en positiv inverkan på tillgängligheten, men kanske inte i sig räcker för att uppfylla ett visst kriterium.
* En *felaktig teknik* är en teknik som beskriver ett specifikt exempel när ett framgångskriterium inte uppfylls.

Informationen om tekniker inkluderar en beskrivning, tillämplighet, exempel, resurser för mer information och detaljer om hur författare kan testa att tekniken har tillämpats korrekt.

Listan över tekniker är inte fullständig och WAI uppdaterar hela tiden listan med nya exempel som återspeglar utvecklingen inom webbteknik, designstrategier och forskningsresultat. Det är därför bra att regelbundet titta efter nyheter i listan över tekniker.

### Understanding WCAG 2.1 {#understanding-wcag}

Detta är en serie dokument som innehåller råd som hjälper läsarna att förstå syftet med specifika riktlinjer och framgångskriterier. Du kan [ladda ned en introduktion samt länkar till mer detaljerad information](https://www.w3.org/WAI/WCAG21/Understanding/).

Varje riktlinje och framgångskriterium har också en egen Understanding-sida med information om:

* Syftet med riktlinjen
* Särskilda framgångskriterier
* Rådgivande tekniker som hjälper till att uppfylla kraven i riktlinjen, men som inte omfattas av något särskilt framgångskriterium.

Sidan Understanding för varje framgångskriterium innehåller information om:

* Syftet med framgångskriteriet.
* Allmänna exempel på hur framgångskriteriet kan uppfyllas.
* Relaterade resurser (ej från W3C) om hur man uppfyller framgångskriteriet.
* Tekniker och fel: specifika och detaljerade exempel på hur framgångskriteriet kan uppfyllas (beskrivs nedan)
* Viktiga termer – en ordlista med termer som är viktiga för att förstå framgångskriteriet.

Ett exempel finns på: [Understanding Success Criterion 1.1.1 (&quot;Non-text content&quot;)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content).

### Så här uppfyller du WCAG 2.1 {#how-to-meet-wcag}

Avsnittet How to Meet finns på sidan [How To Meet WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/). Avsnittet innehåller en alternativ presentation av WCAG som förfinar innehållet i riktlinjerna till de som är mest relevanta för en läsares intressen eller omständigheter. Läsare kan filtrera de framgångskriterier som de vill visa genom att ange särskilda tekniker för webbinnehåll, t.ex. Cascading Style Sheets eller skript eller genom att ange en eller flera prioritetsnivåer.

Utan filtrering visar den här resursen alla framgångskriterier grupperade efter riktlinjer. För varje framgångskriterium anges följande:

* Texten till framgångskriteriet.
* En länk till motsvarande Understanding-dokument.
* En lista över relaterade tillräckliga tekniker med länkar till information om varje teknik.
* En lista över relaterade rådgivande tekniker med länkar till information om varje teknik (om sådan finns).
* En lista över relaterade felaktiga tekniker med länkar till information om varje fel.
