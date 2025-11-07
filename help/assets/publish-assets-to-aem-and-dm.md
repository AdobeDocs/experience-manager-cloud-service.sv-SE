---
title: Snabbpublicera till  [!DNL AEM and Dynamic Media]
description: Med Snabbpublicering i [!DNL Assets view] kan du publicera resurser till  [!DNL AEM and Dynamic Media] samtidigt eller separat. Du kan välja resurser och mappar och välja att publicera till  [!DNL Dynamic Media] eller [!DNL AEM].
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing
role: User
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# Publicera Assets till [!DNL AEM and Dynamic Media]{#Publish-Assets-to-AEM-and-Dynamic-Media}

Med [!DNL Experience Manager Assets] kan du snabbt publicera resurser till [!DNL Experience Manager] och [!DNL Dynamic Media] med [!DNL Assets view]. Detta garanterar att du hanterar dina resurser och sedan publicerar dem med [[!DNL Assets view] utan att behöva växla till  [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences).

[!DNL Experience Manager Assets view] ger flexibilitet att publicera resurser till [!DNL AEM] eller [!DNL Dynamic Media], eller båda samtidigt. Du kan publicera resurser när du överför, bläddrar bland och söker efter resurser. Alla dessa alternativ för att publicera resurser beskrivs i den här artikeln i detalj.

## Innan du börjar {#before-you-begin}

Konfigurera de här inställningarna för att visa publiceringsalternativen för [!DNL AEM and Dynamic Media]:

* Om du vill visa publiceringsalternativen för [!DNL Dynamic Media] konfigurerar du följande inställningar i administratörsvyn:

   * [Skapa en [!DNL Dynamic Media] molnkonfiguration](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Ange publiceringsläget [!DNL Dynamic Media] på mappnivå. Du kan konfigurera de här inställningarna när du skapar [!DNL Dynamic Media]-molnkonfigurationen. Mer information om hur du skriver över de inställningarna på mappnivå finns i [Konfigurera selektiv publicering på mappnivå i [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md).

* Om du vill visa publiceringsalternativen för [!DNL AEM] måste du konfigurera publiceringsslutpunkten [!DNL AEM] för din miljö.

## Publicera Assets under överföring {#piblish-assets-during-upload}

Du kan publicera resurser på [!DNL AEM and Dynamic Media] när du överför resurser till en mapp. Vilka publiceringsalternativ som visas beror på publiceringslägesinställningarna för [!DNL Dynamic Media] i den mapp där resurserna överförs. Publiceringsläget [!DNL Dynamic Media] kan anges till:

* **[!UICONTROL Upon activaton]:** När resurser överförs till den här mappen måste du uttryckligen publicera resursen först innan en URL/inbäddningslänk anges.

* **[!UICONTROL Immediate]:** När resurser överförs till den här mappen, importeras resurserna till Experience Manager och URL/Embed anges omedelbart.
* **[!UICONTROL Selective Publish]:** Assets publiceras antingen till [!DNL Experience Manager] eller till [!DNL Dynamic Media] för leverans i den offentliga domänen.

### [!UICONTROL Dynamic Media Publish Mode] inställd på [!UICONTROL Upon Activation] {#dynamic-media-publish-mode-set-to-upon-activation}

Så här publicerar du resurser när du överför dem till en mapp vars [!DNL Dynamic Media Publish Mode] är inställd på **[!UICONTROL Upon Activation]**:

1. Klicka på **[!UICONTROL Add Assets]** > **[!UICONTROL Browse]** > **[!UICONTROL Browse Files]** för att navigera till rätt mapp för att överföra resurser. Avsnittet **[!UICONTROL Publish Options]** visar **[!UICONTROL DM Publish Mode]** som **[!UICONTROL Upon Activation]**.

   ![Överför bild vid aktivering](/help/assets/assets/upload-uactivation.svg)

1. Markera **[!UICONTROL Publish to AEM and Dynamic Media]** och klicka på **[!UICONTROL Upload]**. Resurserna publiceras till [!DNL AEM and Dynamic Media] samtidigt. Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

### [!UICONTROL Dynamic Media Publish Mode] inställd på [!UICONTROL Immediate] {#dynamic-media-publish-mode-set-to-immediate}

Så här publicerar du resurser när du överför dem till en mapp vars [!UICONTROL Dynamic Media Publish Mode] är inställd på **[!UICONTROL Immediate]**:

1. Klicka på **[!UICONTROL Add Assets]** > **[!UICONTROL Browse]** > **[!UICONTROL Browse Files]** för att navigera till rätt mapp för att överföra resurser. Avsnittet **[!UICONTROL Publish Options]** visar **[!UICONTROL DM Publish Mode]** som **[!UICONTROL Immediate]**.

   ![bild för filöverföring - omedelbart läge](/help/assets/assets/resized-image-pdf-svg-new.svg)

   Eftersom [!UICONTROL Dynamic Media Publish Mode] är **[!UICONTROL Immediate]** publiceras de överförda resurserna automatiskt till [!DNL Dynamic Media] när du klickar på **[!UICONTROL Upload]**.

1. Välj **Publicera på AEM** om du vill publicera de överförda resurserna på [!DNL AEM] och klicka på **[!UICONTROL Upload]**.

   Om du väljer **Publicera på AEM** publiceras resurserna på [!DNL AEM and Dynamic Media], annars publiceras resurserna på [!DNL Dynamic Media].

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

### [!UICONTROL Dynamic Media Publish Mode] inställd på [!UICONTROL Selective Publish] {#dynamic-media-publish-mode-set-to-selective-publish}

Så här publicerar du resurser under överföring till en mapp med [!UICONTROL Dynamic Media Publish Mode] inställd på **[!UICONTROL Selective Publish]**:

1. Klicka på **[!UICONTROL Add Assets]** > **[!UICONTROL Browse]** > **[!UICONTROL Browse Files]** för att navigera till rätt mapp för att överföra resurser. Avsnittet **[!UICONTROL Publish Options]** visar **[!UICONTROL DM Publish Mode]** som **[!UICONTROL Selective Publish]**.

![överför bildselektivt publiceringsläge](/help/assets/assets/upload-selective.svg)

1. Välj **[!UICONTROL Publish to AEM]**, **[!UICONTROL Publish to Dynamic Media]** eller båda beroende på dina behov och klicka på **Överför**.

   Resurserna publiceras till [!DNL AEM and Dynamic Media] baserat på ditt val.

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

## Publicera resurser med resursbläddringssidan {#publish-assets-using-asset-browse-page}

Så här publicerar du resurser via resursbläddringssidan:

1. Klicka på **[!UICONTROL Assets]** i avsnittet **[!UICONTROL Assets Management]** i den vänstra rutan.
1. Markera en eller flera resurser eller mappar som du vill publicera och klicka på **[!UICONTROL Publish]**.
1. Välj **[!UICONTROL AEM]** och klicka på **[!UICONTROL Publish]** för att publicera resurser på [!DNL AEM and Dynamic Media].

   Bläddra bland ![resurser](/help/assets/assets/browse-uactivation-immediate.svg)

   Du kan inte publicera en mapp som har publiceringsläget [!DNL Dynamic Media] inställt på **[!UICONTROL Selective Publishing]**. Alla andra markerade mappar eller resurser publiceras till [!DNL AEM and Dynamic Media] efter att du har valt [!DNL AEM].

   Bläddra bland ![resurser](/help/assets/assets/browse-selective123.svg)

## Publicera resurser med sökresultatsidan {#publish-assets-using-search-results-page}

Så här publicerar du resurser med resurssökningens resultatsida:

1. Ange villkoren i sökfältet och klicka på sökikonen för att visa resultatet.
1. Välj de resurser som du behöver publicera och klicka på **[!UICONTROL Publish].**
1. Välj [!DNL AEM, Dynamic Media] eller båda enligt dina krav och klicka på **[!UICONTROL Publish]**.

   ![sökbild](/help/assets/assets/search-mode.svg)

   Alternativet att publicera till [!DNL Dynamic Media] på sökresultatsidan beror på publiceringsläget för [!DNL Dynamic Media] som är inställt på den mapp där resursen är tillgänglig i databasen.

   >[!NOTE]
   >
   >Om du markerar en mapp och klickar på **[!UICONTROL Publish]** på sökresultatsidan visar [!DNL Experience Manager Assets] ett alternativ för att publicera resurser på [!DNL AEM] och inte på [!DNL Dynamic Media], oavsett mappens [!DNL Dynamic Media] publiceringslägesinställningar.

## Kontrollera publiceringsstatus {#check-publish-status}

Så här kontrollerar du publiceringsstatus för en resurs eller mapp:

1. Klicka på **[!UICONTROL Assets]** i avsnittet **[!UICONTROL Assets Management]** i den vänstra rutan.
1. Växla till listvyn med vyväljaren. Du kan visa resursegenskaper som [!UICONTROL AEM publish], [!UICONTROL Dynamic Media Publish], [!UICONTROL title], [!UICONTROL size], [!UICONTROL dimensions] och så vidare.

   Om en resurs eller mapp inte publiceras visas statusen för kolumnerna **[!UICONTROL AEM Publish]** och **[!UICONTROL Dynamic Media Publish]** som **[!UICONTROL N/A]**.

   ![kontrollera publiceringsstatus1](/help/assets/assets/check-publish-status1.png)

   Om du inte kan visa kolumnerna [!DNL AEM] Publicera och [!DNL Dynamic Media] Publicera i listvyn:

   1. Klicka på ![inställningar](/help/assets/assets/settings-icon.svg) och välj **[!UICONTROL AEM Publish]** och **[!UICONTROL Dynamic Media Publish]** kolumner i dialogrutan **[!UICONTROL Configurable Columns]**.
   1. Klicka på **[!UICONTROL Confirm]**. [!DNL Experience Manager Assets] lägger till de markerade kolumnerna i listvyn.

      ![kontrollera publiceringsstatus2](/help/assets/assets/check-publish-status2.png)

Du kan också kontrollera publiceringsstatus för en resurs genom att markera en resurs och klicka på **[!UICONTROL Details]**. Mer information finns i avsnittet **[!UICONTROL Publish]** i den högra rutan. I avsnittet **[!UICONTROL Publish]** visas datumet när resurserna publiceras till [!DNL Dynamic Media] och [!DNL AEM]. Om du behöver visa tidpunkten när resurserna publiceras kan du navigera till listvyn och visa dessa detaljer.

![kontrollera publiceringsstatus 3](/help/assets/assets/check-publish-status3.png)

## Begränsningar {#limitations}

Följande funktioner ligger utanför omfånget för tillfället när resurser publiceras till [!DNL AEM and Dynamic Media]:

* Publicera resurser till [!DNL AEM and Dynamic Media] från [!DNL Asset details page].
* Visualisera slutpunkterna där resurserna publiceras med Snabbpubliceringsguiden.
* Lägg till eller ta bort fler resurser i Snabbpubliceringsguiden.
* En sida som visar publicerade resurser.
* Det går att kopiera eller klistra in URL:en [!DNL Dynamic Media] på en resursnivå (om resurserna publiceras till [!DNL Dynamic Media]).
* Möjlighet att publicera referenser (resurser, taggar och så vidare) vid publicering till [!DNL AEM].
* Möjlighet att skriva över synkroniseringsstatusen [!DNL Dynamic Media] på mappnivå.
* Möjlighet att skriva över publiceringsläget [!DNL Dynamic Media] på mappnivå
* Hantera publikation stöds inte ännu.
