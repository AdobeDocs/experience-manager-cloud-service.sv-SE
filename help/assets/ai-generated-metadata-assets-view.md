---
title: Förbättra innehållsidentifiering med AI-genererade metadata
description: Lär dig förbättra innehållsidentifiering med AI-genererade metadata
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Förbättra innehållsidentifiering med AI-genererade metadata {#ai-smart-tags}

I stället för att förlita sig på manuell inmatning tilldelar AI automatiskt beskrivande taggar till digitala resurser. Dessa AI-genererade taggar förbättrar metadatakvaliteten och gör materialet enklare att söka, kategorisera och rekommendera. Detta tillvägagångssätt förbättrar inte bara effektiviteten genom att eliminera manuell taggning, utan garanterar också enhetlighet och skalbarhet för stora volymer digitalt innehåll. Om resursen till exempel är en bild kan AI identifiera objekt, scener, känslor eller till och med varumärkeslogotyper i den och generera relevanta taggar som&quot;solnedgång&quot;,&quot;strand&quot;,&quot;semester&quot; eller&quot;leende&quot;. AI-genererat innehåll kan förbättra sökningen efter resurser genom att använda både semantiska och lexikala söktekniker. Se mer [Sök i Assets](search-assets-view.md). <!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![AI-genererade metadata](/help/assets/assets/enhanced-smart-tags.png)

## Hur aktiverar jag AI-genererade metadata? {#enable-ai-generated-metadata}

Så här aktiverar du AI-genererade metadata:

* Den lägsta version av AEM som krävs är `20626`.


## Använda AI-genererade metadata {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

Utför följande steg om du vill använda den förbättrade funktionen för smarta taggar:

1. Gå till önskad mapp i gränssnittet [!DNL Experience Manager] och klicka på **[!UICONTROL Add Assets]**. <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.--> De kompatibla bildfilformaten är `png`, `jpg`, `jpeg`,`psd`, `tiff`, `gif`, `webp`, `crw`, `cr2`, `3fr`, `nef`, `arw` och `bmp`.

1. Vänta tills den nyligen överförda resursen bearbetas. Gå till resursinformationen när du är klar.

1. Gå till fliken **[!UICONTROL AI-Generated]**. Om versionen [!DNL Experience Manager] är inkompatibel eller inte uppdaterad visas inte den här fliken.  Följande fält finns där:

   * **[!UICONTROL Generated title]:** Titeln innehåller en tydlig och kortfattad rubrik som beskriver kärnidén för en överförd resurs, vilket gör det enkelt att förstå direkt. När du lägger till en resurs visas den i resursvyn om du anger en titel (i `dc:title`). Om inget anges tilldelas en AI-genererad titel automatiskt.
   * **[!UICONTROL Generated description]:** Beskrivningen ger en kort men informativ sammanfattning av vad resursen handlar om, vilket hjälper användare och sökmoduler att snabbt förstå dess relevans.
   * **[!UICONTROL Generated keywords]:** Nyckelorden är måltermer som representerar huvudteman för en resurs, vilket underlättar taggning och innehållsfiltrering.

1. [Valfritt] Du kan lägga till ytterligare taggar eller skapa egna om du tror att relevanta taggar saknas. Det gör du genom att skriva dina taggar i fältet **[!UICONTROL Generated keywords]** och klicka på **[!UICONTROL Save]**.

Mer information om hur du inaktiverar AI-genererade metadata finns i [Inaktivera AI-genererade metadata](/help/assets/smart-tags.md#disable-ai-generated-metadata).
