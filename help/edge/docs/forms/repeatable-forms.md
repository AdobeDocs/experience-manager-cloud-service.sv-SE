---
title: Lägga till repeterbara avsnitt i ett formulär
description: Lägga till repeterbara avsnitt i ett EDS-formulär
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Lägga till repeterbara avsnitt i ett formulär

Med adaptiva Forms-block kan du lägga till eller göra ett avsnitt eller en komponent i ett formulär upprepningsbart. På så sätt kan användare ange information flera gånger för samma typ av data, vilket gör det enklare att samla in information som arbetserfarenhet eller utbildningsbakgrund.

Ta till exempel ett formulär som används för att samla in information om en persons arbetsupplevelse. Du kan ha ett upprepningsbart avsnitt där du kan hämta information om varje föregående jobb. Det repeterbara avsnittet innehåller vanligtvis fält som företagsnamn, befattning, anställningsdatum och ansvarsområden. Användaren kan lägga till flera instanser av det repeterbara avsnittet för att ange information om varje jobb som han/hon har utfört.

I slutet av den här artikeln lär du dig att:

- [Skapa ett upprepningsbart avsnitt i ett formulär](#add-repeatable-sections-to-a-form)
- [Ange minsta eller högsta antal upprepningar i ett formulär](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## Skapa ett upprepningsbart avsnitt

Genom att skapa ett upprepningsbart avsnitt i ett formulär kan användarna ange flera instanser av samma datauppsättning, vilket gör det möjligt att effektivt samla in upprepad information. Så här skapar du ett upprepningsbart avsnitt i ett formulär:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.

1. Lägg till ett formulärfält med egenskapen `type` inställd på `fieldset`
1. Ange `Name` för fältet. Egenskapen name används för att skapa ett upprepningsbart avsnitt.
1. Aktivera repeterbarhet genom att ange `repeatable` till `true`.
1. Ange en beskrivande `label` för fältet. Det fungerar som rubrik för det repeterbara avsnittet.

   Se bilden nedan för en illustration av en anställningshistorik i ett ansökningsformulär.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. För varje fält som du vill ta med i avsnittet anger du egenskapen `Fieldset` till samma namn som du valde i steg 3.

   Ange till exempel `experience` i fältegenskapen för alla relevanta fält som ska inkluderas i avsnittet `employment history`.

   ![exempel på ett upprepningsbart avsnittsfält och dess egenskaper](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera bladet. Det repeterbara avsnittet läggs till i formuläret.

   Under det repeterbara avsnittet hittar användarna en intuitiv **Lägg till**-knapp som gör det enkelt att lägga till flera avsnitt.

   ![upprepningsbart avsnitt, knappen Lägg till, om du vill lägga till flera avsnitt &#x200B;](/help/edge/assets/repeatable-section-example.png)


## Ange minsta och högsta antal upprepningar

I formulärdesignen är det bra att ange minsta och högsta repetitioner för repeterbara avsnitt. På så sätt får ni kontroll och enhetlighet samtidigt som ni vägleder användarna effektivt. Så här anger du minsta eller högsta antal upprepningar:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.

1. För ett fält med egenskapen `type` `fieldset` och `repeatable` inställda på `true`:

   - Ange egenskapen `min` för att ange det minsta antal gånger som avsnittet kan upprepas.

   - Ange egenskapen `max` för att ange maximalt antal gånger som avsnittet kan upprepas.

   ![Ange min- och max-egenskapen för att ange hur många gånger avsnittet kan upprepas](/help/edge/assets/repeatable-section-set-min-max.png)

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera bladet.

   När du lägger till ett upprepningsbart avsnitt hittar användarna en intuitiv **Ta bort** -ikon, vilket gör det enklare att ta bort upprepningsbara avsnitt. När du har lagt till de här avsnitten kan de inte minskas till färre instanser än vad som anges av egenskapen `min`. Detta garanterar att minimikraven för ifyllande av formuläret uppfylls.


