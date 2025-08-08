---
title: Skapa miljöer
description: Lär dig hur du använder Cloud Manager för att skapa dina första miljöer.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
feature: Onboarding
source-git-commit: 9c5838a01ceecf094aea19578e6560a5e5ca8c4c
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Skapa miljöer {#create-environments}

I den här delen av [introduktionsresan](overview.md) får du lära dig hur du använder Cloud Manager för att skapa dina första miljöer.

## Syfte {#objective}

När du har läst det föregående dokumentet på den här introduktionsresan, [Skapa program](create-program.md), har du nu ett eget Cloud Manager-program. Nu kan du lära dig hur du använder Cloud Manager för att skapa din första miljö för det programmet.

När du har läst det här dokumentet kommer du att:

* Förstå vad en miljö är.
* Se skillnaden mellan olika miljöer.
* Skapa en egen miljö.

## Vad är en miljö? {#environments}

Miljöer finns nedan i Cloud Manager hierarki. Även om man med ett program kan organisera en lösning och ge vissa medarbetare åtkomst till dessa program, tillhör miljöerna specifika program och är enskilda instanser av Adobe-lösningar inom dessa program. Miljöer används för ett specifikt ändamål, t.ex. att skapa innehåll eller testa ny utveckling. Cloud Manager CI/CD-pipelines underlättar distribution av kod till dessa miljöer från Git-databaser.

Om ni minns exemplet med WKND Travel och Adventure Enterprises, är de en hyresgäst som fokuserar på reserelaterade medier. De kan ha två program. Det vill säga ett Sites-program för divisionen WKND Magazine och ett Assets-program för divisionen WKND Media. Varje program skulle förmodligen ha ett par miljöer, till exempel en produktionsmiljö som betjänar den faktiska trafiken på platsen och en utvecklingsmiljö för att testa ny programkod.

Det finns fem olika typer av miljöer:

* **Produktion och scen** - Produktions- och stagningsmiljöerna är tillgängliga som par och används för produktions- respektive testningsändamål.
* **Utveckling** - En utvecklingsmiljö kan skapas för utvecklings- och testningssyften och kan endast associeras med icke-produktionspipelines.
* **Snabb utveckling** - Med en snabb utvecklingsmiljö kan utvecklare snabbt distribuera och granska ändringar. Det minimerar tiden för att testa funktioner som är beprövade i en lokal utvecklingsmiljö.
* **Specialiserad testmiljö** - Tillhandahåller ett dedikerat utrymme för att validera funktioner under nära produktionsförhållanden, vilket är idealiskt för stresstestning och avancerade kontroller före driftsättning.

För att du ska komma igång med en minimal introduktionsresa skapar du en utvecklingsmiljö som du kan använda för att utforska AEM as a Cloud Service funktioner.

## Skapa en miljö {#creating-environments}

>[!NOTE]
>
>Systemet registrerar användaren som skapar en miljö som skapare. Eftersom borttagna användare ibland kan återställas bör du noga välja den som skapat miljön.

**Så här skapar du en miljö:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj det program som du vill lägga till en miljö för.

1. Om du vill lägga till en miljö väljer du alternativet **Lägg till miljö** på sidan **Programöversikt** på **miljökortet**.

   ![Miljökort](/help/implementing/cloud-manager/assets/no-environments.png)

   * Alternativet **Lägg till miljö** är också tillgängligt på fliken **Miljö**.

     ![Fliken Miljö](/help/implementing/cloud-manager/assets/environments-tab.png)

   * Alternativet **Lägg till miljö** kan vara inaktiverat på grund av bristande behörighet eller beroende på de licensierade resurserna.

1. Gör följande i dialogrutan **Lägg till miljö**:

   * Välj en **miljötyp**.
      * Antalet tillgängliga/använda miljöer visas inom parentes bakom typen av utvecklingsmiljö.
   * Ange ett **miljönamn**.
   * Ange en **miljöbeskrivning**.
   * Välj en **molnregion**.

   ![Dialogrutan Lägg till miljö](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Klicka på **Spara** för att lägga till den angivna miljön.

När miljön är tillgänglig kan medlemmar i din organisation som har tilldelats produktprofilen **Utvecklare** logga in på Cloud Manager och hantera Cloud Manager Git-databaser.

## Vad kommer härnäst? {#whats-next}

Nu när du har läst den här delen av introduktionsresan bör du:

* Förstå vad en miljö är.
* Se skillnaden mellan olika miljöer.
* Skapa en egen miljö.

Teamet har nu tillgång till de molnresurser som du har skapat. Som systemadministratör måste du först tilldela teammedlemmar till produktprofiler i AEM as a Cloud Service från Adobe Admin Console så att de kan komma åt dessa resurser.

Därför bör du fortsätta din introduktionsresa genom att gå igenom dokumentet [Tilldela teammedlemmar till AEM as a Cloud Service produktprofiler](assign-profiles-aem.md) nästa gång. I det dokumentet får du lära dig att ge teammedlemmarna rätt till dina nya miljöer.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md) - Lär dig mer om de typer av miljöer som du kan skapa och hur du skapar dem för ditt Cloud Manager-projekt
* [Använda Adobe Cloud Manager - miljöer](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/cloud-manager/environments) - Cloud Manager-miljöer består av AEM redigerings-, publicerings- och Dispatcher-tjänster. Lär dig hur olika miljöer stöder roller och kan användas med olika CI/CD-ledningar.
* [Snabba utvecklingsmiljöer](/help/implementing/developing/introduction/rapid-development-environments.md) - I den här dokumentationen finns mer information om hur du använder en RDE
<!-- ERROR: Not Found (HTTP error 404) FIND AN ALTERNATE RESOURCE? * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

