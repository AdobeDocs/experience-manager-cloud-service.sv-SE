---
title: Hur konfigurerar jag sökfilter för Inkorgen?
description: Lär dig hur du konfigurerar sökfilter för inkorgsobjekt.
source-git-commit: ee32ab3659ee4696caa55b945b6b7895d94914a9
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
>Kontrollera att du är medlem i gruppen `workflow-administrators` för att konfigurera sökfilter för Inkorgen.

## Skapa eller öppna en anpassad konfiguration {#creating-opening-customized-configuration}

1. Navigera till **[!UICONTROL Tools]**, **[!UICONTROL General]**, **[!UICONTROL Search Forms]**.

1. Välj **[!UICONTROL Inbox Search Rail]**-konfigurationen och tryck på **[!UICONTROL Edit]**.
1. Inkludera ändringarna av predikatkonfigurationen med **[!UICONTROL Edit Search Forms]**.
1. Välj **[!UICONTROL Done]** om du vill spara konfigurationen.

## Ta bort en anpassad konfiguration {#delete-customized-configuration}

Så här tar du bort en anpassad konfiguration:

1. Navigera till **[!UICONTROL Tools]**, **[!UICONTROL General]**, **[!UICONTROL Search Forms]**.

1. Välj **[!UICONTROL Inbox Search Rail]**-konfigurationen och tryck på **[!UICONTROL Delete]**.

## Konfigurera intervallpredikat {#range-predicate}

Du kan filtrera inkorgsobjekt om du vill söka efter ett nummerintervall i en inkorgskolumn med hjälp av intervallpredikatet. Du kan också välja att ta med decimalvärden för tal.

Så här konfigurerar du en intervallpredikat:

