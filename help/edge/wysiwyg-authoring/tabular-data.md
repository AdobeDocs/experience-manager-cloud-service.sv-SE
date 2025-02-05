---
title: Hantera tabelldata med kalkylblad
description: Lär dig hur du använder kalkylblad för att hantera tabelldata för olika värden, som metadata och omdirigeringar för AEM med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 26d4db90-3e4b-4957-bf21-343c76322cdc
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# Hantera tabelldata med kalkylblad {#tabular-data}

Lär dig hur du använder kalkylblad för att hantera tabelldata för olika värden, som metadata och omdirigeringar för AEM med Edge Delivery Services.

## Användningsexempel {#use-cases}

För alla AEM med Edge Delivery Services måste du ha en lista över tabelldata, t.ex. för nyckelvärdesmappningar. De kan vara listor med många olika värden, som metadata och omdirigeringar. Med Edge Deliver Services kan du underhålla sådana tabelllistor med ett intuitivt verktyg: kalkylbladet. AEM översätter dessa kalkylblad till JSON-filer som enkelt kan användas av webbplatsen eller webbprogrammet.

Exempel på vanliga användningsområden:

* [Platshållare](/help/edge/docs/placeholders.md)
* [Metadata](/help/edge/docs/bulk-metadata.md)
* [Sidhuvuden](/help/edge/docs/custom-headers.md)
* [Omdirigeringar](/help/edge/docs/redirects.md)
* [Konfigurationer](/help/edge/docs/setup-byo-cdn-push-invalidation.md), till exempel för CND-inställningar

