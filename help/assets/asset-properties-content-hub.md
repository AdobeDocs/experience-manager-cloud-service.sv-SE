---
title: Förhandsgranska resursen och dess egenskaper i  [!DNL the Content Hub]
description: Lär dig hur du förhandsgranskar resurser och egenskaper i  [!DNL Content Hub]
role: User
exl-id: a85af980-4c51-4d30-9fad-afd16370e9db
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Förhandsgranska resurs och dess egenskaper i Content Hub {#asset-properties}

![Metadatabannerbild](assets/metadata-banner-image.png)

Med [!DNL The Content Hub] kan du visa information om resursen som är viktig för en effektiv resursdistribution. Det är en samling av alla data som är tillgängliga för en tillgång.

Genom att förhandsgranska resurser och deras egenskaper kan du kategorisera resurser ytterligare, vilket är praktiskt när mängden digital information växer. Det går att hantera några hundra filer baserat på bara filnamn, miniatyrbilder och minne. Den här metoden är dock inte skalbar när antalet inblandade personer och antalet hanterade resurser ökar. Dessutom ökar värdet på en digital resurs allt eftersom resursen blir:

* Mer åtkomligt - system och användare hittar det enkelt.
* Enklare att agera på - du har fullständig information om mediers bilder och relaterad information för att kunna agera på dem snabbare och med större förtroende.
* Fullständigt - materialet innehåller mer information och sammanhang.

## Förutsättningar {#prerequisites}

[Content Hub-användare](deploy-content-hub.md#onboard-content-hub-users) kan utföra åtgärder som nämns i den här artikeln.

## Förhandsgranska resurs och dess egenskaper {#properties-ui}

Innan du använder, delar eller hämtar en resurs kan du visa den närmare. Med förhandsvisningsfunktionen kan du visa inte bara bilderna utan även några andra resurstyper som stöds. Du kan inte bara visa resursen utan även visa detaljerad information och vidta andra åtgärder. Om du vill visa information om en resurs går du till resursen eller [söker](search-assets.md) efter resursen och klickar sedan på resursen för att öppna dess egenskaper. I följande bild visas fälten som är tillgängliga på en egenskapssida för en resurs:

![Egenskaper för ett resursgränssnitt](assets/properties-ui.png)

* **A:** Namnet på en tillgång
* **B:** Procentandel av zoomning eller förhandsgranskning av resurser som är närmare zoomat in eller ut
* **C:** Ångra zooma till den tidigare valda procentandelen
* **D:** Gå till föregående eller nästa resurs
* **E:** Antal Assets
* **F:** Hämta resursen
* **G:** Redigera resurs med [!DNL Adobe Express]
* **H:** Komprimera eller förhandsgranska information om en resurs
* **I:** Dela resursen
* **J:** Lägg till resurs i [!DNL Collection]
* **K:** Stäng förhandsgranskningsskärmen
* **L:** Information om en resurs som innehåller titel, format, storlek, upplösning, taggar, färgtaggar och smarta taggar.

## Resursformat som stöds {#supported-formats}

[!DNL Content Hub] stöder alla resurstyper och format som den underliggande [!DNL Assets]-databasen stöder. I följande tabell visas viktiga filformat i [!DNL the Content Hub], som har ytterligare stöd för att förhandsgranska resurser visuellt:

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

### Härledda egenskaper {#derived-properties}

Vissa egenskaper för resurser som visas i [!DNL Content Hub] härleds, eller genereras automatiskt, när resurser överförs till [!DNL Assets] och sedan godkänns för tillgänglighet [!DNL Content Hub]. Nedan följer en lista över några av dem:

* **Storlek:** Storlek representerar storleken på resursens binära fil som lagras i den underliggande databasen.

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **Smarta taggar:** [!DNL The Content Hub] använder Adobe Sensei smarta innehållstjänster för att utbilda resurser med hjälp av igenkänningsalgoritmen i den taggbaserade strukturen. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser. Smarta taggar ökar innehållets hastighet genom att hjälpa dig att snabbt hitta relevanta resurser. De smarta taggarna är ett exempel på resursinformation som inte finns i bilden. [!DNL Experience Manager Assets] använder smarta taggar automatiskt på resurser som standard.

* **Färgtaggar:** [Med färgtaggar](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) kan du identifiera en resurs med hjälp av färger som identifieras automatiskt i en resurs med hjälp av Adobe Sensei AI-funktioner.

* Överföringsdatum

* Överfört av

* Senast ändrad

* Senast ändrad av

Det finns också egenskaper som anges när resurser läggs till i Content Hub. Mer information finns i [Lägga till varumärkesgodkända resurser i Content Hub](upload-brand-approved-assets.md). Dessa egenskaper visas också på sidan med resursegenskaper.

Administratörer kan också konfigurera egenskaperna, som visas för varje resurs:

* I gränssnittet för förhandsgranskning av resurs: se [Konfigurera Content Hub-användargränssnitt](configure-content-hub-ui-options.md#configure-asset-details-content-hub).
* På tillgångskort i sökresultat eller samlingar finns mer information i [Konfigurera Content Hub-användargränssnitt](configure-content-hub-ui-options.md#asset-card).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->
