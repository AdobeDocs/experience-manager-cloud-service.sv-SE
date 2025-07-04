---
title: Integrera fjärr-AEM Assets med AEM Sites
description: Lär dig hur du konfigurerar och ansluter AEM webbplatser med Godkänd AEM Assets.
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 0%

---

# Integrera fjärr-AEM Assets med AEM Sites  {#integrate-approved-assets}

Effektiv hantering av digitala resurser är avgörande för att ni ska kunna leverera engagerande och enhetliga varumärkesupplevelser på olika onlineplattformar. Dynamic Media med OpenAPI-funktioner förbättrar hanteringen av digitala resurser genom smidig integrering mellan AEM Sites och AEM Assets as a Cloud Service. Med den här innovativa funktionen kan du enkelt dela och hantera olika typer av godkänt digitalt material i olika AEM-miljöer, vilket effektiviserar arbetsflödena för webbplatsförfattare och redaktörer.

Med Dynamic Media med OpenAPI-funktioner kan webbplatsförfattare använda resurser från fjärr-DAM direkt i AEM Page Editor och [Content Fragment](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html?lang=sv-SE) vilket förenklar processerna för att skapa och hantera innehåll.

Användare kan ansluta flera AEM Sites-instanser, utan begränsningar av det högsta antalet, till en DAM-fjärrdistribution, vilket är en betydande fördel jämfört med funktionen [Ansluten Assets](use-assets-across-connected-assets-instances.md).

![bild](/help/assets/assets/connected-assets-rdam.png)

Efter den första konfigurationen kan användare skapa sidor i AEM Sites-instansen och lägga till resurser efter behov. När de lägger till resurser kan de antingen välja resurser som lagras i deras lokala DAM eller bläddra och använda resurserna som finns i fjärr-DAM.

Dynamic Media med OpenAPI-funktioner har flera andra fördelar, som att komma åt och använda fjärrresurser i Content Fragment, hämta metadata för fjärrresurserna och mycket annat. Lär dig mer om de andra [fördelarna med Dynamic Media med OpenAPI-funktioner jämfört med Connected Assets](/help/assets/dynamic-media-open-apis-faqs.md).

## Innan du börjar {#pre-requisites-sites-integration}

Stöd för fjärrresurser med Dynamic Media med OpenAPI-funktioner kräver:

* AEM 6.5 SP 18+ eller AEM as a Cloud Service

* Core Components version 2.23.2 eller senare

* Ställ in följande [miljövariabler](/help/implementing/cloud-manager/environment-variables.md#add-variables) för AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxx-eyyyyy.adobeaemcloud.com&quot; <br>

     `pXXXX` refererar till program-ID <br>
     `eYYYY` refererar till miljö-ID

  Variablerna ställs in med Cloud Manager användargränssnitt i AEM as a Cloud Service-miljön som fungerar som din lokala Sites-instans.

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]: Du måste skicka en Adobe-supportbiljett för att få ID:t för IMS-klienten.

     eller konfigurera [OSGi-inställningarna](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html?lang=sv-SE) för AEM 6.5 i AEM Sites-instansen genom att följa dessa steg:

   1. Logga in på konsolen och klicka på **[!UICONTROL OSGi]>** eller
