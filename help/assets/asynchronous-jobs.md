---
title: Asynkrona åtgärder
description: AEM Assets optimerar prestanda genom att utföra vissa resurskrävande uppgifter asynkront.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# Asynkrona åtgärder {#asynchronous-operations}

För att minska den negativa inverkan på prestandan bearbetar Adobe Experience Manager Assets vissa långvariga och resurskrävande resursoperationer asynkront.

Dessa åtgärder omfattar:

* Tar bort många resurser
* Flytta många resurser eller resurser med många referenser
* Exporterar/importerar resursmetadata i grupp.
* Hämtar resurser, som ligger över den angivna tröskelgränsen, från en fjärr-AEM-distribution.

Asynkron bearbetning innebär att du måste placera flera jobb i kö och sedan köra dem på ett seriellt sätt beroende på om det finns systemresurser tillgängliga.

Du kan visa status för asynkrona jobb på sidan **[!UICONTROL Async Job Status]** .

>[!NOTE]
>
>Som standard körs jobb i AEM Resurser parallellt. Om N är antalet processorkärnor kan N/2-jobb köras parallellt som standard. Om du vill använda anpassade inställningar för jobbkön ändrar du konfigurationen av standardkön för **asynkron åtgärd** från webbkonsolen. Mer information finns i [Kökonfigurationer](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Övervaka status för asynkrona åtgärder {#monitoring-the-status-of-asynchronous-operations}

När AEM Resurser bearbetar en åtgärd asynkront får du ett meddelande i din inkorg <!-- and through email -->.

Om du vill visa status för asynkrona åtgärder i detalj går du till sidan **[!UICONTROL Async Job Status]** .

1. Tap/click the AEM logo, and go **[!UICONTROL Assets]** > **[!UICONTROL Jobs]**.
1. Granska informationen om åtgärderna på sidan **[!UICONTROL Async Job Status]** .

   ![job_status](assets/job_status.png)

   Information om förloppet för en viss åtgärd finns i värdet i kolumnen **[!UICONTROL Status]** . Beroende på förloppet visas ett av följande statusvärden:

   **[!UICONTROL Aktiv]**: Åtgärden bearbetas

   **[!UICONTROL Slutfört]**: Åtgärden har slutförts

   **[!UICONTROL Fel]** eller **[!UICONTROL fel]**: Det gick inte att bearbeta åtgärden

   **[!UICONTROL Schemalagd]**: Åtgärden är schemalagd för bearbetning vid ett senare tillfälle

1. Om du vill avbryta en aktiv åtgärd markerar du den i listan och trycker/klickar på **[!UICONTROL stoppikonen]** i verktygsfältet.

   ![stop_icon](assets/stop_icon.png)

1. Om du vill visa extra information, till exempel beskrivning och loggar, markerar du åtgärden och trycker/klickar på ikonen **[!UICONTROL Öppna]** i verktygsfältet.

   ![open_icon](assets/open_icon.png)

   Sidan med jobbinformation visas.

   ![job_details](assets/job_details.png)

1. Om du vill ta bort åtgärden från listan väljer du **[!UICONTROL Ta bort]** i verktygsfältet. Om du vill hämta information i en CSV-fil trycker/klickar du på ikonen **[!UICONTROL Hämta]** .

   >[!NOTE]
   >
   >Du kan inte ta bort ett jobb om dess status är aktiv eller köad.

## Tömmer slutförda jobb {#purging-completed-jobs}

AEM Assets kör ett rensningsjobb varje dag klockan 1:00 för att ta bort slutförda asynkrona jobb som är mer än en dag gamla.

Du kan ändra schemat för rensningsjobbet och hur länge detaljer om slutförda jobb behålls innan de tas bort. Du kan också konfigurera det maximala antalet slutförda jobb för vilka information sparas när som helst.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna det schemalagda **[!UICONTROL rensningsjobbet för]** Adobe CQ DAM Async Jobs.
1. Ange tröskelvärdet för antal dagar efter vilka slutförda jobb tas bort och det maximala antalet jobb för vilka information sparas i historiken.

   ![Konfiguration för att schemalägga rensning av asynkrona jobb](assets/configmgr_purge_asyncjobs.png)
   *Bild: Konfiguration för att schemalägga rensning av asynkrona jobb*

1. Spara ändringarna.

## Konfigurera tröskelvärden för asynkron bearbetning {#configuring-thresholds-for-asynchronous-processing}

Du kan konfigurera tröskelvärdet för antal resurser eller referenser för AEM Resurser för att bearbeta en viss åtgärd asynkront.

### Konfigurera tröskelvärden för asynkrona borttagningsåtgärder {#configuring-thresholds-for-asynchronous-delete-operations}

Om antalet resurser eller mappar som ska tas bort överstiger tröskelvärdet, utförs borttagningsåtgärden asynkront.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna konfigurationen för **[!UICONTROL Async Delete Operation Job Processing]** i webbkonsolen.
1. I rutan **[!UICONTROL Tröskelvärde för antal resurser]** anger du tröskelvärdet för antal resurser/mappar för asynkron bearbetning av borttagningsåtgärder.

   ![delete_threshold](assets/delete_threshold.png)

1. Spara ändringarna.

### Konfigurera tröskelvärden för asynkrona flyttåtgärder {#configuring-thresholds-for-asynchronous-move-operations}

Om antalet resurser/mappar eller referenser som ska flyttas överstiger tröskelvärdet, utförs flyttåtgärden asynkront.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna konfigurationen för **[!UICONTROL Async Move Operation Job Processing]** i webbkonsolen.
1. I rutan **[!UICONTROL Tröskelvärde för antal resurser/referenser]** anger du tröskelvärdet för antal resurser/mappar eller referenser för asynkron bearbetning av flyttåtgärder.

   ![move_threshold](assets/move_threshold.png)

1. Spara ändringarna.
