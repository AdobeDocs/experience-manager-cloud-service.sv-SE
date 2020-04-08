---
title: Utvecklingsriktlinjer för AEM as a Cloud Service
description: Fylls i
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

---


# Utvecklingsriktlinjer för AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

Kod som körs i AEM som molntjänst måste vara medveten om att den alltid körs i ett kluster. Det innebär att fler än en instans alltid körs. Koden måste vara flexibel, särskilt eftersom en instans kan stoppas när som helst.

Under uppdateringen av AEM som en molntjänst kommer det att finnas instanser där gammal och ny kod körs parallellt. Därför får gammal kod inte bryta med innehåll som skapas av ny kod och ny kod måste kunna hantera gammalt innehåll.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Om du behöver identifiera huvudpersonen i klustret kan API:t för Apache Sling Discovery användas för att identifiera det.

## Läge i minnet {#state-in-memory}

Tillståndet får inte sparas i minnet utan sparas i databasen. Annars kan det här läget gå förlorat om en instans stoppas.

## Läge i filsystemet {#state-on-the-filesystem}

Instansens filsystem bör inte användas i AEM som molntjänst. Disken är tillfällig och kommer att kasseras när instanser återvinns. Det är möjligt att använda filsystemet i begränsad omfattning för tillfällig lagring i samband med behandling av enstaka begäranden, men det bör inte missbrukas för stora filer. Detta beror på att det kan ha en negativ inverkan på resursanvändningskvoten och leda till diskbegränsningar.

Som ett exempel där filsystemsanvändningen inte stöds bör publiceringsskiktet se till att alla data som behöver vara beständiga skickas iväg till en extern tjänst för längre lagring.

## Observera {#observation}

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser, utförs lokalt och därför måste användas med försiktighet. Detta gäller både JCR-händelser och Sling-resurshändelser. När en ändring inträffar kan instansen tas ned och ersättas av en annan instans. Andra instanser i topologin som är aktiva vid den tidpunkten kan reagera på den händelsen. I det här fallet kommer detta dock inte att vara en lokal händelse och det kanske inte ens finns någon aktiv ledare i händelse av ett pågående ledarval när evenemanget utställs.

## Bakgrundsuppgifter och tidskrävande jobb {#background-tasks-and-long-running-jobs}

Kod som körs som en bakgrundsuppgift måste anta att instansen som den körs i när som helst kan tas ned. Koden måste därför vara flexibel och de flesta importer kan återupptas. Det innebär att om koden körs igen ska den inte börja om från början, utan i närheten av den plats där den slutade. Detta är inte ett nytt krav för den här typen av kod, men i AEM som en molntjänst är det mer sannolikt att en instans kommer att försvinna.

För att minimera problemet bör långvariga jobb om möjligt undvikas, och de bör kunna återställas till ett minimum. För att utföra sådana jobb använder du Sling Jobs, som har en garanti som är minst en gång och därför, om de avbryts, kommer att köras igen så snart som möjligt. Men de borde förmodligen inte börja från början igen. För schemaläggning av sådana jobb är det bäst att använda schemaläggaren för [delningsjobb](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) så här igen med minst en gång.

Schemaläggaren för Sling Commons ska inte användas för schemaläggning eftersom körning inte kan garanteras. Det är bara mer sannolikt att det kommer att planeras.

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser (som JCR-händelser eller Sling-resurshändelser), utförs och därför måste användas med försiktighet. Detta gäller redan för AEM-distributioner i nuläget.

## Utgående HTTP-anslutningar {#outgoing-http-connections}

Vi rekommenderar starkt att alla utgående HTTP-anslutningar anger rimliga anslutnings- och lästidsgränser. För kod som inte tillämpar dessa tidsgränser kommer AEM-instanser som körs på AEM som en molntjänst att tillämpa en global tidsgräns. Dessa timeoutvärden är 10 sekunder för anslutningsanrop och 60 sekunder för läsanrop för anslutningar som används av följande populära Java-bibliotek:

