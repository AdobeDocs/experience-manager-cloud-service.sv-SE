---
title: Distribuera koden
description: Lär dig hur du distribuerar kod med Cloud Manager-pipelines i AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2aea79d42ef9627a8fc758077a7ee012592888d7
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---


# Distribuera koden {#deploy-your-code}

Lär dig hur du distribuerar koden till Production med Cloud Manager-pipelines i AEM as a Cloud Service.

![Produktionspipeline-diagram](./assets/configure-pipeline/production-pipeline-diagram.png)

Distribuera kod sömlöst till scenen och sedan till produktionen via en produktionsprocess. Körningen av produktionsflödet delas upp i två logiska faser:

1. **Distribution till scenmiljö** - Koden byggs och distribueras till scenmiljön för automatisk funktionstestning, gränssnittstestning, upplevelsegranskning och UAT (User Acceptance Testing).
1. **Distribution till produktionsmiljö** - När bygget har validerats på scenen och godkänts för befordran till produktion distribueras samma byggartefakt till produktionsmiljön.

_Det är bara pipeline-typen Full Stack Code som har stöd för kodskanning, funktionstestning, gränssnittstestning och granskning av upplevelser._

## Distributionsprocess {#deployment-process}

Alla Cloud Service-installationer följer en rullande process för att säkerställa noll driftavbrott. Mer information finns i [Hur rullande distributioner fungerar](/help/implementing/deploying/overview.md#how-rolling-deployments-work).

>[!NOTE]
>
>Dispatcher-cachen rensas bort vid varje distribution. Därefter&quot;värms&quot; det upp&quot; innan de nya publiceringsnoderna tar emot trafik.

## Distribuera koden med Cloud Manager i AEM as a Cloud Service {#deploying-code-with-cloud-manager}

När du har [konfigurerat produktionsflödet](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md), inklusive databas-, miljö- och testmiljön, är du redo att distribuera koden.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på det program som du vill distribuera kod för.

1. Klicka på **Distribuera** i call-to-action-området på sidan **Översikt**.

   ![CTA](assets/deploy-code1.png)

1. Klicka på **Skapa** på sidan **Distribuera till produktion**.

   ![Körningsskärm för pipeline](assets/deploy-code2.png)

Byggprocessen distribuerar koden genom följande tre ordnade faser:

1. [Scendistributionsfas](#stage-deployment)
1. [Scentestningsfas](#stage-testing)
1. [Produktionsdistributionsfas](#production-deployment)

>[!TIP]
>
>Du kan granska stegen från olika distributionsprocesser genom att visa loggar eller granska resultaten för testvillkoren.

### Scendistributionsfas {#stage-deployment}

Fas **Scendistribution** omfattar följande steg:

| Steg för driftsättning | Beskrivning |
| --- | --- |
| Validering | Ser till att pipeline är konfigurerad att använda de tillgängliga resurserna. Du kan till exempel testa att den konfigurerade grenen finns och att miljöerna är tillgängliga. |
| Build &amp; Unit Testing | Kör en innesluten byggprocess.<br>Mer information om byggmiljön finns i [Information om byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). |
| Kodskanning | Utvärderar kvaliteten på programkoden.<br>Mer information om testprocessen finns i [Testa kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md). |
| Skapa bilder | Den här processen konverterar innehåll och Dispatcher-paket från Build-steget till Docker-bilder. Det genererar även Kubernetes-konfigurationer baserade på dessa paket. |
| Distribuera till scenen | Bilden distribueras till mellanlagringsmiljön som förberedelse för [scentestningsfasen](#stage-testing). |

![Scendistribution](assets/stage-deployment.png)

### Scentestningsfas {#stage-testing}

Fas **Scentestning** omfattar följande steg:

| Steg för testning | Beskrivning |
| --- | --- |
| Funktionstestning av produkten | Cloud Manager pipeline kör tester som körs mot scenmiljön.<br>Se även [Funktionstestning av produkter](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing). |
| Anpassad funktionstestning | Det här steget i pipeline körs alltid och kan inte hoppas över. Om bygget inte skapar en JAR-test godkänns testet automatiskt.<br>Se även [Anpassad funktionstestning](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing). |
| Anpassade gränssnittstestningar | En valfri funktion som automatiskt kör gränssnittstester som skapats för anpassade program.<br>Gränssnittstester är självstudiebaserade och paketerade i en Docker-bild för att ge flexibilitet vad gäller språk och ramverk. Med den här metoden kan du använda Java och Maven, Node och WebDriver.io eller valfritt Selenium-baserat ramverk eller teknik.<br>Se även [Anpassad gränssnittstestning](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing). |
| Experience Audit | Det här steget i pipeline körs alltid och kan inte hoppas över. När en produktionsprocess körs inkluderas ett steg för upplevelsegranskning efter anpassad funktionstestning som kör kontrollerna.<ul><li>De konfigurerade sidorna skickas till tjänsten och utvärderas.</li><li>Resultaten är informativa och visar poängen och förändringen mellan aktuella och tidigare poäng.</li><li>Den här insikten är värdefull för att avgöra om det finns en regression som introduceras i den aktuella distributionen.</li></ul>Se [Om Experience Audit-resultat](/help/implementing/cloud-manager/reports/report-experience-audit.md).</li></ul> |

![Scentestning](assets/stage-testing.png)

### Produktionsdistributionsfas {#production-deployment}

Processen för att distribuera till produktionstopologier skiljer sig något för att minimera effekten för besökare på en AEM-webbplats.

Produktionsinstallationer följer i allmänhet samma steg som tidigare, men på ett rullande sätt. Följande steg ingår:

1. Distribuera AEM-paket till författaren.
1. Koppla loss `dispatcher1` från belastningsutjämnaren.
1. Distribuera AEM-paket till `publish1` och Dispatcher-paketet till `dispatcher1`, rensa Dispatcher-cachen.
1. Placera `dispatcher1` i belastningsutjämnaren igen.
1. Koppla loss `dispatcher1` från belastningsutjämnaren när `dispatcher2` är tillbaka i tjänsten.
1. Distribuera AEM-paket till `publish2` och Dispatcher-paketet till `dispatcher2`, rensa Dispatcher-cachen.
1. Placera `dispatcher2` i belastningsutjämnaren igen.

Den här processen fortsätter tills distributionen har nått alla utgivare och utgivare i topologin.

![Produktionsdistributionsfas](assets/production-deployment.png)

## Timeout under distribution {#timeouts}

Följande steg gör en timeout om de lämnas kvar och väntar på användarfeedback under en distribution:

| Steg | Timeout |
|--- |--- |
| Testning av kodkvalitet | 14 dagar |
| Säkerhetstestning | 14 dagar |
| Prestandatestning | 14 dagar |
| Ansökan om godkännande | 14 dagar |
| Schemalägg produktionsdistribution | 14 dagar |
| Stöd för CSE | 14 dagar |

## Kör en produktionsdistribution igen {#reexecute-deployment}

I sällsynta fall kan produktionsdistributionsstegen misslyckas av tillfälliga orsaker. I sådana fall stöds omkörning av produktionsdistributionssteget så länge produktionsdistributionssteget har slutförts, oavsett typ av slutförande (till exempel annullerat eller misslyckat). Omkörning skapar en ny körning med samma pipeline som består av följande tre steg:

1. **Validering** - Samma validering som sker under en normal pipeline-körning.
1. **Build** - I samband med en omkörning kopierar byggsteget artefakter och kör inte någon ny byggprocess.
1. **Produktionsdistribution** - Använder samma konfiguration och alternativ som produktionsdistributionssteget i en normal pipeline-körning.

I sådana fall där en omkörning är möjlig visas statussidan för produktionsflödet med alternativet **Kör om** bredvid det vanliga alternativet **Hämta bygglogg**.

![Alternativet Kör igen i översiktsfönstret för pipeline](assets/re-execute.png)

>[!NOTE]
>
>I en omkörning markeras byggsteget i användargränssnittet för att reflektera att det är kopieringsartefakter och inte återskapande.

### Användningsinformation {#usage-notes}

* Det går bara att köra produktionsdistributionssteget på nytt för den senaste körningen.
* Omkörning är inte tillgängligt för push-uppdateringskörningar. Om den senaste körningen är en push-uppdateringskörning går det inte att utföra om.
* Om den senaste körningen misslyckades någon gång före produktionsdistributionssteget går det inte att utföra om.

### Kör om API {#reexecute-API}

Förutom att vara tillgänglig i användargränssnittet kan du använda [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) för att utlösa omkörningar och identifiera körningar som utlösts som omkörningar.

#### Utlösa en omkörning {#reexecute-deployment-api}

Om du vill utlösa en omkörning gör du en PUT-begäran till HAL Link `https://ns.adobe.com/adobecloud/rel/pipeline/reExecute` i produktionsdistributionstillståndet.

* Om den här länken finns kan körningen startas om från det steget.
* Om den inte finns kan inte körningen startas om från det steget.

Den här länken är bara tillgänglig för produktionsdistributionssteget.

```JavaScript
 {
  "_links": {
    "https://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```

Syntaxen för HAL-länkens href-värde är bara ett exempel. Det faktiska värdet ska alltid läsas från HAL-länken och inte genereras.

Om en PUT-begäran skickas till den här slutpunkten genereras ett 201-svar om det lyckas, och svarsbrödtexten är representationen av den nya körningen. Det här arbetsflödet liknar att starta en vanlig körning via API:t.

#### Identifiera en körning på nytt {#identify-reexecution}

Systemet identifierar omkörningar genom att ställa in fältet `trigger` på värdet `RE_EXECUTE`.
