---
title: Konfigurera icke-produktionsförlopp
description: Följ den här sidan om du vill veta mer om hur du konfigurerar en icke-produktionspipeline i Cloud Manager
index: true
source-git-commit: d090329c46155d77a7b132583c777c09555a03c9
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Konfigurera icke-produktionsförlopp {#configure-non-production-pipeline}

Förutom den huvudsakliga rörledningen som distribuerar till scenen och produktionen kan kunderna även lägga upp ytterligare rörledningar, så kallade icke-produktionsrörledningar.

Det finns två typer av icke-produktionsrörledningar:

1. Kodkvalitet: Kör kodkvalitetsgenomsökningar på koden i en Git-gren. Detta tillvägagångssätt utför stegen för bygg- och kodkvalitet.
1. Distribution: Förutom att utföra stegen för bygg- och kodkvalitet distribuerar den här pipelinen koden till den valda icke-produktionen till AEM as a Cloud Service miljön.

## Lägga till en ny icke-produktionspipeline {#adding-non-production-pipeline}

På startskärmen visas dessa rörledningar i ett nytt kort:

1. Öppna **Pipelines** från startskärmen i Cloud Manager. Klicka på **+Lägg till** och markera **Lägg till icke-produktionsförlopp**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Lägg till icke-produktionsförlopp**  visas. Välj den typ av pipeline som du vill skapa, antingen **Kodkvalitetspipeline** eller **Distributionsförlopp**.

   >[!NOTE]
   >För distributionspipelines måste du välja distributionsmiljö.

   Dessutom kan du konfigurera **Utlösare för distribution** och **Beteende vid viktiga måttfel** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. Välj **[Full Stack-kod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** eller **[Front End-kod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**. Du kan välja **Databas** och **Git-gren**. Klicka på **Spara**.

   >[!IMPORTANT]
   >Om det redan finns en pipeline med fullständig stackkod för den valda miljön inaktiveras det här valet.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   >[!NOTE]
   >Innan du börjar konfigurera frontledningarna finns mer information i [AEM för att skapa webbplatser snabbt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) för ett komplett arbetsflöde med det lättanvända AEM för att skapa en webbplats. På den här dokumentationswebbplatsen kan du effektivisera utvecklingen av AEM och snabbt anpassa webbplatsen utan AEM kunskaper om bakomliggande funktioner.

1. Den nyligen skapade icke-produktionsflödet visas nu i **Pipelines** kort.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   Rörledningen visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   * **Lägg till** - gör det möjligt att lägga till en ny pipeline.
   * **Åtkomst till svarsinformation** - ger användaren tillgång till den information som krävs för att få åtkomst till Git-databasen i Cloud Manager.
   * **Läs mer** - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.