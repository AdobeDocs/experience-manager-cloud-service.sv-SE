---
title: De bästa sätten att designa högpresterande Forms
description: Lär dig de bästa sätten att skapa användarvänliga, tillgängliga och högpresterande formulär med AEM Forms. Förbättra datakvaliteten, användarupplevelsen och antalet lyckade ansökningar.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# De bästa sätten att skapa Forms

Att skapa bra formulär går bortom bara tekniken. Så här ser du till att formulären är användarvänliga och att de uppfyller sina mål:

## Designa användarvänliga och tillgängliga Forms

* **Använd tydliga, synliga etiketter:** Alla formulärfält behöver en `<label>`. Förlita dig inte bara på platshållartext (text i indatafältet), eftersom den försvinner när användaren skriver och inte är tillgänglig.
   * *Bra:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   * *Felaktig:* `<input type="email" placeholder="Email Address">`
* **Behåll det enkelt:** Använd HTML standardindatatyper (`<input type="date">`, `<input type="tel">`) där det är möjligt. De har ofta bättre mobilstöd och tillgänglighet än komplexa anpassade widgetar.
* **Logisk ordning och gruppering:** Ordna fält på ett sätt som är begripligt för användaren. Gruppera relaterade fält tillsammans med `<fieldset>` och `<legend>`.
* **Ange tydliga instruktioner:** Ge kortfattad hjälptext eller verktygstips för fält som kan vara förvirrande.
* **Tangentbordsnavigering:** Se till att användarna bara kan navigera genom hela formuläret via tangentbordet (Tabb, Skift+Tabb, Enter, Blanksteg).
* **Felhantering:** Gör fel tydliga och enkla att korrigera. Visa felmeddelanden bredvid det relevanta fältet och förklara vad som behöver korrigeras.

* **Kontrollera att Forms-inläsningen är snabb och synlig**

   * **Placera Forms tydligt:** Om ett formulär är viktigt bör du se till att användarna ser det enkelt utan att behöva rulla för mycket (&quot;ovanför det veckade&quot; om möjligt). Adobe forskning visar att många formulär får låg interaktion eftersom de är dolda.
   * **Optimera Assets:** Håll alla anpassade JavaScript- eller CSS-format för dina formulär så små som möjligt för att säkerställa snabba inläsningstider. Edge Delivery Services hjälper till med inläsningen av bassidor, men tunga formulärskript kan ändå göra det långsammare.

* **Hantera användardata på ett ansvarsfullt sätt**
   * **Fråga bara vad du behöver:** Ju mindre personligt ID-information (PII) du frågar efter, desto bättre. Varje fält kan vara en anledning till att en användare överger formuläret.
   * **Var genomskinlig:** Förklara *varför* du behöver viss information och *hur den ska användas*. Länk till din integritetspolicy. Detta skapar förtroende.

* **Förbättra användarupplevelsen: Captcha-alternativ**

   * **Rethink Visible Captchas:** Testen &quot;type the wavy text&quot; eller &quot;click all the car lights&quot; kan vara mycket frustrerande för användare, särskilt för personer med funktionshinder, och ofta leda till höga bortfall.

* **Ta hänsyn till alternativ:**
   * **Fläckfält:** Lägg till ett dolt fält som bara kan fyllas i med bågar. Om den innehåller data är överföringen trolig för skräppost.
   * **Tidsbaserade kontroller:** Mät hur snabbt ett formulär skickas. För snabba inlämningar är ofta stötande.
   * **Osynlig reCAPTCHA (v3):** Den här Google-tjänsten analyserar användarbeteendet i bakgrunden och utgör bara en utmaning om användaren verkar misstänkt. Detta är ofta en mycket bättre användarupplevelse.

## Form Design Do&#39;s and Don&#39;ts

| Gör ✅ - för bättre Forms | ❌ - undvik dessa |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| Använd synliga `<label>`-taggar för alla fält | Använd bara platshållartext i stället för riktiga etiketter |
| Använd HTML standardindatatyper (t.ex. `<input type="email">`) | Använda alltför komplexa anpassade widgetar |
| Säkerställ fullständig tangentbordsnavigering | Tillhandahåll otydliga eller saknade felmeddelanden |
| Visa tydliga, åtgärdbara felmeddelanden | Begär överflödiga personuppgifter utan motivering |
| Fråga bara efter nödvändig information | Använda svårlösta synliga CAPTCHA-bilder |
| Förklara hur data används (sekretessinformation eller länkar) | Dölja formuläret djupt på sidan |
| Använd osynliga eller beteendestyrda CAPTCHA-tekniker |                                                                  |
| Gör formuläret enkelt att hitta på sidan (framträdande placering) |                                                                  |


## Nästa steg

Den här guiden innehåller en översikt över hur du använder formulär med AEM Edge Delivery Services. Mer detaljerade, stegvisa instruktioner om specifika konfigurationer finns i Adobe Experience Manager officiella dokumentation:

* [Dokumentbaserad redigering med Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Universell redigerare med Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Dokumentredigering (DA) och inbäddat innehåll](https://www.aem.live/developer/da-tutorial)
* [AEM Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
