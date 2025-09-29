---
title: Märkordstaggar som stöds av HTML i arkivdokumentet
description: Referenshandbok för HTML märkordstaggar stöds nu vid dokumentgenerering, inklusive återgivningsbeteende och tillgänglighetsaspekter
feature: Adaptive Forms
role: Developer, User
exl-id: 8481b0dc-aae7-4bd2-acfe-1f1b6d747683
source-git-commit: 1794ed6cac612ee4600c2f8e1ced18c6130b64a2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Märkordstaggar som stöds av HTML i arkivdokumentet

## Vad den här referensen omfattar?

AEM Forms har nu stöd för HTML-taggar i RTF-fält när PDF-filer (Document of Record, DoR) genereras. Den här guiden förklarar vilka HTML-taggar du kan använda säkert i Adaptive Forms och hur de återges i de genererade dokumenten.

Om du lägger till RTF-innehåll (t.ex. fetstil, listor eller länkar) i formulär är det viktigt att du förstår vilka taggar som stöds och vilka begränsningar de kan ha. Den här referensen hjälper dig att välja lämpliga taggar för att säkerställa att innehållet visas korrekt och att det är tillgängligt i dokumentdokumentet.

## Innan du börjar

### Förutsättningar

Du bör känna till:

- Grundläggande syntax för HTML-markeringar
- [Grundläggande om arkivhandlingar](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- Tillgänglighetsprinciper och WCAG-riktlinjer
- PDF tillgänglighetskrav
- Adaptiva formulärkomponenter som accepterar HTML Markup

### Överväganden

Dokumentet kan vara taggat i PDF, vilket gör att hjälpmedelstekniken blir mer tillgänglig och strukturerad korrekt. Om du vill aktivera taggade PDF-utdata [anger du XCI-egenskapen `config/present/pdf/tagged` till `true`](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). När du har skapat din PDF är det viktigt att kontrollera att hjälpmedelstaggar används på rätt sätt. Du kan använda [Adobe Acrobat för att kontrollera tillgänglighetstaggar](https://helpx.adobe.com/in/acrobat/using/create-verify-pdf-accessibility.html) och kontrollera att dokumentet uppfyller tillgänglighetsstandarder.

### Nyheter

RTF-stöd i&quot;Document of Record&quot; är en ny förbättring. Tidigare visades RTF-innehåll som oformaterad text i genererade dokument. Med den här nya funktionen kan formaterat innehåll återges korrekt i PDF-utdata.

## Referens för stöd för HTML-taggar

### Taggar som stöds fullt ut

Dessa taggar stöds fullt ut när en hjälpmedelsnod skapas:

| HTML-tagg | Beskrivning | Dokumentstöd | Tillgänglighet | Exempel |
|----------|-------------|-------------|---------------|---------|
| `<p>` | Stycke | Ja | Fullt stöd - korrekt `<P>`-nod | `<p>This is a paragraph.</p>` |
| `<br/>` | Radbrytning | Ja | Fullt stöd - inom `<P>`-noden | `<p>Line 1<br/>Line 2</p>` |
| `<b>` | Fet text | Ja | Fullt stöd - inom `<P>`-noden | `<b>bold text</b>` |
| `<i>` | Kursiv text | Ja | Fullt stöd - inom `<P>`-noden | `<i>italic text</i>` |
| `<span>` | Allmän textbunden behållare | Ja | inom blockelement | `<span>styled text</span>` |
| `<sub>` | Nedsänkt | Ja | Fullt stöd - inuti blockelement | `H<sub>2</sub>O` |
| `<sup>` | Upphöjd | Ja | Fullt stöd - inom blockelement | `E=mc<sup>2</sup>` |
| `<a>` | Hyperlänk | Ja | Begränsad support - rätt kapsling krävs | `<a href="url">link text</a>` |


#### Problem med listtillgänglighet

Vid den aktuella liståtergivningen skapas `<P>` noder i stället för en korrekt liststruktur:

```
Current: <P>1. First item
Current: <P>2. Second item

Expected: <L>
Expected:   <LI>
Expected:     <LBL>1.
Expected:     <LBody>First item
```

### Taggar som inte stöds

Dessa taggar stöds inte och kommer inte att återges korrekt:

| HTML-tagg | Beskrivning | Alternativ lösning |
|----------|-------------|---------------------|
| `<h1>` - `<h6>` | Rubriktaggar | Använd formaterade `<p>`-taggar eller rubriker på designnivå |
| `<img>` | Bilder | Använd separata bildfält eller designmallar |
| `<code>` | Kodblock | Använd teckensnitt med fast teckenbredd med `<span>`-format |
| `<blockquote>` | Blockcitat | Använd formaterade `<p>`-taggar med indrag |
| `<table>` | Tabeller | Använda adaptiva formulärtabellkomponenter |

## Exempel på koder

### Grundläggande textformatering

```html
<!--  Supported - renders correctly -->
<p>This paragraph contains <b>bold text</b> and <i>italic text</i>.</p>

<!--  Supported - combined formatting -->
<p>This text is <i><b>bold and italic</b></i>.</p>

<!--  Unsupported - headings don't work -->
<h1>This won't render as a heading</h1>
```

### Listor

```html
<!-- ⚠️ Partially supported - renders but not accessible -->
<ol>
  <li>First numbered item</li>
  <li>Second numbered item</li>
</ol>

<ul>
  <li>First bullet point</li>
  <li>Second bullet point</li>
</ul>
```

### Länkar

```html
<!--  Supported - but must be within block elements -->
<p>Visit our <a href="https://example.com">website</a> for more information.</p>

<!--  Incorrect - link not properly nested -->
<a href="https://example.com">Standalone link</a>
```

### Vetenskaplig notering

```html
<!--  Supported - but limited accessibility -->
<p>Water formula: H<sub>2</sub>O</p>
<p>Einstein's equation: E=mc<sup>2</sup></p>
```

## Relaterat innehåll


- [Generera arkivdokument för adaptiv Forms](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- [Generera arkivdokument för kärnkomponenter](/help/forms/generate-document-of-record-core-components.md)
- [Anpassning av dokumentmall](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record)

