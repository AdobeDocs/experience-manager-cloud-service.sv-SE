---
title: Hantera miljöer
description: Lär dig mer om de typer av miljöer du kan skapa och hur du skapar dem för ditt Cloud Manager-projekt.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 5311ba7f001201fc94c73fa52bc7033716c1ba78
workflow-type: tm+mt
source-wordcount: '2271'
ht-degree: 0%

---


# Hantera miljöer {#managing-environments}

Lär dig mer om de typer av miljöer du kan skapa och hur du skapar dem för ditt Cloud Manager-projekt.

## Miljötyper {#environment-types}

En användare med nödvändig behörighet kan skapa följande miljötyper (inom gränserna för vad som är tillgängligt för den specifika klientorganisationen).

* **Production + Stage** - Produktions- och testmiljöer finns som par och används för produktions- respektive testningsändamål.

* **Utveckling** - En utvecklingsmiljö kan skapas för utvecklings- och testningsändamål och kan endast kopplas till icke-produktionsrörledningar.

* **Snabb utveckling** - Med en snabb utvecklingsmiljö kan utvecklare snabbt driftsätta och granska ändringar, vilket minimerar den tid som krävs för att testa funktioner som är beprövade i en lokal utvecklingsmiljö. Se [dokumentation för snabb utvecklingsmiljö](/help/implementing/developing/introduction/rapid-development-environments.md) om du vill ha mer information om hur du använder en RDE.

De enskilda miljöernas kapacitet beror på vilka lösningar som finns i [program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) av miljön.

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [Skärmar](/help/screens-cloud/home.md)

>[!NOTE]
>
>Produktions- och mellanlagringsmiljöer skapas endast som par. Du kan inte skapa enbart en staging eller bara en produktionsmiljö.

## Lägga till en miljö {#adding-environments}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program som du vill lägga till en miljö för.

1. Från **Programöversikt** sida, klicka **Lägg till miljö** på **Miljö** för att lägga till en miljö.

   ![Miljökort](assets/no-environments.png)

   * The **Lägg till miljö** finns även på **Miljö** -fliken.

     ![Fliken Miljö](assets/environments-tab.png)

   * The **Lägg till miljö** kan vara inaktiverat på grund av bristande behörighet eller beroende på vilka licensierade resurser som används.

