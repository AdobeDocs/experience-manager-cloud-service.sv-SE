---
title: Inledning till omfångsobjekt i anpassade funktioner
description: Formuläret stöder omfångsobjekt i anpassade funktioner som skickas som ett sista argument till funktioner när regeln körs.
keywords: omfångsobjekt i anpassade funktioner, globala objekt, fältobjekt.
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: af211649a4f22d06f4e8669335a8267ee948a408
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Omfångsobjekt i anpassade funktioner

I Adaptiv Forms skickas ett scope-objekt som det sista argumentet till funktioner när en regel körs. Den kan användas för att läsa formuläregenskaper och ändra formuläret inifrån funktionerna. Omfångsobjektet innehåller ett skrivskyddat proxyobjekt för formuläret, den utlösta händelsen och målfältet. Formulär- och fältegenskaper kan nås med scopeobjektet genom att lägga till `$`, till exempel `scope.form.$id` och `scope.field.$id`.

## Formulärändringsfunktioner som använder omfångsobjekt

Omfångsobjektet har följande funktioner för formulärändring:

| Funktion | Syntax | Beskrivning | Kodexempel |
|-----------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Anger en egenskap för `$element` med `$payload`. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) för att visa exemplet. |
| **validate** | `validate([any $element])` | Kör validering på `$element`. Om inget element anges valideras hela formuläret. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) för att visa exemplet. |
| **reset** | `reset([any $element])` | Återställer `$element`. Om inget element anges återställs hela formuläret. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) för att visa exemplet. |
| **importData** | `importData(any $payload)` | Importerar data till formuläret och ersätter befintliga formulärdata. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) för att visa exemplet. |
| **exportData** | `exportData()` | Returnerar formulärets data. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) för att visa exemplet. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Utlöser en formuläröverföring. Parametern `$data` anger vad som ska skickas och `$submit_as` definierar innehållstypen (standardvärdet är multipart/form-data). Det valfria `$validate_form` avgör om formuläret ska valideras (standard: true). `submitSuccess` utlöses när åtgärden lyckades. Vid fel utlöses `submitError`. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) för att visa exemplet. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Ställer in fokus på `$element`, som kan vara en panel eller ett fält. Om inget element anges, fokuseras fältet som utlöste regeln. Den valfria parametern `$focusOption` (av uppräkningstypen `FocusOption`) anger om fokus ska ligga på nextItem eller previousItem i förhållande till `$element`. Om en panel anges är navigeringen begränsad till den panelen, och med ett fält sker navigeringen i den överordnade panelen. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) för att visa exemplet. |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Skickar en händelse av typen `$eventName` för elementet som anges av `$element`. Om inget element anges skickas händelsen i formuläret. Det valfria `$payload` är tillgängligt för uttryck som hanterar händelsen. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) för att visa exemplet. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Markerar fältet som identifieras av `$fieldIdentifier` som ogiltigt och anger valideringsmeddelandet till `$validationMessage`. Den valfria parametern `$option` anger om `$fieldIdentifier` tolkas som `id`, `name` eller `dataRef`. Standardvärdet är `{useId: true}` och de värden som stöds är `{useId: true}`, `{useDataRef: true}` och `{useQualifiedName: true}`. | [Klicka här](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) för att visa exemplet. |

## Se även

{{see-also-rule-editor}}