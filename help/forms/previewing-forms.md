---
title: Hur förhandsgranskar man ett anpassat formulär?
description: Användarna kan förhandsgranska blanketterna innan de publiceras eller aktiveras för att säkerställa att de motsvarar förväntningarna. Alternativen för förhandsgranskning kan variera mellan olika formulärtyper som stöds.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Förhandsgranska ett formulär {#previewing-a-form}

## Ökning {#overview}

I [!DNL AEM Forms]kan du förhandsgranska de formulär och dokument som finns i databasen. Med Förhandsgranska vet man exakt hur formulären ser ut och beter sig när de släpps för slutanvändarna.

När du förhandsgranskar formulär återges de i ett interaktivt gränssnitt och användaren kan fylla i formulären med data. När du förhandsgranskar dokument återges de i icke-interaktivt läge och användaren kan bara visa dokumentet. För formulär finns ytterligare ett alternativ för Anpassad förhandsgranskning. Med det här alternativet kan du förhandsgranska formuläret med data från en XML-fil. Informationen fyller i vissa av fälten, eller alla fält, i det formulär som förhandsgranskas.

I följande tabell visas de förhandsvisningsalternativ som är tillgängliga för olika typer av formulär som stöds:

<table>
 <tbody>
  <tr>
   <td><strong>Tillgångstyp</strong><br /> </td>
   <td><strong>Tillgängliga alternativ för förhandsgranskning</strong><br /> </td>
  </tr>
  <tr>
   <td>Dokument</td>
   <td>PDF preview</td>
  </tr>
  <tr>
   <td>PDF Form</td>
   <td>Förhandsgranska och förhandsgranska PDF med data<br /> </td>
  </tr>
  <tr>
   <td>Adaptiv form</td>
   <td>Förhandsgranska HTML och HTML med data</td>
  </tr>
  <tr>
   <td>Formulärmall</td>
   <td>förhandsgranskning av PDF, förhandsvisning av PDF med data, förhandsgranskning av HTML, förhandsvisning av HTML med data<br /> </td>
  </tr>
 </tbody>
</table>

## Förhandsgranska ett formulär {#previewing-a-form-1}

1. Markera en resurs som du vill förhandsgranska och klicka på Förhandsgranska ![aem6forms_preview](assets/aem6forms_preview.png) i verktygsfältet Åtgärder.

   >[!NOTE]
   >
   >Om du vill välja en resurs växlar du till listvyn från standardkortvyn. Klicka ![aem6forms_viewlist](assets/aem6forms_viewlist.png) eller ![aem6forms_viewcard](assets/aem6forms_viewcard.png) för att växla vy.

1. Om du klickar på Förhandsvisa visas en lista med möjliga förhandsvisningsalternativ för den valda resurstypen. Klicka på önskat alternativ för att återge den markerade resursen på en ny flik.

   Dina alternativ är:

   * Förhandsgranska som HTML
   * Förhandsgranska med data
   * Förhandsgranska som PDF (tillgängligt för formulärmallar)

## Förhandsgranska med data {#preview-with-data}

När du väljer **Förhandsgranska med data** kan du se hur formuläret ser ut med verkliga data som anges i det. Med alternativet Förhandsgranska med data kan du överföra en XML-fil som innehåller exempelanvändardata. Exempelinformationen används för att fylla i förhandsgranskningsformuläret i det format du väljer.

1. Välj en resurs och klicka på Förhandsvisa ![aem6forms_preview](assets/aem6forms_preview.png)och markera **Förhandsgranska med data**.
1. Ange FormData som en XML-fil i dialogrutan Förhandsgranska formulär. Klicka på Förhandsgranska om du vill återge formuläret med sammanfogade data från XML.

