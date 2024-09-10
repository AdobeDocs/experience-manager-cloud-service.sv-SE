---
title: AEM as a Cloud Service riktlinjer för utveckling
description: Lär dig riktlinjer för utveckling på AEM as a Cloud Service och viktiga sätt att skilja den från AEM på plats och AEM i AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ea631743af99879d2a76d3a4a78ecf5883f39c69
workflow-type: tm+mt
source-wordcount: '2770'
ht-degree: 0%

---

# AEM as a Cloud Service riktlinjer för utveckling {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="AEM as a Cloud Service riktlinjer för utveckling"
>abstract="Lär dig riktlinjer för utveckling på AEM as a Cloud Service och viktiga sätt att skilja den från AEM på plats och AEM i AMS."
>additional-url="https://video.tv.adobe.com/v/330555/" text="Demo av paketstruktur"

I det här dokumentet presenteras riktlinjer för utveckling på AEM as a Cloud Service och viktiga sätt som skiljer sig från AEM på plats och AEM i AMS.

## Koden måste vara klustermedveten {#cluster-aware}

Kod som körs i AEM as a Cloud Service måste vara medveten om att den alltid körs i ett kluster. Det innebär att fler än en instans alltid körs. Koden måste vara flexibel, särskilt eftersom en instans kan stoppas när som helst.

Under uppdateringen av AEM as a Cloud Service finns instanser där gammal och ny kod körs parallellt. Därför får gammal kod inte bryta med innehåll som skapas av ny kod och ny kod måste kunna hantera gammalt innehåll.

Om det finns ett behov av att identifiera det primära klustret kan API:t för identifiering av Apache Sling användas för att identifiera det.

## Läge i minnet {#state-in-memory}

Tillståndet får inte sparas i minnet utan sparas i databasen. Annars kan det här läget gå förlorat om en instans stoppas.

## Läge i filsystemet {#state-on-the-filesystem}

Använd inte instansens filsystem i AEM as a Cloud Service. Disken är tillfällig och kasseras när instanser återvinns. Det är möjligt att använda filsystemet i begränsad omfattning för tillfällig lagring i samband med behandling av enstaka begäranden, men det bör inte missbrukas för stora filer. Detta beror på att det kan ha en negativ inverkan på resursanvändningskvoten och leda till diskbegränsningar.

Som ett exempel där det inte finns stöd för filsystemsanvändning bör Publish-nivån se till att alla data som måste vara beständiga skickas iväg till en extern tjänst för längre lagringstid.

## Observera {#observation}

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser, utförs lokalt och därför måste användas med försiktighet. Detta gäller både JCR-händelser och Sling-resurshändelser. När en ändring inträffar kan instansen tas ned och ersättas av en annan instans. Andra instanser i topologin som är aktiva vid den tidpunkten kan reagera på den händelsen. I det här fallet kommer detta dock inte att vara en lokal händelse och det kanske inte ens finns någon aktiv ledare i händelse av ett pågående ledarval när evenemanget utställs.

## Bakgrundsuppgifter och tidskrävande jobb {#background-tasks-and-long-running-jobs}

Kod som körs som en bakgrundsuppgift måste anta att instansen som den körs i när som helst kan tas ned. Därför måste koden vara flexibel och viktigast av allt återtagbar. Det innebär att om koden körs igen ska den inte börja om från början, utan i närheten av den plats där den slutade. Även om detta inte är ett nytt krav för den här typen av kod är det troligare att en instans kommer att tas bort i AEM as a Cloud Service.

För att minimera problemet bör långvariga jobb om möjligt undvikas, och de bör kunna återställas till ett minimum. För att utföra sådana jobb använder du Sling Jobs, som har en garanti som är minst en gång och därför, om de avbryts, kommer att köras igen så snart som möjligt. Men de borde förmodligen inte börja från början igen. För schemaläggning av sådana jobb är det bäst att använda schemaläggaren [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) eftersom detta gör att körningen sker minst en gång.

Använd inte Sling Commons Scheduler för schemaläggning eftersom körning inte kan garanteras. Det är troligare att det är planerat.

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser (som JCR-händelser eller Sling-resurshändelser), utförs och därför måste användas med försiktighet. Detta gäller redan för AEM distributioner i det här läget.

