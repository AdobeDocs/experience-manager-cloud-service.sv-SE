---
title: AEM as a Cloud Service SDK
description: En översikt över AEM as a Cloud Service Software Development Kit
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service SDK består av följande artefakter:

* **QuickStart JAR** - AEM som används för lokal utveckling
* **Java™ API Jar** - Java™ Jar/Maven Dependency som visar alla Java™-API:er som kan användas för att utveckla mot AEM as a Cloud Service. Tidigare kallad Uberjar
* **Javadoc Jar** - javadokarna för Java™ API Jar
* **Dispatcher-verktyg** - Den uppsättning verktyg som används för att utveckla mot Dispatcher lokalt. Separata felaktigheter för UNIX® och Windows

Vissa kunder som tidigare har distribuerats med AEM 6.5 eller tidigare använder artefakterna nedan. Om den lokala kompileringen inte fungerar med Quickstart-behållaren och du misstänker att den inte fungerar när gränssnitt tas bort från AEM distribuerade as a Cloud Service kontaktar du kundsupport. De kan avgöra om du behöver åtkomst. Det kräver ändringar i backend-objektet.

* **6.5 Java™ API Jar** är inaktuellt - en extra uppsättning gränssnitt som har tagits bort sedan AEM 6.5
* **6.5 Javadoc Jar** har tagits bort - Javadocs för den extra uppsättningen gränssnitt

## Building for the SDK {#building-for-the-sdk}

AEM as a Cloud Service SDK används för att skapa och distribuera anpassad kod. Se [AEM Project Archetype-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html). På en hög nivå utförs följande steg:

* **Kompilera kod**. Som förväntat kompileras källkoden och de resulterande innehållspaketen genereras
* **Skapa artefakter**. Artefakter skapas under den här processen
* **Analysera paket**. Paketen analyseras med Maven analyzer-pluginen som söker efter problem i Maven-projektet, till exempel saknade beroenden
* **Distribuera felaktigheter**. Artefakter distribueras till den lokala servern.

Samma steg utförs av Cloud Manager vid distribution till molnmiljöer. När du utför byggen lokalt kan du utveckla och testa dem lokalt. Utvecklare kan effektivt upptäcka kod eller strukturella problem innan de bestämmer sig för att ha källkontroll och utlösa Cloud Manager-driftsättningar, vilket kan ta längre tid.

>[!NOTE]
>
>AEM as a Cloud Service SDK bör byggas med en distribution och version av Java som stöds av [Cloud Manager byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). AEM as a Cloud Service-kunder kan hämta Oracle-JDK från [programdistributionsportalen](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) och ha Java 11 Extended Support (Utökat stöd) fram till september 2026 på grund av Adobe licensiering och supportvillkor för Oraclets Java-teknik när de används i Adobe Experience Manager-projekt.

