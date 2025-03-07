---
title: Använda kontrollpanelen för värdeberäkning för att analysera användningsmönster för formulär och dokument
description: Lär dig hur du använder kontrollpanelen Forms Usage Insights för att övervaka och förstå hur dina formulär och formulärfragment fungerar.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components, Core Components
hide: true
hidefromtoc: true
source-git-commit: 09d383638d6caba596d22a7c6b544768de5245a0
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Använda kontrollpanelen för värdeberäkning för att analysera användningsmönster för formulär och dokument

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande från din officiella adress till aem-forms-ea@adobe.com. <span>

![Instrumentpanel för värdeutjämning](/help/edge/docs/forms/universal-editor/assets/forms-insights-banner.svg)

Genom att regelbundet övervaka mätvärdena som presenteras på kontrollpanelen&quot;Forms Usage Insights&quot; kan ni få värdefulla insikter om hur era formulär, dokument och formulärfragment fungerar. Använd dessa data för att fatta välgrundade beslut om formulärdesign, fragmenthantering och övergripande formulärstrategi.

I den här artikeln finns detaljerade användningsanvisningar och metrisk tolkning för kontrollpanelen för värdeeliminering. En konceptuell översikt och fördelar med kontrollpanelen finns i [Förstå kontrollpanelen för värderealisering](/help/forms/aem-forms-value-realization-dashboard.md).


## Åtkomst till kontrollpanelen för användningsidentiteter

Så här kommer du åt kontrollpanelen Forms Usage Insights:

1. Navigera till **Forms** > **Forms och dokument**
1. Klicka på **InProduct Dashboard**. Kontrollpanelen öppnas i ett nytt fönster.

   ![Instrumentpanel för värdeutjämning](/help/forms/assets/forms-usage-insights.png)

## Ökning

Kontrollpanelen består av två huvudavsnitt:

- **Formulär- och dokumentaktivitet över tid:** Det här avsnittet innehåller insikter om hur dina formulär används och utvecklas under en vald period.
- **Fragmentanvändning:** I det här avsnittet kan du övervaka användning och återanvändning av formulärfragment.

## Formulär- och dokumentaktivitet över tid

Det här avsnittet innehåller fyra diagram, där varje diagram följer upp olika aspekter av formuläraktiviteten. Alla diagram har samma struktur:

- **Diagramtyp:** Linjediagram och stapeldiagram
- **X-axel:** Datum (visar daglig aktivitet)
- **Y-axel:** Antal (representerar antalet förekomster av den spårade aktiviteten)
- **Tidsperiod:** Justerbar via en listruta (alternativ: &quot;Senaste 30 dagarna&quot;, &quot;Senaste 12 månaderna&quot;)




### Skicka formulär

- **Syfte:** Diagrammet visar hur många gånger formulär har skickats in under den valda tidsperioden.

  ![Forms Submissions Chart](/help/forms/assets/forms-submissions-vr-dashboard-form-insights.png)
- **Information att extrahera:**
   - **Trendanalys:** Observera den övergripande trenden när formulär skickas. Ökar, minskar eller förblir talet relativt konstant?
   - **Maximala perioder:** Identifiera dagar eller perioder med ovanligt höga överföringshastigheter. Undersök möjliga orsaker till dessa toppar (t.ex. marknadsföringskampanjer, särskilda händelser).
   - **Låga aktivitetsperioder:** Identifiera perioder med låg överföringshastighet och utforska potentiella orsaker (t.ex. formuläravbrott, användbarhetsproblem).
   - **Jämförelseanalys:** Jämför överföringshastigheter för olika tidsperioder (t.ex. de senaste 30 dagarna jämfört med de föregående 30 dagarna) för att utvärdera prestandaförändringar.

### Dokumentåtergivningar

- **Syfte:** Diagrammet visar antalet dokument som genereras som ett resultat av formuläröverföringar. Detta är relevant om formulären aktiverar skapandet av dokument (t.ex. kontrakt, rapporter).

  ![Diagram över dokumentåtergivningar](/help/forms/assets/document-rendetions-vr-dashboard-form-insights.png)


