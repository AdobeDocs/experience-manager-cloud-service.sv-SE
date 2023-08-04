---
title: Konfigurera massredigering av sidegenskaper
description: Lär dig konfigurera gruppredigering så att du kan redigera egenskaperna för flera sidor samtidigt.
source-git-commit: 9563c24c2794f8209494891da1a4a5a3360781db
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Konfigurera massredigering av sidegenskaper {#configuring-bulk-editing-of-page-properties}

[Massredigering av sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages) gör att du kan redigera egenskaperna för flera sidor samtidigt.

## Överväganden {#considerations}

Sidegenskaper är inte aktiverade för massredigering som standard. De måste vara uttryckligen aktiverade. När du definierar vilka sidegenskaper som ska vara tillgängliga för massredigering måste du ta hänsyn till vissa konsekvenser, till exempel:

* Vissa fält är vanligtvis unika. Du måste bestämma om det är meningsfullt att aktivera sådana fält för massredigering, när ett värde ska användas.
   * Exempelvis är sidtitlar nästan alltid unika.
* Vissa fält kan ha flera värden som behöver återges på ett meningsfullt sätt vid återgivningen.
   * En nedrullningsbar meny med till exempel etiketten **Klar för publicering**. Detta kan ha flera värden före gruppredigering, till exempel **klar**, **granskning**, **pågående**, osv.

På grund av möjligheten att det finns flera värden bör du bara aktivera följande fälttyper för gruppredigering.

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## Aktivera ett fält {#enabling-a-field}

De här stegen använder `/apps/core/wcm/components/page/v1/page` från [WKND-exempelinnehåll](/help/implementing/developing/introduction/develop-wknd-tutorial.md) som ett exempel för att aktivera massredigering på ett fält i en utvecklingsmiljö.

1. Om du använder CRXDE öppnas sidkomponenten.
1. Navigera till det obligatoriska fältet i `cq:dialog` definition.
1. Definiera följande egenskap på fältnoden:

   * **Namn**: `allowBulkEdit`
   * **Typ**: `Boolean`
   * **Värde**: `true`

1. Välj **Spara alla** för att behålla uppdateringarna.

## Begränsningar {#limitations}

Massredigering av sidegenskaper är:

* Inte tillgängligt för sidor i en live-kopia.
* Endast tillgängligt för sidor med samma resurstyp.
