---
title: Aktivera progressiva webbprogramfunktioner
description: AEM Sites gör det möjligt för innehållsförfattaren att aktivera progressiva webbprogramfunktioner för alla webbplatser genom enkel konfiguration istället för kodning.
exl-id: 1552a4ce-137a-4208-b7f6-2fc06db8dc39
source-git-commit: c31f43986e44099a3a36cc6c9c2f1a7251499ffb
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# Aktivera progressiva webbprogramfunktioner {#enabling-pwa}

Genom en enkel konfiguration kan en innehållsförfattare nu aktivera progressiva webbappsfunktioner (PWA) för upplevelser som skapats i AEM Sites.

>[!CAUTION]
>
>Det här är en avancerad funktion som kräver:
>
>* Kunskap om PWA
>* Kunskap om er webbplats och innehållsstruktur
>* Förståelse av cachelagringsstrategier
>* Support från ditt utvecklingsteam
>
>Innan du använder den här funktionen rekommenderar Adobe att du diskuterar detta med ditt utvecklingsteam för att definiera det bästa sättet att använda den i ditt projekt.

## Introduktion {#introduction}

[Progressiva webbprogram (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) möjliggör engagerande appliknande upplevelser för AEM sajter genom att de kan lagras lokalt på användarens dator och vara tillgängliga offline. Användaren kan surfa på en webbplats när han/hon är på språng även om han/hon förlorar en internetanslutning. PWA ger en sömlös upplevelse även om nätverket förloras eller blir instabilt.

I stället för att kräva någon kodning av webbplatsen kan en innehållsförfattare konfigurera PWA-egenskaper som en extra flik i [sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md) för en webbplats.

* När konfigurationen sparas eller publiceras aktiveras en händelsehanterare som skriver ut [manifestfiler](https://developer.mozilla.org/en-US/docs/Web/Manifest) och [servicearbetare](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) som möjliggör funktioner i PWA på webbplatsen.
* Samlingsmappningar upprätthålls också för att säkerställa att servicearbetaren hanteras från programmets rot för att aktivera proxinginnehåll som tillåter offlinefunktioner i appen.

Med PWA har användaren en lokal kopia av webbplatsen, vilket ger en appliknande upplevelse även utan internetanslutning.

>[!NOTE]
>
>Progressiva webbprogram är en teknik som utvecklas och har stöd för installation av lokala appar och andra funktioner [beroende på vilken webbläsare du använder.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Tutorials/js13kGames/Installable_PWAs#summary)

## Förutsättningar {#prerequisites}

För att du ska kunna använda PWA-funktioner för din webbplats finns det två krav för din projektmiljö:

1. [Använd kärnkomponenter](#adjust-components) för att utnyttja den här funktionen
1. [Justera din Dispatcher](#adjust-dispatcher) regler för att visa de filer som krävs

Detta är tekniska steg som författaren måste samordna med utvecklingsteamet. De här stegen krävs bara en gång per plats.

### Använd kärnkomponenter {#adjust-components}

Core Components version 2.15.0 och senare har fullt stöd för PWA-funktionerna i AEM. Eftersom AEMaaCS alltid innehåller den senaste versionen av de centrala komponenterna kan du använda PWA-funktioner direkt. Ditt AEMaaCS-projekt uppfyller automatiskt detta krav.

>[!NOTE]
>
>Adobe rekommenderar inte att du använder PWA-funktionerna i anpassade komponenter eller komponenter som inte [utökas från kärnkomponenterna.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) which supports the PWA features.

 To do this, the developer adds the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer also adds the following link to the `customfooterlibs.html` file of your page component.

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
-->

### Justera utskickaren {#adjust-dispatcher}

Funktionen PWA genererar och använder `/content/<sitename>/manifest.webmanifest` filer. Som standard [Dispatcher](/help/implementing/dispatcher/overview.md) sådana filer visas inte i . För att dessa filer ska kunna visas måste utvecklaren lägga till följande konfiguration i platsprojektet.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

Beroende på vilket projekt du arbetar med kanske du vill inkludera olika typer av tillägg till reglerna för omskrivning. The `webmanifest` tillägg kan vara användbart för att inkludera i omskrivningsvillkoren när du introducerar en regel som döljer och omdirigerar begäranden till `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## Aktivera PWA för din webbplats {#enabling-pwa-for-your-site}

Med [förutsättningarna](#prerequisites) är det enkelt för en innehållsförfattare att aktivera PWA-funktioner för en webbplats. Här följer en grundläggande beskrivning av hur du gör detta. Enskilda alternativ beskrivs i avsnittet [Detaljerade alternativ.](#detailed-options)

1. Logga in i AEM.
1. Tryck eller klicka på huvudmenyn **Navigering** -> **Webbplatser**.
1. Välj ditt webbplatsprojekt och tryck eller klicka [**Egenskaper**](/help/sites-cloud/authoring/fundamentals/page-properties.md) eller använda snabbtangenten `p`.
1. Välj **Progressiv webbapp** och konfigurera tillämpliga egenskaper. Du vill åtminstone:
   1. Välj alternativet **Aktivera PWA**.
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

1. Tryck eller klicka **Spara och stäng**.

Din plats har nu konfigurerats och du kan [installera det som en lokal app.](#using-pwa-enabled-site)

## Använda din PWA-aktiverade webbplats {#using-pwa-enabled-site}

Nu när du har [konfigurerade din webbplats för stöd för PWA,](#enabling-pwa-for-your-site) kan du uppleva det själv.

1. Åtkomst till webbplatsen i en [webbläsare](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Tutorials/js13kGames/Installable_PWAs#summary).
1. En ny ikon visas i webbläsarens adressfält, vilket anger att webbplatsen kan installeras som en lokal app.
   * Ikonen kan variera beroende på webbläsaren och webbläsaren kan även visa ett meddelande (t.ex. en banderoll eller dialogruta) som anger att det går att installera som en lokal app.
1. Installera programmet.
1. Appen installeras på enhetens startskärm.
1. Öppna appen, bläddra lite och se att sidorna är tillgängliga offline.

## Detaljerade alternativ {#detailed-options}

I följande avsnitt beskrivs alternativen mer ingående när [konfigurerar webbplatsen för PWA.](#enabling-pwa-for-your-site)

### Konfigurera installerbar upplevelse {#configure-installable-experience}

Med de här inställningarna kan din webbplats bete sig som ett systemspecifikt program genom att göra den installerbar på besökarens hemskärm och tillgänglig offline.

* **Aktivera PWA** - Det här är huvudväxeln för att aktivera PWA för webbplatsen.
* **Start-URL** - Det här är [önskad start-URL](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) som appen öppnas när användaren läser in det lokalt installerade programmet.
   * Detta kan vara vilken sökväg som helst i innehållsstrukturen.
   * Detta behöver inte vara roten och är ofta en dedikerad välkomstsida för programmet.
   * Om den här URL:en är relativ används manifest-URL:en som bas-URL:en för att matcha den.
   * När funktionen är tom används adressen till den webbsida som appen installerades från.
   * Vi rekommenderar att du anger ett värde.
* **Visningsläge** - En app med stöd för PWA är fortfarande en AEM webbplats som levereras via en webbläsare. [Dessa visningsalternativ](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) definierar hur webbläsaren ska döljas eller på annat sätt visas för användaren på den lokala enheten.
   * **Fristående** - Webbläsaren är dold för användaren och den ser ut som ett inbyggt program. Det här är standardvärdet.
      * Med det här alternativet måste appnavigering vara möjlig helt och hållet via ditt innehåll med hjälp av länkar och komponenter på webbplatsens sidor, utan att webbläsarens navigeringskontroller används.
   * **Webbläsare** - Webbläsaren ser ut som vanligt när du besöker webbplatsen.
   * **Minimalt användargränssnitt** - Webbläsaren är oftast dold, som ett inbyggt program, men grundläggande navigeringskontroller visas.
   * **Helskärm** - Webbläsaren är dold, precis som ett inbyggt program, men återges i helskärmsläge.
      * Med det här alternativet måste appnavigering vara möjlig helt och hållet via ditt innehåll med hjälp av länkar och komponenter på webbplatsens sidor, utan att webbläsarens navigeringskontroller används.
* **Skärmorientering** - Som lokal app måste PWA kunna hantera [enhetsorienteringar](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation).
   * **Alla** - Appen justeras efter orienteringen för användarens enhet. Det här är standardvärdet.
   * **Stående** - Detta tvingar programmet att öppnas i stående format oavsett orientering för användarens enhet.
   * **Liggande** - Detta tvingar programmet att öppnas i liggande format oavsett orientering för användarens enhet.
* **Temafärg** - Detta definierar [appens färg](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) som påverkar hur den lokala användarens operativsystem visar det inbyggda verktygsfältet och navigeringskontrollerna. Beroende på webbläsaren kan det påverka andra presentationselement i programmet.
   * Använd popup-fönstret för färgpaletter för att välja en färg.
   * Färgen kan också definieras med hex- eller RGB-värde.
* **Bakgrundsfärg** - Detta definierar [appens bakgrundsfärg](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color), som visas när appen läses in.
   * Använd popup-fönstret för färgpaletter för att välja en färg.
   * Färgen kan också definieras med hex- eller RGB-värde.
   * Vissa webbläsare [skapa en startskärm automatiskt](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) från programnamnet, bakgrundsfärgen och ikonen.
* **Ikon** - Detta definierar [ikonen](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) som representerar appen på användarens enhet.
   * Ikonen måste vara en PNG-fil med storleken 512x512 pixlar.
   * Ikonen måste vara [lagras i DAM](/help/assets/overview.md).

### Cachehantering (avancerat) {#offline-configuration}

Dessa inställningar gör delar av den här webbplatsen tillgängliga offline och lokalt på besökarens enhet. På så sätt kan du styra cacheminnet för webbprogrammet för att optimera nätverksförfrågningar och stödja offlineupplevelser.

* **Cachelagringsstrategi och uppdateringsfrekvens för innehåll** - Den här inställningen definierar cachningsmodellen för PWA.
   * **Måttligt** - [Den här inställningen](https://web.dev/stale-while-revalidate/) är ett standardvärde för de flesta webbplatser.
      * Med den här inställningen läses det innehåll som först visas av användaren in från cacheminnet, och medan användaren konsumerar det innehållet valideras resten av innehållet i cacheminnet.
   * **Ofta** - Detta gäller webbplatser som behöver uppdateras snabbt, till exempel auktionslokaler.
      * Med den här inställningen söker programmet först efter det senaste innehållet via nätverket, och om det inte är tillgängligt återgår det till den lokala cachen.
   * **Sällan** - Detta gäller för webbplatser som är nästan statiska, t.ex. referenssidor.
      * Med den här inställningen söker programmet först efter innehållet i cachen och om det inte är tillgängligt återgår det till nätverket för att hämta det.
* **Förcachelagring av filer** - Dessa filer som lagras på AEM sparas i den lokala webbläsarcachen när servicearbetaren installeras och innan de används. Detta garanterar att webbprogrammet fungerar som det ska när det är offline.
* **Baninkluderingar** - Nätverksförfrågningar för de definierade sökvägarna fångas upp och cachelagrat innehåll returneras i enlighet med den konfigurerade **Cachelagringsstrategi och uppdateringsfrekvens för innehåll**.
* **Cacheundantag** - Dessa filer cachelagras aldrig oavsett inställningarna under **Förcachelagring av filer** och **Inkluderingar av sökväg**.

>[!TIP]
>
>Utvecklarteamet har troligen värdefulla synpunkter på hur offlinekonfigurationen ska konfigureras.

## Begränsningar och Recommendations {#limitations-recommendations}

Alla PWA-funktioner är inte tillgängliga för AEM Sites. Det här är några tydliga begränsningar.

* Sidorna synkroniseras inte automatiskt eller uppdateras inte om användaren inte använder appen.

Adobe rekommenderar även följande när du implementerar PWA.

### Minimera antalet resurser som ska förcachas. {#minimize-precache}

Adobe rekommenderar att du begränsar antalet sidor som ska förcachas.

* Bädda in bibliotek så att du kan minska antalet poster som ska hanteras vid förcachelagring.
* Begränsa antalet bildvariationer till förcache.

### Aktivera PWA efter att projektskript och formatmallar har stabiliserats. {#pwa-stabilized}

Klientbibliotek levereras med en cacheväljare som har följande mönster `lc-<checksumHash>-lc`. Varje gång en av filerna (och beroenden) som utgör ett bibliotek ändras den här väljaren. Om du har listat ett klientbibliotek som ska cachas i förväg av servicechef och vill referera till en ny version, hämtar och uppdaterar du posten manuellt. Därför rekommenderar Adobe att du konfigurerar platsen till PWA efter att projektskripten och formatmallarna har stabiliserats.

### Minimera antalet bildvariationer. {#minimize-variations}

Bildkomponenten för AEM Core Components avgör den översta delen av den bästa återgivningen som ska hämtas. Den här mekanismen innehåller också en tidsstämpel som motsvarar den senaste ändringstiden för resursen. Den här mekanismen komplicerar konfigurationen av förcache-minnet för PWA.

När användaren konfigurerar pre-cache måste han/hon visa alla sökvägsvariationer som kan hämtas. Dessa variationer består av parametrar som kvalitet och bredd. Vi rekommenderar att du minskar antalet av dessa variationer till högst tre - liten, medel, stor. Det kan du göra med hjälp av dialogrutan för innehållsprincip i dialogrutan [Bildkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html).

Om den inte konfigureras noggrant kan minnes- och nätverkskonsumtionen påverka PWA prestanda negativt. Om du tänker skapa t.ex. 50 bilder framför varandra och har tre bredder per bild, måste användaren som underhåller webbplatsen ha en lista med upp till 150 poster i PWA-avsnittet för förhandscache i sidegenskaperna.

Adobe rekommenderar också att du konfigurerar webbplatsen till PWA efter att projektanvändningen av bilder har stabiliserats.
