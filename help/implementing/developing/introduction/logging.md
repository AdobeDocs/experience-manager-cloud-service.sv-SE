---
title: Loggning för AEM as a Cloud Service
description: Lär dig hur du använder loggning för AEM as a Cloud Service för att konfigurera globala parametrar för den centrala loggningstjänsten, specifika inställningar för de enskilda tjänsterna eller hur du begär dataloggning.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: bc92ed7acefbbd906b0986ea0b6b96fa6d8422de
workflow-type: tm+mt
source-wordcount: '2797'
ht-degree: 0%

---

# Loggning för AEM as a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service är en plattform där kunderna kan inkludera anpassad kod för att skapa unika upplevelser för sina kunder. Med detta i åtanke är loggningstjänsten en viktig funktion för att felsöka och förstå hur kod körs på lokal utveckling och i molnmiljöer, särskilt i AEM as a Cloud Service Dev-miljöer.

AEM as a Cloud Service loggningsinställningar och loggnivåer hanteras i konfigurationsfiler som lagras som en del av det AEM projektet i Git och distribueras som en del av det AEM projektet via Cloud Manager. Inloggning i AEM as a Cloud Service kan delas upp i två logiska uppsättningar:

* AEM loggning, som utför loggning på AEM programnivå
* Apache HTTPD Web Server/Dispatcher-loggning, som utför loggning av webbservern och Dispatcher på Publish-nivå.
* CDN-loggning, som enligt namnet, utför loggning på CDN. Den här funktionen lanseras gradvis för kunderna i början av september.

## AEM loggning {#aem-logging}

Loggning på AEM programnivå hanteras av tre loggar:

1. AEM Java-loggar, som återger Java-loggningsprogramsatser för det AEM programmet.
1. HTTP-begärandeloggar, som loggar information om HTTP-begäranden och deras svar som AEM
1. HTTP Access-loggar, som loggar sammanfattad information och HTTP-begäranden som hanteras av AEM

>[!NOTE]
>
>HTTP-begäranden som opereras från Dispatcher-cachen eller CDN för uppströms i Publish-nivån återspeglas inte i dessa loggar.

## AEM Java-loggning {#aem-java-logging}

AEM as a Cloud Service ger åtkomst till Java-loggsatser. Utvecklare av program för AEM bör följa allmänna bästa praxis för Java-loggning, logga relevanta satser om exekvering av anpassad kod på följande loggnivåer:

<table>
<tr>
<td>
<b>AEM miljö</b></td>
<td>
<b>Loggnivå</b></td>
<td>
<b>Beskrivning</b></td>
<td>
<b>Logginstruktionens tillgänglighet</b></td>
</tr>
<tr>
<td>
Utveckling</td>
<td>
FELSÖKNING</td>
<td>
Beskriver vad som händer i programmet.<br>
När DEBUG-loggning är aktiv, loggas programsatser som ger en tydlig bild av vilka aktiviteter som utförs och alla nyckelparametrar som påverkar bearbetningen.</td>
<td>
<ul>
<li> Lokal utveckling</li>
<li>Utveckling</li>
</ul></td>
</tr>
<tr>
<td>
Scen</td>
<td>
VARNING</td>
<td>
Beskriver villkor som kan bli fel.<br>
När WARN-loggning är aktiv loggas bara programsatser som anger att villkoren närmar sig suboptimaliteten.</td>
<td>
<ul>
<li> Lokal utveckling</li>
<li>Utveckling</li>
<li>Scen</li>
</ul></td>
</tr>
<tr>
<td>
Produktion</td>
<td>
FEL</td>
<td>
Beskriver villkor som indikerar ett fel och som måste åtgärdas.<br>
När FELloggning är aktiv loggas bara programsatser som anger fel. FELloggsatser indikerar ett allvarligt problem som bör lösas så snart som möjligt.</td>
<td>
<ul>
<li> Lokal utveckling</li>
<li>Utveckling</li>
<li>Scen</li>
<li>Produktion</li>
</ul></td>
</tr>
</table>

