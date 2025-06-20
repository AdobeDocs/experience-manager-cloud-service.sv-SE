---
title: Konfigurera massredigering av sidegenskaper
description: Lär dig konfigurera gruppredigering så att du kan redigera egenskaperna för flera sidor samtidigt.
exl-id: 0d10c6b9-8643-479d-adc1-4066d227e83d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 3238b11cdd891cf18048199d4103397e3af75edf
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Konfigurera massredigering av sidegenskaper {#configuring-bulk-editing-of-page-properties}

[Med gruppredigering av sidegenskaper](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#from-the-sites-console-multiple-pages) kan du redigera egenskaperna för flera sidor samtidigt.

## Överväganden {#considerations}

Sidegenskaper är inte aktiverade för massredigering som standard. De måste vara uttryckligen aktiverade. När du definierar vilka sidegenskaper som ska vara tillgängliga för massredigering måste du ta hänsyn till vissa konsekvenser, till exempel:

* Vissa fält är vanligtvis unika. Du måste bestämma om det är meningsfullt att aktivera sådana fält för massredigering, när ett värde ska användas.
   * Exempelvis är sidtitlar nästan alltid unika.
* Vissa fält kan ha flera värden som behöver återges på ett meningsfullt sätt vid återgivningen.
   * En statuslistruta med namnet **Klar för publikation**. Detta kan ha flera värden före gruppredigering, t.ex. **ready**, **in-review**, **in-progress** osv.

På grund av möjligheten att det finns flera värden bör du bara aktivera följande fälttyper för gruppredigering.

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## Aktivera ett fält {#enabling-a-field}

De här stegen använder `/apps/core/wcm/components/page/v1/page` från [WKND-exempelinnehållet](/help/implementing/developing/introduction/develop-wknd-tutorial.md) som exempel för att aktivera massredigering av ett fält i en utvecklingsmiljö.

1. Om du använder CRXDE öppnas sidkomponenten.
1. Navigera till det obligatoriska fältet i definitionen `cq:dialog`.
1. Definiera följande egenskap på fältnoden:

   * **Namn**: `allowBulkEdit`
   * **Typ**: `Boolean`
   * **Värde**: `true`

1. Välj **Spara alla** om du vill behålla uppdateringarna.

## Begränsningar {#limitations}

Massredigering av sidegenskaper är:

* Inte tillgängligt för sidor i en live-kopia.
* Endast tillgängligt för sidor med samma resurstyp.
