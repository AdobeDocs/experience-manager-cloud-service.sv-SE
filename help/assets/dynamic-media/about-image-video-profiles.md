---
title: Om dynamiska mediebildprofiler och videoprofiler
description: En bildprofil eller en videoprofil är ett recept på vilka alternativ som ska användas för resurser som du överför till en mapp. Du kan till exempel ange vilken videokodning som ska användas för de dynamiska medieresurser som du överför. Eller vilken bildprofil som ska användas för dynamiska mediebildresurser för att de ska beskäras ordentligt.
translation-type: tm+mt
source-git-commit: 4fc5ae2aba6a19f37127f795e563a3d079e06bbb
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 2%

---


# Om dynamiska mediebildprofiler och videoprofiler{#about-dm-image-video-profiles}

En bildprofil eller videoprofil är ett recept på vilka alternativ som ska användas för resurser som du överför till en mapp. Du kan till exempel ange vilken videokodning som ska användas för de dynamiska medieresurser som du överför. Eller vilken bildprofil som ska användas för dynamiska mediebildresurser för att de ska beskäras ordentligt.

I Dynamic Media kan du skapa två typer av profiler som beskrivs närmare på följande länkar:

* [Dynamiska mediebildprofiler](/help/assets/dynamic-media/image-profiles.md)
* [Dynamiska videoprofiler för media](/help/assets/dynamic-media/video-profiles.md)

Se även [Metadataprofiler](/help/assets/metadata-profiles.md).

Du måste ha administratörsbehörighet för att skapa, redigera och ta bort dynamiska mediebildprofiler eller dynamiska medievideoprofiler.

När du har skapat din bildprofil eller videoprofil tilldelar du den till en eller flera mappar som du använder som mål för nyligen överförda dynamiska medieresurser.

Se även [Bästa metoder för att ordna dina digitala resurser så att du kan använda bildprofiler eller videoprofiler](/help/assets/dynamic-media/best-practices-for-file-management.md).

>[!NOTE]
>
>Resurser som du flyttar från en mapp till en annan bearbetas inte om. Anta till exempel att du har Mapp 1 som har tilldelats profilen A och Mapp 2 som har profilen B tilldelad. Om du flyttar resurser från Mapp 1 till Mapp 2 behåller de flyttade resurserna sin ursprungliga bearbetning från Mapp 1.
>
>Detsamma gäller även när du flyttar resurser mellan två mappar som har samma profil tilldelad.

## Bearbetar dynamiska medieresurser i en mapp {#reprocessing-assets}

Du kan bearbeta om resurser i en mapp som redan har en befintlig Dynamic Media Image Profile eller en Dynamic Media Video-profil som du senare ändrade.

Anta till exempel att du har skapat en dynamisk mediebildprofil och tilldelat den till en mapp. Bildprofiler som du överförde till mappen tillämpades automatiskt på resurserna. Men senare bestämmer du dig för att lägga till en ny smart beskärningsproportion i bildprofilen. I stället för att nu ha markerat och laddat upp resurserna till mappen igen kör du bara *Scene7: Bearbeta om arbetsflödet Resurser*.

Du kan köra arbetsflödet för ombearbetning på en resurs som bearbetningen misslyckades för första gången. Även om du inte har redigerat en bildprofil eller videoprofil, eller redan har använt en bildprofil eller en videoprofil, kan du ändå köra arbetsflödet för ombearbetning på en mapp med resurser när som helst.

Du kan också justera batchstorleken för arbetsflödet för ombearbetning från standardvärdet 50 resurser upp till 1 000 resurser. När du kör _Scene7: Återbearbeta resurser_-arbetsflöde i en mapp, resurser grupperas tillsammans i grupper och skickas sedan till Dynamic Media-servern för bearbetning. Efter bearbetning uppdateras metadata för varje resurs i hela gruppuppsättningen AEM. Om batchstorleken är mycket stor kan bearbetningen fördröjas. Om gruppstorleken är för liten kan det orsaka för många rundresor till Dynamic Media-servern.

