---
title: Loggning
description: Lär dig hur du konfigurerar globala parametrar för den centrala loggningstjänsten, specifika inställningar för enskilda tjänster eller hur du begär dataloggning.
translation-type: tm+mt
source-git-commit: 436b4d05c88ba227144052fdd63ea78cbf1f03ba
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

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

### AEM Java-loggning {#aem-java-logging}

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