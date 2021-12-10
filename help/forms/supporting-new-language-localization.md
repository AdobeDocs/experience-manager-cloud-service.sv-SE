---
title: Stöd för nya språk för Adaptive Forms-lokalisering
seo-title: Supporting new locales for Adaptive Forms localization
description: Med AEM Forms kan du lägga till nya språk för lokalisering av adaptiv Forms. De språkområden som stöds är som standard engelska, franska, tyska och japanska.
seo-description: AEM Forms allows you to add new locales for localizing Adaptive Forms. The supported locales by default are English, French, German, and Japanese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---


# Stöd för nya språk för Adaptive Forms-lokalisering{#supporting-new-locales-for-adaptive-forms-localization}

## Om språkordlistor {#about-locale-dictionaries}

Lokaliseringen av Adaptive Forms bygger på två typer av språkordlistor:

**Formulärspecifik ordlista** Innehåller strängar som används i Adaptive Forms. Till exempel etiketter, fältnamn, felmeddelanden, hjälpbeskrivningar och så vidare. Den hanteras som en uppsättning XLIFF-filer för varje språkområde och du kan komma åt den på `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Globala ordlistor** Det finns två globala ordlistor, som hanteras som JSON-objekt, AEM klientbiblioteket. De här ordlistorna innehåller standardfelmeddelanden, namn på månader, valutasymboler, datum- och tidsmönster osv. Dessa ordlistor finns i CRXDe Lite på /libs/fd/xfaforms/clientlibs/I18N. Dessa platser innehåller separata mappar för varje språkområde. Eftersom globala ordlistor vanligtvis inte uppdateras så ofta, kan webbläsare cachelagra dem och minska användningen av nätverksbandbredd när de använder olika adaptiva Forms på samma server genom att behålla separata JavaScript-filer för varje språkområde.

### Hur lokalisering av adaptiv form fungerar {#how-localization-of-adaptive-form-works}

Det finns två metoder för att identifiera språkområdet i den adaptiva formen. När ett anpassat formulär återges identifieras det begärda språket av :

* tittar du på `[local]` i URL:en för adaptiv form. URL-formatet är `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Använda `[local]` -väljaren tillåter cachelagring av ett adaptivt formulär.

* Titta på följande parametrar i den angivna ordningen:

   * Begäranparameter `afAcceptLang`
Om du vill åsidosätta webbläsarens språkområde för användare kan du skicka 
`afAcceptLang` begär parameter för att tvinga språkområdet. Följande URL kommer till exempel att tvinga formuläret att återges på japanska språk:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * Webbläsarens språkområdesuppsättning för användaren, som anges i begäran med `Accept-Language` header.

   * Språkinställningen för den användare som anges i AEM.

   * Webbläsarens språkområde är aktiverat som standard. Om du vill ändra språkinställningen för webbläsaren
      * Öppna konfigurationshanteraren. URL:en är `http://[server]:[port]/system/console/configMgr`
      * Leta reda på och öppna **[!UICONTROL Adaptive Form and Interactive Communication Web Channel]** konfiguration.
      * Ändra status för **[!UICONTROL Use Browser Locale]** och  **[!UICONTROL Save]** konfigurationen.

När språkinställningen har identifierats väljer Adaptive Forms den formulärspecifika ordlistan. Om det inte går att hitta den formulärspecifika ordlistan för den begärda språkversionen används ordlistan för det språk som Adaptiv form skapades på.

Om det inte finns någon språkinformation levereras Adaptiv form på formulärets originalspråk. Det ursprungliga språket är det språk som används vid utvecklingen av det adaptiva formuläret.

Om det inte finns något klientbibliotek för det begärda språket söker programmet efter språkkoden i klientbiblioteket. Om det begärda språket till exempel är `en_ZA` (sydafrikansk engelska) och klientbiblioteket för `en_ZA` finns inte, det adaptiva formuläret använder klientbiblioteket för `en` (Engelska), om det finns. Om det inte finns någon av dem används lexikonet för `en` språkinställning.

## Lägg till lokaliseringsstöd för språk som inte stöds {#add-localization-support-for-non-supported-locales}

[!DNL AEM Forms] har för närvarande stöd för lokalisering av adaptivt Forms-innehåll på engelska (en), spanska (es), franska (fr), italienska (it), tyska (de), japanska (ja), portugisiska-brasilianska (pt-BR), kinesiska (zh-CN), kinesiska-taiwanesiska (zh-TW) och koreanska (ko-KR).

Så här lägger du till stöd för en ny språkinställning i Adaptive Forms runtime:

1. [Lägg till en språkinställning i tjänsten GuideLocalizationService](supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Lägg till XFA-klientbibliotek för en språkinställning](supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Lägg till klientbibliotek för adaptiva formulär för en språkinställning](supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Lägg till språkstöd för ordlistan](supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Starta om servern](supporting-new-language-localization.md#p-restart-the-server-p)

### Lägga till en språkinställning i tjänsten för guidelokalisering {#add-a-locale-to-the-guide-localization-service-br}

1. Gå till `https://'[server]:[port]'/system/console/configMgr`.
1. Klicka för att redigera **Guide Localization Service** -komponenten.
1. Lägg till det språkområde som du vill lägga till i listan över språkområden som stöds.

![GuideLocalizationService](assets/configservice.png)

### Lägg till XFA-klientbibliotek för en språkinställning {#add-xfa-client-library-for-a-locale-br}

Skapa en nod av typen `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, med kategori `xfaforms.I18N.<locale>`och lägg till följande filer i klientbiblioteket:

* **I18N.js** definiera `xfalib.locale.Strings` för `<locale>` enligt definition i `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** som innehåller följande:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Lägg till klientbibliotek för adaptiva formulär för en språkinställning {#add-adaptive-form-client-library-for-a-locale-br}

Skapa en nod av typen `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, med kategorin som `guides.I18N.<locale>` och beroenden som `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` och `guide.common`. &quot;

Lägg till följande filer i klientbiblioteket:

* **i18n.js** definiera `guidelib.i18n`, som har mönster av &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` för `<locale>` enligt XFA-specifikationerna som beskrivs i [Ange nationella inställningar](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). Du kan också se hur den är definierad för andra språkområden som stöds i `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definiera `guidelib.i18n.strings` och `guidelib.i18n.LogMessages` för `<locale>` enligt definition i `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** som innehåller följande:

```text
i18n.js
LogMessages.js
```

### Lägg till språkstöd för ordlistan {#add-locale-support-for-the-dictionary-br}

Utför endast det här steget om `<locale>` du lägger till är inte bland `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Skapa en `nt:unstructured` nod `languages` under `etc`, om det inte redan finns.

1. Lägga till en flervärdessträngsegenskap `languages` till noden, om den inte redan finns.
1. Lägg till `<locale>` standardvärden för nationella inställningar `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, om det inte redan finns.

1. Lägg till `<locale>` till värdena för `languages` egenskap för `/etc/languages`.

The `<locale>` visas på `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Starta om servern {#restart-the-server}

Starta om AEM för att den tillagda språkinställningen ska börja gälla.

## Exempelbibliotek för att lägga till stöd för spanska {#sample-libraries-for-adding-support-for-spanish}

Exempel på klientbibliotek för att lägga till stöd för spanska

[Hämta fil](assets/sample.zip)