Java-loggning stöder flera andra nivåer av loggningsgranularitet, men AEM as a Cloud Service rekommenderar att du använder de tre nivåer som beskrivs ovan.

AEM loggnivåer ställs in per miljötyp via OSGi-konfiguration, som i sin tur är implementerade i Git och distribueras via Cloud Manager till AEM as a Cloud Service. På grund av detta är det bäst att hålla loggsatserna konsekventa och välkända för miljötyper för att säkerställa att loggarna som är tillgängliga via AEM eftersom Cloud Service är tillgänglig på optimal loggnivå utan att programmet behöver distribueras om med den uppdaterade loggnivåkonfigurationen.

**Exempel på loggutdata**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**Loggformat**

<table>
<tbody>
<tr>
<td>Datum och tid</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEM as a Cloud Service-nod</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>Loggnivå</td>
<td>FELSÖKNING</td>
</tr>
<tr>
<td>Tråd</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Java, klass</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>Loggmeddelande</td>
<td>Ingen angiven godkännare, standard är [ Creative Approvers user group ]</td>
</tr>
</tbody>
</table>

### Konfigurationsloggare {#configuration-loggers}

AEM Java-loggar definieras som OSGi-konfiguration och är därmed avsedda för specifika AEM as a Cloud Service-miljöer med hjälp av körlägesmappar.

Konfigurera java-loggning för anpassade Java-paket via OSGi-konfigurationer för Sling LogManager-fabriken. Det finns två konfigurationsegenskaper som stöds:

| OSGi Configuration-egenskap | Beskrivning |
|---|---|
| org.apache.sling.commons.log.names | Java-paketen som loggsatser ska samlas in för. |
| org.apache.sling.commons.log.level | Loggnivån som Java-paketen ska loggas på, som anges av org.apache.sling.Commons.log.names |

Om du ändrar andra konfigurationsegenskaper för LogManager OSGi kan det uppstå tillgänglighetsproblem i AEM as a Cloud Service.

Följande är exempel på de rekommenderade loggningskonfigurationerna (med platshållarens Java-paket `com.example`) för de tre miljötyperna i AEM as a Cloud Service.

### Utveckling {#development}

/apps/my-app/config/org.apache.sling.Commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### Scen {#stage}

/apps/my-app/config.stage/org.apache.sling.Commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### Produktion {#productiomn}

/apps/my-app/config.prod/org.apache.sling.Commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## Loggning av AEM HTTP-begäran {#aem-http-request-logging}

AEM as a Cloud Service loggning av HTTP-begäran ger insikt i HTTP-begäranden som gjorts till AEM och deras HTTP-svar i tidsordning. Loggen är användbar för att förstå HTTP-begäranden som gjorts till AEM och i vilken ordning de bearbetas och besvaras.

Nyckeln till att förstå den här loggen är att mappa HTTP-begärande- och svarspar med deras ID:n, som anges med det numeriska värdet inom hakparenteser. Förfrågningar och deras motsvarande svar har ofta andra HTTP-förfrågningar och svar som skickas mellan dem i loggen.

**Exempellogg**

