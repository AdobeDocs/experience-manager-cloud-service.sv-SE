---
title: Snabbpublicering till AEM och Dynamic Media
description: Med Snabbpublicering i Assets-vyn kan du publicera material till AEM och Dynamic Media samtidigt eller separat. Du kan välja resurser och mappar och välja att publicera till Dynamic Media eller AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Publicera Assets till AEM och Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Med Experience Manager Assets kan du snabbt publicera material till Experience Manager och Dynamic Media i Assets-vyn. Detta garanterar att du hanterar dina resurser och sedan publicerar dem i vyn [Assets utan att växla till administrationsvyn](/help/assets/overview.md##persona-based-experiences).

I Experience Manager Assets-vyn kan du publicera material till AEM eller Dynamic Media, eller både och, samtidigt. Du kan publicera resurser när du överför, bläddrar bland och söker efter resurser. Alla dessa alternativ för att publicera resurser beskrivs i den här artikeln i detalj.

## Innan du börjar {#before-you-begin}

Konfigurera de här inställningarna för att visa publiceringsalternativen för AEM och Dynamic Media:

* Om du vill visa publiceringsalternativen för Dynamic Media konfigurerar du följande inställningar i administrationsvyn:

   * [Skapa en dynamisk konfiguration för Media Cloud](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Ange läget för dynamisk mediepublicering på mappnivå. Du kan konfigurera de här inställningarna när du skapar Dynamic Media Cloud-konfigurationen. Mer information om hur du skriver över de inställningarna på mappnivå finns i [Konfigurera selektiv publicering på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Om du vill visa publiceringsalternativen för AEM måste du konfigurera AEM publiceringsslutpunkt för din miljö.

## Publicera Assets under överföring {#piblish-assets-during-upload}

Du kan publicera resurser på AEM och Dynamic Media medan du överför resurser till en mapp. Vilka publiceringsalternativ som visas beror på inställningarna för publiceringsläget för dynamiska media i den mapp där resurserna överförs. Publiceringsläget för dynamiska media kan anges till:

* **Vid aktivering:** När resurser överförs till den här mappen måste du publicera resursen explicit innan en URL/Embed-länk anges.

* **Omedelbar:** När resurser överförs till den här mappen, importeras resurserna till Experience Manager och URL:en/inbäddningen anges omedelbart.
* **Selektiv publicering:** Assets publiceras antingen i Experience Manager eller i Dynamic Media för distribution i den offentliga domänen.

### Publiceringsläget för dynamiska media är inställt på Vid aktivering {#dynamic-media-publish-mode-set-to-upon-activation}

Så här publicerar du resurser när du överför dem till en mapp vars publiceringsläge för dynamiska media är inställt på **Vid aktivering**:

1. Klicka på **Lägg till Assets** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. I avsnittet **Publiceringsalternativ** visas **DM-publiceringsläget** som **Vid aktivering**.
   ![Överför bild vid aktivering](/help/assets/assets/upload-uactivation.svg)
2. Välj **Publicera till AEM och Dynamic Media** och klicka på **Överför**. Materialet publiceras samtidigt till AEM och Dynamic Media. Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

### Dynamiskt publiceringsläge för media är inställt på Omedelbart {#dynamic-media-publish-mode-set-to-immediate}

Så här publicerar du resurser när du överför dem till en mapp där läget för dynamisk mediepublicering är inställt på **Omedelbar**:

1. Klicka på **Lägg till Assets** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. I avsnittet **Publiceringsalternativ** visas **DM-publiceringsläget** som **Omedelbart**.
   ![bild för filöverföring - omedelbart läge](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Eftersom läget för publicering av dynamiska media är **Omedelbar** publiceras de överförda resurserna automatiskt till dynamiska media när du klickar på **Överför**.

2. Välj **Publicera på AEM** om du vill publicera de överförda resurserna på AEM och klicka på Överför.

   Om du väljer **Publicera till AEM** publiceras resurserna till AEM och Dynamic Media, annars publiceras resurserna till Dynamic Media.

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

### Publiceringsläget för dynamiska media är inställt på selektiv publicering {#dynamic-media-publish-mode-set-to-selective-publish}

Så här publicerar du resurser under överföring till en mapp med publiceringsläget för dynamiska media inställt på **Selektiv publicering**:

1. Klicka på **Lägg till Assets** > **Bläddra** > **Bläddra bland filer** för att navigera till rätt mapp för att överföra resurser. I avsnittet **Publiceringsalternativ** visas **DM-publiceringsläget** som **selektiv publicering**.
   ![överför bildselektivt publiceringsläge](/help/assets/assets/upload-selective.svg)

2. Välj **Publicera på AEM**, **Publicera på dynamiska media** eller båda, enligt dina önskemål, och klicka sedan på **Överför**.

   Resurserna publiceras till AEM och Dynamic Media utifrån ditt val.

   Information om den uppdaterade publiceringsstatusen för dessa resurser finns i [Kontrollera publiceringsstatus](#check-publish-status).

## Publicera resurser med resursbläddringssidan {#publish-assets-using-asset-browse-page}

Så här publicerar du resurser via resursbläddringssidan:

1. Klicka på **Assets** i avsnittet **Assets Management** som finns i den vänstra rutan.
2. Markera en eller flera resurser eller mappar som du vill publicera och klicka på **Publicera**.
3. Välj **AEM** och klicka på **Publicera** för att publicera resurser på AEM och Dynamic Media.
   Bläddra bland ![resurser](/help/assets/assets/browse-uactivation-immediate.svg)
Du kan inte publicera en mapp som har läget för dynamisk mediepublicering inställt på **Selektiv publicering.** Alla andra markerade mappar eller resurser publiceras till AEM och Dynamic Media när du har valt AEM.
   Bläddra bland ![resurser](/help/assets/assets/browse-selective123.svg)

## Publicera resurser med sökresultatsidan {#publish-assets-using-search-results-page}

Så här publicerar du resurser med resurssökningens resultatsida:

1. Ange villkoren i sökfältet och klicka på sökikonen för att visa resultatet.
2. Markera de resurser som du vill publicera och klicka på **Publicera.**
3. Välj AEM, Dynamic Media eller båda beroende på dina behov och klicka sedan på **Publicera.**
   ![sökbild](/help/assets/assets/search-mode.svg)
Alternativet att publicera till Dynamic Media på sökresultatsidan beror på det dynamiska publiceringsläget som är inställt på den mapp där resursen är tillgänglig i databasen.

   >[!NOTE]
   >
   >Om du markerar en mapp och klickar på **Publicera** på sökresultatsidan visar Experience Manager Assets ett alternativ för att publicera resurser på AEM och inte på Dynamic Media, oavsett mappens inställningar för publiceringsläge för dynamiska media.

## Kontrollera publiceringsstatus {#check-publish-status}

Så här kontrollerar du publiceringsstatus för en resurs eller mapp:

1. Klicka på **[!UICONTROL Assets]** i avsnittet **[!UICONTROL Assets Management]** i den vänstra rutan.
2. Växla till listvyn med vyväljaren. Du kan visa resursegenskaper som AEM-publicering, Dynamic Media Publish, titel, storlek, dimensioner och så vidare.\
   Om en resurs eller mapp inte publiceras visas statusen för kolumnerna **AEM Publish** och **Dynamic Media Publish** som **N/A.**
   ![kontrollera publiceringsstatus1](/help/assets/assets/check-publish-status1.png)
Om du inte kan visa kolumnerna AEM Publish och Dynamic Media Publish i listvyn:
   1. Klicka på ![inställningar](/help/assets/assets/settings-icon.svg) och välj kolumnerna **AEM Publish** och **Dynamic Media Publish** i dialogrutan **Konfigurerbara kolumner**.
   2. Klicka på **Bekräfta.** Experience Manager Assets lägger till de markerade kolumnerna i listvyn.

      ![kontrollera publiceringsstatus2](/help/assets/assets/check-publish-status2.png)

Du kan också kontrollera en resurspubliceringsstatus genom att markera en resurs och klicka på **Information.** Informationen är tillgänglig i avsnittet **Publicera** som är tillgängligt i den högra rutan. I avsnittet **Publicera** visas datumet när resurserna publiceras till Dynamic Media och AEM. Om du behöver visa tidpunkten när resurserna publiceras kan du navigera till listvyn och visa dessa detaljer.

![kontrollera publiceringsstatus 3](/help/assets/assets/check-publish-status3.png)

## Begränsningar {#limitations}

Följande funktioner är inte tillgängliga just nu när du publicerar material till AEM och Dynamic Media:

* Publicera material på AEM och Dynamic Media från sidan Resursinformation.
* Visualisera slutpunkterna där resurserna publiceras med Snabbpubliceringsguiden.
* Lägg till eller ta bort fler resurser i Snabbpubliceringsguiden.
* En sida som visar publicerade resurser.
* Möjlighet att kopiera eller klistra in Dynamic Media URL på resursnivå (om resurserna publiceras till Dynamic Media).
* Möjlighet att publicera referenser (resurser, taggar och så vidare) när du publicerar till AEM.
* Möjlighet att skriva över synkroniseringsstatusen för dynamiska media på mappnivå.
* Möjlighet att skriva över läget Dynamic Media Publish på mappnivå
* Hantera publikation stöds inte ännu.
