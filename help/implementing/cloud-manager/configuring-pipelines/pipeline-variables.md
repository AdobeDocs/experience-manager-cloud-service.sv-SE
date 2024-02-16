---
title: Konfigurera pipeline-variabler
description: Lär dig hur du kan använda pipeline-variabler i Cloud Manager för att hantera specifika konfigurationsvariabler för ditt bygge.
source-git-commit: 7b98883d16893534387fa10665f5fa432d74470f
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---


# Konfigurera pipeline-variabler {#configuring-pipeline-variables}

Din byggprocess kan vara beroende av specifika konfigurationsvariabler som skulle vara olämpliga att placera i Git-databasen, eller så måste du variera dem mellan pipeline-körningar som använder samma gren. Med Cloud Manager kan du hantera dessa data som pipeline-variabler.

## Rörledningsvariabler {#pipeline-variables}

Med Cloud Manager kan du konfigurera pipeline-variabler på flera olika sätt.

* [Via användargränssnittet i Cloud Manager](#ui)
* [Använda Cloud Manager CLI](#cli)
* [Använda Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

Variabler kan lagras som antingen oformaterad text eller krypteras i vila. I båda fallen görs variablerna tillgängliga i byggmiljön som en miljövariabel som sedan kan refereras inifrån `pom.xml` eller andra byggskript.

### Variabla namngivningskonventioner för pipeline {#naming-conventions}

Variabelnamn måste följa följande konventioner.

* Variabler får endast innehålla alfanumeriska tecken och understreck (`_`).
* Namnen ska vara versaler.
* Det finns en gräns på 200 variabler per pipeline.
* Varje namn får innehålla högst 100 tecken.
* Varje `string` variabelvärdet måste vara mindre än 2 048 tecken.
* Varje `secretString` variabelvärdet type får vara högst 500 tecken.

## Via användargränssnittet i Cloud Manager {#ui}

Pipeline-variabler kan konfigureras och hanteras via användargränssnittet i Cloud Manager. Du måste ha behörighet att redigera pipelinen för att kunna lägga till, redigera och ta bort pipelinevariabler.

Om en pipeline körs blockeras variabelhanteringen.

### Lägga till pipeline-variabler {#add-ui}

1. När [hantera dina rörledningar,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) tryck eller klicka på ellipsknappen för den pipeline som du vill skapa pipelinevariabler för och välj **Visa/redigera variabler** på snabbmenyn.

   ![Visa/redigera pipeline-variabler](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. The **Variabelkonfiguration** öppnas. Ange variabeldetaljerna i den första raden i tabellen och tryck eller klicka på **Lägg till**.

   * **Konfigurationsnamn** är en unik identifierare för variabeln, som måste ha ett huvud [regler för att namnge rörliga variabler.](#naming-conventions)
   * **Värde** är värdet som finns i variabeln.
   * **Steget används** är steget i den pipeline som variabeln gäller för. Det krävs.
      * **Bygge**
      * **Funktionstestning**
      * **UI-testning**
   * **Typ** definierar om variabeln är oformaterad text eller krypterad som en hemlighet.

   ![Lägg till variabel](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. Tabellen läggs till i tabellen. Lägg till ytterligare variabler efter behov och tryck eller klicka **Spara** för att spara de variabler som du har lagt till i pipeline.

### Redigera rörledningsvariabler {#edit-ui}

1. När [hantera dina rörledningar,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) tryck eller klicka på ellipsknappen för den pipeline som du vill skapa pipelinevariabler för och välj **Visa/redigera variabler** på snabbmenyn.

   ![Visa/redigera pipeline-variabler](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. The **Variabelkonfiguration** öppnas. Tryck eller klicka på ellipsknappen för variabeln som du vill redigera och välj **Redigera**.

   ![Redigera variabel](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Uppdatera variabelvärdet efter behov och tryck eller klicka **Använd** (bockmarkeringen i slutet av raden) för att tillämpa ändringen eller **Ignorera** (bakåtpilen) om du vill återställa ändringen.

   * Endast variabelns värde kan redigeras.

   ![Redigera en variabel](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. Tryck eller klicka **Spara** om du vill spara de ändringar du har gjort i variablerna i pipeline.

Om du vill ta bort en variabel väljer du **Ta bort** i stället för **Redigera** på ellipsmenyn för rörledningsvariabeln i **Variabelkonfiguration** -fönstret.

## Använda Cloud Manager CLI {#cli}

Det här CLI-kommandot ställer in en variabel.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Det här kommandot listar variabler.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Vid användning i en Maven `pom.xml` är det praktiskt att mappa dessa variabler till Maven-egenskaper med en syntax som liknar den här.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```
