---
title: Lägg till en Edge Delivery Pipeline
description: Lär dig hur du lägger till en Edge Delivery-pipeline för att bygga och driftsätta din kod i produktionsmiljöer.
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Privat beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---



# Lägg till en Edge Delivery-pipeline {#configure-production-pipeline}

Lär dig hur du konfigurerar Edge Delivery-pipelines för att bygga och driftsätta din kod i produktionsmiljöer. En produktionspipeline distribuerar kod först till scenmiljön. Vid godkännande distribueras samma kod till produktionsmiljön.

En användare måste ha rollen **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** för att kunna konfigurera produktionspipelines.

>[!NOTE]
>
>Det går inte att konfigurera en produktionspipeline förrän följande har inträffat:
>
>* Programmet skapas.
>* Git-databasen har minst en gren.
>* Produktions- och mellanlagringsmiljöerna skapas.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

## Lägg till en ny Edge Delivery-pipeline {#adding-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med användargränssnittet för [!UICONTROL Cloud Manager] kan du lägga till en produktionspipeline genom att följa de här stegen.

>[!TIP]
>
>Innan du konfigurerar en pipeline för framtagning bör du läsa [AEM Quick Site Creation Journey](/help/journey-sites/quick-site/overview.md) för att få en heltäckande guide med det lättanvända verktyget AEM Quick Site Creation. Den här resan kan hjälpa er att effektivisera framtidens utveckling av er AEM-webbplats, så att ni snabbt kan anpassa er webbplats utan kunskaper om AEM bakomliggande system.

**Så här lägger du till en ny Edge Delivery-pipeline:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på **Lägg till** för att välja **Lägg till produktionspipeline**.

   ![Rörledningskortet i programhanteraren - översikt](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Dialogrutan **Lägg till produktionspipeline** visas. Ange ett **Pipelinenamn** som identifierar din pipeline tillsammans med följande alternativ. Klicka på **Fortsätt**.

   **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

   * **Manuell** - Starta pipelinen manuellt.
   * **Vid Git-ändringar** - Startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

   **Beteende vid viktiga måttfel** - Under pipeline-konfiguration eller redigering kan **Distributionshanteraren** definiera pipelinens beteende när ett viktigt fel påträffas i någon av kvalitetsportarna. De tillgängliga alternativen är:

   * **Fråga varje gång** - Standardinställning. Det kräver manuell åtgärd vid varje viktigt fel.
   * **Misslyckades omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Den här processen emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipelinen automatiskt när ett viktigt fel inträffar. Den här processen emulerar i princip en användare som manuellt godkänner varje fel.

   ![Konfiguration av produktionspipeline](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. På fliken **Source Code** väljer du vilken typ av kod som pipeline ska bearbeta.

   * **[Konfigurera en fullständig stackkodspipeline](#full-stack-code)**
   * **[Konfigurera en riktad distributionsprocess](#targeted-deployment)**

Mer information om olika typer av pipelines finns i [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Stegen för att slutföra skapandet av produktionsflödet varierar beroende på vilken typ av källkod du har valt. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet så att du kan slutföra konfigurationen av din pipeline.

