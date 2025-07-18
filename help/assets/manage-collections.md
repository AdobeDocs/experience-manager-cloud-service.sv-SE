---
title: Hantera samlingar med digitala resurser
description: Förstå begreppet samling i Adobe Experience Manager Assets. Lär dig hur du samlar, hanterar, redigerar och samlar med andra användare.
contentOwner: AG
mini-toc-levels: 1
feature: Collections, Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 13%

---

# Hantera samlingar {#manage-collections}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-collections.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

En samling är en uppsättning resurser i Adobe Experience Manager Assets. Använd samlingar för att dela resurser mellan användare. Uppsättningen kan vara en statisk samling eller en dynamisk samling som baseras på sökresultat.

Till skillnad från mappar kan en samling innehålla resurser från olika platser. Du kan dela samlingar med olika användare som har olika behörighetsnivåer, t.ex. visning, redigering och så vidare.

Du kan dela flera samlingar med en användare. Varje samling innehåller referenser till resurser. Resursernas referensintegritet bevaras i alla samlingar.

Samlingar är av följande typer, baserat på det sätt som de samlar resurser på:

* En samling som innehåller en statisk referenslista med resurser, mappar och andra samlingar.

* En smart samling som dynamiskt inkluderar resurser baserat på sökvillkor.

## Åtkomst till samlingskonsolen {#navigate-the-collections-console}

Så här öppnar du konsolen **[!UICONTROL Collections]**:

Om du vill öppna **[!UICONTROL Collections]** väljer du Experience Manager logotyp. Gå till **[!UICONTROL Assets]** > **[!UICONTROL Collections]** från navigeringssidan.

## Skapa en samling {#create-a-collection}

