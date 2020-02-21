---
title: Resurser för nätverksaspekter
description: Diskutera nätverksaspekter när du utformar en AEM Resurser-distribution.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ccfb07b3aef2e357434993cdf87ea9962b3c3566

---


# Resurser - nätverksaspekter {#assets-network-considerations}

Att förstå ert nätverk är lika viktigt som att förstå Adobe Experience Manager-resurser (AEM). Nätverket kan påverka uppladdning, nedladdning och användarupplevelser. Genom att diagram över din nätverkstopologi kan du identifiera kodpunkter och underoptimerade områden i nätverket som du måste åtgärda för att förbättra nätverkets prestanda och användarupplevelsen.

Se till att du inkluderar följande i nätverksdiagrammet:

* Anslutning från klientenheten (till exempel dator, mobil och surfplatta) till nätverket
* Företagets topologi
* Länka till Internet från företagets nätverk och AEM-miljön
* AEM-miljöns topologi
* Definiera samtidiga konsumenter av AEM-nätverksgränssnittet
* Definierade arbetsflöden för AEM-instansen

## Anslutning från klientenheten till företagsnätverket {#connectivity-from-the-client-device-to-the-corporate-network}

Börja med att diagram över anslutningen mellan de enskilda klientenheterna och företagsnätverket. I det här skedet kan du identifiera delade resurser, t.ex. WiFi-anslutningar, där flera användare använder samma punkt eller Ethernet-växlar för att överföra och hämta resurser.

![chlimage_1-353](assets/chlimage_1-353.png)

Klientenheter ansluter till företagsnätverket på olika sätt, t.ex. via WiFi, Ethernet till en delad switch samt via VPN. Det är viktigt att kunna identifiera och förstå kontrollpunkter i det här nätverket för att kunna planera och ändra nätverket.

Överst till vänster i diagrammet visas tre enheter som delar en WiFi-åtkomstpunkt på 48 Mbit/s. Om alla enheter överförs samtidigt delas WiFi-nätverkets bandbredd mellan enheterna. Jämfört med systemet som helhet kan en användare stöta på en annan kontrollpunkt för de tre klienterna över den här delade kanalen.

Det är en utmaning att mäta den verkliga hastigheten för ett WiFi-nätverk eftersom en långsam enhet kan påverka andra klienter på åtkomstpunkten. Om du tänker använda WiFi för resursinteraktioner, ska du utföra ett hastighetstest från flera klienter samtidigt för att utvärdera genomströmningen.

Bilden längst ned till vänster visar två enheter som är anslutna till företagets nätverk via oberoende kanaler. Därför kan varje enhet ha en minimihastighet på 10 Mbit/s och 100 Mbit/s.

Den dator som visas till höger har en begränsad uppström till företagsnätverket via ett VPN med en hastighet på 1 Mbit/s. Användarupplevelsen för 1 Mbit/s-anslutningen skiljer sig avsevärt från användarupplevelsen via 1 Gbit/s-anslutningen. Beroende på storleken på de resurser som användarna interagerar med kan deras VPN-anslutning vara otillräcklig för uppgiften.

## Företagets topologi {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

Diagrammet visar högre hastigheter för överordnad länk inom företagsnätverket än vad som vanligtvis används. Dessa rör är delade resurser. Om den delade växeln förväntas hantera 50 klienter kan det vara en kontrollpunkt. I det inledande diagrammet delar bara två datorer den aktuella anslutningen.

## Länka till Internet från företagsnätverket och AEM-miljön {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

Det är viktigt att ta hänsyn till okända faktorer på Internet och VPC-anslutningen eftersom bandbredden över Internet kan försämras på grund av belastningstopp eller storskaliga leverantörsavbrott. I allmänhet är internetanslutningen tillförlitlig. Ibland kan det dock medföra att kontrollpunkter läggs till.

På uppkopplingen från ett företagsnätverk till Internet kan det finnas andra tjänster som använder bandbredden. Det är viktigt att förstå hur stor del av bandbredden som kan dedikeras eller prioriteras för AEM Assets. Om till exempel en 1 Gbit/s-länk redan har 80 % utnyttjandegrad kan du bara tilldela maximalt 20 % av bandbredden för AEM-resurser.

Företagets brandväggar och proxies kan också forma bandbredden på många olika sätt. Den här typen av enhet kan prioritera bandbredden med hjälp av tjänstekvalitet, bandbreddsbegränsningar per användare eller bithastighetsbegränsningar per värd. Det här är viktiga punkter att undersöka eftersom de kan påverka Assets-användarupplevelsen avsevärt.

I det här exemplet har företaget en upplänk på 10 Gbit/s. Den borde vara tillräckligt stor för flera kunder. Dessutom har brandväggen en värdhastighetsgräns på 10 Mbit/s. Denna begränsning kan potentiellt begränsa trafiken till en enda värd till 10 Mbit/s, även om uppkopplingen till Internet är på 10 Gbit/s.

Det här är den minsta klientorienterade kontrollpunkten. Du kan dock utvärdera om det finns några ändringar eller vitlistor hos den nätverksåtgärdsgrupp som ansvarar för den här brandväggen.

I exempeldiagrammen kan du dra slutsatsen att sex enheter delar en konceptuell kanal på 10 Mbit/s. Beroende på storleken på de tillgångar som används kan detta vara otillräckligt för att uppfylla användarnas förväntningar.

## AEM-miljöns topologi {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

Att designa topologin i AEM-miljön kräver detaljerade kunskaper om systemkonfigurationen och hur nätverket är anslutet i användarmiljön.

Exempelscenariot innehåller en publiceringsgrupp med fem servrar, en binär S3-butik och dynamiska media konfigurerade.

Avsändaren delar med sig av sin 100 Mbit/s-anslutning med två enheter, utsidan av världen och AEM-instansen. För samtidiga överförings- och nedladdningsåtgärder bör du dividera numret med två. Den anslutna externa lagringsplatsen använder en separat anslutning.

AEM-instansen delar sin 1 Gbit/s-anslutning med flera tjänster. Från ett nätverkstopologiperspektiv motsvarar det att dela en kanal med olika tjänster.

## Definierade arbetsflöden för AEM-instansen {#defined-workflows-of-the-aem-instance}

När du tar hänsyn till nätverksprestanda kan det vara viktigt att tänka på arbetsflödena och publiceringen som kommer att ske i systemet. Dessutom använder S3 eller annan nätverksansluten lagring som du använder och I/O-begäranden nätverksbandbredd. Det innebär att även i ett helt optimerat nätverk kan prestanda begränsas av disk-I/O.

Om du vill effektivisera processerna kring tillgångsintag (särskilt när du överför ett stort antal resurser) kan du utforska arbetsflödena och förstå mer om deras konfiguration.

När du utvärderar den interna arbetsflödestopologin bör du analysera följande:

* Rutiner som skriver en tillgång
* Arbetsflöden/händelser som utlöses när resurser/metadata ändras
* Rutiner som läser en resurs

Här är några saker att tänka på:

* Läsa/skriva XMP-metadata
* Automatisk aktivering och replikering
* Intag/sidextrahering av delmaterial
* Överlappande arbetsflöden.

Här är ett kundexempel för definitionen av ett arbetsflöde för resurser.

![chlimage_1-357](assets/chlimage_1-357.png)
