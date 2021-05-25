---
title: Krav för verktyget Innehållsöverföring
description: Krav för verktyget Innehållsöverföring
source-git-commit: c760b97cdb565244cf20f5193de3e3ebab1579ad
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Krav för verktyget Innehållsöverföring {#prerequisites}

I följande tabell sammanfattas förutsättningarna innan verktyget Innehållsöverföring används. Läs alla överväganden som anges nedan:

| Överväganden | Vad stöds för närvarande? |
|--- |--- |
| AEM | Verktyget Innehållsöverföring kan endast köras i AEM 6.3 eller senare. För att kunna använda verktyget för innehållsöverföring med AEM 6.2 eller tidigare krävs en uppgradering av innehållsarkivet på plats till AEM 6.5. Du behöver inte uppgradera koden till AEM 6.5 för detta. |
| Storlek på segmentlager | Innehållsöverföringsverktyget har för närvarande stöd för upp till 83 GB på *Författare* och 31 GB på *Publicera*. |
| Total storlek på innehållslagringsplatsen (innehållslager + datalager) | Verktyget Innehållsöverföring är utformat för att överföra innehåll upp till 10 TB. Allt som är större än 10 TB stöds för närvarande inte. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för innehåll som är större än 10 TB. |
| Innehåll i oföränderliga banor | Verktyget Innehållsöverföring fungerar inte för att migrera innehållet i oföränderliga sökvägar som `“/etc”`. Läs [Omstrukturering av gemensamma databaser](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) om du vill veta mer om omstruktureringar av databaser och arbetsflödesmodeller. |