- **Information att extrahera:**
   - **Jämförelse med formulärskickningar:** Jämför trenden för dokumentåtergivningar med trenden för formulärskickning. I idealfallet bör dessa korrelera nära. Skillnader kan tyda på problem med dokumentgenereringsprocessen.
   - **Volym för dokumentgenerering:** Utvärderar den totala volymen av dokument som genereras för att förstå arbetsbelastningen i dokumentgenereringssystemet.

### Forms Created


- **Syfte:** Diagrammet visar antalet nya formulär som skapats under den valda tidsperioden.

  ![Diagram som skapats av Forms](/help/forms/assets/forms-created-vr-dashboard-form-insights.png)

- **Information att extrahera:**
   - **Skapandefrekvens för formulär:** Spåra den hastighet som nya formulär skapas. Detta ger insikt i efterfrågan på nya formulär inom organisationen.
   - **Inspikar i skapande:** Identifiera perioder med ovanligt hög formulärskapandeaktivitet. Detta kan tyda på specifika projekt eller initiativ som kräver nya formulär.

### Forms Published

- **Syfte:** Diagrammet visar antalet formulär som har publicerats (gjorts tillgängliga för användning) under den valda tidsperioden.

  ![Forms publicerat diagram](/help/forms/assets/forms-publish-vr-dashboard-form-insights.png)


- **Information att extrahera:**
   - **Distributionshastighet för formulär:** Övervaka hastigheten med vilken nya formulär distribueras till användare.
   - **Fördröjning mellan Skapande och Publicering:** Analysera tidsskillnaden mellan diagrammet Forms Created och Forms Published. En betydande fördröjning kan tyda på flaskhalsar i godkännandeprocessen eller driftsättningsprocessen.

## Fragmentanvändning

I det här avsnittet finns information om hur du använder formulärfragment, som är återanvändbara komponenter som kan införlivas i flera formulär.

![Forms publicerat diagram](/help/forms/assets/fragment-usage-vr-dashboard-form-insights.png)

### Antal formulärfragment som används

- **Diagramtyp:** Numerisk visning (visa ett värde)
- **Syfte:** Här visas det totala antalet unika formulärfragment som för närvarande används i aktiva formulär.
- **Information att extrahera:**
   - **Fragmentanvändning:** Utvärderar den övergripande användningen av formulärfragment inom organisationen. Ett högre tal innebär större användning av återanvändbara komponenter.

### Återanvändning av formulärfragment

- **Diagramtyp:** Numerisk visning (visa ett värde)
- **Syfte:** Här visas det totala antalet gånger som formulärfragment har återanvänts i olika formulär. Det här måttet visar hur effektivt fragment används för att undvika dubbletter och upprätthålla konsekvensen.
- **Information att extrahera:**
   - **Återanvändning av fragment:** Övervaka den hastighet med vilken befintliga fragment återanvänds i nya formulär. Ett högre antal innebär bättre utnyttjande av återanvändbara komponenter och ökad effektivitet.

## Exempelscenarier

- **Scenario:** Du märker en plötslig nedgång i &quot;Formulärinskickat material&quot;.
   - **Åtgärd:** Undersök möjliga orsaker, t.ex. formuläravbrott, användbarhetsproblem eller trafiknedgång till formulärets startsida.
- **Scenario:** Värdet för återanvändning av formulärfragment är lågt.
   - **Åtgärd:** Befordra fördelarna med att använda formulärfragment för ditt team, se till att fragment är välorganiserade och lätta att hitta samt tillhandahålla utbildning om hur du skapar och återanvänder fragment på ett effektivt sätt.
- **Scenario:** Det är en avsevärd fördröjning mellan&quot;Forms Created&quot; och&quot;Forms Published&quot;.
   - **Åtgärd:** Granska formulärgodkännande- och distributionsprocessen för att identifiera och eliminera flaskhalsar.



## Se även

- [Förstå kontrollpanelen för värderealisering](/help/forms/aem-forms-value-realization-dashboard.md)
