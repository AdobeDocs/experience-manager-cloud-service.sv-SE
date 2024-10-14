---
title: Pipeline-variabler i Cloud Manager
description: Lär dig hur du kan använda pipeline-variabler i Cloud Manager för att hantera specifika konfigurationsvariabler för ditt bygge.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Pipeline-variabler i Cloud Manager {#configuring-pipeline-variables}

Din byggprocess kan vara beroende av specifika konfigurationsvariabler som inte ska lagras i Git-databasen. Du kan också behöva justera dem mellan olika pipeline-körningar på samma gren. Med Cloud Manager kan du hantera de här inställningarna som pipeline-variabler.

## Om pipeline-variabler {#pipeline-variables}

Med Cloud Manager kan du konfigurera pipeline-variabler på flera olika sätt.

* [Använda Cloud Manager användargränssnitt](#ui)
* [Använda Cloud Manager CLI](#cli)
* [Använda Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

Variabler kan lagras som antingen oformaterad text eller krypteras i vila. I båda fallen görs variabler tillgängliga i byggmiljön som en miljövariabel, som sedan kan refereras inifrån filen `pom.xml` eller andra byggskript.

## Lägga till en pipeline-variabel via Cloud Manager {#ui}

Pipeline-variabler kan konfigureras och hanteras via Cloud Manager användargränssnitt. De hjälper till att effektivisera hanteringen av pipeline, särskilt när olika konfigurationer krävs i olika steg.

Du måste ha behörighet att redigera pipelinen för att lägga till, redigera och ta bort pipelinevariabler.

Om en pipeline körs blockeras variabelhanteringen.

**Så här lägger du till en pipeline-variabel via Cloud Manager:**

1. När du [hanterar dina pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) klickar du på ikonen ![Ellipsis - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för den pipeline som du vill skapa pipelinevariabler för.

1. Klicka på **Visa/redigera variabler** i listrutan.

   ![Visa/redigera pipeline-variabler](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Ange informationen på tabellens första rad i dialogrutan **Variablkonfiguration**.

   | Fält | Beskrivning |
   | --- | --- |
   | Namn | Ett unikt namn på konfigurationsvariabeln. Den identifierar den specifika variabeln som används i pipeline. Den måste följa följande namngivningskonventioner:<ul><li>Variabler får bara innehålla alfanumeriska tecken och understreck (`_`).</li><li>Namnen ska vara versaler.</li><li>Det finns en gräns på 200 variabler per pipeline.</li><li>Varje namn får innehålla högst 100 tecken.</li><li>Varje `string`-variabelvärde måste vara kortare än 2 048 tecken.</li><li>Varje `secretString`-typvariabelvärde måste vara högst 500 tecken.</li></ul> |
   | Värde | Värdet som variabeln innehåller. |
   | Steget används | Obligatoriskt. Det steg i pipeline som variabeln gäller för:<ul><li>**Build** - Variabeln används under byggprocessen.</li><li>**Funktionstestning** - Variabeln används under funktionstestningssteget.</li><li>**UI-testning** - Variabeln används under gränssnittstestningsfasen.</li></ul> |
   | Typ | Välj om variabeln är oformaterad text eller krypterad som en hemlighet. |

   ![Lägg till variabel](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. Klicka på **Lägg till**.

   Lägg till ytterligare variabler efter behov.

1. Klicka på **Spara**.

## Redigera en pipeline-variabel {#edit-ui}

1. När du [hanterar dina pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) klickar du på ikonen ![Ellipsis - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för den pipeline som du vill redigera pipelinevariabler för.

1. Klicka på **Visa/redigera variabler** i listrutan.

   ![Visa/redigera pipeline-variabler](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. I dialogrutan **Variabelkonfiguration** klickar du på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för variabeln som du vill ändra.

1. Klicka på **Redigera** i listrutan.

   ![Redigera variabel](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Uppdatera värdet för variabeln efter behov.

   Endast variabelns värde kan ändras.

1. Gör något av följande:

   * Klicka på ![Använd - bockmarkeringsikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) för att tillämpa ändringen.
   * Klicka på ![Ångra-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg) om du vill ångra ändringen.

1. Klicka på **Spara**.


## Ta bort en pipeline-variabel {#delete-ui}

1. När du [hanterar dina pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) klickar du på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för den pipeline som du vill ta bort pipelinevariabler för.

1. Klicka på **Visa/redigera variabler** i listrutan.

   ![Visa/redigera pipeline-variabler](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. I dialogrutan **Variabelkonfiguration** klickar du på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för variabeln som du vill ta bort och sedan på **Ta bort**.

## Ange pipeline-variabler med Cloud Manager CLI {#cli}

Det här kommandot i CLI (Command Line Interface) anger en variabel.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Det här kommandot listar variabler.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

När den används i en Maven `pom.xml`-fil är det ofta användbart att länka dessa variabler till Maven-egenskaper med en syntax som liknar den i följande exempel:

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
