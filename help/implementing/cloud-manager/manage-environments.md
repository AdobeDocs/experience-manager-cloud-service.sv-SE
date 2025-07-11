---
title: Hantera miljöer
description: Lär dig mer om vilka typer av miljöer du kan skapa och hur du skapar dem för ditt Cloud Manager-projekt.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3e7ce0c7f330ba92b57e36ea8fe5bb17b5998cb1
workflow-type: tm+mt
source-wordcount: '2488'
ht-degree: 0%

---


# Hantera miljöer {#managing-environments}

Lär dig mer om vilka typer av miljöer du kan skapa och hur du skapar dem för ditt Cloud Manager-projekt.

## Miljötyper {#environment-types}

En användare med nödvändig behörighet kan skapa följande miljötyper (inom gränserna för vad som är tillgängligt för den specifika klientorganisationen).

| Miljötyp | Beskrivning |
| --- | --- |
| **Produktion + scen** | Produktions- och testmiljöer finns som par och används för produktions- respektive testningsändamål. Utför prestanda- och säkerhetstester på scenmiljön. Den har samma storlek som produktionen. |
| **Utveckling** | En utvecklingsmiljö kan skapas för utvecklings- och testningsändamål och kan endast kopplas till icke-produktionsrörledningar. Utvecklingsmiljöer har inte samma storlek som fas och produktion och bör inte användas för att utföra prestanda- och säkerhetstester. |
| **Snabb utveckling** | Med en Rapid Development Environment (RDE) kan utvecklare snabbt driftsätta och granska ändringar. Detta minskar tiden som krävs för att testa funktioner som redan har validerats i en lokal utvecklingsmiljö. Mer information om hur du använder en RDE finns i [dokumentationen för den snabba utvecklingsmiljön](/help/implementing/developing/introduction/rapid-development-environments.md). |
| **Specialiserad testmiljö** | Specialiserade testmiljöer ger ett dedikerat utrymme för att validera funktioner under förhållanden som liknar produktionsförhållanden, vilket är idealiskt för stresstestning och avancerade kontroller före driftsättning. Se [Lägg till en anpassad testmiljö](/help/implementing/cloud-manager/specialized-test-environment.md) |

