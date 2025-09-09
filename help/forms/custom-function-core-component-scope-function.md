---
title: Inledning till omfångsobjekt i anpassade funktioner
description: Formuläret stöder omfångsobjekt i anpassade funktioner som skickas som ett sista argument till funktioner när regeln körs.
keywords: omfångsobjekt i anpassade funktioner, globala objekt, fältobjekt.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 248c75a5-6335-41d2-aa0a-28a20a710f88
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Omfångsobjekt i anpassade funktioner

I Adaptiv Forms skickas ett scope-objekt som det sista argumentet till funktioner när en regel körs. Den kan användas för att läsa formuläregenskaper och ändra formuläret inifrån funktionerna. Omfångsobjektet innehåller ett skrivskyddat proxyobjekt för formuläret, den utlösta händelsen och målfältet. Formulär- och fältegenskaper kan nås med scopeobjektet genom att lägga till `$`, till exempel `scope.form.$id` och `scope.field.$id`.

## Formulärändringsfunktioner som använder omfångsobjekt

Omfångsobjektet har följande funktioner för formulärändring:

| Funktion | Syntax | Beskrivning | Kodexempel |
|-----------------|--------|-------------|-------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Anger en egenskap i målfältet med `$payload`. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) för att visa exemplet. |
| **validate** | `validate([any $element])` | Kör validering i målfältet. Kör validering i hela formuläret om inget mål anges och returnerar en array med valideringsfel. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) för att visa exemplet. |
| **reset** *(utgått)* | `reset([any $element])` | Föråldrat. Använd `dispatchEvent($target, 'reset')` i stället. Återställer målfältet eller, om inget mål anges, återställer hela formuläret. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) för att visa exemplet. |
| **importData** | `importData(any $payload)` | Importerar data till formuläret och ersätter befintliga formulärdata. Om `qualifiedName` anges importeras data endast till det behållarfältet. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) för att visa exemplet. |
| **exportData** | `exportData()` | Returnerar formulärets data. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) för att visa exemplet. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Utlöser en formuläröverföring. Du kan ange vad som ska skickas via parametern `$payload` och ange innehållstypen via parametern `$contentType`. Data skickas som `multipart/form-data` som standard. Den valfria parametern `$validateForm` anger om formuläret ska valideras innan det skickas (standard: true). `submitSuccess` utlöses när åtgärden lyckades. Vid fel utlöses `submitError`. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) för att visa exemplet. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Ställer in fokus på målfältet, som kan vara en panel eller ett formulärfält. Om inget mål anges ställs fokus in på fältet som utlöste regeln. Den valfria parametern `$focusOption` anger om nästa eller föregående objekt i förhållande till målet ska fokuseras. Värden som stöds: `'nextItem'`, `'previousItem'`. Om den används med en panel är navigeringen begränsad till den panelen. Om det används med ett fält sker navigeringen i den överordnade panelen för det fältet. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) för att visa exemplet. |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Skickar en händelse av typen `$eventName` för elementet som bestäms av `$target`. Om inget mål anges skickas händelsen i formuläret. Det valfria `$payload` är tillgängligt för uttryck som hanterar händelsen. Den valfria parametern `$dispatch` styr beteendet för händelsespridning. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) för att visa exemplet. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Markerar fältet som identifieras av `$fieldIdentifier` som ogiltigt och visar `$validationMessage`. Den valfria parametern `$option` anger om `$fieldIdentifier` tolkas som `id`, `dataRef` eller `qualifiedName`. Standardvärdet är `{useId: true}`. Värden som stöds: `{useId: true}`, `{useDataRef: true}`, `{useQualifiedName: true}`. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) för att visa exemplet. |

## Se även

{{see-also-rule-editor}}

