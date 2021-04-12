---
title: CDN i AEM as a Cloud Service
description: CDN i AEM as a Cloud Service
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
translation-type: tm+mt
source-git-commit: 3d0f58754aaff3a0c505f60a9c24b4712c2e4c30
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 7%

---

# CDN i AEM as a Cloud Service {#cdn}

AEM när Cloud Servicen levereras med ett inbyggt CDN. Dess huvudsakliga syfte är att minska latensen genom att leverera tillgängligt innehåll från CDN-noder nära webbläsaren. Det är helt managerat och konfigurerat för optimal prestanda i AEM-program.

Det AEM hanterade CDN uppfyller de flesta kunders krav på prestanda och säkerhet. För publiceringsnivån kan kunderna välja att peka på det från sina egna CDN, som de måste hantera. Detta kommer att tillåtas från fall till fall, baserat på att vissa krav uppfylls, inklusive, men inte begränsat till, den kund som har en äldre integrering med sin CDN-leverantör som är svår att överge.

## AEM hanterad CDN {#aem-managed-cdn}

Följ avsnitten nedan för att använda självbetjäningsgränssnittet för Cloud Manager för att förbereda innehållsleverans med hjälp av AEM färdiga CDN:

1. [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Begränsa trafik**

För en AEM hanterad CDN-installation kan all offentlig trafik som standard gå vidare till publiceringstjänsten, både för produktionsmiljöer och icke-produktionsmiljöer (utvecklingsmiljöer och scenmiljöer). Om du vill begränsa trafiken till publiceringstjänsten för en viss miljö (till exempel begränsa mellanlagring med ett intervall av IP-adresser) kan du göra detta på ett självbetjäningssätt via användargränssnittet i Cloud Manager.

Mer information finns i [Hantera IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

>[!CAUTION]
>
>Endast förfrågningar från tillåtna IP-adresser hanteras av AEM hanterade CDN. Om du pekar ditt eget CDN mot det AEM hanterade CDN måste du se till att IP-adresserna för ditt CDN ingår i tillåtelselista.

## Kund-CDN pekar på AEM hanterat CDN {#point-to-point-CDN}

Om en kund måste använda sitt befintliga CDN kan de hantera det och peka det mot det AEM hanterade CDN, förutsatt att följande uppfylls:

* Kunden måste ha ett befintligt CDN som är betungande att ersätta.
* Kunden måste hantera det.
* Kunden måste kunna konfigurera CDN så att det fungerar med AEM som Cloud Service - se konfigurationsinstruktionerna nedan.
* Kunden måste ha tekniska CDN-experter som är i drift om det uppstår problem.
* Kunden måste utföra och klara ett lasttest innan han/hon kan börja producera.

Konfigurationsinstruktioner:

1. Ange `X-Forwarded-Host`-huvudet med domännamnet. Till exempel: `X-Forwarded-Host:example.com`.
1. Ange värdhuvudet med ursprungsdomänen, som är AEM CDN:s ingress. Till exempel: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Skicka SNI-huvudet till origo. Precis som Värdhuvudet måste SNI-huvudet vara ursprungsdomänen.
1. Ange antingen `X-Edge-Key` eller `X-AEM-Edge-Key` (om ditt CDN strips `X-Edge-*`). Värdet ska komma från Adobe.
   * Detta behövs för att Adobe CDN ska kunna validera källan för förfrågningarna och skicka `X-Forwarded-*`-rubrikerna till AEM. Till exempel används `X-Forwarded-Host` av AEM för att fastställa värdhuvudet och `X-Forwarded-For` används för att fastställa klientens IP-adress. Det blir alltså den betrodda anroparen (dvs. kundhanterade CDN) som ansvarar för att `X-Forwarded-*`-huvudena är korrekta (se anteckningen nedan).
   * Åtkomst till Adobe CDN-ingången kan även blockeras om det inte finns någon `X-Edge-Key`. Informera Adobe om du behöver direktåtkomst till Adobe CDN:s ingress (som ska blockeras).

Innan du godkänner direkttrafik bör du validera med Adobe kundsupport att hela trafikflödet fungerar korrekt.

>[!NOTE]
>
>Kunder som hanterar sitt eget CDN bör säkerställa integriteten för de huvuden som skickas vidare till AEM CDN. Vi rekommenderar till exempel att kunderna tar bort alla `X-Forwarded-*`-huvuden och anger dem som kända och kontrollerade värden. `X-Forwarded-For` ska till exempel innehålla klientens IP-adress, medan `X-Forwarded-Host` ska innehålla platsens värd.

Prestandan kan bli liten på grund av det extra hoppet, även om hoppet från kundens CDN till det AEM hanterade CDN sannolikt är effektivt.

Observera att den här kundens CDN-konfiguration stöds för publiceringsnivån, men inte framför författarnivån.

## Geolocation-rubriker {#geo-headers}

Den AEM hanterade CDN lägger till rubriker i varje begäran med:

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

Denna information kan vara användbar vid användning, t.ex. omdirigering till en annan URL som baseras på begärans ursprung (land). Använd rubriken Variera för att cachelagra svar som är beroende av geoinformation. Omdirigeringar till en viss landningssida ska till exempel alltid innehålla `Vary: x-aem-client-country`. Om det behövs kan du använda `Cache-Control: private` för att förhindra cachelagring. Se även [Cachelagring](/help/implementing/dispatcher/caching.md#html-text).
