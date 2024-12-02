---
title: Snabb Publish till AEM och Dynamic Media
description: Med snabbvyn Publish i Assets kan du publicera material till AEM och Dynamic Media samtidigt eller separat. Du kan välja resurser och mappar och välja att publicera till Dynamic Media eller AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 8ab19fe82fc390d28d33b17222177fd8486c8fc7
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Publish Assets till AEM och Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Med Experience Manager Assets kan du snabbt publicera material till Experience Manager och Dynamic Media i Assets-vyn. Detta garanterar att du hanterar dina resurser och sedan publicerar dem i vyn [Assets utan att växla till administrationsvyn](/help/assets/overview.md##persona-based-experiences).

I Experience Manager Assets-vyn kan du publicera resurser till AEM eller Dynamic Media, eller till båda samtidigt. Du kan publicera resurser när du överför, bläddrar bland och söker efter resurser. Alla dessa alternativ för att publicera resurser beskrivs i den här artikeln i detalj.

## Innan du börjar {#before-you-begin}

Konfigurera de här inställningarna för att visa publiceringsalternativ för AEM och Dynamic Media:

* Om du vill visa publiceringsalternativ för Dynamic Media konfigurerar du följande inställningar i administrationsvyn:

   * [Skapa en Dynamic Media Cloud-konfiguration](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Ställ in Dynamic Media Publish-läget på mappnivå. Du kan konfigurera de här inställningarna när du skapar Dynamic Media Cloud-konfigurationen. Mer information om hur du skriver över de här inställningarna på mappnivå finns i [Konfigurera selektiv Publish på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Om du vill visa publiceringsalternativ för AEM måste du konfigurera AEM publiceringsslutpunkt för miljön.

## Publish Assets under överföring {#piblish-assets-during-upload}

Du kan publicera resurser till AEM och Dynamic Media medan du överför resurser till en mapp. Vilka publiceringsalternativ som visas beror på Dynamic Media publiceringsläge som anges i den mapp som resurserna överförs till. Dynamic Media publiceringsläge kan anges till:

* **Vid aktivering:** När resurser överförs till den här mappen måste du publicera resursen explicit innan en URL/Embed-länk anges.

* **Omedelbar:** När resurser överförs till den här mappen, importeras resurserna till Experience Manager och URL:en/inbäddningen anges omedelbart.
* **Selektiv Publish:** Assets publiceras antingen på Experience Manager eller till Dynamic Media för att distribueras offentligt.

### Dynamic Media Publish Mode inställt på Vid aktivering {#dynamic-media-publish-mode-set-to-upon-activation}

Så här publicerar du resurser under överföring till en mapp med Dynamic Media Publish Mode inställt på **Vid aktivering**:

1. Klicka på **Lägg till Assets** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. I avsnittet **Publish-alternativ** visas **DM Publish Mode** som **Vid aktivering**.
   ![Överför bild vid aktivering](/help/assets/assets/upload-uactivation.svg)
2. Välj **Publish att AEM och Dynamic Media** och klicka på **Överför**. Materialet publiceras samtidigt till AEM och Dynamic Media. Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera Publish-status](#check-publish-status).

### Dynamic Media Publish Mode inställt på Omedelbar {#dynamic-media-publish-mode-set-to-immediate}

Så här publicerar du resurser under överföring till en mapp med Dynamic Media Publish Mode inställt på **Omedelbart**:

1. Klicka på **Lägg till Assets** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. Under Publish-alternativ visas **DM Publish Mode** som **Omedelbart**.
   ![bild för filöverföring - omedelbart läge](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Eftersom Dynamic Media Publish Mode är **Omedelbart** publiceras de överförda resurserna automatiskt till Dynamic Media när du klickar på **Överför**.

2. Välj Publish för att **AEM publicera** de överförda resurserna som ska AEM och klicka på Överför.

   Om du väljer **Publish för att AEM** publiceras resurserna till AEM och Dynamic Media, annars publiceras resurserna till Dynamic Media.

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera Publish-status](#check-publish-status).

### Dynamic Media Publish Mode inställt på Selective Publish {#dynamic-media-publish-mode-set-to-selective-publish}

Så här publicerar du resurser under överföring till en mapp med Dynamic Media Publish Mode inställt på **Selektiv Publish**:

1. Klicka på **Lägg till Assets** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. Under Publish-alternativ visas **DM Publish Mode** som **Selektiv Publish**.
   ![överför bildselektivt publiceringsläge](/help/assets/assets/upload-selective.svg)

2. Välj **Publish om du vill AEM**, **Publish till Dynamic Media** eller båda, beroende på dina behov, och klicka sedan på **Överför**.

   Resurserna publiceras till AEM och Dynamic Media baserat på ditt val.

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera Publish-status](#check-publish-status).

## Publish-resurser med resursbläddringssida {#publish-assets-using-asset-browse-page}

Så här publicerar du resurser via resursbläddringssidan:

1. Klicka på **Assets** i avsnittet **Assets Management** som finns i den vänstra rutan.
2. Markera en eller flera resurser eller mappar som du vill publicera och klicka på **Publish**.
3. Välj **AEM** och klicka på **Publish** för att publicera resurser till AEM och Dynamic Media.
   Bläddra bland ![resurser](/help/assets/assets/browse-uactivation-immediate.svg)
Du kan inte publicera en mapp som har Dynamic Media Publish Mode inställt på **Selektiv publicering.** Alla andra markerade mappar eller resurser publiceras till AEM och Dynamic Media när du har valt AEM.
   Bläddra bland ![resurser](/help/assets/assets/browse-selective123.svg)

## Publish-resurser med sökresultatsida {#publish-assets-using-search-results-page}

Så här publicerar du resurser med resurssökningens resultatsida:

1. Ange villkoren i sökfältet och klicka på sökikonen för att visa resultatet.
2. Markera de resurser som du vill publicera och klicka på **Publish.**
3. Välj AEM, Dynamic Media eller båda beroende på dina behov och klicka sedan på **Publish.**
   ![sökbild](/help/assets/assets/search-mode.svg)
Alternativet att publicera till Dynamic Media på sökresultatsidan beror på vilken mapp som är tillgänglig i databasen i Dynamic Media Publish-läget.

   >[!NOTE]
   >
   >Om du markerar en mapp och klickar på **Publish** på sökresultatsidan visas ett alternativ i Experience Manager Assets för att publicera resurser till AEM och inte till Dynamic Media, oavsett vilken Dynamic Media Publish-lägesinställning mappen har.

## Kontrollera Publish-status {#check-publish-status}

Så här kontrollerar du publiceringsstatus för en resurs eller mapp:

1. Klicka på **[!UICONTROL Assets]** i avsnittet **[!UICONTROL Assets Management]** i den vänstra rutan.
2. Växla till listvyn med vyväljaren. Du kan visa resursegenskaper som AEM, Dynamic Media Publish, titel, storlek, dimensioner och så vidare.\
   Om en resurs eller mapp inte publiceras visas statusen för kolumnerna **AEM Publish** och **Dynamic Media Publish** som **Ej tillämpbart.**
   ![kontrollera publiceringsstatus1](/help/assets/assets/check-publish-status1.png)
Om du inte kan visa kolumnerna AEM Publish och Dynamic Media Publish i listvyn:
   1. Klicka på ![inställningar](/help/assets/assets/settings-icon.svg) och välj **AEM kolumnerna Publish** och **Dynamic Media Publish** i dialogrutan **Konfigurerbara kolumner** .
   2. Klicka på **Bekräfta.** Experience Manager Assets lägger till de markerade kolumnerna i listvyn.

      ![kontrollera publiceringsstatus2](/help/assets/assets/check-publish-status2.png)

Du kan också kontrollera en resurspubliceringsstatus genom att markera en resurs och klicka på **Information.** Informationen finns i avsnittet **Publish** i den högra rutan. I avsnittet **Publish** visas datumet när resurserna publiceras till Dynamic Media och AEM. Om du behöver visa tidpunkten när resurserna publiceras kan du navigera till listvyn och visa dessa detaljer.

![kontrollera publiceringsstatus 3](/help/assets/assets/check-publish-status3.png)

## Begränsningar {#limitations}

Följande funktioner är inte tillgängliga för tillfället när du publicerar resurser till AEM och Dynamic Media:

* Publish Assets to AEM and Dynamic Media from the Asset details page.
* Visualisera slutpunkterna där resurserna publiceras med hjälp av guiden Snabba Publish.
* Lägg till eller ta bort fler resurser i guiden för Quick Publish.
* En sida som visar publicerade resurser.
* Möjlighet att kopiera eller klistra in Dynamic Media URL på resursnivå (om resurserna publiceras till Dynamic Media).
* Möjlighet att publicera referenser (resurser, taggar och så vidare) när du publicerar till AEM.
* Möjlighet att skriva över Dynamic Media synkroniseringsstatus på mappnivå.
* Möjlighet att skriva över Dynamic Media Publish-läget på mappnivå
* Hantera publikation stöds inte ännu.
