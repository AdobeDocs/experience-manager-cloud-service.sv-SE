---
title: Integrera fjärr-AEM Assets med AEM Sites
description: Lär dig hur du konfigurerar och ansluter AEM webbplatser med Godkänd AEM Assets i Creative Cloud.
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# Integrera fjärr-AEM Assets med AEM Sites  {#integrate-approved-assets}

Effektiv hantering av digitala resurser är avgörande för att ni ska kunna leverera engagerande och enhetliga varumärkesupplevelser på olika onlineplattformar. Dynamic Media med OpenAPI-funktioner förbättrar den digitala resurshanteringen genom smidig integrering mellan AEM Sites och AEM Assets as a Cloud Service. Med den här innovativa funktionen kan ni enkelt dela och hantera olika typer av godkända digitala resurser i flera AEM miljöer, vilket effektiviserar arbetsflödena för webbplatsförfattare och redaktörer.

Med Dynamic Media med OpenAPI-funktioner kan webbplatsförfattare använda resurser från fjärr-DAM direkt i AEM Page Editor och [Innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html), vilket förenklar processerna för att skapa och hantera innehåll.

Användare kan ansluta flera AEM Sites-instanser till en fjärrdistribution av DAM, utan begränsningar för högsta antal, vilket är en betydande fördel framför [Uppkopplad Assets](use-assets-across-connected-assets-instances.md) -funktion.

![bild](/help/assets/assets/connected-assets-rdam.png)

Efter den första konfigurationen kan användare skapa sidor i AEM Sites-instansen och lägga till resurser efter behov. När de lägger till resurser kan de antingen välja resurser som lagras i deras lokala DAM eller bläddra och använda resurserna som finns i fjärr-DAM.

Dynamic Media med OpenAPI-funktioner har flera andra fördelar, som att komma åt och använda fjärrresurser i Content Fragment, hämta metadata för fjärrresurserna och mycket annat. Läs mer om de andra [fördelarna med Dynamic Media med OpenAPI-funktioner jämfört med uppkopplade Assets](/help/assets/dynamic-media-open-apis-faqs.md).

## Innan du börjar {#pre-requisits-sites-integration}

* Ställ in följande [miljövariabler](/help/implementing/cloud-manager/environment-variables.md#add-variables) för AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` refererar till program-ID <br>
     `eYYYY` refererar till miljö-ID

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  eller konfigurera [OSGi-inställningar](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) för AEM 6.5 i AEM Sites-instansen genom att följa dessa steg:

   1. Logga in på konsolen och klicka på **[!UICONTROL OSGi]>** eller använd den direkta URL:en, till exempel: `http://localhost:4502/system/console/configMgr`

   1. Lägg till **[!UICONTROL repositoryID]**= &quot;delivery-pxxx-eyyyyy.adobeaemcloud.com&quot; och **[!UICONTROL imsClient]**= [IMSClientId]
Läs mer om [IMS-autentisering](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* IMS-åtkomst för att logga in på en DAM AEM as a Cloud Service-fjärrinstans.

* Aktivera växlingen Dynamic Media med OpenAPI-funktioner i fjärr-DAM.

* Konfigurera Image v3-komponenten i AEM Sites-instansen. Om komponenten inte finns hämtar och installerar du [innehållspaket](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Få åtkomst till resurser från fjärr-DAM {#fetch-assets}

Med Dynamic Media med OpenAPI-funktioner kan du komma åt resurser som är tillgängliga i din Remote DAM-instans på den lokala AEM Sites Page Editor och AEM Content Fragment.

![bild](/help/assets/assets/open-APIs.png)

### Åtkomst till fjärrresurser i AEM Page Editor {#access-assets-page-editor}

Följ stegen nedan för att använda fjärrresurser i AEM Page Editor på din AEM Sites-instans. Du kan göra detta genom att integrera AEM as a Cloud Service och AEM 6.5.

1. Gå till **[!UICONTROL Sites]** > _din webbplats_ där AEM **[!UICONTROL Page]** finns där du måste lägga till fjärrresursen.
1. Navigera till AEM **[!UICONTROL Page]** på din webbplats under **[!UICONTROL Sites]** där du tänker lägga till fjärrresursen.
1. Markera sidan och klicka på **[!UICONTROL Edit (_e _)]**. AEM **[!UICONTROL Page Editor]**öppnas.
1. Klicka på layoutbehållaren och lägg till en **[!UICONTROL Image]** -komponenten.
1. Klicka på **[!UICONTROL Image]** och klicka på ![inställningsikon](/help/assets/assets/do-not-localize/settings-icon.svg) -ikon.
1. Avmarkera **[!UICONTROL Inherit featured image from page]** alternativ.
1. Klicka **[!UICONTROL Pick]** och markera **[!UICONTROL Remote]**.
   ![bild](/help/assets/assets/uncheck-inherit-option.jpg)

   Du uppmanas att logga in.
1. Markera resursen och klicka på **[!UICONTROL Select]**.
1. Lägg till en alternativ text och klicka på **[!UICONTROL Done]**.
   <br> Fjärrresursen visas i bildkomponenten. Du kan också verifiera resursens leverans-URL när den läses in på sidan eller genom att använda fliken Förhandsgranska. Leverans-URL:en anger att resursen fjärransluts.

Du har bara åtkomst till fjärranslutna resurser i AEM redigeringsprogram direkt för Image Core Component v3 och Teaser Core Component v2. För andra komponenter, inklusive anpassade komponenter, krävs anpassningar för att integrera resursväljaren med dessa komponenter.

#### Video: Få åtkomst till fjärrresurser AEM sidredigeraren

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Få åtkomst till fjärrresurser i AEM innehållsfragment {#access-assets-content-fragment}

Följ stegen nedan för att använda fjärrresurser i AEM innehållsfragment på din AEM Sites-instans. Du kan göra den här integreringen i AEM 6.5 och inte i AEM as a Cloud Service.

1. Gå till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Välj resursmapp där innehållsfragmentet finns.
1. Markera innehållsavsnittet och klicka på **[!UICONTROL Edit (_e _)]**.

   >[!NOTE]
   >
   >Om du inte har AEM Content Fragment-modell kan du behöva [skapa en](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. Klicka på ![bockikon](/help/assets/assets/do-not-localize/checkmark-icon.svg) -ikonen bredvid textkomponenten.
1. Välj **[!UICONTROL Remote]** för att hämta resursen från fjärr-DAM. <br>
Du kan antingen välja **[!UICONTROL Local]** eller **[!UICONTROL Remote]** DAM-databas baserat på dina behov.

   ![image](/help/assets/assets/cf-pick.jpg)
Du uppmanas att logga in.
1. Välj resursen och klicka på **[!UICONTROL Select]**.
   <br> URL:en för fjärrresursen visas i textkomponenten.

#### Video: Få åtkomst till fjärrresurser i AEM innehållsfragment

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Få åtkomst till fjärrresurser i Edge Delivery Services {#access-assets-eds}

Du kan även komma åt fjärrresurser i Edge Delivery Services. Mer information finns i [Använda material från Assets as a Cloud Service som levereras med Dynamic Media med OpenAPI-funktioner](https://www.aem.live/docs/aem-assets-sidekick-plugin#utilizing-assets-from-assets-cloud-services-delivered-via-dynamic-media-with-openapi).