```
29/Apr/2020:19:14:21 +0000 [137] > POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] > GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**Loggformat**

<table>
<tbody>
<tr>
<td>Datum och tid</td>
<td>29/Apr/2020:19:14:21 +0000</td>
</tr>
<tr>
<td>ID för fråge-/svarspar</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>HTTP-metod</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>Protokoll</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEM as a Cloud Service-nod</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Konfigurera loggen {#configuring-the-log}

Loggen för AEM HTTP-begäran kan inte konfigureras i AEM as a Cloud Service.

## Loggning av AEM HTTP-åtkomst {#aem-http-access-logging}

AEM när HTTP-åtkomstloggning för Cloud Service visar HTTP-begäranden i tidsordning. Varje loggpost representerar den HTTP-begäran som AEM åtkomst till.

Den här loggen är användbar för att snabbt förstå vilka HTTP-begäranden som görs till AEM, om de lyckas genom att titta på den tillhörande HTTP-svarsstatuskoden och hur lång tid det tog att slutföra HTTP-begäran. Den här loggen kan också vara användbar om du vill felsöka en viss användares aktivitet genom att filtrera loggposter efter användare.

**Exempel på loggutdata**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEM as a Cloud Service Node ID | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| Klientens IP-adress | - |
| Användare | myuser@adobe.com |
| Datum och tid | 30/Apr/2020:17:37:14 +0000 |
| HTTP-metod | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| Protokoll | HTTP/1.1 |
| HTTP-svarsstatus | 200 |
| Svarstextens storlek i byte | 1141 |
| Referent | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| Användaragent | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### Konfigurera HTTP-åtkomstloggen {#configuring-the-http-access-log}

HTTP-åtkomstloggen kan inte konfigureras i AEM as a Cloud Service.

## Apache Web Server och Dispatcher Logging {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service tillhandahåller tre loggar för Apache Web Servers- och Dispatcher-lagret på Publish:

* Åtkomstlogg för Apache HTTPD-webbserver
* Fellogg för Apache HTTPD-webbserver
* Dispatcher-logg

Loggarna är bara tillgängliga för Publish.

Den här uppsättningen loggar ger insikter i HTTP-begäranden till AEM as a Cloud Service Publish-nivån innan dessa begäranden når AEM. Detta är viktigt att förstå eftersom de flesta HTTP-begäranden till Publish-skiktservrar betjänas av innehåll som cachas av Apache HTTPD-webbservern och AEM Dispatcher, och som aldrig når själva AEM. Därför finns det inga loggsatser för dessa begäranden i AEM Java-, Request- eller Access-loggar.

### Åtkomstlogg för Apache HTTPD-webbserver {#apache-httpd-web-server-access-log}

Åtkomstloggen för Apache HTTP Web Server innehåller programsatser för varje HTTP-begäran som når Publish-skiktets webbserver/Dispatcher. Begäranden som hanteras från ett CDN-uppströms återspeglas inte i dessa loggar.

Mer information om felloggformatet finns i [den officiella dokumentationen för apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

**Exempel på loggutdata**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**Loggformat**

<table>
<tbody>
<tr>
<td>AEM som molntjänstnod-ID</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>Klientens IP-adress</td>
<td>-</td>
</tr>
<tr>
<td>Användare</td>
<td>-</td>
</tr>
<tr>
<td>Datum och tid</td>
<td>01/May/2020:00:09:46 +0000</td>
</tr>
<tr>
<td>HTTP-metod</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/example.html</td>
</tr>
<tr>
<td>Protokoll</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>HTTP-svarsstatus</td>
<td>200</td>
</tr>
<tr>
<td>Storlek</td>
<td>310</td>
</tr>
<tr>
<td>Referent</td>
<td>-</td>
</tr>
<tr>
<td>Användaragent</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, t.ex. Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Konfigurera åtkomstloggen för Apache HTTPD-webbservern {#configuring-the-apache-httpd-webs-server-access-log}

Loggen kan inte konfigureras i AEM as a Cloud Service.

## Fellogg för Apache HTTPD-webbserver {#apache-httpd-web-server-error-log}

Felloggen för Apache HTTP Web Server innehåller programsatser för varje fel i Publish-skiktets webbserver/Dispatcher.

Mer information om felloggformatet finns i [den officiella dokumentationen för apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

**Exempel på loggutdata**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**Loggformat**

<table>
<tbody>
<tr>
<td>Datum och tid</td>
<td>Fri juli 17 02:16:42.608913 2020</td>
</tr>
<tr>
<td>Händelsenivå</td>
<td>[mpm_worker:notice]</td>
</tr>
<tr>
<td>Process-ID</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Pod name</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Meddelande</td>
<td>AH00094: Kommandorad: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### Konfigurerar felloggen för Apache HTTPD-webbservern {#configuring-the-apache-httpd-web-server-error-log}

Loggnivåerna mod_rewrite definieras av variabeln REWRITE_LOG_LEVEL i filen `conf.d/variables/global.var`.

Den kan ställas in på error, warn, info, debug och trace1 - trace8, med standardvärdet warn. Om du vill felsöka RewriteRules rekommenderar vi att du höjer loggnivån till trace2. Vi rekommenderar att du felsöker omskrivningsregler med [Dispatcher SDK](../../dispatcher/validation-debug.md). Högsta loggnivå för AEM as a Cloud Service är `debug`. Därför är det för närvarande inte möjligt att felsöka omskrivningsregler i molnet.

Mer information finns i dokumentationen för modulen [mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging).

Om du vill ange loggnivån per miljö använder du lämplig villkorsgren i filen global.var enligt beskrivningen nedan:

```
Define REWRITE_LOG_LEVEL debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL error
  ...
