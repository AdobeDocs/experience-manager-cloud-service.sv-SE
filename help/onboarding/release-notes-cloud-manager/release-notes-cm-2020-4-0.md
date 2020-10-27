---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.4.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.4.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.4.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.4.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.4.0 är 9 april 2020.

## Nyheter {#whats-new-cloud-manager}

* Utgivar-URL:er är nu tillgängliga från miljösidan i användargränssnittet för Cloud Manager.
* Ändringar i navigeringen så att användaren kan redigera, byta eller lägga till ett program från översiktssidan i Cloud Manager.
* Ändringar som gör att användaren kan redigera program från programkortet på Cloud Managers startsida.
* Ny pipeline-status **Pipeline som körs** visas mot den miljö som den är associerad med.
* Förbättringar av förståelsen av sidan för att implementera pipeline. Detta inkluderar visning av Pipeline-namn (endast icke-produktionspipeline) och typ samt ett märke som anger om pipelinestatusen pågår/avbryts/misslyckades.
* Verktygstips som förbättrar användarupplevelsen och gör det lättare att förstå varför knappen Lägg till program/miljö är inaktiverad.
* Misslyckade miljöer kan nu tas bort via gränssnittet och API:t.
* Processen som används för att generera Git-lösenord har gjorts mer flexibel mot problem i det underliggande tjänstskiktet.

### Bug Fixes {#bug-fixes-cloud-manager}

* Länkarna till scenmiljön på informationssidan för pipeline-körning navigerade inte konsekvent till rätt plats.
* Enskilda steg i skapandet av miljön skulle timeout inträffa tidigare än nödvändigt och orsaka att processen misslyckas.
* Den Maven-konfiguration som används i byggbehållaren har uppdaterats för att undvika dödlägen när artefaktmetadata hämtas.
* I vissa fall kan steget Skapa bild inte hämta kundpaket.
* Vissa ovanliga förhållanden kan förhindra att miljöer tas bort.
* Meddelanden från Experience Cloud mottogs inte konsekvent.

