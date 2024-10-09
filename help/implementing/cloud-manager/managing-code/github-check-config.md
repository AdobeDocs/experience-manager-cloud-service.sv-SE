---
title: GitHub-kontrollkonfiguration för privata databaser
description: Lär dig hur du styr de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6eabf593a7566129d32d9a5888cc480117bef51f
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# GitHub-kontrollkonfiguration för privata databaser {#github-check-config}

Lär dig hur du styr de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas.

## Konfiguration av GitHub-kontroller {#configuration}

När du använder [privata databaser](private-repositories.md#using) skapas automatiskt en [pipeline för full stackkodkvalitet](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Detta tillvägagångssätt startas vid varje uppdatering av pull-begäran.

Du kan kontrollera dessa kontroller genom att skapa en `.cloudmanager/pr_pipelines.yml`-fil i standardgrenen i den privata databasen.

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| Parameter | Möjliga värden | Standard | Beskrivning |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` eller `false` | `false` | Om bara den sista kommentaren med kodskanningen ska behållas i denna GitHub-pull-begäran eller om alla ska behållas |
| `type` | `CI_CD` | n/a | Definierar beteendet för en CI/CD-pipeline |
| `template.programID` | Heltal | Inga pipeline-variabler återanvänds | Du kan använda den för att återanvända de [pipeline-variabler](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) som angetts för en befintlig pipeline som automatiskt skapats av varje pull-begäran. |
| `template.pipelineID` | Heltal | Inga pipeline-variabler återanvänds | Du kan använda den för att återanvända de [pipeline-variabler](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) som angetts för en befintlig pipeline som automatiskt skapats av varje pull-begäran. |
| `namePrefix` | Sträng | `Full Stack Code Quality Pipeline for PR` | Används för att ange namnet på den pipeline som skapas automatiskt |
| `importantMetricsFailureBehavior` | `CONTINUE` eller `FAIL` eller `PAUSE` | `CONTINUE` | Anger det viktiga måttbeteendet för pipelinen <br>`CONTINUE` = Om ett viktigt mätresultat misslyckas flyttas pipelinen automatiskt framåt <br>`FAIL` = pipelinen avslutas med en FAILED-status om ett viktigt mätresultat misslyckas<br>`PAUSE` = Kodsökningssteget får en VÄNTNINGSstatus när ett viktigt mätvärde misslyckas och måste återupptas manuellt |
