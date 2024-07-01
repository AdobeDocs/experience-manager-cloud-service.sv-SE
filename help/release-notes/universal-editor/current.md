---
title: Versionsinformation om Universal Editor 2024.06.28
description: Detta är versionsinformationen för version 2024.06.28 av Universal Editor.
feature: Release Information
role: Admin
source-git-commit: cc94ad2ba42707bb7541217f0225b995f64ad84f
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2024.06.28 {#release-notes}

Detta är versionsinformationen för den 28 juni 2024-versionen av Universal Editor.

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Nyheter {#what-is-new}

* **Startsida**: De senaste sidorna visas som en lista, utan förhandsvisningsbilder.
* **Platsfält**: Förbättrad URL-validering lades till, HTTPS-URL:er och stöd för hash-värden i URL:er lades till för att ta hänsyn till hash-dirigerade program.
* **Tangentbordsnavigering**: Markeringen av sidövertäckning kopplades från egenskapsfältets fokus för att förbättra tangentbordsnavigeringen på sidan utan att förlora fokus.
* **Objektetiketter**: reservvärdet för etiketter använder nu `data-aue-prop` i stället för `data-aue-type` för tydligare identifiering i övertäckningar och i innehållsträdet.
* **RTE-modul**: A **Avbryt** knappen lades till i den modala textredigeraren när den öppnades från egenskapspanelen.
* **UE Service on Node**: HTTP-stöd för Universal Editor-tjänsten återinfördes eftersom alla HTTPS-anslutningar avslutas på Dispatcher-nivå.
* **Intern kopia-API**: Ett API till Universal Editor-tjänsten för kopiering av komponenter har lagts till, vilket möjliggör framtida introduktioner av verktygsfältsalternativ för kopiering och kopiering av innehåll.

## Felkorrigeringar {#bug-fixes}

* **Panelen Egenskaper - vägbeskrivningar**: Breadcrumb-menyn på egenskapspanelen för djupt kapslade objekt som inte var öppna har korrigerats.
* **Väljare för innehållsfragment**: Väljaren för innehållsfragment har förbättrats för att säkerställa att den följer reglerna som definieras i modellen för innehållsfragment eller i `data-aue-filter`.
* **Komponentinfogning**: Listan för infogning av nya komponenter som inte uppdaterades korrekt efter navigering till en annan sida korrigerades.
* **Publiceringsstatus**: Hanteringen av publiceringsstatus har förbättrats så att den fungerar mer konsekvent.
* **Övriga korrigeringar**: Den här versionen innehåller även olika mindre korrigeringar, rensning av teknisk skuld, säkerhetsförbättringar och konsoliderade tester för övergripande stabilitet och prestanda.
