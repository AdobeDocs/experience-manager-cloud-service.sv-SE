---
title: Importera och exportera resursers metadata gruppvis
description: I den här artikeln beskrivs hur du importerar och exporterar flera metadata samtidigt.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: 561df1d2a2f7b900470084d28b832b4c7a568d3e
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 11%

---

# Importera och exportera resursers metadata gruppvis {#import-and-export-asset-metadata-in-bulk}

Med Adobe Experience Manager Assets kan du importera resursmetadata i grupp med hjälp av en CSV-fil. Du kan göra satsvisa uppdateringar för de nyligen överförda resurserna eller för befintliga resurser genom att importera en CSV-fil. Du kan också importera resursmetadata i grupp från tredjepartssystem i CSV-format.

## Importera metadata {#import-metadata}

Import av metadata är asynkron och påverkar inte systemets prestanda. Samtidig uppdatering av metadata för flera resurser kan vara resurskrävande på grund av återskrivningsaktiviteten för metadata med hjälp av objektmikrotjänster. Adobe rekommenderar att du planerar att göra en gruppåtgärd under resurssnål serveranvändning så att prestanda för andra användare inte påverkas.

>[!NOTE]
>
>Om du vill importera metadata för anpassade namnutrymmen måste du först registrera namnutrymmena.

1. Navigera till användargränssnittet Resurser och tryck/klicka på **[!UICONTROL Create]** i verktygsfältet.
1. Välj **[!UICONTROL Metadata]** i menyn.
1. På sidan **[!UICONTROL Metadata Import]** trycker/klickar du på **[!UICONTROL Select File]**. Markera CSV-filen med metadata.
1. Ange följande parametrar:

   | Parameter | Beskrivning |
   | ---------------------- | ------- |
   | Batchstorlek | Antal resurser i en grupp som metadata ska importeras för. Standardvärdet är 50. Maxvärdet är 100. |
   | Fältavgränsare | Standardvärdet är `,` (ett komma). Du kan ange andra tecken. |
   | Flervärdesavgränsare | Avgränsare för metadatavärden. Standardvärdet är `|`. |
   | Starta arbetsflöden | Falskt som standard. När det är inställt på `true` och standardinställningarna används för arbetsflödet WriteBack för DAM-metadata (som skriver metadata till binära XMP). Om du aktiverar arbetsflödena blir systemet långsammare. |
   | Kolumnnamn för resurssökväg | Definierar kolumnnamnet för CSV-filen med resurser. |

1. Klicka på **[!UICONTROL Import]** i verktygsfältet. När metadata har importerats skickas ett meddelande till din meddelandeinkorg. Navigera till egenskapssidan för resurser och kontrollera om metadatavärdena har importerats korrekt för resurser.

Om du vill lägga till datum och tidsstämpel när du importerar metadata använder du formatet `YYYY-MM-DDThh:mm:ss.fff-00:00` för datum och tid. Datum och tid avgränsas med `T`, `hh` är timmar i 24-timmarsformat, `fff` är nanosekunder och `-00:00` är tidszonsförskjutning. Till exempel är `2020-03-26T11:26:00.000-07:00` 26 mars 2020 vid 11:26:000 AM PST time.

>[!CAUTION]
>
>Om datumformatet inte matchar `YYYY-MM-DDThh:mm:ss.fff-00:00`, ställs datumvärdena inte in. Datumformaten för den exporterade CSV-metadatafilen har formatet `YYYY-MM-DDThh:mm:ss-00:00`. Om du vill importera den konverterar du den till ett godkänt format genom att lägga till värdet för nanosekunder som anges med `fff`.

## Exportera metadata {#export-metadata}

Du kan exportera metadata för flera resurser i ett CSV-format. Metadata exporteras asynkront och påverkar inte systemets prestanda. Om du vill exportera metadata går Experience Manager igenom egenskaperna för objektnoden `jcr:content/metadata` och dess underordnade noder och exporterar metadataegenskaperna i en CSV-fil.

Några exempel på användningsområden för att exportera flera metadata samtidigt är:

* Importera metadata i ett tredjepartssystem när du migrerar resurser.
* Dela metadata med ett större projektteam.
* Testa eller granska metadata för att se om de är kompatibla.
* Gör metadata externt för separat lokalisering.

1. Välj den resursmapp som innehåller resurser som du vill exportera metadata för. Välj **[!UICONTROL Export metadata]** i verktygsfältet.
1. Ange ett namn för CSV-filen i dialogrutan Exportera metadata. Om du vill exportera metadata för resurser i undermappar väljer du **[!UICONTROL Include assets in subfolders]**.

   ![Gränssnitt och alternativ för att exportera metadata för alla resurser i en ](assets/export_metadata_page.png "mappGränssnitt och alternativ för att exportera metadata för alla resurser i en mapp")

1. Välj önskade alternativ. Ange ett filnamn och vid behov ett datum.

1. I fältet **[!UICONTROL Properties to be exported]** anger du om du vill exportera alla eller specifika egenskaper. Om du väljer Selektiva egenskaper som ska exporteras lägger du till de önskade egenskaperna.

1. Tryck/klicka på **[!UICONTROL Export]** i verktygsfältet. Ett meddelande bekräftar att metadata exporteras. Stäng meddelandet.
1. Öppna inkorgsmeddelandet för exportjobbet. Markera jobbet och klicka på **[!UICONTROL Open]** i verktygsfältet. Om du vill hämta CSV-filen med metadata trycker/klickar du på **[!UICONTROL CSV Download]** i verktygsfältet. Klicka på **[!UICONTROL Close]**.

   ![Dialogruta för att hämta CSV-filen som innehåller metadata som exporterats i grupp](assets/csv_download.png)

   *Bild: Dialogruta för att hämta CSV-filen som innehåller metadata som exporterats i grupp.*
