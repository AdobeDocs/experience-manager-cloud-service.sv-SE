---
title: Hur lägger jag till stöd för nya språkområden i ett adaptivt formulär baserat på Foundation Components?
description: För Adaptiv Forms kan du lägga till språkområden för fler språk förutom det som finns i kartongen.
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 0%

---

# Stöd för nya språk för Adaptive Forms-lokalisering {#supporting-new-locales-for-adaptive-forms-localization}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html) |
| Kärnkomponenter | [Klicka här](supporting-new-language-localization-core-components.md) |
| Foundation Components | Den här artikeln |

AEM Forms har stöd för engelska (en), spanska (es), franska (fr), italienska (it), tyska (de), japanska (ja), portugisiska-brasilianska (pt-BR), kinesiska (zh-CN), kinesiska-taiwanesiska (zh-TW) och koreanska (ko-KR). Du kan även lägga till stöd för fler språkområden, som Hindi(hi_IN).

## Om språklexikon {#about-locale-dictionaries}

Lokaliseringen av anpassningsbara formulär bygger på två typer av språkordlistor:

* **Formulärspecifik ordlista** Innehåller strängar som används i adaptiva formulär. Till exempel etiketter, fältnamn, felmeddelanden och hjälpbeskrivningar. Den hanteras som en uppsättning XLIFF-filer för varje språkområde och du kan komma åt den på `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Globala ordlistor** Det finns två globala ordlistor, som hanteras som JSON-objekt, i AEM klientbibliotek. De här ordlistorna innehåller standardfelmeddelanden, namn på månader, valutasymboler, datum- och tidsmönster osv. Du hittar dessa ordlistor på `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Dessa platser innehåller separata mappar för varje språkområde. Eftersom globala ordlistor inte uppdateras så ofta kan olika JavaScript-filer för varje språkområde användas för att cachelagra dem och minska användningen av nätverksbandbredd vid åtkomst av olika adaptiva formulär på samma server.

## Lägg till stöd för nya språk {#add-support-for-new-locales}

Utför följande steg för att lägga till stöd för en ny språkinställning:

1. [Lägg till lokaliseringsstöd för språk som inte stöds](#add-localization-support-for-non-supported-locales)
1. [Använd tillagda språk i Adaptiv Forms](#use-added-locale-in-af)

### Lägg till lokaliseringsstöd för språk som inte stöds {#add-localization-support-for-non-supported-locales}

AEM Forms har för närvarande stöd för lokalisering av Adaptivt Forms-innehåll på engelska (en), spanska (es), franska (fr), italienska (it), tyska (de), japanska (ja), portugisiska-brasilianska (pt-BR), kinesiska (zh-CN), kinesiska-taiwanesiska (zh-TW) och koreanska (ko-KR).

Så här lägger du till stöd för en ny språkinställning i den adaptiva Forms-miljön:

1. [Klona din databas](#clone-the-repository)
1. [Lägg till en språkinställning i tjänsten GuideLocalizationService](#add-a-locale-to-the-guide-localization-service)
1. [Lägg till språknamnsspecifik mapp](#add-locale-name-specific-folder)
1. [Lägg till språkstöd för ordlistan](#add-locale-support-for-the-dictionary)
1. [Genomför ändringarna i databasen och distribuera pipeline](#commit-changes-in-repo-deploy-pipeline)

#### 1. Klona databasen {#clone-the-repository}

1. Navigera från kommandoraden till den plats där du vill klona Forms Cloud Service-databasen.
1. Kör kommandot som du [hämtat från Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) Det liknar `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Använd Git-användarnamnet och -lösenordet för att klona databasen.
1. Öppna den klonade Forms Cloud Service-databasmappen i det redigeringsprogram du föredrar.

#### 2. Lägg till en språkinställning i tjänsten för guidelokalisering {#add-a-locale-to-the-guide-localization-service}

1. Leta reda på `Guide Localization Service.cfg.json` och lägg till det språkområde som du vill lägga till i listan över språkområden som stöds.

   >[!NOTE]
   >
   > Skapa en fil med namnet som `Guide Localization Service.cfg.json` om filen inte finns.

#### 3. Lägg till språknamnsspecifikt mappklientbibliotek {#add-locale-name-specific-folder}

1. Skapa i mappen UI.content `etc/clientlibs` mapp.
1. Skapa sedan en mapp med namnet som `locale-name` under `etc/clientlibs` som behållare för xfa och af clientlibs.

##### 3.1 Lägg till XFA-klientbibliotek för en språkinställning i en mapp för språkinställningar

Skapa en nod med namnet som `[locale-name]_xfa` och skriv som `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`, med kategori `xfaforms.I18N.<locale>`och lägg till följande filer:

* **I18N.js** definiera `xfalib.locale.Strings` för `<locale>` enligt definition i `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** som innehåller följande:
  */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Lägg till klientbibliotek för adaptiv form för en språknamnsmapp

1. Skapa en nod med namnet som `[locale-name]_af` och skriv som `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`, med kategorin som `guides.I18N.<locale>` och beroenden som `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` och `guide.common`.
1. Skapa en mapp med namnet som `javascript` och lägga till följande filer:

   * **i18n.js** definiera `guidelib.i18n`, som har mönster av &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` för `<locale>` enligt XFA-specifikationerna som beskrivs i [Specifikation för språkinställning](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** definiera `guidelib.i18n.strings` och `guidelib.i18n.LogMessages` för `<locale>` enligt definition i `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Lägg till **js.txt** som innehåller följande:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Lägg till språkstöd för ordlistan {#add-locale-support-for-the-dictionary}

Utför endast det här steget om `<locale>` du lägger till är inte bland `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Skapa en mapp `languages` under `etc`, om det inte redan finns.

1. Lägga till en flervärdessträngsegenskap `languages` till noden, om den inte redan finns.
1. Lägg till `<locale-name>` standardvärden för nationella inställningar `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, om det inte redan finns.

1. Lägg till `<locale>` till värdena för `languages` egenskap för `/etc/languages`.
1. Lägg till skapade mappar i `filter.xml` under etc/META-INF/[mapphierarki] as:

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

Innan du implementerar ändringarna i AEM Git-databasen måste du få åtkomst till [Git-databasinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5. Genomför ändringarna i databasen och distribuera pipelinen {#commit-changes-in-repo-deploy-pipeline}

Genomför ändringarna i GIT-databasen när du har lagt till stöd för nationella inställningar. Distribuera koden med hela stackpipeline. Läs [hur du ställer in en pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) för att lägga till stöd för nya språk.
När pipeline är klar visas den nya språkinställningen i AEM.

### Använd tillagda nationella inställningar i Adaptiv Forms {#use-added-locale-in-af}

Utför följande steg för att använda och återge ett adaptivt formulär med nyligen tillagda nationella inställningar:

1. Logga in på AEM författarinstans.
1. Gå till **Forms** >  **Forms och dokument**.
1. Välj ett anpassat formulär och klicka på **Lägg till ordlista** och **Lägg till ordlista i översättningsprojekt** visas.
1. Ange **Projektets titel** och väljer **Målspråk** i listrutan i **Lägg till ordlista i översättningsprojekt** guide.
1. Klicka **Klar** och kör det skapade översättningsprojektet.
1. Välj ett anpassat formulär och klicka på **Förhandsgranska som HTML**.
1. Lägg till `&afAcceptLang=<locale-name>` i URL:en för ett adaptivt formulär.
1. Uppdatera sidan och Adaptiv form renderas i en angiven språkinställning.

Det finns två metoder för att identifiera språkområdet i en adaptiv form. När ett anpassat formulär återges identifieras det begärda språket av:

* Hämtar `[local]` väljaren i den anpassningsbara formulärets URL. URL-formatet är `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Använda `[local]` -väljaren tillåter cachelagring av ett adaptivt formulär.

* Hämtar följande parametrar i listordningen:

   * Begäranparameter `afAcceptLang`
Om du vill åsidosätta webbläsarens språkområde för användare kan du skicka `afAcceptLang` begär parameter för att tvinga språkområdet. Följande URL-adress tvingar till exempel formuläret att återges på kanadensisk-fransk plats:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * Webbläsarens språkområdesuppsättning för användaren, som anges i begäran med `Accept-Language` header.

Om det inte finns något klientbibliotek för det begärda språket söker programmet efter språkkoden i klientbiblioteket. Om det begärda språket till exempel är `en_ZA` (South Africa English) och klientbiblioteket för `en_ZA` finns inte, det adaptiva formuläret använder klientbiblioteket `en` (Engelska), om det finns. Om det inte finns någon av dem används lexikonet för `en` språkinställning.


När språkinställningen har identifierats väljer adaptiv form den formulärspecifika ordlistan. Om det inte går att hitta den formulärspecifika ordlistan för den begärda språkversionen används ordlistan för det språk som Adaptiv form har skapats på.

Om det inte finns någon språkinformation levereras Adaptiv form på formulärets originalspråk. Det ursprungliga språket är det språk som används vid utvecklingen av det adaptiva formuläret.

Få en [exempelklientbibliotek](/help/forms/assets/locale-support-sample.zip) för att lägga till stöd för nya språk. Du måste ändra innehållet i mappen på det språk som krävs.

## De bästa sätten att stödja ny lokalisering {#best-practices}

* Adobe rekommenderar att du skapar ett översättningsprojekt när du har skapat ett adaptivt formulär.

* När nya fält läggs till i ett befintligt adaptivt formulär:
   * **För maskinöversättning**: Återskapa ordlistan och kör översättningsprojektet. Fält som läggs till i ett adaptivt formulär när du har skapat ett översättningsprojekt förblir oöversatta.
   * **För mänsklig översättning**: Exportera ordlistan via `[server:port]/libs/cq/i18n/gui/translator.html`. Uppdatera ordlistan för de nya fälten och överför den.


## Se även {#see-also}

{{see-also}}