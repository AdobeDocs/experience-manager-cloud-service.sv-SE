---
title: Förstå universell redigerare - responsivt läge
description: I den här artikeln beskrivs hur du förhandsgranskar formulär med olika emulatorer i den universella redigeraren för att se hur de ser ut och känns under utvecklingen.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 8f5b4d863ab469c44b4c221eab1fb128706b45c7
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# Responsivt läge i WYSIWYG Authoring

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> med ditt GitHub-organisationsnamn och databasnamn. Om databas-URL:en till exempel är https://github.com/adobe/abc är organisationsnamnet adobe och databasnamnet abc.</span>


Med [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) kan du förhandsgranska Edge Delivery Services Forms med olika emulatorer för att se hur formuläret ser ut och känns vid redigeringen.

Med det responsiva läget kan utvecklare utforma layouter som automatiskt anpassar sig till olika skärmstorlekar, inklusive stationära datorer, surfplattor och mobila enheter. Universal Editor stöder emulatorer för datorer, surfplattor och mobila enheter. Du kan ange höjd och bredd enligt skärmstorleken och utföra följande åtgärder:

* Ange orientering
* Ange bredd och höjd
* Ändra orientering

## Förhandsgranska Forms i responsivt läge för olika enheter

Den universella redigeraren har en **emulatorikon** som finns i skärmens övre högra hörn. Du kan förhandsgranska sidor i olika enhetsstorlekar och testa hur responsiv design fungerar för att få en bättre användarupplevelse.

Så här visar du hur Universal Editor återger formulär i olika skärmstorlekar:

1. Öppna formuläret i Universell redigerare för redigering.
1. Välj ikonen ![Emulator](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} som finns i verktygsfältet för den universella redigeraren och klicka på emulatorikonen för att visa alternativet.

   ![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. Välj ett alternativ för att emulera ett formulär i Universal Editor på en vald enhet: Skrivbord, Surfplatta, Mobil.

   ![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%,height=40%}

   Som standard öppnas redigeraren i en skrivbordslayout där höjden och bredden automatiskt bestäms av webbläsaren. Du kan också emulera ett formulär på en mobil eller surfplatta. Du kan också anpassa skärmbredden och -höjden för anpassade enheter.

Universal Editor har olika emulatorer för att förhandsgranska formulär på olika enheter. I tabellen nedan listas de tillgängliga emulatortyperna tillsammans med motsvarande enhetsbeteckning:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Typ av emulator</th>
        <th style="width: 80%">Enhetsbild</th>
    </tr>
    <tr>
        <td style="width: 20%">Skrivbord</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Desktop Emulator" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tablet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Tablettemulator" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Mobil</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Mobile Emulator" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Egen enhet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Emulator för anpassad enhet" style="width: auto; height: auto"></td>
    </tr>
</table>

Du kan använda ikonen **Skärmrotator** för att växla mellan stående och liggande orientering när du förhandsgranskar ett formulär på olika enheter. Det hjälper utvecklare att testa hur den responsiva designen anpassas till skärmrotationer på olika enheter.

Universal Editor stöder de olika formulärlayouterna. Om du vill utforska de olika layouterna kan du läsa avsnittet [Layoutfunktioner](#layout-capabilities).

## Layoutfunktioner

Med Universal Editor kan du skapa lättanvända formulär som ger användarna dynamiska upplevelser. Formulärlayouten styr hur objekt och komponenter visas i ett formulär.

Universal Editor har stöd för följande typer av layouter för formulär:
* [Panellayout](#panel-layout)
* [Guidelayout](#wizard-layout)
* [Dragspelslayout](#accordion-layout)

### Panellayout

Panelayout är användbart när du vill ordna relaterade fält på ett sätt som gör det enklare att navigera och hitta motsvarande innehåll. Panelayouten ordnar formkomponenterna inom distinkta avsnitt eller paneler i formulär.

![Panellayout](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

Du kan använda [panelkomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) för att lägga till panellayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar olika egenskaper för panelkomponenten finns i artikeln [panelkomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Guidelayout


Med hjälp av guidelayouten kan du förenkla ett komplext formulär genom att dela upp det i distinkta steg. Varje steg representerar en annan del av processen och användarna navigerar genom stegen sekventiellt, ofta med knapparna **Nästa** och **Bakåt** . Du kan använda guidelayouten för att skapa ett formulär som innehåller flera avsnitt eller steg.

![Guidelayout](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

Du kan använda [guidekomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) för att lägga till guidelayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för guidekomponenten finns i artikeln [wizard component](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Dragspelets layout

Dragspelslayouten visar innehåll i komprimerbara avsnitt eller paneler i ett adaptivt formulär. När ett avsnitt är expanderat visas innehållet i det, medan andra avsnitt förblir komprimerade. Den här layouten är idealisk för att visa stora mängder information i ett kompakt format.

![Dragspelslayout](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

Du kan använda [dragspelskomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) för att lägga till dragspelslayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för dragspelskomponenten finns i artikeln om [dragspelskomponenten](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### Hur väljer man rätt layout?

Det är viktigt att välja rätt layout för att optimera användarupplevelsen och formulärfunktionerna. Tabellen hjälper dig att förstå de olika layoutalternativen som finns och hjälper dig att välja den lämpligaste layouten baserat på dina specifika behov och användningsexempel:

| Funktion | Panellayout | Guidelayout | Dragspelets layout |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Syfte** | Grupperar relaterat innehåll i distinkta avsnitt | Hjälper användarna genom en flerstegsprocess eller ett formulär | Ordnar innehållet i komprimerbara avsnitt |
| **Struktur** | Distinkta avsnitt | Sekventiella steg/sidor | Komprimerbara paneler/avsnitt |
| **Navigering** | Klicka på panelrubrikerna för att navigera | - Framåt: Nästa-knappen <br>- Bakåt: Bakåt-knappen <br> - Valfria hoppsteg | Klicka på rubriker för att expandera/komprimera avsnitt |
| **Användarupplevelse** | Organiserar stora mängder innehåll på ett hanterbart sätt | Stegvisa anvisningar som minskar överväldigande | Komprimerad vy med expanderade/komprimerade avsnitt |
| **Använd skiftläge** | Komplexa formulär med kategoriserade avsnitt | Konfigurera processer, komplexa formulär | Vanliga frågor, inställningsmenyer, avsnitt med detaljerat innehåll |

## Se även

{{universal-editor-see-also}}
