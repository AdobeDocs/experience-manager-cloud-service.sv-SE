---
title: Hur sparar man det grundläggande komponentbaserade adaptiva formuläret som ett utkast och använder komponenten Utkast och inskickat material för att lista utkast och inskickade dokument?
description: Lär dig spara grundkomponentbaserade adaptiva formulär som utkast. Vill du också veta hur du använder komponenten Utkast och inskickningar för att lista utkast och inskickade ansökningar för inloggade användare?
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# Spara formulär som utkast och lista dem på sidan Webbplatser

<!--This article provides information about the Auto-save feature, which is currently available as a pre-release feature. The pre-release feature is accessible only through our [pre-release channel](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features).-->

Tänk dig en användare som börjar fylla i ett formulär men behöver göra en paus och returnera det senare. AEM har ett `save-as-draft`-alternativ som gör att användaren kan spara formuläret som ett utkast för framtida slutförande. För att underlätta detta tillhandahåller AEM Forms Portal-komponenten **Utkast och inskickat material** som finns i kartongen och som visar utkast och inskickade data på AEM Sites sidor. Komponenten listar formulär som har sparats som utkast för senare ifyllnad samt de som har skickats in. Endast inloggade användare kan redigera sina utkast eller visa sina skickade formulär. Om en anonym användare navigerar genom listan med formulär med komponenten **Sök efter och visa** och sparar ett formulär som ett utkast, visas det utkastet inte med komponenten **Utkast och överföringar** . Om du vill visa utkast och inskickade formulär måste användarna vara inloggade när de skickas.

![Ikonen Utkast](assets/drafts-component.png)

## Krav

* Installera den senaste versionen för att aktivera adaptiva Forms Core-komponenter för din AEM Cloud-tjänstmiljö.

  När du har distribuerat de senaste Core-komponenterna till din miljö blir Forms Portal-komponenterna tillgängliga i din redigeringsmiljö.

