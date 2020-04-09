---
title: En snabbguide till WCAG 2.1
seo-title: En snabbguide till WCAG 2.1
translation-type: tm+mt
source-git-commit: 11f0509334ebe4456612789fd415a3099687dc64

---


# En snabbguide till WCAG 2.1{#quick-guide-to-wcag}

Adobe Experience Manager (AEM) som en molntjänst har utvecklats för att maximera kompatibiliteten med riktlinjerna för tillgängligt webbinnehåll.

WCAG ( [Web Content Accessibility Guidelines) version 2.1 (WCAG)](https://www.w3.org/TR/WCAG/) är en uppsättning internationellt erkända riktlinjer som tagits fram av [World Wide Web Consortium (W3C)](https://www.w3.org/) inom ramen för deras [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/).

WCAG 2.1 består av en uppsättning teknikoberoende riktlinjer och framgångskriterier som gör webbinnehåll tillgängligt för och användbart för personer med funktionshinder. De ger råd till webbinnehållsförfattare, designers och utvecklare om att se till att de resurser de producerar är så tillgängliga som möjligt för så många människor som möjligt, oavsett vilka funktionshinder de har. t.ex. synnedsättning, hörselbortfall, inlärningssvårigheter, åldersrelaterade begränsningar.

Om du till exempel beskriver en bild (eller något annat innehåll som inte är text) genom att använda attributet `alt` i HTML blir det till stor fördel för personer som är blinda eller som är synkade delvis. Textbeskrivningen i attributet kan antingen konverteras till talutdata eller överföras till elektroniska, uppdateringsbara blindskriftsskärmar. `alt`

Dessutom kan WCAG 2.1 leda till fördelar för andra mottagare, inklusive personer som kan anses vara *tillfälligt inaktiverade*. Personer som på grund av omständigheter som surfteknik, nätverksanslutningshastighet eller surfmiljö kan uppleva hinder som liknar personer med funktionshinder.

Med Adobe Experience Manager kan skribenter och/eller webbplatsägare skapa webbinnehåll som uppfyller relevanta kriterier för WCAG 2.1-nivå A och nivå AA.

Därför är det viktigt att förstå syftet med WCAG 2.1 och hur riktlinjerna är upplagda för att förstå webbtillgänglighet och hur riktlinjerna kan hjälpa till att skapa tillgängligt webbinnehåll.

WCAG 2.1 har för avsikt att ge riktlinjer som

* Är **teknikagnostiska:**
Riktlinjer som kan tillämpas på en rad olika webbinnehållsformat, inte bara HTML. WCAG 2.1 kan alltså omfatta innehåll som genereras av eller tillhandahålls i PDF, Flash, JavaScript och andra befintliga och framtida webbtekniker. <!-- This aims to address a recognized weakness of WCAG 1.0, in that it was focused on HTML at the expense of other web content formats. -->

* Kan **testas:**
Varje riktlinje är skriven på ett sådant sätt att den kan testas objektivt för att säkerställa att en grupp experter på tillgänglighet i allmänhet håller med om att riktlinjen har följts. En av utmaningarna med riktlinjerna för tillgänglighet är att vissa, även om de kan vara tekniskt testbara, andra kräver en mänsklig bedömning för att avgöra om riktlinjerna har följts eller inte. <!-- WCAG 2.1 has been written with the aim of reducing the subjectivity that was present in some of the WCAG 1.0 guidelines and checkpoints. -->

* Stöd för **prioriterad och sammanhangsbaserad implementering:**
   <!-- As with WCAG 1.0, --> WCAG 2.1 guidelines are given priorities, relating to the likely impact of not following a guideline on a particular group of users with disabilities. This allows authors to make an informed decision on the most important guidelines for their particular situation. In addition, the concept of *accessibility supported* is introduced. This allows authors to make decisions on how best to use web technologies that may not have full accessibility support, or may require users to have specific assistive technologies and/or browsers in order to benefit from accessibility features.

Dessa mål har i hög grad påverkat strukturen i WCAG 2.1.

>[!NOTE]
>
>Det går inte att skapa en webbplats som tar hänsyn till alla tänkbara funktionshinder eller persontyper. Syftet med WCAG 2.1 är att hjälpa webbförfattare att skapa webbplatser som så långt det är möjligt är tillgängliga under vissa förhållanden och med vissa orsaker.

<!--
>[!NOTE]
>
>If you are familiar with WCAG 1.0, you will notice some changes in WCAG 2.1. These relate to scope, organization and aim.
-->

## Struktur {#structure}

WCAG 2.1 är strukturerat på ett sätt som introducerar koncept för att skapa tillgängligt webbinnehåll på ett progressivt detaljerat sätt. Detta kan ge intryck av att WCAG 2.1 är en mycket komplex uppsättning sammanlänkade dokument, men målet är att (stegvis) tillhandahålla mer detaljerad information när och när författarna behöver den - i stället för att skicka allt i ett mycket stort dokument.

WCAG 2.1 består av fyra huvudprinciper för hjälpmedelsanpassad design, som ibland kallas akronymen **POUR**. Dessa är:

1. **Perfekt**: Kan en användare känna av webbinnehållet i fråga?
1. **Användbar**: Kan en användare navigera, mata in data eller på annat sätt interagera med webbinnehållet?
1. **Förstå**: kan en användare bearbeta och förstå det webbinnehåll som presenteras för dem?
1. **Robust**: Är webbinnehållet tillgängligt på det sätt som är avsett för en mängd olika webbläsarmiljöer, inklusive äldre och kommande webbläsarmiljöer?

Så här utformar du:
* Varje **princip** består av en eller flera **riktlinjer**.

* Riktlinjer är skrivna som instruktioner, som antingen är positiva (gör det här..) eller negativa (gör inte det här..).
* Riktlinjerna är numrerade 1.1 till 4.1, där den första siffran motsvarar den överordnade principen.
* Varje riktlinje består av ett eller flera **kriterier**.
* Slutförandevillkor skrivs som programsatser, antingen `True` eller `False` för en given webbsida.
* Godkända villkor kan innehålla antingen eller alternativ, eller innehålla undantag; situationer där framgångskriterierna inte behöver uppfyllas.
* Godtagandekriterierna är numrerade enligt den överordnade riktlinjen och principen, från 1.1.1 till 4.1.1. De har också ett kort namn som sammanfattar syftet med kriteriet, så att det blir lättare att referera till det. Exempel: kriterium 1.1.1 är icke-text.
* Kriterierna för lyckade resultat innehåller en lista med relaterade **tekniker** (beskrivs mer ingående nedan).

## Stödresurser {#supporting-resources}

Förutom WCAG 2.1-huvudkomponenterna i principer, riktlinjer och kriterier för framgång finns det en rad styrkande dokument. Vissa av dem ger specifik rådgivning om hur man uppfyller vissa aspekter av riktlinjerna, andra är mer allmänna referenser som hjälper webbförfattare, designers och utvecklare av alla tänkbara möjligheter att förstå och använda WCAG 2.1 så effektivt som möjligt.

WCAG 2.1 är ett stabilt dokument och kommer inte att ändras, men de flesta av dessa stödresurser är dynamiska dokument. de kommer att förändras och växa med tiden, allt eftersom nya tekniker dyker upp, och nya exempel visas på hur webbtillgänglighet kan uppnås.

### WCAG 2.1-resurser {#wcag-resources}

Denna förteckning är inte avsedd att vara uttömmande, utan innehåller en introduktion till de tillgängliga resurserna:
* [En översikt över alla WCAG-relaterade dokument](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [En sammanfattning av de olika dokumenten](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [Nytt i WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [En snabbguide för hur man klarar WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [WCAG 2 Frågor och svar](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### Nyheter i WCAG 2.1 {#what-is-new}

[Nyheter i WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) ger värdefull information om Delta mellan WCAG och 2.0 och WCAG 2.1.

[WCAG 2.0 och 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) klargör ytterligare status för deras relation.

### Tekniker för WCAG 2.1 {#techniques-for-wcag}

Tekniker för WCAG 2.1 finns på sidan [Tekniker för WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/) .

**Tekniker** utgör nivån under framgångskriterierna i WCAG 2.1-hierarkin. De klassas av WAI som informativa, inte normativa. En specifik teknik behöver alltså inte följas för att en resurs ska uppfylla kraven i WCAG 2.1.

Eftersom tekniker är mycket mer specifika än framgångskriterier avser de vanligtvis en viss teknik eller innehållstyp (t.ex. HTML, eller video), eller en situation (t.ex. e-handel eller e-learning-program). Ni kan tänka på tekniker som beprövade exempel på hur specifika riktlinjer och framgångskriterier kan uppfyllas, så de är till stor hjälp för skribenter och utvecklare som arbetar i särskilda sammanhang.

Du kan komma åt tekniker:

* Genom samling (tekniker kan vara allmänna eller relaterade till en viss teknik eller ett visst format, t.ex. HTML, CSS eller Klientskript), eller
* Från relaterade resultatkriterier. Tekniker kan tillämpas på mer än ett framgångsvillkor.

Varje teknik har ett unikt nummer som relaterar till dess samling. En av ARIA-teknikerna är till exempel *Technique ARIA2: Identifiera obligatoriska fält med egenskapen*&quot;required&quot;.

Tekniker kan vara tillräckliga, rådgivande eller ett fel:

* En *Tillräcklig teknik* är en teknik som, om den följs, kommer att vara tillräcklig för att uppfylla ett visst kriterium för framgång.
* En *rådgivande teknik* är en teknik som, om den följs, kommer att ha en positiv inverkan på tillgängligheten, men kanske inte i sig räcker för att säkerställa att ett visst kriterium uppfylls.
* Ett *fel* är en teknik som beskriver ett specifikt exempel på var ett lyckat villkor inte uppfylls.

Detaljer om tekniker omfattar en beskrivning, tillämplighet, exempel, resurser för mer information och detaljer om hur författare kan testa att tekniken har tillämpats korrekt.

Listan över tekniker är inte fullständig och WAI uppdaterar hela tiden listan med nya exempel, som avspeglar utvecklingen inom webbteknik, designstrategier och forskningsresultat. Det är därför mycket värt att regelbundet kontrollera listan över tekniker för nya tillägg.

### Om WCAG 2.1 {#understanding-wcag}

Det handlar om ett antal dokument som innehåller råd som hjälper läsarna att förstå syftet med specifika riktlinjer och kriterier för framgång. Du kan [ladda ned en introduktion samt länkar till mer detaljerad information](https://www.w3.org/WAI/WCAG21/Understanding/).

Varje enskild riktlinje och kriterium för framgång har också en egen&quot;Förstå&quot;-sida med information om:

* Riktlinjens syfte.
* Särskilda kriterier för framgång.
* Rådgivande tekniker, som hjälper till att uppfylla kraven i riktlinjen, men som inte omfattas av något särskilt kriterium för framgång.

Varje resultatkriteris sida för&quot;förståelse&quot; innehåller information om:

* Framgångskriteriets avsikt.
* Allmänna exempel på hur kriteriet om framgång kan uppfyllas.
* Relaterade (icke-W3C) resurser om hur man uppfyller kriteriet för framgång.
* Teknik och fel: specifika och detaljerade exempel på hur kriteriet om framgång kan uppfyllas (beskrivs närmare nedan)
* Viktiga termer - en ordlista med termer som är viktiga för att förstå kriteriet för framgång.

Ett exempel finns på: Om [resultatvillkor 1.1.1 (&quot;Innehåll som inte är text&quot;)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content).

### Så här uppfyller du WCAG 2.1 {#how-to-meet-wcag}

Avsnittet&quot;Hur du uppfyller kraven&quot; finns på sidan [How To Meet WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/) . I detta avsnitt ges en alternativ presentation av WCAG, som gör det möjligt att förfina innehållet i riktlinjerna till de som är mest relevanta för en läsares egna intressen eller omständigheter. Läsare kan filtrera de framgångskriterier som de vill visa genom att ange särskilda tekniker för webbinnehåll, t.ex. Cascading Style Sheets eller skript, eller genom att ange en eller flera prioritetsnivåer.

Utan filtrering ger den här resursen alla resultatkriterier grupperade efter riktlinjer. För varje kriterium för framgång anges följande:

* Texten till kriteriet om framgång.
* En länk till motsvarande dokument om&quot;förståelse&quot;.
* En förteckning över besläktade tillräckligt effektiva tekniker som knyter till detaljerna om varje teknik.
* En förteckning över tillhörande rådgivningstekniker som knyter till detaljer om varje teknik (om sådan finns).
* En lista med relaterade fel som länkar till information om varje fel.
