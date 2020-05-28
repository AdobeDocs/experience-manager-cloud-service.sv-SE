---
title: Utvärderar komplexiteten i övergången till molntjänsten
description: Utvärderar komplexiteten i övergången till molntjänsten
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Cloud Readiness Analyzer {#accesing-complexity}

## Översikt {#overview}

Med Cloud Readiness Analyzer (CRA) kan du kontrollera om befintliga AEM-instanser är redo att gå över till molntjänsten genom att identifiera mönster som:

* Använd en AEM 6.x-funktion som för närvarande inte stöds i molntjänsten

* Vissa regler som påverkas av flytten till molntjänsten har överträtts

>[!NOTE]
>CRA:s resultat snabbar upp bedömningen av den utvecklingsinsats som krävs för att gå över till molntjänsten.

## Konfigurera molnberedskapsanalys {#setting-up-cra}

CRA släpps som ett paket som fungerar på alla AEM-källversioner från XX och senare och utforskar en övergång till molntjänsten.

Det finns på Software Distribution Portal och kan installeras med Package Manager.

### Använda Cloud Readiness Analyzer {#using-cra}

>[!NOTE]
> CRA kan köras i alla miljöer, inklusive lokala utvecklingsinstanser.

>[VIKTIGT]
>För att öka detekteringsgraden och undvika flaskhalsar i affärskritiska instanser rekommenderar vi att programmet körs i miljöer som är så nära produktionsmiljöer som möjligt inom användarprogram, innehåll och konfigurationer

### Visa utdata i molnberedskapsanalys {#viewing-output-cra}


1. Navigera till AEM Web Console genom att gå till **Adobe Experience Manager Web Console Configuration** med `https://serveraddress:serverport/system/console/configMgr`.

1. Välj Status - Cloud Readiness Analyzer enligt bilden nedan.

1. Du kan även visa utdata via ett reaktivt textbaserat eller reguljärt JSON-gränssnitt.

>[!NOTE]
> Mer information om de här metoderna finns i [Mönsteravkännare](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) .) Det här avsnittet måste läggas till när CRA är klart att användas.

## Nästa steg på Cloud-beredskap {#the-next-steps}

För att få mer information om din beredskap för molntjänster måste Adobe utvärdera utdata från CRA.

Skicka tillbaka filen genom att följa stegen nedan:

1. Navigera till AEM Web Console och hämta xx-filen som visas i bilden nedan.

1. Öppna en DayCare-biljett och skicka filen till Adobe senast:
   1. Logga en supportanmälan i Daycare som kallas **Cloud Readiness Analyzer Output**
   1. Bifoga en utdatafil till biljetten

