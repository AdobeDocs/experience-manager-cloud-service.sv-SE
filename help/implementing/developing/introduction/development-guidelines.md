---
title: Utvecklingsriktlinjer för AEM as a Cloud Service
description: Utvecklingsriktlinjer för AEM as a Cloud Service
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 477546f882197291403e59d8ba2e53dd4918a719
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 1%

---

# Utvecklingsriktlinjer för AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

Kod som körs AEM as a Cloud Service måste vara medveten om att den alltid körs i ett kluster. Det innebär att fler än en instans alltid körs. Koden måste vara flexibel, särskilt eftersom en instans kan stoppas när som helst.

Under uppdateringen av AEM as a Cloud Service kommer det att finnas instanser där gammal och ny kod körs parallellt. Därför får gammal kod inte bryta med innehåll som skapas av ny kod och ny kod måste kunna hantera gammalt innehåll.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Om det finns ett behov av att identifiera det primära klustret kan API:t för identifiering av Apache Sling användas för att identifiera det.

## Läge i minnet {#state-in-memory}

Tillståndet får inte sparas i minnet utan sparas i databasen. Annars kan det här läget gå förlorat om en instans stoppas.

## Läge i filsystemet {#state-on-the-filesystem}

Instansens filsystem bör inte användas på AEM as a Cloud Service. Disken är tillfällig och kommer att kasseras när instanser återvinns. Det är möjligt att använda filsystemet i begränsad omfattning för tillfällig lagring i samband med behandling av enstaka begäranden, men det bör inte missbrukas för stora filer. Detta beror på att det kan ha en negativ inverkan på resursanvändningskvoten och leda till diskbegränsningar.

Som ett exempel där filsystemsanvändningen inte stöds bör publiceringsskiktet se till att alla data som behöver vara beständiga skickas iväg till en extern tjänst för längre lagring.

## Observera {#observation}

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser, utförs lokalt och därför måste användas med försiktighet. Detta gäller både JCR-händelser och Sling-resurshändelser. När en ändring inträffar kan instansen tas ned och ersättas av en annan instans. Andra instanser i topologin som är aktiva vid den tidpunkten kan reagera på den händelsen. I det här fallet kommer detta dock inte att vara en lokal händelse och det kanske inte ens finns någon aktiv ledare i händelse av ett pågående ledarval när evenemanget utställs.

## Bakgrundsuppgifter och tidskrävande jobb {#background-tasks-and-long-running-jobs}

Kod som körs som en bakgrundsuppgift måste anta att instansen som den körs i när som helst kan tas ned. Därför måste koden vara flexibel och viktigast av allt återtagbar. Det innebär att om koden körs igen ska den inte börja om från början, utan i närheten av den plats där den slutade. Även om detta inte är ett nytt krav för den här typen av kod är det AEM as a Cloud Service mer sannolikt att en instans kommer att tas bort.

För att minimera problemet bör långvariga jobb om möjligt undvikas, och de bör kunna återställas till ett minimum. För att utföra sådana jobb använder du Sling Jobs, som har en garanti som är minst en gång och därför, om de avbryts, kommer att köras igen så snart som möjligt. Men de borde förmodligen inte börja från början igen. För schemaläggning av sådana jobb är det bäst att använda [Försäljningsjobb](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) schemaläggaren på samma sätt säkerställer körningen minst en gång.

Schemaläggaren för Sling Commons ska inte användas för schemaläggning eftersom körning inte kan garanteras. Det är bara mer sannolikt att det kommer att planeras.

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser (som JCR-händelser eller Sling-resurshändelser), utförs och därför måste användas med försiktighet. Detta gäller redan för AEM distributioner i det här läget.

## Utgående HTTP-anslutningar {#outgoing-http-connections}

Vi rekommenderar starkt att alla utgående HTTP-anslutningar anger rimliga anslutnings- och lästidsgränser. För kod som inte tillämpar dessa tidsgränser kommer AEM instanser som körs på AEM as a Cloud Service att tillämpa en global tidsgräns. Dessa timeoutvärden är 10 sekunder för anslutningsanrop och 60 sekunder för läsanrop för anslutningar som används av följande populära Java-bibliotek:

Adobe rekommenderar att de [Bibliotek för Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) för att skapa HTTP-anslutningar.

