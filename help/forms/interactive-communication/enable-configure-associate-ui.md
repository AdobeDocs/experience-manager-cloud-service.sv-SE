---
title: Aktivera och konfigurera associerat gränssnitt för interaktiv kommunikation
description: Lär dig hur du aktiverar Associate View och konfigurerar arbetsflöde för uppdateringar i Interactive Communication Settings så att associerade kan använda det associerade användargränssnittet.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 7c3e8a2b-5f21-4a1e-9e2d-8a4b6c7d8e9f
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Aktivera och konfigurera associerat gränssnitt för interaktiv kommunikation

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

I den här artikeln beskrivs hur du aktiverar det associerade användargränssnittet för interaktiv kommunikation och konfigurerar ett AEM-arbetsflöde för inskickade data. Författare utför de här stegen i **Interaktiva kommunikationsinställningar**.

En översikt över det associerade användargränssnittet och användarroller finns i [Associera användargränssnitt i den interaktiva kommunikationsredigeraren](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md).

## Förutsättningar

Innan du aktiverar och konfigurerar det associerade användargränssnittet måste du kontrollera att du har:

- **Författare har åtkomst** till redigeraren för interaktiv kommunikation.
- En **interaktiv kommunikation** har skapats med den layout och de databindningar som krävs.
- **Associerade användare** har lagts till i gruppen **forms-associates** (krävs för att associerade ska kunna komma åt det associerade användargränssnittet).
- **Författare** har lagts till i gruppen **forms-associates** (krävs för att författare ska kunna komma åt det associerade användargränssnittet).

När du är redo att integrera Associate-gränssnittet med ditt program och anropa det på Publish-instansen måste du också ha en webbläsare med popup-stöd aktiverat och IC-kortet publicerat. Se [Integrera associerat gränssnitt i ditt program](/help/forms/interactive-communication/invoke-associate-ui.md) för fullständiga integreringskrav.

## Aktivera associerad vy (associerat användargränssnitt)

Aktivera det associerade användargränssnittet på dokumentnivå så att den interaktiva kommunikationen kan användas av associerade användare.

1. Öppna din interaktiva kommunikation i redigeraren.
1. Öppna **Interaktiva kommunikationsinställningar** (eller **Inställningar**) från det övre åtgärdsfältet eller dokumentalternativen.

   ![Interaktiva kommunikationsinställningar - Associera egenskaper med Aktivera redigering av associerad vy](/help/forms/assets/associate-ui-settings.png)

1. Kontrollera att **Associera egenskaper** är markerat i den vänstra panelen.
1. Markera **Aktivera redigering av associerad vy** till höger.
1. Klicka på **Använd ändringar** och spara sedan dokumentet.

   ![Interaktiva kommunikationsinställningar - Associera egenskaper med Aktivera redigering av associerad vy](/help/forms/assets/associate-ui-enable-view.png)

Ett meddelande kan påminna dig om att tillämpa ändringarna och spara dokumentet för att aktivera Associate View. När du har sparat blir grafikkortet tillgängligt för associationsstyrd användning.

### Tillåt redigering av associerat gränssnitt per komponent

När Associate View (Associera vy) har aktiverats för IC måste du aktivera **Tillåt redigering av associerat** för varje komponent som associerar ska kunna redigera. Komponenter utan den här inställningen aktiverad förblir skrivskyddade i det associerade användargränssnittet.

1. I IC-redigeraren markerar du komponenten (till exempel ett textfält) på arbetsytan eller i komponenthierarkin.
1. Expandera **Associera egenskaper** på den högra panelen **Egenskaper**.
1. Aktivera **Tillåt redigering av associerad** **på** för den komponenten.
1. Upprepa för alla komponenter som är kopplade till varandra och spara sedan dokumentet.

![Tillåt redigering efter associering i komponentegenskaper](/help/forms/assets/associate-ui-allow-editing-by-associate.png)

>[!NOTE]
>
> **Associate Properties** innehåller även alternativ som **Typografi** (teckensnitt, storlek och format för fältet i det associerade användargränssnittet), **Verktygstips** och **Mönster** (valideringar). Använd dessa om du vill styra hur komponenten ser ut och fungerar när någon redigerar den - du kan till exempel ange valideringsmönster så att associerade anger data i det format som krävs.

## Konfigurera arbetsflöde för associerat användargränssnitt

Om du vill köra ett AEM-arbetsflöde när användare skickar eller uppdaterar data från det associerade användargränssnittet konfigurerar du följande:

1. I **Inställningar för interaktiv kommunikation** väljer du **Arbetsflöde** i den vänstra panelen (under Associera egenskaper).
1. Aktivera **Konfigurera arbetsflöde för uppdatering** ****.
1. I **Välj arbetsflödesmodell** väljer du den arbetsflödesmodell för AEM som ska köras (till exempel `conversionWorkflow` eller en sökväg som `/var/workflow/models/submit-workflow-1`).
1. Du kan också ange **Meddelande om slutfört arbetsflöde** (visas för användaren när arbetsflödet har slutförts).
1. Du kan också ange **URL:en för omdirigering** om du vill skicka användaren till en viss sida efter överföringen.
1. Klicka på **Använd ändringar** och spara dokumentet.

   ![Interaktiva kommunikationsinställningar - arbetsflödeskonfiguration för associerat gränssnitt](/help/forms/assets/associate-ui-configure-workflow.png)

När du aktiverar ett arbetsflöde körs det när användare skickar från det associerade användargränssnittet. Information om hur insändning och arbetsflöde fungerar - var de körs, vilka instanser och viktiga överväganden som ska göras - finns i [Arbetsflöde för insändning för Associate-gränssnittet](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior). Artikeln innehåller även ett exempel på ett arbetsflöde som genererar PDF från IC-inskickat material.

## Slutför konfigurationen av det associerade användargränssnittet

När du har aktiverat Associate View och eventuellt konfigurerat arbetsflöde:

1. **Aktivera redigerbara fält:** Aktivera de fält som är associerade tillåts redigera i de obligatoriska avsnitten i IC-kortet. Ange valideringar och obligatoriskt/skrivskyddat beteende efter behov.
1. **Publicera IC** så att den är tillgänglig för associerade i publiceringsinstansen.
1. Dela den publicerade konc-länken med kollegor. De autentiserar (till exempel via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) och öppnar användargränssnittet för Associate, anger eller bekräftar kunddata och genererar den slutliga kommunikationen. Om du har konfigurerat ett arbetsflöde körs det när det skickas. Information om hur överföring och arbetsflöde fungerar finns i [Arbetsflöde för överföring för associerat användargränssnitt](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior).

## Se även

- [Associera gränssnittet i interaktiv kommunikationsredigerare](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Integrera associerat gränssnitt i ditt program](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Arbetsflöde för överföring för Associate UI - IC Generate PDF Output](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md) - hur överföring och arbetsflöde fungerar, plus ett exempelarbetsflöde som genererar PDF från IC-överföringar.