## Utgående HTTP-anslutningar {#outgoing-http-connections}

Vi rekommenderar starkt att alla utgående HTTP-anslutningar anger rimliga anslutnings- och lästimeout. Föreslagna värden är 1 sekund för anslutningstimeout och 5 sekunder för lästimeout. De exakta numren måste bestämmas utifrån hur väl serverdelssystemet hanterar dessa begäranden.

För kod som inte tillämpar dessa tidsgränser kommer AEM som körs på AEM as a Cloud Service att tillämpa en global tidsgräns. Dessa timeoutvärden är 10 sekunder för anslutningsanrop och 60 sekunder för läsanrop för anslutningar.

Adobe rekommenderar att du använder det tillhandahållna [Apache HttpComponents Client 4.x-biblioteket](https://hc.apache.org/httpcomponents-client-ga/) för att skapa HTTP-anslutningar.

Alternativ som är kända för att fungera, men som kan kräva att du själv anger beroendet är:

* [java.net.UR](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) och/eller [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (tillhandahålls av AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (rekommenderas inte eftersom den är inaktuell och ersatt av version 4.x)
* [OK Http](https://square.github.io/okhttp/) (tillhandahålls inte av AEM)

Förutom att tillhandahålla timeout bör även en korrekt hantering av sådana tidsgränser och oväntade HTTP-statuskoder implementeras.

## Hantera hastighetsbegränsningar för begäranden {#rate-limit-handling}

När antalet inkommande begäranden som ska AEM överstiger felfria nivåer, svarar AEM på nya begäranden med HTTP-felkod 429. Program som anropar programmatiska AEM kan överväga att koda på ett defensivt sätt och försöka igen efter några sekunder med en exponentiell bakåtstrategi. Före mitten av augusti 2023 svarade AEM på samma villkor med HTTP-felkod 503.

## Inga klassiska gränssnittsanpassningar {#no-classic-ui-customizations}

AEM as a Cloud Service stöder bara Touch-gränssnittet för kundkod från tredje part. Klassiskt användargränssnitt är inte tillgängligt för anpassning.

## Inga inbyggda binärfiler eller inbyggda bibliotek {#avoid-native-binaries}

Inbyggda binära filer och bibliotek får inte distribueras till eller installeras i molnmiljöer.

Koden bör inte heller försöka hämta inbyggda binära filer eller inbyggda Java-tillägg (till exempel JNI) vid körning.

## Inga bindningar för direktuppspelning via AEM as a Cloud Service {#no-streaming-binaries}

Binärfiler bör nås via CDN, som kommer att betjäna binärfiler utanför de centrala AEM.

Använd t.ex. inte `asset.getOriginal().getStream()`, vilket utlöser hämtning av en binär fil till AEM.

## Inga omvända replikeringsagenter {#no-reverse-replication-agents}

Omvänd replikering från Publish till författare stöds inte i AEM as a Cloud Service. Om en sådan strategi behövs kan du använda ett externt beständigt arkiv som delas mellan servergruppen med Publish-instanser och potentiellt Author-klustret.

## Vidarebefordra replikeringsagenter kan behöva porteras {#forward-replication-agents}

Innehållet replikeras från författare till Publish via en pub-sub-mekanism. Anpassade replikeringsagenter stöds inte.

## Inga överbelastade utvecklingsmiljöer {#overloading-dev-envs}

Produktionsmiljöerna storleksanpassas högre för att säkerställa stabil drift, medan scenmiljöer storleksförändras som produktionsmiljöer för att säkerställa realistisk testning under produktionsförhållanden.

Utvecklingsmiljöer och Rapid Dev-miljöer bör begränsas till utveckling, felanalys och funktionstester, och är inte utformade för att bearbeta stora arbetsbelastningar eller stora mängder innehåll.

Om du till exempel ändrar en indexdefinition i en databas med stort innehåll i en Dev-miljö kan det leda till omindexering, vilket resulterar i för mycket bearbetning. Tester som kräver omfattande innehåll bör köras på scenmiljöer.

## Övervakning och felsökning {#monitoring-and-debugging}

### Loggar {#logs}

För lokal utveckling skrivs loggposter till lokala filer i mappen `/crx-quickstart/logs`.

I molnmiljöer kan utvecklare hämta loggar via Cloud Manager eller använda ett kommandoradsverktyg för att svepa loggarna. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Custom logs are not supported and so all logs should be output to the error log. -->

**Anger loggnivå**

Om du vill ändra loggnivåerna för molnmiljöer bör du ändra Sling Logging OSGI-konfigurationen, följt av en fullständig omdistribution. Eftersom detta inte är omedelbart, var försiktig med att aktivera utförliga loggar i produktionsmiljöer som tar emot mycket trafik. I framtiden kan det finnas mekanismer som gör att loggnivån kan ändras snabbare.

>[!NOTE]
>
>Om du vill utföra konfigurationsändringarna som anges nedan skapar du dem i en lokal utvecklingsmiljö och skickar dem sedan till en AEM as a Cloud Service-instans. Mer information om hur du gör detta finns i [Distribuera till AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Aktiverar debug-loggnivån**

Standardloggnivån är INFO, d.v.s. DEBUG-meddelanden loggas inte. Om du vill aktivera DEBUG-loggnivån uppdaterar du följande egenskap till felsökningsläge.

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

Ange till exempel `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` med följande värde.

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

Lämna inte loggen på DEBUG-loggnivån längre än nödvändigt eftersom detta genererar många poster.

Separata loggnivåer kan anges för olika AEM miljöer med hjälp av körlägesbaserad OSGi-konfigurationsinriktning om det är önskvärt att alltid logga på `DEBUG` under utvecklingen. Till exempel:

| Miljö | OSGi-konfigurationsplats via körningsläge | Egenskapsvärdet `org.apache.sling.commons.log.level` |
| - | - | - |
| Utveckling | /apps/example/config/org.apache.sling.Commons.log.LogManager.factory.config~example.cfg.json | FELSÖKNING |
| Scen | /apps/example/config.stage/org.apache.sling.Commons.log.LogManager.factory.config~example.cfg.json | VARNING |
| Produktion | /apps/example/config.prod/org.apache.sling.Commons.log.LogManager.factory.config~example.cfg.json | FEL |

En rad i felsökningsfilen börjar oftast med DEBUG och anger sedan loggnivån, installationsåtgärden och loggmeddelandet. Till exempel:

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Loggnivåerna är följande:

| 0 | Allvarligt fel | Åtgärden misslyckades och installationsprogrammet kan inte fortsätta. |
|---|---|---|
| 1 | Fel | Åtgärden misslyckades. Installationen fortsätter, men en del av CRX installerades inte korrekt och kommer inte att fungera. |
| 2 | Varning | Åtgärden har slutförts men problem uppstod. CRX kanske inte fungerar som det ska. |
| 3 | Information | Åtgärden har slutförts. |

### Trådbitar {#thread-dumps}

Tråddumpar i molnmiljöer samlas in kontinuerligt, men kan för närvarande inte hämtas på ett självbetjäningssätt. Under tiden kontaktar du AEM om det behövs tråddumpar för att felsöka ett problem och ange exakt tidsfönster.

## CRX/DE Lite och AEM as a Cloud Service Developer Console {#crxde-lite-and-developer-console}

### Lokal utveckling {#local-development}

För lokal utveckling har utvecklare fullständig åtkomst till CRXDE Lite (`/crx/de`) och AEM webbkonsol (`/system/console`).

På lokal utveckling (med SDK) kan `/apps` och `/libs` skrivas direkt, vilket skiljer sig från molnmiljöer där mapparna på den översta nivån inte kan ändras.

### AEM as a Cloud Service utvecklingsverktyg {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>AEM as a Cloud Service Developer Console får inte blandas ihop med liknande namn [*Adobe Developer Console*](https://developer.adobe.com/developer-console/).
>

>[!NOTE]
>Vissa kunder kan testa en omgjord upplevelse för AEM Cloud Service Developer Console. Mer information finns i [den här artikeln](/help/implementing/developing/introduction/developer-console.md).]

Kunderna har tillgång till CRXDE-klassen i utvecklingsmiljön, men inte i fas eller produktion. Det går inte att skriva till den oföränderliga databasen (`/libs`, `/apps`) vid körning, så om du försöker göra det kommer det att uppstå fel.

I stället kan databasläsaren startas från AEM as a Cloud Service Developer Console, vilket ger en skrivskyddad vy i databasen för alla miljöer på författarnivå, publicerings- och förhandsgranskningsnivå. Mer information finns i [Databasläsaren](/help/implementing/developing/tools/repository-browser.md).

En uppsättning verktyg för felsökning av AEM as a Cloud Service utvecklingsmiljöer finns i AEM as a Cloud Service Developer Console för RDE-, dev-, stage- och produktionsmiljöer. URL:en kan bestämmas genom att ändra författarens eller Publish tjänste-URL:er enligt följande:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Följande Cloud Manager CLI-kommando kan användas för att starta AEM as a Cloud Service Developer Console baserat på en miljöparameter som beskrivs nedan:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Mer information finns i [Versionsinformation](/help/release-notes/home.md).

Utvecklare kan generera statusinformation och lösa olika resurser.

Som framgår nedan omfattar tillgänglig statusinformation status för paket, komponenter, OSGI-konfigurationer, ekindex, OSGI-tjänster och Sling-jobb.

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Som framgår nedan kan utvecklare lösa paketberoenden och -servrar:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

AEM as a Cloud Service Developer Console är också användbart vid felsökning och har en länk till verktyget Förklara fråga:

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

För produktionsprogram definieras åtkomsten till AEM as a Cloud Service Developer Console av&quot;Cloud Manager - Developer Role&quot; i Adobe Admin Console, medan AEM as a Cloud Service Developer Console för sandlådeprogram är tillgängligt för alla användare med en produktprofil som ger dem tillgång till AEM as a Cloud Service. För alla program krävs&quot;Cloud Manager - utvecklarroll&quot; för statusdumpar och databaswebbläsaren och användare måste också definieras i produktprofilen AEM användare eller AEM administratörer för både författare och publiceringstjänster för att kunna visa data från båda tjänsterna. Mer information om hur du konfigurerar användarbehörigheter finns i [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Prestandaövervakning {#performance-monitoring}

Adobe övervakar programmets prestanda och vidtar åtgärder för att hantera om en försämring observeras. För närvarande kan inte tillämpningsmetrierna följas.

## Skickar e-post {#sending-email}

Avsnitten nedan beskriver hur du begär, konfigurerar och skickar e-post.

>[!NOTE]
>
>E-posttjänsten kan konfigureras med OAuth2-stöd. Mer information finns i [OAuth2-stöd för e-posttjänsten](/help/security/oauth2-support-for-mail-service.md).

### Aktivera utgående e-post {#enabling-outbound-email}

Portar som används för att skicka e-post är som standard inaktiverade. Om du vill aktivera en port konfigurerar du [avancerat nätverk](/help/security/configuring-advanced-networking.md) och ser till att du anger portvidarebefordringsreglerna för `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` för varje nödvändig miljö, som mappar den avsedda porten (till exempel 465 eller 587) till en proxyport.

Vi rekommenderar att du konfigurerar avancerat nätverk med en `kind`-parameter som är inställd på `flexiblePortEgress` eftersom Adobe kan optimera prestanda för flexibel portbelastningstrafik. Om en unik IP-adress för utgångar krävs väljer du parametern `kind` för `dedicatedEgressIp`. Om du redan har konfigurerat VPN av andra skäl kan du även använda den unika IP-adressen som den avancerade nätverksvarianten ger.

Du måste skicka e-post via en e-postserver i stället för direkt till e-postklienter. Annars kan e-postmeddelandena vara blockerade.

### Skicka e-post {#sending-emails}

[Day CQ Mail Service OSGI-tjänsten](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) ska användas och e-postmeddelanden måste skickas till den e-postserver som anges i supportförfrågan i stället för direkt till mottagarna.

### Konfiguration {#email-configuration}

E-post i AEM ska skickas med [Day CQ Mail Service OSGi-tjänsten](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Mer information om hur du konfigurerar e-postinställningar finns i [AEM 6.5-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html). Observera följande nödvändiga justeringar av tjänsten `com.day.cq.mailer.DefaultMailService OSGI` för AEM as a Cloud Service:

* SMTP-serverns värdnamn ska anges till $[env:AEM_PROXY_HOST;default=proxy.tunnel]
* SMTP-serverporten ska anges till värdet för den ursprungliga proxyporten som angetts i parametern portForwards som används i API-anropet när avancerade nätverk konfigureras. Exempel: 30465 (i stället för 465)

SMTP-serverporten ska anges som det `portDest`-värde som anges i parametern portForwards som används i API-anropet när avancerade nätverk konfigureras och `portOrig`-värdet ska vara ett meningsfullt värde som ligger inom det nödvändiga intervallet 30000-30999. Om till exempel SMTP-serverporten är 465 bör port 30465 användas som `portOrig`-värde.

I det här fallet, och om SSL måste aktiveras, i konfigurationen för **Day CQ Mail Service OSGI**:

* Ange `smtp.port` till `30465`
* Ange `smtp.ssl` till `true`

Om målporten är 587 bör `portOrig`-värdet 30587 användas. Om SSL ska vara inaktiverat, konfigureras tjänsten Dag CQ Mail Service OSGI:

* Ange `smtp.port` till `30587`
* Ange `smtp.ssl` till `false`

Egenskapen `smtp.starttls` anges automatiskt av AEM as a Cloud Service vid körning till ett lämpligt värde. Om `smtp.ssl` är true ignoreras `smtp.startls`. Om `smtp.ssl` är inställt på false är `smtp.starttls` inställt på true. Detta är oavsett `smtp.starttls`-värdena som angetts i OSGI-konfigurationen.


E-posttjänsten kan även konfigureras med OAuth2-stöd. Mer information finns i [OAuth2-stöd för e-posttjänsten](/help/security/oauth2-support-for-mail-service.md).

### Äldre e-postkonfiguration {#legacy-email-configuration}

Före version 2021.9.0 konfigurerades e-postmeddelandet via en kundsupportförfrågan. Observera följande nödvändiga justeringar av tjänsten `com.day.cq.mailer.DefaultMailService OSGI`:

AEM as a Cloud Service kräver att post skickas via port 465. Om en e-postserver inte stöder port 465 kan port 587 användas så länge som TLS-alternativet är aktiverat.

Om port 465 har begärts:

* ange `smtp.port` till `465`
* ange `smtp.ssl` till `true`

och om port 587 har begärts:

* ange `smtp.port` till `587`
* ange `smtp.ssl` till `false`

Egenskapen `smtp.starttls` anges automatiskt av AEM as a Cloud Service vid körning till ett lämpligt värde. Om `smtp.ssl` är true ignoreras `smtp.startls`. Om `smtp.ssl` är inställt på false är `smtp.starttls` inställt på true. Detta är oavsett `smtp.starttls`-värdena som angetts i OSGI-konfigurationen.

SMTP-servervärden ska vara samma som e-postservern.

## Undvik stora flervärdesegenskaper {#avoid-large-mvps}

Oak innehållsdatabas som ligger till grund för AEM as a Cloud Service är inte avsedd att användas med ett stort antal flervärdesegenskaper (MVP). En tumregel är att hålla de privata leverantörerna under 1000. Den faktiska prestandan beror dock på många faktorer.

Varningar loggas som standard efter att ha överstigit 1000. De liknar följande.

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

Stora MVP kan leda till fel på grund av att MongoDB-dokumentet överskrider 16 MB, vilket kan leda till fel som liknar följande.

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

Mer information finns i [dokumentationen för Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property).

## [!DNL Assets] utvecklingsriktlinjer och användningsexempel {#use-cases-assets}

Mer information om användningsfall, rekommendationer och referensmaterial för utveckling av Assets as a Cloud Service finns i [Utvecklarreferenser för Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
