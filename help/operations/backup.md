---
title: Säkerhetskopiera och återställ i AEM as a Cloud Service
description: Säkerhetskopiera och återställ i AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: 7778430b409bdd6f30530d34f2e8cd10d63df153
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Säkerhetskopiera och återställ i AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Säkerhetskopiera och återställ"
>abstract="AEM as a Cloud Service kan återställa en kunds fullständiga program (kod och innehåll) till specifika, förutbestämda tider de senaste sju dagarna, vilket ersätter det som fanns i produktionen. Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll. De senaste data mellan tidpunkten för den återställda säkerhetskopieringen och den aktuella kommer att gå förlorade. Mellanlagring återställs också till den gamla versionen."

Om innehåll eller data skadas kan AEM as a Cloud Service återställa en kunds fullständiga program (kod och innehåll) till specifika, förutbestämda tider de senaste sju dagarna och ersätta det som fanns i produktionen.
Om en kunds distribution, dvs. den distribuerade programkoden antingen är trasig eller felfri, är det bättre att åtgärda den och återställa den till en ny version i stället för att återställa den från en säkerhetskopia. Säkerhetskopieringen utförs på ett sätt som inte påverkar programmets körningsprestanda.

>[!CAUTION]
>
>Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll. De senaste data mellan tidpunkten för den återställda säkerhetskopieringen och den aktuella kommer att gå förlorade. Mellanlagring återställs också till den gamla versionen.

## Användning {#how-to-use}

Kunderna ska lämna in en supportanmälan som beskriver det problem som uppstår. Detta kommer att leda till en utredning av Adobe support, som kommer att avgöra om en återställning är nödvändig.

AEM as a Cloud Service stöder:

* Säkerhetskopiera och återställ för scen-, produktions- och utvecklingsmiljöer.
* 24 timmars tidsåterställning, vilket innebär att systemet kan återställas till valfri punkt under de senaste 24 timmarna.
* Återställ från en viss, Adobe-definierad tidsstämpel som tagits två gånger dagligen de senaste 7 dagarna.  Alla replikeringsmeddelanden (som tas bort, uppdateras, skapas) bevaras.

I samtliga fall hämtas den anpassade kodversionen från den senaste distributionen som lyckades före återställningspunkten.

Målet för återställningstiden (RTO) varierar beroende på databasens storlek, men som en allmän riktlinje bör återställningssekvensen ta från 30 minuter till flera timmar.

Efter en återställning uppdateras den AEM versionen till den senaste.

>[!CAUTION]
>
>Data från borttagna miljöer går förlorade permanent och kan inte återställas.

## Säkerhetskopiering offline {#offsite-backup}

Även om regelbundna säkerhetskopieringar täcker risken för oavsiktliga borttagningar eller tekniska fel i AEM Cloud Services, måste även riskerna som kan uppstå om en region slutar fungera täckas. Förutom tillgänglighet är den största risken i sådana dataområdesavbrott i första hand en dataförlust.
AEM as a Cloud Service täcker denna risk som standard för alla AEM produktionsmiljöer genom att kontinuerligt kopiera hela AEM till en fjärrregion och göra den tillgänglig för återställning under en period av tre månader. Den här funktionen kallas för säkerhetskopiering offline.
Återskapandet av AEM Cloud-tjänster för scen- och produktionsmiljöer utförs av AEM Service Reliable Engineering i händelse av dataregionala avbrott.
