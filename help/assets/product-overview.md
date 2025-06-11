---
title: Content Hub - översikt
description: Läs mer om Content Hub, dess viktigaste fördelar, hur man får tillgång till det och hur man kan ge feedback kring de alternativ som finns i Content Hub.
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: cc6c227a566c4d4fd8c9a20d1bb39020974f494f
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# Content Hub - översikt {#overview-content-hub}

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
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub ingår i Experience Manager Assets as a Cloud Service för att demokratisera tillgången till varumärkesinnehåll för organisationer och deras affärspartners. Fokus ligger på att distribuera resurser för aktivering i stor skala och att skapa innehållsvarianter för varumärke, vilket ger förbättrad marknadsföringsflexibilitet.

## Content Hub demo {#content-hub-demo}

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md) och Assets as a Cloud Service innehåller 250 Content Hub-användare. [Assets Prime](/help/assets/assets-prime.md) innehåller 50 Content Hub-användare.

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

## Varför Content Hub?

Content Hub har följande fördelar:

**Hitta och dela alla varumärkesgodkända resurser som finns i en intuitiv portal**

AEM Assets fungerar som en enda källa till sanning och alla godkända mediefiler finns automatiskt tillgängliga på Content Hub i en hierarki för att förbättra sökupplevelsen.

**Konfigurerbart användargränssnitt**

De vanligaste egenskaperna i Content Hub, t.ex. sökfilter, fält som är tillgängliga när du lägger till eller importerar resurser, resursegenskaper, banderollinnehåll för varumärkning kan konfigureras och en administratör kan enkelt konfigurera Content Hub användargränssnitt baserat på deras behov.

**Ge icke-kreatörer möjlighet att redigera och mixa om innehåll samtidigt som de behåller sitt varumärke**

Med Content Hub kan du skapa nytt innehåll med Adobe Express (om du har Adobe Express-rättigheter). Du kan redigera befintligt innehåll med lättanvända verktyg, producera varumärkesanpassade varianter med mallar och märkeselement och skapa nytt innehåll med de senaste GenAI-funktionerna från Adobe Firefly.

**Få insikter om hur innehåll används i olika team**

[!DNL Content Hub] ger värdefulla insikter om resurser, och åtgärdar en vanlig utmaning som marknadsföringsintressenter ofta stöter på - statistik om resursanvändning som används i marknadsföringskampanjer, kanaler och olika regioner. Genom att få en tydlig förståelse för resursernas prestanda och popularitet kan ni få användbara insikter som är viktiga för att förbättra användarupplevelsen.

## Förutsättningar {#prerequisites-content-hub}

Content Hub kräver en produktionsredigeringsmiljö för Experience Manager as a Cloud Service, version 2024.6 eller senare (lägsta version är 2024.6.16799).

## Hur kommer jag åt Content Hub? {#access-content-hub}

[När du har konfigurerat Content Hub](/help/assets/deploy-content-hub.md) och lagt till en användare i [Content Hub produktprofil](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) kan du få åtkomst till Content Hub på följande sätt:

* Öppna Content Hub via följande länk:

  `https://experience.adobe.com/#/assets/contenthub`

* Logga in på [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&client_id=exc_app&scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&locale=en_GB&flow_type=token&dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&idp_flow_type=login&response_type=token&profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&code_challenge_method=plain&redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&use_ms_for_expiry=true#/) och klicka på **[!UICONTROL Experience Manager Assets Content Hub]** som finns i avsnittet **[!UICONTROL Quick access]**:
  ![Content Hub Access](assets/access-content-hub.png)

* Logga in på [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&client_id=exc_app&scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&locale=en_GB&flow_type=token&dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&idp_flow_type=login&response_type=token&profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&code_challenge_method=plain&redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&use_ms_for_expiry=true#/) och klicka på **[!UICONTROL Experience Manager Assets Content Hub]** som finns i produktväljaren:
  ![Content Hub Access-metod 3](assets/access-content-hub-alternate.png)

## Ge Content Hub feedback {#provide-content-hub-feedback}

Om du vill rekommendera produktrelaterade förbättringar klickar du på **[!UICONTROL Feedback]** bredvid ditt organisationsnamn högst upp i Content Hub användargränssnitt.

Ange ett ämne, en beskrivning av rekommendationen och bifoga filer om det behövs. Klicka på **[!UICONTROL Submit]** för att skicka feedback till Adobe.

![Content Hub feedback](assets/content-hub-feedback.png)

## Konfigurera Content Hub för ditt team {#setup-content-hub}

Så här konfigurerar du Content Hub för ditt team:

1. [Aktivera Content Hub för Experience Manager Assets med Cloud Manager](deploy-content-hub.md#enable-content-hub).

1. [Anlita Content Hub-administratör](deploy-content-hub.md#onboard-content-hub-administrator).

1. [Lägg till viktiga Content Hub-användare](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Godkända resurser i Experience Manager Assets som DAM-författare eller administratör](approve-assets.md).

1. [Konfigurera Content Hub-användargränssnitt för andra användare som administratör](configure-content-hub-ui-options.md).

1. [Bevilja Content Hub-åtkomst till fler användare från teamet](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Öppna Content Hub-portalen](#access-content-hub).

1. [Ge Content Hub feedback](#provide-content-hub-feedback).


## Läs mer om de viktigaste funktionerna {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Distribuera Content Hub" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong> Konfigurera Content Hub-användargränssnitt </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur administratörer kan konfigurera Content Hub användargränssnitt. </em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="Sök efter resurser som finns i Content Hub" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong> Söka efter resurser som är tillgängliga i Content Hub </strong>
      </a>
   </div>
   <p>
      <em>Lär dig använda olika funktioner för att begränsa sökresultaten.</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Redigera bilder med Adobe Express" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Redigera bilder med Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Lär dig skapa varianter av bilder i Content Hub med Adobe Express</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="Dela resurser som finns i Content Hub" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>Dela resurser som är tillgängliga i Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du delar en eller flera resurser som en länk och sedan kommer åt dem.</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="Hantera samlingar i Content Hub" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>Hantera samlingar i Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du skapar samlingar med resurser och sedan hanterar dem.</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Dela resurser som finns i Content Hub" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Visa resursinsikter i Content Hub</strong>
      </a>
   </div>
   <p>
      <em> Innehållsmodulen ger värdefulla insikter i resurser och åtgärdar en vanlig utmaning som marknadsföringsintressenter ofta stöter på</em>
   </p>
</td>
</table>
