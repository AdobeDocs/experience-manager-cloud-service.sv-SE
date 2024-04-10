---
title: Användarövervakning i realtid för Edge Delivery Services Forms
description: Användarövervakning i realtid för Edge Delivery Services Forms innefattar kontinuerlig uppföljning och analys av användarinteraktioner med formulär.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# Användarövervakning i realtid för Edge Delivery Services Forms

Adobe Experience Manager använder Real User Monitoring (RUM) för att förstå besökarinteraktioner med Adobe Experience Manager-drivna webbplatser. Det hjälper till att diagnostisera prestandamässiga utmaningar och mäta experimentets effektivitet. Real User Monitoring (Reell användarövervakning) bevarar besökarnas integritet genom att använda samplingstekniker och ser till att ingen personlig information samlas in av webbplatserna du besöker. Det är inte tillåtet att lägga till personuppgifter i RUM-datainsamlingen. Real User Monitoring i Adobe Experience Manager är utformat för att bevara besökarnas integritet och minimera datainsamlingen.

## Fördelar med att använda realtidsanvändarövervakning för Edge Delivery Services i Forms {#advantages}

AEM använder användarövervakning i realtid för följande:

* Identifiera och åtgärda prestandamässiga flaskhalsar på webbplatser.
* Så här beräknar du antalet sidvisningar för kundsajter
* För att förstå Adobe Experience Manager interaktion med analyser, målinriktning eller externa bibliotek på samma sida förbättrar man kompatibiliteten.

## Krav

Du kan visa kontrollpanelen för användarövervakning i realtid för Edge Delivery Services i Forms via följande URL: https://data.aem.live/?ext=forms

![Inloggningsskärm för RUM för Edge Delivery Services Forms ](/help/edge/assets/rum-login-screen.png)

Om du vill logga in på kontrollpanelen för användarövervakning i realtid för Edge Delivery Servicens Forms anger du följande:
* **URL**: URL:en är specifik för användarwebbplatsen eller domänen. Användarna kan filtrera webbplatsen eller domänen för att visa instrumentpanelen efter deras behov.
* **Domännyckel**: Användaren genererar domännyckeln manuellt. Om du behöver hjälp eller frågor kan du läsa [Generera URL-domännyckel](https://aemcs-workspace.adobe.com/rum/generate-domain-key) dokumentation.

### Kontrollpanel för användarövervakning i realtid för Edge Delivery Services i Forms

När du har angett URL- och domännyckeln i inloggningsfönstret får du tillgång till kontrollpanelen för användarövervakning i realtid för Edge Delivery Servicens Forms.

Bilden nedan visar RUM-kontrollpanelen för Edge Delivery Services Forms:

![RUM Forms Dashboard](/help/edge/assets/rum-forms-dashboard.png)

### Olika nyckelvärden för RUM-kontrollpanelen för Forms {#different-metrics-rum-dashboard-forms}

Du kan bedöma besökarnas interaktion med Adobe Experience Manager-drivna webbplatser med hjälp av följande nyckelmätvärden:

* **Formulär**: Det är det totala antalet formulär som återges för en URL inom det angivna datumintervallet.
* **Blanketter**: Det är det totala antalet formulär som har skickats för en URL inom det angivna datumintervallet.
* **Största innehållsfärg**: Den visar den hastighet med vilken URL-adressen läses in, vilket anger den tid det tar att återge det största innehållselementet som är synligt i visningsrutan från det ögonblick användaren begär URL-adressen. Det största innehållselementet kan vara en bild, en video eller ett stort textelement på blocknivå. Prestandaklassificeringarna för URL-inläsningshastighet kategoriseras enligt följande:
   * **Bra**: Om inläsningstiden är 2,5 sekunder eller mindre.
   * **Okej**: Om inläsningstiden är längre än 2,5 sekunder men högst 4 sekunder.
   * **Felaktig**: Om inläsningstiden är längre än 4 sekunder

* **Kumulativ layoutväxling**: Det mäter den totala summan av alla enskilda layoutskiftningar för varje oväntad layoutändring som inträffar under hela sidans livstid. Det spelar en viktig roll när det gäller att identifiera en sidas prestanda, eftersom det leder till en dålig användarupplevelse när sidelementen flyttas när en användare försöker interagera med dem. Den här poängen varierar från noll till ett positivt tal: noll innebär ingen växling, medan ett högre värde innebär fler layoutändringar på sidan. De prestandamått som används för att utvärdera poängen för layoutändringar är kategoriserade enligt följande:

   * **Bra**: Om layoutskifttalet är 0,1 eller mindre.
   * **Okej**: Om layoutskifttalet är större än 0,1 men högst 0,25.
   * **Felaktig**: Om layoutens skifthöjd överstiger 0,25.

* **Interaktion till nästa målning**: Här utvärderas hur snabbt en sida reagerar på användarinteraktioner, med tanke på hur lång tid det tar för sidan att svara på klickningar, tryckningar och tangentbordsinmatningar under en användares besök på sidan. Slutvärdet är den längsta interaktionen som observerats, bortsett från eventuella avvikelser. Prestandamätningarna för Interaction to Next Paint är kategoriserade enligt följande:
   * **Bra**: Om längden mellan användaråtgärder är 200 millisekunder (ms) eller mindre.
   * **Okej**: Om längden är mer än 200 ms men mindre än 500 ms.
   * **Felaktig**: Om längden överstiger 500 ms.