1. I **Lägg till miljö** som visas:

   * Välj en [**miljötyp**.](#environment-types)
      * Antalet tillgängliga/använda miljöer visas inom parentes bakom miljötypsnamnet.
   * Tillhandahålla en miljö **Namn**.
   * Tillhandahålla en miljö **Beskrivning**.
   * Om du lägger till en **Production + Stage** måste du ange ett miljönamn och en beskrivning för både din produktions- och staging-miljö.
   * Välj en **Primär region** i listrutan.
      * Den primära regionen kan inte ändras efter att den har skapats.
      * Beroende på vilka rättigheter du har kan du kanske konfigurera [flera regioner](#multiple-regions).

   ![Dialogrutan Lägg till miljö](assets/add-environment2.png)

1. Klicka **Spara** för att lägga till den angivna miljön.

The **Översikt** visas nu din nya miljö i **Miljö** kort. Nu kan du ställa in rörledningar för din nya miljö.

## Flera publiceringsområden {#multiple-regions}

En användare med **Företagsägare** kan konfigurera produktions- och staging-miljöer så att de omfattar upp till tre ytterligare publiceringsregioner förutom den primära regionen. Ytterligare publiceringsregioner kan förbättra tillgängligheten. Se [Ytterligare dokumentation för publiceringsregioner](/help/operations/additional-publish-regions.md) för mer information.

>[!TIP]
>
>Du kan använda [API för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/api-usage/creating-programs-and-environments/#creating-aem-cloud-service-environments) för att fråga en aktuell lista över tillgängliga regioner.

### Lägga till flera publiceringsregioner i en ny miljö {#add-regions}

När du lägger till en miljö kan du välja att konfigurera ytterligare regioner utöver den primära regionen.

1. Välj **Primär region**.
   * Den primära regionen kan inte ändras efter att miljön har skapats.
1. Välj alternativet **Lägg till ytterligare publiceringsregioner** och en ny **Ytterligare publiceringsregioner** nedrullningsbar meny för alternativ visas.
1. I **Ytterligare publiceringsregioner** väljer du ett extra område.
1. Det markerade området läggs till under listrutan för att ange dess val.
   * Tryck eller klicka på `X` bredvid det markerade området så att du kan avmarkera det.
1. Välj ett annat område på menyn **Ytterligare publiceringsregioner** för att lägga till en annan region.
1. Tryck eller klicka **Spara** när du är redo att skapa din miljö.

![Markera flera områden](assets/select-multiple-regions.png)

De valda regionerna gäller både produktions- och stagningsmiljöer.

Om du inte anger några ytterligare regioner [kan du göra det senare när du har skapat miljöerna.](#edit-regions)

Om du vill etablera [avancerat nätverk](/help/security/configuring-advanced-networking.md) för programmet rekommenderar vi att denna etablering görs innan ytterligare publiceringsregioner läggs till i miljöerna med hjälp av Cloud Manager API. I annat fall går trafiken för de extra publiceringsregionerna igenom den primära regionens proxy.

### Redigera flera publiceringsområden {#edit-regions}

Om du inte angav några ytterligare regioner från början kan du göra det efter att miljöerna har skapats om du har de tillstånd som krävs.

Du kan även ta bort ytterligare publiceringsregioner. Du kan dock bara lägga till eller ta bort regioner i en transaktion. Om du måste lägga till en region och ta bort en region, ska du först lägga till, spara ändringen och sedan ta bort (eller omvänt).

1. Klicka på ellipsknappen för produktionsmiljön i programöversiktskonsolen och välj **Redigera** på menyn.

   ![Redigeringsmiljö](assets/select-edit-environment.png)

1. I **Redigera produktionsmiljö** gör de ändringar som behövs i de ytterligare publiceringsregionerna.
   * Använd **Ytterligare publiceringsregioner** för att välja ytterligare regioner.
   * Klicka på krysset bredvid de valda ytterligare publiceringsregionerna för att avmarkera dem.

   ![Redigeringsmiljö](assets/edit-environment.png)

1. Tryck eller klicka **Spara** för att spara ändringarna.

De ändringar som görs i produktionsmiljön gäller både produktions- och stagningsmiljöer. Ändringar i flera publiceringsregioner kan bara redigeras i produktionsmiljön.

Om du vill etablera [avancerat nätverk](/help/security/configuring-advanced-networking.md) för programmet rekommenderar vi att den här etableringen görs innan du lägger till ytterligare publiceringsregioner i miljöerna. Annars går trafiken i de extra publiceringsregionerna igenom den primära regionens proxy.

## Miljöinformation {#viewing-environment}

Du kan använda **Miljö** på översiktssidan för att få åtkomst till detaljerna i en miljö på två sätt.

1. Från **Översikt** klickar du på **Miljö** överst på skärmen.

   ![Fliken Miljö](assets/environments-tab2.png)

   * Du kan även klicka på **Visa alla** på **Miljö** för att gå direkt till **Miljö** -fliken.

     ![Visa alla, alternativ](assets/environment-showall.png)

1. The **Miljö** öppnar och visar alla miljöer för programmet.

   ![Fliken Miljöer](assets/environment-view-2.png)

1. Klicka på en miljö i listan så att du kan visa informationen om den.

   ![Miljöinformation](assets/environ-preview1.png)

Du kan också klicka på ellipsknappen för den miljö du vill använda och sedan välja **Visa detaljer**.

![Visa miljöinformation](assets/view-environment-details.png)

>[!NOTE]
>
>The **Miljö** endast tre miljöer. Klicka **Visa alla** som tidigare beskrivits för att se alla programmiljöer.

### Åtkomst till förhandsgranskningstjänsten {#access-preview-service}

I Cloud Manager finns en förhandsgranskningstjänst (som levereras som en extra publiceringstjänst) för varje AEM as a Cloud Service miljö.

Med tjänsten kan du förhandsgranska en webbplats slutliga upplevelse innan den når den faktiska publiceringsmiljön och är tillgänglig för allmänheten.

När förhandsvisningstjänsten skapas används en IP-tillåtelselista som standard, märkt `Preview Default [<envId>]`, som blockerar all trafik till förhandsvisningstjänsten. Använd inte standardvärdet för IP-tillåtelselista från förhandsgranskningstjänsten så att du kan aktivera åtkomst.

![Förhandsgranskningstjänst och tillåtelselista](assets/preview-ip-allow.png)

En användare med nödvändig behörighet måste utföra följande steg innan du kan dela URL:en för förhandsvisningstjänsten för att se till att den är tillgänglig.

1. Skapa ett lämpligt IP-tillåtelselista, tillämpa det på förhandsgranskningstjänsten och omedelbart ta bort kopplingen för `Preview Default [<envId>]` tillåtelselista.

   * Se [Använder och tar bort tillämpning av IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) för mer information.

1. Använda uppdateringen **IP Tillåtelselista** arbetsflöde för att ta bort standard-IP och lägga till IP-adresser efter behov. Se [Hantera IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) om du vill veta mer.

När åtkomsten till förhandsgranskningstjänsten har låsts upp visas inte längre låsikonen framför namnet på förhandsgranskningstjänsten.

När det är aktiverat kan du publicera innehåll till förhandsgranskningstjänsten med hjälp av gränssnittet Hantera publikation i AEM. Se [Förhandsgranska innehåll](/help/sites-cloud/authoring/fundamentals/previewing-content.md) för mer information.

>[!NOTE]
>
>Miljön måste vara i AEM version `2021.05.5368.20210529T101701Z` eller nyare för att använda förhandsgranskningstjänsten. Kontrollera att en uppdateringspipeline har körts korrekt i din miljö så att du kan använda förhandsgranskningstjänsten.

## Uppdaterar miljöer {#updating-dev-environment}

Som molnbaserad tjänst hanteras uppdateringar av dina staging- och produktionsmiljöer i produktionsprogrammen automatiskt av Adobe.

Uppdateringar av utvecklingsmiljöer och miljöer i sandlådeprogram hanteras dock i programmen. När en sådan miljö inte kör den senaste allmänt tillgängliga AEM-versionen, anges statusen på **Miljö** på **Översikt** skärm **Uppdatering tillgänglig**.

![Status för miljöuppdatering](assets/environ-update.png)

### Uppdateringar och pipeline {#updates-pipelines}

Rörledningar är det enda sättet att [distribuera kod till miljöer med AEM as a Cloud Service.](deploy-code.md) Därför är varje pipeline kopplad till en viss AEM.

Om Cloud Manager upptäcker att det finns en nyare version av AEM än den som senast distribuerades med pipeline, visas **Uppdatering tillgänglig** status för miljön.

Uppdateringsprocessen är därför en tvåstegsprocess:

1. Uppdaterar pipeline med den senaste AEM versionen
1. Köra pipeline för att distribuera den nya versionen av AEM till en miljö

### Uppdatera dina miljöer {#updating-your-environments}

The **Uppdatera** är tillgängligt från **Miljö** för utvecklingsmiljöer och miljöer i sandlådeprogram genom att klicka på knappen Ellips i miljön.

![Uppdateringsalternativ från miljökort](assets/environ-update2.png)

Det här alternativet är också tillgängligt genom att klicka på **Miljö** -fliken i programmet och sedan markera miljöns ellipsknapp.

![Uppdateringsalternativ på fliken Miljö](assets/environ-update3.png)

En användare med **Distributionshanteraren** kan använda det här alternativet för att uppdatera pipeline som är associerad med den här miljön till den senaste AEM versionen.

När pipeline-versionen har uppdaterats till den senaste allmänt tillgängliga AEM-versionen uppmanas användaren att köra den associerade pipelinen för att distribuera den senaste versionen till miljön.

![Uppmana att köra pipeline för att uppdatera miljön](assets/update-run-pipeline.png)

The **Uppdatera** Alternativets beteende varierar beroende på programmets konfiguration och aktuella tillstånd.

* Om pipeline redan har uppdaterats **Uppdatera** uppmanar användaren att köra pipelinen.
* Om pipelinen redan uppdateras visas **Uppdatera** informerar användaren om att en uppdatering redan körs.
* Om en lämplig pipeline inte finns, **Uppdatera** uppmanar användaren att skapa en.

## Tar bort utvecklingsmiljöer {#deleting-environment}

Användare med nödvändig behörighet kan ta bort en utvecklingsmiljö.

Från **Översikt** programskärmen på **Miljö** klickar du på ellipsknappen i den utvecklingsmiljö du vill ta bort.

![Alternativet Ta bort](assets/environ-delete.png)

Alternativet Ta bort är också tillgängligt från **Miljö** -fliken i **Översikt** programfönstret. Klicka på ellipsknappen i miljön och välj **Ta bort**.

![Alternativet Ta bort på fliken Miljö](assets/environ-delete2.png)

>[!NOTE]
>
>* Produktions- och mellanlagringsmiljöer som skapats i ett produktionsprogram kan inte tas bort.
>* Produktions- och mellanlagringsmiljöer i ett sandlådeprogram kan tas bort.

## Hantera åtkomst {#managing-access}

Välj **Hantera åtkomst** på menyn ellips i miljön på **Miljö** kort. Du kan navigera till författarinstansen direkt och hantera åtkomsten för din miljö.

![Hantera åtkomstalternativ](assets/environ-access.png)

>[!TIP]
>
>Se [AEM as a Cloud Service team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) om du vill veta hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomsten till era licensierade Adobe-lösningar.

## Åtkomst till Developer Console {#accessing-developer-console}

Välj **Developer Console** på menyn ellips i miljön på **Miljö** kort. En ny flik öppnas i webbläsaren med inloggningssidan till **Developer Console**.

![](assets/environ-devconsole.png)

Endast en användare med **Utvecklare** rollen har åtkomst till **Developer Console**. För sandlådeprogram har dock alla användare som har åtkomst till sandlådeprogrammet åtkomst till **Developer Console**.

Se [Viloläge och avvänjningsmiljöer för sandlådor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs.html#hibernation) för mer information.

Det här alternativet är också tillgängligt från **Miljö** -fliken i **Översikt** när du klickar på ellipsmenyn i en enskild miljö.

## Logga in lokalt {#login-locally}

Välj **Lokal inloggning** från ellipsmenyn i miljön i **Miljö** så att du kan logga in lokalt på Adobe Experience Manager.

![Logga in lokalt](assets/environ-login-locally.png)

Du kan även logga in lokalt från **Miljö** -fliken i **Översikt** sida.

![Logga in lokalt från fliken Miljö](assets/environ-login-locally-2.png)

## Hantera anpassade domännamn {#manage-cdn}

Anpassade domännamn stöds i Cloud Manager för Sites-program för både publicerings- och förhandsgranskningstjänster. Varje Cloud Manager-miljö har plats för upp till 250 anpassade domäner.

Om du vill konfigurera egna domännamn går du till **Miljö** och klicka på en miljö för att visa miljöinformation.

![Miljöinformation](assets/domain-names.png)

Följande åtgärder kan utföras på publiceringstjänsten för din miljö.

* [Lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [Kontrollerar status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) eller en [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [Hantera IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## Hantera IP-Tillåtelselista {#manage-ip-allow-lists}

IP-tillåtelselista stöds i Cloud Manager för författare, publicering och förhandsgranskningstjänster för Sites-program.

Om du vill hantera IP-tillåtelselista går du till **Miljö** -fliken i **Översikt** sidan med ditt program. Klicka på en enskild miljö så att du kan hantera informationen om den.

### Använda ett IP-Tillåtelselista {#apply-ip-allow-list}

När du använder en IP-tillåtelselista kopplas alla IP-intervall som ingår i definitionen av tillåtelselista till en författare eller publiceringstjänst i en miljö. En användare i **Företagsägare** eller **Distributionshanteraren** roll måste vara inloggad för att kunna tillämpa en IP-tillåtelselista.

IP-tillåtelselista måste finnas i Cloud Manager för att det ska kunna användas i en miljö. Mer information om IP-tillåtelselista i Cloud Manager finns i [Introduktion till IP-Tillåtelselista i Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

**Så här använder du ett IP-tillåtelselista:**

1. Navigera till den specifika miljön från **Miljö** fliken för programmet **Översikt** och navigera till **IP-Tillåtelselista** tabell.
1. Använd inmatningsfälten högst upp i tabellen IP tillåtelselista så att du kan välja IP-tillåtelselista och den författare eller publiceringstjänst som du vill använda den på.
1. Klicka **Använd** och bekräfta ditt bidrag.

### Ta bort en IP-tillåtelselista {#unapply-ip-allow-list}

Om du tar bort en IP-tillåtelselista kopplas alla IP-intervall som ingår i definitionen av tillåtelselista bort från en författare eller en utgivartjänst i en miljö. En användare i **Företagsägare** eller **Distributionshanteraren** roll måste vara inloggad för att kunna ta bort en IP-tillåtelselista.

**Så här tar du bort ett IP-tillåtelselista:**

1. Navigera till den specifika miljön från **Miljö** fliken för programmet **Översikt** och navigera till **IP-Tillåtelselista** tabell.
1. Identifiera raden där regeln för IP-tillåtelselista som du vill ta bort är listad.
1. Markera ellipsknappen i slutet av raden.
1. Välj **Oanvänd** och bekräfta ditt bidrag.
