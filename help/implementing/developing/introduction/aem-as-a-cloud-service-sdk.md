---
title: SDK för AEM as a Cloud Service
description: En översikt över AEM as a Cloud Service Software Development Kit
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 1%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

Den AEM as a Cloud Service SDK består av följande artefakter:

* **QuickStart JAR** - AEM som används för lokal utveckling
* **Java™ API Jar** - Java™ Jar/Maven Dependency som visar alla Java™-API:er som kan användas för att utveckla mot AEM as a Cloud Service. Tidigare kallad Uberjar
* **Javadoc Jar** - Javadocs för Java™ API Jar
* **Dispatcher Tools** - Den uppsättning verktyg som används för att utveckla mot Dispatcher lokalt. Separata felaktigheter för UNIX® och Windows

Vissa kunder som tidigare har distribuerats med AEM 6.5 eller tidigare använder artefakterna nedan. Om den lokala kompileringen inte fungerar med Quickstart-behållaren och du misstänker att den inte fungerar när gränssnitt tas bort från AEM distribuerade as a Cloud Service kontaktar du kundsupporten. De kan avgöra om du behöver åtkomst. Det kräver ändringar i backend-objektet.

* **6.5 Java™ API Jar har tagits bort** - en extra uppsättning gränssnitt som har tagits bort sedan AEM 6.5
* **6.5 Javadoc Jar har tagits bort** - Javadocs för den ytterligare uppsättningen gränssnitt

## Building for the SDK {#building-for-the-sdk}

AEM as a Cloud Service SDK används för att skapa och distribuera anpassad kod. Mer information finns i [AEM Project Archetype-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). På en hög nivå utförs följande steg:

* **Kompilera kod**. Som förväntat kompileras källkoden och de resulterande innehållspaketen genereras
* **Skapa artefakter**. Artefakter skapas under den här processen
* **Analysera paket**. Paketen analyseras med Maven analyzer-pluginen som söker efter problem i Maven-projektet, till exempel saknade beroenden
* **Distribuera artefakter**. Artefakter distribueras till den lokala servern.

Samma steg utförs av Cloud Manager när du distribuerar till molnmiljöer. När du utför byggen lokalt kan du utveckla och testa dem lokalt. Utvecklare kan effektivt upptäcka kod eller strukturella problem innan de bestämmer sig för källkontroll och utlöser driftsättningar i Cloud Manager, vilket kan ta längre tid.

## Åtkomst till AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Du kan kolla den AEM Admin Console **Om Adobe Experience Manager** om du vill ta reda på vilken version av AEM du använder i produktionen.
* Verktygen quickstart jar och Dispatcher kan laddas ned som en zip-fil från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Åtkomsten till SDK-listorna är begränsad till personer som har miljöer AEM Managed Services eller AEM as a Cloud Service.
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
>Versionsposten för SDK ska matcha versionen av AEM as a Cloud Service. Du kan se vilken version du använder genom att logga in på AEM. I skärmens övre högra hörn går du till frågetecknet och väljer **[!UICONTROL About Adobe Experience Manager]**.


## Uppdatera ett lokalt projekt med en ny SDK-version {#refreshing-a-local-project-with-a-new-skd-version}

När rekommenderas att det lokala projektet uppdateras med ett nytt SDK?

Adobe *rekommenderas* att uppdatera den efter en månadsvis underhållsrelease.

Det är *valfri* för att uppdatera den efter en daglig underhållsrelease. Kunderna informeras om när deras produktionsinstans har uppgraderats till en ny AEM. För de dagliga underhållsreleaserna förväntas inte att det nya SDK:t har ändrats avsevärt, om alls. Vi rekommenderar dock att du ibland uppdaterar den lokala AEM utvecklingsmiljön med den senaste SDK:n och sedan återskapar och testar det anpassade programmet. Den månatliga underhållsreleasen innehåller vanligtvis mer omfattande ändringar och utvecklare bör därför omedelbart uppdatera, återskapa och testa.

Nedan beskrivs den rekommenderade proceduren för uppdatering av en lokal miljö:

1. Se till att allt användbart innehåll antingen är implementerat i projektet i källkontrollen eller tillgängligt i ett ändringsbart innehållspaket för senare import.
1. Lokalt utvecklingstestinnehåll måste lagras separat så att det inte distribueras som en del av molnhanterarens pipeline-bygge. Orsaken är att den bara används för lokal utveckling.
1. Stoppa snabbstarten som körs.
1. Flytta `crx-quickstart` till en annan mapp för säker förvaring.
1. Observera den nya AEM-versionen som beskrivs i Cloud Manager (den används för att identifiera den nya QuickStart Jar-versionen som du kan ladda ned ytterligare).
1. Ladda ned QuickStart JAR vars version matchar Production AEM-versionen från Software Distribution Portal.
1. Skapa en helt ny mapp och placera den nya QuickStart Jar i.
1. Starta nya QuickStart med önskat körningsläge (antingen ändra namn på filen eller skicka i körningsläge via `-r`).
   * Kontrollera att det inte finns någon kvar av den gamla snabbstarten i mappen.
1. Bygg AEM applikation.
1. Distribuera AEM till lokala AEM med hjälp av Package Manager.
1. Installera eventuella ändringsbara innehållspaket som behövs för lokal miljötestning via Package Manager.
1. Fortsätt med utvecklingen och distribuera ändringarna efter behov.

Om det finns innehåll som ska installeras med varje ny AEM snabbstartversion, inkluderar du det i ett innehållspaket och i projektets källkontroll. Installera det sedan varje gång.

Rekommendationen är att uppdatera SDK ofta (t.ex. varannan vecka) och ta bort hela lokala tillstånd varje dag för att inte vara beroende av tillståndskänsliga data i programmet.

Om du är beroende av CryptoSupport ([antingen genom att konfigurera autentiseringsuppgifterna för molntjänsterna eller SMTP Mail-tjänsten i AEM eller genom att använda CryptoSupport API i ditt program](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)) krypteras de krypterade egenskaperna av en nyckel. Den här nyckeln genereras automatiskt första gången en AEM startas. Molninstallationen hanterar automatiskt återanvändning av den miljöspecifika CryptoKey, men du måste injicera kryptonyckeln i den lokala utvecklingsmiljön.

Som standard är AEM konfigurerat att lagra nyckeldata i en mapps datamapp, men för att underlätta återanvändning under utvecklingen kan AEM initieras vid första starten med &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Den här processen genererar krypteringsdata på &quot;`/etc/key`&quot;.

Så här kan du återanvända innehållspaket som innehåller de krypterade värdena:

* När du startar den lokala quickstart.jar ska du lägga till parametern nedan: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Vi rekommenderar att du alltid lägger till det, men det är valfritt.
* Första gången du startar en instans skapar du ett paket som innehåller ett filter för roten`/etc/key`&quot;. Det här paketet innehåller hemligheten som ska återanvändas i alla miljöer som du vill att de ska återanvändas för.
* Exportera muterbart innehåll som innehåller hemligheter eller slå upp krypterade värden med hjälp av `/crx/de` så att du kan lägga till det i paketet som återanvänds i alla installationer.
* När du skapar en ny instans (antingen för att ersätta med en ny version eller för att flera utvecklingsmiljöer ska dela inloggningsuppgifterna för testning) installerar du paketet som skapats i steg 2 och 3. På så sätt kan du återanvända innehållet utan att behöva konfigurera om det manuellt. Orsaken är att nu är kryptonyckeln synkroniserad.
