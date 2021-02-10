---
title: Aktivera progressiva webbprogramfunktioner
description: AEM Sites gör det möjligt för innehållsförfattaren att aktivera progressiva webbprogramfunktioner för alla webbplatser genom enkel konfiguration istället för kodning.
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 071eefa3b6f5e9636ace612e968b6a9627c98550
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 0%

---


# Aktivera progressiva webbprogramfunktioner {#enabling-pwa}

Genom en enkel konfiguration kan en innehållsförfattare nu aktivera progressiva webbprogramfunktioner (PWA) för upplevelser som skapats i AEM Sites.

>[!CAUTION]
>
>Det här är en avancerad funktion som kräver:
>
>* Kunskap om PWA
>* Kunskap om er webbplats och innehållsstruktur
>* Förståelse av cachelagringsstrategier
>* Support från ditt utvecklingsteam

>
>
Innan du använder den här funktionen bör du diskutera detta med utvecklingsteamet för att definiera det bästa sättet att utnyttja den i ditt projekt.

## Introduktion {#introduction}

[Progressiva webbappar (PWA) ](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) möjliggör engagerande appliknande upplevelser för AEM sajter genom att de kan lagras lokalt på användarens dator och vara tillgängliga offline. Användaren kan surfa på en webbplats när han/hon är på språng även om han/hon förlorar en internetanslutning. PWA tillåter sömlösa upplevelser även om nätverket förloras eller är instabilt.

I stället för att kräva omkodning av webbplatsen kan en innehållsförfattare konfigurera PWA-egenskaper som en extra flik i [sidegenskaperna](/help/sites-cloud/authoring/fundamentals/page-properties.md) för en plats.

