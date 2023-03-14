---
title: AEM as a Cloud Service on Unified Shell
description: AEM as a Cloud Service on Unified Shell
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: 24ae6187813de801813236f0bbcb2ea51e8fe5e1
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 2%

---

# AEM as a Cloud Service on Unified Shell {#aem-as-a-cloud-service-on-unified-shell}

## Översikt {#overview}

AEM as a Cloud Service (Author Service) är integrerat med Unified Shell för att förbättra användarupplevelsen och kombinera den med alla andra Experience Cloud-program. Effekten av den här integreringen visas i programmets övre huvud enligt nedan.

![bild](/help/overview/assets/unifiedshell_header.png)

Fördelarna med detta är:

* Enkel inloggning i alla Experience Cloud-program
* Smidig växling mellan företag eller övergång till ett annat program
* Bättre produkthjälp
* Knapp för enkel feedback i produkten för att rapportera problem eller utbyta idéer med Adobe
* Tillgång till globala produktmeddelanden och meddelanden utöver meddelanden som är specifika för AEM as a Cloud Service

## Inaktiverar enhetligt gränssnitt {#disabling-unified-shell}

AEM as a Cloud Service har ett enhetligt skal aktiverat. Om den övre rubriken har anpassats rekommenderar vi att du inaktiverar det enhetliga gränssnittet för att undvika eventuella problem med anpassningarna. Följ stegen nedan för att inaktivera det enhetliga gränssnittet:

>[!NOTE]
>Enhetligt gränssnitt kan endast inaktiveras av ett konto med administratörsbehörighet.

1. Gå till **Verktyg - Cloud Services**.

   En administratörsanvändare ser det enhetliga gränssnittskonfigurationskortet som visas nedan:

   ![bild](/help/overview/assets/unifiedshell2.png)

1. Klicka på **Enhetlig gränssnittskonfiguration**. Avmarkera sedan kryssrutan nedan för att inaktivera Unified Shell:

   ![bild](/help/overview/assets/unifiedshell3.png)

## Ändra till mörkt tema {#changing-to-dark-theme}

Om du vill ändra till det mörka temat klickar du på din profilikon. Då visas ett popup-fönster enligt nedan. Du kan använda växlingsknappen för att växla till ett mörkt tema för det enhetliga skalet.

>[!INFO]
>
>Det mörka temat gäller endast för Unified Shell (det övre fältet).

![bild](/help/overview/assets/unifiedshell4.png)

## Identifiera AEM as a Cloud Service miljö {#identify-aemaacs-environment}

AEM as a Cloud Service innehåller tre typer av miljöer: Produktion, scen och utveckling. Se [Miljötyper](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en) för mer information. I och med den här integreringen med Unified Shell visas den typ av miljö som användaren är inloggad på tjänsten Författare i det övre huvudet via en etikett som visas nedan.

![bild](/help/overview/assets/unifiedshell_header_label.png)

## Åtkomst till AEM Inkorg {#accessing-the-aem-inbox}

Du kommer åt AEM Inkorg genom att klicka på klockikonen i det enhetliga skalet.

>[!INFO]
>
> Numret som visas på klockikonen innehåller olästa meddelanden för alla lösningar i den IMS-organisationen och uppgifter som visas i AEM Inkorg.

![bild](/help/overview/assets/unifiedshell5.png)

Klicka på knappen Inkorg i popup-fönstret för att gå till AEM Inkorg:

![bild](/help/overview/assets/unifiedshell6.png)
