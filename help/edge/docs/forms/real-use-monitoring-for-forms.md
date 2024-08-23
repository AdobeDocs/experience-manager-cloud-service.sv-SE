---
title: Real Use Monitoring (RUM) för Edge Delivery Services för AEM Forms as a Cloud Service
description: Real Use Monitoring (RUM) för Edge Delivery Services för AEM Forms as a Cloud Service innefattar kontinuerlig spårning och analys av användarinteraktioner med formulär.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: b078edeb9da059d3c39ac33ece5ce17b60793a24
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Real Use Monitoring (RUM) för Edge Delivery Services för AEM Forms as a Cloud Service

Med funktionen för övervakning av faktisk användning (RUM) får ni verkliga insikter om hur besökarna interagerar med era Adobe Experience Manager (AEM) webbplatser. Detta inbyggda verktyg ger värdefull information för att förstå användarbeteenden, diagnostisera prestandaproblem och mäta effektiviteten i webbplatsexperiment. RUM går bortom syntetisk testning genom att fånga in Real Use-interaktioner, vilket ger en mer korrekt bild av webbplatsens prestanda.

Men RUM prioriterar besökarnas integritet. Den använder provtagningsmetoder för att samla in data från en representativ undergrupp av användare, vilket säkerställer att ingen personligt identifierbar information någonsin samlas in. Dessutom är RUM utformat med datamängdsminimering i åtanke och samlar bara in de viktiga mätvärden som krävs för prestandaanalys. På så sätt kan du optimera AEM webbplatser samtidigt som du behåller användarförtroendet.


## Krav

Du kan visa kontrollpanelen för Edge Delivery Services för AEM Forms as a Cloud Service genom att gå till följande URL:

https://data.aem.live/?ext=forms

![RUM-inloggningsskärm för Edge Delivery Services för Forms](/help/edge/assets/rum-login-screen.png)

Om du vill logga in på kontrollpanelen för Edge Delivery Services för AEM Forms as a Cloud Service anger du följande:

* **URL**: URL:en är specifik för användarwebbplatsen eller domänen. Användarna kan filtrera webbplatsen eller domänen för att visa instrumentpanelen efter deras behov.

* **Domännyckel**: Användaren genererar domännyckeln manuellt. Kontakta din Adobe-representant om du vill få domännycklar för dina formulär.

### Kontrollpanelen för Edge Delivery Services för AEM Forms as a Cloud Service

När du har angett URL- och domännycklarna på inloggningsskärmen får du tillgång till kontrollpanelen för Edge Delivery Services för AEM Forms as a Cloud Service.

Bilden nedan visar kontrollpanelen för Edge Delivery Services för AEM Forms as a Cloud Service:

![RUM Forms Dashboard](/help/edge/assets/rum-forms-dashboard.png)

### Olika nyckelmått för kontrollpanelen för Forms {#different-metrics-rum-dashboard-forms}

Den här kontrollpanelen ger viktiga insikter i hur besökare interagerar med formulär på din Adobe Experience Manager (AEM) webbplats. Genom att övervaka dessa mätvärden kan ni identifiera områden som kan förbättras och optimera formulären för bättre användarupplevelser och konverteringsgrader:

* **Formulärvningar**: Spåra det totala antalet gånger som formulär visas
* **Formuläröverföringar**: Spåra det totala antalet slutförda överföringar

* **Störst innehållsmässig målning**: Den visar den hastighet med vilken URL-adressen läses in, vilket anger den tid det tar att återge det största innehållselementet som är synligt i visningsrutan från det ögonblick som användaren begär URL-adressen. Det största innehållselementet kan vara en bild, en video eller ett stort textelement på blocknivå. Prestandaklassificeringarna för URL-inläsningshastighet kategoriseras enligt följande:
   * **Bra**: Om inläsningstiden är 2,5 sekunder eller mindre.
   * **OK**: Om inläsningstiden är längre än 2,5 sekunder men mindre än 4 sekunder.
   * **Felaktig**: Om inläsningstiden är längre än 4 sekunder

* **Kumulativ layoutförskjutning**: Den mäter den totala summan av alla enskilda layoutförskjutningar för varje oväntad layoutförskjutning som inträffar under hela sidans livstid. Det spelar en viktig roll när det gäller att identifiera en sidas prestanda, eftersom det leder till en dålig användarupplevelse när sidelementen flyttas när en användare försöker interagera med dem. Den här poängen varierar från noll till ett positivt tal: noll innebär ingen växling, medan ett högre värde innebär fler layoutändringar på sidan. De prestandamått som används för att utvärdera poängen för layoutändringar är kategoriserade enligt följande:

   * **Bra**: Om layoutskifttalet är 0,1 eller mindre.
   * **OK**: Om layoutskifttalet är större än 0,1 men mindre än 0,25.
   * **Dåligt**: Om layoutskifttalet överstiger 0,25.

* **Interaktion med nästa färg**: Den utvärderar hur snabbt en sida reagerar på användarinteraktioner, med tanke på hur lång tid det tar för sidan att svara på klickningar, tryckningar och tangentbordsinmatningar under en användares besök på sidan. Slutvärdet är den längsta interaktionen som observerats, bortsett från eventuella avvikelser. Prestandamätningarna för Interaction to Next Paint är kategoriserade enligt följande:
   * **Bra**: Om längden mellan användaråtgärder är 200 millisekunder (ms) eller mindre.
   * **OK**: Om längden är längre än 200 ms men mindre än 500 ms.
   * **Dåligt**: Om längden överstiger 500 ms.

## Användbara insikter

Genom att analysera dessa mätvärden kan ni identifiera möjligheter att:

* Förenkla formulär och minska antalet fält.
* Förbättra formulärens klarhet med tydliga instruktioner och etiketter.
* Optimera formulärlayouten för mobilrespons.
* Åtgärda tekniska problem som gör det långsammare att läsa in formulär.

Genom att fokusera på dessa områden kan ni skapa formulär som är enklare att använda och uppmuntra besökarna att fylla i dem, vilket i slutänden leder till högre konverteringsgrader.

## Se även

{{see-more-forms-eds}}