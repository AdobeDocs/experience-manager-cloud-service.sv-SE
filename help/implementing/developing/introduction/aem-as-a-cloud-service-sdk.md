---
title: AEM as a Cloud Service SDK
description: Översikt över AEM som Cloud Service Software Development Kit
translation-type: tm+mt
source-git-commit: 0b46cc8ce4229138df84c70193cf9068e1200f0a
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---


# The AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM som Cloud Service-SDK består av följande artefakter:

* **QuickStart JAR** - AEM som används för lokal utveckling
* **Java API Jar** - Java Jar/Maven Dependency, som visar alla Java API:er som kan användas för att utveckla mot AEM som Cloud Service. Tidigare kallad Uberjar
* **Javadoc Jar** - javadokarna för Java API Jar
* **Dispatcher Tools** - den uppsättning verktyg som används för att utveckla mot Dispatcher lokalt. Separata artefakter för unix och windows

Dessutom kommer vissa kunder som tidigare har distribuerats med AEM 6.5 eller tidigare att använda artefakterna nedan. Om den lokala kompileringen inte fungerar med Quickstart-behållaren och du misstänker att den beror på gränssnitt som har tagits bort från AEM distribuerats som en Cloud Service, kontaktar du kundsupporten för att avgöra om du behöver åtkomst. Detta kräver ändringar i serverdelen.

* **6.5 Borttagen Java API JAR** - ytterligare en uppsättning gränssnitt som har tagits bort sedan AEM 6.5
* **6.5 Borttagen Javadoc Jar** - Javadocs för den extra uppsättningen gränssnitt

## Building for the SDK {#building-for-the-sdk}

AEM som en Cloud Service-SDK används för att skapa och distribuera anpassad kod. Mer information finns i dokumentationen [för](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en)AEM Project Archetype. På en hög nivå utförs följande steg:

* **Kompilera kod**. Som förväntat kompileras källkoden och de resulterande innehållspaketen genereras
* **Skapa artefakter**. Artefakter skapas under den här processen
* **Analysera paket**. Paketen analyseras med Maven analyzer-pluginen som söker efter problem i Maven-projektet, till exempel saknade beroenden
* **Distribuera artefakter**. Artefakter distribueras till den lokala servern.

Samma steg utförs av Cloud Manager när du distribuerar till molnmiljöer. När du utför byggen lokalt kan du utveckla och testa lokalt så att utvecklarna effektivt kan identifiera kod- eller strukturproblem innan de bestämmer sig för källkontroll och utlöser driftsättningar i Cloud Manager, vilket kan ta längre tid.

