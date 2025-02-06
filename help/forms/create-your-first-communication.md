---
title: Skapa din första interaktiva kommunikation
description: Designa dynamisk, datadriven kommunikation enkelt med AEM Forms Interactive Communications
feature: Release Information
role: Admin
hide: true
hidefromtoc: true
exl-id: c58ea216-7de0-40e1-9493-9ceb472e5ef8
source-git-commit: a32e30ba71b2b9a4361080bd75deb0d9e61fdfa3
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Skapa din första interaktiva kommunikation


>[!VIDEO](https://video.tv.adobe.com/v/3444094/)

## Steg 1: Planera interaktiv kommunikation

Det första steget i planeringen av interaktiv kommunikation är att färdigställa innehållet i den interaktiva kommunikationen. När innehållet är klart måste du analysera det för att identifiera de olika resurstyper som krävs för att skapa den interaktiva kommunikationen.

### Planeringsöverväganden

En interaktiv kommunikation innehåller följande element:

* **Statisk text** innehåller de flesta delar av den interaktiva kommunikationen som är generiska till sin natur och ingår i kommunikationen med alla kunder. Exempel: sidhuvud, sidfot, hälsning eller friskrivning.

* **Data som har hämtats från ett serverdelssystem (formulärdatamodell)** är kundspecifika och sammanfogas dynamiskt med den interaktiva kommunikationen. Policynumret eller adressen kan till exempel hämtas med hjälp av en formulärdatamodell.

* **Layout eller mallar** för Print- och Web-versionen av Interactive Communication.

* **Ordning** där de olika textstyckena visas i den interaktiva kommunikationen.

* **Villkorliga data** fylls i baserat på fördefinierade villkor. Till exempel datumet då den interaktiva kommunikationen genereras.

* **Bilder som lagras i en databas**, till exempel logotyper och signaturbilder. Bilder som företagslogotyper visas i de flesta eller alla interaktiva kommunikationer.

* **Diagram och tabeller** krävs för att förenkla representationen av komplexa data i en interaktiv kommunikation

### Anatomi i interaktiv kommunikation

När du är klar med innehållet och de element som används för att skapa den interaktiva kommunikationen kan du skapa en beskrivning av den interaktiva kommunikationen. Anatomin måste innehålla de uppgifter som anges i avsnittet Planeringsöverväganden. Till exempel en anatomi för den månadsräkning som en telekomoperatör skickar till sina kunder.

Anatomin innehåller data med följande indatalägen:

* Statisk text
* Formulärdatamodell
* Villkorliga data
* Bilder


## Steg 2: Skapa formulärdatamodell

Med en formulärdatamodell kan du koppla en interaktiv kommunikation till olika datakällor. Till exempel AEM användarprofil, RESTful-webbtjänster, SOAP webbtjänster, OData-tjänster och relationsdatabaser. En formulärdatamodell är ett enhetligt datarepresentationsschema för affärsenheter och tjänster som är tillgängliga i anslutna datakällor. Du kan använda formulärdatamodellen med en interaktiv kommunikation för att hämta data från anslutna datakällor. Mer information om formulärdatamodell finns i [AEM Forms-dataintegrering](/help/forms/data-integration.md).

## Steg 3: Skapa fragment

Dokumentfragment är återanvändbara komponenter i en korrespondens som används för att skapa en interaktiv kommunikation. Dokumentfragmenten är av följande typer: Text, List och Condition.


## Steg 4: Skapa mallar

Interactive Communications editor ger flera mallar OOTB. Du kan ändra de här mallarna efter organisationens behov eller skapa en helt ny mall.


## Steg 5: Skapa en interaktiv kommunikation

När du har skapat alla byggstenar, t.ex. formulärdatamodell, dokumentfragment och mallar för webbversionen, kan du börja skapa en interaktiv kommunikation. Så här skapar du en interaktiv kommunikation:

1. Logga in i din AEM Forms as a Cloud Service-miljö.
1. Gå till Forms > Forms &amp; Documents
1. Klicka på **Skapa** och välj **Kommunikationsdokument**. Du får en konfigurationsskärm där du kan ställa in följande alternativ:

   | Fält | Beskrivning | Obligatoriskt |
   |-------|-------------|----------|
   | Namn | Unik identifierare för kommunikationen | Ja |
   | Titel | Visningsnamn för kommunikationen | Ja |
   | Beskrivning | Kort beskrivning av syftet med meddelandet | Nej |
   | Mall | Välj en förkonfigurerad mall eller börja från början | Ja |
   | Taggar | Lägg till metadatataggar för bättre sortering | Nej |

1. Gå till fliken Förinställningar och konfigurera följande alternativ:

   | Fält | Beskrivning |
   |-------|-------------|
   | Förinställningslista | Välj en förkonfigurerad förinställning för dokumentets storlek. Vanliga alternativ är A4, Letter med mera. |
   | Förinställd bredd | Visar den förinställda bredden för den valda förinställningslistan. |
   | Förinställd höjd | Visar förinställningshöjden för den valda förinställningslistan. |
   | Förinställningsenhet | Välj måttenhet för dokumentets mått (t.ex. Millimeter, Tum). |
   | Förinställd orientering | Välj orientering för dokumentet - antingen stående eller liggande. |

1. Klicka på **Skapa**. Kommunikationen öppnas i redigeraren.
1. Dra och släpp komponenter och fragment för att utforma den interaktiva kommunikationen.

   * Använd **mallsidan** för innehåll som är gemensamt på flera sidor. Mallsidor är avsedda att formatera sidor, och de underlättar designens enhetlighet eftersom de kan ge bakgrunds- och layoutformat för mer än en sida i en dokumentdesign.

   * Använd **Sidor** för att skapa layout för ditt dokument. Varje sida hämtar sin storlek och orientering från en mallsida, och som standard kopplas varje sida till den standardmallsida som skapas i Designer.


1. Använd `@`-notation för att fylla i datafält automatiskt baserat på den anslutna datamodellen.
1. Använd alternativet `PDF Preview` om du vill förhandsgranska dokumentet tillsammans med data. Du behöver datafilen i JSON-format.
