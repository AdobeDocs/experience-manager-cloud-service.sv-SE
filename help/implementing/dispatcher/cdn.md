---
title: CDN i AEM as a Cloud Service
description: CDN i AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: dd32e9357bfbd8a9b23db1167cecc4e713cccd99
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 5%

---


# CDN i AEM as a Cloud Service {#cdn}

AEM som Cloud Service levereras med ett inbyggt CDN. Det huvudsakliga syftet är att minska fördröjningen genom att leverera tillgängligt innehåll från CDN-noderna i kanten, nära webbläsaren. Det är helt managerat och konfigurerat för optimal prestanda i AEM-program.

Det hanterade CDN-nätverket uppfyller de flesta kunders krav på prestanda och säkerhet. Kunderna kan också peka på det från sitt eget CDN, som de måste hantera. Detta kommer att tillåtas från fall till fall, baserat på att vissa krav uppfylls, inklusive, men inte begränsat till, den kund som har en äldre integrering med sin CDN-leverantör som är svår att överge.

## AEM Managed CDN  {#aem-managed-cdn}

Följ dessa för att förbereda materialet för leverans med hjälp av Adobes färdiga CDN:

1. Skicka det signerade SSL-certifikatet och den hemliga nyckeln till Adobe genom att dela en länk till ett säkert formulär som innehåller den här informationen. Samordna med kundsupport för den här uppgiften.
   **Obs!** Aem as a Cloud Service does not support Domain Validated (DV) certificates.
1. Informera kundsupport:
   * vilken anpassad domän som ska kopplas till en viss miljö, enligt definition av program-id och miljö-id. Observera att anpassade domäner på författarsidan inte stöds.
   * om någon IP-tilldelning behövs för att begränsa trafiken till en viss miljö.
1. Koordinera med kundsupport om timing för nödvändiga ändringar av DNS-posterna. Instruktionerna är olika beroende på om en apex-post behövs:
   * Om en apex-post inte behövs ska kunderna ange CNAME DNS-posten till att peka FQDN till `cdn.adobeaemcloud.com`.
   * Om en apex-post behövs skapar du en A-post som pekar på följande IP-adresser: 151.101.3.10, 151.101.67.10, 151.101.131.10, 151.101.195.10. Kunderna behöver en apex-post om det önskade FQDN matchar DNS-zonen. Detta kan testas med Unix-kommandot för att se om SOA-värdet för utdata matchar domänen. Kommandot `dig anything.dev.adobeaemcloud.com` returnerar till exempel SOA (Start of Authority, d.v.s. zonen) för `dev.adobeaemcloud.com` att inte vara en APEX-post, medan `dig dev.adobeaemcloud.com` returnerar SOA på `dev.adobeaemcloud.com` så sätt att det är en apex-post.
1. Du meddelas när SSL-certifikaten upphör att gälla så att du kan skicka om de nya SSL-certifikaten.

**Begränsa trafik**

Som standard kan all offentlig trafik för en Adobe-hanterad CDN-installation gå vidare till publiceringstjänsten, både för produktionsmiljöer och icke-produktionsmiljöer (utvecklingsmiljöer och scenmiljöer). Om du vill begränsa trafiken till publiceringstjänsten för en viss miljö (t.ex. begränsa mellanlagring med ett intervall av IP-adresser) bör du tillsammans med kundsupporten arbeta med att konfigurera dessa begränsningar.

## Kund-CDN pekar på AEM Managed CDN {#point-to-point-CDN}

Om en kund måste använda sitt befintliga CDN kan han eller hon hantera det och hänvisa det till Adobes hanterade CDN, förutsatt att följande uppfylls:

* Kunden måste ha ett befintligt CDN som är betungande att ersätta.
* Kunden måste hantera det.
* Kunden måste kunna konfigurera CDN så att den fungerar med AEM som Cloud Service - se konfigurationsinstruktionerna nedan.
* Kunden måste ha tekniska CDN-experter som är i drift om det uppstår problem.
* Kunden måste utföra och klara ett lasttest innan han/hon kan börja producera.

Konfigurationsinstruktioner:

1. Ange domännamnet som `X-Forwarded-Host` huvud.
1. Ange värdhuvudet med ursprungsdomänen, som är Adobes CDN:s ingress. Värdet ska komma från Adobe.
1. Skicka SNI-huvudet till origo. Precis som med värdhuvudet måste sni-huvudet vara den ursprungliga domänen.
1. Ange `X-Edge-Key`, vilket krävs för att dirigera trafik korrekt till AEM-servrarna. Värdet ska komma från Adobe.

Innan du godkänner direkttrafik bör du med Adobes kundsupport validera att hela trafikflödet fungerar korrekt.

Observera att prestandan kan bli liten på grund av det extra hopp som finns, även om hoppet från kundens CDN till Adobes hanterade CDN sannolikt är effektivt.
