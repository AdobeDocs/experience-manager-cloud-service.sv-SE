---
title: Hur publicerar eller avpublicerar man blanketter i förhandsgransknings- eller publiceringssammanhang?
description: Lär dig publicera och avpublicera formulär från AEM redigeringsmiljö för att förhandsgranska eller publicera instanser. Oavsett om du testar formulären i en staging-miljö eller distribuerar dem live för slutanvändare, har AEM smidiga verktyg för effektiv hantering av processen.
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
exl-id: 6ade40f1-bad5-4f5e-aa0e-84b7c6a82e02
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 0%

---


# &#x200B; Hantera publikation i Experience Manager Forms

Som administratör för Adobe Experience Manager (AEM) Forms kan du publicera formulär från författarinstansen till Experience Manager Forms. Du kan också schemalägga publiceringen av ett formulär eller en mapp för ett senare datum eller en senare tidpunkt. Efter publiceringen kan användarna öppna och fylla i formulären.

I Experience Manager Forms kan du publicera ett formulär på något av följande sätt:

* [Publiceringsalternativ](#publish-forms-using-the-publish-option)
* [Hantera publikation, alternativ](#publish-forms-using-the-manage-publication-option)

## Tänk på

* Endast medlemmar i gruppen `forms-users` kan använda alternativet **Hantera publikation** för att publicera formulären.
* Ändringar som görs i formulär eller mappar i Experience Manager Forms visas inte i instansen **Publish** förrän den publiceras på nytt. Detta garanterar att pågående uppdateringar inte är tillgängliga i instansen **Publish**. Endast ändringar som publicerats explicit av en administratör återspeglas i instansen **Publish**.

## Publicera formulär med alternativet Publicera

Med alternativet **Publicera** kan du publicera ett formulär direkt. Om du vill publicera ett Experience Manager-formulär med knappen **Publicera** i verktygsfältet. Så här publicerar du formulär med alternativet Publicera:

1. I Experience Manager Forms-konsolen går du till den överordnade mappen och väljer ett formulär som du vill publicera.
1. Klicka på alternativet **Publicera** i verktygsfältet och ta en titt på alla referensresurser som skulle publiceras med formuläret.
1. Klicka på **[!UICONTROL Publish]**.

   ![Publicera och avpublicera formulär](/help/edge/docs/forms/assets/publish-form-option.png)

   När formuläret och dess relaterade resurser har publicerats visas en dialogruta **Slutfört**.
1. Klicka på **Stäng**.

   ![Dialogrutan Slutfört](/help/forms/assets/publish-success1.png)

### Avpublicera formuläret

När du har publicerat formuläret med alternativet **Publicera** och dess relaterade resurser kan du även avpublicera det med knappen **[!UICONTROL Unpublish]** i verktygsfältet. Så här avpublicerar du formuläret:

1. Om du vill avpublicera formuläret och dess relaterade resurser markerar du formuläret och klickar på **[!UICONTROL Unpublish]** i verktygsfältet

   När du klickar på knappen **[!UICONTROL Unpublish]** visas dialogrutan **Avpublicera resurs**.
1. Klicka på **[!UICONTROL Unpublish]** för att starta avpubliceringsprocessen

   ![Dialogrutan Upprepa &#x200B;](/help/forms/assets/unpublish-asset.png)

   När formuläret och dess relaterade resurser har avpublicerats visas dialogrutan **Slutfört**.
1. Klicka på **Stäng**.

   ![avpubliceringen lyckades](/help/forms/assets/unpublishing-start.png)

## Publicera formulär med alternativet Hantera publikation

Med Hantera publikation kan du publicera eller avpublicera innehåll till och från det valda målet, lägga till innehåll i publiceringslistan från hela mappen `forms&documents`, välja referenser att publicera och schemalägga publicering till ett senare datum eller en senare tidpunkt.  Så här publicerar du formulär med alternativet **Hantera publikation**:

1. I Experience Manager Forms-konsolen går du till den överordnade mappen och väljer ett formulär som du vill publicera.
1. Klicka på alternativet **[!UICONTROL Manage Publication]** i verktygsfältet.

   ![Hantera publikation, alternativ](/help/forms/assets/manage-publication-option.png)

   Användargränssnittet **Hantera publikation** visas:

   ![Hantera publikation](/help/forms/assets/manage-publication.png)

   Följande alternativ är tillgängliga i användargränssnittet för **Hantera publikation**:

   * **Åtgärder**

      * **Publicera**: Publicera formulär till det valda målet
      * **Avpublicera**: Avpublicera formulär från målet

   * **Mål**

      * **Publicera**: Publicera formulär till publiceringsinstansen Experience Manager Forms (AEM).
      * **Förhandsgranska**: Publicera formulär till förhandsgranskningsinstansen för Experience Manager Forms (AEM).

   * **Schemaläggning**

      * **Nu**: Publicera formulär direkt
      * **Senare**: Publicera formulär baserat på **aktiveringsdatum** eller tid

1. Klicka på **Nästa** för att fortsätta.
1. (Valfritt) Använd alternativet **Lägg till innehåll** på fliken [Omfång](#add-content) för att lägga till mer innehåll för publicering. Du kan t.ex. lägga till fler Forms- eller dokumentfiler.
   ![fliken Omfång](/help/forms/assets/scope-tab.png)
1. Klicka på **[!UICONTROL Publish]** om du vill publicera formulären och tillhörande resurser och ett meddelande om att det lyckades visas.
   ![publicerade meddelande](/help/forms/assets/publish-successful.png)

### Lägg till innehåll

Genom att publicera i Experience Manager Forms kan du lägga till mer innehåll (formulär) i publiceringslistan.
Så här lägger du till fler formulär för publicering:

1. Klicka på knappen **Lägg till innehåll** om du vill lägga till mer innehåll.

   ![Lägg till innehåll](/help/forms/assets/add-content.png)

2. Markera formuläret på skärmen **Välj bana**.

   ![Lägg till innehåll](/help/forms/assets/add-assets.png)

   >[!NOTE]
   >
   > Du kan lägga till fler formulär eller mappar i listan från mappen `formsanddocuments`. Men du kan inte lägga till formulär från flera mappar samtidigt.

3. Om du vill konfigurera referenserna så att de publiceras eller inte publiceras för ett formulär, markerar du formuläret och klickar på **[!UICONTROL Published References]**.

   ![publicerade referenser](/help/forms/assets/published-references.png)

4. I dialogrutan **Publicerade referenser** avmarkerar du de resurser som du inte vill publicera och klickar på **[!UICONTROL Done]**.
   ![dialogrutan med publicerade referenser](/help/forms/assets/published-references-dialog.png)

<!--
### Include Folder Settings
By default, publishing a folder to Experience Manager Forms publishes all the assets, subfolders, and their references. To filter the folder for publishing:

1. Click **[Include Folder Settings]** to filter the folder.

    ![Include folder](/help/forms/assets/include-folder.png)

    The **[UICONTROL Include Folder Settings]** dialog appears. 
    
    ![Include folder dialog](/help/forms/assets/include-folder-dialog.png)
    
    The **[UICONTROL Include Folder Settings]** includes following options:

    * **[!UICONTROL Include folder contents]** checkbox. 
        * If selected, all forms and assets in the chosen folder, its subfolders (including all forms and assets within them), and references are published.
        * If not selected, only the forms and assets in the selected folder are published, while subfolder forms and assets are not.

    * **[!UICONTROL Include only immediate folder contents]** checkbox
        Selecting the **[!UICONTROL Include folder contents]** checkbox enables the **[!UICONTROL Include only immediate folder contents]** checkbox for selection.

        * If you select both options, all the forms and assets of the selected folder, subfolders (empty), and references are published. The forms and assets of the subfolders are not published.
        * -->


### Publicera eller avpublicera ett formulär senare

Förutom att du kan publicera eller avpublicera formulär vid ett senare datum och vid ett senare tillfälle kan du även konfigurera ett arbetsflöde med alternativet Publicera eller avpublicera senare. Formulären publiceras eller publiceras inte när arbetsflödet har slutförts.

Så här schemalägger du ett formulär för publicering eller avpublicering:

1. Gå till den överordnade mappen på Experience Manager Forms-konsolen och välj det formulär som du vill schemalägga för publicering.
1. Klicka på alternativet **[!UICONTROL Manage Publication]** i verktygsfältet.

   ![Hantera publikation](/help/forms/assets/manage-publication.png)

1. Klicka på **Publicera** eller **Avpublicera** från **[!UICONTROL Action]**.
1. Välj den **[!UICONTROL Destination]** där du vill publicera eller avpublicera innehållet.
   * **Förhandsgranska**: Använd alternativet **Förhandsgranska** om du vill publicera eller avpublicera i en Experience Manager Forms-förhandsvisningsmiljö. Experience Manager Forms förhandsvisningsmiljöer används för att testa under utvecklingsformulär.
   * **Publicera**: Använd alternativet Experience Manager Forms **Publicera** för att skicka formuläret till Experience Manager Forms publiceringsmiljö när formuläret är klart att användas i en produktionsmiljö.

1. Välj **[!UICONTROL Later]** från **Schemaläggning**.

   ![Hantera publikation senare](/help/forms/assets/manage-publication-later.png)

1. Välj en **[!UICONTROL Activation date]** och ange datum och tid.
1. Klicka på **[!UICONTROL Next]**.
1. (Valfritt) Lägg till innehåll med **på fliken** Omfång **[!UICONTROL Add Content]** .
   ![Hantera publikation, lägg till innehåll senare](/help/forms/assets/publish-later-add-content.png)
1. Klicka på **[!UICONTROL Next]**.
1. Ange **på fliken** Arbetsflöden **[!UICONTROL Workflow title]**.
1. Klicka på **[!UICONTROL Publish Later]**.

   ![Hantera publikationsarbetsflöde](/help/forms/assets/manage-publication-workflows.png)

## Bestämmer publiceringsstatus

Det finns flera sätt att avgöra publiceringsstatus:

* Logga in på målinstansen för att verifiera publicerade formulär och andra resurser (beroende på schemalagt datum eller tid).

* Använd tidslinjevyn för att bestämma publiceringsstatus.

* Använd sidinformationsmenyn i Adaptiv Forms-redigerare.
