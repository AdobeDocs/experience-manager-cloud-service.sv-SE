---
title: Skapa miljöer
description: Lär dig hur du använder Cloud Manager för att skapa dina första miljöer.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 5c5db0d133adfbbb678930ef27d8ade10fd0c3be
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Skapa miljöer {#create-environments}

I den här delen av [startresan,](overview.md) du får lära dig hur du använder Cloud Manager för att skapa dina första miljöer.

## Syfte {#objective}

Efter att ha läst det föregående dokumentet under den här introduktionsresan, [Skapa program,](create-program.md) har du nu ett eget Cloud Manager-program. Nu kan du lära dig hur du använder Cloud Manager för att skapa dina första miljöer för det programmet.

När du har läst det här dokumentet kommer du att:

* Förstå vad en miljö är.
* Se skillnaden mellan de olika miljöerna.
* Skapa en egen miljö.

## Vad är en miljö? {#environments}

Miljöer finns under program i Cloud Managers hierarki. Med program kan du organisera din lösning och ge vissa teammedlemmar tillgång till dessa program, men miljöer tillhör specifika program och är enskilda instanser av Adobe-lösningar inom dessa program. Miljöer används för ett specifikt ändamål, t.ex. att skapa innehåll eller testa ny utveckling. Cloud Managers pipelines för CI/CD underlättar distributionen av kod till dessa miljöer från Git-databaser.

Om du kommer ihåg exemplet med WKND Travel and Adventure Enterprises, som är en hyresgäst som fokuserar på reserelaterade medier, kan de ha två program: ett Sites-program för divisionen WKND Magazine och ett Assets-program för divisionen WKND Media. Varje program skulle förmodligen ha ett par miljöer, till exempel en produktionsmiljö som betjänar den faktiska trafiken på platsen och en utvecklingsmiljö för att testa ny programkod.

Det finns fyra olika typer av miljöer:

* **Produktion och fas** - Produktions- och testmiljöer finns som par och används för produktions- respektive testningsändamål.
* **Utveckling** - En utvecklingsmiljö kan skapas för såväl utvecklings- som testningsändamål och kan endast kopplas till rörledningar som inte är avsedda för produktion.
* **Snabb utveckling** - Med en snabb utvecklingsmiljö (RDE) kan utvecklare snabbt driftsätta och granska ändringar, vilket minimerar den tid som krävs för att testa funktioner som är beprövade i en lokal utvecklingsmiljö.

För den här introduktionsresan kommer du att skapa en utvecklingsmiljö som du kan använda för att utforska AEM as a Cloud Service funktioner.

## Skapa miljöer {#creating-environments}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program som du vill lägga till en miljö för.

1. Från **Programöversikt** sida, klicka på **Lägg till miljö** på **Miljö** för att lägga till en miljö.

   ![Miljökort](/help/implementing/cloud-manager/assets/no-environments.png)

   * The **Lägg till miljö** finns även på **Miljö** -fliken.

      ![Fliken Miljö](/help/implementing/cloud-manager/assets/environments-tab.png)

   * The **Lägg till miljö** kan vara inaktiverat på grund av bristande behörighet eller beroende på vilka licensierade resurser som används.

1. I **Lägg till miljö** som visas:

   * Välj en **Miljötyp**.
      * Antalet tillgängliga/använda miljöer visas inom parentes bakom typen av utvecklingsmiljö.
   * Ange en **Miljönamn**.
   * Ange en **Miljöbeskrivning**.
   * Välj en **Molnregion**.

   ![Dialogrutan Lägg till miljö](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Klicka **Spara** för att lägga till den angivna miljön.

När miljön är tillgänglig tilldelas medlemmar i organisationen **Utvecklare** produktprofilen kan logga in på Cloud Manager och hantera Cloud Manager Git-databaser.

## What’s Next {#whats-next}

Nu när du har läst den här delen av introduktionsresan bör du:

* Förstå vad en miljö är.
* Se skillnaden mellan de olika miljöerna.
* Skapa en egen miljö.

Dina molnresurser har skapats och är tillgängliga för ditt team. Som systemadministratör måste du först tilldela teammedlemmar till AEM as a Cloud Service produktprofiler från Adobe Admin Console för att de ska kunna komma åt dessa resurser.

Därför bör du fortsätta din introduktionsresa genom att granska dokumentet nästa gång [Tilldela teammedlemmar AEM as a Cloud Service produktprofiler.](assign-profiles-aem.md)  I det dokumentet får du lära dig att ge teammedlemmarna de rättigheter de behöver för att få tillgång till dina nya miljöer.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md) - Lär dig mer om vilka typer av miljöer du kan skapa och hur du skapar dem för ditt Cloud Manager-projekt
* [Använda Adobe Cloud Manager - miljöer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Cloud Manager-miljöer består av AEM tjänster för redigering, publicering och utskickning. Lär dig hur olika miljöer stöder roller och kan användas med olika CI/CD-pipeline.
* [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - I den här videon visas en översikt över olika miljötyper i Cloud Manager från en AEM.
* [Snabba utvecklingsmiljöer](/help/implementing/developing/introduction/rapid-development-environments.md) - Läs den här dokumentationen för mer information om hur du använder en RDE
