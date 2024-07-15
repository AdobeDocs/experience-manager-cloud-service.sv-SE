---
title: Hantera tabelldata med kalkylblad
description: Lär dig hur du använder kalkylblad för att hantera tabelldata för olika värden, som metadata och omdirigeringar för AEM med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 26d4db90-3e4b-4957-bf21-343c76322cdc
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '958'
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
>Mer information om hur kalkylblad i allmänhet fungerar med Edge Delivery Services finns i dokumentet [Kalkylblad och JSON.](/help/edge/developer/spreadsheets.md)

>[!TIP]
>
>Kalkylblad bör endast användas för att underhålla tabelldata. Om du vill lagra strukturerade data ska du [kontrollera AEM rubrikfria funktioner.](/help/headless/introduction.md)

## Förutsättningar {#prerequisites}

Om du vill skapa mappningar med kalkylblad i AEM med Edge Delivery Services måste du ha skapat webbplatsen med den senaste webbplatsmallen.

Mer information finns i dokumentet [Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).

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

## Andra kalkylbladstyper {#other}

Nu när du vet hur man skapar omdirigerade kalkylblad kan du skapa vilken annan standardtyp av kalkylblad som helst:

* Platshållare
* Metadata
* Sidhuvuden
* Konfiguration

Följ bara samma steg i avsnitten [Skapa kalkylblad](#spreadsheet) och [Uppdatera sökvägar.json](#paths-json), välj lämplig mall och uppdatera `paths.json`-filen på lämpligt sätt.

För [Configuration](https://www.aem.live/docs/configuration), [Headers](https://www.aem.live/docs/custom-headers) och [Metadata](https://www.aem.live/docs/bulk-metadata) måste du lägga till en mappning för att publicera dem på deras standardplatser:

* Konfiguration: `/.helix/config.json`
* Rubriker: `/.helix/headers.json`
* Metadata: `/metadata.json`

Dessutom kan du [skapa ett eget kalkylblad](#own-spreadsheet) med godtyckliga kolumner för egen användning.

>[!NOTE]
>
>Du behöver inte skapa ett kalkylblad för att hantera indexering för AEM as a Cloud Service med Edge Delivery Services.
>
>Om du vill skapa egna index [följer du den här dokumentationen](https://www.aem.live/developer/indexing#setting-up-more-index-configurations) och skapar en egen `helix-query.yaml`-fil.

## Skapa ett eget kalkylblad {#own-spreadsheet}

1. Följ samma steg i avsnittet [Skapa kalkylblad.](#spreadsheet)

1. Välj **Kalkylblad** när du väljer mallen.

1. På fliken **Egenskaper** i guiden kan du lägga till egna kolumner.

   ![Lägg till egna kolumner](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * I avsnittet **Kolumner** trycker eller klickar du på **Lägg till** för att lägga till en ny kolumn.
   * Ange ett namn för kolumnen.
   * Ta bort eller ordna om kolumnerna med **Ta bort** och dra i handtagsikonerna.

1. Skapa kalkylbladet och publicera enligt instruktionerna för omdirigeringsbladet.

1. Lägg till en mappning till filen `paths.json` enligt instruktionerna för omdirigeringskalkylbladet.