Dessutom kan du [skapa dina kalkylblad](#own-spreadsheet) av vilken struktur som helst för att lagra mappningar för dina egna syften.

I det här dokumentet används exemplet med omdirigeringar för att illustrera hur du skapar sådana kalkylblad. Mer information om de olika användningsfallen finns i de tidigare länkade avsnitten i Edge Delivery Servicens dokumentation.

>[!TIP]
>
>Mer information om hur kalkylblad i allmänhet fungerar med Edge Delivery Services finns i dokumentet [Kalkylblad och JSON](/help/edge/developer/spreadsheets.md).

>[!TIP]
>
>Kalkylblad bör endast användas för att underhålla tabelldata. [AEM rubrikfria funktioner](/help/headless/introduction.md) för lagring av strukturerade data.

## Förutsättningar {#prerequisites}

Om du vill skapa mappningar med kalkylblad i AEM med Edge Delivery Services måste du ha skapat webbplatsen med den senaste webbplatsmallen.

Mer information finns i dokumentet [Utvecklarhandbok om att komma igång med WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).

## Skapa ett kalkylblad {#spreadsheet}

I det här exemplet skapar du ett kalkylblad för att hantera omdirigeringar för AEM med Edge Delivery Services. Samma steg gäller för [andra kalkylbladstyper](#other) som du vill skapa.

1. Logga in på din AEM as a Cloud Service-redigeringsinstans, gå till konsolen **Platser** och navigera till roten på platsen som kräver ett kalkylblad. Tryck eller klicka på **Skapa** -> **Sida**.

   ![Skapa sida](assets/tabular-data/tabular-data-create-page.png)

1. Tryck eller klicka på mallen **Omdirigerar** på fliken **Mall** i guiden för att skapa en sida och tryck eller klicka sedan på **Nästa**.

   ![Välj mall](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. Fliken **Egenskaper** i guiden visar standardvärdena för omdirigeringskalkylbladet. Tryck eller klicka på **Skapa**.

   * **Titel** - behåll det här värdet som det är.
   * **Kolumner** - De minsta kolumner som krävs för omdirigeringar är förifyllda.
      * **källa** - Den sida som ska omdirigeras
      * **mål** - Den sida som ska omdirigeras till

   ![Kalkylbladets egenskaper](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. I dialogrutan **Slutfört**: tryck eller klicka på **Öppna**.

   ![Dialogrutan Slutfört](assets/tabular-data/tabular-data-success.png)

1. En ny flik öppnas med kalkylbladet inläst i en redigerare med de fördefinierade kolumnerna **source** och **destination**. Definiera omdirigeringar genom att trycka eller klicka på den tomma raden i kolumnen **source** . Ändringarna sparas automatiskt när du redigerar kalkylbladet.

   ![Redigera kalkylblad](assets/tabular-data/tabular-data-edit-redirects.png)

   * **Källan** är relativ till webbplatsens domän, så den innehåller bara den relativa sökvägen.
   * **destination** kan antingen vara en fullständig URL om du omdirigerar till en annan webbplats, eller vara en relativ sökväg om du omdirigerar inom din egen webbplats.
   * Flytta fokus till nästa cell med tabbtangenten.
   * Redigeraren lägger till nya rader i kalkylbladet efter behov.
   * Om du vill ta bort eller flytta en rad använder du ikonen **Ta bort** i slutet av varje rad och drar i början av varje rad.

## Importera kalkylbladsdata {#importing}

Förutom att redigera kalkylblad i AEM Page Editor kan du även importera data från en CSV-fil.

1. När du redigerar kalkylbladet i AEM trycker du på eller klickar på knappen **Överför** längst upp till vänster på skärmen.
1. I listrutan väljer du hur du vill importera dina data.
   * **Ersätt dokument** om du vill ersätta innehållet i hela kalkylbladet med innehållet i den CSV-fil som du ska överföra.
   * **Bifoga till dokument** om du vill bifoga data från CSV-filen som du överför till det befintliga kalkylbladsinnehållet.
1. I den dialogruta som öppnas väljer du din CSV-fil och trycker eller klickar på **Öppna**.

En dialogruta öppnas när importen bearbetas. När informationen i CSV-filen är klar läggs den till i eller ersätter innehållet i kalkylbladet. Om det uppstår fel, t.ex. om kolumnerna inte matchar, rapporteras de så att du kan korrigera CSV-filen.

>[!NOTE]
>
>* Rubrikerna i CSV-filen måste matcha kolumnerna i kalkylbladet exakt.
>* Om du importerar hela CSV-filen ändras inte kolumnrubrikerna, bara innehållsraderna.
>* Om du behöver uppdatera kolumnerna måste du göra det i AEM Page Editor innan du importerar CSV-filen.
>* En CSV-fil får inte vara större än 10 MB för import.

Beroende på vad du väljer av `mode` kan du även `create`, `replace` eller `append` till kalkylblad med hjälp av en CSV-fil och ett cURL-kommando som liknar följande.

```text
curl --request POST \
  --url http://<aem-instance>/bin/asynccommand \
  --header 'content-type: multipart/form-data' \
  --form file=@/path/to/your.csv \
  --form spreadsheetPath=/content/<your-site>/<your-spreadsheet> \
  --form 'spreadsheetTitle=Your Spreadsheet' \
  --form cmd=spreadsheetImport \
  --form operation=asyncSpreadsheetImport \
  --form _charset_=utf-8 \
  --form mode=append
```

Anropet returnerar en HTML-sida med information om jobb-ID:t.

```text
Message | Job(Id:2024/9/18/15/27/5cb0cacc-585d-4176-b018-b684ad2dfd02_90) created successfully. Please check status at Async Job Status Navigation.
```

[Du kan använda konsolen **Jobs**](/help/operations/asynchronous-jobs.md) för att visa jobbets status eller använda det ID som returnerats för att fråga efter det.

```text
https://<aem-instance>/bin/asynccommand?optype=JOBINF&jobid=2024/10/24/14/1/8da63f9e-066b-4134-95c9-21a9c57836a5_1
```

## Publicera ett kalkylbladssökvägar.json {#paths-json}

För att AEM ska kunna publicera data i ditt kalkylblad måste du dessutom uppdatera `paths.json`-filen för ditt projekt.

1. Öppna projektets rot i GitHub.

1. Tryck eller klicka på filen `paths.json` för att öppna informationen om den och sedan på ikonen **Redigera** .

   ![paths.json file](assets/tabular-data/tabular-data-paths-json.png)

1. Lägg till en rad för att mappa ditt nya kalkylblad till en `redirects.json`-resurs.

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

   >[!NOTE]
   >
   >Den här `paths.json`-posten baseras på exemplet med att skapa omdirigeringar med tabelldata. Uppdatera sökvägen som passar den [typ av kalkylblad du skapar](#other).

1. Klicka på **Verkställ ändringar..** om du vill spara ändringarna i `main`.

   * Bekräfta `main` eller skapa en pull-begäran enligt din process.

1. När du har definierat omdirigeringarna och uppdaterat sökvägsmappningen går du tillbaka till konsolen **Platser**.

1. Tryck eller klicka för att markera det omdirigerade kalkylbladet som du skapade i konsolen och tryck eller klicka sedan på **Snabba Publish** i åtgärdsfältet för att publicera kalkylbladet.

   ![Markera kalkylbladet i webbplatskonsolen](assets/tabular-data/tabular-data-select-publish.png)

1. I dialogrutan **Snabb Publish** trycker eller klickar du på **Publish**.

   ![Bekräfta publicering](assets/tabular-data/tabular-data-quick-publish.png)

1. En banderoll bekräftar publikationen.

   ![Banderollbekräftelse av publikationen](assets/tabular-data/tabular-data-publish-banner.png)

Kalkylbladet för omdirigering är nu publicerat och tillgängligt för alla.

>[!TIP]
>
>Mer information om sökvägsmappningar finns i dokumentet [Sökvägsmappning för Edge Delivery Services](/help/edge/wysiwyg-authoring/path-mapping.md).

## Andra kalkylbladstyper {#other}

Nu när du vet hur man skapar omdirigerade kalkylblad kan du skapa vilken annan standardtyp av kalkylblad som helst:

* Platshållare
* Metadata
* Sidhuvuden
* Konfiguration
* [Taxonomi](/help/edge/wysiwyg-authoring/taxonomy.md)

Följ bara samma steg i avsnitten [Skapa kalkylblad](#spreadsheet) och [Uppdatera sökvägar.json](#paths-json), välj lämplig mall och uppdatera `paths.json`-filen på lämpligt sätt.

För [Configuration](https://www.aem.live/docs/configuration), [Headers](https://www.aem.live/docs/custom-headers) och [Metadata](https://www.aem.live/docs/bulk-metadata) måste du lägga till en mappning för att publicera dem på deras standardplatser:

* Konfiguration: `/.helix/config.json`
* Rubriker: `/.helix/headers.json`
* Metadata: `/metadata.json`
* Taxonomi: Mer information finns i dokumentet [Hantera taxonomidata](/help/edge/wysiwyg-authoring/taxonomy.md).

Dessutom kan du [skapa ett eget kalkylblad](#own-spreadsheet) med godtyckliga kolumner för egen användning.

>[!NOTE]
>
>Du behöver inte skapa ett kalkylblad för att hantera indexering för AEM as a Cloud Service med Edge Delivery Services.
>
>Om du vill skapa egna index [följer du den här dokumentationen](https://www.aem.live/developer/indexing#setting-up-more-index-configurations) och skapar en egen `helix-query.yaml`-fil.

## Skapa ett eget kalkylblad {#own-spreadsheet}

1. Följ samma steg i avsnittet [Skapa kalkylblad](#spreadsheet).

1. Välj **Kalkylblad** när du väljer mallen.

1. På fliken **Egenskaper** i guiden kan du lägga till egna kolumner.

   ![Lägg till egna kolumner](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * I avsnittet **Kolumner** trycker eller klickar du på **Lägg till** för att lägga till en ny kolumn.
   * Ange ett namn för kolumnen.
   * Ta bort eller ordna om kolumnerna med **Ta bort** och dra i handtagsikonerna.

1. Skapa kalkylbladet och publicera enligt instruktionerna för omdirigeringsbladet.

1. Lägg till en mappning till filen `paths.json` enligt instruktionerna för omdirigeringskalkylbladet.

