---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.3.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.3.0
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.3.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.3.0 är 11 mars 2021.

## Cloud Manager {#cloud-manager}

### Nyheter {#what-is-new}

* Kunder med miljöer med befintliga konfigurationer av anpassade domännamn för [IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) och [Anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) kommer att få ett meddelande om sina tidigare konfigurationer och kan självbetjäna via användargränssnittet.

* Användare med nödvändig behörighet kan nu redigera ett program och göra följande på ett självbetjäningssätt:
   * Lägg till Sites-lösning i ett befintligt program med Assets eller vice versa.
   * Ta bort platser eller resurser från ett befintligt program med både platser och resurser.
   * Lägg till andra, outnyttjade lösningsberättigande antingen till ett befintligt program eller som ett nytt program.

* **AEM** etiketten visas nu både för Pipeline Execution och Activity screens.

* Om en miljö är i viloläge men det även finns en AEM uppdatering tillgänglig, visas **Viloläge** status har företräde framför **Uppdatering tillgänglig**.

* Användarna kan nu se sin molnhanterarroll(er) genom att välja alternativet Visa molnhanterarroll(er) efter att ha navigerat till ikonen Användarprofil (överst till höger) i Unified Shell.

* Etiketten **Ansökan om godkännande** har fått en ny etikett till **Produktionsgodkännande** för större tydlighet.

* The **Version** etiketten har ändrats till **Git-tagg** i körningsfönstret för produktionspipeline.

* Etiketterna som definierar beteendet när viktiga mätvärden inte uppfyller det definierade tröskelvärdet har märkts om för att återspegla deras verkliga beteende: **Avbryt omedelbart** och **Godkänn omedelbart**.

* Listorna över klass- och metodborttagning har uppdaterats baserat på version `2021.3.4997.20210303T022849Z-210225` av AEM Cloud Service SDK.

* Produktionspipelinen för Cloud Manager kommer nu att innehålla [Testning av anpassat användargränssnitt](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) funktioner.

### Felkorrigeringar  {#bug-fixes}

* Paketversionshantering hoppades över i vissa fall under AEM push-uppgradering.

* Vissa kvalitetsproblem upptäcktes inte korrekt när paket bäddats in i andra paket.

* I svåra fall kan standardprogramnamnet som genereras när dialogrutan Lägg till program öppnas vara en dubblett av ett befintligt programnamn.

* Om användaren navigerar bort från sidan för pipeline-körning omedelbart efter att ha startat en pipeline visas ett felmeddelande om att åtgärden misslyckades, även om körningen faktiskt startar.

* Byggsteget startades om i onödan när kundbyggen resulterade i ogiltiga paket.

* Ibland kan användaren se en grön &quot;aktiv&quot; status bredvid ett IP-Tillåtelselista även när den konfigurationen inte har distribuerats.

* Alla befintliga produktionspipelinjer aktiveras automatiskt med Experience Audit-steget.
