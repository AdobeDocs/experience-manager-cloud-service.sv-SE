---
title: Skapa ett program
description: Lär dig hur du använder Cloud Manager för att skapa ditt första program.
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: 77ae5d79ecb8a11a230cee461f247ffe0e9891a5
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Skapa ett program {#create-program}

I den här delen av [startresan,](overview.md) du får lära dig hur du använder Cloud Manager för att skapa ditt första program.

## Syfte {#objective}

Efter att ha granskat det föregående dokumentet under den här introduktionsresan, [Access Cloud Manager,](cloud-manager.md) du har sett till att du har tillgång till Cloud Manager. Nu kan du skapa ditt första program.

När du har läst det här dokumentet kommer du att:

* Förstå vad ett program är.
* Se skillnaden mellan produktion och sandlådeprogram.
* Skapa ett eget program.

## Vad är ett program? {#programs}

Program är den högsta organisationsnivån i Cloud Manager. Beroende på vilken licens du har hos Adobe kan du ordna din lösning och ge vissa teammedlemmar tillgång till dessa program.

Cloud Manager-program representerar uppsättningar av Cloud Manager-miljöer. Dessa program stöder logiska uppsättningar av affärsinitiativ, som vanligtvis motsvarar ett licensierat serviceavtal (SLA). Ett program kan t.ex. representera de AEM resurserna för att stödja en global offentlig webbplats för en organisation, medan ett annat program representerar en intern, central DAM.

Om du kommer ihåg exemplet med WKND Travel and Adventure Enterprises, som är en hyresgäst som fokuserar på reserelaterade medier, kan de ha två program: ett Sites-program för divisionen WKND Magazine och ett Assets-program för divisionen WKND Media. Olika teammedlemmar skulle då ha tillgång till de olika programmen på grund av sin egen uppdelning av arbetskrav.

Det finns två olika typer av program:

* A **produktionsprogram** skapas för att aktivera livatrafik för din webbplats. Det här är din&quot;riktiga&quot; miljö.
* A **sandlådeprogram** skapas vanligtvis för utbildning, löpande demonstrationer, aktivering, POC eller dokumentation.

Eftersom de har olika syften har de olika miljöerna olika alternativ. Processen att skapa dem liknar dock den du gör. För den här introduktionsresan ska vi skapa en sandlådemiljö.

>[!TIP]
>
>Om du behöver skapa ett produktionsprogram kan du läsa [Ytterligare resurser](#additional-resources) för en länk till dokumentation som beskriver programmen i detalj.

## Skapa ett sandlådeprogram {#create-sandbox}

Följ de här stegen för att skapa ett sandlådeprogram.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på **Lägg till program** i skärmens övre högra hörn.

   ![Startsida för Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. Välj **Konfigurera en sandlåda**, ange ett programnamn och klicka sedan på **Skapa**.

   ![Skapa programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

Du ser ett nytt sandlådeprogramkort på landningssidan med en statusindikator allt eftersom installationsprocessen fortskrider.

![Skapa sandlåda från översiktssida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

När programmet är klart har medlemmar i organisationen tilldelats **Utvecklare** produktprofilen kan logga in på Cloud Manager och hantera Creative Manager Git-databaser.

## What’s Next {#whats-next}

Nu när ditt första program har skapats kan du skapa miljöer för det. Du bör fortsätta din introduktionsresa genom att granska dokumentet nästa gång [Skapa miljöer.](create-environments.md)

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) - Lär dig mer om Cloud Managers hierarki och hur de olika typerna av program passar in i dess struktur och hur de skiljer sig åt.
* [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) - Lär dig hur du använder Cloud Manager för att skapa ett eget sandlådeprogram för utbildning, demo, POC eller andra icke-produktionssyften.
* [Skapa produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) - Lär dig hur du använder Cloud Manager för att skapa ett eget produktionsprogram för livstrafik.
* [Använda Adobe Cloud Manager - Program](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) - Cloud Manager-program representerar uppsättningar AEM miljöer som stöder logiska uppsättningar av affärsinitiativ, vilket vanligtvis motsvarar ett köpt servicenivåavtal (SLA).
* [AEM as a Cloud Service team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) - Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till era licensierade Adobe-lösningar.
