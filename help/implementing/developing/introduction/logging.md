---
title: Loggning
description: Lär dig hur du konfigurerar globala parametrar för den centrala loggningstjänsten, specifika inställningar för enskilda tjänster eller hur du begär dataloggning.
translation-type: tm+mt
source-git-commit: 0b648e1a0da141f8393c62cb269e5498e2ecd23f
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 2%

---


# Loggning {#logging}

AEM som Cloud Service är en plattform där kunderna kan inkludera anpassad kod för att skapa unika upplevelser för sina kunder. Med detta i åtanke är loggning en viktig funktion för att felsöka och förstå kodkörning på lokal utveckling och i molnmiljöer, särskilt AEM som Cloud Servicens Dev-miljöer.

AEM loggnings- och loggnivåer hanteras i konfigurationsfiler som lagras som en del av det AEM projektet i Git och distribueras som en del av det AEM projektet via Cloud Manager. Inloggning AEM som en Cloud Service kan delas upp i två logiska uppsättningar:

* AEM loggning, som utför loggning på AEM programnivå
* Apache HTTPD Web Server/Dispatcher-loggning, som utför loggning av webbservern och Dispatcher på Publiceringsnivå.

## AEM loggning {#aem-loggin}

Loggning på AEM programnivå hanteras av tre loggar:

1. AEM Java-loggar, som återger Java-loggningsprogramsatser för det AEM programmet.
1. HTTP-begärandeloggar, som loggar information om HTTP-begäranden och deras svar som hanteras av AEM
1. HTTP Access-loggar, som loggar sammanfattad information och HTTP-begäranden som hanteras av AEM

>[!NOTE]
>
>HTTP-begäranden som hanteras från Dispatcher-cachen för publiceringsnivån eller CDN för det överordnade flödet återspeglas inte i dessa loggar.

## AEM Java-loggning {#aem-java-logging}

AEM som en Cloud Services ger åtkomst till Java-loggsatser. Utvecklare av program för AEM bör följa allmänna bästa praxis för Java-loggning, logga relevanta satser om exekvering av anpassad kod på följande loggnivåer:

<table>
<tr>
<td>
<b>AEM</b></td>
<td>
<b>Loggnivå</b></td>
<td>
<b>Beskrivning</b></td>
<td>
<b>Logguttryckstillgänglighet</b></td>
</tr>
<tr>
<td>
Utveckling</td>
<td>
FELSÖKNING</td>
<td>
Beskriver vad som händer i programmet.<br>
När DEBUG-loggning är aktiv loggas programsatser som ger en tydlig bild av vilka aktiviteter som utförs samt alla nyckelparametrar som påverkar bearbetningen.</td>
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

Java-loggning har stöd för flera andra nivåer av loggningsgranularitet, men AEM som en Cloud Service rekommenderar att du använder de tre nivåer som beskrivs ovan.

AEM loggnivåer ställs in per miljötyp via OSGi-konfiguration, som i sin tur är implementerade för Git, och distribueras via Cloud Manager för att AEM som en Cloud Service. På grund av detta är det bäst att hålla loggsatserna konsekventa och välkända för miljötyper, för att säkerställa att loggarna som är tillgängliga via AEM eftersom Cloud Service är tillgänglig på optimal loggnivå utan att programmet behöver distribueras om med den uppdaterade loggnivåkonfigurationen.

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
<td>AEM som Cloud Service-nod-ID</td>
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

AEM Java-loggar definieras som OSGi-konfiguration och anger därmed specifika AEM som en Cloud Service-miljö med körlägesmappar.

Konfigurera java-loggning för anpassade Java-paket via OSGi-konfigurationer för Sling LogManager-fabriken. Det finns två konfigurationsegenskaper som stöds:

| OSGi Configuration-egenskap | Beskrivning |
|---|---|
| org.apache.sling.commons.log.names | Java-paketen som loggsatser ska samlas in för. |
| org.apache.sling.commons.log.level | Loggnivån som Java-paketen ska loggas på, som anges av org.apache.sling.Commons.log.names |