Du kan skapa en samling med [statiska referenser](#create-a-collection-with-static-references) eller baserat på ett [sökkriteriebaserat filter](#create-a-smart-collection). Du kan också skapa en samling från en ljuslåda.

### Skapa en samling med statiska referenser {#create-a-collection-with-static-references}

Du kan skapa en samling med statiska referenser, t.ex. en samling med referenser till resurser, mappar, samlingar, snurruppsättningar och bilduppsättningar.

1. Navigera till konsolen **[!UICONTROL Collections]**.
1. Välj **[!UICONTROL Create]** i verktygsfältet.
1. Ange en rubrik och en valfri beskrivning för samlingen på sidan **[!UICONTROL Create Collection]**.
1. Lägg till medlemmar i samlingen och tilldela lämpliga behörigheter. Du kan också välja **[!UICONTROL Public Collection]** om du vill tillåta alla användare att komma åt samlingen.

   >[!NOTE]
   >
   >Om du vill att medlemmarna ska kunna dela samlingar med andra användare anger du `dam-users`-gruppens läsbehörighet på sökvägen `home/users`. Ge användarna på `/content/dam/collections` plats behörighet att tillåta användarna att visa samlingar i popup-listor. Du kan också göra användaren till en del av gruppen `dam-users`.

1. (Valfritt) Lägg till en miniatyrbild för samlingen.
1. Välj **[!UICONTROL Create]** och sedan **[!UICONTROL OK]** för att stänga dialogrutan. En samling med den angivna titeln och de angivna egenskaperna öppnas i konsolen Samlingar.

   >[!NOTE]
   >
   >Med Experience Manager Assets kan du skapa granskningsåtgärder för en samling på samma sätt som du skapar granskningsåtgärder för en resursmapp.

   Om du vill lägga till resurser i samlingen går du till Assets användargränssnitt. Mer information finns i [Lägga till resurser i en samling](#add-assets-to-a-collection).

### Skapa samlingar med dropzone {#create-collections-using-dropzone}

Du kan dra resurser från Assets-gränssnittet till en samling. Du kan också skapa en kopia av en samling och dra resurserna dit.

1. I Assets-användargränssnittet väljer du de resurser du vill lägga till i en samling.
1. Dra resurserna till zonen **[!UICONTROL Drop in Collection]**. Du kan också välja ikonen **[!UICONTROL To Collection]** i verktygsfältet.
1. På sidan **[!UICONTROL Add To Collection]** väljer du ikonen **[!UICONTROL Create Collection]** i verktygsfältet. Om du vill lägga till resurserna i en befintlig samling markerar du den på sidan och väljer **[!UICONTROL Add]**. Som standard väljs den senast uppdaterade samlingen.
1. Ange ett namn för samlingen i dialogrutan **[!UICONTROL Create New Collection]**. Om du vill att samlingen ska vara tillgänglig för alla användare väljer du **[!UICONTROL Public Collection]**.
1. Välj **[!UICONTROL Continue]** om du vill skapa samlingen.

### Skapa en smart samling {#create-a-smart-collection}

En smart samling använder ett sökvillkor för att dynamiskt fylla i resurser. Du kan skapa en smart samling med enbart filer och inte med mappar eller filer och mappar.

1. Navigera till användargränssnittet för Assets och välj ikonen **[!UICONTROL Search]**.
1. Ange söknyckelordet i rutan Omni Search och välj `Enter`. Välj ikonen GlobalNav om du vill visa panelen Filter och använda ett sökfilter från sökpanelen.
1. Välj **[!UICONTROL Files]** i listan **[!UICONTROL Files & Folders]**.
1. Välj **[!UICONTROL Save Smart Collection]**.
1. Ange ett namn för samlingen. Välj **[!UICONTROL Public]** om du vill lägga till DAM-användargruppen med visningsrollen i den smarta samlingen.

   >[!NOTE]
   >
   >Om du väljer **[!UICONTROL Public]** blir den smarta samlingen tillgänglig för alla med rollen Ägare när du har skapat den. Om du avbryter alternativet **[!UICONTROL Public]** är DAM-användargruppen inte längre kopplad till den smarta samlingen.

1. Välj **[!UICONTROL Save]** för att skapa den smarta samlingen och stäng sedan meddelanderutan för att slutföra processen. Den nya smarta samlingen läggs också till i listan **[!UICONTROL Saved Searches]**.
Etiketten på knappen **[!UICONTROL Create Smart Selection]** ändras till **[!UICONTROL Edit Smart Selection]**. Om du vill redigera inställningarna för den smarta samlingen väljer du **[!UICONTROL Files]** i listan **[!UICONTROL Files & Folders]**. Välj sedan knappen **[!UICONTROL Edit Smart Selection]**.

## Lägga till resurser i en samling {#add-assets-to-a-collection}

Du kan lägga till resurser i en samling som innehåller en lista med refererade resurser eller mappar.

>[!NOTE]
>
>Smarta samlingar använder en sökfråga för att fylla i resurser. Statiska referenser till resurser och mappar kan därför inte användas för dem.

1. I Assets-gränssnittet navigerar du till platsen för resursen som du vill lägga till i en samling.
1. Markera resursen och välj ikonen **[!UICONTROL To Collection]** i verktygsfältet. Du kan också dra resursen till zonen **[!UICONTROL Drop in Collection]**. Släpp musknappen när släppzonen blir aktiv och etiketten ändras till **[!UICONTROL Drop to Add]**.
1. På sidan **[!UICONTROL Add To Collection]** väljer du den samling som du vill lägga till resursen i.
1. Välj **[!UICONTROL Add]** och stäng sedan bekräftelsemeddelandet. Resursen läggs till i samlingen.

## Redigera en smart samling {#edit-a-smart-collection}

Smarta samlingar skapas genom att en sökning sparas så att du kan ändra deras innehåll genom att ändra sökparametrarna för den [sparade sökningen](#saved-searches).

1. I Assets-användargränssnittet väljer du ikonen **[!UICONTROL Search]** i verktygsfältet.
1. Markera `Enter` med markören i sökrutan.
1. Välj ikonen GlobalNav för att visa panelen Filter.
1. Välj den smarta samling du vill ändra i listan **[!UICONTROL Saved Searches]**. På sökpanelen visas de filter som har konfigurerats för den sparade sökningen.
1. Välj **[!UICONTROL Files]** i listan **[!UICONTROL Files & Folders]**.
1. Ändra ett eller flera filter efter behov. Välj **[!UICONTROL Edit Smart Collection]**. Du kan också redigera namnet på den smarta samlingen.
1. Välj **[!UICONTROL Save]**. Dialogrutan **[!UICONTROL Edit Smart Collection]** visas.
1. Välj **[!UICONTROL Overwrite]** om du vill ersätta den ursprungliga smarta samlingen med den redigerade samlingen. Du kan också välja **[!UICONTROL Save As]** om du vill spara den redigerade samlingen separat.
1. I bekräftelsedialogrutan väljer du **[!UICONTROL Save]** för att slutföra processen.

## Visa och redigera samlingsmetadata {#view-and-edit-collection-metadata}

Samlingsmetadata omfattar data om samlingen, inklusive taggar som läggs till.

1. Välj en samling i konsolen Samlingar och välj ikonen **[!UICONTROL Properties]** i verktygsfältet.
1. På sidan **[!UICONTROL Collection Metadata]** visar du samlingens metadata från flikarna **[!UICONTROL Basic]** och **Avancerat**.
1. Ändra metadata efter behov och välj sedan **[!UICONTROL Save & Close]** i verktygsfältet för att spara ändringarna.

### Redigera samlingsmetadata {#edit-collection-metadata-in-bulk}

Du kan redigera metadata för flera samlingar samtidigt. Med den här funktionen kan du snabbt replikera vanliga metadata i flera samlingar.

1. I konsolen Samlingar väljer du två eller flera samlingar som du vill redigera metadata för.
1. Välj ikonen **[!UICONTROL Properties]** i verktygsfältet.
1. På sidan **[!UICONTROL Collection Metadata]** redigerar du metadata på flikarna **[!UICONTROL Basic]** och **[!UICONTROL Advanced]** efter behov.
1. Välj **[!UICONTROL Save & Close]** i verktygsfältet och stäng sedan bekräftelsedialogrutan för att slutföra processen.
1. Om du vill lägga till nya metadata till de befintliga metadata väljer du **[!UICONTROL Apend mode]**. Om du inte markerar det här alternativet ersätter de nya metadata de data som finns i fälten. Välj **[!UICONTROL Submit]**.

   >[!NOTE]
   >
   >Tilläggsläget fungerar bara för fält som kan innehålla flera värden. För fält som bara kan innehålla ett enda värde läggs de nya metadata inte till i det befintliga värdet i fältet, även om du väljer **[!UICONTROL Append mode]**.

## Sök {#searching}

Sökfunktionen i samlingar har stöd för både [Söka efter samlingar](#search-collections) och [Söka efter resurser i en samling](#search-within-collections).

### Sök i samlingar {#search-collections}

Du kan söka efter samlingar från samlingskonsolen. När du söker med nyckelord i sökrutan söker [!DNL Experience Manager Assets] efter samlingsnamn, metadata och de taggar som har lagts till i samlingarna.

Om du söker efter samlingar från den översta nivån returneras bara enskilda samlingar i sökresultaten. Assets eller mappar i samlingarna ingår inte. I alla andra fall (till exempel i en enskild samling eller i en mapphierarki) returneras alla relevanta resurser, mappar och samlingar.

### Sök i samlingar {#search-within-collections}

I konsolen Samlingar väljer du en samling för att öppna den.

I en samling är [!DNL Experience Manager]-sökningen begränsad till resurser (och deras taggar och metadata) i samlingen som du visar. När du söker i en mapp returneras alla matchande resurser och underordnade mappar i den aktuella mappen. När du söker i en samling returneras endast matchande resurser, mappar och andra samlingar som är direktmedlemmar i samlingen.

## Redigera samlingsinställningar {#edit-collection-settings}

Du kan redigera samlingsinställningar, till exempel rubrik och beskrivning, eller lägga till medlemmar i en samling.

1. Markera en samling och välj ikonen **[!UICONTROL Settings]** i verktygsfältet. Du kan också använda snabbåtgärden **[!UICONTROL Settings]** från samlingsminiatyrbilden.
1. Ändra inställningarna för samlingen på sidan **[!UICONTROL Collection Settings]**. Du kan till exempel ändra samlingens titel, beskrivningar, medlemmar och behörigheter enligt beskrivningen i [Lägg till samlingar](#create-a-collection).
1. Välj **[!UICONTROL Save]** om du vill spara ändringarna.

## Ta bort en samling {#delete-a-collection}

1. Välj en eller flera samlingar i konsolen Samlingar och välj ikonen Ta bort i verktygsfältet.
1. I dialogrutan väljer du **[!UICONTROL Delete]** för att bekräfta borttagningsåtgärden.

   >[!NOTE]
   >
   >Du kan också ta bort smarta samlingar genom att [ta bort sparade sökningar](#saved-searches).

## Hämta en samling {#download-a-collection}

När du hämtar en samling hämtas hela resurshierarkin i samlingen, inklusive mappar och underordnade samlingar.

1. Välj en eller flera samlingar som du vill hämta från samlingskonsolen.
1. Välj hämtningsikonen i verktygsfältet.
1. Välj **[!UICONTROL Download]** i dialogrutan **[!UICONTROL Download]**. Om du vill hämta återgivningarna av resurserna i samlingen väljer du **[!UICONTROL Renditions]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   När du väljer en samling som ska hämtas hämtas hela mapphierarkin under samlingen. Om du vill inkludera varje samling som du hämtar (inklusive resurser i underordnade samlingar som är kapslade under den överordnade samlingen) i en enskild mapp väljer du **[!UICONTROL Create separate folder for each asset]**.

## Redigera metadataegenskaper för flera samlingar {#editing-metadata-properties-of-multiple-collections}

Med Adobe Enterprise Manager Assets kan du redigera flera samlingars metadata samtidigt. Använd sidan [!UICONTROL Properties] om du vill utföra metadataändringar i flera samlingar, till exempel ändra metadataegenskaper till ett gemensamt värde eller lägga till eller ändra taggar.

Om du vill anpassa sidan med metadata [!UICONTROL Properties], inklusive lägga till, ändra eller ta bort metadataegenskaper, använder du schemaredigeraren.

>[!NOTE]
>
>Massredigeringsmetoderna fungerar för resurser som är tillgängliga i en samling. För resurser som är tillgängliga mellan mappar eller matchar ett gemensamt villkor är det möjligt att [uppdatera metadata satsvis efter sökning](/help/assets/search-assets.md#metadata-updates).

1. I samlingskonsolen väljer du de samlingar du vill redigera.
1. Välj **[!UICONTROL Properties]** i verktygsfältet för att öppna sidan [!UICONTROL Properties] för de valda samlingarna.
1. Ändra metadataegenskaperna för markerade samlingar under de olika flikarna.

   >[!NOTE]
   >
   >De metadata som du lägger till för de valda samlingarna skriver över tidigare metadata för dessa samlingar, med undantag för taggar. Alla taggar som du lägger till i fältet **[!UICONTROL Tags]** läggs till i den befintliga listan med taggar i metadata.

1. Om du vill visa metadataegenskaperna för en viss samling avbryter du valet av de återstående samlingarna i samlingslistan. Metadataredigeringsfälten fylls i med metadata för den aktuella samlingen.

   >[!NOTE]
   >
   >* På sidan med samlingsegenskaper kan du ta bort samlingar från listan med samlingar genom att avbryta markeringen. I samlingslistan är alla samlingar markerade som standard. Metadata för samlingar som du tar bort uppdateras inte.
   >* Högst upp i listan markerar du kryssrutan nära **[!UICONTROL Title]** för att växla mellan att markera samlingarna och rensa listan.

1. Spara ändringarna.

## Skapa kapslade samlingar {#create-nested-collections}

Du kan lägga till en samling i en annan samling och på så sätt skapa en kapslad samling.

1. Välj önskad samling eller grupp med samlingar i konsolen Samlingar och välj **[!UICONTROL To Collection]** i verktygsfältet.
1. På sidan **[!UICONTROL Add To Collection]** väljer du den samling där samlingen ska läggas till.

   >[!NOTE]
   >
   >Den senast uppdaterade samlingen är markerad som standard på sidan **[!UICONTROL Add To Collection]**.

1. Välj **[!UICONTROL Add]**. Ett meddelande bekräftar att samlingen har lagts till i målsamlingen på sidan **[!UICONTROL Select Destination]**. Stäng meddelandet för att slutföra processen.

>[!NOTE]
>
>Smarta samlingar kan inte kapslas. Smarta samlingar kan alltså inte innehålla andra samlingar.

## Sparade sökningar {#saved-searches}

I Assets-gränssnittet kan du söka efter eller filtrera resurser baserat på vissa regler, sökvillkor eller anpassade sökfasetter. Om du sparar dem som **[!UICONTROL Saved Searches]** kan du komma åt dem senare från listan **[!UICONTROL Saved Searches]** på panelen Filter. När du skapar en sparad sökning skapas även en smart samling.

Sparade sökningar skapas när du skapar en smart samling. Smarta samlingar läggs automatiskt till i listan **[!UICONTROL Saved Searches]**. Frågan om sparade sökningar för samlingen sparas i egenskapen `dam:query` i CRXDE på den relativa platsen `/content/dam/collections/`. Det finns inga begränsningar för de sökningar som du kan spara och för de sparade sökningarna som visas i listan.

>[!NOTE]
>
>Du kan dela smarta samlingar på samma sätt som du delar statiska samlingar.

Att redigera sparade sökningar är detsamma som att redigera smarta samlingar. Mer information finns i [Redigera en smart samling](#edit-a-smart-collection).

Så här tar du bort sparade sökningar:

1. I Assets-användargränssnittet väljer du sökikonen i verktygsfältet.

1. Markera tangenten `Enter` med markören i omsökningsfältet.
1. Välj ikonen GlobalNav för att visa panelen Filter.
1. I listan **[!UICONTROL Saved Searches]** väljer du **[!UICONTROL Delete]** bredvid den smarta samling du vill ta bort.
1. I dialogrutan väljer du **[!UICONTROL Delete]** för att ta bort den sparade sökningen.

## Köra ett arbetsflöde i en samling {#run-a-workflow-on-a-collection}

Du kan köra ett arbetsflöde för resurserna i en samling. Om samlingen innehåller kapslade samlingar körs arbetsflödet även på resurserna i de kapslade samlingarna. Om samlingen och den kapslade samlingen innehåller duplicerade resurser körs arbetsflödet bara en gång för sådana resurser.

1. Välj en samling som du vill köra ett arbetsflöde för i samlingskonsolen.
1. Välj ikonen GlobalNav och välj **[!UICONTROL Timeline]** i listan.
1. Välj ikonen Cirkumflex längst ned på tidslinjen och välj sedan **[!UICONTROL Start Workflow]**.
1. I avsnittet **[!UICONTROL Start Workflow]** väljer du en arbetsflödesmodell i listan. Välj till exempel modellen **[!UICONTROL DAM Update Asset]**.
1. Ange en titel för arbetsflödet och välj **[!UICONTROL Start]**.
1. Välj **[!UICONTROL Proceed]** i dialogrutan. Arbetsflödet körs på alla resurser i samlingen.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Skapa en granskningsaktivitet för samlingar](/help/assets/bulk-approval.md)
