---
title: Säkerhetskopiera och återställ i AEM som en molntjänst
description: 'Säkerhetskopiera och återställ i AEM som en molntjänst '
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 1%

---


# Säkerhetskopiera och återställ i AEM som en molntjänst

Om innehåll eller data skadas kan AEM som molntjänst återställa en kunds fullständiga program (kod och innehåll) till specifika, förutbestämda tider de senaste sju dagarna och ersätta det som fanns i produktionen.
Om en kunds distribution, dvs. den distribuerade programkoden antingen är trasig eller felfri, är det bättre att åtgärda den och återställa den till en ny version i stället för att återställa den från en säkerhetskopia.

>[!CAUTION]
>
>Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll. De senaste data mellan tidpunkten för den återställda säkerhetskopieringen och den aktuella kommer att gå förlorade. Mellanlagring återställs också till den gamla versionen.

## Användning

Kunderna ska lämna in en supportanmälan som beskriver det problem som uppstår. Detta kommer att leda till en utredning av Adobes support som kommer att avgöra om en återställning är nödvändig.

AEM som molntjänst har stöd för:

* 24 timmars tidsåterställning, vilket innebär att systemet kan återställas till valfri punkt under de senaste 24 timmarna.
* Återställ från en viss Adobe-definierad tidsstämpel som tagits en gång om dagen de senaste 7 dagarna.  Alla replikeringsmeddelanden (som tas bort, uppdateras, skapas) bevaras.

I samtliga fall hämtas den anpassade kodversionen från den senaste distributionen som lyckades före återställningspunkten.

Målet för återställningstiden (RTO) varierar beroende på databasens storlek, men som en allmän riktlinje när återställningssekvensen börjar bör det ta ca 30 minuter.

Efter en återställning uppdateras AEM-versionen till den senaste versionen.

**Data från borttagna miljöer går förlorade permanent och kan inte återställas.**
