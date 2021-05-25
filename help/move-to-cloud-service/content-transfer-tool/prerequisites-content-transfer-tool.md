---
title: Krav för verktyget Innehållsöverföring
description: Krav för verktyget Innehållsöverföring
source-git-commit: becb8368af8a8228bf3248bde66ad7164187a9c4
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Krav för verktyget Innehållsöverföring {#prerequisites}

I följande tabell sammanfattas förutsättningarna för att använda verktyget Innehållsöverföring.

Läs alla överväganden som anges nedan:

| Överväganden | Vad stöds för närvarande? |
|--- |--- |
| AEM | Verktyget Innehållsöverföring kan endast köras i AEM 6.3 eller senare. För att kunna använda verktyget för innehållsöverföring med AEM 6.2 eller tidigare krävs en uppgradering av innehållsarkivet på plats till AEM 6.5. Du behöver inte uppgradera koden till AEM 6.5 för detta. |
| Storlek på segmentlager | Innehållsöverföringsverktyget har för närvarande stöd för upp till 83 GB på *Författare* och 31 GB på *Publicera*. |
| Total storlek för innehållsdatabas <br>*(segmentarkiv + datalager)* | Verktyget Innehållsöverföring är utformat för att överföra innehåll upp till 10 TB. Allt som är större än 10 TB stöds för närvarande inte. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för innehåll som är större än 10 TB. |
| Innehåll i oföränderliga banor | Verktyget Innehållsöverföring kan inte användas för att migrera innehåll i oföränderliga sökvägar som `“/etc”`. Vissa `"/etc"`-sökvägar kan väljas, men endast för att ge stöd för [AEM Forms till AEM Forms som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). För alla andra användningsfall, se [Omstrukturering av gemensamma databaser](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) om du vill veta mer om omstrukturering av databaser. |

## What&#39;s Next {#whats-next}

När du har granskat kraven och har fastställt om du kan använda verktyget Innehållsöverföring i ditt migreringsprojekt, se [Ytterligare bästa praxis och överväganden](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) när du använder verktyget Innehållsöverföring.
