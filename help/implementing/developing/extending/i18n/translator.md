---
title: Internationaliserar gränssnittssträngar
description: AEM tillhandahåller en konsol för hantering av olika översättningar av texter som används i komponentens användargränssnitt.
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 14a6516872f842d099b902b9f633b1d6f984266d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Använda översättare för att hantera ordlistor{#using-translator-to-manage-dictionaries}

AEM tillhandahåller en konsol för hantering av olika översättningar av texter som används i komponentens användargränssnitt. Den här konsolen finns på:

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

Använd översättningsverktyget för att hantera engelska strängar och deras översättningar. Ordlistorna skapas i databasen, till exempel `/apps/myproject/i18n`.

Översättningsverktyget och de ordlistor du hanterar används för att presentera komponentgränssnitt på olika språk. Om du vill översätta sidor läser du [Översätta innehåll för flerspråkiga platser](/help/sites-cloud/administering/translation/overview.md).

## Skapa en ordlista {#creating-a-dictionary}

Utvecklare kan skapa i18n-ordlistor i AEM för att hantera lokaliserade komponentsträngar. Ordlistor är vanligtvis en del av komponentkoden i `/apps`. Följande är ett exempel från AEM WKND-kod med ett nyckel/värde-par som används i alla WKND-komponenter.

```
{
  "&copy; {0} WKND Site Site. All rights reserved." : "&copy; {0} WKND Site Site. Tous droits réservés."
}
```

Utvecklare kan skapa ytterligare ordlistor genom att lägga till en rotnod (`sling:Folder`) för en ny ordlista som innehåller språkdefinitioner för komponentsträngar.

```shell
/apps/myProject/i18n [sling:Folder]
    - de.json [nt:file] [mix:language]
        + jcr:language = de
    - fr.json [nt:file] [mix:language]
        + jcr:language = fr
```

>[!NOTE]
>
>Det här är strukturen från modulen [Sling i18n](https://sling.apache.org/site/internationalization-support.html).

När ordlistorna har skapats i en AEM GitHub-databas kan de distribueras via en AEM [CI/CD-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

## Ordlisteplatser {#dictionary-locations}

Det är fritt för utvecklare att skapa en källspråksordlista i antingen `/apps` eller `/content/cq:i18n`. Genom att börja med AEM exempelkod för arketypen finns initiala ordlistor vanligtvis i sökvägen `/apps`. Om målet är att lagra motsvarande ordlistekopior även i `/apps` måste dessa språkkopior skapas manuellt och underhållas av utvecklare i komponentkoden.

Den nya AEM runtime-översättningsprocessen för i18n-ordlistor skapar också översatta ordlistor i `/content/cq:i18n/<projectName>`, oavsett om källordlistan lagras i `/apps` eller `/content`.

Beslut om var i18n-ordlistor, källkopior och språkkopior ska placeras bör fattas enligt följande kriterier:

* `/apps`
   * standardplats för ordlistor med komponentsträngöversättningar, efter AEM och WKND-exempelkod
   * högsta återgivningsordning, per Sling ([Hierarkier för resurssökning](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies))
   * men ingen körningsredigering eller översättning av ordlistor är möjlig eftersom `/apps` inte kan ändras i AEM as a Cloud Service-miljöer

* `/content/cq:i18n`
   * alternativ plats för i18n-ordlistor om
      * Det krävs en översättning av ordlistor vid körning
      * kan inte redigera ett lexikon under körning krävs
   * standardplats där översättning av körningsordlista skapar språkkopior.

Eftersom `/apps` alltid ersätter `/content` i återgivningsordningen Sling är det viktigt att komma ihåg att ordlistor med identiska nyckel/värde-par inte får finnas samtidigt i `/apps` och `/content/cq:i18n`, eftersom ordlistan i `/content/cq:i18n` aldrig kommer att användas för återgivning. Om det redan finns en ordlistespråkkopia, dvs. ett översättningsmål, i `/apps` och målet är att göra den översättningsbar vid körning i AEM as a Cloud Service, måste den ursprungliga ordlistespråkskopian i `/apps` antingen flyttas till `/content/cq:i18n` eller tas bort i `/apps` och automatiskt återskapas i `/content/cq:i18n` genom översättning av källordlistan. Den här översättningsprocessen skapar automatiskt språkkopior i `/content/cq:i18n`.

## Skapa ordlista automatiskt {#automatic-creation}

För AEM sidor och upplevelsefragment som innehåller AEM huvudkomponenter skannar den nya ordlisteöversättningsprocessen även in dessa sidor eller använder fragment för komponenter och komponentsträngar som ska översättas. Systemet skapar sedan automatiskt motsvarande nya ordlistespråkskopior i `/content/cq:i18n`. Detta gäller inte för innehållsfragment eftersom dessa är rent, strukturerat innehåll utan AEM kärnkomponenter.

## Exportera en ordlista {#exporting-a-dictionary}

I körningsmiljön går det inte att översätta i18n-ordlistor på `/apps`- eller `/libs`-platser i AEM as a Cloud Service eftersom dessa platser inte kan ändras, men dessa ordlistor kan fortfarande exporteras vid körning för asynkron översättning utanför AEM.

Så här exporterar du källspråkssträngarna för ett lexikon till en XLIFF-fil:

1. Öppna översättningsverktyget `http://<host>:<port>/libs/cq/i18n/gui/translator.html`

   >[!NOTE]
   >
   >Verktyget är bara tillgängligt via denna URL. Det går inte att komma åt det från AEM produktgränssnitt.

1. Använd listrutan Ordlistor för att välja det lexikon som ska exporteras.
1. Klicka på Exportera XLIFF-översättning och sedan Exportera den fullständiga `<locale>` xliff.

## Importera en ordlista {#importing-a-dictionary}

Så här importerar du en XLIFF-fil till en ordlista för att fylla i ordlisteinnehållet:

1. Öppna översättningsverktyget `http://<host>:<port>/libs/cq/i18n/gui/translator.html`
1. Klicka på Importera och sedan på XLIFF-översättningar.
1. Markera filen som ska importeras och klicka på OK.
