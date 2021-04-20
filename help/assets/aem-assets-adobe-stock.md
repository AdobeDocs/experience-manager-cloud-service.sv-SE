---
title: Hantera [!DNL Adobe Stock] resurser i [!DNL Assets].
description: Sök, hämta, licensiera och hantera [!DNL Adobe Stock] resurser inifrån [!DNL Adobe Experience Manager]. Använd de licensierade mediefilerna som andra digitala resurser.
contentOwner: AG
feature: Search,Adobe Stock
role: Administrator,Business Practitioner
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
translation-type: tm+mt
source-git-commit: 0da8eb0eac0c58b5212aa264c9042523460e474e
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 2%

---

# Använd [!DNL Adobe Stock]-resurser i [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Organisationer kan integrera sin [!DNL Adobe Stock] Enterprise-plan med [!DNL Experience Manager Assets] för att säkerställa att licensierade mediefiler finns tillgängliga i stor omfattning för kreativa projekt och marknadsföringsprojekt med de kraftfulla resurshanteringsfunktionerna i [!DNL Experience Manager].

[!DNL Adobe Stock] ger designers och företag tillgång till miljontals utvalda och royaltyfria foton, vektorer, illustrationer, videor, mallar och 3D-resurser av hög kvalitet för alla kreativa projekt. [!DNL Experience Manager] -användare snabbt kan hitta, förhandsgranska och licensiera  [!DNL Adobe Stock] resurser som har sparats i  [!DNL Experience Manager], utan att behöva lämna  [!DNL Experience Manager] gränssnittet.

## Integrera [!DNL Experience Manager] och [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Om du vill tillåta kommunikation mellan [!DNL Experience Manager] och [!DNL Adobe Stock] skapar du en IMS-konfiguration och en [!DNL Adobe Stock]-konfiguration i [!DNL Experience Manager].

>[!NOTE]
>
>Endast [!DNL Experience Manager] administratörer och [!DNL Admin Console] administratörer för en organisation kan utföra integreringen eftersom den kräver administratörsbehörighet.

### Skapa en IMS-konfiguration {#create-an-ims-configuration}