</IfDefine>
```

## Dispatcher Log {#dispatcher-log}

**Exempel**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**Loggformat**

<table>
<tbody>
<tr>
<td>Datum och tid</td>
<td>[17/Jul/2020:23:48:16 +000]</td>
</tr>
<tr>
<td>Pod Name</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>Protokoll</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Dispatcher svarsstatuskod</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Varaktighet</td>
<td>1949ms</td>
</tr>
<tr>
<td>Farm</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>Cachestatus</td>
<td>[åtgärd saknas]</td>
</tr>
<tr>
<td>Värd</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Konfigurera Dispatcher fellogg {#configuring-the-dispatcher-error-log}

Loggnivåer för dispatcher definieras av variabeln DISP_LOG_LEVEL i filen `conf.d/variables/global.var`.

Den kan ställas in på error, warn, info, debug och trace1, med standardvärdet warn.

Dispatcher-loggning stöder flera andra nivåer av loggningsgranularitet, men AEM as a Cloud Service rekommenderar att du använder de nivåer som beskrivs nedan.

Om du vill ställa in loggnivån per miljö använder du lämplig villkorsgren i filen `global.var` enligt beskrivningen nedan:

```
Define DISP_LOG_LEVEL debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL error
  ...
</IfDefine>
```

>[!NOTE]
>
>I AEM as a Cloud Service-miljöer är felsökning den högsta nivån för vertikal intensitet. Spårningsloggsnivån stöds inte, så du bör undvika att ange den när du arbetar i molnmiljöer.

## CDN-logg {#cdn-log}

AEM as a Cloud Service ger åtkomst till CDN-loggar, som är användbara för fall som till exempel optimering av träffkvoten. Det går inte att anpassa CDN-loggformatet och det finns inget koncept för att ställa in det på olika lägen, till exempel info, warn eller error.

CDN-loggar vidarebefordras till Splunk för nya supportförfrågningar för vidarebefordran. Kunder som redan har aktiverat Splunk-vidarebefordran kan lägga till CDN-loggar i framtiden.

**Exempel**

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

**Loggformat**

CDN-loggarna skiljer sig från de andra loggarna på så sätt att de följer ett json-format.

| **Fältnamn** | **Beskrivning** |
|---|---|
| *tidsstämpel* | Den tidpunkt då begäran startades, efter TLS-avslutning |
| *ttfb* | Förkortning för *Tid till första byte*. Tidsintervallet mellan begäran startades fram till punkten innan svarstexten började direktuppspelas. |
| *cli_ip* | Klientens IP-adress. |
| *cli_country* | [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alpha-2-landskod med två bokstäver för klientlandet. |
| *rid* | Värdet på begärandehuvudet som används för att unikt identifiera begäran. |
| *req_ua* | Användaragenten som ansvarar för att göra en given HTTP-begäran. |
| *värd* | Den myndighet som begäran avser. |
| *url* | Den fullständiga sökvägen, inklusive frågeparametrar. |
| *metod* | HTTP-metod som skickas av klienten, till exempel &quot;GET&quot; eller &quot;POST&quot;. |
| *res_type* | Den innehållstyp som används för att ange resursens ursprungliga medietyp. |
| *cache* | Status för cachen. Möjliga värden är HIT, MISS eller PASS |
| *status* | HTTP-statuskoden som ett heltalsvärde. |
| *res_age* | Den tid (i sekunder) som ett svar har cachelagrats (i alla noder). |
| *pop* | Datacenter för CDN-cacheservern. |
| *regler* | Namnen på matchande [trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md) och WAF-flaggor, vilket även anger om matchningen resulterade i ett block. Tom om inga regler matchade. |


## Åtkomst till loggar {#how-to-access-logs}

### Molnmiljöer {#cloud-environments}

Du kan komma åt AEM as a Cloud Service-loggar för molntjänster antingen genom att hämta via Cloud Manager gränssnitt eller genom att svepa loggar på kommandoraden med kommandoradsgränssnittet i Adobe I/O. Mer information finns i [Cloud Manager loggningsdokumentation](/help/implementing/cloud-manager/manage-logs.md).

### Loggar för ytterligare Publish-regioner {#logs-for-additional-publish-regions}

Om ytterligare Publish-regioner är aktiverade för en viss miljö, kommer loggar för varje region att vara tillgängliga för hämtning från Cloud Manager, vilket nämns ovan.

AEM loggar och dispatcherloggar för de ytterligare Publish-regionerna anger regionen i de tre första bokstäverna efter miljö-id:t, vilket visas av **nld2** i exemplet nedan, som refererar till en ytterligare AEM publiceringsinstans som finns i Nederländerna:

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### Lokal SDK {#local-sdk}

AEM as a Cloud Service SDK innehåller loggfiler som kan användas för lokal utveckling.

AEM loggar finns i mappen `crx-quickstart/logs`, där följande loggar kan visas:

* AEM Java-logg: `error.log`
* AEM HTTP-begärandelogg: `request.log`
* AEM HTTP-åtkomstlogg: `access.log`

Lagerloggarna för Apache, inklusive dispatchern, finns i Docker-behållaren som innehåller Dispatcher. Mer information om hur du startar Dispatcher finns i [Dispatcher-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html).

Så här hämtar du loggarna:

1. På kommandoraden skriver du `docker ps` för att visa dina behållare
1. Om du vill logga in i behållaren skriver du `docker exec -it <container> /bin/sh`, där `<container>` är avsändarbehållar-ID:t från föregående steg
1. Navigera till cacheroten under `/mnt/var/www/html`
1. Loggarna är under `/etc/httpd/logs`
1. Loggarna i Inspect: de finns i mappen XYZ, där följande loggar kan visas:
   * Åtkomstlogg för Apache HTTPD-webbserver - `httpd_access.log`
   * Felloggar för Apache HTTPD-webbserver - `httpd_error.log`
   * Dispatcher-loggar - `dispatcher.log`

Loggar skrivs också ut direkt till terminalutdata. Oftast ska loggarna vara DEBUG, vilket kan uppnås genom att skicka felsökningsnivån som en parameter när Docker körs. Till exempel:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Felsöka produktion och scen {#debugging-production-and-stage}

I undantagsfall måste loggnivåerna ändras för att logga med en finare granularitet i scen- eller produktionsmiljöer.

Det här är möjligt men det kräver ändringar av loggnivåerna i konfigurationsfilerna i Git från Varna och Fel till felsökning och en distribution till AEM as a Cloud Service för att registrera konfigurationsändringarna i miljöerna.

Beroende på trafiken och mängden loggsatser som skrivits av Debug kan detta resultera i en negativ prestandapåverkan på miljön, och därför rekommenderas att ändringar i felsökningsnivåerna för Stage och Production är:

* Klar med omdöme och endast när det är absolut nödvändigt
* Återställs till rätt nivå och återdriftsätts så snart som möjligt

## Splunk-loggar {#splunk-logs}

Kunder som har Splunk-konton kan via kundsupportbiljetten begära att deras AEM Cloud Service-loggar vidarebefordras till lämpligt index. Loggningsinformationen motsvarar den som är tillgänglig genom Cloud Manager logghämtningar, men det kan vara praktiskt att använda de frågefunktioner som finns i Splunk-produkten.

Nätverksbandbredden som är kopplad till loggar som skickas till Splunk räknas som en del av kundens I/O-användning i nätverket.

CDN-loggar vidarebefordras till Splunk för nya supportförfrågningar. Kunder som redan har aktiverat Splunk forward kan lägga till CDN-loggar i framtiden.

### Aktivera vidarebefordran av segment {#enabling-splunk-forwarding}

I supportärendet ska man ange

* Splunk HEC-slutpunktsadress. Slutpunkten måste ha ett giltigt SSL-certifikat och vara allmänt tillgänglig.
* Splunk-index
* Splunk-porten
* Splunk HEC-token. Mer information finns på [den här sidan](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples).

Egenskaperna ovan bör anges för varje relevant kombination av program- och miljötyp. Om en kund till exempel vill ha utvecklings-, staging- och produktionsmiljöer bör de tillhandahålla tre uppsättningar information enligt nedan.

>[!NOTE]
>
>Skräppostvidarebefordran för sandlådeprogrammiljöer stöds inte.

>[!NOTE]
>
>Splunk-vidarebefordringsfunktionen är inte möjlig från en dedikerad IP-adress.

Du bör se till att den ursprungliga begäran innehåller all utvecklingsmiljö som ska aktiveras, utöver stage/prod-miljöerna. Splunk måste ha ett SSL-certifikat och vara offentlig.

Om nya utvecklingsmiljöer som skapas efter den ursprungliga begäran ska ha Splunk-vidarebefordran, men inte har det aktiverat, bör ytterligare en begäran göras.

Observera också att om utvecklingsmiljöer har begärts är det möjligt att Splunk-vidarebefordran är aktiverat i andra dev-miljöer som inte finns i begäran eller till och med i sandlådemiljöer, och att Splunk-vidarebefordran delas med ett Splunk-index. Kunder kan använda fältet `aem_env_id` för att skilja mellan dessa miljöer.

Här nedan hittar du ett exempel på en kundsupportförfrågan:

Program 123, Production Env

* Splunk HEC-slutpunktsadress: `splunk-hec-ext.acme.com`
* Segmentindex: acme_123prod (kunden kan välja vilken namnkonvention man vill ha)
* Segmentport: 443
* Splunk HEC-token: ABC123

Program 123, Stage Env

* Splunk HEC-slutpunktsadress: `splunk-hec-ext.acme.com`
* Segmentindex: acme_123stage
* Segmentport: 443
* Splunk HEC-token: ABC123

Program 123, Dev Envs

* Splunk HEC-slutpunktsadress: `splunk-hec-ext.acme.com`
* Segmentindex: acme_123dev
* Segmentport: 443
* Splunk HEC-token: ABC123

Det kan räcka för att samma Splunk-index ska användas för varje miljö. I så fall kan antingen fältet `aem_env_type` användas för att differentiera baserat på värdena dev, stage och prod. Om det finns flera utvecklingsmiljöer kan fältet `aem_env_id` också användas. Vissa organisationer kan välja ett separat index för produktionsmiljöns loggar om det associerade indexet begränsar åtkomsten till en reducerad uppsättning Splunk-användare.

Här är ett exempel på loggpost:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
file_path: /var/log/aem/error.log
host: 172.34.200.12 
level: INFO
msg: [FelixLogListener] com.adobe.granite.repository Service [5091, [org.apache.jackrabbit.oak.api.jmx.SessionMBean]] ServiceEvent REGISTERED
orig_time: 16.07.2020 08:35:32.346
pod_name: aemloggingall-aem-author-77797d55d4-74zvt
splunk_customer: true
```
