---
title: Förstå universell redigerare - responsivt läge
description: I den här artikeln beskrivs hur du förhandsgranskar formulär med olika emulatorer i den universella redigeraren för att se hur de ser ut och känns under utvecklingen.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
source-git-commit: 1abc1092872d4a3e0253ddf0388d23e39a6c2de9
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Responsivt läge i WYSIWYG Authoring

Med [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) kan du förhandsgranska Edge Delivery Services Forms med olika emulatorer för att se hur formuläret ser ut och känns vid redigeringen.

Med det responsiva läget kan utvecklare utforma layouter som automatiskt anpassar sig till olika skärmstorlekar, inklusive stationära datorer, surfplattor och mobila enheter. Universal Editor stöder emulatorer för datorer, surfplattor och mobila enheter. Du kan ange höjd och bredd enligt skärmstorleken och utföra följande åtgärder:
* Ange orientering
* Ange bredd och höjd
* Ändra orientering

## Förhandsgranska Forms i responsivt läge för olika enheter

Den universella redigeraren har en **emulatorikon** som finns i skärmens övre högra hörn. Du kan förhandsgranska sidor i olika enhetsstorlekar och testa hur responsiv design fungerar för att få en bättre användarupplevelse.

Så här visar du hur Universal Editor återger formulär i olika skärmstorlekar:

1. Öppna formuläret i Universell redigerare för redigering.
2. Välj ikonen ![Emulator](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} som finns i verktygsfältet för den universella redigeraren och klicka på emulatorikonen för att visa alternativet.

   ![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

3. Välj alternativet att emulera en mobil enhet i Universell redigerare

   ![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%,height=40%}

   Som standard öppnas redigeraren i en skrivbordslayout där höjden och bredden automatiskt bestäms av webbläsaren. Du kan också emulera ett formulär på en mobil eller surfplatta. Du kan också anpassa skärmbredden och -höjden för anpassade enheter.

Universal Editor har olika emulatorer för att förhandsgranska formulär på olika enheter. I tabellen nedan listas de tillgängliga emulatortyperna tillsammans med motsvarande enhetsbeteckning:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th>Typ av emulator</th>
        <th>Enhetsbild</th>
    </tr>
    <tr>
        <td>Skrivbord</td>
        <td><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Desktop Emulator" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td>Tablet</td>
        <td><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Tablettemulator" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td>Mobil</td>
        <td><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Mobile Emulator" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td>Egen enhet</td>
        <td><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Emulator för anpassad enhet" style="width: auto; height: auto"></td>
    </tr>
</table>

Du kan använda ikonen **Skärmrotator** för att växla mellan stående och liggande orientering när du förhandsgranskar ett formulär på olika enheter. Det hjälper utvecklare att testa hur den responsiva designen anpassas till skärmrotationer på olika enheter.

## Se även

* [Kom igång med Edge Delivery Services för AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Skapa ett formulär med Google eller Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Konfigurera dina Google-blad eller Microsoft Excel-filer så att du kan börja ta emot &#x200B;](/help/edge/docs/forms/submit-forms.md)
* [Publicera formuläret och börja samla in data](/help/edge/docs/forms/publish-forms.md)
* [Anpassa utseendet på &#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [Lägga till repeterbara avsnitt i ett &#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [Visa ett anpassat tackmeddelande efter att formuläret har skickats &#x200B;](/help/edge/docs/forms/thank-you-page-form.md)
* [Komponenter för adaptiva formulärblock och deras egenskaper](/help/edge/docs/forms/form-components.md)
* [Övervakning av faktisk användning](https://www.aem.live/developer/rum#authentication)


