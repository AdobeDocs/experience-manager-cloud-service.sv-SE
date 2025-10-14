---
title: Om dynamiska mediebildprofiler och videoprofiler
description: En bildprofil eller en videoprofil är ett recept på vilka alternativ som ska användas för resurser som du överför till en mapp. Du kan till exempel ange vilken videokodning som ska användas för de dynamiska medieresurser som du överför. Eller vilken bildprofil som ska användas för dynamiska mediebildresurser för att de ska beskäras ordentligt.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%

---

# Om dynamiska mediebildprofiler och videoprofiler{#about-dm-image-video-profiles}

En bildprofil eller videoprofil är ett recept på vilka alternativ som ska användas för resurser som du överför till en mapp. Du kan till exempel ange vilken videokodning som ska användas för de dynamiska medieresurser som du överför. Eller vilken bildprofil som ska användas för dynamiska mediebildresurser för att de ska beskäras ordentligt.

I Dynamic Media kan du skapa två typer av profiler som beskrivs närmare på följande länkar:

* [Dynamiska mediebildprofiler](/help/assets/dynamic-media/image-profiles.md)
* [Dynamiska videoprofiler för media](/help/assets/dynamic-media/video-profiles.md)

Se även [Metadataprofiler](/help/assets/metadata-profiles.md).

Du måste ha administratörsbehörighet för att skapa, redigera och ta bort dynamiska mediebildprofiler eller dynamiska medievideoprofiler.

När du har skapat din bildprofil eller videoprofil tilldelar du den till en eller flera mappar som du använder för nyligen överförda dynamiska medieresurser.

Se även [Bästa metoder för att ordna din digitala Assets för att använda Bearbeta profiler](/help/assets/organize-assets.md).


>[!NOTE]
>
>Assets som du flyttar från en mapp till en annan bearbetas inte om. Anta till exempel att du har Mapp 1 som har tilldelats profilen A och Mapp 2 som har profilen B tilldelad. Om du flyttar resurser från Mapp 1 till Mapp 2 behåller de flyttade resurserna sin ursprungliga bearbetning från Mapp 1.
>
>Detsamma gäller även när du flyttar resurser mellan två mappar som har samma profil tilldelad.

## Bearbeta dynamiskt mediematerial i en mapp igen {#reprocessing-assets}

Du kan bearbeta om resurser i en mapp som redan har en befintlig Dynamic Media Image Profile eller en Dynamic Media Video-profil som du senare ändrade.

Anta till exempel att du har skapat en dynamisk mediebildprofil och tilldelat den till en mapp. Bildprofiler som du överförde till mappen tillämpades automatiskt på resurserna. Men senare bestämmer du dig för att lägga till en ny smart beskärningsproportion i bildprofilen. I stället för att nu behöva välja och överföra resurserna till mappen igen kör du arbetsflödet *Dynamisk medieombearbetning*.

Du kan köra arbetsflödet för ombearbetning på en resurs som bearbetningen misslyckades för första gången. Även om du inte har redigerat en bildprofil eller videoprofil, eller redan har använt en bildprofil eller videoprofil, kan du köra arbetsflödet för ombearbetning på en mapp med resurser när som helst.

Du kan också justera batchstorleken för arbetsflödet för ombearbetning från standardvärdet 50 resurser upp till 1 000 resurser. När du kör arbetsflödet _Dynamisk medieombearbetning_ på en mapp grupperas resurserna i grupper och skickas sedan till Dynamic Media-servern för bearbetning. Efter bearbetning uppdateras metadata för varje resurs i hela gruppuppsättningen [!DNL Adobe Experience Manager]. Om gruppstorleken är stor kan bearbetningen fördröjas. Om gruppstorleken är för liten kan det orsaka för många rundningar till Dynamic Media-servern.

