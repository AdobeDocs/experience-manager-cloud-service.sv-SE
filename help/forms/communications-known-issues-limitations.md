---
title: 'Kända fel '
description: Kommunicera bästa praxis, kända problem och begränsningar
source-git-commit: 06da7d2a5063e163aa1534bedbc79ae50ef27515
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---


# Vanliga frågor och svar, god praxis, kända problem och begränsningar {#best-practices-known-issues-and-limitations}

Innan du börjar använda API:er för kommunikation, vanliga frågor och svar, bör du granska följande kända problem och begränsningar:

## Kända fel

- Du kan bara använda en viss renderingstyp (PDF, PRINT) en gång i listan med utskriftsalternativ. Du kan t.ex. inte ha två PRINT-alternativ där var och en anger en PCL-återgivningstyp.

- För en gruppkonfiguration är det bara en instans av en kombination av värden av OutputType (PDF, PRINT) och RenderType(PostScript, PCL, IPL, ZPL, osv.) är tillåtet.

## Bästa praxis

- Adobe rekommenderar att du använder blobbbehållarlagring för datafiler i molnregionen som används av AEM Cloud Service.

## Vanliga frågor {#faq}

**Kan jag använda en bevakad mapp eller andra lagringsmekanismer för att lagra indata och utdata?**

För tillfället kan du använda Microsoft Azure Storage för att spara indata och genererade dokument. Microsoft Azure-lagring ger olika alternativ för att [automatisera dataförflyttningar](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Ingår ett Microsoft Azure Storage-konto i Experience Manager Forms Cloud Service-licensen?**

Microsoft Azure Storage-kontot är oberoende av Experience Manager Forms Cloud Service-licensen.

**Lagrar kommunikations-API:er data på Experience Manager Forms Cloud Service-servrar?**

Indata och utdata sparas endast på Microsoft Azure Storage.

**Finns bara API:er för kommunikation för Experience Manager Forms Cloud Service? Kan jag få liknande funktionalitet i en lokal miljö?**

Du kan använda AEM Forms Output-tjänsten för att kombinera en mall (XFA eller PDF) med kunddata för att generera dokument i PDF, PS-, PCL- och ZPL-format.

Jämfört med en lokal miljö ger Cloud Servicen ytterligare fördelar med automatisk skalning och kostnadseffektivitet.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**Kan jag köra flera gruppåtgärder samtidigt?**
Ja, du kan köra flera batchåtgärder samtidigt. Använd alltid olika käll- och målmappar för varje åtgärd för att undvika konflikter.
