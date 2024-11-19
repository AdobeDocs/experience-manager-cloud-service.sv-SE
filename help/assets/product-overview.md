---
title: Content Hub - översikt
description: Läs mer om Content Hub, dess viktigaste fördelar, hur man får tillgång till det och hur man kan ge feedback kring de alternativ som finns i Content Hub.
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Content Hub - översikt {#overview-content-hub}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |----|-----|

![Content Hub - översikt](assets/content-hub-overview.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub ingår som en del av Experience Manager Assets as a Cloud Service för att demokratisera tillgången till varumärkesinnehåll för organisationer och deras affärspartners. Fokus ligger på att distribuera resurser för aktivering i stor skala och att skapa innehållsvarianter för varumärke, vilket ger förbättrad marknadsföringsflexibilitet.

## Varför Content Hub?

Content Hub har följande fördelar:

**Hitta och dela alla varumärkesgodkända resurser som finns i en intuitiv portal**

AEM Assets fungerar som en enda källa till sanning och alla godkända mediefiler finns automatiskt tillgängliga på Content Hub i en hierarki för att förbättra sökupplevelsen.

**Konfigurerbart användargränssnitt**

De vanligaste egenskaperna i Content Hub, t.ex. sökfilter, fält som är tillgängliga när du lägger till eller importerar resurser, resursegenskaper, banderollinnehåll för varumärkning kan konfigureras och en administratör kan enkelt konfigurera Content Hub användargränssnitt baserat på deras behov.

**Ge icke-kreatörer möjlighet att redigera och mixa om innehåll samtidigt som de behåller sitt varumärke**

Med Content Hub kan du skapa nytt innehåll med Adobe Express (om du har Adobe Express). Du kan redigera befintligt innehåll med lättanvända verktyg, producera varumärkesanpassade varianter med mallar och märkeselement och skapa nytt innehåll med de senaste GenAI-funktionerna från Adobe Firefly.

**Få insikter om hur innehåll används i olika team**

[!DNL Content Hub] ger värdefulla insikter om resurser, och åtgärdar en vanlig utmaning som marknadsföringsintressenter ofta stöter på - statistik om resursanvändning som används i marknadsföringskampanjer, kanaler och olika regioner. Genom att få en tydlig förståelse för resursernas prestanda och popularitet kan ni få användbara insikter som är viktiga för att förbättra användarupplevelsen.

## Förutsättningar {#prerequisites-content-hub}

Content Hub kräver en produktionsredigeringsmiljö i Experience Manager as a Cloud Service, version 2024.6 eller senare (lägsta version är 2024.6.16799).

## Hur kommer jag åt Content Hub? {#access-content-hub}

[När du har konfigurerat Content Hub](/help/assets/deploy-content-hub.md) och lagt till en användare i [Content Hub produktprofil](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) kan du få åtkomst till Content Hub på följande sätt:

* Öppna Content Hub via följande länk:

  `https://experience.adobe.com/#/assets/contenthub`

* Logga in på experience.adobe com och klicka på **[!UICONTROL Experience Manager Assets Content Hub]** som finns i avsnittet **[!UICONTROL Quick access]**:
  ![Content Hub Access](assets/access-content-hub.png)

* Logga in på experience.adobe com och klicka på **[!UICONTROL Experience Manager Assets Content Hub]** i produktväljaren:
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

1. [DAM-författare eller -administratörer som ska godkänna resurser med Experience Manager-resurser](approve-assets.md).

1. [Administratörer kan konfigurera Content Hub-användargränssnittet för andra användare](configure-content-hub-ui-options.md).

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
      <strong> Redigera bilder med Adobe Express </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du skapar varianter av bilder i Content Hub med Adobe Express</em>
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
