---
title: En snabbguide till WCAG 2.0
seo-title: En snabbguide till WCAG 2.0
translation-type: tm+mt
source-git-commit: 039b926ca0775979430c70c96ae77d0eaa5662b3

---


# En snabbguide till WCAG 2.0{#quick-guide-to-wcag}

AEM har utvecklats för att maximera kompatibiliteten med Web Content Accessibility Guidelines:

WCAG2 ( [Web Content Accessibility Guidelines version 2.0)](https://www.w3.org/TR/WCAG/) är en uppsättning internationellt erkända riktlinjer som tagits fram av [World Wide Web Consortium (W3C)](https://www.w3.org/) inom ramen för deras [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/).

WCAG 2.0 består av en uppsättning teknikoberoende riktlinjer och framgångskriterier som gör webbinnehåll tillgängligt för och användbart för personer med funktionshinder. De ger råd till webbinnehållsförfattare, designers och utvecklare om att se till att de resurser de producerar är så tillgängliga som möjligt för så många människor som möjligt, oavsett vilka funktionshinder de har. t.ex. synnedsättning, hörselbortfall, inlärningssvårigheter, åldersrelaterade begränsningar.

Om du till exempel beskriver en bild (eller något annat innehåll som inte är text) genom att använda attributet `alt` i HTML blir det till stor fördel för personer som är blinda eller som är synkade delvis. Textbeskrivningen i attributet kan antingen konverteras till talutdata eller överföras till elektroniska, uppdateringsbara blindskriftsskärmar. `alt`

Dessutom kan WCAG 2.0 leda till fördelar för andra mottagare, inklusive personer som kan anses vara *tillfälligt inaktiverade*. Personer som på grund av omständigheter som surfteknik, nätverksanslutningshastighet eller surfmiljö kan uppleva hinder som liknar personer med funktionshinder.

Med Adobe Experience Manager kan skribenter och/eller webbplatsägare skapa webbinnehåll som uppfyller relevanta kriterier för WCAG 2.0-nivå A och nivå AA.

Därför är det viktigt att förstå syftet med WCAG 2.0 och hur riktlinjerna är upplagda för att förstå webbtillgänglighet och hur riktlinjerna kan hjälpa till att skapa tillgängligt webbinnehåll.

WCAG 2.0 har för avsikt att ge riktlinjer som

* Är **teknikagnostiska:**

Riktlinjer som kan tillämpas på en rad olika webbinnehållsformat, inte bara HTML. WCAG 2.0 kan alltså omfatta innehåll som genereras av eller tillhandahålls i PDF, Flash, JavaScript och andra befintliga och framtida webbtekniker. Detta syftar till att åtgärda en svaghet i WCAG 1.0, eftersom det fokuserades på HTML på bekostnad av andra webbinnehållsformat.

* Kan **testas:**

Varje riktlinje är skriven på ett sådant sätt att den kan testas objektivt för att säkerställa att en grupp experter på tillgänglighet i allmänhet håller med om att riktlinjen har följts. En av utmaningarna med riktlinjerna för tillgänglighet är att vissa, även om de kan vara tekniskt testbara, andra kräver en mänsklig bedömning för att avgöra om riktlinjerna har följts eller inte. WCAG 2.0 har skrivits i syfte att minska den subjektivitet som fanns i vissa av WCAG 1.0-riktlinjerna och kontrollpunkterna.

* Stöd för **prioriterad och sammanhangsbaserad implementering:**

Precis som i WCAG 1.0 ges WCAG 2.0-riktlinjerna prioriteringar som rör den troliga effekten av att inte följa en riktlinje för en viss grupp användare med funktionshinder. Detta gör det möjligt för författare att fatta ett välgrundat beslut om de viktigaste riktlinjerna för sin särskilda situation. Dessutom introduceras begreppet *tillgänglighet som stöds* . Detta gör att författare kan fatta beslut om hur de bäst använder webbtekniker som kanske inte har fullständigt stöd för tillgänglighet eller som kan kräva att användarna har särskilda hjälpmedelstekniker och/eller webbläsare för att kunna utnyttja tillgänglighetsfunktionerna.

Dessa mål har i hög grad påverkat strukturen i WCAG 2.0.

>[!NOTE]
>
>Det går inte att skapa en webbplats som tar hänsyn till alla tänkbara funktionshinder eller persontyper. Syftet med WCAG 2.0 är att hjälpa webbutvecklare att skapa webbplatser som så långt det är möjligt är tillgängliga under vissa förhållanden och inom vissa ramar.

>[!NOTE]
>
>Om du känner till WCAG 1.0 kommer du att märka vissa förändringar i WCAG 2.0. De rör omfattning, organisation och mål.

## Struktur {#structure}

WCAG 2.0 är strukturerat på ett sätt som introducerar koncept för att skapa tillgängligt webbinnehåll på ett progressivt detaljerat sätt. Detta kan ge intryck av att WCAG 2.0 är en mycket komplex uppsättning sammanlänkade dokument, men målet är att (stegvis) tillhandahålla mer detaljerad information när och när författarna behöver den - istället för att skicka allt i ett mycket stort dokument.

WCAG 2.0 består av fyra huvudprinciper för hjälpmedelsanpassad design. Dessa är:

1. **Perfekt**: Kan en användare känna av webbinnehållet i fråga?
1. **Användbar**: Kan en användare navigera, mata in data eller på annat sätt interagera med webbinnehållet?
1. **Förstå**: kan en användare bearbeta och förstå det webbinnehåll som presenteras för dem?
1. **Robust**: Är webbinnehållet tillgängligt på det sätt som är avsett för en mängd olika webbläsarmiljöer, inklusive äldre och kommande webbläsarmiljöer?

Dessa principer kallas ibland akronymen POUR.

* Varje **princip** består av en eller flera **riktlinjer**.

* Riktlinjer är skrivna som instruktioner, som antingen är positiva (gör det här..) eller negativa (gör inte det här..).
* Riktlinjerna är numrerade 1.1 till 4.1, där den första siffran motsvarar den överordnade principen.

* Varje riktlinje består av ett eller flera **kriterier**.

* Slutförandevillkor skrivs som programsatser, antingen `True` eller `False` för en given webbsida.
* Godkända villkor kan innehålla antingen eller alternativ, eller innehålla undantag; situationer där framgångskriterierna inte behöver uppfyllas.
* Godtagandekriterierna är numrerade enligt den överordnade riktlinjen och principen, från 1.1.1 till 4.1.1. De har också ett kort namn som sammanfattar syftet med kriteriet, så att det blir lättare att referera till det. Exempel: kriterium 1.1.1 är icke-text.
* Kriterierna för lyckade resultat innehåller en lista med relaterade **tekniker** (beskrivs mer ingående nedan).

## Stödresurser {#supporting-resources}

Förutom de viktigaste delarna i WCAG 2.0 i principer, riktlinjer och kriterier för framgång finns det en rad styrkande dokument. Vissa av dem ger specifik rådgivning om hur man uppfyller vissa aspekter av riktlinjerna, andra är mer allmänna referenser som hjälper webbförfattare, designers och utvecklare av alla tänkbara möjligheter att förstå och använda WCAG 2.0 så effektivt som möjligt.

WCAG 2.0 är ett stabilt dokument och kommer inte att ändras, men de flesta av dessa resurser är dynamiska dokument. de kommer att förändras och växa med tiden, allt eftersom nya tekniker dyker upp, och nya exempel visas på hur webbtillgänglighet kan uppnås.

### WCAG 2.0-resurser {#wcag-resources}

* [En översikt över alla WCAG 2.0-relaterade dokument](https://www.w3.org/WAI/intro/wcag.php).
* [Förklaring av hur olika komponenter relaterar till varandra](https://www.w3.org/WAI/intro/wcag20).
* [WCAG 2.0 Frågor och svar](https://www.w3.org/WAI/WCAG20/wcag2faq.html);

### Tekniker för WCAG 2.0 {#techniques-for-wcag}

Tekniker för WCAG 2.0 finns på sidan [Tekniker för WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/) .

**Tekniker** utgör nivån nedan för framgångsvillkor i WCAG 2.0-hierarkin. De klassas av WAI som informativa, inte normativa. En specifik teknik behöver alltså inte följas för att en resurs ska uppfylla kraven i WCAG 2.0.

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

### Om WCAG 2.0 {#understanding-wcag}

Det handlar om ett antal dokument som innehåller råd som hjälper läsarna att förstå syftet med specifika riktlinjer och kriterier för framgång. Du kan [ladda ned en introduktion samt länkar till mer detaljerad information](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/Overview.html).

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

Ett exempel finns på: Om [resultatvillkor 1.1.1 (&quot;Innehåll som inte är text&quot;)](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/text-equiv-all.html).

### Så här uppfyller du WCAG 2.0 {#how-to-meet-wcag}

Avsnittet&quot;Hur du uppfyller kraven&quot; finns på [sidan How To Meet WCAG 2.0](https://www.w3.org/WAI/WCAG20/quickref/) . I detta avsnitt ges en alternativ presentation av WCAG, som gör det möjligt att förfina innehållet i riktlinjerna till de som är mest relevanta för en läsares egna intressen eller omständigheter. Läsare kan filtrera de framgångskriterier som de vill visa genom att ange särskilda tekniker för webbinnehåll, t.ex. Cascading Style Sheets eller skript, eller genom att ange en eller flera prioritetsnivåer.

Utan filtrering ger den här resursen alla resultatkriterier grupperade efter riktlinjer. För varje kriterium för framgång anges följande:

* Texten till kriteriet om framgång.
* En länk till motsvarande dokument om&quot;förståelse&quot;.
* En förteckning över besläktade tillräckligt effektiva tekniker som knyter till detaljerna om varje teknik.
* En förteckning över tillhörande rådgivningstekniker som knyter till detaljer om varje teknik (om sådan finns).
* En lista med relaterade fel som länkar till information om varje fel.