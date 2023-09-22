---
title: Hur lägger man till stöd för nya språk i ett adaptivt formulär baserat på kärnkomponenterna?
description: Lär dig hur du lägger till nya språkområden i ett adaptivt formulär.
source-git-commit: 056aecd0ea1fd9ec1e4c05299d2c50bca161615f
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---


# Lägg till en språkinställning för adaptiv Forms baserat på kärnkomponenter {#supporting-new-locales-for-adaptive-forms-localization}

| Version | Artikellänk |
| -------- | ---------------------------- |
| Foundation Components | [Klicka här](supporting-new-language-localization.md) |
| Kärnkomponenter | Den här artikeln |

AEM Forms har stöd för engelska (en), spanska (es), franska (fr), italienska (it), tyska (de), japanska (ja), portugisiska-brasilianska (pt-BR), kinesiska (zh-CN), kinesiska-taiwanesiska (zh-TW) och koreanska (ko-KR).

## Hur väljs språkinställningen för ett anpassat formulär?

Det finns två metoder för att identifiera och välja språkområde för ett adaptivt formulär när det återges:

* **Använda [locale] Väljaren i URL**: Vid återgivning av ett adaptivt formulär identifierar systemet det begärda språkområdet genom att granska [locale] -väljaren i det adaptiva formulärets URL. URL:en har följande format: http:/[AEM Forms Server-URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled. Användning av [locale] -väljaren gör det möjligt att cachelagra det adaptiva formuläret.

* Hämtar parametrarna i den ordning som anges nedan:

   * Begäranparameter `afAcceptLang`: Om du vill åsidosätta användarens språkområde i webbläsaren kan du skicka begäran-parametern afAcceptLang. Den här URL:en tvingar till exempel formulärets rendering på kanadensisk franska: `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`.

   * Webbläsarens språkinställning (Accept-Language Header): Systemet hanterar också användarens språkområde i webbläsaren, som anges i begäran med hjälp av `Accept-Language` header.

  Om det inte finns något klientbibliotek för det begärda språket kontrollerar systemet om det finns ett klientbibliotek för språkkoden i språket. Om det begärda språket till exempel är `en_ZA` (sydafrikansk engelska) och det finns inget klientbibliotek för `en_ZA`används klientbiblioteket för en (engelska) om tillgängligt. Om ingen av dem hittas, används lexikonet för `en` språkinställning.

  När språkområdet har identifierats väljer det adaptiva formuläret motsvarande formulärspecifika ordlista. Om det inte går att hitta ordlistan för det begärda språket använder den som standard ordlistan på det språk som det anpassade formuläret skapades på.

  Om ingen språkinformation finns tillgänglig visas det adaptiva formuläret på sitt originalspråk, det språk som används under formulärutvecklingen


## Förutsättningar {#prerequistes}

Innan du börjar lägga till stöd för ett nytt språk

* Installera en vanlig textredigerare (IDE) för enklare redigering. Exemplen i det här dokumentet är baserade på Microsoft® Visual Studio Code.
* Klona den adaptiva Forms Core Components-databasen. Så här klonar du databasen:
   1. Öppna kommandoraden eller terminalfönstret och navigera till en plats där databasen ska lagras. Till exempel `/adaptive-forms-core-components`
   1. Kör följande kommando för att klona databasen:

      ```SHELL
          git clone https://github.com/adobe/aem-core-forms-components.git
      ```

  Databasen innehåller ett klientbibliotek som behövs för att lägga till en språkinställning.


## Lägga till en språkinställning {#add-localization-support-for-non-supported-locales}

Så här lägger du till stöd för en ny språkinställning:

![Lägga till en språkinställning i en databas](add-a-locale-adaptive-form-core-components.png)

### Klona din AEM as a Cloud Service Git-databas {#clone-the-repository}

1. Öppna kommandoraden och välj en katalog där databasen ska lagras, t.ex. `/cloud-service-repository/`.

1. Kör följande kommando för att klona databasen:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/
   ```

   Ersätt `<my-org>` och `<my-program>` i ovanstående URL med ditt organisationsnamn och programnamn. Detaljerade instruktioner om hur du får reda på organisationens namn, programnamn eller den fullständiga sökvägen till Git-databasen och de inloggningsuppgifter som krävs för att klona databasen finns i [Åtkomst till Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) artikel.

   När kommandot är klart skapas en mapp `<my-program>` skapas. Den innehåller det innehåll som klonats från Git-databasen. I resten av artikeln refereras mappen som, `[AEM Forms as a Cloud Service Git repository]`.


### Lägg till den nya språkinställningen i tjänsten för guidelokalisering {#add-a-locale-to-the-guide-localization-service}

1. Öppna databasmappen, som klonats i föregående avsnitt, i en vanlig textredigerare.
1. Navigera till `[AEM Forms as a Cloud Service Git repository]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config` mapp. Du hittar `<appid>` i `archetype.properties` filer i projektet.
1. Öppna `[AEM Forms as a Cloud Service Git repository]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config/Guide Localization Service.cfg.json` fil för redigering. Om filen inte finns skapar du den. En exempelfil med språkområden som stöds ser ut så här:

   ![Ett exempel på en guide till lokaliseringstjänsten.cfg.json](locales.png)

1. Lägg till [språkkod](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) som du vill lägga till, till exempel, &quot;hi&quot; för hindi.
1. Spara och stäng filen.

### Skapa ett klientbibliotek för att lägga till en språkinställning

AEM Forms har ett exempelbibliotek som hjälper dig att enkelt lägga till nya språkområden. Du kan hämta och lägga till `clientlib-it-custom-locale` klientbibliotek från den adaptiva Forms Core Components-databasen på GitHub till din as a Cloud Service Forms-databas. Så här lägger du till klientbiblioteket:

1. Öppna databasen Adaptive Forms Core Components i textredigeraren. Om databasen inte är klonad kan du läsa [Förutsättningar](#prerequistes) för instruktioner om hur du klonar databasen.
1. Navigera till `/aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs` katalog.
1. Kopiera `clientlib-it-custom-locale` katalog.
1. Navigera till `[AEM Forms as a Cloud Service Git repository]/ui.apps/src/main/content/jcr_root/apps/moonlightprodprogram/clientlibs` och klistra in `clientlib-it-custom-locale` katalog.


### Skapa en språkspecifik fil {#locale-specific-file}

1. Navigera till `[AEM Forms as a Cloud Service Git repository]/ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/`
1. Leta reda på [English locale .json file on GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json), som innehåller den senaste uppsättningen standardsträngar som ingår i produkten.
1. Skapa en JSON-fil för just din språkinställning.
1. I den nyligen skapade .json-filen speglar du strukturen i den engelska språkfilen.
1. Ersätt de engelska språksträngarna i din .json-fil med motsvarande översatta strängar för ditt språk.
1. Spara och stäng filen.


### Lägg till språkstöd i ordlistan {#add-locale-support-for-the-dictionary}

Utför endast det här steget om `<locale>` du lägger till är inte bland `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Navigera till `[AEM Forms as a Cloud Service Git repository]/ui.content/src/main/content/jcr_root/etc/` mapp.

1. Skapa en `etc` mappen under `jcr_root` om den inte finns.

1. Skapa en mapp `languages` under `etc` om den inte finns.

   ![Alt-text](etc-content-xml.png)

1. Skapa en `.content.xml` filen under `languages` mapp. Lägg till följande innehåll i filen:

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr]"/>
   ```

1. Lägg till språkkoden i `languages` -egenskap. Hhi har till exempel lagts till som hindi till följande exempelkod.


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

1. Lägg till de nya mapparna i `filter.xml` under `/ui.content/src/main/content/meta-inf/vault/filter.xml` as:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Lägg till de nyligen skapade mapparna i `filter.xml` under `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

