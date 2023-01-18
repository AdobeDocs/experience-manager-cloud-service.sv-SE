---
title: Extrahera innehåll via GraphQL API
description: Lär dig hur du använder innehållsfragment och GraphQL API som ett headless-system för innehållshantering.
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---


# Extrahera innehåll via GraphQL API {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="Extrahera innehåll med GraphQL API"
>abstract="I den här modulen får du lära dig hur du kan använda innehållsfragment och GraphQL API som ett headless-system för innehållshantering."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="Starta GraphQL Explorer"
>abstract="GraphQL tillhandahåller ett frågebaserat API som tillåter externa klientprogram att fråga AEM efter endast det innehåll som behövs, med hjälp av ett enda API-anrop. Följ den här modulen för att lära dig hur du kör två olika typer av frågor. Lär dig sedan hur du hämtar innehållet från det innehållsfragment som du skapade i föregående modul.<br><br>Starta den här modulen på en ny flik genom att klicka nedan."
>additional-url="https://video.tv.adobe.com/v/328618" text="Extrahera innehåll i video"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="Snyggt jobbat! Du har lärt dig mer om de två grundläggande typerna av frågor och hur du ställer frågor till ditt eget innehåll. Du förstår nu hur du använder AEM GraphQL API för att skapa effektiva frågor som levererar innehåll i ett format som du förväntar dig av appen."
>abstract=""

## Fråga efter en lista med exempelinnehåll {#list-query}

Klicka på **Starta GraphQL Explorer** klickar du på knappen ovan öppnas Utforskaren i GraphQL på en ny flik.

![GraphQL Query Editor](assets/extract-content/query-editor.png)

Med Utforskaren i GraphQL kan du skapa och validera frågor mot ditt headless-innehåll innan du använder dem för att styra innehållet i din app eller på din webbplats. Låt oss se hur det går till!

1. Din AEM headless-testversion innehåller en förinläst slutpunkt med innehållsfragment som du kan extrahera innehåll från för testning. Välj **AEM demoresurser** slutpunkt från **Slutpunkt** nedrullningsbar meny längst upp till höger i redigeraren.

   ![Markera slutpunkt](assets/extract-content/select-endpoint.png)

1. Kopiera följande kodfragment för en listfråga för den förinlästa **AEM demoresurser** slutpunkt. En listfråga returnerar en lista med allt innehåll som använder en viss modell för innehållsfragment. Lagersidor och kategorisidor använder vanligtvis det här frågeformatet.

   ```text
   {
       adventureList {
         items {
            _path
            adventureTitle
            adventurePrice
            adventureTripLength
            adventurePrimaryImage {
              ... on ImageRef {
               _path
               mimeType
               width
               height
             }
           }
         }
      }
    }
   ```

1. Ersätt det befintliga innehållet i frågeredigeraren genom att klistra in den kopierade koden.

   ![Listfråga](assets/extract-content/list-query.png)

1. När du har klistrat in klickar du på **Spela upp** längst upp till vänster i frågeredigeraren för att köra frågan.

1. Resultatet visas i den högra panelen bredvid frågeredigeraren. Om frågan är felaktig visas ett fel på den högra panelen.

   ![Listfrågeresultat](assets/extract-content/list-query-results.png)

Du har just validerat en listfråga för en fullständig lista över alla innehållsfragment. Den här processen bidrar till att säkerställa att svaret blir vad din app förväntar sig, med resultat som visar hur dina appar och webbplatser kommer att hämta innehåll som skapas i AEM.

## Fråga efter en viss del av exempelinnehållet {#bypath-query}

Genom att köra en byPath-fråga kan du hämta innehåll för ett visst innehållsfragment. Produktinformationssidor och sidor som fokuserar på en viss uppsättning innehåll kräver vanligtvis den här typen av fråga. Låt oss se hur det fungerar!

1. Kopiera följande kodfragment för en byPath-fråga för den förinlästa **AEM demoresurser** slutpunkt.

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         adventureTitle
         adventureDescription {
           json
         }
         adventurePrimaryImage {
           ... on ImageRef {
             _path
             width
             height
           }
         }
       }
     }
   }
   ```

1. Ersätt det befintliga innehållet i frågeredigeraren genom att klistra in den kopierade koden.

   ![byPath-fråga](assets/extract-content/bypath-query.png)

1. När du har klistrat in klickar du på **Spela upp** längst upp till vänster i frågeredigeraren för att köra frågan.

1. Resultatet visas i den högra panelen bredvid frågeredigeraren. Om frågan är felaktig visas ett fel på den högra panelen.

   ![byPath-frågeresultat](assets/extract-content/bypath-query-results.png)

Du har precis validerat en byPath-fråga för att hämta ett specifikt innehållsfragment som identifieras av sökvägen för det fragmentet.

## Fråga ditt eget innehåll {#own-queries}

Nu när du har kört de två primära typerna av frågor kan du fråga efter ditt eget innehåll!

1. Om du vill köra frågor mot dina egna innehållsfragment ändrar du slutpunkten från **AEM demoresurser** mapp till **Ditt projekt** mapp.

   ![Välj en egen slutpunkt](assets/extract-content/select-endpoint.png)

1. Ta bort allt befintligt innehåll i frågeredigeraren. Skriv sedan inledande hakparentes `{` och tryck på Ctrl+Blanksteg eller Alt+Blanksteg om du vill visa en lista över de modeller som definierats i slutpunkten automatiskt. Välj den modell som du skapade och som slutar i `List` från alternativen.

   ![Komplettera automatiskt modeller i frågeredigeraren](assets/extract-content/auto-complete-models.png)

1. Definiera de objekt som frågan ska innehålla för den valda innehållsfragmentmodellen. Igen, skriv den öppna klammerparentesen `{`och trycker sedan på Ctrl+Blanksteg eller Alt+Blanksteg för att visa en lista som fylls i automatiskt. Välj `items` från alternativen.

   ![Fyll i objekt automatiskt i frågeredigeraren](assets/extract-content/auto-complete-items.png)

1. Definiera fälten som frågan ska innehålla för innehållsfragmentmodellen som du valde. Ännu en gång: skriv den öppna hakparentesen `{`Tryck sedan på Ctrl+Blanksteg eller Alt+Blanksteg för att få en lista över tillgängliga fält i modellen för innehållsfragment automatiskt. Välj fält som du vill använda från modellen i listan.

   ![Fyll i fält automatiskt i frågeredigeraren](assets/extract-content/auto-complete-fields.png)

1. Avgränsa flera fält med kommatecken (`,`) eller blanksteg och tryck på Ctrl+Blanksteg eller Alt+Blanksteg igen för att markera ytterligare fält.

1. När du arbetar kan du trycka eller klicka på **Förtifiera** för att automatiskt formatera koden så att den blir lättare att läsa.

   ![Förtifiera](assets/extract-content/prettify.png)

1. När du är klar trycker du på eller klickar på **Spela upp** längst upp till vänster i redigeraren för att köra frågan.

   ![Resultat av din egen fråga](assets/extract-content/custom-query-results.png)

1. Resultatet visas i den högra panelen bredvid frågeredigeraren.

Så här kan ert innehåll levereras till digitala upplevelser i flera kanaler.
