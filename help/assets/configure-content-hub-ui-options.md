---
title: Konfigurera Content Hub användargränssnitt
description: Konfigurera Content Hub användargränssnitt
exl-id: e9e22862-9bcd-459a-bcf4-7f376a0b329a
source-git-commit: deeb1487ce51f2a91e556b32f9db2a644656d828
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Konfigurera Content Hub användargränssnitt {#configure-content-hub-user-interface}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!CONTEXTUALHELP]
>id="configure_content_hub"
>title="Konfigurera Content Hub användargränssnitt"
>abstract="Med Experience Manager Assets kan administratörer konfigurera de alternativ som finns i Content Hub användargränssnitt. Baserat på de konfigurationsalternativ som valts av administratörer kan Content Hub-användare visa fält på Content Hub. Konfigurationsalternativen inkluderar metadata vid import av resurser, filter, resursegenskaper, metadata vid sökning av resurser, anpassad varumärkning och eventuella anpassade länkar."
>additional-url="https://images-tv.adobe.com/mpcv3/4477/74a81d1c-0cfe-41f4-8a06-18ff70604e45_1732023385.854x480at800_h264.mp4" text="Titta på videon"

<!-- ![Download assets](assets/download-asset.jpg) -->
![Konfigurera resurser på Content Hub](assets/configure-assets.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Med Experience Manager Assets kan administratörer konfigurera de alternativ som finns i Content Hub användargränssnitt. Baserat på de konfigurationsalternativ som valts av administratörer kan Content Hub-användare visa fält på Content Hub. Konfigurationsalternativen är:

* Filter som är tillgängliga för användare när de söker efter resurser.

* Tillgångsinformation eller egenskaper som är tillgängliga för varje resurs.

* Metadatafält som är tillgängliga för användare när resurser läggs till i Content Hub.

* Metadatafält för resurser som är tillgängliga för sökning i Content Hub.

* Varumärkesinnehåll som du behöver visa för din organisation.

* Alla anpassade länkar som du behöver inkludera på Content Hub förutom resurser, samlingar och insikter.

## Förutsättningar {#prerequisites-configuration-ui}

[Content Hub-administratörer](/help/assets/deploy-content-hub.md#step-3-onboard-content-hub-administrator) kan ange konfigurationsalternativ för andra användare i organisationen.

## Få åtkomst till konfigurationsalternativ på Content Hub {#access-configuration-options-content-hub}

Så här öppnar du konfigurationsalternativ på Content Hub:

1. Klicka på användarikonen i den högra rutan.

1. Välj **[!UICONTROL Configurations]** i avsnittet **[!UICONTROL Product Settings]**.

   ![Få åtkomst till konfigurationsalternativ på Content Hub](assets/access-content-hub-configuration-ui.png)

## Hantera konfigurationsalternativ på Content Hub {#manage-configuration-options}

Som administratör hanterar du följande konfigurationsalternativ för dina användare:

* [Importera](#configure-import-options-content-hub)

* [Filter](#configure-filters-content-hub)

* [Resursinformation](#configure-asset-details-content-hub)
* [Tillgångskort](#asset-card)

* [Sök](#configure-metadata-search-content-hub)

* [Varumärke](#configure-branding-content-hub)

* [Assets har gått ut](#expired-assets-content-hub)

* [Återgivningar](#renditions-content-hub)

* [Anpassade länkar](#configure-custom-links-content-hub)

### Importera {#configure-import-options-content-hub}

Du kan konfigurera metadatafält som visas för användarna när du överför eller importerar resurser till Content Hub-portalen, till exempel kampanjnamn, nyckelord, kanaler, tidsram, region och så vidare. Gör så här:

1. Klicka på **[!UICONTROL Import]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).

1. Klicka på **[!UICONTROL Add metadata]**.

1. Ange en etikett för egenskapen, mappa den till en egenskap med hjälp av fältet **[!UICONTROL Metadata]** och välj indatatypen för de nya metadata för resursen.

1. Klicka på växlingsknappen **[!UICONTROL Required field]** för att göra det nya metadatafältet obligatoriskt att ange för användare när nya resurser överförs.

1. Klicka på **[!UICONTROL Confirm]**. De nya metadata visas i listan över befintliga resursegenskaper.

1. Klicka på **[!UICONTROL Save]** för att tillämpa ändringarna.

På samma sätt kan du klicka på ikonen ![Redigera](assets/do-not-localize/edit_icon.svg) , som finns bredvid varje tillgänglig egenskap, om du vill redigera etiketterna, göra dessa fält obligatoriska eller icke-obligatoriska för användare när du överför resurser med hjälp av växlingsknappen **[!UICONTROL Required field]** eller klicka på ikonen Ta bort om du vill ta bort en metadataegenskap.

Klicka på växlingsknappen **[!UICONTROL Auto-approval]** om du vill att alla resurser som du lägger till i Experience Manager Assets-databasen ska godkännas automatiskt så att de är tillgängliga i Content Hub direkt. Annars måste DAM-författare eller -administratörer manuellt godkänna mediefilerna för att göra dem tillgängliga på Content Hub. Växlingsknappen är som standard inställd på Av.

Klicka på **[!UICONTROL Save]** när du har gjort alla ändringar för att tillämpa ändringarna.

![Överföringsinformation för konfigurationsgränssnittet på Content Hub](assets/configuration-ui-upload-details.png)

Metadata är aktiverade i konfigurationsanvändargränssnittet på sidan för överföring av resurser:

![Överför metadata på Content Hub](assets/configuration-ui-add-assets.png)

### Filter {#configure-filters-content-hub}

I Content Hub kan administratörer konfigurera filter som visas när de söker efter resurser. Utför följande steg för att lägga till ett nytt filter:

1. Klicka på **[!UICONTROL Filters]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).

1. Klicka på **[!UICONTROL Add filters]**.

1. Ange en etikett för filtret, mappa det till en egenskap med fältet **[!UICONTROL Metadata]** och välj indatatypen för det nya filtret.
1. Klicka på **[!UICONTROL Confirm]**. Det nya filtret visas i listan över befintliga filter.

1. Klicka på **[!UICONTROL Save]** om du vill använda ändringarna så att det nya filtret visas på söksidan när du filtrerar resurser.

   >[!NOTE]
   >
   Det nya filtret visas bara på söksidan om det finns minst en resurs i databasen som matchar filtervillkoren.

På samma sätt kan du klicka på ikonen ![Redigera](assets/do-not-localize/edit_icon.svg), som finns bredvid varje tillgängligt filter, för att redigera etiketterna eller klicka på ikonen Ta bort för att ta bort befintliga filter. Klicka på **[!UICONTROL Save]** när du har gjort alla ändringar för att tillämpa ändringarna.

![Gränssnittsfilter för konfiguration på Content Hub](assets/configuration-ui-filters.png)

De filter som är aktiverade i konfigurationsanvändargränssnittet visas på söksidan:

![Sök på Content Hub](assets/filters-for-search.png)


### Resursinformation {#configure-asset-details-content-hub}

Du kan också konfigurera resursegenskaperna som visas för varje resurs, till exempel filnamn, titel, format, storlek och så vidare. Gör så här:

1. Klicka på **[!UICONTROL Asset details]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).

1. Klicka på **[!UICONTROL Add metadata]**.

1. Ange en etikett för egenskapen, mappa den till en egenskap med hjälp av fältet **[!UICONTROL Metadata]** och välj indatatypen för de nya metadata för resursen.
1. Klicka på **[!UICONTROL Confirm]**. De nya metadata visas i listan över befintliga resursegenskaper.

1. Klicka på **[!UICONTROL Save]** för att tillämpa ändringarna så att den nya egenskapen visas på sidan med resursinformation.

På samma sätt kan du klicka på ikonen ![Redigera](assets/do-not-localize/edit_icon.svg), som finns bredvid varje tillgänglig egenskap, för att redigera etiketterna eller klicka på ikonen Ta bort för att ta bort alla befintliga resursdetaljer. Klicka på **[!UICONTROL Save]** när du har gjort alla ändringar för att tillämpa ändringarna.

![Information om användargränssnittsresurser för konfiguration på Content Hub](assets/configuration-ui-asset-details.png)

De egenskaper som är aktiverade i konfigurationsanvändargränssnittet visas på sidan Resursinformation:

![Resursegenskaper i Content Hub](assets/config-ui-asset-properties.png)

### Tillgångskort {#asset-card}

Du kan också konfigurera de viktiga metadatafält som du behöver visa på **resurskortet** upp till högst 6 fält. Gör så här:

![nyckelmetadata på resurskortet](/help/assets/assets/asset-card-key-metadata.png)

1. Klicka på **Resurskort** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).
2. Klicka på **Lägg till metadata**. Dialogrutan **Lägg till metadata för resurskort** visas.
3. Ange metadatanamnet i fältet **Etikett** och välj en metadataegenskap i fältet **Metadata**.
4. Klicka på **Bekräfta** och sedan på **Spara** för att tillämpa ändringarna så att den nya egenskapen visas på sidan med resursinformation.
   ![resurskort](/help/assets/assets/asset-card.png)

Klicka på ![redigera](/help/assets/assets/edit-content-hub.svg) som är tillgänglig bredvid varje tillgänglig egenskap om du vill göra nödvändiga ändringar eller klicka på ![ta bort](/help/assets/assets/delete-content-hub.svg) om du vill ta bort en befintlig metadataegenskap. Klicka på **Spara** när du har gjort alla ändringar för att tillämpa ändringarna.

### Sök {#configure-metadata-search-content-hub}

Administratörer kan definiera metadatafält som söks igenom när en användare anger ett sökvillkor i Content Hub. Utför följande steg:

1. Klicka på **[!UICONTROL Add metadata]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).

1. Ange metadatafältet och klicka på **[!UICONTROL Confirm]**.

1. Klicka på **[!UICONTROL Save]** för att tillämpa ändringarna så att den nya metadataegenskapen visas i listan med metadatafält.

På samma sätt kan du klicka på ikonen ![Redigera](assets/do-not-localize/edit_icon.svg), som finns bredvid varje tillgänglig metadataegenskap, om du vill redigera egenskapen eller klicka på ikonen Ta bort om du vill ta bort en befintlig egenskap. Klicka på **[!UICONTROL Save]** när du har gjort alla ändringar för att tillämpa ändringarna.

![Sökning i konfigurationsgränssnittet på Content Hub](assets/configuration-ui-metadata-search.png)


### Varumärke {#configure-branding-content-hub}

Administratörer kan också anpassa rubrik och brödtext på banderollen på Content Hub-portalen efter varumärkeskraven. Gör så här:

1. Klicka på **[!UICONTROL Branding]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).

1. Ange text i fälten **[!UICONTROL Title text on banner]** och **[!UICONTROL Body text on banner]**.

1. Klicka på **[!UICONTROL Save]** för att tillämpa ändringarna.

![Gränssnittsmärkning för konfiguration på Content Hub](assets/configuration-ui-branding.png)

De varumärkningsuppdateringar som är aktiverade på skärmen för användargränssnittet för konfiguration på bannern för Content Hub-portalen:

![Gränssnittsmärkning för konfiguration på Content Hub](assets/configuration-ui-branding-updates.png)

### Utgångna resurser{#expired-assets-content-hub}

Administratörer kan kontrollera om utgångna resurser behöver vara synliga på Content Hub. Om de utgångna resurserna blir synliga kan de även definiera om användare kan hämta dem.

Utgångna mediefiler visas inte i Content Hub som standard.

Gör så här:

1. Klicka på **[!UICONTROL Expired Assets]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).

1. Aktivera alternativet **[!UICONTROL Allow users to view expired assets]** i avsnittet **[!UICONTROL Visible]** för att göra alla förfallna resurser synliga på Content Hub.

1. När du har aktiverat synlighet för resurser kan du aktivera eller inaktivera möjligheten att hämta utgångna resurser med hjälp av växlingsknappen **[!UICONTROL Allow users to download expired assets]**.

1. Klicka på **[!UICONTROL Save]** för att tillämpa ändringarna.

   ![Utgångna resurser på Content Hub](assets/expired-assets-content-hub.png)

När du har aktiverat synlighet för resurser kan du visa de förfallna resurserna på Content Hub, enligt bilden nedan:

![Utgångna resurser på Content Hub](assets/view-download-expired-assets.png)

Om administratören har aktiverat nedladdning kan Content Hub-användarna även hämta dem, vilket är markerat i bilden.

Om synligheten för utgångna resurser är aktiverad markeras även resurser som förfaller inom 15 dagar med meddelandet `Expiring in n days` på tillgångskortet.

### Återgivningar {#renditions-content-hub}

Återgivningar är anpassade versioner av digitala resurser, som bilder, dokument och så vidare, som utformats för olika enheter och plattformar för att ge optimala prestanda. Se mer om [återgivningar i Adobe Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/renditions).

Content Hub tillåter hämtning av statiska återgivningar. Statiska återgivningar är olika representationer av en resurs ursprungliga fil som genereras internt. Exempel är miniatyrbilder eller mobiloptimerade renderingar. Administratörer kan hantera och kontrollera tillgängligheten för resursrenderingar och hantera om du kan hämta originalresurser eller inte.

Gör så här:

Klicka på **[!UICONTROL Renditions]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub). Följande alternativ är tillgängliga:

* Aktivera växlingsknappen [!UICONTROL Enable availability of static renditions] för att göra alla statiska återgivningar synliga på Content Hub.

* Aktivera eller inaktivera **[!UICONTROL Allow users to download original assets]** för att kontrollera tillgängligheten för hämtning av originalresurser.

  ![Konfigurera renderingar på Content Hub](assets/config-renditions.png)

Mer information om hur du visar och hämtar statiska återgivningar i Content Hub finns i [Hämta resurser i Content Hub](/help/assets/download-assets-content-hub.md).

### Anpassade länkar {#configure-custom-links-content-hub}

Du kan även lägga till anpassade flikar utöver standardflikarna **[!UICONTROL All Assets]**, **[!UICONTROL Collections]** och **[!UICONTROL Insights]** på Content Hub-portalen precis nedanför banderollen. Gör så här:

1. Klicka på **[!UICONTROL Custom Links]** i användargränssnittet för [konfigurationer](#access-configuration-options-content-hub).

1. Klicka på **[!UICONTROL Add link]**.

1. Ange text i fälten **[!UICONTROL Label]** och **[!UICONTROL URL]**. Etiketten som du definierar visas som en flik och när du klickar på etiketten navigerar du till den URL som definierats i fältet **[!UICONTROL URL]**.

1. Klicka på **[!UICONTROL Confirm]**.

1. Klicka på **[!UICONTROL Save]** för att tillämpa ändringarna.

På samma sätt kan du klicka på ikonen ![Redigera](assets/do-not-localize/edit_icon.svg), som finns bredvid varje URL, om du vill redigera länkarna eller klicka på ikonen Ta bort om du vill ta bort en befintlig URL. Klicka på **[!UICONTROL Save]** när du har gjort alla ändringar för att tillämpa ändringarna.

![Anpassade länkar i konfigurationsgränssnittet på Content Hub](assets/configuration-ui-custom-links.png)

Den anpassade länken visas som en ny flik bredvid fliken Insikter på Content Hub hemsida.

![Anpassade länkar i konfigurationsgränssnittet på Content Hub](assets/configuration-ui-custom-link-tab.png)