Alternativ som är kända för att fungera, men som kan kräva att du själv anger beroendet är:

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) och/eller [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (tillhandahålls av AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (rekommenderas inte eftersom den är inaktuell och ersatt av version 4.x)
* [OK HTTP](https://square.github.io/okhttp/) (Tillhandahålls inte av AEM)

## Inga klassiska gränssnittsanpassningar {#no-classic-ui-customizations}

AEM as a Cloud Service stöder bara Touch-gränssnittet för kundkod från tredje part. Klassiskt användargränssnitt är inte tillgängligt för anpassning.

## Undvik inbyggda binärfiler {#avoid-native-binaries}

Koden kommer inte att kunna hämta binärfiler vid körning och inte heller ändra dem. Den kan t.ex. inte packa upp `jar` eller `tar` filer.

## Inga bindningar för direktuppspelning via AEM as a Cloud Service {#no-streaming-binaries}

Binärfiler bör nås via CDN, som kommer att betjäna binärfiler utanför de centrala AEM.

Använd till exempel inte `asset.getOriginal().getStream()`, som startar nedladdningen av en binärfil till AEM.

## Inga omvända replikeringsagenter {#no-reverse-replication-agents}

Omvänd replikering från Publicera till Författare stöds inte i AEM as a Cloud Service. Om en sådan strategi behövs kan du använda ett externt beständigt arkiv som delas mellan gruppen med publiceringsinstanser och eventuellt klustret Författare.

## Vidarebefordra replikeringsagenter kan behöva porteras {#forward-replication-agents}

Innehållet replikeras från författare till publicering via en pub-sub-mekanism. Anpassade replikeringsagenter stöds inte.

## Övervakning och felsökning {#monitoring-and-debugging}

### Loggar {#logs}

För lokal utveckling skrivs loggposterna till lokala filer i `/crx-quickstart/logs` mapp.

I molnmiljöer kan utvecklare hämta loggar via Cloud Manager eller använda ett kommandoradsverktyg för att avsluta loggarna. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Ange loggnivå**

Om du vill ändra loggnivåerna för molnmiljöer bör du ändra Sling Logging OSGI-konfigurationen, följt av en fullständig omdistribution. Eftersom detta inte sker omedelbart bör du vara försiktig med att aktivera utförliga loggar i produktionsmiljöer som tar emot mycket trafik. I framtiden kan det finnas mekanismer för att snabbare ändra loggnivån.

>[!NOTE]
>
>För att kunna utföra de konfigurationsändringar som anges nedan måste du skapa dem i en lokal utvecklingsmiljö och sedan överföra dem till en AEM as a Cloud Service instans. Mer information om hur du gör detta finns i [Distribuera till AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Aktivera felsökningsloggnivån**

Standardloggnivån är INFO, d.v.s. DEBUG-meddelanden loggas inte.
Om du vill aktivera DEBUG-loggnivån anger du

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

egenskap som ska felsökas. Lämna inte loggen på DEBUG-loggnivån längre än nödvändigt eftersom den genererar många loggar.
En rad i felsökningsfilen börjar oftast med DEBUG och anger sedan loggnivån, installationsåtgärden och loggmeddelandet. Till exempel:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Loggnivåerna är följande:

| 0 | Allvarligt fel | Åtgärden misslyckades och installationsprogrammet kan inte fortsätta. |
|---|---|---|
| 1 | Fel | Åtgärden misslyckades. Installationen fortsätter, men en del av CRX installerades inte korrekt och kommer inte att fungera. |
| 2 | Varning | Åtgärden har slutförts men problem uppstod. CRX fungerar eventuellt inte korrekt. |
| 3 | Information | Åtgärden har slutförts. |

### Trådbitar {#thread-dumps}

Tråddumpar i molnmiljöer samlas in kontinuerligt, men kan för närvarande inte hämtas på ett självbetjäningssätt. Under tiden kontaktar du AEM om tråddumpar behövs för att felsöka ett problem och ange exakt tidsfönster.

## CRX/DE Lite och Developer Console {#crxde-lite-and-developer-console}

### Lokal utveckling {#local-development}

För lokal utveckling har utvecklare full tillgång till CRXDE Lite (`/crx/de`) och AEM webbkonsol (`/system/console`).

Observera att vid lokal utveckling (med SDK) `/apps` och `/libs` kan skrivas direkt, vilket skiljer sig från molnmiljöer där mapparna på den översta nivån inte kan ändras.

### AEM as a Cloud Service utvecklingsverktyg {#aem-as-a-cloud-service-development-tools}

Kunderna har tillgång till CRXDE-klassen i utvecklingsmiljön, men inte i fas eller produktion. Den oföränderliga databasen (`/libs`, `/apps`) kan inte skrivas till vid körning, så om du försöker göra det uppstår fel.

En uppsättning verktyg för felsökning AEM as a Cloud Service utvecklingsmiljöer finns på Developer Console för dev-, stage- och produktionsmiljöer. URL:en kan bestämmas genom att ändra författarens eller publiceringstjänstens URL:er enligt följande:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Följande CLI-kommando för Cloud Manager kan användas som en genväg för att starta utvecklarkonsolen baserat på en miljöparameter som beskrivs nedan:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Se [den här sidan](/help/release-notes/home.md) för mer information.

Utvecklare kan generera statusinformation och lösa olika resurser.

Som framgår nedan omfattar tillgänglig statusinformation status för paket, komponenter, OSGI-konfigurationer, ekindex, OSGI-tjänster och Sling-jobb.

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Som framgår nedan kan utvecklare lösa paketberoenden och -servrar:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utvecklarkonsolen är också användbar vid felsökning och har en länk till verktyget Förklara fråga:

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

För produktionsprogram definieras åtkomst till Developer Console av&quot;Cloud Manager - Developer Role&quot; i Admin Console, medan Developer Console för sandlådeprogram är tillgänglig för alla användare med en produktprofil som ger dem tillgång till AEM as a Cloud Service. För alla program krävs&quot;Cloud Manager - Developer Role&quot; för statusdumpar och användare måste också definieras i produktprofilen AEM användare eller AEM administratörer på både författare och publiceringstjänster för att kunna visa statusdumpdata från båda tjänsterna. Mer information om hur du ställer in användarbehörigheter finns i [Dokumentation för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### AEM för mellanlagring och produktion {#aem-staging-and-production-service}

Kunderna har inte tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

### Prestandaövervakning {#performance-monitoring}

Adobe övervakar programmets prestanda och vidtar åtgärder för att hantera om en försämring observeras. För närvarande kan inte programmått beaktas.

## Skickar e-post {#sending-email}

Avsnitten nedan beskriver hur du begär, konfigurerar och skickar e-post.

>[!NOTE]
>
>E-posttjänsten kan konfigureras med OAuth2-stöd. Mer information finns i [OAuth2-stöd för e-posttjänsten](/help/security/oauth2-support-for-mail-service.md).

### Aktivera utgående e-post {#enabling-outbound-email}

Portar som används för att skicka e-post är som standard inaktiverade. Om du vill aktivera en port konfigurerar du [avancerat nätverk](/help/security/configuring-advanced-networking.md)och se till att för varje nödvändig miljö ställa in `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` slutpunktens regler för portvidarebefordran, som mappar den avsedda porten (t.ex. 465 eller 587) till en proxyport.

Vi rekommenderar att du konfigurerar avancerade nätverk med `kind` parametern inställd på `flexiblePortEgress` eftersom Adobe kan optimera prestandan för flexibel trafik i hamnutgångar. Om en unik IP-adress för utgångar krävs väljer du en `kind` parameter för `dedicatedEgressIp`. Om du redan har konfigurerat VPN av andra skäl kan du även använda den unika IP-adressen som den avancerade nätverksvarianten ger.

Du måste skicka e-post via en e-postserver i stället för direkt till e-postklienter. Annars kan e-postmeddelandena vara blockerade.

### Skicka e-post {#sending-emails}

The [Day CQ Mail Service OSGI Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) ska användas och e-post måste skickas till den e-postserver som anges i supportförfrågan i stället för direkt till mottagarna.

### Konfiguration {#email-configuration}

E-post i AEM ska skickas med [Day CQ Mail Service OSGi-tjänst](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Se [AEM 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) för mer information om hur du konfigurerar e-postinställningar. Observera följande nödvändiga justeringar för AEM as a Cloud Service `com.day.cq.mailer.DefaultMailService OSGI` tjänst:

* SMTP-serverns värdnamn ska anges till $[env:AEM_PROXY_HOST]
* SMTP-serverporten ska anges till värdet för den ursprungliga proxyporten som angetts i parametern portForwards som används i API-anropet när avancerade nätverk konfigureras. Exempel: 30465 (i stället för 465)

Vi rekommenderar även att om port 465 har begärts:

* set `smtp.port` till `465`
* set `smtp.ssl` till `true`

och om port 587 har begärts:

* set `smtp.port` till `587`
* set `smtp.ssl` till `false`

The `smtp.starttls` egenskapen ställs automatiskt in av AEM as a Cloud Service vid körning till ett lämpligt värde. Om `smtp.ssl` är inställt på true, `smtp.startls` ignoreras. If `smtp.ssl` är inställt på false, `smtp.starttls` är inställt på true. Detta är oberoende av `smtp.starttls` värden som anges i OSGI-konfigurationen.


E-posttjänsten kan även konfigureras med OAuth2-stöd. Mer information finns i [OAuth2-stöd för e-posttjänsten](/help/security/oauth2-support-for-mail-service.md).

### Äldre e-postkonfiguration {#legacy-email-configuration}

Före version 2021.9.0 konfigurerades e-postmeddelandet via en kundsupportförfrågan. Observera följande nödvändiga justeringar i `com.day.cq.mailer.DefaultMailService OSGI` tjänst:

AEM as a Cloud Service kräver att e-post skickas via port 465. Om en e-postserver inte stöder port 465 kan port 587 användas så länge som TLS-alternativet är aktiverat.

Om port 465 har begärts:

* set `smtp.port` till `465`
* set `smtp.ssl` till `true`

och om port 587 har begärts:

* set `smtp.port` till `587`
* set `smtp.ssl` till `false`

The `smtp.starttls` egenskapen ställs automatiskt in av AEM as a Cloud Service vid körning till ett lämpligt värde. Om `smtp.ssl` är inställt på true, `smtp.startls` ignoreras. If `smtp.ssl` är inställt på false, `smtp.starttls` är inställt på true. Detta är oberoende av `smtp.starttls` värden som anges i OSGI-konfigurationen.

SMTP-servervärden ska vara samma som e-postservern.


## [!DNL Assets] riktlinjer för utveckling och användningsfall {#use-cases-assets}

Mer information om användningsfall, rekommendationer och referensmaterial för Assets as a Cloud Service finns i [Utvecklarreferenser för Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
