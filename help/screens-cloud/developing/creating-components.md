---
title: Skapa komponenter
description: AEM används för att lagra, formatera och återge innehåll som är tillgängligt på dina webbsidor. Följ den här sidan om du vill veta mer om redigeringskanaler och återgivningskomponenter.
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Skapa komponenter {#creating-components}

AEM används för att lagra, formatera och återge innehåll som är tillgängligt på dina webbsidor.

## Redigeringskanaler {#authoring-channels}

Kanalen är det centrala objektet för innehåll som levereras till en uppsättning skärmar. Därför öppnar en innehållsförfattare vanligtvis en kanal i redigeraren för att lägga till eller ändra innehåll. Eftersom kanalen är en ***cq:Page*** kommer att följa samma traditionella UX-mönster för att lägga till och ändra komponenter i kanalen.

Men eftersom komponenter i en kanal vanligtvis återges i helskärmsläge blir redigeringsupplevelsen lidande när du försöker redigera enskilda komponenter eller skapa nya order. Kanalen använder därför väljare för att återge olika vyer av komponenterna. Redigeringsmiljön använder redigeringsväljaren för att aktivera den anpassade kanalåtergivningen.

Till exempel, `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

Användaren behöver inte ta hand om att lägga till väljaren till URL-adressen när han/hon redigerar. En logik på klientsidan lyssnar på lagerväxlingshändelsen och lägger till väljaren om en kanal har den dedikerade resurstypen *skärmar/kärna/komponenter/kanal.*

## Återger komponenter {#rendering-components}

För att möjliggöra en korrekt redigering måste komponenterna tillhandahålla följande två återgivningar:

| **Komponent** | **Återgivningar** |
|---|---|
| *my-component/my-component.html* | produktionsrendering |
| *my-component/edit.html* | redigera återgivning i en mindre vy |

De inbyggda komponenterna utnyttjar följande klientbibliotekskategorier:

| **Komponent** | **Klientbibliotek** |
|---|---|
| *cq.screens.components.edit* | CSS och JS som måste läsas in vid redigering |
| *cq.screens.components.production* | CSS och JS som måste läsas in när kanalen körs |
| *cq.screens.components* | delad CSS och JS |

>[!NOTE]
>
>Om du vill utveckla anpassade komponenter använder du ***[AEM Screens exempelkomponentmall](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***.
