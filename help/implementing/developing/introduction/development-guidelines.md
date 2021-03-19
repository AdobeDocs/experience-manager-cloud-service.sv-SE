---
title: Utvecklingsriktlinjer för AEM as a Cloud Service
description: Utvecklingsriktlinjer för AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: ce797518714a4919bcdb6187aeaaf35dd1cb76b4
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 1%

---


# Utvecklingsriktlinjer för AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

Kod som körs i AEM som Cloud Service måste vara medveten om att den alltid körs i ett kluster. Det innebär att fler än en instans alltid körs. Koden måste vara flexibel, särskilt eftersom en instans kan stoppas när som helst.

Under uppdateringen av AEM som Cloud Service kommer det att finnas instanser där gammal och ny kod körs parallellt. Därför får gammal kod inte bryta med innehåll som skapas av ny kod och ny kod måste kunna hantera gammalt innehåll.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Om det finns ett behov av att identifiera det primära klustret kan API:t för identifiering av Apache Sling användas för att identifiera det.

## Läge i minnet {#state-in-memory}

Tillståndet får inte sparas i minnet utan sparas i databasen. Annars kan det här läget gå förlorat om en instans stoppas.

## Läge i filsystemet {#state-on-the-filesystem}

Instansens filsystem ska inte användas i AEM som Cloud Service. Disken är tillfällig och kommer att kasseras när instanser återvinns. Det är möjligt att använda filsystemet i begränsad omfattning för tillfällig lagring i samband med behandling av enstaka begäranden, men det bör inte missbrukas för stora filer. Detta beror på att det kan ha en negativ inverkan på resursanvändningskvoten och leda till diskbegränsningar.

Som ett exempel där filsystemsanvändningen inte stöds bör publiceringsskiktet se till att alla data som behöver vara beständiga skickas iväg till en extern tjänst för längre lagring.

## Obs {#observation}

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser, utförs lokalt och därför måste användas med försiktighet. Detta gäller både JCR-händelser och Sling-resurshändelser. När en ändring inträffar kan instansen tas ned och ersättas av en annan instans. Andra instanser i topologin som är aktiva vid den tidpunkten kan reagera på den händelsen. I det här fallet kommer detta dock inte att vara en lokal händelse och det kanske inte ens finns någon aktiv ledare i händelse av ett pågående ledarval när evenemanget utställs.

## Bakgrundsuppgifter och tidskrävande jobb {#background-tasks-and-long-running-jobs}

Kod som körs som en bakgrundsuppgift måste anta att instansen som den körs i när som helst kan tas ned. Koden måste därför vara flexibel och de flesta importer kan återupptas. Det innebär att om koden körs igen ska den inte börja om från början, utan i närheten av den plats där den slutade. Även om detta inte är ett nytt krav för den här typen av kod är det mer sannolikt att en instans kommer att tas bort i AEM som en Cloud Service.

För att minimera problemet bör långvariga jobb om möjligt undvikas, och de bör kunna återställas till ett minimum. För att utföra sådana jobb använder du Sling Jobs, som har en garanti som är minst en gång och därför, om de avbryts, kommer att köras igen så snart som möjligt. Men de borde förmodligen inte börja från början igen. För schemaläggning av sådana jobb är det bäst att använda schemaläggaren [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) så här igen med minst en körning.

Schemaläggaren för Sling Commons ska inte användas för schemaläggning eftersom körning inte kan garanteras. Det är bara mer sannolikt att det kommer att planeras.

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser (som JCR-händelser eller Sling-resurshändelser), utförs och därför måste användas med försiktighet. Detta gäller redan för AEM distributioner i det här läget.

## Utgående HTTP-anslutningar {#outgoing-http-connections}

Vi rekommenderar starkt att alla utgående HTTP-anslutningar anger rimliga anslutnings- och lästidsgränser. För kod som inte tillämpar dessa tidsgränser AEM instanser som körs på AEM som en Cloud Service en global tidsgräns. Dessa timeoutvärden är 10 sekunder för anslutningsanrop och 60 sekunder för läsanrop för anslutningar som används av följande populära Java-bibliotek:

