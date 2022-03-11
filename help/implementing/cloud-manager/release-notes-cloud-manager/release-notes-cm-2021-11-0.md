---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.11.0
description: Det här är versionsinformationen för Cloud Manager i AEM as a Cloud Service release 2021.11.0
feature: Release Information
exl-id: 98fd6d8a-ddc2-4f53-9dfc-d8e21af0c14d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.11.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.11.0.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager i AEM as a Cloud Service 2021.11.0 är 4 november 2021.
Nästa version är planerad till den 16 december 2021.

## Nyheter {#what-is-new}

* Användare kan nu utnyttja nya frontledningslinjer för att exklusivt distribuera frontendkod snabbare. Se [Front End Pipelines för Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) om du vill veta mer.

   >[!IMPORTANT]
   >Du måste ha AEM version `2021.10.5933.20211012T154732Z` för att utnyttja nya frontledningslinjer.

* Varaktigheten i bildrutorna för kodkvalitet minskar avsevärt genom att utföra kodanalysen på ett mer effektivt sätt utan att behöva skapa en hel AEM. Denna förändring rullar ut progressivt under de veckor som följer efter releasen.

* Git-implementerings-ID visas nu i körningsinformationen för pipeline, vilket gör det enklare att spåra koden som skapades.

* Nu kan du skapa program via offentligt exponerade API:er.

* Miljöskapande är nu tillgängligt via offentligt exponerade API.

* The `x-request-id` svarshuvudet är nu synligt i API-uppspelningen på [www.adobe.io](https://www.adobe.io/). Det här huvudet är användbart när du skickar in kundvårdsproblem för felsökning.

* Som användare ser jag att Pipeline-kortet med noll rörledningar ger mig lämplig vägledning.

* Det finns nu en ny aktivitetssida där aktiviteter som pipeline och kodkörningar kan visas tillsammans med tillhörande information. Med tiden kommer de aktiviteter som listas på den här sidan att utvidgas tillsammans med de angivna detaljerna.

* Nu finns det en ny sida med Pipelines (Pipelines) med en statuspekare som du kan använda när du hovrar för att enkelt visa sammanfattningen av detaljer. Pipeline-körningar kan visas tillsammans med tillhörande information.

* API:t Redigera pipeline har nu stöd för att ändra miljön som används i distributionsfaserna.

* En optimering i OakPal-skanningsprocessen har införts för stora paket.

* CSV-filen för kvalitetsutgåva kommer nu att innehålla tidsstämpeln för varje kvalitetsproblem.

## Felkorrigeringar {#bug-fixes}

* Vissa oortodoxa byggkonfigurationer resulterade i att onödiga filer sparades i Pipelins Maven-artefaktcache, vilket resulterade i överflödig nätverks-I/O när byggbehållaren startades och stoppades.

* Pipeline PATCH API misslyckas om det inte finns någon distributionsfas.

* The `ClientlibProxyResourceCheck` kvalitetsregeln genererade falskt positiva problem när det fanns klientbibliotek med gemensamma grundsökvägar.

* Felmeddelandet när det maximala antalet databaser har uppnåtts specificerade inte orsaken till felet.

* I sällsynta fall misslyckades rörledningar på grund av olämplig hantering av vissa svarskoder.
