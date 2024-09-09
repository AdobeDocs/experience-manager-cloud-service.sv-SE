---
title: Översätta och lokalisera en Edge Delivery Services för AEM Forms
description: Översätta och lokalisera en Edge Delivery Services för AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# Översätta och lokalisera en Edge Delivery Services för AEM Forms

I Edge Delivery Services innebär formuläröversättning att man konverterar formulärinnehåll från ett språk till ett annat med fokus på precision, tydlighet och enhetlighet. Översatta eller lokaliserade formulär ger en bredare publik över olika geografiska platser, vilket förbättrar användarupplevelsen och underlättar bättre kommunikation mellan olika språk.


I slutet av artikeln lär du dig att:

* [Översätt formulär i Google Drive](#translate-form-google-drive)
* [Översätta formulär på SharePoint webbplats](#translate-form-sharepoint)

## Översätt formulär i Google Drive {#translate-form-google-drive}

Funktionen `GOOGLETRANSLATE` på Google-blad översätter formulär genom att trycka på det inbyggda översättningsverktyget, vilket ändrar text från ett språk till ett annat direkt i ett Google-blad. Så här översätter du formulär i Google Drive:

1. Gå till AEM projektmapp på Google Drive och öppna Google-bladet.
2. Byt namn på det befintliga bladet (`shared-default`) till `shared-en`.
3. Lägg till ett blad med namnet `shared-default`. Bladet `shared-default` innehåller innehåll för lokalisering till ett specifikt språk.
4. Lägg till det lokaliserade innehållet i bladet `shared-default` med funktionen `GOOGLETRANSLATE`.
Du kan använda en formel för att översätta innehållet i cell D2 från bladet `shared-en` till franska i bladet `shared-default`. Här är formeln som ska användas:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Fråga om översätt kalkylblad](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Du kan hänvisa till [kalkylbladet](/help/forms/assets/enquirytranslate.xlsx) som innehåller formulärdefinitionen för ett `enquiry`-formulär översatt från engelska till franska.

![Fråga om översatt formulär](/help/forms/assets/translate-form-french.png)

Se URL:en nedan, där du kan visa formuläret med dess franska språköversättning:
https://main—portal—wkndforms.hlx.live/enquirytranslate

## Översätta formulär på SharePoint webbplats{#translate-form-sharepoint}

Om du vill översätta formulären på Microsoft® SharePoint webbplats måste du ändra fältetiketterna manuellt med hjälp av en översättningstjänst. Så här översätter du formulären på SharePoint Site:

1. Gå till AEM projektmapp i Microsoft® SharePoint och öppna kalkylbladet.
2. Byt namn på det befintliga bladet (`shared-default`) till `shared-en`.
3. Lägg till ett blad med namnet `shared-default`. Bladet `shared-default` innehåller innehåll för lokalisering till ett specifikt språk.
4. Lägg till det lokaliserade innehållet i bladet `shared-default` manuellt.

   ![Fråga om översätt kalkylblad](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Se [kalkylbladet](/help/forms/assets/enquirytranslate-sp.xlsx) som innehåller formulärdefinitionen för ett `enquiry`-formulär översatt från engelska till franska.

![Fråga om översatt formulär](/help/forms/assets/translate-form-french.png)

Se URL:en nedan, där du kan visa formuläret med dess franska språköversättning:
https://main—weFinance—wkndforms.hlx.live/enquirytranslate

## Kända fel {#known-issues}

* Etiketterna för formuläret översätts till det angivna lokaliserade språket i bladet `shared-default`, men felmeddelandena visas på webbläsarens standardspråk.

  ![Felmeddelande](/help/forms/assets/translate-error-message.png)

* När du öppnar kalendern visas kalenderns listruta på webbläsarens standardspråk.

  ![Felmeddelande](/help/forms/assets/translate-calender-display.png)


## Frågor och svar {#faq}

**Q**: Hur skriver jag indata på det angivna lokaliserade språket i ett formulär?

**A**: Justera tangentbordsinställningarna på enheten om du vill skriva in text på ett specifikt lokaliserat språk. På följande länkar finns instruktioner om hur du gör det:

* [Konfigurera din Mac för inmatning på ett annat språk](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [Konfigurera Windows för inmatning på ett annat språk](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [Konfigurera din Android eller iPhone/iPad så att du kan mata in på ett annat språk](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**Q**: Hur hämtar jag en lista över språk som används i funktionen `GOOGLETRANSLATE`?

**A**: I den [officiella dokumentationen för Google](https://cloud.google.com/translate/docs/languages) finns en omfattande lista med språkområden som används i GOOGLETRANSLATE.

## Se även

{{see-more-forms-eds}}

