---
title: Översätt och lokalisera ett AEM Forms Edge Delivery ServicesForm
description: Översätt och lokalisera ett AEM Forms Edge Delivery ServicesForm
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Översätt och lokalisera ett AEM Forms Edge Delivery ServicesForm

I Edge Delivery Services innebär formuläröversättning att man konverterar formulärinnehåll från ett språk till ett annat med fokus på precision, tydlighet och enhetlighet. Översatta eller lokaliserade formulär ger en bredare publik över olika geografiska platser, vilket förbättrar användarupplevelsen och underlättar bättre kommunikation mellan olika språk.


I slutet av artikeln lär du dig att:

* [Översätt formulär i Google Drive](#translate-form-google-drive)
* [Översätta formulär på SharePoint webbplats](#translate-form-sharepoint)

## Översätt formulär i Google Drive {#translate-form-google-drive}

The `GOOGLETRANSLATE` på Google sheets översätts blanketterna genom att man går in i det inbyggda översättningsverktyget och byter text från ett språk till ett annat direkt i ett Google-blad. Så här översätter du formulär i Google Drive:

1. Gå till AEM projektmapp på Google Drive och öppna Google-bladet.
2. Byt namn på det befintliga bladet (`shared-default`) till `shared-en`.
3. Lägg till ett blad med namnet `shared-default`. The `shared-default` bladet innehåller innehållet för lokalisering till ett visst språk.
4. Lägg till det lokaliserade innehållet i `shared-default` bladet med `GOOGLETRANSLATE` funktion.
Du kan använda en formel för att översätta innehållet i cell D2 från `shared-en` till franska inom `shared-default` blad. Här är formeln som ska användas:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Fråga om översätt kalkylblad](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Du kan se [kalkylblad](/help/forms/assets/enquirytranslate.xlsx) som innehåller formulärdefinitionen för en `enquiry` från engelska till franska.

![Fråga om översatt formulär](/help/forms/assets/translate-form-french.png)

Se URL:en nedan, där du kan visa formuläret med dess franska språköversättning: https://main—portal—wkndforms.hlx.live/enquirytranslate

## Översätta formulär på SharePoint webbplats{#translate-form-sharepoint}

Om du vill översätta formulären på Microsoft® SharePoint webbplats måste du ändra fältetiketterna manuellt med hjälp av en översättningstjänst. Så här översätter du formulären på SharePoint Site:

1. Gå till AEM projektmapp i Microsoft® SharePoint och öppna kalkylbladet.
2. Byt namn på det befintliga bladet (`shared-default`) till `shared-en`.
3. Lägg till ett blad med namnet `shared-default`. The `shared-default` bladet innehåller innehållet för lokalisering till ett visst språk.
4. Lägg till det lokaliserade innehållet i `shared-default` bladet manuellt.

   ![Fråga om översätt kalkylblad](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Se [kalkylblad](/help/forms/assets/enquirytranslate-sp.xlsx) som innehåller formulärdefinitionen för en `enquiry` från engelska till franska.

![Fråga om översatt formulär](/help/forms/assets/translate-form-french.png)

Se URL:en nedan, där du kan visa formuläret med dess franska språköversättning: https://main—weFinance—wkndforms.hlx.live/enquirytranslate

## Kända fel {#known-issues}

* Etiketterna i formuläret översätts till det angivna lokaliserade språket i `shared-default` -bladet, men felmeddelandena visas på standardspråket i webbläsaren.

  ![Felmeddelande](/help/forms/assets/translate-error-message.png)

* När du öppnar kalendern visas kalenderns listruta på webbläsarens standardspråk.

  ![Felmeddelande](/help/forms/assets/translate-calender-display.png)


## Frågor och svar {#faq}

**Q**: Hur skriver jag indata på det angivna lokaliserade språket i ett formulär?

**A**: Justera tangentbordsinställningarna på enheten om du vill skriva in text på ett specifikt språk. På följande länkar finns instruktioner om hur du gör det:

* [Konfigurera din Mac så att du kan göra inmatningar på ett annat språk](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [Konfigurera Windows för inmatning på ett annat språk](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [Konfigurera din Android eller iPhone/iPad så att du kan skriva på ett annat språk](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**Q**: Hur hämtar jag en lista över de språk som används i `GOOGLETRANSLATE` funktion?

**A**: Du kan använda [officiell dokumentation om Google](https://cloud.google.com/translate/docs/languages) för en omfattande lista över de språkområden som används i GOOGLETRANSLATE.

## Se även

{{see-more-forms-eds}}

