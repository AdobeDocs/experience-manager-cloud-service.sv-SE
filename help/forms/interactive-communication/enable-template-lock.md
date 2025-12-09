---
title: Lås mall i interaktiv kommunikationsredigerare
description: Malllås i den interaktiva kommunikationsredigeraren gör det möjligt för mallskaparna att låsa layouten eller innehållet för dokumentförfattarna.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# Lås mall i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med funktionen Template Lock i Interactive Communication (IC) Editor kan mallförfattare begränsa ändringar av vissa element i en kommunikationsmall. Detta säkerställer en enhetlig design, skyddar viktigt innehåll och upprätthåller styrning mellan team som återanvänder mallar för att skapa personaliserad kommunikation.

När låsta komponenter används ser de ut som distinkta och kan inte ändras av författare eller medarbetare längre fram i kedjan, beroende på låstypen. Den här funktionen hjälper till att upprätthålla varumärkesstandarder, dataintegritet och enhetlig layout i all kommunikation.

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/template-lock.png)

## &#x200B;2. Lås typer

Mallförfattare kan använda innehålls- och layoutlås, individuellt eller tillsammans, för att styra innehålls- och layoutändringar i mallar för interaktiv kommunikation:

### 2.1 Content Lock

Ett innehållslås begränsar alla ändringar av det markerade elementets innehåll eller egenskaper. Den här typen av lås säkerställer att viktiga data, text och designegenskaper förblir oförändrade, även när de återanvänds i flera dokument.

När det används kan författare inte ändra:

- Textinnehåll eller bildtexter

- Utseendeinställningar (teckensnitt, färg, bakgrund, kanter osv.)

- Databindningskonfigurationer

- Komponentelement i en behållarkomponent (t.ex. delformulär)

### 2.2 Layout Lock

Ett Layout Lock begränsar ändringar som rör ett elements position och storlek. Detta säkerställer att den visuella justeringen och designhierarkin överensstämmer med varumärkets eller dokumentets standarder.

När det används kan författare inte:

- Flytta elementet till en ny position på sidan

- Ändra storlek på elementets bredd eller höjd

## &#x200B;3. Så här använder du malllås i den interaktiva kommunikationsredigeraren

Följ stegen nedan för att använda innehålls- eller layoutlås i mallen för interaktiv kommunikation:

1. Öppna din mall
Öppna eller skapa en mall, följ guiden [Skapa en interaktiv kommunikationsmall](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/overview/create-interactive-communication-template)

1. Välj komponenten
Klicka på den komponent (textruta, bild eller delformulär) som du vill begränsa.

1. Alternativ för Access Lock
Gå till avsnittet Låsning i panelen Egenskaper.

1. Använd lås

   1. Content Lock: Förhindrar text-, format- och dataredigeringar.

   1. Layoutlås: Begränsar förflyttning och storleksändring.

   1. Du kan aktivera båda för fullständigt skydd.

1. Spara och verifiera
Spara mallen och skapa en ny IC som baseras på den för att bekräfta att låsta element inte kan ändras.

## &#x200B;4. Bästa praxis

- **Lås viktiga komponenter tidigt:** Använd lås för sidhuvuden, sidfötter, friskrivningsklausuler och logotyper för att bevara regelefterlevnad och varumärkesidentitet.

- **Använd innehållslås för precision:** Skydda fält som är bundna till centrala datamodeller eller regeltext.

- **Använd layoutlås för konsekvens:** Förhindra felpassning eller visuell förvrängning i mallar som används ofta.

- **Kommunicera om låsanvändning:** Se till att nedströmsanvändare är medvetna om vilka avsnitt som är avsiktligt begränsade för att undvika förvirring.
