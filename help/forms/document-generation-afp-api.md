---
title: Hur använder man AFP-API för utdatasynkronisering?
description: Lär dig hur du använder API:t för AFP-utdatasynkronisering för att hämta och synkronisera utdatarenderingar.
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
exl-id: 5602fc63-ef74-44eb-b3be-61b8f8a2795a
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Generera AFP-utdata med AEM Forms API

<span class="preview"> Den här funktionen är en förhandsversion och kan nås via vår [förhandsutgåva](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=sv-SE#new-features). </span>

AFP (Advanced Function Presentation) är ett högpresterande dokumentformat som huvudsakligen är avsett för tryck.\
I den här guiden beskrivs alla nödvändiga steg och konfigurationer för att generera AFP-utdata med AEM Forms.

<!--
## Prerequisites

To support AFP output generation, the following OSGi bundles must be present and in an **active** state:

* **AFP Core Bundle** – Available in the AFP repository
* **Forms Output Core** – Found in the Forms Output comments package
* **Bedrock Connector** – Provided by the Forms Output API
* **Cloud Ready Implementation** – Available through the Forms installer

>[!NOTE]
>
> * If any bundle is inactive, resolve dependency issues or reinstall manually.
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.-->

## API för AFP-generering

Skapar en AFP-fil (Advanced Function Presentation) med en XDP-mall och indata.

### Behörighet

Du kan antingen använda **BasicAuth** (administratörsuppgifter) för lokala miljöer eller **BearerAuth**-auktorisering för AEM Cloud-instanser.

### Begäran

**Slutpunkt:**
`POST http://<server>:<port>/adobe/forms/document/generate/afp`

### Sidhuvuden

| Nyckel | Värde |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### Begärandetext

**Innehållstyp: multipart/form-data**

| Nyckel | Typ | Obligatoriskt | Beskrivning |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | Fil/text | Ja | XDP-fil som används som mall för AFP-generering (t.ex. `demo.xdp`) |
| `data` | Fil/text | Nej | Datafil (XML eller JSON) som ska sammanfogas med mallen (t.ex. `data.xml`) |
| `options` | Text | Nej | JSON-sträng med alternativ för att styra AFP-utdata (t.ex. upplösning, språkområde) |

**Exempel `options` JSON (textfält):**

```json
{
  "pdfVersion": "1.7",
  "resolution": 300,
  "locale": "en-US",
  "embedFonts": true,
  "contentRoot": "/usr/tmp"
}
```

### Svar

| Code | Beskrivning |
| ----- | ------------------------------------------------------------------------- |
| `200` | Åtgärden lyckades. Returnerar AFP-dokumentströmmen. |
| `400` | Felaktig begäran. Nyttolasten för begäran är felaktig eller nödvändiga fält saknas. |
| `500` | Internt serverfel. Försök igen om en stund. |

### Kommandot Rulla

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### Testa API:t

Du kan hämta .yaml-filen och överföra den till Postman för att kontrollera API:ernas funktioner.

![AFP Postman-bild](/help/forms/assets/afp-postman.png)

Du kan spara svaret och öppna den sparade filen i AFP-läsaren för att visa den.

![PDF Reader](/help/forms/assets/afp-pdf.png)
