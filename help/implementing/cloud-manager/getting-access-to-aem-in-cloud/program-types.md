---
title: Program och programtyper
description: Läs om hierarkin i Cloud Manager och hur de olika programtyperna passar in i strukturen, och hur de skiljer sig åt.
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dc4008a33f6a786884a9aad30096ff4f0561346c
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 4%

---


# Program och programtyper {#understanding-programs}

Cloud Manager bygger på en hierarki av enheter. Informationen är inte viktig för ditt dagliga arbete i Cloud Manager, men en översikt över den kan hjälpa dig att förstå program och skapa egna.

![Cloud Manager-hierarki](assets/program-types1.png)

* **TENANT** - Hierarkins överkant. Alla kunder tillhandahålls med en klientorganisation.
* **PROGRAM** - Varje klientorganisation har ett eller flera program, [som ofta återspeglar kundens licensierade lösningar](introduction-production-programs.md).
* **MILJÖER** - Varje program har flera miljöer, till exempel produktion för direktinnehåll, en för mellanlagring och en för utvecklingsändamål.
   * Varje program kan bara ha en produktionsmiljö, men flera icke-produktionsmiljöer.
* **REPOSITORY** - Program har Git-databaser där program och slutkod bevaras för miljöerna.
* **VERKTYG OCH ARBETSFLÖDEN** - Pipelines hanterar distributionen av kod från databaser till miljöer medan andra verktyg ger åtkomst till loggar, övervakning och miljöhantering.

Ett exempel är ofta användbart när hierarkin ska sammanställas.

* WKND Travel and Adventure Enterprises kan vara en **tenant** som fokuserar på reserelaterade medier.
* WKND Travel and Adventure Enterprises-klienten kan ha två **program**: ett Sites-program för WKND Magazine och ett Assets-program för WKND Media.
* Programmen WKND Magazine och WKND Media skulle båda ha **miljöerna dev, stage och production**.

## Source kodarkiv {#source-code-repository}

Ett Cloud Manager-program levereras automatiskt med en egen Git-databas.

Användare har åtkomst till Cloud Manager Git-databasen via en Git-klient med ett kommandoradsverktyg eller en fristående visuell Git-klient. Alternativt kan de använda den integrerade utvecklingsmiljön (IDE) som de föredrar, till exempel Eclipse, IntelliJ eller NetBeans.

När en Git-klient har konfigurerats kan du hantera Git-databasen från Cloud Manager användargränssnitt. Mer information om hur du hanterar Git med Cloud Manager-användargränssnittet finns i [Access Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

Du börjar utveckla AEM Cloud-programmet genom att checka ut programkoden från Cloud Manager-databasen till din lokala dator.

```java
$ git clone {URL}
```

Arbetsflödet följer en standard-Git-process:

1. En användare klonar Git-fjärrdatabasen lokalt.
1. Användaren gör ändringar i sin lokala databas.
1. När det är klart implementerar användaren ändringarna i Git-fjärrdatabasen.

Den enda skillnaden är att Git-fjärrdatabasen är en del av Cloud Manager, som är transparent för utvecklaren.

## Programtyper {#program-types}

En användare kan skapa ett **produktion**-program eller ett **sandbox**-program.

* Ett **produktionsprogram** har skapats för att aktivera livatrafik för din webbplats.
   * Mer information finns i [Introduktion till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).
* Ett **sandlådeprogram** skapas vanligtvis för att fungera som träning, som kör demos, aktivering, POC eller dokumentation.
   * En sandlådemiljö är inte avsedd att bära trafik i realtid och har begränsningar som inte finns i ett produktionsprogram.
   * Den innehåller Sites, Assets och Edge Delivery Services och är förifylld med en Git-gren som innehåller exempelkod, en utvecklingsmiljö och en icke-produktionsprocess.
   * Mer information finns i [Introduktion till sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).
