---
title: Personalisering och målgruppsanpassning av innehåll
description: Lär dig hur du kan skapa personaliserat, målinriktat innehåll med AEM
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 566cd449c536de4179e32c94df90b46d61e0103a
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---


# Personalisering och målgruppsanpassning av innehåll {#personalization-and-content-targeting}

Personalisering av webbinnehåll som ni ger kunderna innebär att skräddarsy upplevelserna efter deras intressen och behov. Du kan göra detta baserat på den information du har om dem; till exempel köpsammanfattning, ålder, kön, geografi, bland annat.

Med Adobe Experience Manager as a Cloud Service (AEM) kan du skapa ett urval av innehåll och sedan ange vilka målgrupper (grupper av slutanvändare) som ska se varje enskild upplevelse. Det innebär att ni inriktar era personaliserade upplevelser på specifika målgrupper.

När läsaren är online granskar målmotorn informationen om slutanvändaren och jämför den med upplevelsedefinitionerna. Motorn *&quot;bestämmer&quot;* vilka personaliserade upplevelser som ska visas.

AEM tillhandahåller ett ramverk av verktyg för:

* Skapa riktat innehåll som passar en rad olika målgrupper och som är beroende av tillgänglig kundinformation.
* Definiera reglerna som används för att matcha den kända användarinformationen mot en målgruppsdefinition.
* Konfigurera era sidor för att presentera målinriktade personaliserade upplevelser, för att återge det specifika innehåll som gäller för den aktuella slutanvändaren.

I följande översikt visas några termer som används för personalisering i AEM as a Cloud Service, följt av en rekommenderad åtgärdsordning.

## Upplevelse {#experience}

En upplevelse är innehåll som du vill ska visas för slutanvändarna.

## Personlig upplevelse {#personalized-experience}

En personaliserad upplevelse är en upplevelse som visas för en begränsad publik. Publiken definieras av dig, och innehållet visas bara när informationen som är känd om den aktuella slutanvändaren motsvarar den målgruppsdefinitionen.

När du skapar sidor definierar du flera upplevelser, där varje upplevelse blir en (eller flera) målgrupp(er). Om ingen målgrupp är löst visas standardupplevelsen.

### Erbjudande {#offer}

Ett erbjudande är en personaliserad upplevelse som ofta är tillgänglig under en begränsad tidsperiod.

En sida från en exempelwebbplats kan t.ex. använda erbjudanden som en teaserbild som visas högst upp på sidan. En person över 30 och en person under 30 kommer att se olika erbjudanden som upplevelseteraren.

## Målgrupp {#audience}

En målgrupp är en grupp slutanvändare som ni vill inrikta er på med personaliserat innehåll. När en besökare öppnar en webbsida avgör sidlogiken vilken målgrupp de tillhör baserat på känd information. Baserat på den bedömningen AEM det innehåll som du har skapat för den målgruppen.

Målgrupperna bygger på marknadsföringssegment. De skapas antingen i AEM eller Adobe Target. kan du skapa Adobe Target-målgrupper direkt i AEM med hjälp av publikkonsolen.

### Segment {#segment}

I AEM ContextHub definieras en målgrupp som ett segment baserat på regler (villkor). Dessa löses sedan för att återge det önskade innehållet.

## Aktivitet {#activity}

En aktivitet:

* definierar mappningen av en viss målgrupp (ett visst segment) med en viss upplevelse
* definierar den tidsperiod för vilken målinriktningen tillämpas
* identifierar [målmotor](#targeting-engine) som dina sidor använder

Aktiviteten kan antingen vara en personaliseringsaktivitet eller en A/B-testaktivitet (för arbetsflödet AEM och Adobe Target personalisering).

En aktivitet kan till exempel definiera upplevelser för två olika målgrupper: Personer över 30 år och personer under 30 år. En sida på webbplatsen kan sedan visa olika produkter för varje målgrupp.

Eller, som ett annat exempel, kan din produktkatalog innehålla lärare som fokuserar på säsongsprodukter. Sommarsportsaktiviteten kan alltså definiera målgrupperna som lärarna målar under sommarmånaderna.

Använd [Aktivitetskonsol](/help/sites-cloud/authoring/personalization/activities.md) för att skapa och hantera aktiviteter för [Varumärken](#brand). Du kan också skapa aktiviteter medan du redigerar [riktat innehåll](/help/sites-cloud/authoring/personalization/targeted-content.md) med [Målläge](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### Varumärke {#brand}

Ett varumärke har ett urval av marknadsföringsaktiviteter och marknadsföringsområden.

När du skapar ett varumärke med hjälp av aktivitetskonsolen visas det också i offertkonsolen.

### Yta {#area}

Ett område är en underindelning av ett varumärke.

## Målläge {#targeting-mode}

Vid redigering är det här redigeringsläget som används för att aktivera och konfigurera komponenter för personalisering.

Du kan [Skapa riktat innehåll](/help/sites-cloud/authoring/personalization/targeted-content.md) med målinriktningsläget för AEM. Målinriktningsläget och Target-komponenten tillhandahåller verktyg för att skapa innehåll för upplevelserna av era marknadsföringsaktiviteter.

## Experience Fragment {#experience-fragments}

En grupperad uppsättning komponenter som utgör en upplevelse.

[Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) är gjorda av innehåll och information (format, etc.) för att skapa en upplevelse, kan användas direkt vid redigering av sidor. De kan ses som en delmängd av en AEM. De gör det möjligt för innehållsförfattare att återanvända innehåll i olika kanaler, inklusive webbplatser och tredjepartssystem.

För ett personaliseringsexempel kan du kombinera en titel, bild, beskrivning och knappen Anropa till åtgärd för att skapa en suddig upplevelse. Att använda Experience Fragments är en viktig del i att använda Adobe Target personalisering.

## Målmotor {#targeting-engine}

Målmotorn är den mekanism som löser logiken för målinnehåll. [Verksamhet](/help/sites-cloud/authoring/personalization/activities.md) är konfigurerade att använda en av två målmotorer som är tillgängliga: AEM och Adobe Target.

Målmotorn är den plattform eller mekanism som avgör vilket personaliseringssystem som ska användas.

För närvarande kan AEM använda:

* [AEM ContextHub](#aem-contexthub) (AEM)
* den [Adobe Target](#adobe-target) personaliseringsmotor

>[!CAUTION]
>
>En enda AEM kan inte använda båda motorerna samtidigt.
>
>Du kan använda båda motorerna på separata sidor på samma plats.

### AEM ContextHub {#aem-contexthub}

AEM har den inbyggda målgruppsmotorn [ContextHub](/help/implementing/developing/personalization/contexthub.md) som bearbetar sidförfrågningar och avgör vilket innehåll som ska visas. När ni använder den AEM målgruppsmotorn begränsas ni till att använda segment som skapas i AEM för att definiera målgrupperna för era upplevelser.

### Adobe Target {#adobe-target}

The [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) med målmotorn spåras information som samlats in från sidbesök i Adobe Target.

* När ni använder den här målgruppsmotorn använder ni de segment ni importerar från Adobe Target för att definiera målgrupperna för era upplevelser.
* Aktiviteter som använder Adobe Target-motorn är [synkroniserat med mål](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Du kan använda den här motorn när du har [integrerat med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

## Konfigurera ditt personaliserade innehåll {#how-to-setup-personalized-content}

Det finns olika steg och definitioner som krävs för att leverera ditt personaliserade innehåll:

1. Konfigurera målmotorn genom att antingen:

   1. Konfigurerar [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. Integrera med [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)

1. Konfigurera målgrupperna.

   1. Ange [Målgrupper](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) eller [ContextHub-segment](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md), tillsammans med reglerna.

1. Skapa [Varumärke och verksamhet](/help/sites-cloud/authoring/personalization/activities.md).

1. Skapa det urval av upplevelser som du vill visa för olika målgrupper.

1. personalisera upplevelserna med [mål](/help/sites-cloud/authoring/personalization/targeted-content.md) dem till specifika målgrupper (segment).