1. Öppna [formuläret för konfiguration](#creating-opening-customized-configuration).
1. Tryck på fliken **[!UICONTROL Select Predicate]** och dra **[!UICONTROL Range Predicate]** till formuläret.
1. På fliken **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på i fältet **[!UICONTROL Column Name]**.
1. Ange filtrets etikett i fältet **[!UICONTROL Filter Label]**. Markera kryssrutan **[!UICONTROL Enable Decimal Values]** om du vill acceptera decimalvärden för tal när du definierar intervallet.
1. Ange en valfri beskrivning för konfigurationen och tryck på **[!UICONTROL Done]** för att spara den.

Konfigurationsändringarna återspeglas när du öppnar filtersidan. Filteretiketten som du angav i steg 4 visas som etikett med ett alternativ för att definiera maximum- och minimum-värden. När du trycker på Retur tillämpar [!DNL Experience Manager] sökvillkoren på kolumnnamnet som anges i steg 3 och returnerar inkorgsobjekten.

>[!NOTE]
>
>I artikeln visas de senaste alternativen för användargränssnittet. Alternativnamnen uppdateras i användargränssnittet i den kommande versionen.

## Konfigurera textpredikat {#text-predicate}

Filtrera inkorgsobjekt om du vill söka efter en textsträng i en inkorgskolumn med hjälp av Textpredikat.

Så här konfigurerar du en textpredikat:

1. Öppna [formuläret för konfiguration](#creating-opening-customized-configuration).
1. Tryck på fliken **[!UICONTROL Select Predicate]** och dra **[!UICONTROL Text Predicate]** till formuläret.
1. På fliken **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på i fältet **[!UICONTROL Column Name]**.
1. Ange den text som visas i söktextrutan som platshållartext i fältet **[!UICONTROL Search Text Box Placeholder]**.
1. Ange en valfri beskrivning för konfigurationen och tryck på **[!UICONTROL Done]** för att spara den.

Konfigurationsändringarna återspeglas när du öppnar filtersidan. När du trycker på Retur använder [!DNL Experience Manager] den söktext som anges i steg 4 på kolumnnamnet som anges i steg 3 och returnerar inkorgsobjekten.

## Konfigurera predikat för datumintervall {#date-range-predicate}

Du kan filtrera inkorgsobjekt om du vill söka efter ett datumintervall i en inkorgskolumn med hjälp av Förutsägelse för datumintervall.

Så här konfigurerar du en predikat för datumintervall:

1. Öppna [formuläret för konfiguration](#creating-opening-customized-configuration).
1. Tryck på fliken **[!UICONTROL Select Predicate]** och dra **[!UICONTROL Date Range Predicate]** till formuläret.
1. På fliken **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på i fältet **[!UICONTROL Column Name]**.
1. Ange etiketten för datumintervallfiltret i fältet **[!UICONTROL Filter Label]**.
1. Ange startdatum och slutdatumetiketter för filtret.
1. Ange en valfri beskrivning för konfigurationen och tryck på **[!UICONTROL Done]** för att spara den.

Konfigurationsändringarna återspeglas när du öppnar filtersidan. Filteretiketten som du angav i steg 4 visas som etikett för datumintervallfiltret tillsammans med etiketterna för startdatum och slutdatum som anges i steg 5. [!DNL Experience Manager] använder sökvillkoren på kolumnnamnet som anges i steg 3 och returnerar inkorgsobjekten.

## Konfigurera alternativ för anpassade kolumner {#custom-column-options-predicate}

Du kan filtrera inkorgsobjekt om du vill söka efter ett anpassat alternativ i en inkorgskolumn med hjälp av Förutsägelse för anpassade kolumnalternativ.

Så här konfigurerar du en predikat för anpassade kolumnalternativ:

1. Öppna [formuläret för konfiguration](#creating-opening-customized-configuration).
1. Tryck på fliken **[!UICONTROL Select Predicate]** och dra **[!UICONTROL Custom Column Options Predicate]** till formuläret.
1. På fliken **[!UICONTROL Settings]** väljer du namnet på inkorgskolumnen som du vill basera sökningen på i fältet **[!UICONTROL Column Name]**.
1. Ange etiketten för det anpassade kolumnalternativfiltret i fältet **[!UICONTROL Filter Label]**.
1. Markera kryssrutan **[!UICONTROL Single Select]** om du vill aktivera valet av endast ett alternativ när du använder filter på en inkorgskolumn.
1. I avsnittet **[!UICONTROL Add Options]**:
   1. Välj **[!UICONTROL Manual]** om du vill definiera filtersökalternativen manuellt. Tryck på **[!UICONTROL Add Filter Options]** för att definiera det första alternativet. Ange etiketten för kolumnalternativet och alternativvärdestexten som du vill söka efter. Om du till exempel vill söka efter **Kvinna** som ett värde i en inkorgskolumn kan du ange **F** som etikett för kolumnalternativet och lägga till **Kvinna** som alternativvärdestext. På samma sätt kan du lägga till fler filteralternativ.
   1. Välj **[!UICONTROL JSON Path]** om du vill definiera alternativ med en JSON-filsökväg. Här följer ett exempel på en JSON-fil som definierar filteralternativ:

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

   1. Välj **[!UICONTROL CRX Options Path]** om du vill definiera alternativ med hjälp av sökvägarna för CRX-databasen. Tryck på **[!UICONTROL Add Option Paths]** om du vill lägga till flera sökvägar. Följande är ett exempel som definierar filteralternativen `Male` och `Female`:

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

I följande video visas stegen för att filtrera en kolumn baserat på alternativvärdena `true` och `false`.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Visa sökfilter baserade på predikt {#view-search-filters-for-predicates}

Du kan visa sökfilter baserat på predikat. Välj **[!UICONTROL Filter]** på sidan Inkorg. Filtren visas i den vänstra rutan. Du kan sedan ange sökvillkor för att filtrera inkorgsobjekt.

![Filtersida](assets/apply-filters.png)

Mer information om hur du hanterar predikatkonfigurationer finns i [Konfigurera Search Forms](search-forms.md).


