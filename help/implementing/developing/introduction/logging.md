---
title: Loggning
description: Lär dig hur du konfigurerar globala parametrar för den centrala loggningstjänsten, specifika inställningar för enskilda tjänster eller hur du begär dataloggning.
translation-type: tm+mt
source-git-commit: bbcadf29dbac89191a3a1ad31ee6721f8f57ef95
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 2%

---


# Loggning {#logging}

AEM som Cloud Service är en plattform där kunderna kan inkludera anpassad kod för att skapa unika upplevelser för sina kunder. Med detta i åtanke är loggning en viktig funktion för att felsöka och förstå kodkörning på lokal utveckling och i molnmiljöer, särskilt AEM som Cloud Servicens Dev-miljöer.

AEM loggnings- och loggnivåer hanteras i konfigurationsfiler som lagras som en del av det AEM projektet i Git och distribueras som en del av det AEM projektet via Cloud Manager. Inloggning AEM som en Cloud Service kan delas upp i två logiska uppsättningar:

* AEM loggning, som utför loggning på AEM programnivå
* Apache HTTPD Web Server/Dispatcher-loggning, som utför loggning av webbservern och Dispatcher på publiceringsnivån.

## AEM loggning {#aem-loggin}

Loggning på AEM programnivå hanteras av tre loggar:

1. AEM Java-loggar, som återger Java-loggningsprogramsatser för det AEM programmet.
1. HTTP-begärandeloggar, som loggar information om HTTP-begäranden och deras svar som hanteras av AEM
1. HTTP Access-loggar, som loggar sammanfattad information och HTTP-begäranden som hanteras av AEM

Observera att HTTP-begäranden som opereras från publiceringsskiktets Dispatcher-cache eller CDN i det överordnade flödet inte återspeglas i dessa loggar.

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

### Loggformat {#log-format}

| Datum och tid | AEM som Cloud Service-ID | Loggnivå | Tråd | Java-klass | Loggmeddelande |
|---|---|---|---|---|---|
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | `No specified approver, defaulting to [ Creative Approvers user group ]` |

**Exempel på loggutdata**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

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

Nyckeln till att förstå den här loggen är att mappa HTTP-begärande- och svarspar med deras ID:n, som anges med det numeriska värdet inom hakparenteser. Observera att ofta förfrågningar och deras motsvarande svar har andra HTTP-förfrågningar och svar som har intervjuats mellan dem i loggen.

### Loggformat {#http-request-logging-format}

| Datum och tid | ID för fråge-/svarspar |  | HTTP-metod | Webbadress | Protokoll | AEM som Cloud Service-nod-ID |
|---|---|---|---|---|---|---|
| 29/Apr/2020:19:14:21 +000 | `[137]` | -> | POST | /conf/global/settings/dam/adminui-extension/metadataprofile/ | HTTP/1.1 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` |

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

### Konfigurera loggen {#configuring-the-log}

Loggen för AEM HTTP-begäran kan inte konfigureras i AEM som en Cloud Service.

## Loggning av AEM HTTP-åtkomst {#aem-http-access-logging}

AEM när HTTP-åtkomstloggning för Cloud Service visar HTTP-begäranden i tidsordning. Varje loggpost representerar den HTTP-begäran som AEM åtkomst till.

Loggen är användbar för att snabbt förstå vilka HTTP-begäranden som görs till AEM, om de lyckas genom att titta på den tillhörande HTTP-svarsstatuskoden och hur lång tid det tog att slutföra HTTP-begäran. Den här loggen kan också vara användbar om du vill felsöka en viss användares aktivitet genom att filtrera loggposter efter användare.

### Loggformat {#access-log-format}

<table>
<tbody>
<tr>
<td><b>AEM som Cloud Service-nod-ID</b></td>
<td><b>Klientens IP-adress</b></td>
<td><b>Användare</b></td>
<td><b>Datum och tid</b></td>
<td><b>Tom</b></td>
<td><b>HTTP-metod</b></td>
<td><b>Webbadress</b></td>
<td><b>Protokoll</b></td>
<td><b>Tom</b></td>
<td><b>HTTP-svarsstatus</b></td>
<td><b>HTTP-svarstid i millisekunder</b></td>
<td><b>Referent</b></td>
<td><b>Användaragent</b></td>
</tr>
<tr>
<td>cm-p1235-e2644-aem-author-59555cb5b8-8kgr2</td>
<td>-</td>
<td>myuser@adobe.com</td>
<td>30/Apr/2020:17:37:14 +000</td>
<td>"</td>
<td>GET</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
<td>HTTP/1.1</td>
<td>"</td>
<td>200</td>
<td>1141</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
<td>"Mozilla/5.0 (Macintosh); Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, t.ex. Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>


**Exempel**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

### Konfigurera HTTP-åtkomstloggen {#configuring-the-http-access-log}

HTTP-åtkomstloggen kan inte konfigureras som en Cloud Service i AEM.

## Apache Web Server/Dispatcher Logging {#dispatcher-logging}

AEM som en Cloud Service innehåller tre loggar för Apache-webbservrar och dispatcherskiktet i publiceringslagret:

* Åtkomstlogg för Apache HTTPD-webbserver
* Fellogg för Apache HTTPD-webbserver
* Dispatcher-logg

Observera att dessa loggar endast är tillgängliga för publiceringsnivån.

Den här uppsättningen loggar ger information om HTTP-begäranden till AEM som en Cloud Service-publiceringsnivå innan dessa begäranden når det AEM programmet. Detta är viktigt att förstå eftersom de flesta HTTP-begäranden till publiceringsskiktsservrar betjänas av cachelagrat innehåll från Apache HTTPD-webbservern och AEM Dispatcher, och aldrig når själva AEM-programmet, vilket innebär att det inte finns några loggsatser för dessa begäranden i AEM Java-, Request- eller Access-loggar.