## Åtkomst till AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Du kan kontrollera ikonen AEM Admin Console **Om Adobe Experience Manager** för att ta reda på vilken version av AEM du använder i produktionen.
* Snabbstartburken och Dispatcher Tools kan laddas ned som en zip-fil från [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Åtkomsten till SDK-listorna är begränsad till personer som har miljöer AEM Managed Services eller AEM as a Cloud Service.
* Java™ API Jar och Javadoc Jar kan laddas ned via maven-verktygen, antingen kommandoraden eller med den utvecklingsmiljö du föredrar.
* Maven project poms ska referera till följande API Jar-paket. Beroende av delpaketets öppningar ska också refereras.

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
>Versionsposten för SDK ska matcha versionen av AEM as a Cloud Service. Du kan se vilken version du använder genom att logga in på AEM. Gå till frågetecknet i skärmens övre högra hörn och välj **[!UICONTROL About Adobe Experience Manager]**.


## Uppdatera ett lokalt projekt med en ny SDK-version {#refreshing-a-local-project-with-a-new-skd-version}

När rekommenderas att det lokala projektet uppdateras med ett nytt SDK?

Adobe *rekommenderar att* uppdaterar den efter en månadsvis underhållsversion.

Det är *valfritt* att uppdatera det efter en daglig underhållsrelease. Kunderna informeras om när deras produktionsinstans har uppgraderats till en ny AEM. För de dagliga underhållsreleaserna förväntas inte att det nya SDK:t har ändrats avsevärt, om alls. Vi rekommenderar dock att du emellanåt uppdaterar den lokala AEM utvecklingsmiljön med den senaste SDK:n och sedan återskapar och testar det anpassade programmet. Den månatliga underhållsreleasen innehåller vanligtvis mer omfattande ändringar och utvecklare bör därför omedelbart uppdatera, återskapa och testa.

Nedan beskrivs den rekommenderade proceduren för uppdatering av en lokal miljö:

1. Se till att allt användbart innehåll antingen är implementerat i projektet i källkontrollen eller tillgängligt i ett ändringsbart innehållspaket för senare import.
1. Lokalt utvecklingstestinnehåll måste lagras separat så att det inte distribueras som en del av Cloud Manager pipeline-bygget. Orsaken är att den bara används för lokal utveckling.
1. Stoppa snabbstarten som körs.
1. Flytta mappen `crx-quickstart` till en annan mapp för säker lagring.
1. Observera den nya AEM som beskrivs i Cloud Manager (den används för att identifiera den nya QuickStart Jar-versionen som du kan ladda ned ytterligare).
1. Ladda ned QuickStart JAR vars version matchar Production AEM-versionen från Software Distribution Portal.
1. Skapa en helt ny mapp och placera den nya QuickStart Jar i.
1. Starta den nya snabbstarten med de önskade körningslägena (antingen ändra namn på filen eller skicka i körningsläge med `-r`).
   * Kontrollera att det inte finns någon kvar av den gamla snabbstarten i mappen.
1. Bygg AEM applikation.
1. Distribuera AEM till lokala AEM med hjälp av Package Manager.
1. Installera eventuella ändringsbara innehållspaket som behövs för lokal miljötestning via Package Manager.
1. Fortsätt med utvecklingen och distribuera ändringarna efter behov.

Om det finns innehåll som ska installeras med varje ny AEM snabbstartversion, inkluderar du det i ett innehållspaket och i projektets källkontroll. Installera det sedan varje gång.

Rekommendationen är att uppdatera SDK ofta (till exempel varannan vecka) och ta bort hela lokala tillstånd varje dag för att inte oavsiktligt vara beroende av tillståndskänsliga data i programmet.

Om du är beroende av CryptoSupport ([antingen genom att konfigurera autentiseringsuppgifterna för molntjänster eller SMTP Mail-tjänsten i AEM eller genom att använda CryptoSupport API i ditt program ](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), krypteras de krypterade egenskaperna av en nyckel. Den här nyckeln genereras automatiskt första gången en AEM startas. Molninstallationen hanterar automatiskt återanvändning av den miljöspecifika CryptoKey, men du måste injicera kryptonyckeln i den lokala utvecklingsmiljön.

Som standard är AEM konfigurerat att lagra nyckeldata i en mapps datamapp, men för att underlätta återanvändning under utvecklingen kan AEM initieras vid första starten med `-Dcom.adobe.granite.crypto.file.disable=true`. Den här processen genererar krypteringsdata på `/etc/key`.

Så här kan du återanvända innehållspaket som innehåller de krypterade värdena:

* När du startar den lokala quickstart.jar ska du lägga till följande parameter: `-Dcom.adobe.granite.crypto.file.disable=true`. Vi rekommenderar att du alltid lägger till det, men det är valfritt.
* Första gången du startar en instans skapar du ett paket som innehåller ett filter för roten `/etc/key`. Det här paketet innehåller hemligheten som ska återanvändas i alla miljöer som du vill att de ska återanvändas för.
* Exportera valfritt innehåll som innehåller hemligheter eller slå upp krypterade värden med hjälp av `/crx/de` så att du kan lägga till det i paketet som återanvänds i alla installationer.
* När du skapar en ny instans (antingen för att ersätta med en ny version eller för att flera utvecklingsmiljöer ska dela inloggningsuppgifterna för testning) installerar du paketet som skapats i steg 2 och 3. På så sätt kan du återanvända innehållet utan att behöva konfigurera om det manuellt. Orsaken är att nu är kryptonyckeln synkroniserad.
