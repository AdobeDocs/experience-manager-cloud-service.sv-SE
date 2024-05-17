---
title: Snabbpublicering till AEM och Dynamic Media
description: Med snabbpublicering i resursvyn kan du publicera resurser till AEM och dynamiska medier samtidigt eller separat. Du kan välja resurser och mappar och välja att publicera till Dynamic Media eller AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
source-git-commit: 9ad74a9c7ecd193446506cb883fff723c806f0a7
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---

# Publicera resurser till AEM och Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

Med Experience Manager Assets kan du snabbt publicera resurser på Experience Manager och Dynamic Media med hjälp av resursvyn. Detta garanterar att du hanterar dina resurser och sedan publicerar dem med [Resursvyn utan att växla till administrationsvyn](/help/assets/overview.md##persona-based-experiences).

I Experience Manager Assets-vyn kan du publicera resurser till AEM eller Dynamic Media, eller till båda samtidigt. Du kan publicera resurser när du överför, bläddrar bland och söker efter resurser. Alla dessa alternativ för att publicera resurser förklaras i den här artikeln i detalj.

## Innan du börjar {#before-you-begin}

Konfigurera de här inställningarna för att visa publiceringsalternativen för AEM och Dynamic Media:

* Om du vill visa publiceringsalternativen för Dynamic Media konfigurerar du följande inställningar i administrationsvyn:

   * [Skapa en molnkonfiguration för Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Ange publiceringsläget för Dynamic Media på mappnivå. Du kan konfigurera de här inställningarna när du skapar Dynamic Media molnkonfiguration. Mer information om hur du skriver över inställningarna på mappnivå finns i [Konfigurera selektiv publicering på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Om du vill visa publiceringsalternativen för AEM måste du konfigurera AEM publiceringsslutpunkt för miljön.

## Publicera resurser under överföring {#piblish-assets-during-upload}

Du kan publicera resurser till AEM och Dynamic Media medan du överför resurser till en mapp. Vilka publiceringsalternativ som visas beror på publiceringsläget för Dynamic Media som är inställt på den mapp som resurserna överförs till. Dynamic Media publiceringsläge kan anges till:

* **Vid aktivering:** När resurser överförs till den här mappen måste du uttryckligen publicera resursen innan en URL/Embed-länk anges.

* **Omedelbar:** När resurser överförs till den här mappen, importeras resurserna till Experience Manager och URL:en/inbäddningen anges omedelbart.
* **Selektiv publicering:** Resurser publiceras till Experience Manager eller till Dynamic Media för att distribueras offentligt.

### Dynamic Media publiceringsläge inställt på Vid aktivering {#dynamic-media-publish-mode-set-to-upon-activation}

Så här publicerar du resurser under överföring till en mapp med publiceringsläget för Dynamic Media inställt på **Vid aktivering**:

1. Klicka **Lägg till resurser** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. The **Publiceringsalternativ** visas **DM-publiceringsläge** as **Vid aktivering**.
   ![Överför bild vid aktivering](/help/assets/assets/upload-uactivation.svg)
2. Välj **Publicera till AEM och Dynamic Media** och klicka **Överför**. Materialet publiceras samtidigt till AEM och Dynamic Media. Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

### Dynamic Media publiceringsläge inställt på Omedelbar {#dynamic-media-publish-mode-set-to-immediate}

Så här publicerar du resurser under överföring till en mapp med publiceringsläget för Dynamic Media inställt på **Omedelbar**:

1. Klicka **Lägg till resurser** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. I avsnittet Publiceringsalternativ visas **DM-publiceringsläge** as **Omedelbar**.
   ![filöverföringsbild - läget Direkt](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Som publiceringsläget i Dynamic Media är **Omedelbar** publiceras de överförda resurserna automatiskt till Dynamic Media när du klickar på **Överför**.

2. Välj Publicera till **AEM att publicera** de överförda resurserna som ska AEM och klicka på Överför.

   Om du väljer **Publicera till AEM**, publiceras resurserna till AEM och Dynamic Media, annars publiceras de till Dynamic Media.

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

### Dynamic Media publiceringsläge inställt på selektiv publicering {#dynamic-media-publish-mode-set-to-selective-publish}

Så här publicerar du resurser under överföring till en mapp med publiceringsläget för Dynamic Media inställt på **Selektiv publicering**:

1. Klicka **Lägg till resurser** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. I avsnittet Publiceringsalternativ visas **DM-publiceringsläge** as **Selektiv publicering**.
   ![överför bildselektivt blixtläge](/help/assets/assets/upload-selective.svg)

2. Välj **Publicera till AEM**, **Publicera till Dynamic Media** eller både och enligt dina önskemål och klicka **Överför**.

   Resurserna publiceras till AEM och Dynamic Media baserat på ditt val.

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

## Publicera resurser med resursbläddringssidan {#publish-assets-using-asset-browse-page}

Så här publicerar du resurser via resursbläddringssidan:

1. Klicka **Resurser** i **Resurshantering** som finns i den vänstra rutan.
2. Markera de resurser eller mappar som du vill publicera och klicka på **Publicera**.
3. Välj **AEM** och klicka **Publicera** för att publicera material till AEM och Dynamic Media.
   ![bläddra bland resurser](/help/assets/assets/browse-uactivation-immediate.svg)
Du kan inte publicera en mapp som har publiceringsläget Dynamic Media inställt på **Selektiv publicering.** Alla andra markerade mappar eller resurser publiceras till AEM och Dynamic Media när du har valt AEM.
   ![bläddra bland resurser](/help/assets/assets/browse-selective123.svg)

## Publicera resurser med sökresultatsidan {#publish-assets-using-search-results-page}

Så här publicerar du resurser med resurssökningens resultatsida:

1. Ange villkoren i sökfältet och klicka på sökikonen för att visa resultatet.
2. Välj de resurser du behöver publicera och klicka på **Publicera.**
3. Välj AEM, Dynamic Media eller båda beroende på dina behov och klicka på **Publicera.**
   ![sökbild](/help/assets/assets/search-mode.svg)
Alternativet att publicera till Dynamic Media på sökresultatsidan beror på vilken mapp som är tillgänglig i databasen i Dynamic Media publiceringsläge som är inställd på.

   >[!NOTE]
   >
   >Om du väljer en mapp och klickar på **Publicera** På sökresultatsidan visar Experience Manager Assets ett alternativ för att publicera resurser till AEM och inte till Dynamic Media, oavsett mappens inställningar för publiceringsläge för Dynamic Media.

## Kontrollera publiceringsstatus {#check-publish-status}

Så här kontrollerar du publiceringsstatusen för en resurs eller mapp:

1. Klicka **[!UICONTROL Assets]** i **[!UICONTROL Assets Management]** som finns i den vänstra rutan.
2. Växla till listvyn med Visa väljare. Du kan visa resursegenskaper som AEM, Dynamic Media Publish, titel, storlek, dimensioner och så vidare.\
   Om en resurs eller mapp inte har publicerats är statusen för **AEM Publish** och **Dynamic Media Publish** kolumner visas som **Ej tillämpligt.**
   ![kontrollera publiceringsstatus1](/help/assets/assets/check-publish-status1.png)
Om du inte kan visa kolumnerna AEM Publicera och Dynamic Media Publish i listvyn:
   1. Klicka ![inställningar](/help/assets/assets/settings-icon.svg) och markera **AEM Publish** och **Dynamic Media Publish** kolumner från **Konfigurerbara kolumner** -dialogrutan.
   2. Klicka **Bekräfta.** Experience Manager Assets lägger till de markerade kolumnerna i listvyn.

      ![kontrollera publiceringsstatus2](/help/assets/assets/check-publish-status2.png)

Du kan även kontrollera publiceringsstatus för en resurs genom att markera en resurs och klicka på **Information.** Mer information finns i **Publicera** som finns i den högra rutan. The **Publicera** anger det datum då resurserna publiceras till Dynamic Media och AEM. Om du behöver visa tidpunkten när resurserna publiceras kan du navigera till listvyn och visa dessa detaljer.

![kontrollera publiceringsstatus 3](/help/assets/assets/check-publish-status3.png)

## Begränsningar {#limitations}

Följande funktioner är inte tillgängliga för tillfället när du publicerar resurser till AEM och Dynamic Media:

* Publicera resurser till AEM och Dynamic Media från sidan Resursinformation.
* Visualisera slutpunkterna där resurserna publiceras med hjälp av snabbpubliceringsguiden.
* Lägg till eller ta bort fler resurser i Snabbpubliceringsguiden.
* En sida som visar publicerade resurser.
* Möjlighet att kopiera eller klistra in Dynamic Media URL på resursnivå (om resurserna publiceras till Dynamic Media).
* Möjlighet att publicera referenser (resurser, taggar och så vidare) när du publicerar till AEM.
* Möjlighet att skriva över Dynamic Media synkroniseringsstatus på mappnivå.
* Möjlighet att skriva över Dynamic Media Publish-läget på mappnivå
* Hantera publikation stöds inte ännu.
