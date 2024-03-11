---
title: Hantera tabelldata med kalkylblad
description: Lär dig hur du använder kalkylblad för att hantera tabelldata för olika värden, som metadata och omdirigeringar för AEM med Edge Delivery Services.
feature: Edge Delivery Services
source-git-commit: 0fa88453a7d7c58a3ccb2a4baf7d2b143acf7ad5
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Hantera tabelldata med kalkylblad {#tabular-data}

Lär dig hur du använder kalkylblad för att hantera tabelldata för olika värden, som metadata och omdirigeringar för AEM med Edge Delivery Services.

{{aem-authoring-edge-early-access}}

## Användningsexempel {#use-cases}

För alla AEM med Edge Delivery Services måste du ha en lista över tabelldata, t.ex. för nyckelvärdesmappningar. De kan vara listor med många olika värden, som metadata och omdirigeringar. Med Edge Deliver Services kan du underhålla sådana tabelllistor med ett intuitivt verktyg: kalkylbladet. AEM översätter dessa kalkylblad till JSON-filer som enkelt kan användas av webbplatsen eller webbprogrammet.

Exempel på vanliga användningsområden:

* [Platshållare](/help/edge/docs/placeholders.md)
* [Metadata](/help/edge/docs/bulk-metadata.md)
* [Sidhuvuden](/help/edge/docs/custom-headers.md)
* [Omdirigeringar](/help/edge/docs/redirects.md)
* [Konfigurationer](/help/edge/docs/setup-byo-cdn-push-invalidation.md) till exempel för CND-inställningar

Dessutom kan du [skapa kalkylblad](#own-spreadsheet) av en struktur för att lagra mappningar för dina egna syften.

I det här dokumentet används exemplet med omdirigeringar för att illustrera hur du skapar sådana kalkylblad. Mer information om de olika användningsfallen finns i de tidigare länkade avsnitten i Edge Delivery Servicens dokumentation.

>[!TIP]
>
>Mer information om hur kalkylblad i allmänhet fungerar med Edge Delivery Services finns i dokumentet [Kalkylblad och JSON.](/help/edge/developer/spreadsheets.md)

>[!TIP]
>
>Kalkylblad bör endast användas för att underhålla tabelldata. För lagring av strukturerade data [AEM utan rubriker.](/help/headless/introduction.md)

## Förutsättningar {#prerequisites}

Om du vill skapa mappningar med kalkylblad i AEM med Edge Delivery Services måste du ha skapat webbplatsen med den senaste webbplatsmallen.

Se dokumentet [Guiden Komma igång för utvecklare för AEM med Edge Delivery Services](/help/edge/edge-dev-getting-started.md) för mer information.

## Skapa ett kalkylblad {#spreadsheet}

I det här exemplet skapar du ett kalkylblad för att hantera omdirigeringar för AEM med Edge Delivery Services. Samma steg gäller för [andra kalkylbladstyper](#other) som du vill skapa.

1. Logga in på din AEM as a Cloud Service redigeringsinstans, gå till **Webbplatser** konsolen och navigera till roten på platsen som kräver ett kalkylblad. Tryck eller klicka **Skapa** -> **Sida**.

   ![Skapa sida](assets/tabular-data/tabular-data-create-page.png)

1. På **Mall** för att skapa sidguiden trycker du på eller klickar på **Omdirigeringar** för att markera den och sedan trycka eller klicka på **Nästa**.

   ![Välj mall](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. The **Egenskaper** -fliken i guiden visar standardvärdena för omdirigeringskalkylbladet. Tryck eller klicka **Skapa**.

   * **Titel** - Låt det här värdet vara.
   * **Kolumner** - De minsta kolumner som krävs för omdirigeringar är förifyllda.
      * **källa** - Den sida som ska omdirigeras
      * **mål** - Den sida som ska omdirigeras till

   ![Kalkylbladets egenskaper](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. I **Lyckades** dialogruta, trycka eller klicka **Öppna**.

   ![Dialogrutan Slutfört](assets/tabular-data/tabular-data-success.png)

1. En ny flik öppnas med kalkylbladet inläst i en redigerare med det fördefinierade **källa** och **mål** kolumner. Definiera omdirigeringar genom att trycka eller klicka på den tomma raden på **källa** kolumn. Ändringarna sparas automatiskt när du redigerar kalkylbladet.

   ![Redigera kalkylblad](assets/tabular-data/tabular-data-edit-redirects.png)

   * The **källa** är relativ till webbplatsens domän, så den innehåller bara den relativa sökvägen.
   * The **mål** kan antingen vara en fullständig URL-adress om du dirigerar om till en annan webbplats, eller vara en relativ sökväg om du dirigerar om inom din egen webbplats.
   * Flytta fokus till nästa cell med tabbtangenten.
   * Redigeraren lägger till nya rader i kalkylbladet efter behov.
   * Om du vill ta bort eller flytta en rad använder du **Ta bort** ikonen i slutet av varje rad och draghandtagen i början av varje rad.

1. När du har definierat omdirigeringarna stänger du fliken och går tillbaka till **Webbplatser** konsol.

1. Tryck eller klicka för att välja det omdirigerade kalkylblad som du skapade i konsolen och tryck eller klicka sedan på **Snabbpublicering** i åtgärdsfältet för att publicera kalkylbladet.

   ![Markera kalkylbladet i webbplatskonsolen](assets/tabular-data/tabular-data-select-publish.png)

1. I **Snabbpublicering** dialogruta, trycka eller klicka **Publicera**.

   ![Bekräfta publicering](assets/tabular-data/tabular-data-quick-publish.png)

1. En banderoll bekräftar publikationen.

   ![Banderollens bekräftelse på publicering](assets/tabular-data/tabular-data-publish-banner.png)

Kalkylbladet för omdirigering är nu publicerat och tillgängligt för alla.

## Uppdatera paths.json {#paths-json}

För att AEM ska kunna använda data i ditt kalkylblad måste du dessutom uppdatera `paths.json` projektfil.

1. Öppna projektets rot i GitHub.

1. Tryck eller klicka på `paths.json` för att öppna informationen och sedan **Redigera** -ikon.

   ![paths.json-fil](assets/tabular-data/tabular-data-paths-json.png)

1. Lägga till en linje för att mappa ditt nya kalkylblad till en `redirects.json` resurs.

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

1. Klicka **Genomför ändringar...** för att spara ändringarna i `main`.

   * Genomför `main` eller skapa en pull-begäran enligt din process.

När ändringarna är `paths.json` om de sammanfogas, omdirigeringarna är aktiva för din webbplats.

## Andra kalkylbladstyper {#other}

Nu när du vet hur man skapar omdirigerade kalkylblad kan du skapa vilken annan standardtyp av kalkylblad som helst:

* Platshållare
* Metadata
* Sidhuvuden
* Konfiguration

Följ bara samma steg i avsnitten [Skapa kalkylblad](#spreadsheet) och [Uppdatera paths.json](#paths-json) och välja lämplig mall och uppdatera `paths.json` filen korrekt.

Dessutom kan du [skapa ett eget kalkylblad](#own-spreadsheet) med godtyckliga kolumner för egen användning.

>[!NOTE]
>
>Du behöver inte skapa ett kalkylblad för att hantera indexering för AEM as a Cloud Service med Edge Delivery Services-projekt.
>
>Om du vill skapa egna index [följ dokumentationen](https://www.aem.live/developer/indexing#setting-up-more-index-configurations) för att skapa `helix-query.yaml` -fil.

## Skapa ett eget kalkylblad {#own-spreadsheet}

1. Följ samma steg i avsnittet [Skapa kalkylblad.](#spreadsheet)

1. När du väljer mallen väljer du **Kalkylblad**.

1. I **Egenskaper** -fliken i guiden kan du lägga till egna kolumner.

   ![Lägg till egna kolumner](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * I **Kolumner** -sektion, trycka eller klicka **Lägg till** om du vill lägga till en ny kolumn.
   * Ange ett namn för kolumnen.
   * Ta bort eller ordna om kolumnerna med **Ta bort** och dra i handtagsikonerna.

1. Skapa kalkylbladet och publicera enligt instruktionerna för omdirigeringsbladet.

1. Lägg till en mappning till `paths.json` enligt instruktionerna för omdirigeringsbladet.