## Åtkomst till AEM som en Cloud Service-SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Du kan ta reda på vilken version av AEM som du använder i produktionen genom att titta på AEM Admin Console **Om Adobe Experience Manager** .
* Snabbstartsverktyget och Dispatcher Tools kan laddas ned som en zip-fil från [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Observera att åtkomsten till SDK-listorna är begränsad till dem som har AEM Managed Services eller AEM som en Cloud Service-miljö.
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

>[!NOTE]
>
>Versionsposten för SDK ska matcha versionen av AEM som en Cloud Service. Du kan se vilken version du använder genom att logga in på AEM och sedan gå till frågetecknet i skärmens övre högra hörn och välja **[!UICONTROL About Adobe Experience Manager]**


## Uppdatera ett lokalt projekt med en ny SDK-version {#refreshing-a-local-project-with-a-new-skd-version}

När rekommenderas att det lokala projektet uppdateras med ett nytt SDK?

Vi *rekommenderar* att du uppdaterar den minst efter en månadsvis underhållsrelease.

Det är *valfritt* att uppdatera den efter en daglig underhållsrelease. Kunderna informeras när deras produktionsinstans har uppgraderats till en ny AEM. För de dagliga underhållsreleaserna förväntas inte att det nya SDK-värdet kommer att ha ändrats avsevärt, om något alls. Vi rekommenderar dock att du ibland uppdaterar den lokala AEM utvecklingsmiljön med den senaste SDK:n och sedan återskapar och testar det anpassade programmet. Den månatliga underhållsreleasen innehåller vanligtvis mer omfattande ändringar och utvecklare bör därför omedelbart uppdatera, återskapa och testa.

Nedan beskrivs den rekommenderade proceduren för uppdatering av en lokal miljö:

1. Se till att allt användbart innehåll antingen är implementerat i projektet i källkontrollen eller tillgängligt i ett ändringsbart innehållspaket för senare import
1. Lokalt utvecklingstestinnehåll måste lagras separat så att det inte distribueras som en del av molnhanterarens pipeline-bygge. Detta beror på att det bara behöver användas för lokal utveckling
1. Stoppa snabbstart som körs
1. Flytta `crx-quickstart` mappen till en annan mapp för säker lagring
1. Observera den nya AEM-versionen som beskrivs i Cloud Manager (används för att identifiera den nya QuickStart Jar-versionen som du kan ladda ned ytterligare)
1. Ladda ned QuickStart JAR vars version matchar Production AEM-versionen från Software Distribution Portal
1. Skapa en helt ny mapp och placera den nya QuickStart Jar i
1. Starta den nya snabbstarten med de körningslägen du vill ha (antingen genom att byta namn på filen eller genom att skicka i körningslägen via `-r`).
   * Kontrollera att det inte finns någon kvar av den gamla snabbstarten i mappen.
1. Bygg AEM
1. Distribuera AEM till lokala AEM via PackageManager
1. Installera alla ändringsbara innehållspaket som behövs för lokal miljötestning via PackageManager
1. Fortsätt med utvecklingen och distribuera ändringarna efter behov

Om det finns innehåll som ska installeras med varje ny AEM snabbstartversion, inkluderar du det i ett innehållspaket och i projektets källkontroll. Installera det sedan varje gång.

Rekommendationen är att uppdatera SDK ofta (t.ex. varannan vecka) och ta bort hela lokala tillstånd varje dag för att inte vara beroende av tillståndskänsliga data i programmet.

Om du är beroende av CryptoSupport ([antingen genom att konfigurera inloggningsuppgifterna för Cloudservices eller SMTP Mail-tjänsten i AEM eller genom att använda CryptoSupport API i ditt program](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), krypteras de krypterade egenskaperna av en nyckel som genereras automatiskt första gången en AEM startas. Molnkonfigurationen tar hand om automatisk återanvändning av den miljöspecifika CryptoKey, men du måste injicera kryptonyckeln i den lokala utvecklingsmiljön.

Som standard är AEM konfigurerat för att lagra nyckeldata i en mapps datamapp, men för att underlätta återanvändning under utvecklingen kan AEM initieras vid första starten med &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Detta genererar krypteringsdata på &quot;`/etc/key`&quot;.

För att kunna återanvända innehållspaket som innehåller de krypterade värdena måste du följa dessa steg:

* När du startar den lokala quickstart.jar ska du lägga till parametern nedan: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Vi rekommenderar att du alltid lägger till det, men det är valfritt.
* Första gången du startar en instans skapar du ett paket som innehåller ett filter för roten &quot;`/etc/key`&quot;. Detta håller hemligheten att återanvändas i alla miljöer som du vill att de ska återanvändas för
* Exportera muterbart innehåll som innehåller hemligheter eller slå upp krypterade värden via för `/crx/de` att lägga till det i paketet som ska återanvändas i alla installationer
* När du skapar en ny instans (antingen för att ersätta med en ny version eller för att flera utvecklingsmiljöer ska dela inloggningsuppgifterna för testning) installerar du paketet som skapats i steg 2 och 3 för att kunna återanvända innehållet utan att behöva konfigurera om det manuellt. Detta beror på att nu är kryptonyckeln synkroniserad.
