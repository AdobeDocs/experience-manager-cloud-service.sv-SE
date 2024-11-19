---
title: Godkänn resurser för Content Hub
description: Lär dig hur du godkänner resurser i Assets as a Cloud Service och gör dem tillgängliga i Content Hub.
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Godkänn resurser för Content Hub {#approve-assets-content-hub}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Godkänn resurser för Content Hub](assets/content-hub-approve-assets.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Varumärkesansvariga och marknadsförare har strikt kontroll över varumärkestillgångarna. Det är bara en godkänd och den senaste versionen av mediefilen som kan användas i Content Hub, vilket ger ett enhetligt varumärke i alla kanaler och i alla tillämpningar.

Ni kan godkänna mediefiler med AEM Assets as a Cloud Service för att effektivisera resurshanteringen och säkerställa en kontrollerad och effektiv process för hantering av mediefiler.

## Innan du börjar {#pre-requisites}

Innan du börjar bör du ha:

* Tillgång till AEM Assets as a Cloud Service

* Skriv behörigheter för att redigera metadata för resurser så att du kan redigera fältet **[!UICONTROL Status]** som är tillgängligt i [resursegenskaperna](/help/assets/manage-organize-assets-view.md##manage-asset-status) för en resurs.

## Godkänn resurser för Content Hub{#approve-assets-for-content-hub}

Resurserna som markerats som `approved` i Assets as a Cloud Service är automatiskt tillgängliga i Content Hub.

>[!NOTE]
>
Assets as a Cloud Service och Content Hub måste använda samma organisation för de mediefiler som ska visas i Content Hub.

Så här anger du resursstatus som `approved` med hjälp av Assets-vyn i AEM as a Cloud Service:

1. Markera resursen och klicka på **[!UICONTROL Details]** i verktygsfältet.

1. På fliken **[!UICONTROL Basic]** väljer du resursstatus som `approved` i listrutan **[!UICONTROL Status]**.
1. Klicka på **[!UICONTROL Save]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3433172)

Om du behöver godkänna resurser i administratörsvyn läser du [Godkänn resurser i administratörsvyn](/help/assets/approve-assets.md#approve-assets).

## Godkänn resurser för Content Hub gruppvis i Assets-vyn {#bulk-approve-assets-content-hub}

Godkänn mediefiler gruppvis i Assets-vyn för AEM Assets as a Cloud Service. Alla mediefiler som godkänts i grupp blir sedan tillgängliga i Content Hub.

Så här godkänner du resurser i en mapp i Assets-vyn satsvis:

1. Markera resurserna och klicka på **[!UICONTROL Bulk Metadata Edit]**.

1. Välj **[!UICONTROL Approved]** i fältet **[!UICONTROL Status]** som är tillgängligt i avsnittet [!UICONTROL Properties] i den högra rutan.

1. Klicka på **[!UICONTROL Save]**.

## Automatisera godkännande av nya inkapslade resurser i administratörsvyn {#automate-approval-newly-ingested-assets}

När du har växlat från Assets-vyn till administratörsvyn kan du konfigurera mappinställningar så att alla nya resurser som läggs till i mappen godkänns automatiskt.

Du kan växla mellan vyerna Admin och Assets på följande sätt:
![Min Workspace-översikt](assets/assets-view.png)

Följ de här stegen för att automatisera godkännande av nyimporterade resurser i [!DNL Experience Manager Admin view]:

1. Skapa en mapp i författarmiljön (https://author-pXXX-eYYY.adobeaemcloud.com). Ersätt _XXX_ med ditt program-ID och _YY_ med miljö-ID från Experience Manager.
1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Klicka på **[!UICONTROL Create]** överst till höger på sidan.
1. Lägg till en profiltitel och klicka på **[!UICONTROL Create]**. Metadataprofilen har skapats.
1. Markera den nya metadataprofilen och klicka på **[!UICONTROL Edit _(e)_]**. <br>Formuläret **[!UICONTROL Edit Metadata Profile]** öppnas med fliken **[!UICONTROL Basic]** markerad.
1. Dra och släpp **[!UICONTROL Single Line Text Field]** från avsnittet **[!UICONTROL Build Form]** på höger sida till avsnittet Metadata i formuläret.
1. Klicka på det nya fältet och gör sedan följande uppdateringar på panelen **[!UICONTROL Settings]**:
   1. Ändra **[!UICONTROL Field Label]** till _Godkänd Assets_.
   1. Uppdatera **[!UICONTROL Map to property]** till _./jcr:content/metadata/dam:status_.
   1. Ändra standardvärdet till _godkänt_.

1. Klicka på **[!UICONTROL Save]**.
1. På sidan **[!UICONTROL Metadata Profiles]** väljer du den nya metadataprofilen.
1. Klicka på **[!UICONTROL Apply Metadata Profile to Folder(s)]** i det övre åtgärdsfältet.
1. Markera den eller de mappar som du vill godkänna och klicka på **[!UICONTROL Apply]**.
   <br> Behörigheten för hela mappen är inställd för godkännande och alla resurser som överförs till den här mappen godkänns automatiskt.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
Detta tillvägagångssätt godkänner de nya resurserna i mappen. För befintliga resurser i mappen måste du välja och godkänna dem manuellt.

## Hantera resurser som överförts med Content Hub {#manage-assets-uploaded-using-content-hub}

[Content Hub-användare med behörighet att lägga till resurser](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) kan [lägga till resurser i Content Hub](/help/assets/upload-brand-approved-assets.md) antingen från det lokala filsystemet eller importera resurser från datakällor i OneDrive eller Dropbox. Alla resurser visas på den översta nivån i Content Hub, oavsett vilken mappstruktur som finns i det lokala filsystemet eller datakällorna OneDrive och Dropbox för att förbättra sökfunktionerna.

Visningen av resurser som överförts med Content Hub beror på om du har [aktiverat alternativet för automatiskt godkännande](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Om växlingsknappen **[!UICONTROL Auto-approval]** är aktiverad blir de resurser som du överför med Content Hub automatiskt tillgängliga.

* Om **[!UICONTROL Auto-approval]**-växeln är inaktiverad visas inte de resurser som du överför med Content Hub automatiskt. Resurserna är tillgängliga i mappen `hydrated-assets` i din Assets as a Cloud Service-miljö. Navigera till mappen och [massredigera](#bulk-approve-assets-content-hub) statusen för dessa resurser till `Approved` för de resurser som ska visas i Content Hub.

![Content Hub godkännandeprocess](/help/assets/assets/content-hub-approval.png)
