---
title: Utveckla SPA för AEM
description: I den här artikeln finns viktiga frågor att tänka på när en frontutvecklare ska utveckla en SPA för AEM. Den ger också en översikt över arkitekturen i AEM vad gäller SPA som ska beaktas när en utvecklad SPA distribueras på AEM.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '2034'
ht-degree: 0%

---

# Utveckla SPA för AEM {#developing-spas-for-aem}

Single page applications (SPA) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som skapats med sådana ramverk.

I den här artikeln finns viktiga frågor att tänka på när en frontendutvecklare ska utveckla en SPA för AEM och en översikt över arkitekturen i AEM för att distribuera SPA på AEM.

## SPA utvecklingsprinciper för AEM {#spa-development-principles-for-aem}

Utveckla single page-applikationer AEM förutsätter att frontutvecklaren följer vedertagna standarder när han skapar en SPA. Om du som gränssnittsutvecklare följer dessa allmänna bästa metoder och några AEM specifika principer fungerar SPA med [AEM och funktioner för att skapa innehåll](introduction.md#content-editing-experience-with-spa).

* **[Portabilitet](#portability)** - Precis som med andra komponenter bör komponenterna byggas så att de är så bärbara som möjligt. SPA bör byggas med rörliga och återanvändbara komponenter.
* **[AEM diskar platsstruktur](#aem-drives-site-structure)** - Utvecklaren skapar komponenter och äger sin interna struktur, men använder AEM för att definiera webbplatsens innehållsstruktur.
* **[Dynamisk återgivning](#dynamic-rendering)** - All återgivning ska vara dynamisk.
* **[Dynamisk routning](#dynamic-routing)** - SPA ansvarar för routningen och AEM lyssnar på den och hämtar baserat på den. Alla routningar ska också vara dynamiska.

Om du håller dessa principer i åtanke när du utvecklar SPA blir det så flexibelt och säkert som möjligt i framtiden, samtidigt som du aktiverar alla funktioner för AEM som stöds.

Om du inte behöver ha stöd AEM redigeringsfunktionerna kan du välja något annat [SPA](#spa-design-models).

### Portabilitet {#portability}

Precis som när du utvecklar en komponent bör dina komponenter utformas på ett sådant sätt att de blir så bärbara som möjligt. Mönster som motverkar komponenternas bärbarhet eller återanvändbarhet bör undvikas för att säkerställa kompatibilitet, flexibilitet och underhållbarhet.

Den resulterande SPA ska byggas med mycket portabla och återanvändbara komponenter.

### AEM diskar platsstruktur {#aem-drives-site-structure}

Utvecklaren måste tänka på sig själv som ansvarig för att skapa ett bibliotek med SPA komponenter som används för att bygga appen. Utvecklaren har fullständig kontroll över komponenternas interna struktur. [AEM äger dock alltid webbplatsens struktur](editor-overview.md).

Den här kontrollen innebär att gränssnittsutvecklaren kan lägga till kundinnehåll före eller efter komponenternas startpunkt och även göra ett tredjepartssamtal inuti komponenten. Utvecklaren har dock inte fullständig kontroll över hur komponenterna kapslas, till exempel.

### Dynamisk återgivning {#dynamic-rendering}

SPA ska endast förlita sig på dynamisk återgivning av innehåll. Detta är standardinställningen där AEM hämtar och återger alla underordnade element i innehållsstrukturen.

All explicit återgivning som pekar på visst innehåll betraktas som statisk återgivning och även om den stöds är kompatibel med AEM innehållsredigeringsfunktioner. Det går också emot principen om [bärbarhet](#portability).

### Dynamisk routning {#dynamic-routing}

Precis som vid återgivning ska all routning också vara dynamisk. AEM [SPA ska alltid äga routningen](routing.md) och AEM lyssnar på den och hämtar innehåll baserat på den.

Alla statiska routningar fungerar mot [bärbarhetsprincip](#portability) och begränsar författaren genom att inte vara kompatibel med redigeringsfunktionerna i AEM. Om innehållsförfattaren till exempel vill ändra en väg eller ändra en sida för statisk routning måste han eller hon be den som utvecklar sidan att göra det.

## AEM Project Archetype {#aem-project-archetype}

Alla AEM ska använda [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), som stöder SPA projekt med React eller Angular och använder SPA SDK.

## SPA designmodeller {#spa-design-models}

Om [principer för utveckling av SPA inom AEM](#spa-development-principles-for-aem) följs, SPA fungerar med alla funktioner som stöds AEM innehåll.

Det kan dock finnas fall då denna funktion inte är helt nödvändig. Tabellen nedan ger en översikt över de olika designmodellerna, deras fördelar och nackdelar.

<table>
 <tbody>
  <tr>
   <th><strong>Designmodell<br /> </strong></th>
   <th><strong>Fördelar</strong></th>
   <th><strong>Nackdelar</strong></th>
  </tr>
  <tr>
   <td>AEM används som headless CMS utan att använda <a href="/help/implementing/developing/hybrid/reference-materials.md">SPA SDK-ramverket.</a></td>
   <td>Utvecklaren har fullständig kontroll över appen.</td>
   <td><p>Innehållsförfattare kan inte använda AEM.</p> <p>Koden är inte portabel eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>Utvecklaren använder SDK-ramverket för SPA Editor, men bara vissa områden öppnas för innehållsförfattaren.</td>
   <td>Utvecklaren behåller kontrollen över appen genom att endast aktivera redigering i begränsade delar av appen.</td>
   <td><p>Innehållsförfattare är begränsade till en begränsad uppsättning AEM upplevelser.</p> <p>Koden riskerar att inte vara flyttbar eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>I projektet används SPA Editor SDK fullt ut och klientkomponenterna utvecklas som ett bibliotek och innehållsstrukturen i programmet delegeras till AEM.</td>
   <td><p>Appen är återanvändbar och portabel.</p> <p>Innehållsförfattaren kan redigera appen med hjälp av AEM.<br /> </p> <p>SPA är kompatibelt med mallredigeraren.</p> </td>
   <td><p>Utvecklaren har inte kontroll över programmets struktur och den del av innehållet som har delegerats till AEM.</p> <p>Utvecklaren kan fortfarande reservera områden i programmet för innehåll som inte ska redigeras med AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Även om alla modeller stöds i AEM, är det bara genom att implementera den tredje (och följa de rekommenderade [Principer för SPA](#spa-development-principles-for-aem)) är det innehåll som författarna kan interagera med och redigera innehållet i SPA i AEM.

## Migrerar befintliga SPA till AEM {#migrating-existing-spas-to-aem}

Om SPA följer [SPA utvecklingsprinciper för AEM](#spa-development-principles-for-aem)fungerar SPA i AEM och kan redigeras med AEM SPA Editor.

Följ de här stegen för att göra dina befintliga SPA redo att arbeta med AEM.

1. **Gör dina JS-komponenter modulära.** - Gör att de kan återges i valfri ordning, position och storlek.
1. **Använd behållarna från SDK för att placera dina komponenter på skärmen.** - AEM innehåller en sid- och styckesystemkomponent som du kan använda.
1. **Skapa en AEM för varje JS-komponent.** - AEM komponenter definierar dialogrutan och JSON-utdata.

## Instruktioner för gränssnittsutvecklare {#instructions-for-front-end-developers}

Den främsta uppgiften att engagera en gränssnittsutvecklare för att skapa en SPA för AEM är att komma överens om komponenterna och deras JSON-modeller.

Här följer en översikt över de steg som en frontendutvecklare måste följa när han utvecklar en SPA för AEM.

1. **Godkänn komponenterna och deras JSON-modell**

   Utvecklare och AEM måste komma överens om vilka komponenter som är nödvändiga och en modell så att det går att hitta en exakt motsvarighet mellan komponenterna SPA bakomliggande komponenter.

   AEM är fortfarande nödvändiga för att kunna tillhandahålla redigeringsdialogrutor och exportera komponentmodellen.

1. **I Reagera-komponenter får du åtkomst till modellen via`this.props.cqModel`**

   När komponenterna är överenskomna och JSON-modellen är på plats kan den som utvecklar SPA utveckla den och enkelt komma åt JSON-modellen via `this.props.cqModel`.

1. **Implementera komponentens `render()` method**

   Utvecklaren implementerar `render()` metoden så som den passar och kan använda fälten i `cqModel` -egenskap. Den här metoden matar ut DOM- och HTML-fragmenten som infogas på sidan. Den här metoden är också standardmetoden för att skapa en app i React.

1. **Mappa komponenten till AEM-resurstypen via`MapTo()`**

   Mappningen lagrar komponentklasser och används internt av den angivna `Container` för att hämta och dynamiskt instansiera komponenter baserat på den angivna resurstypen.

   Den här kartan fungerar som en&quot;limma&quot; mellan fram- och bakände så att redigeraren vet vilka komponenter som de olika reaktionskomponenterna motsvarar.

   The `Page` och `ResponsiveGrid` är bra exempel på klasser som utökar basen `Container`.

1. **Definiera komponentens `EditConfig` som parameter till`MapTo()`**

   Den här parametern är nödvändig för att tala om för redigeraren hur komponenten ska namnges så länge som den inte har återgetts eller inte har något innehåll att återge.

1. **Utöka den angivna `Container` klass för sidor och behållare**

   Sidor och styckesystem bör utöka den här klassen så att delegering till inre komponenter fungerar som förväntat.

1. **Implementera en routningslösning som använder HTML5 `History` API.**

   När `ModelRouter` är aktiverat, anropar `pushState` och `replaceState` funktioner som utlöser en begäran till `PageModelManager` för att hämta ett saknat fragment av modellen.

   Den aktuella versionen av `ModelRouter` stöder endast användning av URL:er som pekar på den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av vanity-URL:er eller alias.

   The `ModelRouter` kan inaktiveras eller konfigureras för att ignorera en lista med reguljära uttryck.

## AEM {#aem-agnostic}

Dessa kodblock illustrerar hur komponenterna React och Angular inte behöver något som är specifikt för Adobe eller AEM.

* Allt som finns inuti JavaScript-komponenten är AEM-agnostiskt.
* Men det som är specifikt för AEM är att JS-komponenten måste mappas till en AEM med MapTo-hjälpen.

![AEM](assets/aem-agnostic.png)

The `MapTo` helper är den limning som gör att bakände och framände kan matchas ihop:

* Den talar om för JS-behållaren (eller JS-styckesystemet) vilken JS-komponent som ansvarar för återgivningen av varje komponent som finns i JSON.
* Det lägger till ett dataattribut för HTML i HTML som JS-komponenten återger, så att SPA Editor vet vilken dialogruta som ska visas för författaren när komponenten redigeras.

Mer information om hur du använder `MapTo` och skapa SPA för AEM i allmänhet, se Komma igång-guiden för ditt valda ramverk.

* [Komma igång med SPA i AEM med React](getting-started-react.md)
* [Komma igång med SPA i AEM med Angularna](getting-started-angular.md)

## AEM och SPA {#aem-architecture-and-spas}

Den allmänna arkitekturen för AEM, inklusive utvecklings-, skribent- och publiceringsmiljöer, förändras inte när SPA används. Men det är bra att förstå hur SPA kan integreras i arkitekturen.

![AEM och SPA](assets/aem-architecture.png)

* **Bygg miljö**

  I den här miljön är källan för SPA program och komponentkälla utcheckad.

   * NPM-generatorn för klientlib skapar ett klientbibliotek från det SPA projektet.
   * Biblioteket tas av Maven och distribueras av Maven Build-pluginen tillsammans med komponenten till AEM Author.

* **AEM Author**

  Innehåll skapas på AEM författare, inklusive SPA.

  När en SPA redigeras med SPA Editor i redigeringsmiljön:

   1. SPA begär yttre HTML.
   1. CSS läses in.
   1. JavaScript-koden för det SPA programmet läses in.
   1. När SPA körs begärs JSON, vilket gör att programmet kan skapa sidans DOM inklusive `cq-data` attribut.
   1. The `cq-data` kan redigeraren läsa in ytterligare sidinformation så att den vet vilka redigeringskonfigurationer som är tillgängliga för komponenterna.

* **AEM Publish**

  Om det innehåll och de kompilerade biblioteken som innehåller SPA programartefakter, klientbibliotek och komponenter publiceras för offentlig konsumtion.

* **Dispatcher/CDN**

  Dispatcher fungerar som AEM för webbplatsens besökare.
   * Förfrågningar behandlas på samma sätt som de behandlas i AEM Author. Det finns dock ingen begäran om sidinformationen eftersom den bara behövs av redigeraren.
   * JavaScript, CSS, JSON och HTML cachelagras, vilket optimerar sidan för snabb leverans.

>[!NOTE]
>
>I AEM finns ingen anledning att köra JavaScript-byggmekanismer eller själva JavaScript. AEM är bara värd för de kompilerade artefakterna från det SPA programmet.

## Nästa steg {#next-steps}

* [Komma igång med SPA i AEM med React](getting-started-react.md) visar hur en grundläggande SPA har utvecklats för att fungera med SPA Editor i AEM med React.
* [Komma igång med SPA i AEM med Angular](getting-started-angular.md) visar hur en grundläggande SPA är byggd för att fungera med SPA Editor i AEM med Angular.
* [SPA](editor-overview.md) fördjupar sig i kommunikationsmodellen mellan AEM och SPA.
* [WKND SPA Project](wknd-tutorial.md) är en stegvis självstudiekurs som implementerar ett enkelt SPA i AEM.
* [Dynamisk mappning av modell till komponent för SPA](model-to-component-mapping.md) I förklaras den dynamiska modellen för komponentmappning och hur den fungerar i SPA i AEM.
* [SPA Blueprint](blueprint.md) ger en djupdykning i hur SPA SDK för AEM fungerar om du vill implementera SPA i AEM för ett annat ramverk än React eller Angular. Eller så vill du bara ha en djupare förståelse.
