---
title: Resursrelationer
description: Lär dig hur du relaterar digitala resurser som delar vissa gemensamma attribut. Skapa också källbaserade relationer mellan digitala resurser med hjälp av resursrelationer.
role: User
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 77dab2731f8d442bf999bf1614ef060944794574
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Resursrelationer {#related-assets}

Med [!DNL Adobe Experience Manager Assets] kan du manuellt relatera resurser baserat på organisationens behov med hjälp av funktionen för relaterade resurser. Du kan till exempel relatera en licensfil till en resurs eller en bild/video på ett liknande ämne. Du kan relatera resurser som delar vissa gemensamma attribut. Du kan också använda funktionen för att skapa käll-/härledda relationer mellan resurser. Om du till exempel har en PDF-fil som genereras från en INDD-fil kan du koppla PDF-filen till dess INDD-källfil.

Med den här funktionen kan du dela en lågupplöst PDF- eller JPG-fil med leverantörer eller byråer och göra den högupplösta INDD-filen tillgänglig endast på begäran.

>[!NOTE]
>
>Endast användare med redigeringsbehörighet för resurser kan relatera och ta bort kopplingen för resurserna.

## Steg för att relatera tillgångar {#steps-to-relate-assets}

1. Öppna sidan **[!UICONTROL Properties]** i gränssnittet [!DNL Experience Manager] för en resurs som du vill relatera.

   ![öppnar sidan Egenskaper för en resurs för att relatera resursen](assets/asset-properties-relate-assets.png)

1. Om du vill relatera en annan resurs till den valda resursen klickar du på **[!UICONTROL Asset Relations]** ![Relatera resurser](assets/do-not-localize/link-relate.png).
1. Gör något av följande:

   * Om du vill relatera källfilen för resursen väljer du **[!UICONTROL Add Source]** i listan. Du kan bara associera en enskild resurs som en källa.
   * Om du vill relatera en härledd fil väljer du **[!UICONTROL Add Derived]** i listan. Du kan associera flera resurser i den här kategorin.
   * Om du vill skapa en dubbelriktad relation mellan resurserna väljer du **[!UICONTROL Add Other]** i listan. Du kan associera flera resurser i den här kategorin.

1. På skärmen **[!UICONTROL Select Assets]** navigerar du till platsen för resursen som du vill relatera och markerar den. Du kan markera en enskild resurs i taget eller flera resurser genom att hålla ned skifttangenten samtidigt som du klickar, vilket kan innehålla något av de [filformat som stöds i Assets View](/help/assets/supported-file-formats-assets-view.md).

   ![lägg till relaterad resurs](assets/add-related-asset.png)

1. Klicka på **[!UICONTROL Select]**. Beroende på ditt val av relation i steg 3 listas den relaterade resursen under en lämplig kategori i avsnittet **[!UICONTROL Asset Relations]**. Om resursen du relaterade till till till exempel är källfilen för den aktuella resursen visas den under **[!UICONTROL Source]**.

   ![Exempel på Assets-relation](assets/asset-relations-example.png)

1. Klicka på **[!UICONTROL Unrelate]** ![Ej relaterade resurser](assets/do-not-localize/link-unrelate-icon.png) som är tillgängliga för alla relaterade resurser i varje avsnitt ([!UICONTROL Source], [!UICONTROL Derived] och [!UICONTROL Other]) för att ta bort kopplingen för en resurs.

## Översätta relaterade resurser {#translating-related-assets}

Det är också praktiskt att skapa käll-/härledda relationer mellan resurser med hjälp av funktionen för relaterade resurser i översättningsarbetsflöden. När du kör ett översättningsarbetsflöde på en härledd resurs hämtar [!DNL Experience Manager Assets] automatiskt alla resurser som källfilen refererar till och inkluderar dem för översättning. På så sätt översätts den resurs som källresursen refererar till tillsammans med källresursen och de härledda resurserna. Om källfilen är relaterad till en annan resurs hämtar [!DNL Experience Manager Assets] den refererade resursen och inkluderar den för översättning.

Se [Översätta resurser i AEM](/help/assets/translate-assets.md).

## Nästa steg {#next-steps}

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/sv?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Visa versioner av en resurs](/help/assets/manage-organize-assets-view.md#view-versions)
>* [Översätt resurser i AEM](/help/assets/translate-assets.md)
>* [Filformat som stöds i Assets View](/help/assets/supported-file-formats-assets-view.md).