Adobe rekommenderar att du använder det medföljande biblioteket [](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x för att skapa HTTP-anslutningar.

Alternativ som är kända för att fungera, men som kan kräva att du själv anger beroendet är:

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) och/eller [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (tillhandahålls av AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (rekommenderas inte eftersom den är inaktuell och ersatt av version 4.x)
* [OK HTTP](https://square.github.io/okhttp/) (tillhandahålls inte av AEM)

## Inga klassiska gränssnittsanpassningar {#no-classic-ui-customizations}

AEM som en molntjänst har endast stöd för Touch UI för kundkod från tredje part. Klassiskt användargränssnitt är inte tillgängligt för anpassning.

## Undvik inbyggda binärfiler {#avoid-native-binaries}

Koden kommer inte att kunna hämta binärfiler vid körning och inte heller ändra dem. Den kan till exempel inte packa upp `jar` eller packa upp `tar` filer.

## Inga bindningar för direktuppspelning via AEM som molntjänst {#no-streaming-binaries}

Binärfiler bör nås via CDN, som kan användas för binärfiler utanför de centrala AEM-tjänsterna.

Använd till exempel inte `asset.getOriginal().getStream()`, vilket medför att en binärfil laddas ned till AEM-tjänstens tillfälliga disk.

## Inga omvända replikeringsagenter {#no-reverse-replication-agents}

Omvänd replikering från Publicera till Författare stöds inte i AEM som en molntjänst. Om en sådan strategi behövs kan du använda ett externt beständigt arkiv som delas mellan gruppen med publiceringsinstanser och eventuellt klustret Författare.

## Vidarebefordra replikeringsagenter kan behöva porteras {#forward-replication-agents}

Innehållet replikeras från författare till publicering via en pub-sub-mekanism. Anpassade replikeringsagenter stöds inte.

## Övervakning och felsökning {#monitoring-and-debugging}

### Loggar {#logs}

För lokal utveckling skrivs loggposterna till lokala filer i `/crx-quickstart/logs` mappen.

I molnmiljöer kan utvecklare hämta loggar via Cloud Manager eller använda ett kommandoradsverktyg för att avsluta loggarna. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Ange loggnivå**

Om du vill ändra loggnivåerna för molnmiljöer bör du ändra Sling Logging OSGI-konfigurationen, följt av en fullständig omdistribution. Eftersom detta inte sker omedelbart bör du vara försiktig med att aktivera utförliga loggar i produktionsmiljöer som tar emot mycket trafik. I framtiden kan det finnas mekanismer för att snabbare ändra loggnivån.

>[!NOTE]
>
>För att kunna utföra de konfigurationsändringar som anges nedan måste du skapa dem i en lokal utvecklingsmiljö och sedan överföra dem till en AEM-instans som en molntjänst. Mer information om hur du gör detta finns i [Distribuera till AEM som en molntjänst](/help/implementing/deploying/overview.md).

**Aktivera felsökningsloggnivån**

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

### Trådbitar {#thread-dumps}

Tråddumpar i molnmiljöer samlas in kontinuerligt, men kan för närvarande inte hämtas på ett självbetjäningssätt. Under tiden kontaktar du AEM-supporten om tråddumpar behövs för att felsöka ett problem och ange exakt tidsfönster.

## CRX/DE Lite och System Console {#crxde-lite-and-system-console}

### Lokal utveckling {#local-development}

För lokal utveckling har utvecklare full tillgång till CRXDE Lite (`/crx/de`) och AEM Web Console (`/system/console`).

Observera att vid lokal utveckling (med molnklar snabbstart) `/apps` och `/libs` kan skrivas direkt till, vilket skiljer sig från molnmiljöer där dessa mappar på den översta nivån inte kan ändras.

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

Kunderna har tillgång till CRXDE-stilen i utvecklingsmiljön, men inte i fas eller produktion. Det går inte att skriva till den oföränderliga databasen (`/libs`, `/apps`) vid körning, så om du försöker göra det kommer det att leda till fel.

En uppsättning verktyg för felsökning av AEM som utvecklingsmiljö i molnet finns på Developer Console för dev-, stage- och produktionsmiljöer. URL:en kan bestämmas genom att ändra författarens eller publiceringstjänstens URL:er enligt följande:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Följande CLI-kommando för Cloud Manager kan användas som en genväg för att starta utvecklarkonsolen baserat på en miljöparameter som beskrivs nedan:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Mer information finns [på den här sidan](/help/release-notes/home.md) .

Utvecklare kan generera statusinformation och lösa olika resurser.

Som framgår nedan omfattar tillgänglig statusinformation status för paket, komponenter, OSGI-konfigurationer, ekindex, OSGI-tjänster och Sling-jobb.

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Som framgår nedan kan utvecklare lösa paketberoenden och -servrar:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utvecklarkonsolen är också användbar vid felsökning och har en länk till verktyget Förklara fråga:

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

### AEM Staging and Production Service {#aem-staging-and-production-service}

Kunderna har inte tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

### Prestandaövervakning {#performance-monitoring}

Adobe övervakar programprestanda och vidtar åtgärder för att åtgärda eventuella försämringar. För närvarande kan inte programmått beaktas.