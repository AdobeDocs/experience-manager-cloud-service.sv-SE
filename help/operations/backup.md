---
title: Säkerhetskopiera och återställ i AEM as a Cloud Service
description: Läs mer om säkerhetskopiering och återställning på AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: 83b5d9a3ff0e9a3c69e36a97a3f733b05f827d3b
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Säkerhetskopiera och återställ i AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Säkerhetskopiera och återställ"
>abstract="AEM as a Cloud Service kan återställa en kunds fullständiga program (kod och innehåll) till specifika, förutbestämda tider de senaste sju dagarna, vilket ersätter det som fanns i produktionen. Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll. De senaste data som finns mellan tidpunkten för den återställda säkerhetskopieringen och den aktuella säkerhetskopian går förlorade. Mellanlagring återställs också till den gamla versionen."

Om innehåll eller data skadas kan AEM as a Cloud Service återställa en kunds fullständiga program (kod och innehåll). Den har återställts till specifika, förutbestämda tider under de senaste sju dagarna och ersätter det som fanns i produktionen.
Om en kunds distribution, dvs. den distribuerade programkoden antingen är trasig eller felfri, är det bättre att åtgärda den och återställa den till en ny version i stället för att återställa den från en säkerhetskopia. Säkerhetskopieringen utförs på ett sätt som inte påverkar programmets körningsprestanda.

>[!CAUTION]
>
>Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll. De senaste data som finns mellan tidpunkten för den återställda säkerhetskopieringen och den aktuella säkerhetskopian går förlorade. Mellanlagring återställs också till den gamla versionen.

## Användning {#how-to-use}

Kunderna ska lämna in en supportanmälan som beskriver det problem som uppstår. Supportbiljetten leder vanligtvis till en utredning av supporten från Adobe som sedan kan avgöra om en återställning är nödvändig.

AEM as a Cloud Service stöder:

* Säkerhetskopiera och återställ för scen-, produktions- och utvecklingsmiljöer.
* 24 timmars tidsåterställning, vilket innebär att systemet kan återställas till valfri punkt under de senaste 24 timmarna.
* Återställ från en specifik, Adobe-definierad tidsstämpel som tagits två gånger dagligen de senaste sju dagarna. Alla replikeringsmeddelanden (som tas bort, uppdateras och skapas) bevaras.

I samtliga fall är den anpassade kodversionen hämtad från den senast slutförda distributionen före återställningspunkten.

Målet för återställningstiden (RTO) kan variera, men som en allmän riktlinje tar återställningssekvensen mellan 60 och 90 minuter i genomsnitt beroende på flera faktorer, till exempel databasstorlek. Förhandsgranskningsmiljöer och utgivare i flera regioner kan förlänga återställningstiden.

Efter en återställning uppdateras den AEM versionen till den senaste.

>[!CAUTION]
>
>Data från borttagna miljöer går förlorade permanent och kan inte återställas.

## Säkerhetskopiering offline {#offsite-backup}

Även om regelbundna säkerhetskopieringar täcker risken för oavsiktliga raderingar eller tekniska fel inom AEM Cloud Service måste även de risker som kan uppstå om en region inte fungerar täckas. Förutom tillgänglighet är den största risken i sådana dataområdesavbrott i första hand en dataförlust.
AEM as a Cloud Service täcker denna risk som standard för alla AEM produktionsmiljöer. Det kopierar kontinuerligt hela AEM till en fjärrregion och gör det tillgängligt för återställning i tre månader. Adobe anropar den här funktionen för säkerhetskopiering offline.
Återställandet av AEM Cloud Service för fas- och produktionsmiljöer utförs av AEM Service Reliable Engineering om dataregionsfel uppstår.