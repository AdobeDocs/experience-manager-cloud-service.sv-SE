---
title: Skapa en interaktiv kommunikation
description: Skapa personaliserad, datadriven kommunikation. Utforska viktiga funktioner, introduktionssteg och verkliga användningsexempel med guider och självstudiekurser.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: c23145c9-078d-4b03-a8f4-2d835cdd1592
source-git-commit: f587a30da747ae3d53848ef5bb30c32a9b5d78e1
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# Skapa en interaktiv kommunikation

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

Med interaktiv kommunikation kan ni skapa, hantera och leverera personaliserad och interaktiv kommunikation, inklusive kundtjänst, fakturering, onboarding-dokument, anställningserbjudanden, kontouppdateringar med mera. Det är utformat för att stödja alla situationer där dynamiskt, användarspecifikt innehåll förbättrar kommunikationsupplevelsen i olika branscher.

Tänk dig att du måste skicka ett kontoutdrag, en försäkring eller en faktura till tusentals kunder. Alla har samma layout men personaliserade data. Interaktiv kommunikation gör detta möjligt på ett effektivt sätt.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/introduction.png)

Manuell framtagning av dessa dokument kan vara tidskrävande och leder ofta till inkonsekvenser, särskilt när personalisering och dataintegrering krävs. Med Interactive Communication Editor kan man effektivisera arbetet med att skapa interaktiv kommunikation.

## Förutsättning

* [Kontrollera att författaren är medlem i gruppen för användare av formulär](/help/forms/setup-forms-cloud-service.md#configure-users)

## Skapa en interaktiv kommunikation

Välj mellan olika scenarier för att skapa en interaktiv kommunikation, baserat på den nivå av återanvändning och dataintegrering som krävs:

+++ Skapa en tom interaktiv kommunikation

Om du skapar en tom interaktiv kommunikation kan du börja från grunden, perfekt när du vill ha full kontroll över layout, struktur och logik.
Steg som ska följas:

1. Öppna din **Adobe Experience Manager (AEM) Forms as a Cloud Service-instans**.
1. Navigera till **Forms > Forms &amp; Documents**.
1. Klicka på **Skapa > Interaktiv kommunikation**.

   ![Sök efter IC Docu](/help/forms/interactive-communication/assets/comm.png)

1. Lämna fältet **Mall** tomt på skärmen som visas.

   ![Sök efter IC Docu](/help/forms/interactive-communication/assets/create-ic-document.png)

1. Fyll i annan information som titel, namn, författare osv.
1. Klicka på **Skapa** för att öppna gränssnittet för den interaktiva kommunikationsredigeraren och börja designa.
1. Den öppnar konc.int. redigeraren där du kan börja utforma din kommunikation.
+++

+++ Skapa en mallbaserad interaktiv kommunikation

Om du använder en mall kan du snabba upp designarbetet genom att återanvända konsekventa layoutelement som sidhuvuden, sidfötter, logotyper och standardformatering.
Mallarna säkerställer varumärkets enhetlighet och sparar tid för de vanligaste kommunikationstyperna. Utför följande steg:

1. Öppna instansen AEM Forms as a Cloud Service.
1. Gå till **Forms > Forms &amp; Documents** och klicka på **Skapa > Interaktiv kommunikation**.
1. I det formulär som skapas **väljer du** en aktiverad mall från väljaren.
1. Fyll i annan information som titel, namn, författare osv.
1. Klicka på **Skapa** för att utforma kommunikationen med den valda mallstrukturen.
1. Den öppnar konc.int. redigeraren där du kan börja utforma din kommunikation.
+++

+++ Skapa en interaktiv datakommunikation

Datainteraktiv kommunikation anpassar automatiskt innehållet med backend-data.
Idealiskt för kontoutdrag, fakturor eller meddelanden där strukturen förblir konstant, men informationen varierar beroende på mottagare. Steg som ska följas:

1. Öppna instansen AEM Forms as a Cloud Service.
1. Gå till **Forms > Forms &amp; Documents** och klicka på **Skapa > Interaktiv kommunikation**.
1. I fältet **Formulärdatamodell** länkar du fördefinierade **FDM (Form Data Model)**.
1. Fyll i annan information som titel, namn, författare osv.
1. Använd **datamodell** i redigeraren för att binda fält till dynamiska data (t.ex. kundens namn, saldo, kontonummer).
1. Använd **innehållsområden, delformulär** och **fragment** för att strukturera och upprepa data där det behövs.
1. Förhandsgranska med **PDF Preview** och slutför kommunikationen för leverans.
1. Den öppnar konc.int. redigeraren där du kan börja utforma din kommunikation.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/ic-ui.png)
+++

Börja bygga interaktiv kommunikation för att effektivisera arbetsflödena och leverera slagkraftiga, användarspecifika upplevelser.

## Nästa steg

[Skapa en interaktiv kommunikationsmall](/help/forms/interactive-communication/create-interactive-communication-template.md)
[&#x200B; Skapa ett interaktivt kommunikationsfragment &#x200B;](/help/forms/interactive-communication/create-interactive-communication-fragment.md)
