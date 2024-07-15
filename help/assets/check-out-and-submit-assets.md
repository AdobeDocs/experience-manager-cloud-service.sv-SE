---
title: Checka in och checka ut filer i  [!DNL Assets]
description: Lär dig hur du checkar ut resurser för redigering och checkar in dem igen när ändringarna är klara.
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Checka in och checka ut filer i [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/check-out-and-submit-assets.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Med [!DNL Adobe Experience Manager Assets] kan du checka ut resurser för redigering och checka in dem igen när du har gjort ändringarna. När du har checkat ut en resurs kan bara du redigera, kommentera, publicera, flytta eller ta bort resursen. När du checkar ut en resurs låses den. Andra användare kan inte utföra någon av dessa åtgärder på resursen förrän du checkar in resursen igen på [!DNL Assets]. De kan dock fortfarande ändra metadata för den låsta resursen.

Om du vill kunna checka ut/in resurser måste du ha skrivbehörighet för dem.

Den här funktionen förhindrar att andra användare åsidosätter ändringar som gjorts av en författare där flera användare samarbetar i redigeringsarbetsflöden mellan team.

## Checka ut resurser {#checking-out-assets}

1. I användargränssnittet [!DNL Assets] väljer du den resurs du vill checka ut. Du kan också välja flera resurser att checka ut.

1. Klicka på **[!UICONTROL Checkout]** i verktygsfältet. Alternativet **[!UICONTROL Checkout]** växlar till **[!UICONTROL Checkin]**.
Logga in som en annan användare om du vill kontrollera om andra användare kan redigera den utcheckade resursen. Ikonen ![ikon för utcheckningslås](assets/do-not-localize/checkout_lock.png) visas på miniatyrbilden för den resurs som du har checkat ut.

   ![ikonen för utcheckning i kortvyn](assets/checkout-icon-card-view.png)

   Markera resursen. Observera att verktygsfältet inte visar några alternativ som gör att du kan redigera, kommentera, publicera eller ta bort resursen.

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   Om du vill redigera metadata för den låsta resursen klickar du på **[!UICONTROL View Properties]**.

1. Klicka på **[!UICONTROL Edit]** för att öppna resursen i redigeringsläge.

1. Redigera resursen och spara ändringarna. Beskär till exempel bilden och spara. Du kan också välja att anteckna eller publicera resursen.

1. Välj den redigerade resursen i [!DNL Assets]-gränssnittet och klicka på **[!UICONTROL Checkin]** i verktygsfältet. Den ändrade resursen checkas in på [!DNL Assets] och är tillgänglig för andra användare för redigering.

## Tvingad incheckning {#forced-check-in}

Administratörer kan checka in resurser som är utcheckade av andra användare.

1. Logga in på [!DNL Assets] som administratör.
1. I användargränssnittet [!DNL Assets] väljer du en eller flera resurser som har checkats ut av andra användare.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Klicka på **[!UICONTROL Release Lock]** i verktygsfältet. Resursen checkas in igen och är tillgänglig för redigering för andra användare.

## Bästa praxis och begränsningar {#tips-limitations}

* Det går att ta bort en *mapp* som innehåller utcheckade resursfiler. Innan du tar bort en mapp kontrollerar du att inga digitala resurser är utcheckade av användarna.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Förstå incheckning och utcheckning i [!DNL Experience Manager] datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Videosjälvstudiekurs för att förstå incheckning och utcheckning i [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)
