---
title: Ansluta en databas till [!DNL AEM Forms] as a Cloud Service?
seo-title: AEM Forms Data Integration
description: Du kan hämta och spara data till en RESTful-webbtjänst, SOAP-baserade webbtjänster och OData-tjänster från [!DNL AEM Forms] as a Cloud Service. Tjänsten tillhandahåller ett dedikerat verktyg för att hämta, testa, validera och skicka data till olika typer av datakällor.
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Koppla datakällor till Cloud Service {#aem-forms-data-integration}

![Dataintegrering](do-not-localize/data-integeration.png)

Företagsinfrastrukturer omfattar olika datasystem eller datakällor som databaser, webbtjänster, REST-tjänster, OData-tjänster och CRM-lösningar. Tillsammans utgör de ett informationssystem som skickar data till affärssystemen för att utföra den dagliga verksamheten. Å andra sidan hämtar applikationerna in data och skickar tillbaka dem för att uppdatera datakällorna.

[!DNL AEM Forms] program som Adaptiv Forms och interaktiv kommunikation kräver integration med datakällor för att hämta in kunddata när formulär återges och interaktiv kommunikation skapas. Det finns situationer när data hämtas från datakällor baserat på användarindata i Adaptive Forms. Dessutom kan inskickade data i adaptiva formulär skrivas tillbaka för att uppdatera respektive datakälla.

Ett distribuerat modulärt system har sina fördelar, men utmaningen består i att integrera och skapa dataassociationer mellan datakällor. Dataintegrering är nyckeln till en fungerande och effektiv företagsinfrastruktur med olika datakällor kopplade till applikationer för utbyte av affärsdata.

## Översikt över dataintegrering {#data-integration-overview}

![aem-forms-data-integeration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] Med dataintegrering kan du konfigurera och ansluta olika datakällor med [!DNL AEM Forms]. Det ger ett intuitivt användargränssnitt för att skapa ett enhetligt datarepresentationsschema för affärsenheter och tjänster över anslutna datakällor. Den enhetliga representationen kallas för en formulärdatamodell, ett tillägg till JSON-schema. Enheterna i en formulärdatamodell kallas datamodellsobjekt. Med en formulärdatamodell kan du:

* Få åtkomst till datamodellsobjekt, egenskaper och tjänster från anslutna datakällor.
* Skapa anpassade datamodellsobjekt och egenskaper
* Bygg kopplingar mellan datamodellsobjekt inom och mellan datakällor.
* Anropa datamodellsobjekttjänster för att fråga efter eller skriva data till och från datakällor.

När du har skapat en formulärdatamodell kan du använda den i olika arbetsflöden för adaptiv form och interaktiv kommunikation, till exempel:

* Skapa adaptiv Forms och interaktiv kommunikation baserat på formulärdatamodell
* Förifyll adaptiva Forms och interaktiv kommunikation från konfigurerade datakällor
* Anropa datakälltjänster/åtgärder med hjälp av regler för anpassat formulär
* Skriv data för anpassat formulär till datakällor

## Kom igång med dataintegrering {#get-started-with-data-integration}

Det första steget för att implementera dataintegrering är att identifiera och konfigurera datakällor som lagrar information som du vill använda i Adaptiv Forms och interaktiva kommunikationssituationer. Därefter skapar du en formulärdatamodell som använder datamodellsobjekt, egenskaper och tjänster från en eller flera datakällor. Du kan skapa adaptiv Forms och interaktiv kommunikation baserat på en formulärdatamodell där fält eller platshållare för adaptiva formulär i interaktiv kommunikation är bundna till respektive egenskaper för datakälla.

[!DNL AEM Forms] I kan du också skapa en formulärdatamodell som är oberoende av datakällor och senare associera eller binda datamodellsobjekt och egenskaper i formulärdatamodellen med datakällan. Det eliminerar eventuella beroenden till datakällor när du arbetar med en formulärdatamodell.

Läs följande för att komma igång, förstå och implementera dataintegrering.

* [Konfigurera datakällor](configure-data-sources.md)
* [Skapa formulärdatamodell](create-form-data-models.md)
* [Arbeta med formulärdatamodell](work-with-form-data-model.md)
* [Använd formulärdatamodell](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] stöder inte relationsdatabaser.