>[!NOTE]
>
>Funktionen **Specialiserad testmiljö** är för närvarande bara tillgänglig via det privata betaprogrammet. Mer information om hur du registrerar dig för den privata betaversionen finns i [Specialiserad testmiljö](/help/implementing/cloud-manager/release-notes/current.md#specialized-test-environment).

Funktionerna i enskilda miljöer beror på vilka lösningar som är aktiverade i [programmet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) i miljön.

* [Sites](/help/overview/introduction.md)
* [Assets](/help/assets/overview.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/introduction/introduction.md)

>[!NOTE]
>
>Produktions- och mellanlagringsmiljöer skapas endast som par. Du kan inte skapa en miljö som bara är för produktion eller endast för staging.

## Lägga till en miljö {#adding-environments}

Om du vill lägga till eller redigera en miljö måste användaren vara medlem i rollen **Affärsägare**.

**Så här lägger du till en miljö:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på programmet som du vill lägga till en miljö för.

1. Gör något av följande:

   Om alternativet **Lägg till miljö** är nedtonat (inaktiverat) kan det bero på att behörigheter saknas eller att de är beroende av de licensierade resurserna.

   * På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på **Lägg till miljö** på **miljökortet**.

   ![Miljökort](assets/no-environments.png)

   * Klicka på ![dataikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljöer** på den vänstra panelen och klicka sedan på **Lägg till miljö** på sidan Miljöer, i det övre högra hörnet.

     ![Fliken Miljö](assets/environments-tab.png)

1. Gör följande i dialogrutan **Lägg till miljö**:

   * Välj en [**miljötyp**](#environment-types). Antalet tillgängliga/använda miljöer visas inom parentes bakom miljötypsnamnet.
   * Ange miljön **Namn**. Miljönamnet kan inte ändras efter att miljön har skapats.
   * Ange en valfri **beskrivning** för miljön.
   * Om du lägger till en **Produktion + Stage**-miljö måste du ange ett miljönamn och en beskrivning för både din produktions- och mellanlagringsmiljö.
   * Välj en **primär region** i listrutan. Den primära regionen kan inte ändras efter att den har skapats. Beroende på vilka berättiganden du har kan du konfigurera [flera regioner](#multiple-regions).

   ![Dialogrutan Lägg till miljö](assets/add-environment2.png)

1. Klicka på **Spara**.

Sidan **Översikt** visar nu din nya miljö på kortet **Miljöer**. Nu kan du ställa in rörledningar för din nya miljö.

## Flera publiceringsregioner {#multiple-regions}

En användare med rollen **Affärsägare** kan konfigurera produktions- och mellanlagringsmiljöer så att ytterligare tre publiceringsregioner ingår förutom den primära regionen. Ytterligare publiceringsregioner kan förbättra tillgängligheten. Mer information finns i [dokumentationen för ytterligare publiceringsregioner](/help/operations/additional-publish-regions.md).

>[!TIP]
>
>Du kan använda [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/api-usage/creating-programs-and-environments/#creating-aem-cloud-service-environments) för att fråga en aktuell lista över tillgängliga regioner.

### Lägga till flera publiceringsregioner i en ny miljö {#add-regions}

När du lägger till en miljö kan du välja att konfigurera ytterligare regioner utöver den primära regionen.

1. Markera den primära regionen **1**.
   * Den primära regionen kan inte ändras efter att miljön har skapats.
1. Välj alternativet **Lägg till ytterligare publiceringsregioner** och en ny listruta med alternativet **Ytterligare publiceringsregioner** visas.
1. I listrutan **Ytterligare publiceringsregioner** väljer du en extra region.
1. Det markerade området läggs till under listrutan för att ange dess val.
   * Markera `X` bredvid den markerade regionen så att du kan avmarkera den.
1. Välj en annan region i listrutan **Ytterligare publiceringsregioner** om du vill lägga till en annan region.
1. Välj **Spara** när du är redo att skapa din miljö.

![Markera flera regioner](assets/select-multiple-regions.png)

De valda regionerna gäller både produktions- och stagningsmiljöer.

Om du inte anger några ytterligare regioner kan [du göra det senare när miljöerna har skapats](#edit-regions).

Om du vill etablera [avancerat nätverk](/help/security/configuring-advanced-networking.md) för programmet rekommenderar vi att den här etableringen görs innan du lägger till ytterligare publiceringsregioner i miljöerna med hjälp av Cloud Manager API. I annat fall går trafiken för de extra publiceringsregionerna igenom den primära regionens proxy.

### Redigera flera publiceringsområden {#edit-regions}

Om du inte angav några ytterligare regioner från början kan du göra det när miljön har skapats och du har de rättigheter som krävs.

Du kan även ta bort ytterligare publiceringsregioner. Du kan dock bara lägga till eller ta bort regioner i en transaktion. Om du måste lägga till en region och ta bort en region, ska du först lägga till, spara ändringen och sedan ta bort (eller omvänt).

1. Klicka på ![Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för produktionsmiljön i programöversiktskonsolen och välj **Redigera** på menyn.

   ![Redigeringsmiljö](assets/select-edit-environment.png)

1. I dialogrutan **Redigera produktionsmiljö** gör du nödvändiga ändringar i de ytterligare publiceringsregionerna.
   * Använd listrutan **Ytterligare publiceringsregioner** för att välja ytterligare regioner.
   * Klicka på krysset bredvid de valda ytterligare publiceringsregionerna för att avmarkera dem.

   ![Redigeringsmiljö](assets/edit-environment.png)

1. Välj **Spara** om du vill spara ändringarna.

De ändringar som görs i produktionsmiljön gäller både produktions- och stagningsmiljöer. Ändringar i flera publiceringsregioner kan bara redigeras i produktionsmiljön.

Om du vill etablera [avancerat nätverk](/help/security/configuring-advanced-networking.md) för programmet rekommenderar vi att den här etableringen görs innan du lägger till ytterligare publiceringsregioner i miljöerna. I annat fall går trafiken för de extra publiceringsregionerna igenom den primära regionens proxy.

## Visa information om en miljö {#viewing-environment}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på programmet som du vill visa information om en miljö för.

1. Visa alla miljöer för programmet genom att göra något av följande:

   * På den vänstra menyn, under **Tjänster**, klickar du på ![Dataikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö**.

   ![Fliken Miljö](assets/environments-1.png)

   * Klicka på **Översikt** under **Program** på den vänstra menyn och klicka sedan på **Arbetsflödesikonen** ![Visa alla](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) på **miljökortet** .

     ![Visa alla alternativ](assets/environments-2.png)

   >[!NOTE]
   >
   >Kortet **Environment** innehåller endast tre miljöer. Klicka på **Visa alla** på kortet för att visa *alla* miljöer för programmet.

1. Gör något av följande på sidan Miljöer:

   * Klicka på en miljö i listan för att visa information om den.

   ![Miljöinformation](assets/environ-preview1.png)

   * Klicka på ![Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för miljön som du vill använda och klicka sedan på **Visa detaljer**.

   ![Visa miljöinformation](assets/view-environment-details.png)


## Återställa innehåll i en miljö {#restore-environment}

Se [Återställa innehåll i AEM as a Cloud Service](/help/operations/restore.md).

## Återställ tidigare kod som distribuerats {#restore-previous-code-deployed}

Se [Återställa tidigare kod som distribuerats i AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).


### Öppna förhandsgranskningstjänsten {#access-preview-service}

Cloud Manager tillhandahåller en förhandsgranskningstjänst (som levereras som en extra publiceringstjänst) för varje AEM as a Cloud Service-miljö.

Med tjänsten kan du förhandsgranska en webbplats slutliga upplevelse innan den når den faktiska publiceringsmiljön och är tillgänglig för allmänheten.

När förhandsgranskningstjänsten skapas används en standard-IP-tillåtelselista, som heter `Preview Default [<envId>]`, som blockerar all trafik till förhandsgranskningstjänsten. Använd inte standardvärdet för IP-tillåtelselista från förhandsgranskningstjänsten så att du kan aktivera åtkomst.

![Förhandsgranskningstjänsten och tillåtelselista](assets/preview-ip-allow.png)

En användare med nödvändig behörighet måste utföra följande steg innan du kan dela URL:en för förhandsvisningstjänsten för att se till att den är tillgänglig.

1. Skapa en lämplig IP-Tillåtelselista, använd den för förhandsgranskningstjänsten och ta omedelbart bort tillåtelselista `Preview Default [<envId>]`.

   Mer information finns i [Använd och ta bort tillämpning av IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md).

1. Använd uppdateringsarbetsflödet **IP Tillåtelselista** för att ta bort standard-IP och lägga till nödvändiga IP-adresser. Mer information finns i [Hantera IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md).

När åtkomsten till förhandsvisningstjänsten har låsts upp visas inte längre låsikonen framför namnet på förhandsgranskningstjänsten.

När det är aktiverat kan du publicera innehåll till förhandsgranskningstjänsten med hjälp av användargränssnittet **`Manage Publication`** i AEM. Mer information finns i [Förhandsgranska innehåll](/help/sites-cloud/authoring/sites-console/previewing-content.md).

>[!NOTE]
>
>Miljön måste finnas i AEM version `2021.05.5368.20210529T101701Z` eller senare för att du ska kunna använda förhandsgranskningstjänsten. Kontrollera att en uppdateringspipeline har körts korrekt i din miljö så att du kan använda förhandsgranskningstjänsten.

### Status för ytterligare publiceringsregioner {#additional-region-status}

Om du har aktiverat ytterligare publiceringsregioner kan du kontrollera statusen för dessa regioner från kortet **Environment**.

1. På sidan **Översikt** letar du reda på kortet **Miljöer**.

1. På **miljökortet** visar kolumnen **Status** om det finns några problem med de konfigurerade ytterligare publiceringsregionerna. Klicka på ikonen **Info** om du vill ha information om regionerna.

   ![Ytterligare statusinformation om publiceringsregioner på miljökortet](assets/additional-publish-region-status-environments-card.png)

Du kan även få tillgång till samma information från fliken **Miljö**.

1. På sidan **Översikt** klickar du på ![Dataikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö**.

1. På sidan **Miljö** väljer du den miljö som du vill fråga på den vänstra menyn.

1. När en miljö har valts:

   * Tabellen **Miljöinformation** visar vilka regioner som har konfigurerats för den valda miljön.
   * Kolumnen **Status** i tabellen **Miljösegment** visar om det finns några problem med de konfigurerade ytterligare publiceringsregionerna. Håll muspekaren över statusen för att få information om eventuella problem.

   ![Ytterligare statusinformation om publiceringsregioner på fliken Miljö](assets/additional-publish-region-status-environments-tab.png)

Om några problem rapporteras med ytterligare publiceringsregioner ska du vara tålmodig. Cloud Manager försöker ständigt återskapa regionen och den kan bli tillgänglig när som helst. Om problemet kvarstår efter flera timmar kan du ta bort den extra publiceringsregionen och lägga till den igen (antingen samma region eller en annan region) för att utlösa en fullständig distribution.

Hur länge du väntar på att systemet ska återställas fristående innan du vidtar ytterligare åtgärder beror på hur svårt det är för dina system.

Oavsett vilket dirigeras [trafik alltid till den närmaste regionen som är online](/help/operations/additional-publish-regions.md). Kontakta Adobe kundtjänst om du fortsätter att se problem.

## Uppdatera miljöer {#updating-dev-environment}

Som molnbaserad tjänst hanterar Adobe automatiskt uppdateringar för din utvecklings-, staging- och produktionsmiljö i produktionsprogrammen.

Uppdateringar av miljöer i sandlådeprogram hanteras dock i programmen. Om en sådan miljö inte kör den senaste allmänt tillgängliga AEM-versionen visas **Uppdatering tillgänglig** på **miljökortet** på skärmen **Översikt** i programmet.

![Status för miljöuppdatering](assets/environ-update.png)

### Uppdateringar och rörledningar {#updates-pipelines}

Pipelines är det enda sättet att [distribuera kod till AEM as a Cloud Service](deploy-code.md)-miljöer. Därför är varje pipeline kopplad till en viss AEM-version.

När Cloud Manager identifierar en nyare version av AEM än den som senast distribuerades med pipeline, visas statusen **Uppdatering tillgänglig** för miljön.

Uppdateringsprocessen är därför en tvåstegsprocess:

1. Uppdatera pipeline med den senaste AEM-versionen
1. Köra pipeline för att distribuera den nya versionen av AEM till en miljö

### Uppdatera dina miljöer {#updating-your-environments}

>[!NOTE]
> 2024 uppdateras redan utvecklingsinstanser och vissa sandlådeprogram automatiskt, så det finns inget behov av att hantera uppdateringar manuellt. Som ett resultat av den här övergången kanske alternativet att uppdatera miljön manuellt för utvecklingsinstanser inte är tillgängligt för _vissa_ av dina program.

Alternativet **Update** är tillgängligt på kortet **Environmental** för specifika utvecklings- och sandlådemiljöer. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid miljön för att komma åt **Uppdatering**.

![Uppdateringsalternativ från miljökort](assets/environ-update2.png)

Det här alternativet är också tillgängligt genom att klicka på fliken **Miljö** i programmet och sedan på ![Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i miljön.

![Uppdateringsalternativ på fliken Miljö](assets/environ-update3.png)

En användare med rollen **Distributionshanteraren** eller **Affärsägare** kan använda det här alternativet för att uppdatera pipeline som är associerad med den här miljön till den senaste AEM-versionen.

När pipeline-versionen har uppdaterats till den senaste allmänt tillgängliga AEM-versionen uppmanas användaren att köra den associerade pipeline för att distribuera den senaste versionen till miljön.

![Exempel på uppmaningen att köra pipelinen för att uppdatera miljön](assets/update-run-pipeline.png)

Beteendet för alternativet **Uppdatera** varierar beroende på programmets konfiguration och aktuella tillstånd.

| Läge | Uppdateringsalternativet.. |
| --- | --- |
| Pipelinen har redan uppdaterats | uppmanar användaren att köra pipelinen. |
| Pipelinen uppdateras redan | informerar användaren om att en uppdatering redan körs. |
| Pipelinen finns inte | uppmanar användaren att skapa en. |

## Ta bort utvecklingsmiljöer {#deleting-environment}

En användare med rollen **Distributionshanteraren** eller **Affärsägare** kan ta bort en utvecklingsmiljö.

På skärmen **Översikt** i programmet på kortet **Miljöer** klickar du på ![Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i den utvecklingsmiljö som du vill ta bort.

![Alternativet Ta bort](assets/environ-delete.png)

Alternativet **Ta bort** är också tillgängligt på fliken **Miljö** i programfönstrets **Översikt** . Klicka på ![Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i miljön och välj **Ta bort**.

![Alternativet Ta bort på fliken Miljö](assets/environ-delete2.png)

>[!NOTE]
>
>* Produktions- och mellanlagringsmiljöer som skapats i ett produktionsprogram kan inte tas bort.
>* Produktions- och mellanlagringsmiljöer i ett sandlådeprogram kan tas bort.

## Hantera åtkomst {#managing-access}

Välj **Hantera åtkomst** på menyn Ellips i miljön på kortet **Miljöer**. Du kan navigera till författarinstansen direkt och hantera åtkomsten för din miljö.

![Hantera åtkomstalternativ](assets/environ-access.png)

>[!TIP]
>
>Läs [AEM as a Cloud Service Team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) om du vill veta hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till licensierade Adobe-lösningar.

## Gå till Developer Console {#accessing-developer-console}

1. Klicka på ikonen **Mer** på ![miljökortet](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och sedan på **Developer Console**.

En ny flik öppnas i webbläsaren med inloggningssidan till **Developer Console**.

![Logga in på Developer Console](assets/environ-devconsole.png)

Endast en användare med rollen **Utvecklare** har åtkomst till **Developer Console**. För sandlådeprogram har dock alla användare med åtkomst till sandlådeprogrammet åtkomst till **Developer Console**.

Mer information finns i [Vilolägen och Fristående sandlådemiljöer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs#hibernation).

Det här alternativet är också tillgängligt på fliken **Miljö** i fönstret **Översikt** när du klickar på ![Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i en enskild miljö.

## Logga in lokalt {#login-locally}

1. Gör något av följande:

   * Klicka på ikonen **Mer** på ![miljökortet](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och klicka sedan på **Lokal inloggning**.

     ![Logga in lokalt](assets/environ-login-locally.png)

   * Klicka på ikonen ![Data](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö** från den vänstra panelen. På sidan **Miljö** klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och sedan på **Lokal inloggning**.

     ![Logga in lokalt från miljöfliken](assets/environ-login-locally-2.png)

## Hantera anpassade domännamn {#manage-cdn}

Anpassade domännamn stöds i Cloud Manager for Sites-program för både publicerings- och förhandsgranskningstjänster.

>[!TIP]
>
>Mer information finns i [Introduktion till anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

## Hantera IP-Tillåtelselista {#manage-ip-allow-lists}

Ett IP-Tillåtelselista stöds i Cloud Manager för författare, publicering och förhandsgranskning av Sites-program.

Om du vill hantera IP Tillåtelselista går du till sidan ![Dataikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö** på sidan **Översikt** i programmet. Klicka på en enskild miljö så att du kan hantera informationen om den.

### Använd en IP-Tillåtelselista {#apply-ip-allow-list}

När du använder en IP Tillåtelselista länkas alla definierade IP-intervall till en författare eller publiceringstjänst i miljön.

>[!TIP]
>
>Mer information finns i [Introduktion till IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).
