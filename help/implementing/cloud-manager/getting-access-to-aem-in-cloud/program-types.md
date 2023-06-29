---
title: Program och programtyper
description: Lär dig mer om Cloud Managers hierarki och hur de olika typerna av program passar in i dess struktur och hur de skiljer sig åt.
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Program och programtyper {#understanding-programs}

Cloud Manager byggs kring en hierarki av enheter. Detaljerna i det här är inte viktiga för ditt dagliga arbete i Cloud Manager, men en översikt av det hjälper dig att förstå program och konfigurera dina egna.

![Cloud Manager-hierarki](assets/program-types1.png)

* **TENANT** - Detta är överst i hierarkin. Alla kunder tillhandahålls med en klient.
* **PROGRAM** - Varje innehavare har ett eller flera program, [som ofta återspeglar kundens licensierade lösningar.](introduction-production-programs.md)
* **MILJÖ** - Varje program har flera miljöer, t.ex. produktion för direktinnehåll, en för mellanlagring och en för utvecklingsändamål.
   * Varje program kan bara ha en produktionsmiljö, men flera icke-produktionsmiljöer.
* **DATABAS** - Program har Git-databaser där program och frontkod bevaras för miljöer.
* **VERKTYG OCH ARBETSFLÖDEN** - Pipelines hanterar koddistribution från databaser till miljöer medan andra verktyg ger åtkomst till loggar, övervakning och miljöhantering.

Ett exempel är ofta användbart när hierarkin ska sammanställas.

* WKND Travel and Adventure Enterprises kan vara en **tenant** som fokuserar på reserelaterade medier.
* Innehavare av WKND Travel och Adventure Enterprises kan ha två **program**: ett Sites-program för WKND Magazine och ett Assets-program för WKND Media.
* Programmen WKND Magazine och WKND Media skulle ha både utveckling, scen och produktion **miljöer**.

## Databas för källkod {#source-code-repository}

Ett Cloud Manager-program etableras automatiskt med en egen Git-databas.

För att få åtkomst till molnhanterarens Git-databas måste användarna använda en Git-klient med ett kommandoradsverktyg, en fristående visuell Git-klient eller användarens valfria IDE som Eclipse, IntelliJ eller NetBeans.

När en Git-klient har konfigurerats kan du hantera din Git-databas via användargränssnittet i Cloud Manager. Mer information om hur du hanterar Git med användargränssnittet i Cloud Manager finns i [Åtkomst till Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

Om du vill börja utveckla AEM Cloud-programmet måste du checka ut den från Cloud Manager-databasen till en plats på den lokala datorn.

```java
$ git clone {URL}
```

Arbetsflödet är alltså ett standard-Git-arbetsflöde.

1. En användare klonar en lokal kopia av Git-databasen.
1. Användaren gör ändringar i den lokala koddatabasen.
1. När det är klart genomför användaren ändringarna tillbaka till Git-fjärrdatabasen.

Den enda skillnaden är att Git-fjärrdatabasen är en del av Cloud Manager, som är genomskinlig för utvecklaren.

## Programtyper {#program-types}

En användare kan skapa en **produktion** program eller **sandlåda** program.

* A **produktionsprogram** skapas för att aktivera livatrafik för din webbplats.
   * Se [Introduktion till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) för mer information.
* A **sandlådeprogram** skapas vanligtvis för utbildning, löpande demonstrationer, aktivering, POC eller dokumentation.
   * En sandlådemiljö är inte avsedd att bära trafik i realtid och har begränsningar som ett produktionsprogram inte kommer att ha.
   * Den innehåller Sites and Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en utvecklingsmiljö och en icke-produktionsprocess.
   * Se [Introduktion till sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) för mer information.