### Bekräfta ändringarna och distribuera pipelinen {#commit-changes-in-repo-deploy-pipeline}

Genomför ändringarna i GIT-databasen när du har lagt till ett nytt språkstöd. Distribuera koden med hela stackpipeline. Läs [hur du ställer in en pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) för att lägga till stöd för nya språk.

När pipeline-körningen har slutförts är den nya språkinställningen klar att användas.

## Förhandsgranska ett anpassat formulär med nyligen tillagda språk {#use-added-locale-in-af}

Utför följande steg för att förhandsgranska en anpassad version med nyligen tillagda nationella inställningar:

1. Logga in på din as a Cloud Service AEM Forms-instans.
1. Gå till **Forms** >  **Forms och dokument**.
1. Välj ett anpassat formulär och klicka på **Lägg till ordlista** och **Lägg till ordlista i översättningsprojekt** visas.
1. Ange **Projektets titel** och väljer **Målspråk** i listrutan i **Lägg till ordlista i översättningsprojekt** guide.
1. Klicka **Klar** och kör det skapade översättningsprojektet.
1. Välj ett anpassat formulär och klicka på **Förhandsgranska som HTML**.
1. Lägg till `&afAcceptLang=<locale-name>` i URL:en för ett adaptivt formulär.
1. Uppdatera sidan och Adaptiv form renderas i en angiven språkinställning.

Det finns två metoder för att identifiera språkområdet i en adaptiv form. När ett anpassat formulär återges identifieras det begärda språket av:

* Hämtar `[local]` väljaren i den anpassningsbara formulärets URL. URL-formatet är `http:/[AEM Forms Server URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Använda `[local]` -väljaren tillåter cachelagring av ett adaptivt formulär.

* Hämtar följande parametrar i listordningen:

   * Begäranparameter `afAcceptLang`
Om du vill åsidosätta webbläsarens språkområde för användare kan du skicka `afAcceptLang` begär parameter för att tvinga språkområdet. Följande URL-adress tvingar till exempel formuläret att återges på kanadensisk-fransk plats:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * Webbläsarens språkområdesuppsättning för användaren, som anges i begäran med `Accept-Language` header.

Om det inte finns något klientbibliotek för det begärda språket söker programmet efter språkkoden i klientbiblioteket. Om det begärda språket till exempel är `en_ZA` (South Africa English) och klientbiblioteket för `en_ZA` finns inte, det adaptiva formuläret använder klientbiblioteket `en` (Engelska), om det finns. Om det inte finns någon av dem används lexikonet för `en` språkinställning.

När språkinställningen har identifierats väljer adaptiv form den formulärspecifika ordlistan. Om det inte går att hitta den formulärspecifika ordlistan för den begärda språkversionen används ordlistan för det språk som Adaptiv form har skapats på.

Om det inte finns någon tillgänglig språkinformation visas det adaptiva formuläret på sitt ursprungliga språk, det språk som användes vid formulärutvecklingen.


## De bästa sätten att stödja ny lokalisering {#best-practices}

* Adobe rekommenderar att du skapar ett översättningsprojekt när du har skapat ett adaptivt formulär.

* När nya fält läggs till i ett befintligt adaptivt formulär:
   * **För maskinöversättning**: Återskapa ordlistan och kör översättningsprojektet. Fält som läggs till i ett adaptivt formulär när du har skapat ett översättningsprojekt förblir oöversatta.
   * **För mänsklig översättning**: Exportera ordlistan via `[server:port]/libs/cq/i18n/gui/translator.html`. Uppdatera ordlistan för de nya fälten och överför den.


