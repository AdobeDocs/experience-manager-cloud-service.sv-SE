---
title: Hur lägger jag till stöd för nya språkområden i ett adaptivt formulär baserat på kärnkomponenterna?
description: Lär dig hur du lägger till nya språkområden i ett adaptivt formulär.
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 0%

---

# Lägg till en språkinställning för adaptiv Forms baserat på kärnkomponenter {#supporting-new-locales-for-adaptive-forms-localization}

| Version | Artikellänk |
| -------- | ---------------------------- |
| Foundation Components | [Klicka här](supporting-new-language-localization.md) |
| Kärnkomponenter | Den här artikeln |

<span class="preview"> Språkstöd för höger-till-vänster-språk är tillgängligt i det tidiga adopterprogrammet. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

AEM Forms har stöd för engelska (en), spanska (es), franska (fr), italienska (it), tyska (de), japanska (ja), portugisiska-brasilianska (pt-BR), kinesiska (zh-CN), kinesiska-taiwanesiska (zh-TW) och koreanska (ko-KR). Du kan även lägga till stöd för fler språkområden, som Hindi(hi_IN). Du kan också presentera Adaptiv Forms på höger-till-vänster-språk (RTL) som arabiska, persiska och urdu genom att lägga till dessa språkområden.

## Hur avgör AEM Forms språkområdet för ett adaptivt formulär?

Att förstå hur AEM Forms väljer språkområde för återgivning av ett adaptivt formulär är avgörande för en korrekt lokalisering. Här följer en beskrivning av urvalsprocessen:

### Prioritetsbaserad språkinställning

AEM Forms prioriterar följande metoder för att fastställa språkområdet för ett adaptivt formulär:

1. **URL-språkväljare ([locale])**:

   Systemet prioriterar det språkområde som anges i URL:en med väljaren [locale] . Det här formatet möjliggör cachelagring för bättre prestanda.

   Format: URL:en har följande format: http:/[AEM Forms Server URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled.

   Exempel: https://[server]/content/forms/af/contact-us.hi.html återger formuläret på hindi.


1. **afAcceptLang-begärandeparameter**:

   Om du vill åsidosätta användarens språkområde i webbläsaren kan du använda parametern `afAcceptLang` i URL:en.

   Exempel: https://[server]/forms/af/survey.ca-fr.html?afAcceptLang=ca-fr tvingar formuläret att återges på kanadensisk franska.

1. **Användarens språkområde (Accept-Language Header)**:

   Om ingen annan språkinställning har angetts hanterar AEM Forms användarens språkområde i webbläsaren som har skickats med rubriken `Accept-Language`.


### Reservmekanism:


* Om ett klientbibliotek (processen för att lägga till ett nytt språk, som förklaras senare i det här dokumentet) för det begärda språket inte är tillgängligt söker AEM Forms efter ett bibliotek baserat på språkkoden i språkinställningen.

  Exempel: Om en_ZA (sydafrikansk engelska) begärs och det inte finns något en_ZA-bibliotek, används en (engelska) om tillgängligt.

  Om inget lämpligt klientbibliotek hittas används standardordlistan (mest `en`) för formulärets redigeringsspråk.

  Om det inte finns någon språkområdesinformation visas det adaptiva formuläret på det ursprungliga språk som användes under utvecklingen.


## Krav för att lägga till en språkinställning

Innan du börjar lägga till en ny språkinställning för din adaptiva Forms måste du ha följande:

**Programvara:**

* Oformaterad textredigerare (IDE): En integrerad utvecklingsmiljö (IDE) som [Microsoft Visual Studio Code](https://code.visualstudio.com/download) fungerar, men en vanlig textredigerare har avancerade funktioner för enklare redigering.

* Git: Det här versionskontrollsystemet krävs för att hantera kodändringar. Om du inte har det installerat hämtar du det från [https://git-scm.com](https://git-scm.com).


**Koddatabas:**

Klona den adaptiva Forms Core Components-databasen: Du behöver ett klientbibliotek från den här databasen för att lägga till en språkinställning. Så här klonar du databasen:

1. Öppna kommandoraden eller terminalfönstret.

1. Navigera till önskad plats på datorn där du vill lagra databasen (till exempel /adaptive-forms-core-components).

1. Kör följande kommando för att klona databasen:

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   Det här kommandot hämtar databasen och skapar en mapp med namnet `aem-core-forms-components` på datorn. I den här guiden ser vi den här mappen som `[Adaptive Forms Core Components repository]`


## Lägga till en språkinställning {#add-localization-support-for-non-supported-locales}

Följ de här stegen för att lägga till stöd för nya språkområden i ett adaptivt formulär baserat på kärnkomponenter:

### Klona din AEM as a Cloud Service Git-databas

1. Öppna kommandoraden och välj en katalog där AEM as a Cloud Service-databasen ska lagras, t.ex. `/cloud-service-repository/`.

1. Kör följande kommando för att klona databasen:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   För att klona din Git-databas behöver du viss information:

   * **Organisationsnamn**: Detta identifierar ditt team eller projekt inom Adobe Experience Manager as a Cloud Service (AEM as a Cloud Service).

   * **Program-ID**: Detta anger det program som är associerat med din databas.

   * **Autentiseringsuppgifter**: Du behöver ett användarnamn och ett lösenord (eller en personlig åtkomsttoken) för att komma åt databasen på ett säkert sätt.

   **Var hittar du den här informationen?**

   Stegvisa instruktioner om hur du hittar dessa uppgifter finns i Adobe Experience League-artikeln [Accessing Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

   **Projektet är klart!**

   När kommandot har slutförts visas en ny mapp som har skapats i din lokala katalog. Den här mappen namnges efter programmet (till exempel program-id). Den här mappen innehåller alla filer och all kod som hämtats från din AEM as a Cloud Service Git-databas.

   I hela den här guiden ser vi den här mappen som `[AEMaaCS project directory]`.


### Lägg till den nya språkinställningen i tjänsten för guidelokalisering

1. Öppna databasmappen i en redigerare.

   ![Databasmapp i en redigerare](/help/forms/assets/repository-folder-in-an-editor.png)

1. Leta reda på filen `Guide Localization Service.cfg.json`. Den här filen kontrollerar de språkområden som stöds av ditt AEM Forms-program. Du kan redigera den här filen om du vill lägga till en ny språkinställning.

   * **Befintlig fil**: Om filen redan finns letar du reda på den i AEM Forms projektkatalog. Den typiska platsen är:

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     Ersätt `<appid>` med ditt projektspecifika program-ID. Du kan hitta `<appid>` för ditt AEM projekt i filen `archetype.properties`.

     ![Egenskaper för arkitekttyp](/help/forms/assets/archetype-properties.png)

   * **Ny fil**: Om filen inte finns måste du skapa den på samma plats som anges ovan. Kopiera inte filnamnet från det här dokumentet, utan skriv in namnet manuellt. Filnamnet `Guide Localization Service.cfg.json` innehåller blanksteg. Detta är avsiktligt och inte ett stavfel i dokumentationen.

     En exempelfil med en lista över språk som stöds av OOTB är:

     ```
         {
             "supportedLocales":[
             "en",
             "fr",
             "de",
             "ja",
             "pt-br",
             "zh-cn",
             "zh-tw",
             "ko-kr",
             "it",
             "es"
             ]
         }
     ```

1. Lägg till språkkoden för det språk du vill använda i filen.
   1. Använd [List of ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) för att hitta den tvåbokstavskod som representerar det språk du vill använda.

   1. Inkludera språkkoden i filen `Guide Localization Service.cfg.json`. Här är några exempel:

      * Vänster till höger-språk:
         * Engelska (USA): en-US
         * Spanska (Spanien): es-ES
         * Franska (Frankrike): fr-FR
      * Höger till vänster-språk:
         * Arabiska (Förenade Arabemiraten): ar-ae
         * Hebreiska: han (eller iw for history reference)
         * Persiska: fa

1. När du har gjort ändringar kontrollerar du att filen `Guide Localization Service.cfg.json` är korrekt formaterad som en giltig JSON-fil. JSON-formateringsfel kan förhindra att det fungerar som det ska. Spara filen.



### Utnyttja exempelbiblioteket för enkel språkinställning

AEM Forms tillhandahåller ett användbart exempel på klientbibliotek, `clientlib-it-custom-locale`, för att förenkla tillägg av nya språkområden. Det här biblioteket ingår i [databasen för adaptiva Forms Core-komponenter](https://github.com/adobe/aem-core-forms-components), som finns på GitHub.


Kontrollera att du har en lokal kopia av databasen [Adaptive Forms Core Components] innan vi börjar. Annars kan du enkelt klona den med Git med följande kommando:

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

Det här kommandot hämtar hela databasen, inklusive clientlib-it-custom-locale-biblioteket, till en katalog med namnet aem-core-forms-components på datorn.

![Katalog för adaptiv Forms Core Components-databas på den lokala datorn](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### Integrera exempelklientbiblioteket

Nu ska vi lägga in biblioteket `clientlib-it-custom-locale` i din AEM as a Cloud Service, [AEMaaCS-projektkatalog]:

1. Leta reda på exempelklientbiblioteket:

   Gå till följande sökväg i den lokala kopian av [adaptiva Forms Core Components-databasen]:

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. Kopiera och klistra in biblioteket:

   1. Kopiera mappen `clientlib-it-custom-locale`.

      ![Kopierar clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. Navigera till följande katalog i din [AEMaaCS-projektkatalog]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **Viktigt**: Ersätt `<app-id>` med ditt programs faktiska ID.

   1. Klistra in den kopierade mappen `clientlib-it-custom-locale` i den här katalogen.

      ![Klistrar in clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-paste.png)


### Skapa en fil för din nya språkinställning:

1. Navigera till språkkatalogen:

   Navigera till följande sökväg i din `[AEMaaCS project directory]`:

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **Viktigt**: Ersätt `<program-id>` med ditt faktiska program-ID.

1. Leta reda på exempelfilen för engelska:

   AEM Forms tillhandahåller en [exempelfil för engelska språk (.json) på GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json).

   Den engelska språkfilen innehåller standarduppsättningen med strängar för referens. Den språkområdesspecifika filen bör härma strukturen i den engelska språkfilen.

   För språk som arabiska, hebreiska och farsi läses texten från höger till vänster (RTL) i stället för från vänster till höger (LTR) som engelska. För att formulären ska visas på rätt sätt på dessa språk rekommenderar vi att du använder våra exempelspråkfiler som vägledning. Dessa filer innehåller en referens för hur du formaterar text, datum och andra element för RTL-språk. Du kan hitta exempelfilerna för språkområdet för:

   * [Arabiska](/help/forms/assets/ar-ae.json)
   * [Hebreiska](/help/forms/assets/he.json)
   * [Persiska](/help/forms/assets/fa.json)

   Genom att utnyttja dessa exempelfiler kan du säkerställa att formulären blir en smidig upplevelse för användare som arbetar på RTL-språk.


1. Skapa din språkfil:

   1. Skapa en ny .json-fil i katalogen `i18n`.
   1. Namnge filen med rätt språkkod för det språk du vill arbeta med (t.ex. fr-FR.json för franska och ar-ae.json för arabiska). Strukturen i den här filen ska spegla den engelska språkfilen.


1. Struktur och översättning:

   1. Öppna den nya filen i en textredigerare.

   1. Ersätt de engelska värdena med motsvarande översättningar för målspråket.

   1. När du är klar med översättningen av strängarna sparar du filen.




### Lägg till språkstöd i ordlistan

Det här steget gäller endast för andra språk än de som stöds vanligtvis: engelska (en), tyska (de), spanska (es), franska (fr), italienska (it), brasiliansk portugisiska (pt-br), kinesiska (förenklad - zh_cn), kinesiska (traditionell - zh_tw), japanska (ja) och koreanska (ko_kr).

1. Hitta konfigurationsmappen:

   Navigera till följande katalog i din [AEMaaCS-projektkatalog]:

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. Skapa nödvändiga mappar (om de saknas):

   Om mappen `etc` inte finns i mappen `jcr_root` skapar du den. I `etc` skapar du en annan mapp med namnet `languages` om den saknas.

1. Skapa språkkonfigurationsfilen:

   Skapa en ny fil med namnet `.content.xml` i mappen `languages`. Kopiera inte filnamnet från det här dokumentet, utan skriv in namnet manuellt.

   ![skapa en ny fil med namnet `.content.xml`](etc-content-xml.png)

   Öppna den här filen och klistra in följande innehåll och ersätt [LOCALE_CODE] med den faktiska språkkoden (t.ex. ar-ae för arabiska).


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   VARNING: Ersätt inte den befintliga listan. Lägg i stället till den nya språkkoden inom hakparenteser, avgränsade med kommatecken, som detta (med ar-ae som exempel):

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. Inkludera de nya mapparna i filter.xml:

   Navigera till filen `/ui.content/src/main/content/meta-inf/vault/filter.xml` i [AEMaaCS-projektkatalogen].

   Öppna filen och lägg till följande rad i slutet:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Lägg till skapade mappar i `filter.xml` under `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

1. Spara filen.

### Distribuera den nyligen skapade språkinställningen till AEM

Nu kan du börja använda det nya språkområdet med din adaptiva Forms. Du kan

* Distribuera AEM as a Cloud Service, [AEMaaCS-projektkatalogen], till din lokala utvecklingsmiljö och testa den nya språkkonfigurationen på din lokala dator. Så här distribuerar du till din lokala utvecklingsmiljö:

   1. Kontrollera att den lokala utvecklingsmiljön är igång och körs. Om du inte redan har konfigurerat en lokal utvecklingsmiljö läser du i guiden [Konfigurera lokal utvecklingsmiljö för AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Öppna terminalfönstret eller kommandotolken.

   1. Navigera till [AEMaaCS-projektkatalogen]

   1. Kör följande kommando:

      ```
      mvn -PautoInstallPackage clean install
      ```

* Distribuera AEM as a Cloud Service, [AEMaaCS-projektkatalogen], till din Cloud Service. Så här distribuerar du till din Cloud Service:

   1. Genomför dina ändringar:

      När du har lagt till den nya språkkonfigurationen verkställer du ändringarna med ett tydligt Git-meddelande som beskriver språktillägget (till exempel&quot;Tillagt stöd för [språknamn]&quot;).

   1. Distribuera den uppdaterade koden:

      Utlös en distribution av koden via den [befintliga pipelinen för hela stacken](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline). Detta skapar och distribuerar automatiskt den uppdaterade koden med det nya språkstödet.

      Om du inte redan har konfigurerat en pipeline kan du läsa guiden [Konfigurera en pipeline för AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).


## Förhandsgranska ett anpassat formulär med nyligen tillagda språk

Med de här stegen får du hjälp att förhandsgranska ett adaptivt formulär med den nya språkinställningen:

1. Logga in på din AEM Forms as a Cloud Service-instans.
1. Gå till **Forms** > **Forms och dokument**.
1. Välj ett anpassat formulär och klicka på guiden **Lägg till ordlista** och **Lägg till ordlista i översättningsprojekt** visas.
1. Ange **Projektnamn** och välj **Målspråk** i listrutan i guiden **Lägg till ordlista i översättningsprojekt**.
1. Klicka på **Klar** och kör det skapade översättningsprojektet.
1. Gå till **Forms** > **Forms och dokument**.
1. Markera det anpassade formuläret och välj alternativet **Förhandsgranska som HTML**.
1. Lägg till `&afAcceptLang=<locale-name>` i förhandsgransknings-URL:en och tryck på returtangenten. Ersätt `<locale-name>` med den faktiska språkkoden. Det anpassningsbara formuläret visas på det angivna språket.

## De bästa sätten att stödja ny lokalisering {#best-practices}

* Adobe rekommenderar att du skapar ett översättningsprojekt när du har skapat ett adaptivt formulär. Detta effektiviserar lokaliseringsprocessen.
* När komponenterna Numerisk ruta och Datumväljare översätts till ett visst språkområde kan det uppstå formateringsproblem. För att minska detta har ett **Language**-alternativ integrerats i dialogrutan Konfigurera för [datumväljarkomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker#format-tab) och [Numeric Box-komponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/numeric-box#formats-configure-tab).


* Hantera nya fält:

   * **Maskinöversättning**: Om du använder maskinöversättning måste du återskapa ordlistan och [köra översättningsprojektet](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) igen när du har lagt till nya fält i ett befintligt adaptivt formulär. Nya fält som läggs till efter det inledande översättningsprojektet förblir oöversatta.

   * **Översättning av människor**: Exportera ordboken med användargränssnittet på `[AEM Forms Server]/libs/cq/i18n/gui/translator.html` för arbetsflöden för översättning av människor. Uppdatera ordlistan för de nya fälten och överför den reviderade versionen.


## Se även {#see-also}

{{see-also}}

* [Generera urkunder för Adaptive Forms](/help/forms/generate-document-of-record-core-components.md)
* [Lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

