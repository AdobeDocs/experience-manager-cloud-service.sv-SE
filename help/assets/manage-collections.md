---
title: Hantera samlingar med digitala resurser
description: Förstå begreppet samling i Adobe Experience Manager Assets. Lär dig hur du samlar, hanterar, redigerar och samlar med andra användare.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# Hantera samlingar {#manage-collections}

En samling är en uppsättning resurser i Adobe Experience Manager Assets. Använd samlingar för att dela resurser mellan användare. Uppsättningen kan vara en statisk samling eller en dynamisk samling som baseras på sökresultat.

Till skillnad från mappar kan en samling innehålla resurser från olika platser. Du kan dela samlingar med olika användare som har olika behörighetsnivåer, t.ex. visning, redigering och så vidare.

Du kan dela flera samlingar med en användare. Varje samling innehåller referenser till resurser. Resursernas referensintegritet bevaras i alla samlingar.

Samlingar är av följande typer, baserat på det sätt som de samlar resurser på:

* En samling som innehåller en statisk referenslista med resurser, mappar och andra samlingar.

* En smart samling som dynamiskt inkluderar resurser baserat på sökvillkor.

## Åtkomst till samlingskonsolen {#navigate-the-collections-console}

Så här öppnar du konsolen **[!UICONTROL Samlingar]** :

Om du vill öppna **[!UICONTROL Samlingar]** trycker eller klickar du på Experience Manager-logotypen. From the navigation page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

## Skapa en samling {#create-a-collection}

