---
title: Hur använder jag layoutläget för att ändra storlek på komponenter för anpassningsbara formulär?
description: Definiera placeringen av AEM Forms-komponenterna, lär dig komma åt layoutläget, ändra storlek på komponenter, ändra storlek på paneler och definiera layout med flera kolumner för en panel.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components
exl-id: 53896a8e-4568-460b-bca7-994baea0c8eb
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Använd layoutläget för att ändra storlek på komponenter för adaptiv Forms {#use-layout-mode-to-resize-components}

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/resize-using-layout-mode.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Med redigeringsgränssnittet Adaptivt formulär kan du ändra storlek på komponenter i layoutläget. Dra blå punkter i kolumner för att definiera start- och slutpunkterna för att placera komponenter. De blå punkterna visas när du har tryckt på komponenten i det responsiva rutnätet. Det responsiva rutnätet består av 12 lika stora kolumner. Den vita och blå färgskuggningen i alternativa kolumner skiljer den ena kolumnen från den andra.

Du kan använda layoutläget för att ändra storlek på komponenter för alla enhetstyper, som stationära datorer, surfplattor, telefoner och andra mindre enheter. Tabletten hämtar automatiskt layoutkonfigurationen från skrivbordsversionen och de mindre enheterna hämtar layoutkonfigurationen från telefonen. Du kan dock åsidosätta de automatiskt härledda konfigurationerna för att definiera olika konfigurationer för varje enhetstyp.

## Åtkomst till layoutläge {#access-layout-mode}

Välj **[!UICONTROL Layout]** i listrutan som visas högst upp i redigeringsgränssnittet för adaptiva formulär bredvid alternativet **[!UICONTROL Preview]**. Formuläret visas i layoutläget.

1. Logga in på [!DNL Adobe Experience Manager]-författarinstansen och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Skapa ett nytt eller öppna ett befintligt [anpassat formulär](creating-adaptive-form.md).
1. Välj **[!UICONTROL Layout]** i listrutan som visas högst upp bredvid alternativet **[!UICONTROL Preview]**. Formuläret visas i layoutläget.

   ![Layoutläge](assets/layout_mode_ic_new.png)

## Ändra storlek på komponenter {#resize-components}

1. Markera den komponent som du vill ändra storlek på i layoutläget. De blå punkterna visas i början och slutet av det responsiva rutnätet.
1. Dra och släpp de blå punkterna för att definiera placeringen av komponenten i det responsiva rutnätet.

   ![Ändra storlek i layoutläge](assets/layout_mode_resize_new_updated1.png)

   Verktygsfältet som visas när du har tryckt på komponenter består av följande alternativ:

   * **[!UICONTROL Parent]**: Välj den överordnade komponenten för en komponent.
   * **[!UICONTROL Revert breakpoint layout]**: Ångra alla ändringar av storleksändring och använd standardlayout på komponenten.
   * **[!UICONTROL Float to new line]**: Skift komponenten till nästa rad om det finns flera komponenter på samma rad.

   Du kan också använda alternativet **[!UICONTROL Revert breakpoint layout]** ( ![ Återställ brytpunkt ](assets/reverttopreviouslypublishedversion.png)) på panelnivå för att ångra alla ändringar av storleksändring.

   >[!NOTE]
   >
   >Du kan inte ändra storlek på tabellkolumn, verktygsfält, verktygsfältsknapp och målområdeskomponenter i layoutläget. Använd stilläget om du vill ändra storlek på de här komponenterna.

### Exempel {#example}

**Mål:** Du vill infoga en tabellkomponent och en bildkomponent och placera dem parallellt med varandra i ett adaptivt format.

1. Infoga tabell- och bildkomponenterna i läget [!UICONTROL Edit] i det adaptiva formuläret. Bildkomponenten visas efter tabellkomponenten.
1. Växla till läget [!UICONTROL Layout] och markera komponenten [!UICONTROL Table]. De blå punkter som komponentvisningen ska ändra storlek på i kolumnerna 1 och 12.
1. Dra den blå punkten i kolumn 12 till kolumn 6 i det responsiva rutnätet.

   ![Definiera tabellens slutpunkt](assets/layout_mode_end_point_table_new.png)

1. Markera på liknande sätt komponenten [!UICONTROL Image] och dra den blå punkten i kolumn 1 till kolumn 7 i det responsiva rutnätet. Tabellen och bildkomponenterna visas parallellt med varandra.

   ![Tabell och bilden parallellt i layoutläge](assets/table_image_parallel_new.png)

   Du kan markera bildkomponenten och välja alternativet **[!UICONTROL Float to new line]** i verktygsfältet för att flytta bildkomponenten till nästa rad.

## Ändra storlek på paneler {#resize-panels-layout-mode}

Utför följande steg om du vill ändra storlek på hela panelen i stället för enskilda komponenter:

1. Markera någon av komponenterna på panelen som du vill ändra storlek på, välj ![Markera överordnad](assets/select_parent_icon.svg) och välj det första alternativet i listrutan, om panelen är komponentens omedelbara överordnade.

   De blå punkterna visas i början och slutet av det responsiva rutnätet.

1. Dra och släpp de blå punkterna för att definiera panelens position i det responsiva rutnätet.
Du kan upprepa steg 1 och 2 och välja ![Välj överordnad](assets/float_to_new_line_icon.svg) för att flytta den storleksändrade panelen till nästa rad.

## Definiera layout med flera kolumner för en panel

Utför följande steg för att definiera antalet kolumner för en panel:

1. I läget **[!UICONTROL Edit]** markerar du panelen, väljer ![Konfigurera](assets/configure-icon.svg) och väljer **[!UICONTROL Responsive - everything on the page without navigation]** alternativ i listrutan **[!UICONTROL Panel Layout]**.

1. Välj ![Spara](assets/save_icon.svg) om du vill spara egenskaperna.

1. I **[!UICONTROL Layout]**-läget markerar du någon av komponenterna på panelen, väljer ![Markera överordnad](assets/select_parent_icon.svg) och markerar panelen.

1. Välj ![flera kolumner](assets/multi-column.svg) och välj antalet kolumner i listrutan. Antalet kolumner kan vara mellan 1 och 12. Panelen delas upp i en layout med flera kolumner.

![flera kolumner i layoutläge](assets/multi-column-layout.png)

## Aktivera det nya responsiva rutnätet för äldre responsiva layouter {#enableresponsivegrid}

Aktivera det nya responsiva stödrastret för formulär som du skapar med [!DNL Adobe Experience Manager] Forms 6.4 eller tidigare för att ändra storlek på komponenter.

>[!NOTE]
>
>När du växlar till det nya responsiva rutnätet tas de layoutegenskaper som redan har definierats bort för komponenter som används i formuläret.

Gör så här för att aktivera det nya responsiva rutnätet:

1. Välj **[!UICONTROL Layout]** i listrutan som visas högst upp bredvid alternativet **[!UICONTROL Preview]**. En bekräftelse som aktiverar layoutläget visas.
1. Välj **[!UICONTROL Yes]** om du vill aktivera **[!UICONTROL Layout]**-läget för formuläret.

### Bädda in ett gammalt fragment i ett adaptivt formulär med ny responsiv layout {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

Med den nya responsiva layouten för adaptiva formulär kan du lägga till ett adaptivt formulärfragment med den gamla responsiva layouten i formuläret. Den nya layouten tar dock bort de layoutegenskaper som redan har definierats för komponenter som används i fragmentet. Du kan växla till layoutläget för att definiera layoutegenskaperna för komponenter som används i fragmentet.

### Bädda in ett fragment med ny responsiv layout i ett gammalt adaptivt format {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Om du bäddar in ett fragment med den nya responsiva layouten i ett adaptivt formulär med en gammal responsiv layout uppmanas du att aktivera layoutläget för formuläret och bädda in fragmentet igen.

Om du vill aktivera layoutläget väljer du **[!UICONTROL Layout]** i listrutan som visas högst upp bredvid alternativet **[!UICONTROL Preview]** och väljer **[!UICONTROL Yes]** för att bekräfta. Välj läget **[!UICONTROL Edit]** om du vill bädda in fragmentet igen.

## Inaktivera layoutläget för formulär med gammal responsiv layout {#disable-layout-mode-for-forms-with-old-responsive-layout}

Du kan inaktivera layoutläget för formulär med äldre responsiv layout genom att redigera egenskaperna för mallen som används i formuläret.

Utför följande steg för att inaktivera layoutläget:

1. Välj **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Templates]** och öppna mallen som används i formuläret i **[!UICONTROL Edit]**-läge.
1. Markera formulärbehållaren i den vänstra rutan och välj **[!UICONTROL Policy]**.

   ![Inaktivera layoutläge](assets/policy_disable_layout_mode.png)

1. Välj fliken **[!UICONTROL Layout Settings]** och välj **[!UICONTROL Disable Layout Mode]**.
1. Välj ![Spara ändringar](assets/save_icon.svg) om du vill spara mallegenskaperna.

## Se även {#see-also}

{{see-also}}