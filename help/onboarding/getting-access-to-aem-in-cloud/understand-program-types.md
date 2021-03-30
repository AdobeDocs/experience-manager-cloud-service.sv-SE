---
title: Program- och programtyper
description: Program- och programtyper - Cloud Services
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# Förstå program och programtyper {#understanding-programs}

I Cloud Manager har du klientorganisationen högst upp som kan ha flera program inuti. Varje program får inte innehålla mer än en produktionsmiljö och flera icke-produktionsmiljöer.

I följande diagram visas hierarkin för enheter i Cloud Manager.

![bild](assets/program-types1.png)

## Databas för källkod {#source-code-repository}

Cloud Manager-programmet kommer att etableras automatiskt med sin egen Git-databas.

För att en användare ska få åtkomst till molnhanterarens Git-databas måste användaren använda en Git-klient med ett kommandoradsverktyg, en fristående visuell Git-klient eller användarens IDE som Eclipse, IntelliJ, NetBeans.

När en Git-klient har konfigurerats kan du hantera din Git-databas via användargränssnittet i Cloud Manager. Mer information om hur du hanterar Git med hjälp av användargränssnittet i Cloud Manager finns i [Åtkomst till Git](/help/implementing/cloud-manager/accessing-git.md).

För att börja utveckla AEM Cloud-programmet måste en lokal kopia av programkoden göras genom att checka ut den från Cloud Manager-databasen till en plats på den lokala datorn där de vill skapa sin databas.

```java
$ git clone {URL}
```

>[!NOTE]
>En användare kan checka ut en kopia av sin kod och göra ändringar i den lokala koddatabasen. När det är klart kan användaren spara sina kodändringar i fjärrkoddatabasen i Cloud Manager.

## Programtyper {#program-types}

En användare kan skapa en **sandlåda** eller ett **Production**-program.

* Ett *produktionsprogram* skapas för att aktivera livstrafik vid rätt tidpunkt i framtiden.
Mer information finns i [Introduktion till produktionsprogram](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md).


* Ett *sandlådeprogram* skapas vanligtvis för att användas i utbildningssyfte, köra demo, aktivering, POC eller dokumentation. Den är inte avsedd att transportera livstrafik och kommer att ha begränsningar som ett produktionsprogram inte kommer att ha. Den kommer att innehålla Sites and Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en Dev-miljö och en icke-produktionsprocess.
Mer information finns i [Introduktion till sandlådeprogram](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).