Se [Justera gruppstorleken för arbetsflödet för ombearbetning](#adjusting-load).

>[!NOTE]
>
>Om du utför en massmigrering av resurser från Dynamic Media Classic till [!DNL Experience Manager] aktiverar du migreringsreplikeringsagenten på den dynamiska medieservern. När migreringen är klar kontrollerar du att agenten är inaktiverad.
>
>Publiceringsagenten för migrering måste inaktiveras på Dynamic Media-servern så att arbetsflödet för ombearbetning fungerar som förväntat.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Så här bearbetar du om dynamiska medieresurser i en mapp:**

1. I [!DNL Experience Manager] navigerar du från Assets-sidan till en resursmapp som har en bildprofil eller en videoprofil tilldelad och för vilken du vill tillämpa arbetsflödet för **Dynamisk medieombearbetning**.

   Mappar som har tilldelats en bildprofil eller videoprofil visas med profilens namn direkt under mappnamnet i kortvyn.

1. Välj en mapp.

   * Arbetsflödet hanterar alla filer i den valda mappen rekursivt.
   * Om det finns en eller flera undermappar med resurser i den markerade huvudmappen, bearbetas alla resurser i mapphierarkin om i arbetsflödet.
   * Det är en god vana att undvika att köra det här arbetsflödet på en mapphierarki som har fler än 1 000 resurser.

1. I den nedrullningsbara listan i det övre vänstra hörnet av sidan väljer du **[!UICONTROL Timeline]**.
1. I närheten av sidans nedre vänstra hörn, till höger om fältet [!UICONTROL Comment], väljer du karikonen ( **^** ).

   ![Skärmbild av Assets i Experience Manager med en vald mapp med resurser, listrutan Tidslinje markerad, knappen Starta arbetsflöde markerad och karikonen till höger om fältet Kommentar markerad](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Välj **[!UICONTROL Start Workflow]**.
1. Välj **[!UICONTROL Dynamic Media Reprocess]** i listrutan **[!UICONTROL Start Workflow]**.
1. (Valfritt) Ange ett namn för arbetsflödet i textfältet **Ange arbetsflödets namn**. Du kan använda namnet för att referera till arbetsflödesinstansen, om det behövs.

   ![Skärmbild av tidslinjens användargränssnitt med &quot;Dynamisk medieombearbetning&quot; markerat i listrutan Starta arbetsflöde och knappen Start markerad](/help/assets/dynamic-media/assets/reprocess-assets2.png).

1. Välj **[!UICONTROL Start]** och sedan **[!UICONTROL Confirm]**.

   Om du vill övervaka arbetsflödet eller kontrollera förloppet väljer du **[!UICONTROL Tools > Workflow]** på huvudkonsolsidan för [!DNL Experience Manager]. Välj ett arbetsflöde på sidan Arbetsflödesinstanser. Välj **[!UICONTROL Open History]** på menyraden. Du kan också avsluta, göra uppehåll i eller byta namn på ett valt arbetsflöde från samma sida för arbetsflödesinstanser.

### Justera batchstorleken för arbetsflödet för ombearbetning (valfritt) {#adjusting-load}

(Valfritt) Standardbatchstorleken i ombearbetningsarbetsflödet är 50 resurser per jobb. Den optimala batchstorleken styrs av den genomsnittliga tillgångsstorleken och de MIME-typer av resurser som ombearbetningen körs på. Ett högre värde innebär att du har många filer i ett och samma ombearbetningsjobb. Bearbetningsbanderollen är alltså kvar på [!DNL Experience Manager] resurser under en längre tid. Om den genomsnittliga filstorleken är liten, 1 MB eller mindre, rekommenderar Adobe att du ökar värdet till flera 100, men aldrig mer än 1 000. Om den genomsnittliga filstorleken är hundratals MB rekommenderar Adobe att du minskar gruppstorleken med upp till 10.

**Om du vill justera gruppstorleken för arbetsflödet för ombearbetning:**

1. I [!DNL Experience Manager] väljer du **[!UICONTROL Adobe Experience Manager]** för att komma åt den globala navigeringskonsolen och väljer sedan **[!UICONTROL Tools]**-ikonen (hammare) > **[!UICONTROL Workflow > Models]**.
1. Välj **[!UICONTROL Dynamic Media Reprocess]** i kortvyn eller listvyn på sidan Arbetsflödesmodeller.

   ![Skärmbild av sidan Arbetsflödesmodeller med arbetsflödet &quot;Dynamic Media Reprocess&quot; markerat i kortvyn i Experience Manager](/help/assets/dynamic-media/assets/reprocess-assets7.png).

1. Välj **[!UICONTROL Edit]** i verktygsfältet. En ny flik i webbläsaren öppnar sidan Dynamisk medieombearbetning.
1. På sidan Dynamic Media Reprocess workflow, i det övre högra hörnet, väljer du **[!UICONTROL Edit]** för att låsa upp arbetsflödet.
1. I arbetsflödet väljer du komponenten Scene7 Batch Upload för att öppna verktygsfältet och väljer sedan **[!UICONTROL Configure]** i verktygsfältet.

   ![Skärmbild av komponenten &quot;Scene7 Batch Upload&quot; på sidan &quot;Dynamic Media Reprocess&quot; med muspekaren över ikonen &quot;Configure&quot; &#x200B;](/help/assets/dynamic-media/assets/reprocess-assets8.png).

1. Ange följande i dialogrutan **[!UICONTROL Batch Upload to Scene7—Step Properties]**:
   * I textfälten **[!UICONTROL Title]** och **[!UICONTROL Description]** anger du en ny titel och beskrivning för jobbet, om så önskas.
   * Välj **[!UICONTROL Handler Advance]** om hanteraren ska gå vidare till nästa steg.
   * I fältet **[!UICONTROL Timeout]** anger du tidsgränsen för den externa processen (sekunder).
   * I fältet **[!UICONTROL Period]** anger du ett avsökningsintervall (sekunder) som ska testas för att den externa processen ska slutföras.
   * I **[!UICONTROL Batch field]** anger du det maximala antalet resurser (50-1000) som ska bearbetas i ett batchbearbetningsjobb för en Dynamic Media-server.
   * Välj **[!UICONTROL Advance on timeout]** om du vill fortsätta när tidsgränsen nås. Avmarkera alternativet om du vill fortsätta till inkorgen när tidsgränsen nås.

   ![Skärmbild av sidan &quot;Gruppöverföring till scen7 - Stegegenskaper&quot; &#x200B;](/help/assets/dynamic-media/assets/reprocess-assets3.png).

1. Välj **[!UICONTROL Done]** i det övre högra hörnet i dialogrutan **[!UICONTROL Batch Upload to Scene7 – Step Properties]**.

1. Välj **[!UICONTROL Sync]** i det övre högra hörnet på sidan för arbetsflödesmodellen för ombearbetning av dynamiska media. När du ser **[!UICONTROL Synced]** synkroniseras arbetsflödets körningsmodell och kan bearbeta resurser i en mapp igen.

   ![Skärmbild av Assets i Experience Manager med en vald mapp med resurser, listrutan Tidslinje markerad, knappen Starta arbetsflöde markerad och karikonen till höger om fältet Kommentar markerad](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Stäng webbläsarfliken som visar arbetsflödesmodellen för dynamisk medieombearbetning.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.

-->
