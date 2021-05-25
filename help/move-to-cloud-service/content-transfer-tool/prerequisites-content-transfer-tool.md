---
title: Krav för verktyget Innehållsöverföring
description: Krav för verktyget Innehållsöverföring
source-git-commit: ebe12a71df610a68c43048667136e331c1bd8f86
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Krav för verktyget Innehållsöverföring {#prerequisites}

I följande tabell sammanfattas förutsättningarna för att använda verktyget Innehållsöverföring. Läs alla överväganden som anges nedan:

| Överväganden | Vad stöds för närvarande? |
|--- |--- |
| AEM | Verktyget Innehållsöverföring kan endast köras i AEM 6.3 eller senare. För att kunna använda verktyget för innehållsöverföring med AEM 6.2 eller tidigare krävs en uppgradering av innehållsarkivet på plats till AEM 6.5. Du behöver inte uppgradera koden till AEM 6.5 för detta. |
| Storlek på segmentlager | Innehållsöverföringsverktyget har för närvarande stöd för upp till 83 GB på *Författare* och 31 GB på *Publicera*. |
| Total storlek på innehållsdatabas <br>*(innehållsarkiv + datalager)* | Verktyget Innehållsöverföring är utformat för att överföra innehåll upp till 10 TB. Allt som är större än 10 TB stöds för närvarande inte. Skapa en supportanmälan med Adobe kundtjänst för att diskutera alternativ för innehåll som är större än 10 TB. |
| Innehåll i oföränderliga banor | Verktyget Innehållsöverföring fungerar inte för att migrera innehållet i oföränderliga sökvägar som `“/etc”`. <br>Mer information om omstrukturering av databaser och arbetsflödesmodeller finns i  [Common ](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) Restructuring. |