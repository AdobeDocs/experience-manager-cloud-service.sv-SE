---
title: AEM as a Cloud Service SDK
description: Fylls i
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

---


# The AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM som en molntjänst-SDK består av följande artefakter:

* **QuickStart JAR** - AEM-miljön som används för lokal utveckling
* **Java API Jar** - Java Jar/Maven Dependency, som visar alla Java API:er som kan användas för att utveckla mot AEM som molntjänst. Tidigare kallad Uberjar
* **Javadoc Jar** - javadokarna för Java API Jar
* **Dispatcher Tools** - den uppsättning verktyg som används för att utveckla mot Dispatcher lokalt. Separata artefakter för unix och windows

Dessutom kommer vissa kunder som tidigare har distribuerats med AEM 6.5 eller tidigare att använda artefakterna nedan. Om den lokala kompileringen inte fungerar med QuickStart-behållaren och du misstänker att den beror på gränssnitt som har tagits bort från AEM distribuerat som en molntjänst, kontaktar du kundsupporten för att avgöra om du behöver åtkomst. Detta kräver ändringar i serverdelen.

* **6.5 Föråldrad Java API Jar** - ytterligare en uppsättning gränssnitt som har tagits bort sedan AEM 6.5
* **6.5 Borttagen Javadoc Jar** - Javadocs för den extra uppsättningen gränssnitt

## Åtkomst till AEM som en molntjänst-SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Du kan kontrollera ikonen **Om Adobe Experience Manager** på AEM Admin Console för att ta reda på vilken version av AEM du använder i produktionen.
* Snabbstartsverktyget och Dispatcher Tools kan laddas ned som en zip-fil från [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Observera att åtkomsten till SDK-listorna är begränsad till dem som har AEM Managed Services eller AEM som molntjänster.
* Java API Jar och Javadoc Jar kan laddas ned via maven-verktygen, antingen kommandoraden eller med den IDE du föredrar.
* Maven project poms ska referera till följande API Jar-paket. Det här beroendet ska också refereras i alla delpaketets omgångar.

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version>
  <scope>provided</scope>
</dependency>
```

>[!NOTE] Versionsposten för SDK ska matcha versionen av AEM som en molntjänst. Du kan se vilken version du använder genom att logga in på AEM, sedan gå till frågetecknet i skärmens övre högra hörn och välja **[!UICONTROL Om Adobe Experience Manager]**

* Fjärrkoordinaten för maven-databasen där paketet finns bör inkluderas i pom-filen.

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## Uppdatera ett lokalt projekt med en ny SDK-version {#refreshing-a-local-prokect-with-a-new-skd-version}

När rekommenderas att det lokala projektet uppdateras med ett nytt SDK?

Vi *rekommenderar* att du uppdaterar den minst efter en månadsvis underhållsrelease.

Det är *valfritt* att uppdatera den efter en daglig underhållsrelease. Kunderna informeras när deras produktionsinstans har uppgraderats till en ny AEM-version. För de dagliga underhållsreleaserna förväntas inte att det nya SDK-värdet kommer att ha ändrats avsevärt, om något alls. Vi rekommenderar dock att du ibland uppdaterar den lokala AEM-utvecklingsmiljön med den senaste SDK:n och sedan återskapar och testar det anpassade programmet. Den månatliga underhållsreleasen innehåller vanligtvis mer omfattande ändringar och utvecklare bör därför omedelbart uppdatera, återskapa och testa.

Nedan beskrivs den rekommenderade proceduren för uppdatering av en lokal miljö:

1. Se till att allt användbart innehåll antingen är implementerat i projektet i källkontrollen eller tillgängligt i ett ändringsbart innehållspaket för senare import
1. Lokalt utvecklingstestinnehåll måste lagras separat så att det inte distribueras som en del av molnhanterarens pipeline-bygge. Detta beror på att det bara behöver användas för lokal utveckling
1. Stoppa snabbstart som körs
1. Flytta `crx-quickstart` mappen till en annan mapp för säker lagring
1. Observera den nya AEM-versionen, som beskrivs i Cloud Manager (används för att identifiera den nya QuickStart Jar-versionen som du kan ladda ned ytterligare)
1. Ladda ned QuickStart JAR vars version matchar Production AEM-versionen från Software Distribution Portal
1. Skapa en helt ny mapp och placera den nya QuickStart Jar i
1. Starta den nya snabbstarten med de körningslägen du vill ha (antingen genom att byta namn på filen eller genom att skicka i körningslägen via `-r`).
   * Kontrollera att det inte finns någon kvar av den gamla snabbstarten i mappen.
1. Bygg ditt AEM-program
1. Distribuera ditt AEM-program till lokala AEM via PackageManager
1. Installera alla ändringsbara innehållspaket som behövs för lokal miljötestning via PackageManager
1. Fortsätt med utvecklingen och distribuera ändringarna efter behov

Om det finns innehåll som ska installeras med varje ny AEM snabbstartsversion inkluderar du det i ett innehållspaket och i projektets källkontroll. Installera det sedan varje gång.

Rekommendationen är att uppdatera SDK ofta (t.ex. varannan vecka) och ta bort hela lokala tillstånd varje dag för att inte vara beroende av tillståndskänsliga data i programmet.

Om du är beroende av CryptoSupport ([antingen genom att konfigurera inloggningsuppgifterna för Cloudservices eller SMTP Mail-tjänsten i AEM eller genom att använda CryptoSupport API i ditt program](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), krypteras de krypterade egenskaperna av en nyckel som genereras automatiskt första gången en AEM-miljö startas. Molnkonfigurationen tar hand om automatisk återanvändning av den miljöspecifika CryptoKey, men du måste injicera kryptonyckeln i den lokala utvecklingsmiljön.

Som standard är AEM konfigurerad för att lagra nyckeldata i en mapps datamapp, men för att underlätta återanvändning vid utveckling kan AEM-processen initieras vid första starten med&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Detta genererar krypteringsdata på &quot;`/etc/key`&quot;.

För att kunna återanvända innehållspaket som innehåller de krypterade värdena måste du följa dessa steg:

* När du startar den lokala quickstart.jar ska du lägga till parametern nedan: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Vi rekommenderar att du alltid lägger till det, men det är valfritt.
* Första gången du startar en instans skapar du ett paket som innehåller ett filter för roten &quot;`/etc/key`&quot;. Detta håller hemligheten att återanvändas i alla miljöer som du vill att de ska återanvändas för
* Exportera muterbart innehåll som innehåller hemligheter eller slå upp krypterade värden via för `/crx/de` att lägga till det i paketet som ska återanvändas i alla installationer
* När du skapar en ny instans (antingen för att ersätta med en ny version eller för att flera utvecklingsmiljöer ska dela inloggningsuppgifterna för testning) installerar du paketet som skapats i steg 2 och 3 för att kunna återanvända innehållet utan att behöva konfigurera om det manuellt. Detta beror på att nu är kryptonyckeln synkroniserad.