Du kan skapa en samling med [statiska referenser](#create-a-collection-with-static-references) eller baserat på ett [sökkriteriebaserat filter](#create-a-smart-collection). Du kan också skapa en samling från en ljuslåda.

### Skapa en samling med statiska referenser {#create-a-collection-with-static-references}

Du kan skapa en samling med statiska referenser, t.ex. en samling med referenser till resurser, mappar, samlingar, snurrsuppsättningar och bilduppsättningar.

1. Gå till **[!UICONTROL samlingskonsolen]** .
1. Tryck/klicka på **[!UICONTROL Skapa]** i verktygsfältet.
1. Ange en rubrik och en valfri beskrivning för samlingen på sidan **[!UICONTROL Skapa samling]** .
1. Lägg till medlemmar i samlingen och tilldela lämpliga behörigheter. Alternatively, select **[!UICONTROL Public Collection]** to allow all users to access the collection.

   >[!NOTE]
   >
   >Om du vill att medlemmarna ska kunna dela samlingar med andra användare anger du gruppens läsbehörighet på sökvägen `dam-users` `home/users`. Ge användarna på `/content/dam/collections` platsen behörighet att visa samlingar i popup-listor. Du kan också göra användaren till en del av `dam-users` gruppen.

1. (Valfritt) Lägg till en miniatyrbild för samlingen.
1. Tap/click **[!UICONTROL Create]**, and then tap/click **[!UICONTROL OK]** to close the dialog. En samling med den angivna titeln och de angivna egenskaperna öppnas i konsolen Samlingar.

   >[!NOTE]
   >
   >Med Experience Manager Assets kan du skapa granskningsåtgärder för en samling på samma sätt som du skapar granskningsåtgärder för en resursmapp.

   Om du vill lägga till resurser i samlingen går du till användargränssnittet Resurser. Mer information finns i [Lägga till resurser i en samling](#add-assets-to-a-collection).

### Skapa samlingar med dropzone {#create-collections-using-dropzone}

Du kan dra resurser från resursgränssnittet till en samling. Du kan också skapa en kopia av en samling och dra resurserna dit.

1. I resursanvändargränssnittet väljer du de resurser som du vill lägga till i en samling.
1. Dra resurserna till zonen **[!UICONTROL Släpp i samling]** . Du kan också trycka/klicka på ikonen **[!UICONTROL Till samling]** i verktygsfältet.
1. Tryck/klicka på ikonen **[!UICONTROL Skapa samling]** i verktygsfältet på sidan **[!UICONTROL Lägg till i samling]** . If you want to add the assets to an existing collection, select it from the page, and tap/click **[!UICONTROL Add]**. Som standard väljs den senast uppdaterade samlingen.
1. In the **[!UICONTROL Create New Collection]** dialog, specify a name for the collection. If you want the collection to be accessible to all users, select **[!UICONTROL Public Collection]**.
1. Tryck/klicka på **[!UICONTROL Fortsätt]** för att skapa samlingen.

### Skapa en smart samling {#create-a-smart-collection}

En smart samling använder ett sökvillkor för att dynamiskt fylla i resurser. Du kan skapa en smart samling med enbart filer och inte med mappar eller filer och mappar.

1. Navigate to the Assets UI, and tap/click the **[!UICONTROL Search]** icon.
1. Ange sökordet i rutan Omni Search och tryck på Retur. Tryck/klicka på ikonen GlobalNav för att visa filterpanelen och använda ett sökfilter från sökpanelen.
1. I listan **[!UICONTROL Filer och mappar]** väljer du **[!UICONTROL Filer]**.
1. Tryck/klicka på **[!UICONTROL Spara smart samling]**.
1. Ange ett namn för samlingen. Välj **[!UICONTROL Offentlig]** om du vill lägga till gruppen DAM-användare med visningsprogramrollen i den smarta samlingen.

   >[!NOTE]
   >
   >Om du väljer **[!UICONTROL Offentlig]** blir den smarta samlingen tillgänglig för alla med rollen Ägare när du har skapat den. Om du avmarkerar alternativet **[!UICONTROL Offentlig]** är DAM-användargruppen inte längre kopplad till den smarta samlingen.

1. Tap/click **[!UICONTROL Save]** to create the smart collection, and then close the message box to complete the process. The new smart collection is also added to the **[!UICONTROL Saved Searches]** list.
Etiketten för knappen **[!UICONTROL Skapa smart markering]** ändras till **[!UICONTROL Redigera smart markering]**. To edit the settings of the smart collection, select **[!UICONTROL Files]** from the **[!UICONTROL Files &amp; Folders]** list. Tryck/klicka sedan på knappen **[!UICONTROL Redigera smart markering]** .

## Lägga till resurser i en samling {#add-assets-to-a-collection}

Du kan lägga till resurser i en samling som innehåller en lista med refererade resurser eller mappar.

>[!NOTE]
>
>Smarta samlingar använder en sökfråga för att fylla i resurser. Statiska referenser till resurser och mappar kan därför inte användas för dem.

1. I resursgränssnittet navigerar du till platsen för resursen som du vill lägga till i en samling.
1. Markera resursen och tryck/klicka på ikonen **[!UICONTROL Till samling]** i verktygsfältet. Du kan också dra resursen till zonen **[!UICONTROL Släpp i samling]** . Släpp musknappen när släppzonen blir aktiv och etiketten ändras till **[!UICONTROL Släpp för att lägga]** till.
1. På sidan **[!UICONTROL Lägg till i samling]** väljer du den samling du vill lägga till resursen i.
1. Tryck/klicka på **[!UICONTROL Lägg till]** och stäng sedan bekräftelsemeddelandet. Resursen läggs till i samlingen.

## Redigera en smart samling {#edit-a-smart-collection}

Smarta samlingar skapas genom att en sökning sparas så att du kan ändra deras innehåll genom att ändra sökparametrarna för den [sparade sökningen](#saved-searches).

1. Tryck/klicka på ikonen **[!UICONTROL Sök]** i verktygsfältet i användargränssnittet för Resurser.
1. Tryck på Retur med markören i rutan Omnisch.
1. Tryck/klicka på ikonen GlobalNav för att visa panelen Filter.
1. From the **[!UICONTROL Saved Searches]** list, select the smart collection you want to modify. På sökpanelen visas de filter som har konfigurerats för den sparade sökningen.
1. I listan **[!UICONTROL Filer och mappar]** väljer du **[!UICONTROL Filer]**.
1. Ändra ett eller flera filter efter behov. Tryck/klicka på **[!UICONTROL Redigera smart samling]**. Du kan också redigera namnet på den smarta samlingen.
1. Tryck/klicka på **[!UICONTROL Spara]**. Dialogrutan **[!UICONTROL Redigera smart samling]** visas.
1. Tryck/klicka på **[!UICONTROL Skriv över]** om du vill ersätta den ursprungliga smarta samlingen med den redigerade samlingen. Du kan också välja **[!UICONTROL Spara som]** om du vill spara den redigerade samlingen separat.
1. Tryck/klicka på **[!UICONTROL Spara]** i bekräftelsedialogrutan för att slutföra processen.

## Visa och redigera samlingsmetadata {#view-and-edit-collection-metadata}

Samlingsmetadata omfattar data om samlingen, inklusive taggar som läggs till.

1. Välj en samling i konsolen Samlingar och tryck/klicka på ikonen **[!UICONTROL Egenskaper]** i verktygsfältet.
1. In the **[!UICONTROL Collection Metadata]** page, view the collection metadata from the **[!UICONTROL Basic]** and **Advanced** tabs.
1. Ändra metadata efter behov och tryck/klicka sedan på **[!UICONTROL Spara och stäng]** i verktygsfältet för att spara ändringarna.

### Redigera samlingsmetadata {#edit-collection-metadata-in-bulk}

Du kan redigera metadata för flera samlingar samtidigt. Med den här funktionen kan du snabbt replikera vanliga metadata i flera samlingar.

1. I konsolen Samlingar väljer du två eller flera samlingar som du vill redigera metadata för.
1. Tryck/klicka på ikonen **[!UICONTROL Egenskaper]** i verktygsfältet.
1. På sidan Metadata för **[!UICONTROL samling]** redigerar du metadata på flikarna **[!UICONTROL Grundläggande]** och **[!UICONTROL Avancerat]** .
1. Tryck/klicka på **[!UICONTROL Spara och stäng]** i verktygsfältet och stäng sedan bekräftelsedialogrutan för att slutföra processen.
1. To append the new metadata with the existing metadata, select **[!UICONTROL Apend mode]**. Om du inte markerar det här alternativet ersätter de nya metadata de data som finns i fälten. Tryck/klicka på **[!UICONTROL Skicka]**.

   >[!NOTE]
   >
   >Tilläggsläget fungerar bara för fält som kan innehålla flera värden. For fields that can contain only a single value, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

## Sökning {#searching}

Sökfunktionen i samlingar har stöd för både [Söka efter samlingar](#search-collections) och [Söka efter resurser i en samling](#search-within-collections).

### Sök i samlingar {#search-collections}

Du kan söka efter samlingar från samlingskonsolen. När du söker med nyckelord i rutan Omnissearch söker AEM Resurser efter samlingsnamn, metadata och de taggar som har lagts till i samlingarna.

Om du söker efter samlingar från den översta nivån returneras bara enskilda samlingar i sökresultaten. Resurser eller mappar i samlingarna exkluderas. I alla andra fall (till exempel i en enskild samling eller i en mapphierarki) returneras alla relevanta resurser, mappar och samlingar.

### Sök i samlingar {#search-within-collections}

Tryck/klicka på en samling i Samlingar-konsolen för att öppna den.

I en samling är sökning efter AEM-resurser begränsad till resurser (och deras taggar och metadata) i den samling som du visar. När du söker i en mapp returneras alla matchande resurser och underordnade mappar i den aktuella mappen. När du söker i en samling returneras endast matchande resurser, mappar och andra samlingar som är direktmedlemmar i samlingen.

## Redigera samlingsinställningar {#edit-collection-settings}

Du kan redigera samlingsinställningar, till exempel rubrik och beskrivning, eller lägga till medlemmar i en samling.

1. Markera en samling och tryck/klicka på ikonen **[!UICONTROL Inställningar]** i verktygsfältet. Du kan även använda **[!UICONTROL snabbåtgärden Inställningar]** från samlingsminiatyrbilden.
1. Modify the collection settings in the **[!UICONTROL Collection Settings]** page. Du kan till exempel ändra samlingens titel, beskrivningar, medlemmar och behörigheter enligt beskrivningen i [Lägg till samlingar](#create-a-collection).
1. Tap/click **[!UICONTROL Save]** to save the changes.

## Ta bort en samling {#delete-a-collection}

1. Välj en eller flera samlingar i konsolen Samlingar och tryck/klicka på ikonen Ta bort i verktygsfältet.
1. Tryck/klicka på **[!UICONTROL Ta bort]** i dialogrutan för att bekräfta borttagningsåtgärden.

   >[!NOTE]
   >
   >Du kan också ta bort smarta samlingar genom att [ta bort sparade sökningar](#saved-searches).

## Hämta en samling {#download-a-collection}

När du hämtar en samling hämtas hela resurshierarkin i samlingen, inklusive mappar och underordnade samlingar.

1. Välj en eller flera samlingar som du vill hämta från samlingskonsolen.
1. Tryck/klicka på nedladdningsikonen i verktygsfältet.
1. I dialogrutan **[!UICONTROL Hämta]** trycker/klickar du på **[!UICONTROL Hämta]**. Om du vill hämta återgivningarna av resurserna i samlingen väljer du **[!UICONTROL Återgivningar]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   När du väljer en samling som ska hämtas hämtas hela mapphierarkin under samlingen. Om du vill inkludera varje samling som du hämtar (inklusive resurser i underordnade samlingar som är kapslade under den överordnade samlingen) i en enskild mapp väljer du **[!UICONTROL Skapa separata mappar för varje resurs]**.

## Redigera metadataegenskaper för flera samlingar {#editing-metadata-properties-of-multiple-collections}

Med Adobe Enterprise Manager (AEM) Assets kan du redigera flera samlingars metadata samtidigt. Använd sidan [!UICONTROL Egenskaper] om du vill göra metadataändringar i flera samlingar, till exempel ändra metadataegenskaper till ett gemensamt värde eller lägga till eller ändra taggar.

Om du vill anpassa [!UICONTROL egenskapssidan för] metadata, inklusive lägga till, ändra eller ta bort metadataegenskaper, använder du schemaredigeraren.

>[!NOTE]
>
>Massredigeringsmetoderna fungerar för resurser som är tillgängliga i en samling. För resurser som är tillgängliga i olika mappar eller som matchar ett gemensamt villkor är det möjligt att [uppdatera metadata satsvis efter sökning](/help/assets/search-assets.md#metadataupdates).

1. I samlingskonsolen väljer du de samlingar du vill redigera.
1. Tryck/klicka på **[!UICONTROL Egenskaper]** i verktygsfältet för att öppna sidan [!UICONTROL Egenskaper] för de valda samlingarna.
1. Ändra metadataegenskaperna för markerade samlingar under de olika flikarna.

   >[!NOTE]
   >
   >De metadata som du lägger till för de valda samlingarna skriver över tidigare metadata för dessa samlingar, med undantag för taggar. Alla taggar som du lägger till i fältet **[!UICONTROL Taggar]** läggs till i den befintliga listan med taggar i metadata.

1. Om du vill visa metadataegenskaperna för en viss samling avmarkerar du de återstående samlingarna i samlingslistan. Metadataredigeringsfälten fylls i med metadata för den aktuella samlingen.

   >[!NOTE]
   >
   >* På sidan med samlingsegenskaper kan du ta bort samlingar från listan med samlingar genom att avmarkera dem. I samlingslistan är alla samlingar markerade som standard. Metadata för samlingar som du tar bort uppdateras inte.
   >* Överst i listan markerar du kryssrutan vid **[!UICONTROL Titel]** för att växla mellan att markera samlingarna och rensa listan.


1. Spara ändringarna.

## Skapa kapslade samlingar {#create-nested-collections}

Du kan lägga till en samling i en annan samling och på så sätt skapa en kapslad samling.

1. Välj önskad samling eller grupp med samlingar i konsolen Samlingar och tryck eller klicka på **[!UICONTROL Till samling]** i verktygsfältet.
1. På sidan **[!UICONTROL Lägg till i samling]** väljer du den samling där samlingen ska läggas till.

   >[!NOTE]
   >
   >Den senast uppdaterade samlingen väljs som standard på sidan **[!UICONTROL Lägg till i samling]** .

1. Tryck/klicka på **[!UICONTROL Lägg till]**. Ett meddelande bekräftar att samlingen har lagts till i målsamlingen på sidan **[!UICONTROL Välj mål]** . Stäng meddelandet för att slutföra processen.

>[!NOTE]
>
>Smarta samlingar kan inte kapslas. Smarta samlingar kan alltså inte innehålla andra samlingar.

## Sparade sökningar {#saved-searches}

I Assets-gränssnittet kan du söka efter eller filtrera resurser baserat på vissa regler, sökvillkor eller anpassade sökfasetter. If you save these as **[!UICONTROL Saved Searches]**, you can access them later from the **[!UICONTROL Saved Searches]** list in the Filter panel. När du skapar en sparad sökning skapas även en smart samling.

Sparade sökningar skapas när du skapar en smart samling. Smart collections are automatically added to the **[!UICONTROL Saved Searches]** list. Frågan om sparade sökningar för samlingen sparas i egenskapen `dam:query` i CRXDE på den relativa sökvägen `/content/dam/collections/`.

>[!NOTE]
>
>Du kan dela smarta samlingar på samma sätt som du delar statiska samlingar.

Att redigera sparade sökningar är detsamma som att redigera smarta samlingar. Mer information finns i [Redigera en smart samling](#edit-a-smart-collection).

Så här tar du bort sparade sökningar:

1. I resursanvändargränssnittet: tryck/klicka på sökikonen i verktygsfältet.

1. Tryck på Retur när markören är i omsökningsfältet.
1. Klicka på eller tryck på ikonen GlobalNav för att visa filterpanelen.
1. From the **[!UICONTROL Saved Searches]** list, tap/click **[!UICONTROL Delete]** next to the smart collection you want to delete.
1. Tryck/klicka på **[!UICONTROL Ta bort]** i dialogrutan för att ta bort den sparade sökningen.

## Köra ett arbetsflöde i en samling {#run-a-workflow-on-a-collection}

Du kan köra ett arbetsflöde för resurserna i en samling. Om samlingen innehåller kapslade samlingar körs arbetsflödet även på resurserna i de kapslade samlingarna. Om samlingen och den kapslade samlingen innehåller duplicerade resurser körs arbetsflödet bara en gång för sådana resurser.

1. Välj en samling som du vill köra ett arbetsflöde för i samlingskonsolen.
1. Tryck/klicka på ikonen GlobalNav och välj **[!UICONTROL Tidslinje]** i listan.
1. Klicka eller tryck på cirkumflexikonen längst ned på tidslinjen och tryck/klicka sedan på **[!UICONTROL Starta arbetsflöde]**.
1. I avsnittet **[!UICONTROL Starta arbetsflöde]** väljer du en arbetsflödesmodell i listan. Välj till exempel modellen **[!UICONTROL DAM Update Asset]**.
1. Ange en titel för arbetsflödet och tryck/klicka på **[!UICONTROL Start]**.
1. Tryck/klicka på **[!UICONTROL Fortsätt]** i dialogrutan. Arbetsflödet körs på alla resurser i samlingen.

>[!MORELIKETHIS]
>
>* [Skapa en granskningsuppgift för samlingar](/help/assets/bulk-approval.md)

