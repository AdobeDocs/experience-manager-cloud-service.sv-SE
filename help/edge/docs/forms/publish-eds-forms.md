---
title: Publicera ett AEM Forms-formulär för Edge Delivery Services
description: Publicera ett AEM Forms-formulär för Edge Delivery Services
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 39bb45b285fcd938d44b9748aa8559b89a3636b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Publicera formuläret

När du är redo att dela formuläret med dina kunder för datainsamling eller insändning kan du helt enkelt publicera det, så att formuläret blir lätt tillgängligt för kunderna.

## Krav

* The [Formulärblocket är aktiverat för ditt EDS-projekt på Github](/help/edge/docs/forms/create-forms.md).
* Formuläret är fullständigt testat och klart att användas.
* Dina [kalkylbladet har konfigurerats](/help/edge/docs/forms/submit-forms.md) för att ta emot data.

## Publicera formuläret

Så här publicerar du formuläret:

1. Gå till ditt Microsoft SharePoint- eller Google Drive-konto och navigera till ditt `[AEM Edge Delivery project directory]`.

1. Öppna en dokumentfil där du vill bädda in formuläret. Du kan till exempel öppna indexfilen eller skapa ett nytt dokument.

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

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska sidan. Formuläret visas nu på sidan. Här är till exempel formuläret baserat på [frågekalkylblad](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Ett exempel på ett EDS-formulär](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   Nu kan kunderna fylla i formuläret och skicka in det.

## Felsökning

+++ Det går inte att skicka data till formuläret

Om du råkar ut för ett fel som påminner om följande meddelande, indikerar det att kalkylbladet inte har konfigurerats för att ta emot skickade data än.

![fel vid inlämning av formulär](/help/edge/assets/form-error.png)

+++


## Se mer

* [Skapa och förhandsgranska ett formulär](/help/edge/docs/forms/create-forms.md)
* [Aktivera formulär för att skicka data](/help/edge/docs/forms/submit-forms.md)
* [Publicera ett formulär på webbplatssidan](/help/edge/docs/forms/publish-eds-forms.md)
* [Lägga till valideringar i formulärfält](/help/edge/docs/forms/validate-forms.md)
* [Ändra teman och format för formulär](/help/edge/docs/forms/style-theme-forms.md)
