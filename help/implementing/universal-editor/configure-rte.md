---
title: Konfigurera RTE för Universal Editor
description: Lär dig hur du konfigurerar RTF-redigeraren i Universell redigerare.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 60699db418e5f02b8bdb0471eb2996c9caf5694b
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Konfigurera RTE för Universal Editor {#configure-rte}

Lär dig hur du konfigurerar RTF-redigeraren i Universell redigerare.

>[!NOTE]
>
>Den här dokumentationen gäller den nya RTE-versionen för den universella redigeraren, som är tillgänglig som en tidig adopter-funktion. Om du är intresserad av att testa den här nya funktionen [kan du få mer information i versionsinformationen.](/help/release-notes/universal-editor/current.md#new-rte)

## Ökning {#overview}

Den universella redigeraren har en RTF-redigerare som både finns på plats och på egenskapspanelen där författare kan tillämpa formateringsändringar när de redigerar texten.

Den här textredigeraren kan konfigureras med [-komponentfilter.](/help/implementing/universal-editor/filtering.md) Det här dokumentet beskriver vilka konfigurationsalternativ som är tillgängliga tillsammans med exempel.

## Konfigurationsstruktur {#structure}

RTE-konfigurationen består av två delar:

* [`toolbar`](#toolbar): Verktygsfältskonfigurationen styr vilka redigeringsalternativ som är tillgängliga i användargränssnittet och hur de är ordnade.
* [`actions`](#actions): Med åtgärdskonfigurationen kan du anpassa beteendet och utseendet för enskilda redigeringsåtgärder.

Dessa konfigurationer kan definieras som en del av ett [komponentfilter](/help/implementing/universal-editor/filtering.md) med egenskapen `rte`.

```json
[
  {
    "id": "richtext",
    "rte": {
      "toolbar": {
        // Toolbar configuration
      },
      "actions": {
        // Action-specific configurations
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## Konfiguration av verktygsfält {#toolbar}

Verktygsfältskonfigurationen styr vilka redigeringsalternativ som är tillgängliga i användargränssnittet och hur de är ordnade. Det här är tillgängliga avsnitt

```json
{
  "toolbar": {
    // Text formatting options
    "format": ["bold", "italic", "underline", "strike"],
    // Text alignment options
    "alignment": ["left", "center", "right", "justify"],
    // Text direction options, right-to-left or left-to-right
    "direction": ["rtl", "ltr"],
    // Indentation controls
    "indentation": ["indent", "outdent"],
    // Block-level elements
    "blocks": ["paragraph", "h1", "h2", "h3", "h4", "h5", "h6", "code_block"],
    // List options
    "list": ["bullet_list", "ordered_list"],
    // Content insertion
    "insert": ["link", "unlink"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## Åtgärdskonfiguration {#actions}

Med åtgärdskonfigurationen kan du anpassa beteendet och utseendet för enskilda redigeringsåtgärder. Det här är de tillgängliga avsnitten.

### Formatera funktionsmakron {#format}

Formateringsåtgärder används för att formatera och stödja byte av taggar i HTML för att välja mellan semantiska varianter. Följande avsnitt är tillgängliga.

```json
{
  "actions": {
    "bold": {
      "tag": "strong",      // Use <strong> instead of <b>
      "shortcut": "Mod-B",  // Custom keyboard shortcut
      "label": "Make Bold"  // Custom button label 
    },
    "italic": {
      "tag": "em",          // Use <em> instead of <i>
      "shortcut": "Mod-I",
      "label": "Italicize"
    },
    "strike": {
      "tag": "del"          // Use <del> instead of <s>
    }
  }
}
```

### Liståtgärder {#list}

Liståtgärder har stöd för innehållsbrytning för att styra HTML-strukturen. Följande avsnitt är tillgängliga.

```json
{
  "actions": {
    "bullet_list": {
      "wrapInParagraphs": true,    // <ul><li><p>content</p></li></ul>
      "shortcut": "Mod-Shift-8",   // Custom shortcut
      "label": "Bullet List"       // Custom label
    },
    "ordered_list": {
      "wrapInParagraphs": false,   // <ol><li>content</li></ol> (default)
      "shortcut": "Mod-Shift-9"
    }
  }
}
```

### Länkåtgärder {#link}

Länkåtgärder stöder kontroll av målattribut för att hantera länkbeteenden. Följande avsnitt är tillgängliga.

```json
{
  "actions": {
    "link": {
      "hideTarget": false,       // Show target attribute options (default)
      "shortcut": "Mod-K",       // Custom keyboard shortcut
      "label": "Insert Link"     // Custom button label
    },
    "unlink": {
      "shortcut": "Mod-Shift-K", // Custom keyboard shortcut
      "label": "Remove Link"     // Custom button label
    }
  }
}
```

#### Alternativ för länkkonfiguration {#link-options}

* `hideTarget`: `false` (standard) - Inkludera målattribut i länkar, tillåter `_self`, `_blank` osv.
* `hideTarget`: `true` - Uteslut målattribut från länkar helt

Åtgärden `unlink` visas bara när markören är placerad i en befintlig länk. Länkformateringen tas bort samtidigt som textinnehållet bevaras.

### Andra åtgärder {#other}

Alla andra åtgärder har stöd för grundläggande anpassning. Följande avsnitt är tillgängliga.

```json
{
  "actions": {
    "h1": {
      "shortcut": "Mod-Alt-1",
      "label": "Large Heading"
    },
    "paragraph": {
      "shortcut": "Mod-Alt-0",
      "label": "Normal Text"
    },
    "link": {
      "shortcut": "Mod-K",
      "label": "Insert Link",
      "hideTarget": false    // Show target attribute options (default: false)
    }
  }
}
```

## Fullständigt exempel {#example}

Följande är ett exempel på en fullständig konfiguration.

```json
[
  {
    "id": "richtext",
    "rte": {
      // Configure which tools appear in toolbar
      "toolbar": {
        "format": [
          "bold",
          "italic"
        ],
        "blocks": [
          "paragraph",
          "h1",
          "h2"
        ],
        "list": [
          "bullet_list",
          "ordered_list"
        ],
        "insert": [
          "link",
          "unlink"
        ],
        "sections": [
          "format",
          "blocks",
          "list",
          "insert"
        ]
      },
      // Customize individual action behavior
      "actions": {
        // Format actions with HTML tag choices
        "bold": {
          "tag": "strong",
          "shortcut": "Mod-B",
          "label": "Bold"
        },
        "italic": {
          "tag": "em",
          "shortcut": "Mod-I"
        },
        // List actions with content wrapping
        "bullet_list": {
          "wrapInParagraphs": true,
          "label": "Bullet List"
        },
        "ordered_list": {
          "wrapInParagraphs": false
        },
        // Link actions with target control
        "link": {
          "hideTarget": false,
          "shortcut": "Mod-K",
          "label": "Add Link"
        },
        "unlink": {
          "label": "Remove Link"
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## Information om åtgärdsalternativ {#action-details}

Flera alternativ har ytterligare information som är viktig att tänka på.

### `wrapInParagraphs` {#wrapInParagraphs}

Alternativet `wrapInParagraphs` för listor styr HTML-strukturen.

#### `wrapInParagraphs: false` (standard) {#wrapInParagraphs-false}

```html
<ul>
  <li>Simple text content</li>
  <li>Another item</li>
</ul>
```

#### `wrapInParagraphs: true` {#wrapInParagraphs-true}

```html
<ul>
  <li><p>Text wrapped in paragraphs</p></li>
  <li><p>Supports rich formatting within items</p></li>
</ul>
```

Använd `wrapInParagraphs: true` när du behöver:

* Omfattande formatering i listobjekt
* Flera stycken per listobjekt
* Enhetlig formatering på blocknivå

### Alternativ för länkmål {#link-target}

Alternativet `hideTarget` för länkar styr om attributet `target` ingår i genererade länkar och om dialogrutan för att skapa länkar innehåller ett fält för målval.

#### `hideTarget: false` (standard) {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### Märkordsalternativ {#tag}

Med formateringsåtgärder kan du växla mellan HTML varianter.

| Åtgärd | Standardtagg | Alternativa taggar | Användningsfall |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | Semantisk kontra visuell betoning |
| `italic` | `<em>` | `<i>` | Semantisk kontra visuell stil |
| `strike` | `<del>` | `<s>` | Visuell kontra semantisk borttagning |

Välj semantiska taggar (`<strong>`, `<em>`, `<del>`) för bättre tillgänglighet och SEO.

### Kortkommandon {#keyboard-shortcuts}

Kortkommandon använder formatet `Mod-Key` där:

* `Mod` = `Cmd` på Mac, `Ctrl` på Windows/Linux
* Exempel: `Mod-B`, `Mod-Shift-8`, `Mod-Alt-1`
