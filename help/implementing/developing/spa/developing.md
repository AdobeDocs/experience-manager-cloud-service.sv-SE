---
title: Utveckla SPA för AEM
description: I den här artikeln presenteras viktiga frågor som du bör tänka på när du engagerar en frontendutvecklare att utveckla ett SPA för AEM samt ger en översikt över AEM arkitektur när det gäller SPA som du bör tänka på när du driftsätter ett utvecklat SPA för AEM.
translation-type: tm+mt
source-git-commit: d0685af8b05d5491debf7bad99b5c8f111808f26
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 0%

---


# Utveckla SPA för AEM {#developing-spas-for-aem}

Single page applications (SPAs) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA-ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som skapats med sådana ramverk.

I den här artikeln finns viktiga frågor att tänka på när en frontutvecklare ska utveckla ett SPA för AEM och en översikt över AEM arkitektur när det gäller att driftsätta SPA på AEM.

## SPA:s utvecklingsprinciper för AEM {#spa-development-principles-for-aem}

Utveckla single page-applikationer AEM förutsätter att frontutvecklaren följer vedertagna standarder när han skapar en SPA. Om ni som frontendutvecklare följer dessa allmänna bästa metoder samt få AEM specifika principer, kommer er SPA att fungera med [AEM och dess innehållsredigeringsfunktioner](introduction.md#content-editing-experience-with-spa).

* **[Portabilitet](#portability)** - Precis som med andra komponenter bör komponenterna vara så portabla som möjligt. SPA bör byggas med rörliga och återanvändbara komponenter.
* **[AEM Drives Site Structure](#aem-drives-site-structure)** (Webbplatsstruktur) - Utvecklaren på frontsidan skapar komponenter och äger sin interna struktur, men använder AEM för att definiera webbplatsens innehållsstruktur.
* **[Dynamisk återgivning](#dynamic-rendering)** - All återgivning ska vara dynamisk.
* **[Dynamisk routning](#dynamic-routing)** - SPA ansvarar för routningen och AEM lyssnar på den och hämtar baserat på den. Alla routningar ska också vara dynamiska.

Om du håller dessa principer i åtanke när du utvecklar din SPA-fil kommer den att vara så flexibel och framtidssäkrad som möjligt samtidigt som du aktiverar alla funktioner för AEM som stöds.

Om du inte behöver ha stöd för AEM kan du behöva fundera på en annan [SPA-designmodell](#spa-design-models).

### Portabilitet {#portability}

Precis som när du utvecklar en komponent bör dina komponenter utformas på ett sådant sätt att de blir så bärbara som möjligt. Mönster som motverkar komponenternas bärbarhet eller återanvändbarhet bör undvikas för att säkerställa kompatibilitet, flexibilitet och underhållbarhet.

Den resulterande produktresumén bör byggas med mycket portabla och återanvändbara komponenter.

### AEM diskar platsstruktur {#aem-drives-site-structure}

Utvecklaren måste själv se sig själv som ansvarig för att skapa ett bibliotek med SPA-komponenter som används för att bygga appen. Utvecklaren har fullständig kontroll över komponenternas interna struktur. [AEM äger dock alltid platsens struktur.](editor-overview.md)

Det innebär att frontendutvecklaren kan lägga till kundinnehåll före eller efter startpunkten för komponenterna och även göra tredjepartsanrop inuti komponenten. Utvecklaren har dock inte fullständig kontroll över hur komponenterna kapslas, till exempel.

### Dynamisk återgivning {#dynamic-rendering}

SPA bör endast förlita sig på dynamisk återgivning av innehåll. Detta är standardförväntningen där AEM hämtar och återger alla underordnade element i innehållsstrukturen.

All explicit återgivning som pekar på visst innehåll betraktas som statisk återgivning och även om den stöds kommer den inte att vara kompatibel med AEM innehållsredigeringsfunktioner. Detta strider också mot principen om [bärbarhet](#portability).

### Dynamisk routning {#dynamic-routing}

Precis som vid återgivning ska all routning också vara dynamisk. I AEM ska [SPA alltid äga routningen](routing.md) och AEM lyssnar på den och hämtar innehåll baserat på den.

Statisk routning fungerar mot [principen om bärbarhet](#portability) och begränsar författaren genom att inte vara kompatibel med innehållsredigeringsfunktionerna i AEM. Om innehållsförfattaren till exempel vill ändra en väg eller ändra en sida med statisk routning måste han eller hon be den som skapar sidan att göra det.

## AEM Project Archetype {#aem-project-archetype}

Alla AEM ska utnyttja den [AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)som stöder SPA-projekt med React eller Angular och som utnyttjar SPA SDK.

## SPA-designmodeller {#spa-design-models}

Om [principerna för utveckling av SPA i AEM](#spa-development-principles-for-aem) följs, kommer SPA att fungera med alla AEM funktioner som stöds.

Det kan dock finnas fall där detta inte är helt nödvändigt. Tabellen nedan ger en översikt över de olika designmodellerna, deras fördelar och nackdelar.

<table>
 <tbody>
  <tr>
   <th><strong>Designmodell<br /> </strong></th>
   <th><strong>Fördelar</strong></th>
   <th><strong>Nackdelar</strong></th>
  </tr>
  <tr>
   <td>AEM används som headless CMS utan <a href="https://docs.adobe.com/content/help/en/experience-manager-65/developing/headless/spas/spa-reference-materials.html">SPA Editor SDK-ramverket.</a></td>
   <td>Utvecklaren har fullständig kontroll över appen.</td>
   <td><p>Innehållsförfattare kan inte utnyttja AEM upplevelse.</p> <p>Koden är varken flyttbar eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>Utvecklaren använder SPA Editor SDK-ramverket, men bara vissa områden öppnas för innehållsförfattaren.</td>
   <td>Utvecklaren behåller kontrollen över appen genom att endast aktivera redigering i begränsade delar av appen.</td>
   <td><p>Innehållsförfattare är begränsade till en begränsad uppsättning AEM upplevelser.</p> <p>Koden kan varken vara flyttbar eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>Projektet utnyttjar SPA Editor SDK fullt ut och klientkomponenterna utvecklas som ett bibliotek och innehållsstrukturen i programmet delegeras till AEM.</td>
   <td><p>Appen är återanvändbar och portabel.</p> <p>Innehållsförfattaren kan redigera appen med hjälp av AEM.<br /> </p> <p>SPA är kompatibelt med mallredigeraren.</p> </td>
   <td><p>Utvecklaren har inte kontroll över programmets struktur och den del av innehållet som har delegerats till AEM.</p> <p>Utvecklaren kan fortfarande reservera områden i programmet för innehåll som inte ska redigeras med AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Även om alla modeller stöds i AEM är det bara genom att implementera den tredje (och därmed följa de rekommenderade [SPA-utvecklingsprinciperna i AEM](#spa-development-principles-for-aem)) som innehållsförfattarna kan interagera med och redigera innehållet i SPA i AEM som de är vana vid.

## Migrera befintliga SPA till AEM {#migrating-existing-spas-to-aem}

I allmänhet om SPA följer [SPA-utvecklingsprinciperna för AEM](#spa-development-principles-for-aem)fungerar SPA i AEM och kan redigeras med AEM SPA-redigerare.

Följ de här stegen för att göra din befintliga SPA klar att arbeta med AEM.

1. **Gör dina JS-komponenter modulära.** - Gör dem kapabla att återges i valfri ordning, position och storlek.
1. **Använd behållarna från SDK för att placera dina komponenter på skärmen.** - AEM innehåller en sid- och styckesystemkomponent som du kan använda.
1. **Skapa en AEM för varje JS-komponent.** - AEM komponenter definierar dialogrutan och JSON-utdata.

## Instruktioner för gränssnittsutvecklare {#instructions-for-front-end-developers}

Den främsta uppgiften att engagera en frontutvecklare att skapa ett SPA för AEM är att komma överens om komponenterna och deras JSON-modeller.

Här följer en översikt över de steg som en frontendutvecklare måste följa när han eller hon utvecklar en SPA för AEM.

1. **Godkänn komponenterna och deras JSON-modell**

   Utvecklare och AEM måste komma överens om vilka komponenter som är nödvändiga och en modell så att det går att matcha SPA-komponenterna mot bakomliggande komponenter med en och samma komponent.

   AEM är fortfarande nödvändiga för att kunna tillhandahålla redigeringsdialogrutor och exportera komponentmodellen.

1. **I React-komponenter kommer du åt modellen via`this.props.cqModel`**

   När komponenterna är överenskomna och JSON-modellen är på plats kan frontendutvecklaren utveckla SPA och enkelt komma åt JSON-modellen via `this.props.cqModel`.

1. **Implementera komponentens`render()`metod**

   Utvecklaren implementerar metoden så som den passar och kan använda fälten för `render()` `cqModel` egenskapen. Detta genererar DOM- och HTML-fragmenten som ska infogas på sidan. Detta är standardsättet att bygga en app i React.

1. **Mappa komponenten till AEM-resurstypen via`MapTo()`**

   Mappningen lagrar komponentklasser och används internt av den angivna `Container` komponenten för att hämta och dynamiskt instansiera komponenter baserat på den angivna resurstypen.

   Det här fungerar som en&quot;limma&quot; mellan fram- och bakände så att redigeraren vet vilka komponenter som de olika reaktionskomponenterna motsvarar.

   De `Page` och `ResponsiveGrid` är bra exempel på klasser som utökar basen `Container`.

1. **Definiera komponentens`EditConfig`som parameter till`MapTo()`**

   Den här parametern är nödvändig för att tala om för redigeraren hur komponenten ska namnges så länge som den inte har återgetts eller inte har något innehåll att återge.

1. **Utöka den angivna`Container`klassen för sidor och behållare**

   Sidor och styckesystem bör utöka den här klassen så att delegering till inre komponenter fungerar som förväntat.

1. **Implementera en routningslösning som använder HTML5-`History`API.**

   När `ModelRouter` funktionen är aktiverad, kommer anrop av `pushState` och `replaceState` funktioner att utlösa en begäran till användaren om `PageModelManager` att hämta ett saknat fragment av modellen.

   Den aktuella versionen av det `ModelRouter` enda stödet för användning av URL:er som pekar på den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av vanity-URL:er eller alias.

   Den `ModelRouter` kan inaktiveras eller konfigureras för att ignorera en lista med reguljära uttryck.

## AEM {#aem-agnostic}

Dessa kodblock visar hur dina React- och Angular-komponenter inte behöver något som är specifikt för Adobe eller AEM.

* Allt som finns inuti JavaScript-komponenten är AEM-agnostiskt.
* Vad som är specifikt för AEM är att JS-komponenten måste mappas till en AEM med MapTo-hjälpen.

![AEM](assets/aem-agnostic.png)

Handledaren är den&quot;limning&quot; som gör att bakände och framände kan matchas ihop: `MapTo`

* Den talar om för JS-behållaren (eller JS-styckesystemet) vilken JS-komponent som ansvarar för återgivningen av varje komponent som finns i JSON.
* Det lägger till ett HTML-dataattribut i HTML-koden som JS-komponenten återger, så att SPA-redigeraren vet vilken dialogruta som ska visas för författaren när komponenten redigeras.

Mer information om hur du använder `MapTo` och skapar SPA för AEM finns i Komma igång-guiden för det valda ramverket.

* [Komma igång med SPA i AEM med React](getting-started-react.md)
* [Komma igång med SPA i AEM med hjälp av vinkeln](getting-started-angular.md)

## AEM och SPA {#aem-architecture-and-spas}

Den allmänna arkitekturen för AEM, inklusive utvecklings-, skribent- och publiceringsmiljöer, förändras inte när SPA används. Det är dock bra att förstå hur SPA-utvecklingen passar in i den här arkitekturen.

![AEM och SPA](assets/aem-architecture.png)

* **Bygg miljö**

   Det är här som källan för SPA-programkällan och komponentkällan checkas ut.

   * NPM-generatorn för klientlib skapar ett klientbibliotek från SPA-projektet.
   * Biblioteket kommer att tas av Maven och användas av pluginmodulen Maven Build tillsammans med komponenten till AEM Author.

* **AEM Author**

   Innehåll skapas på AEM författare, inklusive redigering av SPA.

   När en SPA redigeras med SPA-redigeraren i redigeringsmiljön:

   1. SPA begär den yttre HTML-koden.
   1. CSS läses in.
   1. Javascript för SPA-programmet läses in.
   1. När SPA-programmet körs begärs JSON, vilket gör att programmet kan skapa sidans DOM inklusive `cq-data` attributen.
   1. Med dessa `cq-data` attribut kan redigeraren läsa in ytterligare sidinformation så att den vet vilka redigeringskonfigurationer som är tillgängliga för komponenterna.

* **AEM Publish**

   Här publiceras det innehåll och de kompilerade biblioteken, inklusive SPA-programartefakter, klientlibs och komponenter för offentlig konsumtion.

* **Dispatcher/CDN**

   Dispatchern fungerar som AEM för webbplatsens besökare.
   * Förfrågningar behandlas på samma sätt som de behandlas i AEM Author, men det finns ingen begäran om sidinformation eftersom detta bara behövs av redigeraren.
   * Javascript, CSS, JSON och HTML cachelagras, vilket optimerar sidan för snabb leverans.

>[!NOTE]
>
>Inuti AEM finns inget behov av att köra Javascript-byggmekanismer eller att köra Javascript-skriptet. AEM är bara värd för kompilerade artefakter från SPA-programmet.

## Nästa steg {#next-steps}

* [Komma igång med SPA i AEM med React](getting-started-react.md) visar hur en grundläggande SPA har byggts för att fungera med SPA-redigeraren i AEM med React.
* [Komma igång med SPA i AEM med hjälp av Angular](getting-started-angular.md) visar hur en grundläggande SPA har byggts för att fungera med SPA Editor i AEM med hjälp av Angular.
* [Översikt över](editor-overview.md) SPA-redigeraren går in mer i kommunikationsmodellen mellan AEM och SPA.
* [WKND SPA Project](wknd-tutorial.md) är en stegvis självstudiekurs som implementerar ett enkelt SPA-projekt i AEM.
* [Dynamisk mappning av modell till komponent för SPA](model-to-component-mapping.md) förklarar den dynamiska mappningen av modell till komponent och hur den fungerar i SPA i AEM.
* [SPA Blueprint](blueprint.md) ger en djupdykning i hur SPA SDK för AEM fungerar om du vill implementera SPA i AEM för ett annat ramverk än React eller Angular eller bara vill ha en djupare förståelse.
