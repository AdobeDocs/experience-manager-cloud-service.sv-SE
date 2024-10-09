---
title: Konfigurera pipeline-variabler
description: Lär dig hur du kan använda pipeline-variabler i Cloud Manager för att hantera specifika konfigurationsvariabler för ditt bygge.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Konfigurera pipeline-variabler {#configuring-pipeline-variables}

Din byggprocess kan vara beroende av specifika konfigurationsvariabler som skulle vara olämpliga att placera i Git-databasen, eller så måste du variera dem mellan pipeline-körningar som använder samma gren. Med Cloud Manager kan du hantera dessa data som pipeline-variabler.

## Pipeline-variabler {#pipeline-variables}

Med Cloud Manager kan du konfigurera pipeline-variabler på flera olika sätt.

* [Via användargränssnittet i Cloud Manager](#ui)
* [Använda Cloud Manager CLI](#cli)
* [Använda Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

Variabler kan lagras som antingen oformaterad text eller krypteras i vila. I båda fallen görs variabler tillgängliga i byggmiljön som en miljövariabel som sedan kan refereras inifrån filen `pom.xml` eller andra byggskript.

### Variabelnamnkonventioner för pipeline {#naming-conventions}

Variabelnamn måste följa följande konventioner:

* Variabler får bara innehålla alfanumeriska tecken och understreck (`_`).
* Namnen ska vara versaler.
* Det finns en gräns på 200 variabler per pipeline.
* Varje namn får innehålla högst 100 tecken.
* Varje `string`-variabelvärde måste vara kortare än 2 048 tecken.
* Varje `secretString`-typvariabelvärde måste vara högst 500 tecken.

## Via Cloud Manager användargränssnitt {#ui}

Pipeline-variabler kan konfigureras och hanteras via Cloud Manager användargränssnitt. Du måste ha behörighet att redigera pipelinen för att lägga till, redigera och ta bort pipelinevariabler.

Om en pipeline körs blockeras variabelhanteringen.

### Lägg till pipeline-variabler {#add-ui}

1. När du [hanterar dina pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) klickar du på ellipsknappen för den pipeline som du vill skapa pipeline-variabler för och väljer **Visa/redigera variabler** på snabbmenyn.

   ![Visa/redigera pipeline-variabler](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Fönstret **Variabelkonfiguration** öppnas. Ange variabelinformationen i den första raden i tabellen och klicka på **Lägg till**.

   * **Konfigurationsnamn** är en unik identifierare för variabeln, som måste ha huvudnamnet [för regler för namn på pipelinevariabler](#naming-conventions).
   * **Värde** är det värde som variabeln innehåller.
   * **Steg som används** är det steg i pipeline som variabeln gäller för. Det krävs.
      * **Bygg**
      * **Funktionstestning**
      * **UI-testning**
   * **Type** definierar om variabeln är oformaterad text eller krypterad som en hemlighet.

   ![Lägg till variabel](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. Tabellen läggs till i tabellen. Lägg till ytterligare variabler efter behov och tryck eller klicka sedan på **Spara** för att spara de variabler du lade till i pipeline.

### Redigera rörledningsvariabler {#edit-ui}

1. När du [hanterar dina pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) klickar du på ellipsknappen för den pipeline som du vill skapa pipeline-variabler för och väljer **Visa/redigera variabler** på snabbmenyn.

   ![Visa/redigera pipeline-variabler](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Fönstret **Variabelkonfiguration** öppnas. Klicka på ellipsknappen för variabeln som du vill redigera och välj **Redigera**.

   ![Redigera variabel](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Uppdatera värdet för variabeln efter behov och klicka på **Använd** (bockmarkeringen i slutet av raden) för att tillämpa ändringen eller **Ignorera** (bakåtpilen) för att återställa ändringen.

   * Endast variabelns värde kan redigeras.

   ![Redigera en variabel](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. Klicka på **Spara**.

Om du vill ta bort en variabel väljer du **Ta bort** i stället för **Redigera** på ellipsmenyn för pipelinevariabeln i fönstret **Variabelkonfiguration**.

## Använda Cloud Manager CLI {#cli}

Det här CLI-kommandot ställer in en variabel.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Det här kommandot listar variabler.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

När de används i en Maven `pom.xml`-fil är det oftast bra att mappa dessa variabler till Maven-egenskaper med en syntax som liknar den här.

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
