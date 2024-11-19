---
title: Hämta resurser från Content Hub
description: Lär dig hur du hämtar resurser från Content Hub-portalen
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Hämta resurser från Content Hub {#download-assets}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![Hämta resurser](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Med Content Hub kan du hämta och dela dina resurser. Dessa resurser kan vara bilder, videor eller annat digitalt innehåll. Content Hub förbättrar tillgängligheten och anpassbarheten för effektiv materialdistribution.

Du kan hämta en eller flera resurser med Content Hub. De ursprungliga versionerna av resursen hämtas.

## Ladda ned en licensierad resurs {#single-download-asset}

Välj en resurs och klicka på ![hämta](/help/assets/assets/download-icon.svg) i den övre listen. I dialogrutan Hämta resurs visas resursens licens. Godkänn licensvillkoren och klicka på **Hämta**.
Du kan också klicka på ![hämta](/help/assets/assets/download-icon.svg) på resurskortet om du vill hämta resursen.

### Hämta en licensierad resurs från dialogrutan Resurs {#single-download-from-asset-dialog-box}

1. Klicka på miniatyrbilden för resursen. Dialogrutan Resurser visas.
1. Klicka på ![hämta](/help/assets/assets/download-icon.svg) i verktygsfältet längst till höger. I hämtningsfönstret visas kryssrutan för resursåtergivningar och godkännande av licensvillkor.
   ![single-download-dialog-box](/help/assets/assets/asset-dialog-box-for-single-download.png)
   * Klicka på länken Villkor för att se licensvillkoren i den vänstra rutan.

     >[!NOTE]
     >
     Kryssrutan Villkor visas endast för licensierade mediefiler. Dessutom visas i dialogrutan för mediefiler en förhandsgranskning av licensvillkoren endast för mediefiler med godkända licenser. [Godkänn resursens licens](/help/assets/approve-assets-content-hub.md) innan du hämtar den för att aktivera förhandsgranskningen av licensieringsvillkor i dialogrutan för mediefiler.

   * Klicka på den **ursprungliga återgivningsrutan** för att återgå till den ursprungliga återgivningen i den vänstra rutan.
1. Acceptera licensvillkoren (för licensierad mediefil) och klicka på **Hämta** för att hämta mediefilen.

## Ladda ned flera licensierade Assets{#multi-download}

1. Markera resurserna och klicka på ![hämta](/help/assets/assets/download-icon.svg) i den övre listen. Vilken dialogruta som visas beror på om hämtningslistan innehåller resurser som har gått ut eller bara resurser som inte har gått ut. <br/>
   **Dialogrutan Hämta utgångna resurser:** Den här dialogrutan visar förhandsvisningen av de utgångna resurserna tillsammans med deras förfallodatum i den vänstra rutan. Antalet utgångna resurser som är av det totala antalet markerade visas i den högra rutan. Klicka på **Fortsätt med alla resurser** om du vill hämta utgångna resurser med andra resurser (om sådana finns). Dialogrutan Hämta resurser visas. Gå till dialogrutan [Hämta resurser](#Download-asset-dialog-box) om du vill fortsätta.

   >[!NOTE]
   >
   [Aktivera nedladdningsalternativet för utgångna resurser](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) om du vill hämta dem. Endast material som har upphört att gälla och som har aktiverat hämtning är tillgängliga för hämtning.

   <a id="Download-asset-dialog-box"></a> **Dialogrutan Hämta resurser:** Den här dialogrutan visar en lista över licenser som är associerade med de valda resurserna i den vänstra rutan. Välj en licens om du vill förhandsgranska villkoren (i pdf-format) i den mittersta rutan och förhandsvisningen av de associerade resursernas antal i den högra rutan. Granskade licenser markeras med ljusblått.

   >[!NOTE]
   >
   I dialogrutan **Hämta mediefil** förhandsvisas licensvillkoren endast för godkända licenser. [Godkänn resurslicenserna](/help/assets/approve-assets-content-hub.md) innan du hämtar dem för att förhandsvisa deras licensvillkor i dialogrutan **Hämta mediefiler**.

1. Klicka på ![remove-icon](/help/assets/assets/remove-icon.svg) om du vill ta bort en licens från hämtningsdialogrutan.

1. Acceptera villkoren och klicka sedan på **Hämta** för att hämta resurser som är associerade med tillgängliga licenser i den vänstra rutan.
   ![download-multiple-license](/help/assets/assets/download-multiple-license.png)

### Ladda ned Assets utan licens {#download-non-licensed-assets}

Om du vill hämta icke-licensierade resurser markerar du resurserna och klickar på ![Hämta](/help/assets/assets/download-icon.svg) i den övre listen.