Adobe rekommenderar att du använder det angivna [Apache HttpComponents Client 4.x-biblioteket](https://hc.apache.org/httpcomponents-client-ga/) för att skapa HTTP-anslutningar.

Alternativ som är kända för att fungera, men som kan kräva att du själv anger beroendet är:

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLand/or  [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (tillhandahålls av AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)  (rekommenderas inte eftersom den är inaktuell och ersatt av version 4.x)
* [OK HTTP](https://square.github.io/okhttp/) (tillhandahålls inte av AEM)

## Inga klassiska gränssnittsanpassningar {#no-classic-ui-customizations}

AEM som Cloud Service stöder endast Touch-gränssnittet för kundkod från tredje part. Klassiskt användargränssnitt är inte tillgängligt för anpassning.

## Undvik inbyggda binärfiler {#avoid-native-binaries}

Koden kommer inte att kunna hämta binärfiler vid körning och inte heller ändra dem. Den kan till exempel inte packa upp `jar`- eller `tar`-filer.

## Det finns inga bindningar för direktuppspelning via AEM som en Cloud Service {#no-streaming-binaries}

Binärfiler bör nås via CDN, som kommer att betjäna binärfiler utanför de centrala AEM.

Använd t.ex. inte `asset.getOriginal().getStream()`, som utlöser hämtning av en binär fil till AEM.

## Inga omvända replikeringsagenter {#no-reverse-replication-agents}

Omvänd replikering från Publicera till Författare stöds inte i AEM som Cloud Service. Om en sådan strategi behövs kan du använda ett externt beständigt arkiv som delas mellan gruppen med publiceringsinstanser och eventuellt klustret Författare.

## Vidarebefordra replikeringsagenter kan behöva porteras {#forward-replication-agents}

Innehållet replikeras från författare till publicering via en pub-sub-mekanism. Anpassade replikeringsagenter stöds inte.

## Övervakning och felsökning {#monitoring-and-debugging}

### Loggar {#logs}

För lokal utveckling skrivs loggposter till lokala filer i mappen `/crx-quickstart/logs`.

I molnmiljöer kan utvecklare hämta loggar via Cloud Manager eller använda ett kommandoradsverktyg för att avsluta loggarna. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Ange loggnivå**

Om du vill ändra loggnivåerna för molnmiljöer bör du ändra Sling Logging OSGI-konfigurationen, följt av en fullständig omdistribution. Eftersom detta inte sker omedelbart bör du vara försiktig med att aktivera utförliga loggar i produktionsmiljöer som tar emot mycket trafik. I framtiden kan det finnas mekanismer för att snabbare ändra loggnivån.

>[!NOTE]
>
>För att kunna utföra de konfigurationsändringar som anges nedan måste du skapa dem i en lokal utvecklingsmiljö och sedan överföra dem till en AEM som en Cloud Service-instans. Mer information om hur du gör detta finns i [Distribuera till AEM som en Cloud Service](/help/implementing/deploying/overview.md).

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

För lokal utveckling har utvecklare fullständig åtkomst till CRXDE Lite (`/crx/de`) och AEM webbkonsol (`/system/console`).

Observera att vid lokal utveckling (med SDK) kan `/apps` och `/libs` skrivas direkt till , vilket skiljer sig från molnmiljöer där mapparna på den översta nivån inte kan ändras.

### AEM som ett utvecklingsverktyg för Cloud Service {#aem-as-a-cloud-service-development-tools}

Kunderna har tillgång till CRXDE-klassen i utvecklingsmiljön, men inte i fas eller produktion. Det går inte att skriva till den oföränderliga databasen (`/libs`, `/apps`) vid körning, så om du försöker göra det uppstår fel.

En uppsättning verktyg för felsökning AEM som utvecklingsmiljö finns i Developer Console för dev-, stage- och produktionsmiljöer. URL:en kan bestämmas genom att ändra författarens eller publiceringstjänstens URL:er enligt följande:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Följande CLI-kommando för Cloud Manager kan användas som en genväg för att starta utvecklarkonsolen baserat på en miljöparameter som beskrivs nedan:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Mer information finns på [den här sidan](/help/release-notes/home.md).

Utvecklare kan generera statusinformation och lösa olika resurser.

Som framgår nedan omfattar tillgänglig statusinformation status för paket, komponenter, OSGI-konfigurationer, ekindex, OSGI-tjänster och Sling-jobb.

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Som framgår nedan kan utvecklare lösa paketberoenden och -servrar:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utvecklarkonsolen är också användbar vid felsökning och har en länk till verktyget Förklara fråga:

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

I produktionsprogram definieras åtkomst till Developer Console av&quot;Cloud Manager - Developer Role&quot; i Admin Console, medan Developer Console för sandlådeprogram är tillgänglig för alla användare med en produktprofil som ger dem tillgång till AEM som Cloud Service. För alla program krävs&quot;Cloud Manager - Developer Role&quot; för statusdumpar och användare måste också definieras i produktprofilen AEM användare eller AEM administratörer på både författare och publiceringstjänster för att kunna visa statusdumpdata från båda tjänsterna. Mer information om hur du konfigurerar användarbehörigheter finns i [Cloud Manager-dokumentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).


### AEM för mellanlagring och produktion {#aem-staging-and-production-service}

Kunderna har inte tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

### Prestandaövervakning {#performance-monitoring}

Adobe övervakar programmets prestanda och vidtar åtgärder för att hantera om en försämring observeras. För närvarande kan inte programmått beaktas.

## IP-adress för dedikerad gruppress {#dedicated-egress-ip-address}

På begäran kommer AEM som Cloud Service att tillhandahålla en statisk, dedikerad IP-adress för HTTP (port 80) och HTTPS (port 443) utgående trafik som programmerats i Java-kod.

### Fördelar {#benefits}

Den här dedikerade IP-adressen kan förbättra säkerheten vid integrering med SaaS-leverantörer (som en CRM-leverantör) eller andra integreringar utanför AEM som en Cloud Service som erbjuder en tillåtelselista IP-adresser. Genom att lägga till den dedikerade IP-adressen till tillåtelselista säkerställer det att endast trafik från kundens AEM Cloud Service tillåts att flöda in i den externa tjänsten. Detta är utöver trafik från andra IP-adresser som tillåts.

Utan den dedikerade IP-adressfunktionen aktiverad flödar trafik från AEM som en Cloud Service genom en uppsättning IP-adresser som delas med andra kunder.

### Konfiguration {#configuration}

Om du vill aktivera en dedikerad IP-adress skickar du en begäran till kundsupporten som ska ange IP-adressinformationen. I begäran bör varje miljö anges, och ytterligare förfrågningar bör göras om nya miljöer behöver funktionen efter den ursprungliga begäran. Sandlådeprogrammiljöer stöds inte.

### Funktionsanvändning {#feature-usage}

Funktionen är kompatibel med Java-kod eller bibliotek som resulterar i utgående trafik, förutsatt att de använder Java-standardegenskaper för proxykonfigurationer. I praktiken bör detta omfatta de vanligaste biblioteken.

Nedan visas ett kodexempel:

```
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

Samma dedikerade IP-adress används för alla kundprogram i Adobe och för alla miljöer i respektive program. Det gäller både författare och publiceringstjänster.

Endast HTTP- och HTTPS-portar stöds. Detta inkluderar HTTP/1.1 och HTTP/2 när de är krypterade.

### Felsökningsöverväganden {#debugging-considerations}

Kontrollera loggarna i destinationstjänsten om de är tillgängliga för att validera att trafiken faktiskt är utgående från den förväntade dedikerade IP-adressen. Annars kan det vara praktiskt att ringa ut till en felsökningstjänst som [https://ifconfig.me/ip](https://ifconfig.me/ip), som returnerar den anropande IP-adressen.

## Skickar e-post {#sending-email}

AEM som en Cloud Service kräver att utgående e-post krypteras. Avsnitten nedan beskriver hur du begär, konfigurerar och skickar e-post.

### Begär åtkomst {#requesting-access}

Som standard är utgående e-post inaktiverad. Aktivera den genom att skicka en supportanmälan med:

1. Det fullständiga domännamnet för e-postservern (till exempel `smtp.sendgrid.net`)
1. Den port som ska användas. Den bör vara port 465 om den stöds av e-postservern, annars port 587. Observera att port 587 bara kan användas om e-postservern kräver och tillämpar TLS på den porten
1. Program-ID och miljö-ID för de miljöer de vill skicka ut
1. Oavsett om SMTP-åtkomst krävs för författare, publicering eller båda.

### Skickar e-postmeddelanden {#sending-emails}

Tjänsten [Day CQ Mail OSGI](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) ska användas och e-post måste skickas till den e-postserver som anges i supportförfrågan i stället för direkt till mottagarna.

AEM CS kräver att e-post skickas via port 465. Om en e-postserver inte stöder port 465 kan port 587 användas så länge som TLS-alternativet är aktiverat.

>[!NOTE]
>
>Observera att Adobe inte stöder SMTP-komprimering över en unik dedikerad IP-adress.

### Konfiguration {#email-configuration}

E-post i AEM ska skickas med tjänsten [Day CQ Mail Service OSGi](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Mer information om hur du konfigurerar e-postinställningar finns i [AEM 6.5-dokumentationen](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html). För AEM som Cloud Service måste följande justeringar göras för tjänsten `com.day.cq.mailer.DefaultMailService OSGI`:

Om port 465 har begärts:

* ange `smtp.port` till `465`
* ange `smtp.ssl` till `true`

Om port 587 har begärts (endast tillåtet om e-postservern inte stöder port 465):

* ange `smtp.port` till `587`
* ange `smtp.ssl` till `false`

Egenskapen `smtp.starttls` anges automatiskt av AEM som en Cloud Service vid körning till ett lämpligt värde. Om `smtp.tls` är true ignoreras `smtp.startls`. Om `smtp.ssl` är inställt på false är `smtp.starttls` inställt på true. Detta är oavsett `smtp.starttls`-värdena som angetts i OSGI-konfigurationen.
