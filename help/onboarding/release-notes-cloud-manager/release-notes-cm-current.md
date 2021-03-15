---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.3.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.3.0
translation-type: tm+mt
source-git-commit: 36e5e90785a1bc9a4f4f8d4febd462e00252a0ea
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2021.3.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.3.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.3.0 är 11 mars 2021.
Nästa version är planerad till den 8 april 2021.

## Cloud Manager {#cloud-manager}

### Nyheter {#what-is-new}

* Kunder som har miljöer med redan befintliga konfigurationer av anpassade domännamn för [IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) och [anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) kommer att se ett meddelande om sina tidigare konfigurationer och kommer att kunna självbetjäna via användargränssnittet.

* Användare med nödvändig behörighet kan nu redigera ett program och göra följande på ett självbetjäningssätt:
   * Lägg till Sites-lösning i ett befintligt program med Assets (eller vice versa).
   * Ta bort platser (eller resurser) från ett befintligt program med både platser och resurser.
   * Lägg till andra, outnyttjade lösningsberättigande antingen till ett befintligt program eller som ett nytt program.

* Etiketten AEM push-uppdatering visas nu för både Pipeline Execution och Activity screens.

* Om en miljö är i viloläge men det även finns en AEM tillgänglig, prioriteras statusen&quot;Viloläge&quot; framför&quot;Tillgänglig uppdatering&quot;.

* Användarna kan nu se sin molnhanterarroll(er) genom att välja alternativet Visa molnhanterarroll(er) efter att ha navigerat till ikonen Användarprofil (överst till höger) i Unified Shell.

* Etiketten&quot;Ansökan om godkännande&quot; har ändrats till&quot;Produktionsgodkännande&quot; för större tydlighet.

* Versionsetiketten har ändrats till&quot;Git-tagg&quot; i körningsfönstret för produktionspipeline.

* Etiketterna som definierar beteendet när viktiga mätvärden inte uppfyller det definierade tröskelvärdet har märkts om för att återspegla deras verkliga beteende - Avbryt omedelbart och godkänn omedelbart.

* Listorna över klass- och metodborttagning har uppdaterats baserat på version `2021.3.4997.20210303T022849Z-210225` av AEM Cloud Service-SDK.

* Produktionspipelinen för Cloud Manager kommer nu att innehålla testning av anpassade användargränssnitt.

### Felkorrigeringar {#bug-fixes}

* Paketversionshantering hoppades över i vissa fall under AEM push-uppgradering.

* Vissa kvalitetsproblem upptäcktes inte korrekt när paket bäddats in i andra paket.

* I svåra fall kan standardprogramnamnet som genereras när dialogrutan Lägg till program öppnas vara en dubblett av ett befintligt programnamn.

* Om användaren navigerar bort från sidan för pipeline-körning omedelbart efter att ha startat en pipeline visas ett felmeddelande om att åtgärden misslyckades, även om körningen faktiskt startar.

* Byggsteget startades om i onödan när kundbyggen resulterade i ogiltiga paket.

* Ibland kan användaren se en grön &quot;aktiv&quot; status bredvid ett IP-Tillåtelselista även när den konfigurationen inte har distribuerats.

* Alla befintliga produktionspipelinjer aktiveras automatiskt med Experience Audit-steget.