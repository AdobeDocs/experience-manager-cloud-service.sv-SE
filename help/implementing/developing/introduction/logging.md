---
title: Loggning
description: Lär dig hur du konfigurerar globala parametrar för den centrala loggningstjänsten, specifika inställningar för enskilda tjänster eller hur du begär dataloggning.
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

---


# Loggning{#logging}

Med AEM som molntjänst kan du konfigurera:

* globala parametrar för den centrala loggningstjänsten
* begära dataloggning, en särskild loggningskonfiguration för begärandeinformation
* särskilda inställningar för de enskilda tjänsterna, t.ex. en enskild loggfil och ett format för loggmeddelandena

För lokal utveckling skrivs loggposterna till lokala filer i `/crx-quickstart/logs` mappen.

I molnmiljöer kan utvecklare hämta loggar via Cloud Manager eller använda ett kommandoradsverktyg för att avsluta loggarna.

>[!NOTE]
>
>Inloggning av AEM som molntjänst baseras på Sling-principer. Mer information finns i [Sling Logging](https://sling.apache.org/site/logging.html) .

## Global loggning {#global-logging}

[Loggningskonfiguration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) för Apache Sling används för att konfigurera rotloggaren. Detta definierar de globala inställningarna för inloggning med AEM som en molntjänst:

* loggningsnivån
* platsen för den centrala loggfilen
* antalet versioner som ska behållas
* versionsrotation; antingen maximal storlek eller ett tidsintervall
* det format som ska användas när loggmeddelanden skrivs

## Loggare och skribenter för enskilda tjänster {#loggers-and-writers-for-individual-services}

Förutom de globala loggningsinställningarna kan du med AEM som molntjänst konfigurera specifika inställningar för en enskild tjänst:

* den specifika loggningsnivån
* platsen för den enskilda loggfilen
* antalet versioner som ska behållas
* versionsrotation; antingen maxstorlek eller tidsintervall
* det format som ska användas när loggmeddelanden skrivs
* loggaren (OSGi-tjänsten som tillhandahåller loggmeddelanden)

På så sätt kan du kanalisera loggmeddelanden för en enskild tjänst till en separat fil. Detta kan vara särskilt användbart under utveckling eller testning. om du till exempel behöver en högre loggnivå för en viss tjänst.

AEM som en molntjänst använder följande för att skriva loggmeddelanden till filen:

1. En **OSGi-tjänst** (logger) skriver ett loggmeddelande.
1. En **loggningsloggare** tar det här meddelandet och formaterar det enligt din specifikation.
1. En **loggningsskrivare** skriver alla dessa meddelanden till den fysiska filen som du har definierat.

Dessa element är länkade med följande parametrar för de relevanta elementen:

* **Logger (loggningslogg)**

   Definiera de tjänster som genererar meddelandena.

* **Loggfil (loggningslogg)**

   Definiera den fysiska filen för lagring av loggmeddelanden.

   Detta används för att länka en loggningslogg till en loggningsförfattare. Värdet måste vara identiskt med samma parameter i loggningsskrivarens konfiguration för att anslutningen ska kunna upprättas.

* **Loggfil (loggningsskrivare)**

   Definiera den fysiska fil som loggmeddelandena ska skrivas till.

   Detta måste vara identiskt med samma parameter i loggningsskrivarkonfigurationen, annars görs ingen matchning. Om det inte finns någon matchning skapas ett implicit skrivprogram med standardkonfigurationen (daglig loggrotation).

### Standardloggare och -författare {#standard-loggers-and-writers}

Vissa loggare och skrivprogram ingår i en standard-AEM som en molninstallation.

Det första är ett specialfall eftersom det styr både `request.log` och `access.log` filer:

* Loggaren:

   * Dataloggning för anpassningsbara Apache Sling-begäranden

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Skriv meddelanden om att begära innehåll till `request.log`.

* Länkar till:

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Skriver meddelanden till antingen `request.log` eller `access.log`.

Dessa kan anpassas vid behov, men standardkonfigurationen passar de flesta installationer.

De andra paren följer standardkonfigurationen:

* Loggaren:

   * Konfiguration av loggningsloggare för Apache Sling

      (org.apache.sling.Commons.log.LogManager.factory.config)

   * Skriver `Information` meddelanden till `logs/error.log`.

* Länkar till skrivprogrammet:

   * Konfiguration av skrivprogram för Apache Sling Logging

      (org.apache.sling.Commons.log.LogManager.factory.writer)

* Loggaren:

   * Konfiguration av Apache Sling Logging Logger (org.apache.sling.Commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Skriver `Warning` meddelanden till `../logs/error.log` för tjänsten `org.apache.pdfbox`.

* Länkar inte till ett specifikt skrivprogram, så skapar och använder ett implicit skrivprogram med standardkonfiguration (daglig loggrotation).

## Ange loggnivå {#setting-the-log-level}

Om du vill ändra loggnivåerna för molnmiljöer bör du ändra Sling Logging OSGI-konfigurationen, följt av en fullständig omdistribution. Eftersom detta inte sker omedelbart bör du vara försiktig med att aktivera utförliga loggar i produktionsmiljöer som tar emot mycket trafik. I framtiden kan det finnas mekanismer för att snabbare ändra loggnivån.

>[!NOTE]
>
> För att kunna utföra de konfigurationsändringar som anges nedan måste du skapa dem i en lokal utvecklingsmiljö och sedan överföra dem till en AEM-instans som en molntjänst. Mer information om hur du gör detta finns i [Distribuera till AEM som en molntjänst](/help/implementing/deploying/overview.md).

### Aktivera felsökningsloggnivån {#activating-the-debug-log-level}

>[!WARNING]
>
> Om du aktiverar loggnivån DEBUG globalt genereras en stor mängd information som är svår att gå igenom. Vi rekommenderar att du bara aktiverar den för de tjänster som kräver felsökning. Mer information finns i [Loggare and Writers for Individual Services](logging.md#loggers-and-writers-for-individual-services).

Standardloggnivån är INFO, d.v.s. DEBUG-meddelanden loggas inte.
Om du vill aktivera DEBUG-loggnivån anger du

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

egenskap som ska felsökas. Lämna inte loggen på DEBUG-loggnivån längre än nödvändigt eftersom den genererar många loggar.
En rad i felsökningsfilen börjar oftast med DEBUG och anger sedan loggnivån, installationsåtgärden och loggmeddelandet. Exempel:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Loggnivåerna är följande:

| 0 | Allvarligt fel | Åtgärden misslyckades och installationsprogrammet kan inte fortsätta. |
|---|---|---|
| 1 | Fel | Åtgärden misslyckades. Installationen fortsätter, men en del av CRX installerades inte korrekt och kommer inte att fungera. |
| 2 | Varning | Åtgärden har slutförts men problem uppstod. CRX fungerar eventuellt inte korrekt. |
| 3 | Information | Åtgärden har slutförts. |

### Skapa egna loggare och författare {#creating-your-own-loggers-and-writers}

Du kan definiera ett eget par för loggare/skrivare:

1. Skapa en ny instans av loggningskonfigurationen [för](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based)Apache Sling-loggning för fabrikskonfiguration.

   1. Ange loggfilen.
   1. Ange loggaren.
   1. Konfigurera de andra parametrarna efter behov.

1. Skapa en ny instans av Factory Configuration [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

   1. Ange loggfilen - den måste matcha den som har angetts för loggaren.
   1. Konfigurera de andra parametrarna efter behov.

### Skapa en anpassad loggfil {#create-a-custom-log-file}

>[!NOTE]
>
>När du arbetar med Adobe Experience Manager finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster.

I vissa fall kanske du vill skapa en anpassad loggfil med en annan loggnivå. Du kan göra detta i databasen genom att:

1. Om den inte redan finns skapar du en ny konfigurationsmapp ( `sling:Folder`) för projektet `/apps/<*project-name*>/config`.
1. Under `/apps/<*project-name*>/config`skapar du en nod för den nya konfigurationen för loggningsloggning för Apache Sling:

   * Namn: `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (eftersom detta är en loggare)

      Där `<*identifier*>` ersätts av fri text som du (måste) anger för att identifiera förekomsten (du kan inte utelämna den här informationen).

      Exempel: `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * Typ: `sling:OsgiConfig`
   >[!NOTE]
   >
   >Även om det inte är ett tekniskt krav är det tillrådligt att göra `<*identifier*>` unikt.

1. Ange följande egenskaper för den här noden:

   * Namn: `org.apache.sling.commons.log.file`

      Typ: Sträng

      Värde: Ange loggfilen. till exempel `logs/myLogFile.log`

   * Namn: `org.apache.sling.commons.log.names`

      Typ: Sträng[] (String + Multi)

      Värde: Ange de OSGi-tjänster som loggningsmeddelanden ska användas för. till exempel alla följande:

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * Namn: `org.apache.sling.commons.log.level`

      Typ: Sträng

      Värde: Ange den loggnivå som krävs ( `debug`, `info`, `warn` eller `error`). till exempel `debug`

   * Konfigurera de andra parametrarna efter behov:

      * Namn: `org.apache.sling.commons.log.pattern`

         Typ: `String`

         Värde: Ange loggmeddelandets mönster efter behov. till exempel

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` stöder upp till sex argument.

   >{0} Tidsstämpeln av typen `java.util.Date`
   >
   >{1}{2} the log marker the name of the current thread{3} the name of the logger{4} the log level{5} the log message

   >Om logganropet innehåller en `Throwable` stackspårning läggs den till i meddelandet.

   >[!CAUTION]
   org.apache.sling.Commons.log.names måste ha ett värde.

   >[!NOTE]
   Loggskrivarsökvägarna är relativa till `crx-quickstart` platsen.
   Därför har en loggfil angetts som:
   `logs/thelog.log`

   >skriver till:
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   Och en loggfil har angetts som:
   `../logs/thelog.log`

   >skriver till en katalog:
   ` <*cq-installation-dir*>/logs/`
&quot;(dvs. bredvid ` `&lt;*cq-installation-dir*>/`crx-quickstart/`)

1. Det här steget är bara nödvändigt när ett nytt skrivprogram krävs (dvs. med en konfiguration som inte är densamma som standardskrivaren).

   >[!CAUTION]
   En ny loggningsskrivarkonfiguration krävs bara när den befintliga standardinställningen inte är lämplig.

   >Om inget explicit skrivprogram är konfigurerat genereras automatiskt ett implicit skrivprogram baserat på standardvärdet.

   Under `/apps/<*project-name*>/config`skapar du en nod för den nya `Apache Sling Logging Writer` konfigurationen:

   * Namn: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (eftersom detta är ett skrivprogram)

      Precis som med Logger `<*identifier*>` ersätts den av fri text som du (måste) anger för att identifiera instansen (du kan inte utelämna den här informationen). Exempel: `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * Typ: `sling:OsgiConfig`
   >[!NOTE]
   Även om det inte är ett tekniskt krav är det tillrådligt att göra `<*identifier*>` unikt.

   Ange följande egenskaper för den här noden:

   * Namn: `org.apache.sling.commons.log.file`

      Typ: `String`

      Värde: Ange loggfilen så att den överensstämmer med den fil som anges i loggboken.

      i det här exemplet, `../logs/myLogFile.log`.

   * Konfigurera de andra parametrarna efter behov:

      * Namn: `org.apache.sling.commons.log.file.number`

         Typ: `Long`

         Värde: Ange hur många loggfiler du vill behålla. till exempel `5`

      * Namn: `org.apache.sling.commons.log.file.size`

         Typ: `String`

         Värde: Ange vad som krävs för att kontrollera filens rotation efter storlek/datum. till exempel `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` styr rotationen av loggfilen genom att ange antingen:
   * maximal filstorlek
   * ett tids-/datumschema
   för att ange när en ny fil ska skapas (och den befintliga filen får ett nytt namn enligt namnmönstret).
   * En storleksgräns kan anges med ett tal. Om ingen storleksindikator anges används detta som antal byte, eller så kan du lägga till en av storleksindikatorerna - `KB`, `MB`eller `GB` (versaler ignoreras).
   * Ett tids-/datumschema kan anges som ett `java.util.SimpleDateFormat` mönster. Detta anger den tidsperiod efter vilken filen ska roteras. det suffix som läggs till i den roterade filen (för identifiering).
   Standardvärdet är &#39;.&#39;yyyy-MM-dd (för daglig loggrotation)
   Så vid midnatt den 20 januari 2010 (eller när det första loggmeddelandet efter detta blir exakt) kommer ../logs/error.log att byta namn till ../logs/error.log.2010-01-20. Loggning för den 21 januari kommer att skickas till (en ny och tom) ../logs/error.log tills den överförs vid nästa ändring av dagen.
       | `&#39;.&#39;yyyy-MM`|Rotation i början av varje månad|
    |—|—|
    | `&#39;.&#39;yyyy-ww`|Rotation på den första dagen i varje vecka (beroende på språkområde). |
       | `&#39;.&#39;yyyy-MM-dd`|Rotation vid midnatt varje dag. |
       | `&#39;.&#39;yyyy-MM-dd`|Rotation vid midnatt och middag varje dag. |
       | `&#39;.&#39;yyyy-MM-dd-HH`|Rotation överst i varje timme. |
       | `&#39;.&#39;yyyy-MM-dd-HH-mm`|Rotation i början av varje minut. |
     
     Obs! När du anger tid/datum:
       1. Du bör&quot;escape&quot;-text inom ett par enkla citattecken (&#39; &#39;);
   Detta     gör du för att undvika att vissa tecken tolkas som mönsterbokstäver.
       1. Använd bara tecken som är tillåtna för ett giltigt filnamn var som helst i alternativet.
   

1. Läs den nya loggfilen med det verktyg du valt.

   Loggfilen som skapas i det här exemplet blir `../crx-quickstart/logs/myLogFile.log`.

Felix Console innehåller även information om stöd för loggning på `../system/console/slinglog`. till exempel `https://localhost:4502/system/console/slinglog`.draw