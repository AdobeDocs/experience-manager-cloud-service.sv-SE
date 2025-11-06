---
title: Utveckla SPA för AEM
description: I den här artikeln finns viktiga frågor att tänka på när en frontutvecklare ska utveckla en SPA för AEM. Den ger också en översikt över AEM arkitektur när det gäller SPA-program som man bör tänka på när man inför en utvecklad SPA på AEM.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 0%

---


# Utveckla SPA för AEM {#developing-spas-for-aem}

Single page applications (SPAs) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA-ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med sådana ramverk.

I den här artikeln finns viktiga frågor att tänka på när en frontutvecklare ska utveckla ett SPA för AEM och få en översikt över AEM arkitektur när det gäller att driftsätta SPA för AEM.

{{ue-over-spa}}

## SPA Development Principles for AEM {#spa-development-principles-for-aem}

Utveckla single page-applikationer på AEM förutsätter att frontutvecklaren följer vedertagna standarder när han skapar en SPA. Om du som gränssnittsutvecklare följer dessa allmänna bästa metoder och några AEM-specifika principer fungerar din SPA med [AEM och dess innehållsredigeringsfunktioner](introduction.md#content-editing-experience-with-spa).

* **[Portabilitet](#portability)** - Precis som med andra komponenter bör komponenterna byggas så att de blir så portabla som möjligt. SPA bör byggas med rörliga och återanvändbara komponenter.
* **[AEM Drives Site Structure](#aem-drives-site-structure)** - front-end-utvecklaren skapar komponenter och äger sin interna struktur, men använder AEM för att definiera webbplatsens innehållsstruktur.
* **[Dynamisk återgivning](#dynamic-rendering)** - All återgivning ska vara dynamisk.
* **[Dynamisk routning](#dynamic-routing)** - SPA ansvarar för routningen och AEM lyssnar på den och hämtar baserat på den. Alla routningar ska också vara dynamiska.

Om du håller dessa principer i åtanke när du utvecklar din SPA blir den så flexibel och framtidssäker som möjligt samtidigt som alla funktioner som stöds i AEM aktiveras.

Om du inte behöver stöd för AEM-redigeringsfunktioner kan du överväga en annan [SPA-designmodell](#spa-design-models).

### Portabilitet {#portability}

Precis som när du utvecklar en komponent bör dina komponenter utformas på ett sådant sätt att de blir så bärbara som möjligt. Mönster som motverkar komponenternas bärbarhet eller återanvändbarhet bör undvikas för att säkerställa kompatibilitet, flexibilitet och underhållbarhet.

Den resulterande produktresumén bör byggas med mycket portabla och återanvändbara komponenter.

### AEM Drives Site Structure {#aem-drives-site-structure}

Utvecklaren måste tänka på sig själv som ansvarig för att skapa ett bibliotek med SPA-komponenter som används för att bygga appen. Utvecklaren har fullständig kontroll över komponenternas interna struktur. [AEM äger dock alltid webbplatsens struktur](editor-overview.md).

Den här kontrollen innebär att gränssnittsutvecklaren kan lägga till kundinnehåll före eller efter komponenternas startpunkt och även göra ett tredjepartssamtal inuti komponenten. Utvecklaren har dock inte fullständig kontroll över hur komponenterna kapslas, till exempel.

### Dynamisk återgivning {#dynamic-rendering}

SPA bör endast förlita sig på dynamisk återgivning av innehåll. Detta är standardinställningen där AEM hämtar och återger alla underordnade objekt i innehållsstrukturen.

All explicit återgivning som pekar på visst innehåll betraktas som statisk återgivning och är kompatibel med AEM innehållsredigeringsfunktioner, även om den stöds. Det går också emot principen för [portability](#portability).

### Dynamisk routning {#dynamic-routing}

Precis som vid återgivning ska all routning också vara dynamisk. I AEM ska [SPA alltid äga routningen](routing.md) och AEM lyssnar på den och hämtar innehåll baserat på den.

Statisk routning fungerar mot [principen för bärbarhet](#portability) och begränsar författaren genom att inte vara kompatibel med innehållsredigeringsfunktionerna i AEM. Om innehållsförfattaren till exempel vill ändra en väg eller ändra en sida för statisk routning måste han eller hon be den som utvecklar sidan att göra det.

## AEM Project Archetype {#aem-project-archetype}

Alla AEM-projekt ska använda [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE), som har stöd för SPA-projekt med React eller Angular och som använder SPA SDK.

## SPA-designmodeller {#spa-design-models}

Om [principerna för att utveckla SPA i AEM](#spa-development-principles-for-aem) följs, fungerar SPA med alla AEM innehållsredigeringsfunktioner som stöds.

Det kan dock finnas fall då denna funktion inte är helt nödvändig. Tabellen nedan ger en översikt över de olika designmodellerna, deras fördelar och nackdelar.

<table>
 <tbody>
  <tr>
   <th><strong>Designmodell<br /> </strong></th>
   <th><strong>Fördelar</strong></th>
   <th><strong>Nackdelar</strong></th>
  </tr>
  <tr>
   <td>AEM används som headless CMS utan att <a href="/help/implementing/developing/hybrid/reference-materials.md">SDK-ramverket för SPA-redigeraren används.</a></td>
   <td>Utvecklaren har fullständig kontroll över appen.</td>
   <td><p>Innehållsförfattare kan inte använda AEM redigeringsgränssnitt.</p> <p>Koden är inte portabel eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>Framtidsutvecklaren använder SPA Editor SDK-ramverket, men bara vissa delar öppnas för innehållsförfattaren.</td>
   <td>Utvecklaren behåller kontrollen över appen genom att endast aktivera redigering i begränsade delar av appen.</td>
   <td><p>Innehållsförfattare är begränsade till en begränsad uppsättning av AEM funktioner för innehållsutveckling.</p> <p>Koden riskerar att inte vara flyttbar eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>I projektet används SPA Editor SDK fullt ut och klientkomponenterna utvecklas som ett bibliotek och innehållsstrukturen för programmet delegeras till AEM.</td>
   <td><p>Appen är återanvändbar och portabel.</p> <p>Innehållsförfattaren kan redigera appen med hjälp av AEM innehållsredigeringsgränssnitt.<br /> </p> <p>SPA är kompatibelt med mallredigeraren.</p> </td>
   <td><p>Utvecklaren har inte kontroll över programmets struktur och den del av innehållet som delegerats till AEM.</p> <p>Utvecklaren kan fortfarande reservera delar av programmet för innehåll som inte ska redigeras med AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Även om alla modeller stöds i AEM är det bara genom att implementera den tredje (och följa de rekommenderade [SPA-utvecklingsprinciperna](#spa-development-principles-for-aem)) som innehållsförfattarna kan interagera med och redigera innehållet i SPA i AEM.

## Migrera befintliga SPA till AEM {#migrating-existing-spas-to-aem}

I allmänhet om SPA följer [SPA-utvecklingsprinciperna för AEM](#spa-development-principles-for-aem) fungerar SPA i AEM och kan redigeras med AEM SPA-redigeraren.

Följ de här stegen så att du kan göra din befintliga SPA redo att arbeta med AEM.

1. **Gör dina JS-komponenter modulära.** - Gör att de kan återges i valfri ordning, position och storlek.
1. **Använd behållarna från SDK för att placera dina komponenter på skärmen.** - AEM tillhandahåller en sid- och styckesystemkomponent som du kan använda.
1. **Skapa en AEM-komponent för varje JS-komponent.** - AEM-komponenterna definierar dialogrutan och JSON-utdata.

## Instruktioner för gränssnittsutvecklare {#instructions-for-front-end-developers}

Den främsta uppgiften att engagera en gränssnittsutvecklare att skapa ett SPA för AEM är att komma överens om komponenterna och deras JSON-modeller.

Här följer en översikt över de steg som en gränssnittsutvecklare måste följa när han eller hon utvecklar ett SPA för AEM.

1. **Godkänn komponenter och deras JSON-modell**

   Framtidsutvecklare och AEM-utvecklare måste komma överens om vilka komponenter som är nödvändiga och en modell så att det går att matcha SPA-komponenterna med bakomliggande komponenter.

   AEM-komponenter behövs fortfarande mest för att kunna tillhandahålla redigeringsdialogrutor och för att exportera komponentmodellen.

1. **I Reagera-komponenter kommer du åt modellen via`this.props.cqModel`**

   När komponenterna är överenskomna och JSON-modellen är på plats kan frontendutvecklaren utveckla SPA och bara få åtkomst till JSON-modellen via `this.props.cqModel`.

1. **Implementera komponentens `render()`-metod**

   Utvecklaren implementerar metoden `render()` så som den passar och kan använda fälten för egenskapen `cqModel`. Den här metoden matar ut DOM- och HTML-fragmenten som infogas på sidan. Den här metoden är också standardmetoden för att skapa en app i React.

1. **Mappa komponenten till AEM-resurstypen via`MapTo()`**

   Mappningen lagrar komponentklasser och används internt av den angivna `Container`-komponenten för att hämta och dynamiskt instansiera komponenter baserat på den angivna resurstypen.

   Den här kartan fungerar som en&quot;limma&quot; mellan fram- och bakände så att redigeraren vet vilka komponenter som de olika reaktionskomponenterna motsvarar.

   `Page` och `ResponsiveGrid` är bra exempel på klasser som utökar basen `Container`.

1. **Definiera komponentens `EditConfig` som parameter till`MapTo()`**

   Den här parametern är nödvändig för att tala om för redigeraren hur komponenten ska namnges så länge som den inte har återgetts eller inte har något innehåll att återge.

1. **Utöka den angivna `Container`-klassen för sidor och behållare**

   Sidor och styckesystem bör utöka den här klassen så att delegering till inre komponenter fungerar som förväntat.

1. **Implementera en routningslösning som använder HTML5 `History` API.**

   När `ModelRouter` är aktiverat utlöser ett anrop till funktionerna `pushState` och `replaceState` en begäran till `PageModelManager` om att hämta ett saknat fragment av modellen.

   Den aktuella versionen av `ModelRouter` stöder endast användning av URL:er som pekar mot den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av vanity-URL:er eller alias.

   `ModelRouter` kan inaktiveras eller konfigureras för att ignorera en lista med reguljära uttryck.

## AEM-Agnostic {#aem-agnostic}

Dessa kodblock visar hur komponenterna React och Angular inte behöver något som är specifikt för Adobe eller AEM.

* Allt som finns inuti JavaScript-komponenten är AEM-agnostiker.
* Men det som är specifikt för AEM är att JS-komponenten måste mappas till en AEM-komponent med MapTo-hjälpen.

![AEM Agnostic approach](assets/aem-agnostic.png)

Hjälpprogrammet `MapTo` är den limma som gör att bakände och framände-komponenterna kan matchas tillsammans:

* Den talar om för JS-behållaren (eller JS-styckesystemet) vilken JS-komponent som ansvarar för återgivningen av varje komponent som finns i JSON.
* Det lägger till ett HTML-dataattribut i HTML som JS-komponenten återger, så att SPA-redigeraren vet vilken dialogruta som ska visas för författaren när komponenten redigeras.

Mer information om hur du använder `MapTo` och skapar SPA för AEM i allmänhet finns i guiden Komma igång för det valda ramverket.

* [Komma igång med SPA i AEM med React](getting-started-react.md)
* [Komma igång med SPA i AEM med Angular](getting-started-angular.md)

## AEM arkitektur och SPA {#aem-architecture-and-spas}

Den allmänna arkitekturen i AEM, inklusive utvecklings-, skribent- och publiceringsmiljöer, förändras inte när SPA används. Det är dock bra att förstå hur SPA-utvecklingen passar in i den här arkitekturen.

![AEM-arkitektur och SPA](assets/aem-architecture.png)

* **Byggmiljö**

  I den här miljön checkas källan för SPA-programmet och komponentkällan ut.

   * NPM-generatorn för klientlib skapar ett klientbibliotek från SPA-projektet.
   * Biblioteket tas av Maven och distribueras av Maven Build-pluginen tillsammans med komponenten till AEM Author.

* **AEM Author**

  Innehåll skapas på AEM-författaren, inklusive framtagning av SPA-filer.

  När en SPA redigeras med SPA-redigeraren i redigeringsmiljön:

   1. SPA begär den yttre HTML.
   1. CSS läses in.
   1. SPA-programmets JavaScript läses in.
   1. När SPA-programmet körs begärs JSON, vilket gör att programmet kan skapa sidans DOM inklusive attributen `cq-data`.
   1. Med attributen `cq-data` kan redigeraren läsa in ytterligare sidinformation så att den vet vilka redigeringskonfigurationer som är tillgängliga för komponenterna.

* **AEM Publish**

  Om det innehåll och de kompilerade biblioteken, inklusive SPA-programartefakter, klientbibliotek och komponenter, publiceras för offentlig konsumtion.

* **Dispatcher/CDN**

  Dispatcher fungerar som cachelagringslager för AEM för besökare på webbplatsen.
   * Förfrågningar behandlas på samma sätt som de behandlas i AEM Author. Det finns dock ingen begäran om sidinformationen eftersom den bara behövs av redigeraren.
   * JavaScript, CSS, JSON och HTML cachelagras, vilket optimerar sidan för snabb leverans.

>[!NOTE]
>
>I AEM behöver man inte köra JavaScript byggmekanismer eller själva JavaScript. AEM är bara värd för kompilerade artefakter från SPA-programmet.

## Nästa steg {#next-steps}

* [Komma igång med SPA i AEM med hjälp av React](getting-started-react.md) visar hur en grundläggande SPA har skapats för att fungera med SPA-redigeraren i AEM med hjälp av React.
* [Komma igång med SPA i AEM med Angular](getting-started-angular.md) visar hur en grundläggande SPA har skapats för att fungera med SPA-redigeraren i AEM med Angular.
* [Översikt över SPA-redigeraren](editor-overview.md) går in mer i kommunikationsmodellen mellan AEM och SPA.
* [WKND SPA-projekt](wknd-tutorial.md) är en stegvis självstudiekurs som implementerar ett enkelt SPA-projekt i AEM.
* [Dynamisk mappning av modell till komponent för SPA](model-to-component-mapping.md) förklarar den dynamiska mappningen av modell till komponent och hur den fungerar i SPA i AEM.
* [SPA Blueprint](blueprint.md) ger en djupdykning i hur SPA SDK för AEM fungerar om du vill implementera SPA i AEM för ett annat ramverk än React eller Angular. Eller så vill du bara ha en djupare förståelse.
