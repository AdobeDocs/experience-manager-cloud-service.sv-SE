---
title: Pull Request Checks for Private Repositories
description: Lär dig hur du styr de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0ec47218d598aad6b225a9d5d8faeab20e606716
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Hämta begärandekontroller för privata databaser {#github-check-config}

Lär dig hur du styr de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas.

## Konfiguration av kontroller av privata databaser {#configuration}

När du använder [privata databaser](private-repositories.md#using) skapas automatiskt en [pipeline för full stackkodkvalitet](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Detta tillvägagångssätt startas vid varje uppdatering av pull-begäran.

Du kan kontrollera de här kontrollerna genom att skapa en `.cloudmanager/pr_pipelines.yml`-konfigurationsfil i standardgrenen i den privata databasen.

```yaml
pullRequest:
  shouldDeletePreviousComment: false
  shouldSkipCheckAnnotations: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR
    importantMetricsFailureBehavior: CONTINUE
```

| Parameter | Möjliga värden | Standard | Beskrivning |
| --- | --- | --- | --- |
| `shouldDeletePreviousComment` | `true` eller `false` | `false` | Om bara den sista kommentaren med kodskanningen ska behållas i den här GitHub-pull-begäran eller om alla ska behållas. Om du anger det till `false` (standard) innebär det att tidigare kommentarer inte tas bort. |
| `shouldSkipCheckAnnotations` | `true` eller `false` | `false` | Anger om det ska finnas ytterligare anteckningar i kontrollen för GitHub-pull-begäran eller inte. Om du anger det som `false` (standard) betyder det att kontrollanteckningar inte hoppas över och inkluderas i feedback. |
| `type` | `CI_CD` | n/a | Definierar beteendet för pipelinekonfigurationer för CI/CD (Continuous Integration/Continuous Deployment). |
| `template.programId` | Heltal | Inga pipeline-variabler återanvänds | Du kan använda den för att återanvända de [pipeline-variabler](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) som angetts för en befintlig pipeline som automatiskt skapats av varje pull-begäran. |
| `template.pipelineId` | Heltal | Inga pipeline-variabler återanvänds | Du kan använda den för att återanvända de [pipeline-variabler](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) som angetts för en befintlig pipeline som automatiskt skapats av varje pull-begäran. |
| `namePrefix` | Sträng | `Full Stack Code Quality Pipeline for PR` | Används för att ange prefixet för namnet på den pipeline som skapas automatiskt. |
| `importantMetricsFailureBehavior` | `CONTINUE` eller `FAIL` eller `PAUSE` | `CONTINUE` | Anger det viktiga måttbeteendet för pipelinen <br>`CONTINUE` = Om ett viktigt mätresultat misslyckas flyttas pipelinen automatiskt framåt <br>`FAIL` = pipelinen avslutas med en FAILED-status om ett viktigt mätresultat misslyckas<br>`PAUSE` = Kodsökningssteget får en VÄNTNINGSstatus när ett viktigt mätvärde misslyckas och måste återupptas manuellt |




