---
title: Dataskydd och dataintegritet - AEM Sites beredskap
description: Läs om Experience Manager as a Cloud Service Sites support for the various Data Protection and Data Privacy Regulations, including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to compliance when implementation a new AEM as a Cloud Service project.
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
feature: Compliance
role: Admin, Architect, Developer, Leader
source-git-commit: 974f85b91a629ea6d4f34e2066d242c42a04015b
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# Experience Manager Sites beredskap för dataskydd och sekretess {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Innehållet i detta dokument utgör inte juridisk rådgivning och är inte avsett som ersättning för juridisk rådgivning.
>
>Kontakta företagets juridiska avdelning för råd om dataskydd och dataintegritet.

>[!NOTE]
>
>Mer information om Adobe svar på sekretessfrågor och vad detta innebär för dig som Adobe-kund finns i [Adobe Sekretesscenter](https://www.adobe.com/privacy.html).

Adobe Experience Manager as a Cloud Service Sites är redo att hjälpa kunderna med deras skyldigheter vad gäller datasekretess och skydd. På den här sidan får kunderna hjälp med hur de hanterar sådana förfrågningar i AEM Sites. Den beskriver platsen för privata data som lagras och hur du tar bort dem manuellt eller med kod.

Mer information finns i [Adobe Sekretesscenter](https://www.adobe.com/privacy.html).

>[!NOTE]
>
>Mer information finns i [Adobe Experience Manager as a Cloud Service beredskap för dataskydd och sekretesspolicyer](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md).

## AEM-redigeringsnivå {#aem-author-tier}

Användarkonton och UGC-innehåll på författarservern beskrivs i [AEM Foundation-dokumentationen](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## AEM-publiceringsnivå {#aem-publish-tier}

Användarkonton som används för att autentisera besökare på webbplatsen och UGC-innehåll på publiceringsservern beskrivs i [AEM Foundation-dokumentationen](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md).

Som standard lagrar inte AEM Sites-komponenter formulärdata som anges av besökare på publiceringsservern. Vi rekommenderar att du vidarebefordrar data till ett tredjepartssystem eller Adobe Campaign för vidare bearbetning.

## Opt-In/Opt-Out {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager omfattas av en anmälningstjänst för cookies som används för att hantera anmälan/avanmälan för användare.

Så här avanmäler du:

1. Navigera till:
   [Adobe Sekretesscenter - avanmäl dig](https://www.adobe.com/privacy/opt-out.html)

1. Bläddra ned till **Tjänster** - **Experience Cloud tjänstanvändningsdata**.

1. Markera den refererade länken, som för närvarande heter **här**.

1. Du får följande information tillsammans med alternativen för att avanmäla dig eller i:

   * Om du vill avanmäla dig från aggregering och analys av data om ditt besök på webbplatsen måste du installera en cookie i webbläsaren. Den här cookien identifierar att du har avanmält dig.

     Om du tar bort cookien för anmälan eller om du byter dator eller webbläsare måste du avanmäla dig igen.

     Avanmäl dig - Uteslut mig från sessionsaggregering och analys för besökare (installera cookie för `amcglobal.sc.omtrdc.net` avanmälan) - Klicka här.

     Opt-in - Inkludera mig i sessionsaggregering och analys för besökare (installera inte cookie för `amcglobal.sc.omtrdc.net` opt-out) - klicka här.

   Följ stegen ovan för att komma åt de faktiska länkarna.

   >[!NOTE]
   >
   > Det finns ytterligare en beskrivning i **2. Integritet.** i [Adobe allmänna användningsvillkor](https://www.adobe.com/legal/terms.html).

## Analytics Foundation {#analytics-foundation}

AEM Sites innehåller en valfri integrering med Analytics Foundation som använder funktioner i Adobe Analytics On-Demand Service.

Mer information om hur du hanterar förfrågningar från registrerade personer relaterade till Adobe Analytics finns i [Adobe Analytics och Dataintegritet](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html?lang=sv-SE).

## Personalization Foundation by Target {#personalization-foundation-by-target}

AEM Sites innehåller en valfri integrering med Personalization Foundation by Target som använder funktioner i Adobe Target On-Demand Service.

Mer information om hur du hanterar förfrågningar från registrerade personer relaterade till Adobe Target finns i [Adobe Target - Sekretess och allmänna dataskyddsförordningen](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=sv-SE).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM tillhandahåller ett valfritt datalager med ContextHub. På så sätt behålls besökarspecifika data i webbläsaren som ska användas för regelbaserad personalisering.

Som standard lagras inte dessa besökardata i AEM. AEM skickar regler till datalagret för att fatta personaliseringsbeslut i webbläsaren.

### Implementera anmälan/avanmälan {#implementing-opt-in-opt-out}

Webbplatsägaren måste implementera en avanmälningskomponent enligt följande riktlinjer.

I dessa riktlinjer används anmälan som standard. Därför måste en besökare på webbplatsen tydligt hålla med om detta innan några personuppgifter lagras i webbläsarens (klientsidan) beständighet.

* Avanmälningskomponenten ska inkluderas varje gång ContextHub-komponenten inkluderas.
* De villkor som rör dataskydd och integritet för webbplatsen måste visas för besökaren på webbplatsen så att de kan

   * acceptera
   * avvisa
   * ändra sitt föregående val

* Om en besökare godkänner villkoren för webbplatsen bör cookien för ContextHub-avanmälan tas bort:

  ```
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* Om en besökare inte accepterar webbplatsens villkor ska cookie för ContextHub-avanmälan anges:

  ```
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* För att kontrollera om ContextHub körs i avanmälningsläge bör följande anrop göras i webbläsarens konsol:

  ```
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### Förhandsgranska Persistence för ContextHub {#previewing-persistence-of-contexthub}

Om du vill förhandsgranska den beständiga ContextHub som används kan användaren:

* Använd webbläsarens konsol, till exempel:

   * Chrome:

      * Öppna Utvecklarverktyg > Program > Lagring:

         * Lokal lagring > (webbplats) > ContextHubPersistence
         * Sessionslagring > (webbplats) > ContextHubPersistence
         * Cookies > (website) > SessionPersistence

   * Firefox:

      * Öppna Utvecklarverktyg > Lagring:

         * Lokal lagring > (webbplats) > ContextHubPersistence
         * Sessionslagring > (webbplats) > ContextHubPersistence
         * Cookies > (website) > SessionPersistence

   * Safari:

      * Öppna Inställningar > Avancerat > Visa menyn Framkalla i menyraden
      * Öppna Framkalla > Visa JavaScript Console

         * Konsol > Lagring > Lokal lagring > (webbplats) > ContextHubPersistence
         * Konsol > Lagring > Sessionslagring > (webbplats) > ContextHubPersistence
         * Konsol > Lagring > Cookies > (webbplats) > ContextHubPersistence

   * Internet Explorer:

      * Öppna Utvecklarverktyg > Konsol

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`

* Använd ContextHub-API:t i webbläsarens konsol:

   * ContextHub tillhandahåller följande beständiga datalager:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (standard)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

     ContextHub-arkivet definierar vilket beständigt lager som används, och för att visa det aktuella läget för beständigheten bör alla lager kontrolleras.

Så här visar du data som lagras i localStorage:

Om du vill förhandsgranska den beständiga ContextHub som används kan användaren:

* Använd webbläsarens konsol:

   * Chrome - öppna Developer Tools > Application > Storage:

      * Lokal lagring > (webbplats) > ContextHubPersistence
      * Sessionslagring > (webbplats) > ContextHubPersistence
      * Cookies > (website) > SessionPersistence

   * Firefox - öppna Utvecklarverktyg > Lagring:

      * Lokal lagring > (webbplats) > ContextHubPersistence
      * Sessionslagring > (webbplats) > ContextHubPersistence
      * Cookies > (website) > SessionPersistence

* Använd ContextHub-API:t i webbläsarens konsol:

   * ContextHub tillhandahåller följande beständiga datalager:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (standard)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

     ContextHub-arkivet definierar vilket beständigt lager som används, och för att visa det aktuella läget för beständigheten bör alla lager kontrolleras.

Så här visar du data som lagras i localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Rensar Persistence för ContextHub {#clearing-persistence-of-contexthub}

Så här rensar du ContextHub-beständighet:

* Så här rensar du beständighet för inlästa arkiv:

  ```
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* Så här rensar du ett visst beständigt lager, till exempel sessionStorage:

  ```
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* Om du vill ta bort alla ContextHub-beständiga lager måste rätt kod anropas för alla lager:

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (standard)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