Om du ändrar andra konfigurationsegenskaper för LogManager OSGi kan det leda till tillgänglighetsproblem i AEM som Cloud Service.

Följande är exempel på de rekommenderade loggningskonfigurationerna (med platshållarens Java-paket från `com.example`) för de tre AEM som en Cloud Service-miljötyp.

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

AEM som en Cloud Services loggning av HTTP-begäran ger insikt i HTTP-begäranden som gjorts till AEM och deras HTTP-svar i tidsordning. Loggen är användbar för att förstå HTTP-begäranden som gjorts till AEM och i vilken ordning de bearbetas och besvaras.

Nyckeln till att förstå den här loggen är att mappa HTTP-par för begäran och svar med deras ID:n, som anges med det numeriska värdet inom hakparenteser. Observera att ofta förfrågningar och deras motsvarande svar har andra HTTP-förfrågningar och svar som har intervjuats mellan dem i loggen.

**Exempellogg**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
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
<td>29/Apr/2020:19:14:21 +000</td>
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
<td>Webbadress</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>Protokoll</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEM som Cloud Service-nod-ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Konfigurera loggen {#configuring-the-log}

Loggen för AEM HTTP-begäran kan inte konfigureras i AEM som en Cloud Service.

## Loggning av AEM HTTP-åtkomst {#aem-http-access-logging}

AEM när HTTP-åtkomstloggning för Cloud Service visar HTTP-begäranden i tidsordning. Varje loggpost representerar den HTTP-begäran som AEM åtkomst till.

Loggen är användbar för att snabbt förstå vilka HTTP-begäranden som görs till AEM, om de lyckas genom att titta på den tillhörande HTTP-svarsstatuskoden och hur lång tid det tog att slutföra HTTP-begäran. Den här loggen kan också vara användbar om du vill felsöka en viss användares aktivitet genom att filtrera loggposter efter användare.

**Exempel på loggutdata**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

**Loggformat**

<table>
<tbody>
<tr>
<td>AEM som Cloud Service-nod-ID</td>
<td>cm-p1235-e2644-aem-author-59555cb5b8-8kgr2</td>
</tr>
<tr>
<td>Klientens IP-adress</td>
<td>-</td>
</tr>
<tr>
<td>Användare</td>
<td>myuser@adobe.com</td>
</tr>
<tr>
<td>Datum och tid</td>
<td>30/Apr/2020:17:37:14 +000</td>
</tr>
<tr>
<td>HTTP-metod</td>
<td>GET</td>
</tr>
<tr>
<td>Webbadress</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
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
<td>HTTP-begärandetid i millisekunder</td>
<td>1141</td>
</tr>
<tr>
<td>Referent</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>Användaragent</td>
<td>"Mozilla/5.0 (Macintosh); Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, t.ex. Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Konfigurera HTTP-åtkomstloggen {#configuring-the-http-access-log}

HTTP-åtkomstloggen kan inte konfigureras som en Cloud Service i AEM.

## Apache Web Server och Dispatcher Logging {#apache-web-server-and-dispatcher-logging}

AEM som en Cloud Service innehåller tre loggar för Apache-webbservrar och dispatcherskiktet i publiceringslagret:

* Åtkomstlogg för Apache HTTPD-webbserver
* Fellogg för Apache HTTPD-webbserver
* Sändningslogg

Observera att dessa loggar endast är tillgängliga för publiceringsnivån.

Den här uppsättningen loggar ger information om HTTP-begäranden till AEM som en Cloud Service-publiceringsnivå innan dessa begäranden når det AEM programmet. Detta är viktigt att förstå eftersom de flesta HTTP-begäranden till publiceringsskiktsservrar betjänas av innehåll som cachas av Apache HTTPD-webbservern och AEM Dispatcher, och som aldrig når själva AEM. Därför finns det inga loggsatser för dessa förfrågningar i AEM Java-, Request- eller Access-loggar.

### Åtkomstlogg för Apache HTTPD-webbserver {#apache-httpd-web-server-access-log}

Åtkomstloggen för Apache HTTP Web Server innehåller programsatser för varje HTTP-begäran som når publiceringsskiktets webbserver/Dispatcher. Observera att förfrågningar som hanteras från ett CDN i ett tidigare flöde inte återspeglas i dessa loggar.

Mer information om felloggformatet finns i den [officiella dokumentationen](https://httpd.apache.org/docs/2.4/logs.html#accesslog)för cacheminnet.

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
<td>01/May/2020:00:09:46 +000</td>
</tr>
<tr>
<td>HTTP-metod</td>
<td>GET</td>
</tr>
<tr>
<td>Webbadress</td>
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
<td>"Mozilla/5.0 (Macintosh); Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, t.ex. Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Konfigurera åtkomstloggen för Apache HTTPD-webbservern {#configuring-the-apache-httpd-webs-server-access-log}

Loggen kan inte konfigureras i AEM som en Cloud Service.

## Fellogg för Apache HTTPD-webbserver {#apache-httpd-web-server-error-log}

Felloggen för Apache HTTP Web Server innehåller programsatser för varje fel i Publish-skiktets webbserver/Dispatcher.

Mer information om felloggformatet finns i den [officiella dokumentationen](https://httpd.apache.org/docs/2.4/logs.html#errorlog)för cacheminnet.

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
<td>Fri Jul 17 02:16:42.608913 2020</td>
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

Den kan anges till Error, Warn, Info, Debug och Trace1 - Trace8, med standardvärdet Warn. Om du vill felsöka RewriteRules rekommenderar vi att du höjer loggnivån till Trace2.

Mer information finns i dokumentationen [för modulen](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) mod_rewrite.

Om du vill ange loggnivån per miljö använder du lämplig villkorsgren i filen global.var enligt beskrivningen nedan:

```
Define REWRITE_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL Error
  ...
</IfDefine>
```

## Dispatcher-logg {#dispatcher-log}

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
<td>Webbadress</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Statuskod för avsändarens svar</td>
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

### Konfigurera felloggen för Dispatcher {#configuring-the-dispatcher-error-log}

Loggnivåer för dispatcher definieras av variabeln DISP_LOG_LEVEL i filen `conf.d/variables/global.var`.

Den kan anges till Error, Warn, Info, Debug och Trace1 med standardvärdet Warn.

Även om Dispatcher-loggning har stöd för flera andra nivåer av loggningsgranularitet rekommenderar AEM som en Cloud Service att du använder de nivåer som beskrivs nedan.

Om du vill ange loggnivån per miljö använder du lämplig villkorsgren i `global.var` filen enligt beskrivningen nedan:

```
Define DISP_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL Error
  ...
</IfDefine>
```

## Åtkomst till loggar {#how-to-access-logs}

### Molnmiljöer {#cloud-environments}

Du kan komma åt AEM som en Cloud Service för molntjänster antingen genom att hämta via Cloud Manager-gränssnittet eller genom att svepa loggar på kommandoraden med hjälp av kommandoradsgränssnittet i Adobe. Mer information finns i loggningsdokumentationen [för](/help/implementing/cloud-manager/manage-logs.md)Cloud Manager.

### Lokal SDK {#local-sdk}

AEM som Cloud Service-SDK tillhandahåller loggfiler som stöder lokal utveckling.

AEM loggar finns i mappen `crx-quickstart/logs`där följande loggar kan visas:

* AEM Java-logg: `error.log`
* Logg för AEM HTTP-begäran: `request.log`
* AEM HTTP Access-logg: `access.log`

Lagerloggarna för Apache, inklusive dispatchern, finns i Docker-behållaren som innehåller Dispatcher. Mer information om hur du startar Dispatcher finns i [Dispatcher-dokumentationen](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) .

Så här hämtar du loggarna:

1. På kommandoraden skriver du `docker ps` en lista över dina behållare
1. Om du vill logga in i behållaren skriver du&quot;`docker exec -it <container> /bin/sh`&quot;, där `<container>` är avsändarens behållar-ID från föregående steg
1. Navigera till cacheroten under `/mnt/var/www/html`
1. Loggarna är under `/etc/httpd/logs`
1. Inspect loggarna: De kan nås under mappen XYZ, där följande loggar kan visas:
   * Åtkomstlogg för Apache HTTPD-webbserver - `httpd_access.log`
   * Felloggar för Apache HTTPD-webbserver - `httpd_error.log`
   * Utskicksloggar - `dispatcher.log`

Loggar skrivs också ut direkt till terminalutdata. Oftast ska loggarna vara DEBUG, vilket kan uppnås genom att skicka felsökningsnivån som en parameter när Docker körs. Till exempel:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Felsöka produktion och scen {#debugging-production-and-stage}

I undantagsfall måste loggnivåerna ändras för att logga med en finare granularitet i scen- eller produktionsmiljöer.

Detta är möjligt men kräver ändringar av loggnivåerna i konfigurationsfilerna i Git från Varna och Fel till felsökning, och en distribution AEM som Cloud Service för att registrera konfigurationsändringarna i miljöerna.

Beroende på trafiken och mängden loggsatser som skrivits av Debug kan detta resultera i en negativ prestandapåverkan på miljön, och därför rekommenderas att ändringar i felsökningsnivåerna för Stage och Production är:

* Klar med omdöme och endast när det är absolut nödvändigt
* Återställs till rätt nivå och återdriftsätts så snart som möjligt

## Splunk-loggar {#splunk-logs}

Kunder som har Splunk-konton kan via kundsupportbiljetten begära att deras AEM Cloud Service-loggar vidarebefordras till lämpligt index. Loggningsinformationen motsvarar vad som är tillgängligt via hämtningen av loggen i Cloud Manager, men det kan vara praktiskt för kunderna att utnyttja de frågefunktioner som finns i Splunk-produkten.

Nätverksbandbredden som är kopplad till loggar som skickas till Splunk räknas som en del av kundens I/O-användning i nätverket.

### Aktivera vidarebefordran av segment {#enabling-splunk-forwarding}

I supportärendet ska man ange

* Splunk HEC-slutpunktsadress
* Splunk-indexvärdet
* Splunk-porten
* Splunk HEC-token. Mer information finns [på den här sidan](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) .

Egenskaperna ovan bör anges för varje relevant kombination av program- och miljötyp.  Om en kund till exempel vill ha utvecklings-, staging- och produktionsmiljöer bör de tillhandahålla tre uppsättningar information enligt nedan.

>[!NOTE]
>
>Skräppostvidarebefordran för sandlådeprogrammiljöer stöds inte.

Här nedan hittar du ett exempel på en kundsupportförfrågan:

Program 123, Production Env

* Splunk HEC-slutpunktsadress: `splunk-hec-ext.acme.com`
* Segmentindex: acme_123prod (kunden kan välja vilken namnkonvention man vill)
* Splunk-port: 443
* Splunk HEC-token: ABC123

Program 123, Stage Env

* Splunk HEC-slutpunktsadress: `splunk-hec-ext.acme.com`
* Segmentindex: acme_123stage
* Splunk-port: 443
* Splunk HEC-token: ABC123

Program 123, Dev Envs

* Splunk HEC-slutpunktsadress: `splunk-hec-ext.acme.com`
* Segmentindex: acme_123dev
* Splunk-port: 443
* Splunk HEC-token: ABC123

Det kan räcka för att samma Splunk-index ska användas för varje miljö. I så fall kan antingen `aem_env_type` fältet användas för att differentiera baserat på värdena dev, stage och prod. Om det finns flera utvecklingsmiljöer kan även `aem_env_id` fältet användas. Vissa organisationer kan välja ett separat index för produktionsmiljöns loggar om det associerade indexet begränsar åtkomsten till en reducerad uppsättning Splunk-användare.

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
