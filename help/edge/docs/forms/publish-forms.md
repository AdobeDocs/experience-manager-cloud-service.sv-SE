---
title: Publicera en Edge Delivery Services för AEM Forms
description: Publicera en Edge Delivery Services för AEM Forms
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# Publicera formuläret och börja samla in data

När du är redo att dela formuläret med dina kunder för datainsamling eller insändning kan du helt enkelt publicera det, så att formuläret blir lätt tillgängligt för kunderna.

![Dokumentbaserat redigeringssystem](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Krav

- Du har ett AEM-projekt baserat på [AEM Forms-standardmallen](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) eller [har lagt till Adaptivt Forms-block i ditt befintliga AEM-projekt](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
- Formuläret är fullständigt testat och klart att användas.
- Ditt [kalkylblad är konfigurerat](/help/edge/docs/forms/submit-forms.md) för att ta emot data.


## Publicera formuläret

+++ &#x200B;1. Publicera kalkylbladet

1. Öppna ditt Microsoft SharePoint- eller Google Drive-konto och gå till din projektkatalog för AEM Edge Delivery.

1. Öppna det kalkylblad som innehåller ditt formulär. [Förfrågan](/help/edge/assets/enquiry.xlsx) är till exempel en Microsoft Excel-arbetsbok.

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska bladet.

   ![Använd AEM Sidekick för att förhandsgranska bladet](/help/edge/assets/preview-form.png)

   När förhandsgranskningen har slutförts konverteras kalkylbladsinnehållet till JSON-format. Förhandsgranskningssidan visar sedan innehållet i ett strukturerat tabellformat. Till exempel illustrerar den medföljande bilden innehållet i ett frågeformulär.

   ![Forms Preview JSON-format](/help/edge/assets/forms-preview-json-format.png)

1. Publicera bladet med AEM Sidekick. Se till att du hämtar publicerings-URL:en, eftersom detta krävs för att återge formuläret i nästa avsnitt. URL-formatet är följande:


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form>.json
   ```

   - `<branch>` refererar till din GitHub-databas.
   - `<repository>` betecknar din GitHub-databas.
   - `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.

   Om projektdatabasen till exempel heter&quot;weFinance&quot;, finns den under kontot&quot;wkndform&quot; och du använder huvudgrenen och formuläret som&quot;förfrågan&quot;, ser URL:en ut så här:

   `https://main--wefinance--wkndform.aem.live/enquiry.json`
&lt;!—(https://main—weFinance—wkndform.aem.live/inquiry.json)—>

+++

+++ &#x200B;2. Lägg till formuläret på din webbsida

Lägg till `<form>.json` på en webbsida för att underlätta kundinteraktion, så att formuläranvändare enkelt kan fylla i och skicka formuläret.


Så här lägger du till formuläret på din webbsida:

1. Gå till ditt Microsoft SharePoint- eller Google Drive-konto och navigera till din `[AEM Edge Delivery project directory]`.

1. Öppna en dokumentfil där du vill bädda in formuläret. Du kan t.ex. öppna filen [förfrågningsformulär.docx](/help/edge/assets/enquiry-form.docx) eller skapa ett nytt dokument.

1. Identifiera det önskade avsnittet i dokumentet där du vill infoga formuläret och navigera sedan till det.

1. Lägg till ett block med namnet &#39;Formulär&#39; i filen. Om projektdatabasen till exempel heter&quot;weFinance&quot; finns den under kontoägaren&quot;wkndform&quot; och du använder huvudgrenen.

   | Formulär |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

   ![Lägg till ett block med namnet Form i filen](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Det här blocket fungerar som en platshållare där formuläret är inbäddat. Lägg till URL:en för din `<form>.json`-fil som en hyperlänk på den andra raden i blocket.

   >[!IMPORTANT]
   >
   >
   > Kontrollera att URL-adressen är formaterad som en hyperlänk i stället för att visas som oformaterad text.

   Använd URL:en för förhandsgranskning (.page URL) för utvecklings- eller teständamål, eller publicerings-URL:en (.live) för produktion.

   Om projektdatabasen till exempel heter&quot;weFinance&quot; finns den under kontoägaren&quot;wkndform&quot; och du använder huvudgrenen.

   Här är några exempel på förhandsgransknings- och publicerings-URL:

   **Förhandsgranska URL**

   | Formulär |
   |---|
   | `https://main--wefinance--wkndform.aem.page/enquiry.json` |


   **Publicera URL**

   | Formulär |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska webbsidan. Formuläret visas nu på sidan. Här är till exempel formuläret baserat på kalkylbladet [för förfrågan](/help/edge/assets/enquiry-form.docx):


   ![Ett exempel på EDS-formulär](/help/edge/assets/updated-form.png)

1. Använd AEM Sidekick för att publicera formuläret. Nu kan kunderna fylla i formuläret och skicka in det.

+++

## Felsökning

+++ Det går inte att skicka data till formuläret

Om du råkar ut för ett fel som påminner om följande meddelande anger det att kalkylbladet inte har konfigurerats för att [acceptera skickade](/help/edge/docs/forms/submit-forms.md)-data än.

![fel vid formuläröverföring](/help/edge/assets/form-error.png)

+++



