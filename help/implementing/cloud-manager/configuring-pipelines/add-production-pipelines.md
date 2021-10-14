---
title: Lägga till produktionsförlopp
description: Lägga till produktionsförlopp
index: false
source-git-commit: 16e3280d7eaf53d8f944a60ec93b21c6676f0133
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# Skapa en produktionspipeline {#create-production-pipeline}

När du har konfigurerat ditt program och har minst en miljö med användargränssnittet [!UICONTROL Cloud Manager] är du redo att konfigurera din distributionskanal.

Följ de här stegen för att konfigurera beteendet och inställningarna för din pipeline:

1. Klicka på **Konfigurera pipeline** för att konfigurera och konfigurera din pipeline.

   ![](assets/set-up-pipeline1.png)

1. Skärmen **Setup Pipeline** visas. Markera grenen och klicka på **Nästa**.

   ![](assets/setup-1.png)

1. Konfigurera distributionsalternativen.

   ![](assets/setup-pipeline.png)

   Du kan definiera utlösaren för att starta pipelinen:

   * **Manuell**  - använd gränssnittet för att starta pipelinen manuellt.
   * **På Git Changes**  - startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

   Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

   Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:

   * **Fråga varje gång**  - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Avbryt omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Godkänn omedelbart**  - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. Produktionens pipeline-inställningar innehåller en tredje flik med namnet **Experience Audit**. Det här alternativet innehåller en tabell för de URL-sökvägar som alltid ska inkluderas i Experience Audit.

   >[!NOTE]
   >Du måste klicka på **Lägg till ny sida** för att definiera en egen anpassad länk.

   ![](assets/setup-3.png)

   Klicka på **Lägg till ny sida** för att ange en URL-sökväg som ska inkluderas i Experience Audit.

   Om du till exempel vill inkludera `https://wknd.site/us/en/about-us.html` i Experience Audit (Upplevelsegranskning) anger du sökvägen `us/en/about-us.html` i det här fältet och klickar på **Save**.

   ![](assets/exp-audit4.png)

   Den URL som visas i tabellen är:

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   Högst 25 rader kan inkluderas. Om användaren inte har skickat in några sidor i det här avsnittet, kommer webbplatsens hemsida som standard att inkluderas i Experience Audit.

   Mer information finns i [Understanding Experience Audit Results](/help/implementing/cloud-manager/experience-audit-testing.md).

   >[!NOTE]
   > De konfigurerade sidorna skickas till tjänsten och utvärderas utifrån prestanda, tillgänglighet, SEO (Search Engine Optimization), bästa praxis och PWA (Progressive Web App)-tester.

1. Klicka på **Spara** på skärmen **Redigera pipeline**. Sidan **Översikt** visar nu **Distribuera ditt program**-kort. Klicka på **Distribuera** för att distribuera programmet.

   ![](assets/configure-pipeline5.png)

