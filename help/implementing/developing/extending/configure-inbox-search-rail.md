---
title: Hur konfigurerar jag sökfilter för Inkorgen?
description: Lär dig hur du konfigurerar sökfilter för inkorgsobjekt.
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Konfigurera sökfilter för Inkorgen {#configure-search-filters-inbox}

Du kan konfigurera sökfilter för inkorgsobjekt. Basera sökvillkoren på en specifik inkorgskolumn för att filtrera resultaten.

Om du till exempel vill filtrera inkorgsobjekten baserat på kolumnintervallet Födelsedatum och Inkorg kan du använda predikatet Datumintervall för att definiera datumintervallet.

Följande predikattyper är tillgängliga för Inkorg:

* Intervallpredikering

* Textpredikat

* Prediktion för datumintervall

* Egenskapspredikat för alternativ

>[!NOTE]
>
>Se till att du är medlem i `workflow-administrators` grupp för att konfigurera sökfilter för Inkorg.

## Skapa eller öppna en anpassad konfiguration {#creating-opening-customized-configuration}

1. Navigera till **[!UICONTROL Tools]**, **[!UICONTROL General]**, **[!UICONTROL Search Forms]**.

1. Välj **[!UICONTROL Inbox Search Rail]** konfiguration och knacka **[!UICONTROL Edit]**.
1. Inkludera ändringar av predikatkonfigurationen med **[!UICONTROL Edit Search Forms]**.
1. Välj **[!UICONTROL Done]** för att spara konfigurationen.

## Ta bort en anpassad konfiguration {#delete-customized-configuration}

Så här tar du bort en anpassad konfiguration:

1. Navigera till **[!UICONTROL Tools]**, **[!UICONTROL General]**, **[!UICONTROL Search Forms]**.

1. Välj **[!UICONTROL Inbox Search Rail]** konfiguration och knacka **[!UICONTROL Delete]**.

## Konfigurera intervallpredikat {#range-predicate}

Du kan filtrera inkorgsobjekt om du vill söka efter ett nummerintervall i en inkorgskolumn med hjälp av intervallpredikatet. Du kan också välja att ta med decimalvärden för tal.

Så här konfigurerar du en intervallpredikat:

1. Öppna [formulär för konfiguration](#creating-opening-customized-configuration).
1. Tryck på **[!UICONTROL Select Predicate]** tabb och dra **[!UICONTROL Range Predicate]** till formuläret.
1. I **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på, från **[!UICONTROL Column Name]** fält.
1. Ange etiketten för filtret i **[!UICONTROL Filter Label]** fält. Välj **[!UICONTROL Enable Decimal Values]** om du vill acceptera decimalvärden för tal när du definierar intervallet.
1. Ange en valfri beskrivning för konfigurationen och tryck på **[!UICONTROL Done]** för att spara den.

Konfigurationsändringarna återspeglas när du öppnar filtersidan. Filteretiketten som du angav i steg 4 visas som etikett med ett alternativ för att definiera maximum- och minimum-värden. När du trycker på Retur [!DNL Experience Manager] använder sökvillkoren på kolumnnamnet som anges i steg 3 och returnerar inkorgsobjekten.

>[!NOTE]
>
>I artikeln visas de senaste alternativen för användargränssnittet. Alternativnamnen uppdateras i användargränssnittet i den kommande versionen.

## Konfigurera textpredikat {#text-predicate}

Filtrera inkorgsobjekt om du vill söka efter en textsträng i en inkorgskolumn med hjälp av Textpredikat.

Så här konfigurerar du en textpredikat:

1. Öppna [formulär för konfiguration](#creating-opening-customized-configuration).
1. Tryck på **[!UICONTROL Select Predicate]** tabb och dra **[!UICONTROL Text Predicate]** till formuläret.
1. I **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på, från **[!UICONTROL Column Name]** fält.
1. Ange den text som visas i söktextrutan som platshållartext i dialogrutan **[!UICONTROL Search Text Box Placeholder]** fält.
1. Ange en valfri beskrivning för konfigurationen och tryck på **[!UICONTROL Done]** för att spara den.

Konfigurationsändringarna återspeglas när du öppnar filtersidan. När du trycker på Retur [!DNL Experience Manager] använder söktexten som anges i steg 4 på kolumnnamnet som anges i steg 3 och returnerar inkorgsobjekten.

## Konfigurera predikat för datumintervall {#date-range-predicate}

Du kan filtrera inkorgsobjekt om du vill söka efter ett datumintervall i en inkorgskolumn med hjälp av Förutsägelse för datumintervall.

Så här konfigurerar du en predikat för datumintervall:

1. Öppna [formulär för konfiguration](#creating-opening-customized-configuration).
1. Tryck på **[!UICONTROL Select Predicate]** tabb och dra **[!UICONTROL Date Range Predicate]** till formuläret.
1. I **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på, från **[!UICONTROL Column Name]** fält.
1. Ange etiketten för datumintervallfiltret i **[!UICONTROL Filter Label]** fält.
1. Ange startdatum och slutdatumetiketter för filtret.
1. Ange en valfri beskrivning för konfigurationen och tryck på **[!UICONTROL Done]** för att spara den.

Konfigurationsändringarna återspeglas när du öppnar filtersidan. Filteretiketten som du angav i steg 4 visas som etikett för datumintervallfiltret tillsammans med etiketterna för startdatum och slutdatum som anges i steg 5. [!DNL Experience Manager] använder sökvillkoren på kolumnnamnet som anges i steg 3 och returnerar inkorgsobjekten.

## Konfigurera alternativ för anpassade kolumner {#custom-column-options-predicate}

Du kan filtrera inkorgsobjekt om du vill söka efter ett anpassat alternativ i en inkorgskolumn med hjälp av Förutsägelse för anpassade kolumnalternativ.

Så här konfigurerar du en predikat för anpassade kolumnalternativ:

1. Öppna [formulär för konfiguration](#creating-opening-customized-configuration).
1. Tryck på **[!UICONTROL Select Predicate]** tabb och dra **[!UICONTROL Custom Column Options Predicate]** till formuläret.
1. I **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på, från **[!UICONTROL Column Name]** fält.
1. Ange etiketten för det anpassade kolumnalternativfiltret i dialogrutan **[!UICONTROL Filter Label]** fält.
1. Välj **[!UICONTROL Single Select]** om du vill aktivera valet av endast ett alternativ när du använder filter på en inkorgskolumn.
1. I **[!UICONTROL Add Options]** avsnitt:
   1. Välj **[!UICONTROL Manual]** om du vill definiera filtersökalternativen manuellt. Tryck **[!UICONTROL Add Filter Options]** för att definiera det första alternativet. Ange etiketten för kolumnalternativet och alternativvärdestexten som du vill söka efter. Om du till exempel vill söka efter **Kvinna** som ett värde i en inkorgskolumn kan du ange **F** som etikett för kolumnalternativet och lägg till **Kvinna** som alternativvärdestext. På samma sätt kan du lägga till fler filteralternativ.
   1. Välj **[!UICONTROL JSON Path]** för att definiera alternativ med hjälp av en JSON-filsökväg. Här följer ett exempel på en JSON-fil som definierar filteralternativ:

      ```JSON
          {
         "options":[
            {
            "text":"Female",
            "value":"F"
            },
            {
            "text":"Male",
            "value":"M"
            }
          ]
        }
      ```

   1. Välj **[!UICONTROL CRX Options Path]** för att definiera alternativ med hjälp av sökvägar för CRX-databaser. Tryck **[!UICONTROL Add Option Paths]** om du vill lägga till flera sökvägar. Här följer ett exempel som du kan definiera `Male` och `Female` filteralternativ:

      ```JSON
         <gender jcr:primaryType="sling:OrderedFolder">
                        <male
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Male"
                            value="M"/>
                        <female
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Female"
                            value="F"/>
                    </gender>
      ```

1. Ange en valfri beskrivning för konfigurationen och tryck på **[!UICONTROL Done]** för att spara den.

Konfigurationsändringarna återspeglas när du öppnar filtersidan. Filteretiketten som du angav i steg 4 visas som etikett för alternativet för anpassade kolumner. [!DNL Experience Manager] använder sökvillkoren som definieras i steg 6 på kolumnnamnet som anges i steg 3 och returnerar inkorgsobjekten.

I följande video visas stegen för att filtrera en kolumn baserat på `true` och `false` alternativvärden.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Visa sökfilter baserade på predikt {#view-search-filters-for-predicates}

Du kan visa sökfilter baserat på predikat. Välj **[!UICONTROL Filter]** på sidan Inkorg. Filtren visas i den vänstra rutan. Du kan sedan ange sökvillkor för att filtrera inkorgsobjekt.

![Filtersida](assets/apply-filters.png)

Mer information om hur du hanterar prediktiva konfigurationer finns i [Konfigurera Sök i Forms](search-forms.md).
