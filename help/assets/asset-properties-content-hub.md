---
title: Resursegenskaper i [!DNL the Content Hub]
description: Lär dig hur du visar och hanterar resursegenskaper i [!DNL Content Hub]
role: User
source-git-commit: e590c34c177e6b45b6a52370caa88da54b61ebc0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---


# Hantera resursegenskaper i Content Hub {#asset-properties}

![Bild på metadatabubrik](assets/metadata-banner-image.png)

[!DNL The Content Hub] gör att du kan visa information om resursen som är viktig för en effektiv resursdistribution. Det är en samling av alla data som är tillgängliga för en tillgång.

Genom att visa resursegenskaper kan du kategorisera resurser ytterligare och det är praktiskt när mängden digital information ökar. Det går att hantera några hundra filer baserat på bara filnamn, miniatyrbilder och minne. Den här metoden är dock inte skalbar när antalet inblandade personer och antalet hanterade resurser ökar. Dessutom ökar värdet på en digital resurs allt eftersom resursen blir:

* Mer åtkomligt - system och användare hittar det enkelt.
* Enklare att hantera - du kan enkelt hitta resurser med samma uppsättning egenskaper och använda ändringar på dem.
* Fullständigt - materialet innehåller mer information och sammanhang.

## Visa egenskaper för en resurs {#properties-ui}

Innan du använder, delar eller hämtar en resurs kan du visa den närmare. Med förhandsvisningsfunktionen kan du visa inte bara bilderna utan även några andra resurstyper som stöds. Du kan inte bara visa resursen utan även visa detaljerad information och vidta andra åtgärder. Om du vill visa information om en resurs går du till resursen eller [sök](search-assets.md) resursen och klicka sedan på resursen för att öppna dess egenskaper. I följande bild visas fälten som är tillgängliga på en egenskapssida för en resurs:

![Egenskaper för ett tillgångsgränssnitt](assets/properties-ui.png)

* **S:** En tillgångs namn
* **B:** Procentandel av zoomning eller förhandsgranskning av resurser som zoomas in eller ut
* **C:** Ångra zoomning till tidigare markerad procent
* **D:** Gå till föregående eller nästa resurs
* **E:** Antal Assets
* **F:** Hämta resursen
* **G:** Redigera resurs med [!DNL Adobe Express]
* **H:** Komprimera eller förhandsgranska information om en resurs
* **I:** Dela resursen
* **J:** Lägg till resurs i [!DNL Collection]
* **K:** Stäng förhandsgranskningsskärmen
* **L:** Information om en resurs som innehåller titel, format, storlek, upplösning, taggar, färgtaggar och smarta taggar.

## Format som stöds {#supported-formats}

I följande tabell visas vilka filformat som stöds i [!DNL the Content Hub]:

<table> 
    <tbody>
     <tr>
      <th><strong>Filtyp</strong></th>
      <th><strong>Format som stöds</strong></th>
     </tr>
     <tr>
      <td>Bild</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL SVG]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Video</td>
      <td>
        <ul>
            <li>[!UICONTROL Quicktime]</li>  
            <li>[!UICONTROL MP4]</li> 
        </ul>
      </td>
     </tr>
      <tr>
      <td>Dokument</td>
      <td>
        <ul>
            <li>[!UICONTROL txt] (Oformaterad)</li>  
            <li>[!UICONTROL Doc/Docx]</li> 
            <li>[!UICONTROL XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Skriv ut media</td>
      <td>
        <ul>
            <li>[!UICONTROL PDF]</li>  
        </ul>
      </td>
     </tr>  
    </tbody>
   </table>

### Härledda egenskaper efter överföring av en resurs {#derived-properties}

När du har överfört en resurs hämtar Content Hub vissa egenskaper som genereras automatiskt. Nedan följer en lista över några av dem:

* **Storlek:** Storlek visar det logiska värdet för en resurs utifrån dess dimensioner. Det klargör hur mycket utrymme en resurs tar i en databas. [!DNL The Content Hub] stöder resurser på upp till 2 GB.

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **Smarta taggar:** [!DNL The Content Hub] använder Adobe Sensei smarta innehållstjänster för att utbilda resurser med hjälp av algoritmen för igenkänning i den taggbaserade strukturen. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser. Smarta taggar ökar innehållets hastighet genom att hjälpa dig att snabbt hitta relevanta resurser. De smarta taggarna är ett exempel på resursinformation som inte finns i bilden. [!DNL The Content Hub] använder automatiskt smarta taggar på resurser som standard.

* **Färgtaggar:** [Färgtaggar](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) hjälper dig att identifiera en resurs med hjälp av färger som identifieras automatiskt i en resurs med hjälp av Adobe Sensei AI-funktioner.

* Överföringsdatum

* Överfört av

* Senast ändrad

* Senast ändrad av

Det finns också egenskaper som anges när resurser läggs till i Content Hub. Mer information finns i [Lägg till varumärkesgodkända mediefiler i Content Hub](upload-brand-approved-assets.md). Dessa egenskaper visas också på sidan med resursegenskaper.

Administratörer kan också konfigurera de egenskaper som ska visas för varje resurs. Mer information finns i [Konfigurera Content Hub användargränssnitt](configure-content-hub-ui-options.md#configure-asset-details-content-hub).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