* När konfigurationen sparas eller publiceras utlöses en händelsehanterare som skriver ut [manifestfilerna](https://developer.mozilla.org/en-US/docs/Web/Manifest) och [servicearbetaren](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) som aktiverar PWA-funktioner på platsen.
* Manifest- och servicearbetaren lagras i [kontextmedveten konfiguration](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) som gäller för platsen. Samlingsmappningar upprätthålls också för att säkerställa att servicearbetaren hanteras från programmets rot för att aktivera proxinginnehåll som tillåter offlinefunktioner i appen.

Med PWA har användaren en lokal kopia av webbplatsen, vilket ger en appliknande upplevelse även utan internetanslutning.

>[!NOTE]
>
>Progressiva webbprogram är en teknik som utvecklas och stöd för installation av lokala appar och andra funktioner [beror på vilken webbläsare du använder.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Förutsättningar {#prerequisites}

För att du ska kunna använda PWA-funktioner för din webbplats finns det två krav för din projektmiljö:

1. [Justera dina ](#adjust-components) komponenter för att aktivera den här funktionen
1. [Justera ](#adjust-dispatcher) skickade regler för att visa de filer som behövs

Detta är tekniska steg som författaren måste samordna med utvecklingsteamet. Dessa steg krävs bara en gång per plats.

### Justera dina komponenter {#adjust-components}

Komponenterna måste innehålla [manifestfilerna](https://developer.mozilla.org/en-US/docs/Web/Manifest) och [servicearbetaren](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) som stöder PWA-funktionerna.

För att göra detta måste utvecklaren lägga till följande länk till `customheaderlibs.html`-filen för sidkomponenten.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

Utvecklaren måste också lägga till följande länk till `customfooterlibs.html`-filen för sidkomponenten.

```xml
<script>
        // Check that service workers are supported
        if ('serviceWorker' in navigator) {
            // Use the window load event to make sure the page load performs well
            window.addEventListener('load', () => {
                let serviceWorker = '/<projectName>sw.js';
                navigator.serviceWorker.register(serviceWorker);
            });
        }
</script>
```

>[!NOTE]
>
>I framtida versioner av [kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) inkluderas dessa funktioner automatiskt. Men om du använder anpassade komponenter i stället för kärnkomponenter kommer dessa justeringar alltid att krävas.

### Justera din Dispatcher {#adjust-dispatcher}

Funktionen PWA genererar och använder `/content/<sitename>/manifest.webmanifest`-filer. Som standard visar [dispatchern](/help/implementing/dispatcher/overview.md) inte sådana filer. För att dessa filer ska kunna visas måste utvecklaren lägga till följande konfiguration i platsprojektet.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

>[!NOTE]
>
>I framtida versioner av [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en#developing) inkluderas den här konfigurationen.

## Aktivera PWA för din webbplats {#enabling-pwa-for-your-site}

När [förutsättningarna](#prerequisites) är uppfyllda är det mycket enkelt för en innehållsförfattare att aktivera PWA-funktioner för en webbplats. Här följer en grundläggande beskrivning av hur du gör detta. Enskilda alternativ beskrivs i avsnittet [Detaljerade alternativ.](#detailed-options)

1. Logga in i AEM.
1. Tryck eller klicka på **Navigering** -> **Platser** på huvudmenyn.
1. Välj ditt webbplatsprojekt och tryck eller klicka på [**Egenskaper**](/help/sites-cloud/authoring/fundamentals/page-properties.md) eller använd snabbtangenten `p`.
1. Välj fliken **Progressiv webbapp** och konfigurera tillämpliga egenskaper. Du vill åtminstone:
   1. Markera alternativet **Aktivera PWA**.
   1. Definiera **Start-URL**.

      ![Aktivera PWA](../assets/pwa-enable.png)

   1. Överför en 512x512-png-ikon till DAM och referera till den som programikonen.

      ![Definiera PWA-ikon](../assets/pwa-icon.png)

   1. Konfigurera de sökvägar som du vill att tjänstarbetaren ska arbeta offline. Vanliga sökvägar är:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Alla teckensnittsreferenser från tredje part
      * `/etc/clientlibs/<sitename>`

      ![Definiera offlinesökvägar för PWA](../assets/pwa-offline.png)


1. Tryck eller klicka på **Spara och stäng**.

Platsen är nu konfigurerad och du kan [installera den som en lokal app.](#using-pwa-enabled-site)

## Använda din PWA-aktiverade webbplats {#using-pwa-enabled-site}

Nu när du har [konfigurerat din webbplats för att stödja PWA](#enabling-pwa-for-your-site) kan du uppleva den själv.

1. Gå till webbplatsen i en [webbläsare som stöds.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. En `+`-ikon visas i webbläsarens adressfält, vilket anger att webbplatsen kan installeras som en lokal app.
   * Beroende på webbläsaren kan det även visas ett meddelande (t.ex. en banderoll eller dialogruta) som anger att det går att installera som en lokal app.
1. Installera programmet.
1. Appen installeras på enhetens startskärm.
1. Öppna appen, bläddra lite och se att sidorna är tillgängliga offline.

## Detaljerade alternativ {#detailed-options}

Följande avsnitt innehåller mer information om de alternativ som är tillgängliga när du konfigurerar platsen för PWA.](#enabling-pwa-for-your-site)[

### Konfigurera installerbar upplevelse {#configure-installable-experience}

Med de här inställningarna kan din webbplats bete sig som ett systemspecifikt program genom att göra den installerbar på besökarens hemskärm och tillgänglig offline.

* **Aktivera PWA**  - Det här är huvudreglaget för att aktivera PWA för webbplatsen.
* **Start-URL**  - Detta är den  [rekommenderade start-](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) URL:en som programmet öppnas när användaren läser in det lokalt installerade programmet.
   * Detta kan vara vilken sökväg som helst i innehållsstrukturen.
   * Detta behöver inte vara roten och är ofta en dedikerad välkomstsida för programmet.
   * Om den här URL:en är relativ används manifest-URL:en som bas-URL:en för att matcha den.
   * När funktionen är tom används adressen till webbsidan som webbappen installerades från.
   * Vi rekommenderar att du anger ett värde.
* **Visningsläge**  - En app med stöd för PWA är fortfarande en AEM webbplats som levereras via en webbläsare. [Dessa ](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) visningsalternativ definierar hur webbläsaren ska döljas eller på annat sätt visas för användaren på den lokala enheten.
   * **Fristående**  - Webbläsaren är helt dold för användaren och ser ut som en inbyggd app. Detta är standardvärdet.
      * Med det här alternativet måste appnavigering vara möjlig helt och hållet via ditt innehåll med hjälp av länkar och komponenter på webbplatsens sidor, utan att webbläsarens navigeringskontroller används.
   * **Webbläsare**  - Webbläsaren ser ut som vanligt när du besöker webbplatsen.
   * **Minimalt användargränssnitt**  - Webbläsaren är oftast dold, som ett systemspecifikt program, men grundläggande navigeringskontroller visas.
   * **Helskärm**  - Webbläsaren är helt dold, som ett inbyggt program, men den återges i helskärmsläge.
      * Med det här alternativet måste appnavigering vara möjlig helt och hållet via ditt innehåll med hjälp av länkar och komponenter på webbplatsens sidor, utan att webbläsarens navigeringskontroller används.
* **Skärmorientering**  - Som lokal app behöver PWA veta hur man hanterar  [enhetsorienteringar.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Valfritt**  - Appen justeras efter orienteringen för användarens enhet. Detta är standardvärdet.
   * **Stående**  - Detta tvingar programmet att öppnas i stående format oavsett orientering för användarens enhet.
   * **Liggande**  - Detta medför att programmet öppnas i liggande format oavsett orientering för användarens enhet.
* **Temafärg**  - Detta definierar  [färgen på ](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) appen som påverkar hur den lokala användarens operativsystem visar det inbyggda verktygsfältet och navigeringskontrollerna. Beroende på webbläsaren kan det påverka andra presentationselement i programmet.
   * Använd popup-fönstret för färgbrunn för att välja en färg.
   * Färgen kan också definieras med hex- eller RGB-värden.
* **Bakgrundsfärg**  - Detta definierar  [bakgrundsfärgen för programmet, ](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) som visas när programmet läses in.
   * Använd popup-fönstret för färgbrunn för att välja en färg.
   * Färgen kan också definieras med hex- eller RGB-värden.
   * I vissa webbläsare [skapas en välkomstskärm automatiskt](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) från programnamnet, bakgrundsfärgen och ikonen.
* **Ikon**  - Detta definierar  [den ](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) ikon som representerar appen på användarens enhet.
   * Ikonen måste vara en PNG-fil med storleken 512x512 pixlar.
   * Ikonen måste vara [lagrad i DAM.](/help/assets/overview.md)

### Cachehantering (avancerat) {#offline-configuration}

Dessa inställningar gör delar av den här webbplatsen tillgängliga offline och lokalt på besökarens enhet. På så sätt kan du styra cacheminnet för webbprogrammet för att optimera nätverksförfrågningar och stödja offlineupplevelser.

* **Cachelagringsstrategi och frekvens för innehållsuppdatering**  - Den här inställningen definierar cachningsmodellen för PWA.
   * **Måttligt**  -  [Den här ](https://web.dev/stale-while-revalidate/) inställningen gäller de flesta webbplatser och är standardvärdet.
      * Med den här inställningen läses det innehåll som först visas av användaren in från cacheminnet, och medan användaren konsumerar det innehållet kommer resten av innehållet i cacheminnet att omvalideras.
   * **Ofta**  - Detta är fallet för webbplatser som behöver uppdateras mycket snabbt, till exempel auktionslokaler.
      * Med den här inställningen söker programmet först efter det senaste innehållet via nätverket och om det inte är tillgängligt återgår det till den lokala cachen.
   * **Sällan**  - Detta gäller webbplatser som är nästan statiska, t.ex. referenssidor.
      * Med den här inställningen söker programmet först efter innehållet i cachen och om det inte är tillgängligt återställs det till nätverket för att hämta det.
* **Förcachelagring**  av filer - Dessa filer som lagras på AEM sparas i den lokala webbläsarcachen när servicearbetaren installerar och innan de används. Detta garanterar att webbprogrammet fungerar fullt ut offline.
* **Sökvägar omfattar**  - Nätverksbegäranden för de definierade sökvägarna fångas upp och det cachelagrade innehållet returneras i enlighet med den konfigurerade  **cachelagringsstrategin och frekvensen för innehållsuppdatering**.
* **Cacheundantag**  - Dessa filer kommer aldrig att cachelagras oavsett inställningarna under  **Inkludering av filer före** cachelagring och  **sökväg**.

>[!TIP]
>
>Utvecklarteamet har troligen värdefulla synpunkter på hur offlinekonfigurationen ska konfigureras.

## Begränsningar {#limitations}

Alla PWA-funktioner är inte tillgängliga för AEM Sites. Det här är några tydliga begränsningar.

* Användaren måste bläddra på sidan minst en gång innan den kan cachas offline.
* Sidorna synkroniseras inte automatiskt eller uppdateras inte om användaren inte använder appen.