Se [Justera batchstorleken för arbetsflödet för ombearbetning](#adjusting-load).

>[!NOTE]
>
>Om du utför en massmigrering av resurser från Dynamic Media Classic till Experience Manager måste du aktivera migreringsreplikeringsagenten på Dynamic Media-servern. När migreringen är klar kontrollerar du att agenten är inaktiverad.
>
>Migreringens publiceringsagent måste inaktiveras på Dynamic Media-servern så att arbetsflödet för ombearbetning fungerar som förväntat.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Så här bearbetar du om dynamiska medieresurser i en mapp**:
1. I Adobe Experience Manager navigerar du från Assets-sidan till en mapp med dynamiska medieresurser som har en bildprofil eller en videoprofil tilldelad och för vilken du vill använda **Scene7: Arbetsflöde för att bearbeta om resurs**,

   Mappar som redan har tilldelats en bildprofil eller en videoprofil visas genom att profilens namn visas direkt under mappnamnet i kortvyn.

1. Välj en mapp.

   * Arbetsflödet hanterar alla filer i den valda mappen rekursivt.
   * Om det finns en eller flera undermappar med resurser i den markerade huvudmappen bearbetas alla resurser i mapphierarkin igen.
   * Som en god vana bör du undvika att köra det här arbetsflödet på en mapphierarki som har fler än 1 000 resurser.

1. Klicka på **[!UICONTROL Timeline]** i listrutan nära sidans övre vänstra hörn.
1. Klicka på karikonen ( **^** ) nära sidans nedre vänstra hörn till höger om kommentarsfältet.

   ![Bearbeta resursarbetsflöde 1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Klicka på **[!UICONTROL Start Workflow]**.
1. Välj **[!UICONTROL Scene7: Reprocess Assets]** i listrutan **[!UICONTROL Start Workflow]**.
1. (Valfritt) Ange ett namn för arbetsflödet i **textrutan**. Du kan använda namnet för att referera till arbetsflödesinstansen, om det behövs.

   ![Bearbeta resurser 2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. Klicka på **[!UICONTROL Start]** och sedan på **[!UICONTROL Confirm]**.

   Om du vill övervaka arbetsflödet eller kontrollera förloppet går du till huvudkonsolsidan för Experience Manager och klickar på **[!UICONTROL Tools > Workflow]**. Välj ett arbetsflöde på sidan Arbetsflödesinstanser. Klicka på **[!UICONTROL Open History]** på menyraden. Du kan också avsluta, göra uppehåll i eller byta namn på ett valt arbetsflöde från samma sida för arbetsflödesinstanser.

### Justera batchstorleken för arbetsflödet för ombearbetning {#adjusting-load}

(Valfritt) Standardbatchstorleken i ombearbetningsarbetsflödet är 50 resurser per jobb. Den optimala batchstorleken styrs av den genomsnittliga tillgångsstorleken och de Mime-typer av resurser som ombearbetningen körs på. Ett högre värde innebär att du kommer att ha många filer i ett och samma ombearbetningsjobb. Bearbetningsbanderollen ligger alltså kvar på Experience Manager resurser under en längre tid. Om den genomsnittliga filstorleken är liten-1 MB eller mindre-Adobe rekommenderar du att du ökar värdet till flera hundra, men aldrig mer än 1 000. Om den genomsnittliga filstorleken är stor-hundratals megabyte-Adobe rekommenderar du att du minskar gruppstorleken upp till 10.

**Om du vill justera batchstorleken för arbetsflödet för ombearbetning**

1. I Experience Manager trycker du på **[!UICONTROL Adobe Experience Manager]** för att komma åt den globala navigeringskonsolen och sedan på **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Workflow > Models]**.
1. Välj **[!UICONTROL Scene7: Reprocess Assets]** i kortvyn eller listvyn på sidan Arbetsflödesmodeller.

   ![Workflow Models page with Scene7: Arbetsflödet för att bearbeta resurser som valts i kortvyn](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. Klicka på **[!UICONTROL Edit]** i verktygsfältet. En ny flik i webbläsaren öppnar Scene7: Sidan med arbetsflödesmodellen Återbearbeta resurser.
1. På Scene7: Återbearbeta arbetsflödessidan Resurser, i det övre högra hörnet, tryck på **[!UICONTROL Edit]** för att låsa upp arbetsflödet.
1. Öppna verktygsfältet genom att välja Scene7 Batch Upload-komponenten i arbetsflödet och tryck sedan på **[!UICONTROL Configure]** i verktygsfältet.

   ![Komponenten Scene7 Batch Upload](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. Ange följande i dialogrutan **[!UICONTROL Batch Upload to Scene7—Step Properties]**:
   * I textfälten **[!UICONTROL Title]** och **[!UICONTROL Description]** anger du en ny titel och beskrivning för jobbet, om du vill.
   * Välj **[!UICONTROL Handler Advance]** om hanteraren ska gå vidare till nästa steg.
   * I fältet **[!UICONTROL Timeout]** anger du timeout för extern process (sekunder).
   * I fältet **[!UICONTROL Period]** anger du ett avsökningsintervall (sekunder) som ska testas för att den externa processen ska slutföras.
   * I **[!UICONTROL Batch field]** anger du det maximala antalet resurser (50-1000) som ska bearbetas i ett batchbearbetningsjobb för en Dynamic Media-server.
   * Välj **[!UICONTROL Advance on timeout]** om du vill fortsätta när tidsgränsen nås. Avmarkera alternativet om du vill fortsätta till inkorgen när tidsgränsen nås.

   ![Egenskaper, dialogruta](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. Tryck på **[!UICONTROL Done]** i det övre högra hörnet av dialogrutan **[!UICONTROL Batch Upload to Scene7 – Step Properties]**.

1. I det övre högra hörnet av Scene7: Återbearbeta arbetsflödesmodellsidan Resurser, tryck på **[!UICONTROL Sync]**. När du ser **[!UICONTROL Synced]** är arbetsflödets körningsmodell synkroniserad och klar att bearbeta resurser i en mapp igen.

   ![Synkronisera arbetsflödesmodellen](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Stäng webbläsarfliken som visar Scene7: Arbetsflödesmodellen Återbearbeta resurser.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
