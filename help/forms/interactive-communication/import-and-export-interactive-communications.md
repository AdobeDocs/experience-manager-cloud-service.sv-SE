---
title: Importera och exportera interaktiv kommunikation
description: Med import och export av interaktiv kommunikation kan användarna smidigt migrera, återanvända och hantera kommunikation mellan olika miljöer.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---


# Importera och exportera interaktiv kommunikation

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

Med import- och exportfunktionen i Interactive Communication (IC) kan man smidigt migrera, återanvända och hantera kommunikation i olika miljöer. Med den kan du exportera en interaktiv kommunikation (IC) tillsammans med tillhörande fragment och datamodeller från en miljö och importera den till en annan, vilket ger enhetlighet och minskar dubbelarbetet under driftsättningen.

## Viktiga fördelar

- Förenklar migrering av IC:er mellan miljöer.
- Bevarar fragment, datamodeller och samband.
- Minskar arbetet med att återskapa konc i olika projekt.

## Importera och exportera interaktiv kommunikation

Skapa en interaktiv kommunikation (IC) i en miljö och återanvänd den i en annan miljö genom att exportera och importera den enligt följande steg:

+++&#x200B;1. Exportera interaktiv kommunikation

1.1. Välj en [skapad interaktiv kommunikation](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication) (IC).
1.2. Klicka på alternativet **Hämta** om du vill exportera den som en ZIP-fil.
1.3. Den hämtade ZIP-filen innehåller IC-kortet tillsammans med dess valda **mall**, **fragment** och **datamodell**.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++&#x200B;2. Importera interaktiv kommunikation

2.1. Gå till målmiljön.
2.2. Navigera till **Forms > Forms och dokument > Skapa > Filöverföring**.
2.3. Överför ZIP-filen till **importera** till IC-kortet.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/uploadfile.png)

2.4. Efter överföring visas IC-kortet tillsammans med tillhörande fragment och datamodell.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++&#x200B;3. Importera och exportera fragment

3.1. Om du vill exportera markerar du det önskade fragmentet i **Forms > Forms och dokument** och klickar sedan på **Hämta** för att exportera det som en ZIP-fil.

3.2. Om du vill importera går du till målmiljön, navigerar till Forms > Forms och dokument > Skapa > **Filöverföring** och överför den exporterade ZIP-filen.

Detta gör det enkelt att återanvända fragment i olika miljöer, vilket ger en konsekvent design och minskar dubbelarbetet.
+++
