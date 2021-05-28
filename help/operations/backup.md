---
title: Säkerhetskopiera och återställa i AEM som en Cloud Service
description: Säkerhetskopiera och återställa i AEM som en Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Säkerhetskopiera och återställa i AEM som en Cloud Service


>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Säkerhetskopiera och återställ"
>abstract="AEM som en Cloud Service kan återställa en kunds fullständiga program (kod och innehåll) till specifika, förutbestämda tider de senaste sju dagarna och ersätta det som fanns i produktionen. Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll. De senaste data mellan tidpunkten för den återställda säkerhetskopieringen och den aktuella kommer att gå förlorade. Mellanlagring återställs också till den gamla versionen."

Om innehåll eller data skadas kan AEM som Cloud Service återställa en kunds fullständiga program (kod och innehåll) till specifika, förutbestämda tider de senaste sju dagarna och ersätta det som fanns i produktionen.
Om en kunds distribution, dvs. den distribuerade programkoden antingen är trasig eller felfri, är det bättre att åtgärda den och återställa den till en ny version i stället för att återställa den från en säkerhetskopia. Säkerhetskopieringen utförs på ett sätt som inte påverkar programmets körningsprestanda.

>[!CAUTION]
>
>Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll. De senaste data mellan tidpunkten för den återställda säkerhetskopieringen och den aktuella kommer att gå förlorade. Mellanlagring återställs också till den gamla versionen.

## Användning

Kunderna ska lämna in en supportanmälan som beskriver det problem som uppstår. Detta kommer att leda till en utredning av Adobe support, som kommer att avgöra om en återställning är nödvändig.

AEM som en Cloud Service har stöd för:

* 24 timmars tidsåterställning, vilket innebär att systemet kan återställas till valfri punkt under de senaste 24 timmarna.
* Återställ från en specifik, Adobe-definierad tidsstämpel som tagits en gång om dagen de senaste 7 dagarna.  Alla replikeringsmeddelanden (som tas bort, uppdateras, skapas) bevaras.

I samtliga fall hämtas den anpassade kodversionen från den senaste distributionen som lyckades före återställningspunkten.

Målet för återställningstiden (RTO) varierar beroende på databasens storlek, men som en allmän riktlinje när återställningssekvensen börjar bör det ta ca 30 minuter.

Efter en återställning uppdateras den AEM versionen till den senaste.

**Data från borttagna miljöer går förlorade permanent och kan inte återställas.**
