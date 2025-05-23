---
title: Hur ansluter jag en databas till  [!DNL AEM Forms] as a Cloud Service?
description: Hämta och spara data till RESTful-webbtjänster, SOAP webbtjänster och OData-tjänster från ett adaptivt formulär eller ett AEM arbetsflöde.
feature: Adaptive Forms, Form Data Model
role: Admin, User
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 5ee37f59bb959e0549c0541c6568aa8c135c330e
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Ansluta AEM Forms till en databas {#aem-forms-data-integration}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/data-integration.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |



![Dataintegrering](do-not-localize/data-integeration.png)

Företagsinfrastrukturer omfattar olika datasystem eller datakällor som databaser, webbtjänster, REST-tjänster, OData-tjänster och CRM-lösningar. Tillsammans utgör de ett informationssystem som skickar data till affärssystemen för att utföra den dagliga verksamheten. Å andra sidan hämtar applikationerna in data och skickar tillbaka dem för att uppdatera datakällorna.

När du ansluter adaptivt formulär till en databas krävs integration med datakällor för att hämta kunddata när du återger formulär. Det finns situationer när data hämtas från datakällor baserat på användarindata i Adaptive Forms. När du skickar ett adaptivt formulär till en databas kan du dessutom skriva tillbaka inskickade adaptiva formulärdata för att uppdatera de olika datakällorna.

Ett distribuerat modulärt system har sina fördelar, men utmaningen består i att integrera och skapa dataassociationer mellan datakällor. Dataintegrering är nyckeln till en fungerande och effektiv företagsinfrastruktur med olika datakällor kopplade till applikationer för utbyte av affärsdata.

## Översikt över dataintegrering {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] Med dataintegrering kan du konfigurera och ansluta olika datakällor med [!DNL AEM Forms]. Det ger ett intuitivt användargränssnitt för att skapa ett enhetligt datarepresentationsschema för affärsenheter och tjänster över anslutna datakällor. Den enhetliga representationen kallas för en formulärdatamodell (FDM), ett tillägg till JSON-schemat. Enheterna i en formulärdatamodell kallas datamodellsobjekt. Med en formulärdatamodell (FDM) kan du

* Få åtkomst till datamodellsobjekt, egenskaper och tjänster från anslutna datakällor.
* Skapa anpassade datamodellsobjekt och egenskaper
* Bygg kopplingar mellan datamodellsobjekt inom och mellan datakällor.
* Anropa datamodellsobjekttjänster för att fråga efter eller skriva data till och från datakällor.

När du har skapat en formulärdatamodell (FDM) kan du använda den för att:

* Skapa adaptiv Forms baserat på en formulärdatamodell (FDM)
* Förifyll anpassad Forms från konfigurerade datakällor
* Anropa datakälltjänster/åtgärder med hjälp av regler för anpassat formulär
* Skriv data för anpassat formulär till datakällor

## Kom igång med dataintegrering {#get-started-with-data-integration}

Det första steget för att implementera dataintegrering för att skicka adaptiva formulär till en databas är att identifiera och konfigurera datakällor som lagrar information som du vill använda i adaptiva Forms. Därefter skapar du en FDM (Form Data Model) som använder datamodellsobjekt, egenskaper och tjänster från en eller flera datakällor. Du kan skapa adaptiv Forms baserat på en formulärdatamodell (FDM) där fält för adaptiva formulär är bundna till respektive datakällegenskaper.

Med [!DNL AEM Forms] kan du även skapa en formulärdatamodell (FDM) som är oberoende av datakällor och associera eller binda datamodellsobjekt och egenskaper i formulärdatamodellen (FDM) med datakällan senare. Det eliminerar eventuella beroenden till datakällor när du arbetar med en formulärdatamodell (FDM).

Läs följande för att komma igång, förstå och implementera dataintegrering:

* [Konfigurera datakällor](configure-data-sources.md)
* [Skapa formulärdatamodell (FDM)](create-form-data-models.md)
* [Arbeta med formulärdatamodell (FDM)](work-with-form-data-model.md)
* [Använd formulärdatamodell (FDM)](using-form-data-model.md)

<!--

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] does not support relational database.

-->