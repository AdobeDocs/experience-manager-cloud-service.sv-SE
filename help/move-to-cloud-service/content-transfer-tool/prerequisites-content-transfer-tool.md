---
title: Krav för verktyget Innehållsöverföring
description: Krav för verktyget Innehållsöverföring
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: 2c0874ca14b9dd91ef62f2af85a9961b07c1b60b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Krav för verktyget Innehållsöverföring {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Viktigt att tänka på när du använder verktyget Innehållsöverföring"
>abstract="Granska viktiga aspekter av att använda verktyget för innehållsöverföring, inklusive Java- och AEM-versioner, datastortyper som stöds, användargrupper med mera."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Viktigt att tänka på när du använder Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="God praxis och riktlinjer"

I följande tabell sammanfattas förutsättningarna för att använda verktyget Innehållsöverföring.

Läs alla överväganden som anges nedan:

| Överväganden | Vad stöds för närvarande? |
|--- |--- |
| AEM | Verktyget Innehållsöverföring kan endast köras i AEM 6.3 eller senare. För att kunna använda verktyget för innehållsöverföring med AEM 6.2 eller tidigare krävs en uppgradering av innehållsarkivet på plats till AEM 6.5. Du behöver inte uppgradera koden till AEM 6.5 för detta. |
| Storlek på segmentlager | En befintlig databas som har mindre än 55 miljoner JCR-noder och upp till 83 GB (komprimerad onlinestorlek) på *Författare* och 31 GB på *Publicera* stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för segmentbutikens storlek över dessa gränser. |
| Total storlek för innehållsdatabas <br>*(segmentarkiv + datalager)* | Verktyget Innehållsöverföring är utformat för att överföra innehåll upp till 10 TB för datalagringstypen. Allt som är större än 10 TB stöds för närvarande inte. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för innehåll som är större än 10 TB. <br>För datalager av typen Amazon S3 och Azure Data Store kan ett valfritt  [förkopieringssteg ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) användas för att avsevärt snabba upp innehållsöverföringsprocessen och stöder större datalager än 10 TB. |
| Total indexstorlek | Den totala indexstorleken på högst 25 GB stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för indexstorlek över denna gräns. |
| Nodnamnslängd | Längden på ett nodnamn måste vara 150 byte eller mindre. Nodnamn som är längre än 150 byte måste förkortas till &lt;= 150 byte för att kunna användas som Cloud Service i dokumentnodarkivet AEM. Inställningarna misslyckas om de långa nodnamnen inte är fasta. |
| Innehåll i oföränderliga banor | Verktyget Innehållsöverföring kan inte användas för att migrera innehåll i oföränderliga sökvägar. Om du vill överföra innehåll från `/etc` får endast vissa `/etc`-sökvägar väljas, men bara för att ha stöd för [AEM Forms till AEM Forms som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). För alla andra användningsfall, se [Omstrukturering av gemensamma databaser](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) om du vill veta mer om omstrukturering av databaser. |
| Nodegenskapsvärde i MongoDB | Nodegenskapsvärden som lagras i MongoDB får inte överskrida 16 MB. Detta påtvingas av MongoDB. Inmatningar misslyckas om det finns egenskapsvärden som är större än denna gräns. Kör det här [ekkörningsskriptet](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) innan du kör en extrahering. Granska alla stora egenskapsvärden och validera om de behövs. De som överskrider 16 MB måste konverteras till binära värden. |

## What&#39;s Next {#whats-next}

När du har granskat kraven och har fastställt om du kan använda verktyget Innehållsöverföring i ditt migreringsprojekt, se [Ytterligare bästa praxis och överväganden](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) när du använder verktyget Innehållsöverföring.