1. I [!DNL Experience Manager]-användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Klicka på **[!UICONTROL Create]** och välj **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Återanvänd ett befintligt certifikat eller välj **[!UICONTROL Create new certificate]**.
1. Klicka på **[!UICONTROL Create certificate]**. Ladda ned den offentliga nyckeln när du har skapat den. Klicka på **[!UICONTROL Next]**. Lämna skärmen [!UICONTROL Adobe IMS Technical Account Configuration] öppen så att de värden som krävs anges inom kort.
1. Åtkomst till [Adobe Developer Console](https://console.adobe.io). Se till att ditt konto har administratörsbehörighet för organisationen som integreringen krävs för.
1. Klicka på **[!UICONTROL Create new project]** och klicka på **[!UICONTROL Add API]**. Välj **[!UICONTROL Adobe Stock]** i listan över API:er som är tillgängliga för dig. Välj [!UICONTROL OAUTH 2.0 Web].
1. Ange **[!UICONTROL Default redirect URI]**- och **[!UICONTROL Redirect URI pattern]**-värden. Klicka på **[!UICONTROL Save configured API]**. Kopiera genererat ID och hemlighet.
1. På skärmen [!UICONTROL Adobe IMS Technical Account Configuration] anger du värdena i rutorna **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]** och **[!UICONTROL Payload]**. Mer information om dessa värden finns i [Snabbstart för JWT-autentisering](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Skapa [!DNL Adobe Stock]-konfiguration i [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. I [!DNL Experience Manager] går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Klicka på **[!UICONTROL Create]** för att skapa en konfiguration och koppla den till din befintliga IMS-konfiguration. Välj `PROD` som miljöparameter.
1. Lämna en plats som den är i fältet **[!UICONTROL Licensed Assets Path]**. Ändra inte platsen där du vill lagra [!DNL Adobe Stock]-resurserna.
1. Skapa genom att lägga till alla nödvändiga egenskaper. Klicka på **[!UICONTROL Save & Close]**.
1. Lägg till [!DNL Experience Manager] användare eller grupper, som kan licensiera resurserna.

>[!NOTE]
>
>Om det finns flera [!DNL Adobe Stock]-konfigurationer väljer du den önskade konfigurationen på panelen Användarinställningar. Du öppnar panelen från Experience Manager hemsida genom att klicka på användarikonen och sedan på **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

## Använd och hantera [!DNL Adobe Stock]-resurser i [!DNL Experience Manager] {#usemanage}

Med den här funktionen kan organisationer tillåta användare att arbeta med [!DNL Adobe Stock]-resurser i [!DNL Experience Manager Assets]. I [!DNL Experience Manager]-användargränssnittet kan användare söka efter [!DNL Adobe Stock]-resurser och licensiera de nödvändiga resurserna.

När en [!DNL Adobe Stock]-resurs har licensierats i [!DNL Experience Manager] kan den användas och hanteras som en vanlig resurs. I [!DNL Experience Manager] kan användarna söka efter och förhandsgranska resurserna; kopiera och publicera tillgångarna, dela resurserna på [!DNL Brand Portal], få tillgång till och använda resurserna via [!DNL Experience Manager]-datorprogrammet; och så vidare.

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

### Sök efter resurser {#find-assets}

Dina [!DNL Experience Manager]-användare kan söka efter resurser i både, [!DNL Experience Manager] och [!DNL Adobe Stock]. När sökplatsen inte är begränsad till [!DNL Adobe Stock] visas sökresultaten från [!DNL Experience Manager] och [!DNL Adobe Stock].

* Om du vill söka efter [!DNL Adobe Stock] resurser klickar du på **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* Om du vill söka efter resurser i [!DNL Adobe Stock] och [!DNL Experience Manager Assets] klickar du på sök ![sök](assets/do-not-localize/search_icon.png).

Du kan också börja skriva `Location: Adobe Stock` i sökfältet för att välja [!DNL Adobe Stock]-resurser. [!DNL Experience Manager] har avancerade filtreringsfunktioner för de sökbara resurserna, vilket gör att användarna snabbt kan nollställa de resurser som behövs med hjälp av filter, som typer av resurser som stöds, bildorientering och licensierat läge.

>[!NOTE]
>
>Resurser som söks igenom från [!DNL Adobe Stock] visas bara i [!DNL Experience Manager]. [!DNL Adobe Stock] resurser hämtas och lagras i  [!DNL Experience Manager] databasen först när en användare antingen  [sparar en ](/help/assets/aem-assets-adobe-stock.md#saveassets) resurslicens  [och sparar en resurs](/help/assets/aem-assets-adobe-stock.md#licenseassets). Resurser som redan är lagrade i [!DNL Experience Manager] visas och markeras för att underlätta referens och åtkomst. Dessutom sparas [!DNL Stock]-resurserna med ytterligare metadata för att ange källan som [!DNL Stock].

![Sökfilter i Experience Manager och markerade Adobe Stock-resurser i sökresultat](assets/aem-search-filters2.jpg)

*Bild: Sök efter filter i  [!DNL Experience Manager] och markerade  [!DNL Adobe Stock] resurser i sökresultaten.*

### Spara och visa nödvändiga resurser {#saveassets}

Välj en resurs som du vill spara i [!DNL Experience Manager]. Klicka på [!UICONTROL Save] i verktygsfältet överst och ange resursens namn och plats. De olicensierade resurserna sparas lokalt med en vattenstämpel.

Nästa gång du söker efter resurser markeras de sparade resurserna med ett märke som anger att sådana resurser är tillgängliga i [!DNL Experience Manager Assets].

>[!NOTE]
>
>De nyligen tillagda resurserna visas med märket Nytt i stället för Licensierad.

### Licensiera resurser {#licenseassets}

Användare kan licensiera [!DNL Adobe Stock]-resurser genom att använda kvoten för deras [!DNL Adobe Stock] Enterprise-plan. När du licensierar en resurs sparas den utan vattenstämpel och är tillgänglig för sökning och användning i [!DNL Experience Manager Assets].

![Dialogruta där du kan licensiera och spara Adobe Stock-resurser i Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Bild: Dialogruta där du kan licensiera och spara  [!DNL Adobe Stock] resurser  [!DNL Experience Manager Assets].*

### Få åtkomst till metadata och resursegenskaper {#access-metadata-and-asset-properties}

Användarna kan komma åt och förhandsgranska metadata, inklusive metadataegenskaperna [!DNL Adobe Stock] för resurserna som sparats i [!DNL Experience Manager], och lägga till **[!UICONTROL License References]** för en resurs. Uppdateringarna av licensreferensen synkroniseras dock inte mellan [!DNL Experience Manager]- och [!DNL Adobe Stock]-webbplatsen.

Användarna kan se egenskaperna för både, licensierade och olicensierade resurser.

![Visa och få tillgång till metadata och licensreferenser för sparade resurser](assets/metadata_properties.jpg)

*Bild: Visa och öppna metadata och licensreferenser för sparade resurser.*

## Kända begränsningar {#known-limitations}

* **Varning om redigeringsbild visas** inte: När du licensierar en bild kan du inte kontrollera om en bild endast är för redaktionellt bruk. För att förhindra eventuell felaktig användning kan administratören stänga av åtkomsten till redaktionella mediefiler från Admin Console.

* **Fel licenstyp visas**: Det är möjligt att en felaktig licenstyp visas i  [!DNL Experience Manager] för en resurs. Användarna kan logga in på [!DNL Adobe Stock]-webbplatsen för att se licenstypen.

* **Referensfält och metadata synkroniseras** inte: När en användare uppdaterar ett licensreferensfält uppdateras licensreferensinformationen i  [!DNL Experience Manager] men inte på  [!DNL Adobe Stock] webbplatsen. Om användaren uppdaterar referensfälten på webbplatsen [!DNL Adobe Stock] synkroniseras inte uppdateringarna i [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Videosjälvstudiekurs om hur du använder Adobe Stock-resurser med Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Adobe Stock Enterprise Plan - hjälp](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock FAQ](https://helpx.adobe.com/stock/faq.html)

