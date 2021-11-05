---
title: Konfigurera icke-produktionsförlopp
description: Följ den här sidan om du vill veta mer om hur du konfigurerar en icke-produktionspipeline i Cloud Manager
index: true
source-git-commit: 2ac65af4cf410491d1196b9e20f67647e0a1b4d1
workflow-type: tm+mt
source-wordcount: '559'
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

   Du kan definiera följande distributionsutlösare för att starta pipelinen.

   * **Manuell** - med användargränssnittet startar du pipelinen manuellt.
   * **Vid Git-ändringar** - startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

      Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

      Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:
   Du kan definiera det viktiga felmåttets beteende för att starta pipelinen.

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. Välj **[Full Stack-kod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** eller **[Front End-kod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**.

   Om du valde **Front End-kod** måste du välja **Databas**, **Git-gren** och **Kodplats**, vilket visas i figuren nedan:

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   Om du valde **Full Stack-kod** måste du välja **Databas** och **Git-gren**, vilket visas i figuren:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack1.png)

   >[!IMPORTANT]
   >Om det redan finns en pipeline med fullständig stackkod för den valda miljön inaktiveras det här valet.

   >[!NOTE]
   >Innan du börjar konfigurera frontledningarna finns mer information i [AEM för att skapa webbplatser snabbt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) för ett komplett arbetsflöde med det lättanvända AEM för att skapa en webbplats. På den här dokumentationswebbplatsen kan du effektivisera utvecklingen av AEM och snabbt anpassa webbplatsen utan AEM kunskaper om bakomliggande funktioner.

1. Den nyligen skapade icke-produktionsflödet visas nu i **Pipelines** kort.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack2.png)


   Rörledningen visas på kortet på startskärmen med fyra åtgärder, vilket visas nedan:

   * **Lägg till** - gör det möjligt att lägga till en ny pipeline.
   * **Visa alla** - gör att användaren kan se alla rörledningar.
   * **Åtkomst till svarsinformation** - ger användaren tillgång till den information som krävs för att få åtkomst till Git-databasen i Cloud Manager.
   * **Läs mer** - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.