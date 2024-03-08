---
title: Publicera ett AEM Forms-formulär för Edge Delivery Services
description: Publicera ett AEM Forms-formulär för Edge Delivery Services
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Publicera formuläret

När du är redo att dela formuläret med dina kunder för datainsamling eller insändning kan du helt enkelt publicera det, så att formuläret blir lätt tillgängligt för kunderna.

![Dokumentbaserat redigeringssystem](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Krav

* The [Adaptivt formulärblock är aktiverat för ditt EDS-projekt på GitHub](/help/edge/docs/forms/create-forms.md).
* Formuläret är fullständigt testat och klart att användas.
* Dina [kalkylbladet har konfigurerats](/help/edge/docs/forms/submit-forms.md) för att ta emot data.

## Publicera formuläret

+++ 1. Publicera kalkylbladet

1. Öppna ditt Microsoft SharePoint- eller Google Drive-konto och gå till AEM Edge Delivery-projektkatalog.

1. Öppna det kalkylblad som innehåller ditt formulär. Till exempel `enquiry` från Microsoft Excel-arbetsbok.

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) om du vill förhandsgranska bladet.

   ![Använd AEM Sidekick för att förhandsgranska bladet](/help/edge/assets/preview-form.png)

   När förhandsgranskningen har slutförts konverteras kalkylbladsinnehållet till JSON-format. Förhandsgranskningssidan visar sedan innehållet i ett strukturerat tabellformat. Till exempel illustrerar den medföljande bilden innehållet i ett frågeformulär.

   ![Forms Preview JSON-format](/help/edge/assets/forms-preview-json-format.png)

1. Använd AEM Sidekick för att publicera bladet. Se till att du hämtar publicerings-URL:en, eftersom detta krävs för att återge formuläret i nästa avsnitt. URL-formatet är följande:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` refererar till grenen i din GitHub-databas.
   * `<repository>` anger din GitHub-databas.
   * `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.

   Om projektets databas till exempel heter &quot;portal&quot;, finns den under kontot &quot;wkndforms&quot; och du använder huvudgrenen, ser URL:en ut så här:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2. Lägg till formuläret på din webbsida

Lägg till `<form>.json` till en webbsida för att underlätta kundernas interaktion, så att de som fyller i formulären enkelt kan fylla i och skicka in dem.


Så här lägger du till formuläret på din webbsida:

1. Gå till ditt Microsoft SharePoint- eller Google Drive-konto och navigera till ditt `[AEM Edge Delivery project directory]`.

1. Öppna en dokumentfil där du vill bädda in formuläret. Du kan till exempel öppna `index.docx` eller skapa ett nytt dokument.

1. Identifiera det önskade avsnittet i dokumentet där du vill infoga formuläret och navigera sedan till det.

1. Lägg till ett block med namnet &#39;Form&#39; i filen, som i exemplet nedan:

   | Formulär |
   |---|
   | [https://main—portal—wkndforms.hlx.live/inquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   Det här blocket fungerar som en platshållare där formuläret är inbäddat. Lägg till URL:en för `<form>.json` som en hyperlänk.

   >[!IMPORTANT]
   >
   >
   > Kontrollera att URL-adressen är formaterad som en hyperlänk i stället för att visas som oformaterad text.

   Använd URL:en för förhandsgranskning (.page URL) för utvecklings- eller teständamål, eller publicerings-URL:en (.live) för produktion. Här är några exempel på förhandsgransknings- och publicerings-URL:

   **Förhandsgranska URL**
| Formulär | |—| | [https://main—portal—wkndforms.hlx.page/inquiry.json](https://main--portal--wkndforms.hlx.page/enquiry.json)  |


   **Publicera URL**
| Formulär | |—| | [https://main—portal—wkndforms.hlx.live/inquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json)  |

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska webbsidan. Formuläret visas nu på sidan. Här är till exempel formuläret baserat på [frågekalkylblad](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Ett exempel på ett EDS-formulär](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

1. Använd AEM Sidekick för att publicera formuläret. Nu kan kunderna fylla i formuläret och skicka in det.

+++

## Felsökning

+++ Det går inte att skicka data till formuläret

Om du råkar ut för ett fel som påminner om följande meddelande anger det att kalkylbladet inte är konfigurerat till [acceptera inskickade](/help/edge/docs/forms/submit-forms.md) ännu.

![fel vid inlämning av formulär](/help/edge/assets/form-error.png)

+++




## Se mer
