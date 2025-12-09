---
title: PDF Preview in Interactive Communication Editor with Different Data Options
description: PDF Preview in Interactive Communication Editor with Different Data Options to preview Interactive Communications in three different ways.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# PDF Preview in Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

Med funktionen PDF Preview kan man förhandsgranska interaktiv kommunikation på tre olika sätt: utan data, med lokala JSON-baserade data eller med exempeldata från den konfigurerade datamodellen.

## Viktiga fördelar

- Förhandsgranska interaktiv kommunikation med exempeldata för att visualisera hur livedata kommer att se ut när de sammanfogas med kommunikationen.

- Ladda upp lokala JSON-datafiler för att generera datadrivna förhandsgranskningar utan serverdelskonfiguration.

- Använd sammankopplade FDM-modeller (Form Data Models) för att simulera dataintegrering i realtid med exempeldata under utformningen.

- Växla enkelt mellan dataalternativ (inga data, lokala data, FDM) för att validera layout, struktur och personalisering.

## PDF Preview in Interactive Communication Editor with Different Data Options

Förgranska interaktiv kommunikation utan data, lokala data eller exempeldata från konfigurerad datamodell för flexibel testning och validering.

+++&#x200B;1. Förhandsgranska utan data.

1.1. Öppna din interaktiva kommunikation i IC Editor.

1.2. Använd alternativet PDF Preview och välj alternativet **Inga data** för att visa en kommunikation utan data.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/nodata.png)

+++

+++&#x200B;2. Förhandsgranska med lokala JSON-data

2.1. Förbered en strukturerad JSON-fil. Som referens kan du kopiera exempeldata från JSON-schemat [(FDM)](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model) som används för kommunikationen.

2.2. Gå till **PDF Preview** > Använda lokala data i IC Editor.

2.3. Markera och överför JSON-filen för att återge en PDF-förhandsvisning med angivna data.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/localdata.png)

+++

+++&#x200B;3. Förhandsgranska med datamodell 

3.1. Välj **Använda datamodell** om du vill använda exempeldata från en redan konfigurerad formulärdatamodell (FDM) för konc.

3.2. Förhandsgranskningen fyller i data automatiskt från modellfält. Se till att exempeldata sparas i FDM vid första användningen, annars kan förhandsvisningen visas som inga data.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/datamodel.png)

+++

