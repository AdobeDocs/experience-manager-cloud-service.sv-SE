---
title: Krav för verktyget Innehållsöverföring (äldre)
description: Krav för verktyget Innehållsöverföring
hide: true
hidefromtoc: true
exl-id: 6b2878cb-6882-452b-8cab-e590316633f6
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Krav för verktyget Innehållsöverföring (äldre) {#prerequisites}

I följande tabell sammanfattas förutsättningarna för att använda verktyget Innehållsöverföring.

Läs alla överväganden som anges nedan:

| Överväganden | Vad stöds för närvarande? |
|--- |--- |
| AEM | Verktyget Innehållsöverföring kan endast köras i AEM 6.3 eller senare. |
| Storlek på segmentlager | En befintlig databas som har mindre än 55 miljoner JCR-noder och upp till 83 GB (komprimerad storlek online) på *Upphovsman* och 31 GB på *Publicera* stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för segmentbutikens storlek över dessa gränser. |
| Total storlek på innehållsdatabas <br>*(segmentbutik + datalager)* | Verktyget Innehållsöverföring är utformat för att överföra innehåll upp till 20 TB för datalagringstypen. Allt som är större än 20 TB stöds för närvarande inte. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för innehåll som är större än 20 TB. <br>Om du vill snabba upp innehållsöverföringsprocessen avsevärt för stora databaser kan du välja [förkopia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) kan användas. Detta gäller för datalagrets fildatalager, Amazon S3 och Azure Data Store-typer. För Amazon S3 och Azure Data Store stöds databasstorlekar större än 20 TB. |
| Total Lucene-indexstorlek | Total Lucene-indexstorlek på högst 25 GB stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för indexstorlek över denna gräns. |
| Nodnamnslängd | Längden på ett nodnamn måste vara 150 byte eller mindre. Nodnamn som är längre än 150 byte måste förkortas till &lt;= 150 byte för att det ska gå att använda dokumentnodarkivet i AEM as a Cloud Service. Inställningarna misslyckas om de långa nodnamnen inte är fasta. |
| Innehåll i oföränderliga banor | Verktyget Innehållsöverföring kan inte användas för att migrera innehåll i oföränderliga sökvägar. Överför innehåll från `/etc` endast säker `/etc` banor kan markeras, men bara för att ha stöd [AEM Forms till AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). För alla andra användningsfall, se [Omstrukturering av gemensamma lager](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) om du vill veta mer om omstrukturering av databaser. |
| Nodegenskapsvärde i MongoDB | Nodegenskapsvärden som lagras i MongoDB får inte överskrida 16 MB. Detta påtvingas av MongoDB. Inmatningar misslyckas om det finns egenskapsvärden som är större än denna gräns. Kör detta innan du kör en extrahering [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) skript. Granska alla stora egenskapsvärden och validera dem om de behövs. De som överskrider 16 MB måste konverteras till binära värden. |

## What&#39;s Next {#whats-next}

När du har granskat kraven och har fastställt om du kan använda verktyget för innehållsöverföring i ditt migreringsprojekt, se [Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
