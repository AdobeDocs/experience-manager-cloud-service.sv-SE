---
title: Krav för verktyget Innehållsöverföring
description: Krav för verktyget Innehållsöverföring
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: 4ccebe19d38f1ece58ea7170344ef2fd86a513d2
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

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
| AEM | Verktyget Innehållsöverföring kan endast köras i AEM 6.3 eller senare. |
| Storlek på segmentlager | En befintlig databas som har mindre än 55 miljoner JCR-noder och upp till 83 GB (komprimerad storlek online) på *Upphovsman* och 50 GB på *Publicera* stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för segmentbutikens storlek över dessa gränser. |
| Total storlek på innehållsdatabas <br>*(segmentbutik + datalager)* | Verktyget Innehållsöverföring är utformat för att överföra innehåll upp till 20 TB för datalagringstypen. Allt som är större än 20 TB stöds för närvarande inte. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för innehåll som är större än 20 TB. <br>Om du vill snabba upp innehållsöverföringsprocessen avsevärt för stora databaser kan du välja [förkopia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) kan användas. Detta gäller för datalagrets fildatalager, Amazon S3 och Azure Data Store-typer. För Amazon S3 och Azure Data Store stöds databasstorlekar större än 20 TB. |
| Total Lucene-indexstorlek | Total Lucene-indexstorlek på högst 25 GB, exklusive `/oak:index/lucene` och `/oak:index/damAssetLucene` stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för indexstorlek över denna gräns. |
| Nodnamnslängd | Längden på ett nodnamn måste vara 150 byte eller mindre när nodens överordnade sökväg är >= (lika med eller större än) 350 byte. Dessa nodnamn måste förkortas till &lt;= 150 byte för att det ska gå att använda dokumentnodarkivet på AEM as a Cloud Service. Inställningarna misslyckas om de långa nodnamnen inte är fasta. |
| Innehåll i oföränderliga banor | Verktyget Innehållsöverföring kan inte användas för att migrera innehåll i oföränderliga sökvägar. Överför innehåll från `/etc` endast säker `/etc` banor kan markeras, men bara för att ha stöd [AEM Forms till AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). För alla andra användningsfall, se [Omstrukturering av gemensamma lager](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) om du vill veta mer om omstrukturering av databaser. |
| Nodegenskapsvärde i MongoDB | Nodegenskapsvärden som lagras i MongoDB får inte överskrida 16 MB. Detta påtvingas av MongoDB. Inmatningar misslyckas om det finns egenskapsvärden som är större än denna gräns. Kör detta innan du kör en extrahering [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) skript. Granska alla stora egenskapsvärden och validera dem om de behövs. De som överskrider 16 MB måste konverteras till binära värden. |

## What&#39;s Next {#whats-next}

När du har granskat kraven och har fastställt om du kan använda verktyget för innehållsöverföring i ditt migreringsprojekt, se [Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
