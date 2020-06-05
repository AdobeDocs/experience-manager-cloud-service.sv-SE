---
title: CDN i AEM som molntjänst
description: CDN i AEM som molntjänst
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---


# CDN i AEM som molntjänst {#cdn}

AEM som molntjänst levereras med ett inbyggt CDN. Det huvudsakliga syftet är att minska fördröjningen genom att leverera tillgängligt innehåll från CDN-noderna i kanten, nära webbläsaren. Det är helt managerat och konfigurerat för optimal prestanda i AEM-program.

Totalt finns det två alternativ i AEM:

1. AEM Managed CDN - AEM&#39;s out-of-box CDN. Det är ett nära integrerat alternativ och kräver inga stora kundinvesteringar för att stödja CDN-integreringen med AEM.
1. Kundhanterad CDN pekar på AEM Managed CDN - kunden pekar på ett eget CDN till AEM:s CDN som är färdig. Kunden måste fortfarande hantera sitt eget CDN, men investeringen i integreringen med AEM är måttlig.

Det första alternativet bör uppfylla de flesta krav på kundprestanda och säkerhet. Dessutom kräver det minimal kundinsats.

Det andra alternativet kommer att tillåtas från fall till fall. Beslutet bygger på att man uppfyller vissa krav, bland annat, men inte begränsat till, den kund som har en äldre integrering med sin CDN-leverantör som är svår att överge.

Nedan finns en beslutsmatris som jämför de två alternativen. Mer detaljerad information finns i följande avsnitt.

| Information | AEM Managed CDN | Kundhanterad CDN pekar på AEM CDN |
|---|---|---|
| **Kundansträngning** | Inget, det är helt integrerat. Du behöver bara peka CNAME mot AEM Managed CDN. | Måttlig kundinvestering. Kunden måste hantera sitt eget CDN. |
| **Krav** | Inget | Befintligt CDN som är betungande att ersätta. Måste visa ett lyckat lastprov innan live. |
| **CDN-expertis** | Inget | Kräver minst en deltidskonstruktionsresurs med detaljerad CDN-kunskap som kan konfigurera kundens CDN. |
| **Dokumentskydd** | Hanteras av Adobe. | Hanteras av Adobe (och eventuellt av kunden i deras eget CDN). |
| **Prestanda** | Optimerat av Adobe. | Kommer att dra nytta av vissa AEM CDN-funktioner, men eventuellt en liten prestandaförsämring på grund av det extra hoppet. **Obs**: Hoppar från kundens CDN till Adobes CDN (snart klart). |
| **Cachelagring** | Stöder cachehuvuden som används vid dispatchern. | Stöder cachehuvuden som används vid dispatchern. |
| **Komprimeringsfunktioner för bilder och video** | Kan fungera med Adobe Dynamic Media. | Kan användas med Adobe Dynamic Media eller en CDN-lösning för bild/video som hanteras av kunden. |

## AEM Managed CDN  {#aem-managed-cdn}

Det är enkelt att förbereda sig för innehållsleverans med hjälp av Adobes färdiga CDN enligt beskrivningen nedan:

1. Du skickar det signerade SSL-certifikatet och den hemliga nyckeln till Adobe genom att dela en länk till ett säkert formulär som innehåller den här informationen. Samordna med kundsupport för den här uppgiften.
   **Obs!** Aem as a Cloud Service does not support Domain Validated (DV) certificates.
1. Informera kundsupporten:
   * vilken anpassad domän som ska kopplas till en viss miljö, enligt definition av program-id och miljö-id.
   * om vitlistning av IP-adresser behövs för att begränsa trafiken till en viss miljö.
1. Kundsupport koordinerar sedan med dig tidpunkten för en CNAME DNS-post och pekar på deras FQDN till `cdn.adobeaemcloud.com`.
1. Du meddelas när SSL-certifikaten upphör att gälla så att du kan skicka om de nya SSL-certifikaten.

**Begränsa trafik**

Som standard kan all offentlig trafik för en Adobe-hanterad CDN-installation gå vidare till publiceringstjänsten, både för produktionsmiljöer och icke-produktionsmiljöer (utvecklingsmiljöer och scenmiljöer). Om du vill begränsa trafiken till publiceringstjänsten för en viss miljö (t.ex. begränsa mellanlagring med ett intervall av IP-adresser) bör du tillsammans med kundsupporten arbeta med att konfigurera dessa begränsningar.

## Kund-CDN pekar på AEM Managed CDN {#point-to-point-CDN}

Stöds om du vill använda ditt befintliga CDN, men inte kan uppfylla kraven från ett kundhanterat CDN. I så fall hanterar du ditt eget CDN, men pekar på Adobes hanterade CDN.

Tänk på följande:

1. Du måste ha ett befintligt CDN.
1. Du måste hantera det.
1. Du måste kunna konfigurera CDN så att det fungerar med AEM som en molntjänst - se konfigurationsinstruktionerna nedan.
1. Du måste ha tekniska CDN-experter som är i bruk om det skulle uppstå problem.
1. Du måste utföra och godkänna ett lasttest innan du går till produktion.

Konfigurationsinstruktioner:

1. Ange domännamnet som `X-Forwarded-Host` huvud.
1. Ange värdhuvudet med ursprungsdomänen, som är Adobes CDN:s ingress. Värdet ska komma från Adobe.
1. Skicka SNI-huvudet till origo. Precis som med värdhuvudet måste sni-huvudet vara den ursprungliga domänen.
1. Ange `X-Edge-Key`, vilket krävs för att dirigera trafik korrekt till AEM-servrarna. Värdet ska komma från Adobe.

Innan du godkänner direkttrafik bör du med Adobes kundsupport validera att hela trafikflödet fungerar korrekt.
