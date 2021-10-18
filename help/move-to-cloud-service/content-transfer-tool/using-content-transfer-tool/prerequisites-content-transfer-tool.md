---
title: Prerequisites for Content Transfer Tool
description: Prerequisites for Content Transfer Tool
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: fa7e5d07ed52a71999de95bbf6299ae5eb7af537
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# Krav för verktyget Innehållsöverföring {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Important Considerations for using Content Transfer Tool"
>abstract="Review important considerations to use the Content Transfer tool including Java and AEM verions, supported Datastore types, user groups considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Viktigt att tänka på när du använder Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="God praxis och riktlinjer"

I följande tabell sammanfattas förutsättningarna för att använda verktyget Innehållsöverföring.

Läs alla överväganden som anges nedan:

| Considerations | What is Currently Supported |
|--- |--- |
| AEM Version | Verktyget Innehållsöverföring kan endast köras i AEM 6.3 eller senare. För att kunna använda verktyget för innehållsöverföring med AEM 6.2 eller tidigare krävs en uppgradering av innehållsarkivet på plats till AEM 6.5. Du behöver inte uppgradera koden till AEM 6.5 för detta. |
| Storlek på segmentlager | En befintlig databas som har mindre än 55 miljoner JCR-noder och upp till 83 GB (komprimerad onlinestorlek) på *Författare* och 31 GB på *Publicera* stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för segmentbutikens storlek över dessa gränser. |
| Total storlek för innehållsdatabas <br>*(segmentarkiv + datalager)* | Content Transfer Tool is designed to transfer content up to 10 TB for File Data Store type of data store. Anything higher than 10 TB is not currently supported. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för innehåll som är större än 10 TB. <br>För datalager av typen Amazon S3 och Azure Data Store kan ett valfritt  [förkopieringssteg ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) användas för att avsevärt snabba upp innehållsöverföringsprocessen och stöder större datalager än 10 TB. |
| Total indexstorlek | Den totala indexstorleken på högst 25 GB stöds för närvarande. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för indexstorlek över denna gräns. |
| Node Name Length | Längden på ett nodnamn måste vara 150 byte eller mindre. Nodnamn som är längre än 150 byte måste förkortas till &lt;= 150 byte för att det ska gå att använda dokumentnodarkivet i AEM as a Cloud Service. Ingestions will fail if these long node names are not fixed. |
| Content in Immutable Paths | Verktyget Innehållsöverföring kan inte användas för att migrera innehåll i oföränderliga sökvägar. Om du vill överföra innehåll från `/etc` får endast vissa `/etc`-sökvägar väljas, men bara för att ha stöd för [AEM Forms till AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). För alla andra användningsfall, se [Omstrukturering av gemensamma databaser](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) om du vill veta mer om omstrukturering av databaser. |
| Node property value in MongoDB | Node property values stored in MongoDB cannot exceed 16MB. This is enforced by MongoDB. Inmatningar misslyckas om det finns egenskapsvärden som är större än denna gräns. Before running an extraction, run this [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Granska alla stora egenskapsvärden och validera om de behövs. De som överskrider 16 MB måste konverteras till binära värden. |

## What&#39;s Next {#whats-next}

När du har granskat kraven och har fastställt om du kan använda verktyget Innehållsöverföring i ditt migreringsprojekt, se [Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
