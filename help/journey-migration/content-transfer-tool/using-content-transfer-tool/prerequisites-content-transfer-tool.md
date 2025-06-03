---
title: Krav för verktyget Innehållsöverföring
description: Bekanta dig med kraven för verktyget Innehållsöverföring
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
feature: Migration
role: Admin
source-git-commit: 3e3d018dfd4babce9abef858e487bf1c116ed3a6
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Krav för verktyget Innehållsöverföring {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Viktigt att tänka på när du använder verktyget Innehållsöverföring"
>abstract="Läs igenom viktiga aspekter av att använda verktyget för innehållsöverföring, inklusive Java™- och AEM-versioner, datastore-typer som stöds, användargrupper med mera."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html" text="Viktigt att tänka på när du använder verktyget Innehållsöverföring"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#best-practices" text="God praxis och riktlinjer"

I följande tabell sammanfattas förutsättningarna för att använda verktyget Innehållsöverföring.

Granska alla överväganden som anges nedan:

| Överväganden | Vad stöds för närvarande? |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM Version | Innehållsöverföringsverktyget kan endast köras i AEM 6.3 eller senare. |
| Storlek på segmentlager | En befintlig databas som har mindre än 750 miljoner JCR-noder och upp till 500 GB (komprimerad onlinestorlek) på *Författare* och 50 GB på *Publicera* stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst så att du kan diskutera olika alternativ för segmentbutikens storlek över dessa gränser. |
| Total storlek för innehållslagringsplatsen <br>*(segmentarkivet + datalagret)* | Verktyget Innehållsöverföring är utformat för att överföra innehåll på upp till 20 terabyte för datalagringstypen. Allt som är större än 20 terabyte stöds för närvarande inte. Skapa en supportanmälan med Adobe kundtjänst så att du kan diskutera olika alternativ för innehåll som är större än 20 terabyte. <br>Om du vill snabba upp innehållsöverföringsprocessen avsevärt för stora databaser kan du använda ett [pre-copy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step) -steg (valfritt). Den här processen gäller datalagrets fildatalager, Amazon S3 och Azure Data Store-typer. För Amazon S3 och Azure Data Store stöds databasstorlekar större än 20 terabyte. |
| Total Lucene-indexstorlek | Total Lucene-indexstorlek på högst 25 GB, exklusive `/oak:index/lucene` och `/oak:index/damAssetLucene` stöds. Skapa en supportanmälan med Adobe kundtjänst så att du kan diskutera olika alternativ för indexstorlek över denna gräns. |
| Innehåll i oföränderliga banor | Verktyget Innehållsöverföring kan inte användas för att migrera innehåll i oföränderliga sökvägar. Om du vill överföra innehåll från `/etc` kan du markera vissa `/etc`-sökvägar, men bara för att stödja [AEM Forms till AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). För alla andra användningsfall, se [Omstrukturering av gemensamma databaser](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) om du vill veta mer om omstrukturering av databaser. |
| Nodegenskapsvärde i MongoDB | Nodegenskapsvärden som lagras i MongoDB får inte överskrida 16 MB. Den här regeln används av MongoDB. Inställningarna misslyckas om det finns egenskapsvärden som är större än denna gräns. Innan du kör en extrahering kör du det här [ekörningsskriptet](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar). Granska alla stora egenskapsvärden och validera dem om de behövs. De som överskrider 16 MB måste konverteras till binära värden. |

## What&#39;s Next {#whats-next}

När du har granskat kraven och har fastställt om du kan använda verktyget Innehållsöverföring i ditt migreringsprojekt, se [Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html).