använd den direkta URL:en, till exempel: `https://localhost:4502/system/console/configMgr`

   1. Konfigurera OSGi-konfigurationen för **nästa generations dynamiska mediekonfiguration** (`NextGenDynamicMediaConfigImpl`) enligt följande och ersätt värdena med värdena i din fjärrmiljö.

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg` är inte en obligatorisk inmatning.
      `repositoryId` = &quot;delivery-pxxx-eyyyyy.adobeaemcloud.com&quot;
där `pXXXX` refererar till program-ID
      `eYYYY` refererar till miljö-ID

      ![Nästa generations OSGi-konfigurationsfönster för Dynamic Media Config](/help/assets/assets/remote-assets-osgi.png)

  Läs mer om [IMS-autentisering](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html?lang=sv-SE).

  Mer information om hur du konfigurerar OSGi finns i följande dokument:

   * [Konfigurera OSGi för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=sv-SE) för AEM as a Cloud Service
   * [Konfigurerar OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=sv-SE) för AEM 6.5

* IMS-åtkomst för att logga in på en DAM AEM as a Cloud Service-fjärrinstans. Det avser den webbplatsförfattare som har IMS-åtkomst till den fjärranslutna DAM-miljön.

* Konfigurera Image v3-komponenten i AEM Sites-instansen. Om komponenten inte finns hämtar och installerar du [innehållspaketet](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Konfigurera HTTPS {#https}

Vi rekommenderar att du kör alla dina AEM-produktioner med HTTP. Dina lokala utvecklingsmiljöer kanske inte konfigureras som sådana. Fjärrresurser som använder Dynamic Media med OpenAPI kräver dock HTTPS för att fungera.

[Använd den här guiden](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=sv-SE) för att konfigurera HTTPS var du vill använda fjärrresurser, inklusive utvecklingsmiljöer.

## Få åtkomst till resurser från fjärr-DAM {#fetch-assets}

Med Dynamic Media med OpenAPI-funktioner kan du komma åt resurser som finns i din Remote DAM-instans på den lokala AEM Sites Page Editor och AEM Content Fragment.

![bild](/help/assets/assets/open-APIs.png)

### Få åtkomst till fjärrresurser i AEM Page Editor {#access-assets-page-editor}

Följ stegen nedan för att använda fjärrresurser i AEM Page Editor på din AEM Sites-instans. Du kan göra detta genom att integrera AEM as a Cloud Service och AEM 6.5.

1. Gå till **[!UICONTROL Sites]** > _din webbplats_ där AEM **[!UICONTROL Page]** finns där du måste lägga till fjärrresursen.
1. Markera sidan och klicka på **[!UICONTROL Edit (_e _)]**. AEM **[!UICONTROL Page Editor]**&#x200B;öppnas.
1. Klicka på layoutbehållaren och lägg till en **[!UICONTROL Image]**-komponent.
1. Klicka på komponenten **[!UICONTROL Image]** och klicka på ikonen ![settings](/help/assets/assets/do-not-localize/settings-icon.svg) .
1. Avmarkera alternativet **[!UICONTROL Inherit featured image from page]**.
1. Klicka på **[!UICONTROL Pick]** och välj **[!UICONTROL Remote]**.
   ![bild](/help/assets/assets/uncheck-inherit-option.jpg)

   Du uppmanas att logga in.
1. Markera resursen och klicka på **[!UICONTROL Select]**.
1. Lägg till en alternativ text och klicka på **[!UICONTROL Done]**.
   <br> Fjärrresursen visas i bildkomponenten. Du kan också verifiera resursens leverans-URL när den läses in på sidan eller genom att använda fliken Förhandsgranska. Leverans-URL:en anger att resursen fjärransluts.

Du har bara tillgång till fjärranslutna resurser i AEM sidredigerare direkt för Image Core Component v3 och Teaser Core Component v2. För andra komponenter, inklusive anpassade komponenter, krävs anpassningar för att integrera resursväljaren med dessa komponenter.

#### Video: Få åtkomst till fjärrresurser i AEM Page Editor

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Få åtkomst till fjärrresurser i AEM Content Fragment {#access-assets-content-fragment}

Följ stegen nedan för att använda fjärrresurser i AEM Content Fragment på din AEM Sites-instans. Du kan göra detta i AEM 6.5 och inte i AEM as a Cloud Service.

1. Gå till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Välj resursmapp där innehållsfragmentet finns.
1. Markera innehållsavsnittet och klicka på **[!UICONTROL Edit (_e _)]**.

   >[!NOTE]
   >
   >Om du inte har någon AEM Content Fragment-modell kan du behöva [skapa en](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=sv-SE).

1. Klicka på ikonen ![bock](/help/assets/assets/do-not-localize/checkmark-icon.svg) bredvid textkomponenten.
1. Välj **[!UICONTROL Remote]** om du vill hämta resursen från fjärr-DAM. <br>
Du kan antingen välja **[!UICONTROL Local]** eller **[!UICONTROL Remote]** DAM-databas baserat på dina behov.

   ![bild](/help/assets/assets/cf-pick.jpg)
Du uppmanas att logga in.
1. Välj resursen och klicka på **[!UICONTROL Select]**.
   <br> URL:en för fjärrresursen visas i textkomponenten.

#### Video: Få åtkomst till fjärrresurser i AEM Content Fragment

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Få åtkomst till fjärrresurser i Edge Delivery Services {#access-assets-eds}

Du kan få åtkomst till fjärrresurser när du redigerar innehåll i Microsoft Word, Google Docs eller Universal Editor och sedan publicera innehållet till Edge Delivery Services. Ni kan också använda Dynamic Media med OpenAPI för att leverera varumärkesgodkända mediefiler och utnyttja många andra fördelar som det erbjuder. Mer information finns i [Integrera AEM Assets när du redigerar innehåll för Edge Delivery Services](/help/assets/integrate-aem-assets-edge-delivery-services.md).