* [Konfigurera Azure Storage och Unified Storage Connector för Forms Portal-komponenten för utkast och överföringar](#configure-azure-storage-and-unified-storage-connector-for-drafts--submissions-forms-portal-component)

### Konfigurera Azure Storage och Unified Storage Connector för Forms Portal-komponenten för utkast och överföringar

Komponenten **Utkast och överföringar** behöver en lagringskonfiguration för att kunna spara och visa utkast på AEM Sites-sidan. Unified Storage Connector erbjuder ett ramverk för att länka AEM till extern lagring. Om du vill spara formuläret som ett utkast måste du se till att du har ett Azure-lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till lagringskontot [!DNL Azure]. När du har ett Azure-lagringskonto och åtkomstnyckeln gör du följande för att skapa en Azure Storage-konfiguration:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.

   ![Val av Azure-lagringskort](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Välj en konfigurationsmapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.

   ![Välj Azure Storage Configuration-mapp](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Ange en rubrik för konfigurationen i fältet **[!UICONTROL Title]**.
1. Ange namnet på lagringskontot [!DNL Azure] i fälten **[!UICONTROL Azure Storage Account]** och **[!UICONTROL Azure Access Key]**.

   ![Azure-lagringskonfiguration](/help/forms/assets/save-form-as-draft-azure-storage.png)

   Ange `Connection String` i textrutan `Azure Storage Account` och `Azure Key` i textrutan `Azure Access key`.

1. Klicka på **Spara**.

   >[!NOTE]
   >
   > Du kan hämta **[!UICONTROL Azure Storage Account]** och **[!UICONTROL Azure Access Key]** från [Microsoft Azure-portalen](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).

   När du har skapat Azure Storage-konfigurationen konfigurerar du Unified Storage Connector för Forms Portal enligt följande:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Unified Storage Connector]**.

   ![Enhetlig anslutningslagring](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. I avsnittet **[!UICONTROL Forms Portal]** väljer du **[!UICONTROL Azure]** i listrutan **[!UICONTROL Storage]**.
1. Ange konfigurationssökvägen för Azure-lagringskonfigurationen i fältet **[!UICONTROL Storage Configuration Path]**.

   ![Inställning för enhetlig anslutningslagring](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Välj **[!UICONTROL Save]**.

>[!NOTE]
>
> Om du behöver konfigurera ett annat lagringsalternativ än Azure kan du skriva till aem-forms-ea@adobe.com från din officiella e-postadress med dina detaljerade krav.

När du har konfigurerat Azure Storage och Unified Storage Connector för lagring av utkast och skickade formulär lägger du till komponenten **Utkast och överföringar** på AEM Sites-sidan.

## Hur lägger man till komponenten Utkast och inskickat material på en AEM Sites-sida?

Du kan använda färdiga Forms Portal-komponenter för att lista utkast och inskickade dokument på sidan Webbplatser. Utför följande steg för att lägga till portalkomponenten **Utkast och överföringar**:

1. Öppna AEM Sites-sidan i **redigeringsläge**.
1. Gå till **[!UICONTROL Page Information]** > **[!UICONTROL Edit Template]**
   ![Redigera mallprincip](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Klicka på **[!UICONTROL Policy]** och markera kryssrutan **[!UICONTROL Drafts & Submissions]** under **[Projektnamn för AEM-arkityp] - Forms och kommunikationsportal**.

   ![Principval](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Klicka på **[!UICONTROL Done]**.
1. Öppna nu AEM Sites-sidan igen i redigeringsläget.
1. Leta reda på det avsnitt i sidredigeraren där du kan lägga till Forms Portal-komponenten.
1. Klicka på ikonen **Lägg till** . Ikonen är ett plustecken (+) som anger att du kan lägga till nya komponenter.

   Om du klickar på ikonen **Lägg till** visas dialogrutan **Infoga ny komponent** som visar olika komponenter som ska infogas.

   >[!NOTE]
   >
   > Du kan också dra och släppa komponenten.

1. Bläddra bland de tillgängliga komponenterna i dialogrutan och välj önskad komponent i listan. Välj till exempel komponenten **Utkast och överföringar** i listan om du vill lägga till Forms Portal-komponenten **Utkast och överföringar** .

   ![Lägg till utkast och skicka-komponent](/help/forms/assets/save-form-as-draft-add-dns.png)

Konfigurera nu egenskaperna för komponenten **Utkast och överföringar** enligt kraven.

## Konfigurera egenskaper för komponenten Utkast och överföringar

Du kan konfigurera egenskaperna för **Utkast och överföringar**:

1. Markera komponenten **Utkast och överföringar**.
1. Klicka på ikonen ![Konfigurera](assets/configure_icon.png) så visas dialogrutan.
1. Ange följande i dialogrutan **[!UICONTROL Drafts and Submissions]**:

   * **Titel** Om du vill identifiera en komponent på en webbplatssida visas titeln som standard ovanpå komponenten.
   * **Välj typ**: Om du vill ange formulärlistan som utkast eller skickade formulär. Om du väljer **Utkast till Forms** visas de formulär som sparats som utkast. Om du väljer **Skickat Forms** visas även de formulär som skickats in av inloggade användare.
   * **Layout**: Om du vill visa en lista med formulärutkast eller skickade formulär i kort- eller listformat.

   ![Egenskaper för utkast och skicka komponent](/help/forms/assets/save-form-as-draft-dns-properties.png)

## Konfigurera formulär som ska sparas som utkast

Du kan konfigurera Adaptiv Forms på följande två sätt:

* [Användaråtgärd](#user-action)
* [Spara automatiskt](#auto-save)

### Användaråtgärd

>[!NOTE]
>
> Kontrollera att [Core Components-versionen är inställd på 3.0.24 eller senare](https://github.com/adobe/aem-core-forms-components) för att spara formulär som utkast med regeln **Spara formulär** .

Om du vill spara ett formulär som ett utkast skapar du en **Spara formulär**-regel för en formulärkomponent, till exempel en knapp. När användaren klickar på knappen aktiveras regeln och formuläret sparas som ett utkast. Så här skapar du en **Spara formulär**-regel för en knappkomponent:

1. Öppna ett adaptivt formulär i redigeringsläge.
1. Välj ikonen **[!UICONTROL Edit Rules]** för att öppna regelredigeraren för komponenten **Button**.
1. Välj **[!UICONTROL Create]** om du vill konfigurera och skapa regeln för knappen.
1. I avsnittet **[!UICONTROL When]** väljer du **är klickad** och i avsnittet **[!UICONTROL Then]** väljer du alternativet **Spara formulär**.
1. Välj **[!UICONTROL Done]** om du vill spara regeln.

   ![Skapa regel för knapp](/help/forms/assets/save-form-as-drfat-create-rule.png)

När du förhandsgranskar ett adaptivt formulär, fyller i det och klickar på knappen **Spara formulär** sparas formuläret som ett utkast.

### Utkast

>[!NOTE]
>
> Kontrollera att [Core Components-versionen är inställd på 3.0.52 eller senare](https://github.com/adobe/aem-core-forms-components) för att spara formulär som utkast med funktionen Spara automatiskt.

Du kan också konfigurera ett adaptivt formulär så att det sparas automatiskt baserat på en tidsbaserad händelse och säkerställer att formuläret sparas efter den angivna varaktigheten. När du [aktiverar Forms Portal-komponenter för din miljö](/help/forms/list-forms-on-sites-page.md#enable-forms-portal-components-for-your-existing-environment) visas fliken **Spara automatiskt** i Forms behållaregenskaper. Du kan konfigurera funktionen för att spara automatiskt för ett anpassat formulär:

1. Öppna ett adaptivt formulär i redigeringsläge i författarinstansen.
1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen ![Egenskaper för stödlinjebehållare](/help/forms/assets/configure-icon.svg) och öppna fliken **[!UICONTROL Drafts]**.

   ![Spara automatiskt](/help/forms/assets/auto-save.png)

1. Markera kryssrutan **[!UICONTROL Automatically Save Drafts]** om du vill aktivera autosparande av formuläret som utkast.
1. Konfigurera **[!UICONTROL Save Preference]** som **Spara utkast med regelbundna intervall** om du vill spara formuläret <!--based on the occurrence of an event or--> automatiskt efter ett visst tidsintervall.
1. Ange tidsintervallet i **[!UICONTROL Save interval frequency (Seconds)]** för att ange den varaktighet som utlöser det automatiska sparandet av formuläret vid det definierade intervallet.
1. Klicka på **[!UICONTROL Done]**.

## Visa utkast/skickade formulär på webbplatssidan med komponenten Utkast och inskickningar

Om du vill visa sparade utkast eller skickade formulär använder du Forms Portal-komponenten **Utkast och överföringar** .
När **[!UICONTROL Select Type]** har valts som **Utkast-Forms** i dialogrutan [Konfigurera i komponenten Utkast och överföringar](#configure-properties-of-the-drafts--submissions-component) visas de formulär som har sparats som utkast på sidan Webbplatser. Du kan öppna utkasten genom att klicka på ellipsen (..) för att fylla i formuläret.

![Ikonen Utkast](assets/drafts-component.png)

När **[!UICONTROL Select Type]** har valts som **Skickat Forms** i dialogrutan [Konfigurera i komponenten Utkast och överföringar](#configure-properties-of-the-drafts--submissions-component) visas de skickade formulären. Du kan visa de skickade formulären men inte redigera dem.

![Ikonen Skicka](assets/submission-listing.png)

Du kan också ta bort formulären genom att klicka på ellipsen (..) som visas i formulärets nedre högra hörn.

>[!NOTE]
>
> I Forms Portal har komponenten Utkast och inskickningar bara stöd för inskickningar från Foundation-baserade formulär.

## Nästa steg

I nästa artikel kan vi lära oss [hur du lägger till referenser till formulär på sidan Webbplatser med hjälp av komponenten Länka Forms Portal](/help/forms/add-form-link-to-aem-sites-page.md).

## Relaterade artiklar

{{forms-portal-see-also}}

## Se även {#see-also}

{{see-also}}