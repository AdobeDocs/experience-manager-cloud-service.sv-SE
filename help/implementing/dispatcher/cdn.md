---
title: CDN i AEM as a Cloud Service
description: CDN i AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: b6ae5cab872a3cca4eb41259f6c242b1fbeb98bb
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 5%

---


# CDN i AEM as a Cloud Service {#cdn}

AEM när Cloud Servicen levereras med ett inbyggt CDN. Det huvudsakliga syftet är att minska fördröjningen genom att leverera tillgängligt innehåll från CDN-noderna i kanten, nära webbläsaren. Det är helt managerat och konfigurerat för optimal prestanda i AEM-program.

Det AEM hanterade CDN uppfyller de flesta kunders krav på prestanda och säkerhet. För publiceringsnivån kan kunderna välja att peka på det från sina egna CDN, som de måste hantera. Detta kommer att tillåtas från fall till fall, baserat på att vissa krav uppfylls, inklusive, men inte begränsat till, den kund som har en äldre integrering med sin CDN-leverantör som är svår att överge.

## AEM hanterad CDN {#aem-managed-cdn}

Följ nedanstående avsnitt för att använda självbetjäningsgränssnittet för Cloud Manager för att förbereda innehållsleverans med hjälp av Adobe:s färdiga CDN:

1. [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Begränsa trafik**

Som standard kan all offentlig trafik för en Adobe hanterad CDN-installation gå vidare till publiceringstjänsten, både för produktionsmiljöer och icke-produktionsmiljöer (utvecklingsmiljöer och scenmiljöer). Om du vill begränsa trafiken till publiceringstjänsten för en viss miljö (till exempel begränsa mellanlagring med ett intervall av IP-adresser) kan du göra detta på ett självbetjäningssätt via användargränssnittet i Cloud Manager.

Mer information finns i [Hantera IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

>[!CAUTION]
>
>Endast förfrågningar från tillåtna IP-adresser hanteras av AEM hanterade CDN. Om du pekar ditt eget CDN mot det AEM hanterade CDN måste du se till att IP-adresserna för ditt CDN ingår i tillåtelselista.

## Kund-CDN pekar på AEM hanterat CDN {#point-to-point-CDN}

Om en kund måste använda sitt befintliga CDN kan han eller hon hantera det och peka det mot Adobe CDN, förutsatt att följande uppfylls:

* Kunden måste ha ett befintligt CDN som är betungande att ersätta.
* Kunden måste hantera det.
* Kunden måste kunna konfigurera CDN så att det fungerar med AEM som Cloud Service - se konfigurationsinstruktionerna nedan.
* Kunden måste ha tekniska CDN-experter som är i drift om det uppstår problem.
* Kunden måste utföra och klara ett lasttest innan han/hon kan börja producera.

Konfigurationsinstruktioner:

1. Ange `X-Forwarded-Host`-huvudet med domännamnet.
1. Ange värdhuvudet med ursprungsdomänen, som är Adobe CDN:s ingress. Värdet ska komma från Adobe.
1. Skicka SNI-huvudet till origo. Precis som med värdhuvudet måste sni-huvudet vara den ursprungliga domänen.
1. Ange `X-Edge-Key` som behövs för att dirigera trafik korrekt till AEM servrar. Värdet ska komma från Adobe.

Innan du godkänner direkttrafik bör du med Adobe kundsupport validera att trafikdirigeringen från början till slut fungerar som den ska.

Prestandan kan bli liten på grund av det extra hoppet, även om hoppet från kundens CDN till Adobe hanterade CDN sannolikt är effektivt.

Observera att den här kundens CDN-konfiguration stöds för publiceringsnivån, men inte framför författarnivån.

## Geolocation-rubriker {#geo-headers}

Det CDN som hanteras av Adobe lägger till rubriker i varje begäran med:

* landskod: `x-aem-client-country`
* Kontinentalkod: `x-aem-client-continent`

Värdena för landskoderna är de Alpha-2-koder som beskrivs [här](https://en.wikipedia.org/wiki/ISO_3166-1).

Värdena för kontinentkoderna är:

* AF Africa
* AN Antarktis
* AS Asien
* EU Europa
* NA Nordamerika
* OC Oceanien
* Sydamerika

Denna information kan vara användbar vid användning, t.ex. omdirigering till en annan URL som baseras på begärans ursprung (land). I detta specifika fall bör omdirigeringen inte cachas eftersom den varierar. Om det behövs kan du använda `Cache-Control: private` för att förhindra cachelagring. Se även [Cachelagring](/help/implementing/dispatcher/caching.md#html-text).
