---
title: Hur utformar man JSON Schema för komponenter i adaptiva Form Core?
description: Lär dig att skapa ett JSON-schema för en adaptiv Form-kärna och skapa en adaptiv form (kärnkomponenter) baserad på schemat för att skapa schemalagda data.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 185b12bc-cea9-45c8-9b57-dc313bd0cfaa
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---

# Utforma JSON-schema för en adaptiv form (kärnkomponenter){#creating-adaptive-forms-using-json-schema}


| Version | Artikellänk |
| -------- | ---------------------------- |
| Foundation | [Klicka här](/help/forms/adaptive-form-json-schema-form-model.md) |
| Kärnkomponenter | Den här artikeln |


## Förutsättningar {#prerequisites}

Att skapa ett adaptivt formulär baserat på kärnkomponenter med ett JSON-schema som formulärmodell kräver grundläggande kunskaper i JSON-schema. Du bör läsa igenom följande innehåll före den här artikeln.

* [Skapa ett adaptivt formulär baserat på kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md)
* [JSON-schema](https://json-schema.org/)

## Använda ett JSON-schema som formulärmodell  {#using-a-json-schema-as-form-model}

Adobe Experience Manager Forms har stöd för att skapa ett adaptivt formulär baserat på kärnkomponenter genom att använda ett befintligt JSON-schema som formulärmodell. Detta JSON-schema representerar strukturen i vilken data produceras eller används av det bakomliggande systemet i din organisation. Det JSON-schema som du använder ska vara kompatibelt med [v4-specifikationer](https://json-schema.org/draft-04/schema).

De viktigaste funktionerna i ett JSON-schema är:

* Strukturen för JSON visas som ett träd på fliken Innehållssökning i redigeringsläget för ett adaptivt formulär. Du kan dra och lägga till element från JSON-hierarkin till den adaptiva formen baserat på kärnkomponenterna.
* Du kan fylla i formuläret i förväg med JSON som är kompatibel med det associerade schemat.
* När data skickas skickas skickas de som anges av användaren som JSON som är anpassad efter det associerade schemat.
* Du kan också skapa formuläret baserat på JSON-schemat enligt specifikationerna i [2012-20 version](https://json-schema.org/draft/2020-12/release-notes).

Ett JSON-schema består av enkla och komplexa elementtyper. Elementen har attribut som lägger till regler i elementet. När dessa element och attribut dras till ett adaptivt formulär mappas de automatiskt till motsvarande adaptiva formulärkomponenter.

Den här mappningen av JSON-element med adaptiva formulärkomponenter är följande:

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON-element, egenskaper eller attribut</strong></th>
   <th><strong>Adaptiv Form-komponent</strong></th>
  </tr>
  <tr>
   <td><p>Strängegenskaper med enum- och enumNames-begränsningen.</p> <p>Syntax,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Nedrullningsbar komponent:</p>
    <ul>
     <li>Värden som anges i enumNames visas i listrutan.</li>
     <li>Värden som anges i uppräkningen används för beräkning.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Strängegenskap med formatbegränsning. Till exempel e-post och datum.</p> <p>Syntax,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>E-postkomponenten mappas när typen är sträng och formatet är e-post.</li>
     <li>Textrutekomponent med validering mappas när typen är sträng och formatet är värdnamn.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Textfält<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number, egenskap<br /> </td>
   <td>Numeriskt fält med undertyp inställd på flytande<br /> </td>
  </tr>
  <tr>
   <td>heltalsegenskap<br /> </td>
   <td>Numeriskt fält med subtyp inställd på heltal<br /> </td>
  </tr>
  <tr>
   <td>boolesk egenskap<br /> </td>
   <td>Byt<br /> </td>
  </tr>
  <tr>
   <td>object, egenskap<br /> </td>
   <td>Panel<br /> </td>
  </tr>
  <tr>
   <td>arrayegenskap</td>
   <td>Upprepningsbar panel med min och max lika med minItems respektive maxItems. Endast homogena arrayer stöds. Objektbegränsningen måste därför vara ett objekt och inte en array.<br /> </td>
  </tr>
 </tbody>
</table>

### Vanliga schemaegenskaper {#common-schema-properties}

Det adaptiva formuläret använder information som finns i JSON-schemat för att mappa varje genererat fält. Särskilt gäller följande:

* The `title` fungerar som etikett för adaptiva formulärkomponenter.
* The `description` -egenskapen anges som en lång beskrivning för en adaptiv formulärkomponent.
* The `default` fungerar som det ursprungliga värdet i ett fält med adaptiv form.
* The `maxLength` egenskapen är inställd som `maxlength` textfältskomponentens attribut.
* The `minimum`, `maximum`, `exclusiveMinimum`och `exclusiveMaximum` -egenskaper används för NumericBox-komponenter.
* Till supportintervall för `DatePicker component` ytterligare egenskaper för JSON-schema `minDate` och `maxDate` tillhandahålls.
* The `minItems` och `maxItems` -egenskaper används för att begränsa antalet objekt/fält som kan läggas till eller tas bort från en panelkomponent.
* The `readOnly` egenskapen ställer in `readonly` för en adaptiv formulärkomponent.
* The `required` egenskapen anger att fältet Adaptivt formulär är obligatoriskt, medan den slutliga inskickade JSON-informationen i panelen (där typen är objekt) har fält med ett tomt värde som motsvarar det objektet.
* The `pattern` egenskapen anges som valideringsmönster (reguljärt uttryck) i adaptiv form.
* Tillägget för JSON-schemafilen måste behållas som .schema.json. Till exempel: &lt;filename>.schema.json.

## Exempel på JSON-schema {#sample-json-schema}

>[!BEGINTABS]

>[!TAB JSON Schema v4]

```json
{
"$schema": "https://json-schema.org/draft-04/schema#",
"definitions": {
  "employee": {
  "type": "object",
  "properties": {
    "userName": {
     "type": "string"
   },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
    "type": "string",
    "format": "email"
    },
    "language": {
     "type": "string"
   },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
   },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
  },
  "required": [
   "userName",
   "dateOfBirth",
   "language"
  ]
  },
    "personalDetails": {
   "type": "object",
  "properties": {
     "GeneralDetails": {
    "$ref": "#/definitions/GeneralDetails"
   },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
   }
   }
     },
  "projectDetails": {
   "type": "array",
   "items": {
   "properties": {
   "name": {
    "type": "string"
   },
   "age": {
    "type": "number"
   },
   "projects": {
    "$ref": "#/definitions/projects"
   }
  }
 },
 "minItems": 1,
 "maxItems": 4
},
"projects": {
 "type": "array",
 "items": {
  "properties": {
   "name": {
    "type": "string"
   },
   "age": {
    "type": "number"
   },
   "projectsAdditional": {
    "$ref": "#/definitions/projectsAdditional"
   }
  }
 },
 "minItems": 1,
 "maxItems": 4
},
"projectsAdditional": {
 "type": "array",
 "items": {
  "properties": {
   "Additional_name": {
    "type": "string"
   },
   "Additional_areacode": {
    "type": "number"
   }
  }
 },
 "minItems": 1,
 "maxItems": 4
},
"GeneralDetails": {
 "type": "object",
 "properties": {
  "age": {
   "type": "number"
  },
  "married": {
   "type": "boolean"
  },
  "phone": {
   "type": "number",
  },
  "address": {
   "type": "string"
  }
 }
},
"Family": {
 "type": "object",
 "properties": {
  "spouse": {
   "$ref": "#/definitions/spouse"
  },
  "kids": {
   "$ref": "#/definitions/kids"
  }
 }
},
"Income": {
 "type": "object",
 "properties": {
  "monthly": {
   "type": "number"
  },
  "yearly": {
   "type": "number"
  }
 }
},
"spouse": {
 "type": "object",
 "properties": {
  "name": {
   "type": "string"
  },
  "Income": {
   "$ref": "#/definitions/Income"
  }
 }
},
"kids": {
 "type": "array",
 "items": {
  "properties": {
   "name": {
    "type": "string"
   },
   "age": {
    "type": "number"
   }
  }
 },
 "minItems": 1,
 "maxItems": 4
}
},
"type": "object",
"properties": {
"employee": {
 "$ref": "#/definitions/employee"
}
}
}
```


>[!TAB JSON Schema 2012-20]


```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://example.com/employee.schema.json",
  "$defs": {
    "employee": {
      "type": "object",
      "properties": {
        "userName": {
          "type": "string"
        },
        "dateOfBirth": {
          "type": "string",
          "format": "date"
        },
        "email": {
          "type": "string",
          "format": "email"
        },
        "language": {
          "type": "string"
        },
        "personalDetails": {
          "$ref": "#/$defs/personalDetails"
        },
        "projectDetails": {
          "$ref": "#/$defs/projectDetails"
        }
      },
      "required": [
        "userName",
        "dateOfBirth",
        "language"
      ]
    },
    "personalDetails": {
      "type": "object",
      "properties": {
        "GeneralDetails": {
          "$ref": "#/$defs/GeneralDetails"
        },
        "Family": {
          "$ref": "#/$defs/Family"
        },
        "Income": {
          "$ref": "#/$defs/Income"
        }
      }
    },
    "projectDetails": {
      "type": "array",
      "items": {
        "properties": {
          "name": {
            "type": "string"
          },
          "age": {
            "type": "number"
          },
          "projects": {
            "$ref": "#/$defs/projects"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "projects": {
      "type": "array",
      "items": {
        "properties": {
          "name": {
            "type": "string"
          },
          "age": {
            "type": "number"
          },
          "projectsAdditional": {
            "$ref": "#/$defs/projectsAdditional"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "projectsAdditional": {
      "type": "array",
      "items": {
        "properties": {
          "Additional_name": {
            "type": "string"
          },
          "Additional_areacode": {
            "type": "number"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "GeneralDetails": {
      "type": "object",
      "properties": {
        "age": {
          "type": "number"
        },
        "married": {
          "type": "boolean"
        },
        "phone": {
          "type": "number",
        },
        "address": {
          "type": "string"
        }
      }
      }
  }
  }
```

>[!ENDTABS]

De viktigaste ändringarna från JSON Schema V4 till specifikationerna för version 2020-12 är:
* Id har deklarerats som `$id`
* definitioner deklareras som `$defs`

### Återanvändbara schemadefinitioner {#reusable-schema-definitions}

Definitionsnycklar används för att identifiera återanvändbara scheman. Återanvändbara schemadefinitioner används för att skapa fragment. <!-- It is similar to identifying complex types in XSD.--> Ett exempel på JSON-schema med definitioner ges nedan:

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

Exemplet ovan definierar en kundpost där varje kund har både en leveransadress och en faktureringsadress. Adressernas struktur är densamma - adresserna har en gatuadress, ort och delstat - så det är en bra idé att inte duplicera adresserna. Det gör det också enkelt att lägga till och ta bort fält för framtida ändringar.

<!--
## Pre-Configuring fields in JSON Schema Definition {#pre-configuring-fields-in-json-schema-definition}

You can use the **aem:afProperties** property to preconfigure JSON Schema field to map to a custom Adaptive Form component. An example is listed below:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}

```

<!--- ## Configure scripts or expressions for form objects  {#configure-scripts-or-expressions-for-form-objects}

JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. You can pre-configure form objects to [evaluate an expression](adaptive-form-expressions.md) on a form event.

Use the aem:afproperties property to preconfigure Adaptive Form expressions or scripts for Adaptive Form components. For example, when the initialize event is triggered, the below code sets value of telephone field and prints a value to the log :

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

You should be a member of the [forms-power-user group](forms-groups-privileges-tasks.md) to configure scripts or expressions for form object. The below table lists all the script events supported for an Adaptive Form component.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Component \ Event</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>Visibility</td>
   <td>Validate</td>
   <td>Enabled</td>
   <td>Value Commit</td>
   <td>Click </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Text Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Stepper</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Radio Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telephone</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Switch</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Check Box</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Drop-down</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Image Choice</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Date Input Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Date Picker</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Email</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>File Attachment</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Image</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Some examples of using events in a JSON are hiding a field on initialize event and configure value of another field on value commit event. For detailed information about creating expressions for the script events, see [Adaptive Form Expressions](adaptive-form-expressions.md).

Here is the sample JSON code for previously mentioned examples.

### Hiding a field on initialize event {#hiding-a-field-on-initialize-event}

```json

"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configure value of another field on value commit event {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}

```
-->

## Begränsa tillåtna värden för en adaptiv formulärkomponent {#limit-acceptable-values-for-an-adaptive-form-component}

Du kan lägga till följande begränsningar i JSON-schemaelement för att begränsa vilka värden som tillåts i en Adaptiv Form-kärnkomponent:

<table>
 <tbody>
  <tr>
   <td><p><strong> Schemaegenskap</strong></p> </td>
   <td><p><strong>Datatyp</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
   <td><p><strong>Komponent</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger den övre gränsen för numeriska värden och datum. Som standard inkluderas maxvärdet.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege<br /> </li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger den nedre gränsen för numeriska värden och datum. Som standard inkluderas minimivärdet.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege</li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Boolean</p> </td>
   <td><p>Om värdet är true måste det numeriska värdet eller datumet som anges i formulärets komponent vara mindre än det numeriska värdet eller datumet som anges för egenskapen maximum.</p> <p>Om värdet är false måste det numeriska värdet eller datumet som anges i formulärets komponent vara mindre än eller lika med det numeriska värdet eller datumet som anges för egenskapen maximum.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege</li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Boolean</p> </td>
   <td><p>Om true måste det numeriska värdet eller datumet som anges i formulärets komponent vara större än det numeriska värdet eller datumet som anges för egenskapen minimum.</p> <p>Om värdet är false måste det numeriska värdet eller datumet som anges i formulärets komponent vara större än eller lika med det numeriska värdet eller datumet som anges för egenskapen minimum.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege</li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger det minsta antalet tecken som tillåts i en komponent. Minimilängden måste vara lika med eller större än noll.</p> </td>
   <td>
    <ul>
     <li>Textruta</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>Sträng</td>
   <td>Anger maximalt antal tecken som tillåts i en komponent. Den maximala längden måste vara lika med eller större än noll.</td>
   <td>
    <ul>
     <li>Textruta</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger teckensekvensen. En komponent accepterar tecknen om tecknen överensstämmer med det angivna mönstret.</p> <p>Egenskapen pattern mappar till valideringsmönstret för motsvarande komponent i adaptiv form.</p> </td>
   <td>
    <ul>
     <li>Alla adaptiva Forms-komponenter som är mappade till ett XSD-schema </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>Sträng</td>
   <td>Anger maximalt antal objekt i en array. Det maximala antalet objekt måste vara lika med eller större än noll.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>Sträng</td>
   <td>Anger det minsta antalet objekt i en array. Minimiobjekten måste vara lika med eller större än noll.</td>
   <td> </td>
  </tr>
 </tbody>
</table>


## Aktivera schemakompatibla data {#enablig-schema-compliant-data}

Följ de här stegen för att aktivera alla schemabaserade anpassningsbara Forms för att generera schemakompatibla data när formulär skickas:

1. Gå till webbkonsolen Experience Manager på `https://server:host/system/console/configMgr`.
1. Sök **[!UICONTROL Adaptive Form and Interactice Communication Web Channel Configuration]**.
1. Välj det här alternativet om du vill öppna konfigurationen i redigeringsläge.
1. Välj **[!UICONTROL Generate Schema Compliant Data]** kryssrutan.
1. Spara inställningarna.

![adaptiv form och konfiguration av interaktiv kommunikationskanal](/help/forms/assets/af-ic-web-channel-configuration.png)


## Konstruktioner som inte stöds  {#non-supported-constructs}

Adaptiv Forms stöder inte följande JSON-schemakonstruktioner:

* Null-typ
* Unionstyper, t.ex., och
* OneOf, AnyOf, AllOf, och NOT
* Endast homogena arrayer stöds. Objektbegränsningen måste därför vara ett objekt och inte en array.
* URI-referenser i $ref

## Frågor och svar {#frequently-asked-questions}

**Varför kan jag inte dra enskilda element i ett delformulär (struktur som genereras från en komplex typ) för repeterbara delformulär (värdena minOcCours och maxOccurs är större än 1)?**

I ett upprepningsbart delformulär måste du använda hela delformuläret. Om du bara vill ha selektiva fält använder du hela strukturen och tar bort de oönskade.

**Jag har en lång komplex struktur i Content Finder. Hur hittar jag ett specifikt element?**

Du har två alternativ:

* Bläddra genom trädstrukturen
* Använd sökrutan för att hitta ett element

**Vad ska tillägget för JSON-schemafilen vara?**

Tillägget för JSON-schemafilen måste vara .schema.json. Till exempel: &lt;filename>.schema.json.

**Är `aem:afProperties` stöds som en del av JSON-schemat i Adaptive Forms baserat på kärnkomponenter?**

Nej, `aem:afProperties` stöds inte för kärnkomponenter. Den här egenskapen stöds bara för grundkomponenter.

## Se även {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Design XML Schema for an Adaptive Form](/help/forms/adaptive-form-xml-schema-form-model.md)

-->
