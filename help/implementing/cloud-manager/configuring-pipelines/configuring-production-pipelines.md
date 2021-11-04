---
title: Konfigurera produktionsförlopp
description: Konfigurera produktionsförlopp
index: true
source-git-commit: 8bdc246d1f47e1bdc9a217588f0be69a09982be5
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Konfigurera en produktionspipeline {#configure-production-pipeline}

Distributionshanteraren ansvarar för att konfigurera produktionsförloppet.

>[!NOTE]
>Det går inte att konfigurera en produktionspipeline förrän ett program har skapats, Git-databasen har minst en gren och en Production- och Stage-miljöuppsättning har skapats.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>Du kan ändra pipeline-inställningarna efter den första konfigurationen.

## Lägga till en ny produktionspipeline {#adding-production-pipeline}

När du har konfigurerat programmet och har minst en miljö som använder [!UICONTROL Cloud Manager] UI, du är redo att lägga till en produktionspipeline.

Så här konfigurerar du beteendet och inställningarna för produktionsflödet:

1. Navigera till **Pipelines** från **Programöversikt** sida.
Klicka på **+Lägg till** och markera **Lägg till produktionspipeline**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Lägg till produktionspipeline** visas. Ange pipelinenamnet.

   Dessutom kan du konfigurera **Utlösare för distribution** och **Beteende vid viktiga måttfel** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Du kan definiera distributionsutlösarna för att starta pipelinen.

   * **Manuell** - med användargränssnittet startar du pipelinen manuellt.
   * **Vid Git-ändringar** - startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

      Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

      Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:
   Du kan definiera det viktiga felmåttets beteende för att starta pipelinen.

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. The **Lägg till produktionspipeline** innehåller en andra flik med etiketten **Källkod**. Du kan antingen välja **[Front End-kod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)** eller **[Full Stack-kod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   Om du valde **Front End-kod** måste du välja **Databas**, **Git-gren** och **Kodplats**, vilket visas i figuren nedan:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   Om du valde **Full Stack-kod** måste du välja **Databas**, **Git-gren** och **Alternativ för produktionsdistribution** (detaljer nedan), enligt bilden:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack2.png)

   **Alternativ för produktionsdistribution:**

   * **Pausa före distribution till produktion**: Med det här alternativet kan distributionen pausa före produktionen.
   * **Schemalagd**: Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

   >[!IMPORTANT]
   >Om det redan finns en pipeline med fullständig stackkod för den valda miljön inaktiveras det här valet.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/full-stack-disabled.png)

   >[!NOTE]
   >Innan du börjar konfigurera frontledningarna finns mer information i [AEM för att skapa webbplatser snabbt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) för ett komplett arbetsflöde med det lättanvända AEM för att skapa en webbplats. På den här dokumentationswebbplatsen kan du effektivisera utvecklingen av AEM och snabbt anpassa webbplatsen utan AEM kunskaper om bakomliggande funktioner.

1. Klicka på **Fortsätt** när du har valt alternativ i **Källkod** -fliken.

1. The **Lägg till produktionspipeline** innehåller en tredje flik med etiketten **Experience Audit**. Det här alternativet innehåller en tabell för de URL-sökvägar som alltid ska inkluderas i Experience Audit.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >Du måste klicka på **Lägg till sida** för att definiera en egen länk. Sidsökvägen måste börja med `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   Klicka **Lägg till ny sida** för att ange en URL-sökväg som ska inkluderas i Experience Audit.

   Om du till exempel vill inkludera `https://wknd.site/us/en/about-us.html` Ange sökvägen i Experience Audit `/us/en/about-us.html` i det här fältet och klicka **Spara**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   Den URL som visas i tabellen är:

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   Högst 25 rader kan inkluderas. Om användaren inte har skickat in några sidor i det här avsnittet, kommer webbplatsens hemsida som standard att inkluderas i Experience Audit.

   Se [Upplevelsegranskningsresultat](/help/implementing/cloud-manager/experience-audit-testing.md) för mer information.

   >[!NOTE]
   > De konfigurerade sidorna skickas till tjänsten och utvärderas utifrån prestanda, tillgänglighet, SEO (Search Engine Optimization), bästa praxis och PWA (Progressive Web App)-tester.

1. Klicka på **Spara**. Produktionspipelinen som skapades visas nu i **Pipelines** kort.

   Rörledningen visas på kortet på startskärmen med fyra åtgärder, vilket visas nedan:

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-created.png)

   * **Lägg till** - gör det möjligt att lägga till en ny pipeline.
   * **Visa alla** - gör att användaren kan se alla rörledningar.
   * **Åtkomst till svarsinformation** - ger användaren tillgång till den information som krävs för att få åtkomst till Git-databasen i Cloud Manager.
   * **Läs mer** - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.


