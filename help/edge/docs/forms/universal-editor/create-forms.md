---
title: Skapa och publicera adaptiva Forms med Edge Delivery Services
description: Stegvisa instruktioner för att skapa, skriva och publicera adaptiva Forms med hjälp av mallar i Core Component eller Edge Delivery Services i AEM, med fokus på teknisk precision och tydlighet.
keywords: adaptiva blanketter, edge delivery services, core components, universal editor, form creation, AEM forms, template selection, form publishing
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---


# Skapa och publicera adaptiva Forms med Edge Delivery Services

Det här dokumentet innehåller anvisningar om hur du skapar, konfigurerar och publicerar Adaptive Forms i AEM med Edge Delivery Services. Det omfattar Core Component- och Edge Delivery Services-mallar.

I slutet av guiden får du lära dig att:

- Välj lämplig malltyp för ditt användningsfall
- Skapa formulär med hjälp av grundkomponenter eller Edge Delivery Services-mallar
- Skapa formulär med rätt redigerare
- Konfigurera och publicera formulär till Edge Delivery Services
- Få åtkomst till publicerade formulär och verifiera distributionen

## Mallval

Innan du börjar ska du avgöra vilken malltyp som passar dina krav:

| Kriterier | Kärnkomponentmall | Edge Delivery Services-mall |
|-------------------------|-----------------------------------------|-------------------------------------|
| Bäst för | Företagsarbetsflöden, komplexa integreringar | Högpresterande offentliga blanketter |
| Redigerare | Adaptiv Forms Editor | Universal Editor |
| Publicering | AEM Publish + Edge Delivery Services | Endast Edge Delivery Services |
| Komplex | Avancerade blankettfunktioner | Effektiva, snabba formulär |
| Integrering | Fullständigt AEM-ekosystem | Git-baserad utveckling |
| Inlärningskurva | Välbekant för AEM | Modernt, förenklat tillvägagångssätt |

**Vägledning för beslut:**

- Använd **kärnkomponenter** för komplexa arbetsflöden, djup AEM-integrering eller om du vill utnyttja befintliga AEM-resurser.
- Använd **Edge Delivery Services** för prestanda, enkelhet och moderna utvecklingsmetoder.

![Beslut om mallval](/help/edge/docs/forms/universal-editor/assets/template-selection-decision.svg)
*Beslutsflödesschema för val av lämplig malltyp*

## Förutsättningar

Kontrollera att följande krav är uppfyllda innan du fortsätter:

### Tekniska krav

- **AEM Forms as a Cloud Service**: En aktiv författarinstans med en Forms-licens.
- **GitHub-konto**: Personligt eller organisatoriskt konto för databashantering.
- **Databasinställningar**: Välj något av följande:
   - **Nytt projekt**: [Skapa ett nytt AEM-projekt med Adaptivt Forms-block](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block). Databasen är förkonfigurerad för Edge Delivery Services.
   - **Befintligt projekt**: [Lägg till anpassat Forms-block i en befintlig databas](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) och uppdatera konfigurationen.

### Miljökonfiguration

- **AEM-GitHub-anslutning**: [Upprätta en anslutning](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) mellan din AEM-instans och GitHub-databasen.
- **Edge Delivery Services**: Kontrollera att databasen har konfigurerats för automatisk distribution.
- **Behörigheter**: Kontrollera att du har de nödvändiga åtkomstbehörigheterna för att skapa och publicera formulär.

### Konfigurera validering


1. Bekräfta att GitHub-databasen innehåller det adaptiva Forms-blocket.
2. Testa anslutningen mellan AEM och din GitHub-databas.
3. Se till att du kan publicera innehåll på Edge Delivery Services.



## Arbetsflöde för att skapa och publicera formulär

Processen består av tre huvudfaser:

- **Fas 1:** [Mallval och skapande av formulär](#step-1-template-selection-and-form-creation)
- **Fas 2:** [Skapa och utforma formulär](#step-2-form-authoring-and-design)
- **Fas 3:** [Konfiguration och publicering](#step-3-configuration-and-publishing)

I varje fas finns valideringssteg som bekräftar korrekt konfiguration.

![Arbetsflöde för tre faser](/help/edge/docs/forms/universal-editor/assets/three-phase-workflow.svg)
*Översikt över de tre huvudsakliga faserna för att skapa och publicera formulär*

### Steg 1: Välj mall och skapa formulär

Välj arbetsflöde baserat på mallval:

>[!BEGINTABS]

>[!TAB Edge Delivery Services-mall]

**Använd skiftläge:** Högpresterande formulär och moderna utvecklingsarbetsflöden.

**Funktioner:** Universell redigerare och Edge Delivery Services-publicering.

#### Förfarande

1. **Skapa formulär för åtkomst**
   - Logga in på din AEM Forms as a Cloud Service-författarinstans.
   - Navigera till **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
   - Klicka på **Skapa** > **Adaptiv Forms**.

1. **Välj mall**
   - På fliken **Source** väljer du en **Edge Delivery Services-baserad mall**.
   - Knappen **Skapa** aktiveras.

     ![Skapa EDS Forms](/help/edge/assets/create-eds-forms.png)

1. **Konfigurera alternativ (valfritt)**
   - **Source-fliken Data**: Välj dataintegrering om det behövs.
   - **fliken Skicka**: Välj en skicka-åtgärd (kan konfigureras senare).
   - **Leveransflik**: Ange publicerings-/avpubliceringsschema.

1. **Slutför formulärinställning**
   - Klicka på **Skapa** för att öppna guiden Skapa formulär.
   - Ange följande:
      - **Namn**: Intern identifierare (inga blanksteg, använd bindestreck).
      - **Titel**: Formulärets visningsnamn.
      - **GitHub-URL**: Databas-URL (t.ex. `https://github.com/your-org/your-repo`).

   ![Guiden Skapa formulär](/help/edge/assets/create-form-wizard.png)

1. **Validering**
   - När du har klickat på **Skapa**, verifiera:
      - Formuläret öppnas i Universal Editor.
      - GitHub-URL:en är korrekt länkad.
      - Komponentpaletten är tillgänglig.
      - Formulärets arbetsyta är synlig.

   ![Universellt redigeringsgränssnitt](/help/edge/assets/author-form.png)

**Resultat:** Formuläret är klart för redigering i den universella redigeraren.

>[!TAB Kärnkomponentmall]

**Användningsfall:** Företagsarbetsflöden och komplexa integreringar.

**Funktioner:** Adaptiv redigering av Forms-program, dubbel publicering (AEM + Edge Delivery Services), avancerade formulärfunktioner.

#### Förfarande

1. **Skapa formulär för åtkomst**
   - Logga in på din AEM Forms as a Cloud Service-författarinstans.
   - Navigera till **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
   - Klicka på **Skapa** > **Adaptiv Forms**.

1. **Välj mall och tema**
   - På fliken **Source** väljer du en **Core Component-baserad mall**.
   - Välj ett **tema** för formatering.
   - Knappen **Skapa** aktiveras.

   ![Val av kärnkomponentmall](/help/forms/assets/core-component-based-template.png)

1. **Konfigurera alternativ (valfritt)**
   - **Source-fliken Data**: Välj dataintegrering om det behövs.
   - **fliken Skicka**: Välj en skicka-åtgärd (kan konfigureras senare).
   - **Leveransflik**: Ange publicerings-/avpubliceringsschema.

1. **Slutför formulärinställning**
   - Klicka på **Skapa** för att öppna guiden Skapa formulär.
   - Ange följande:
      - **Namn**: Intern identifierare (inga blanksteg, använd bindestreck).
      - **Titel**: Formulärets visningsnamn.
      - **Sökväg**: Lagringsplats i AEM-databasen.

     ![Guiden Skapa formulär](/help/forms/assets/create-cc-form.png)

1. **Validering**
   - När du har klickat på **Skapa**, verifiera:
      - Formuläret öppnas i Adaptiv Forms Editor.
      - Komponentverktygsfältet är tillgängligt.
      - Egenskapspanelen är tillgänglig.
      - Temamallen används.

     ![Adaptiv formulärredigerare](/help/forms/assets/af-editor-form.png)

**Resultat:** Formuläret kan redigeras i den adaptiva Forms-redigeraren.

>[!ENDTABS]

### Steg 2: Skapa och utforma formulär

Redigeringsupplevelsen varierar beroende på mall:

- **Edge Delivery Services-mall**: Universell redigerare
- **Kärnkomponentmall**: Adaptiv Forms-redigerare

![Jämförelse av redigerare](/help/edge/docs/forms/universal-editor/assets/editor-comparison.svg)
*Jämförelse mellan funktionerna i Universal Editor och Adaptive Forms Editor*

>[!BEGINTABS]

>[!TAB Universell redigerare (Edge Delivery Services)]

**Gränssnitt:** Modern, smidig redigering som är optimerad för prestanda.

#### Lägg till formulärkomponenter

1. **Access Component Library**
   - Öppna innehållsläsaren i Universal Editor.
   - Navigera till komponenten **Adaptiv form** i innehållsträdet.

   ![Navigering i innehållsträd](/help/edge/assets/content-tree.png)

1. **Lägg till formulärfält**
   - Klicka på ikonen **Lägg till** för att öppna komponentbiblioteket.
   - Välj komponenter i listan **Adaptiva formulärkomponenter**.
   - Dra och släpp komponenter på arbetsytan.

   ![Lägg till komponenter](/help/edge/assets/add-component.png)

1. **Designa formuläret**
   - Konfigurera fältegenskaper i egenskapspanelen.
   - Ange verifieringsregler och -beteenden.
*s Justera format och layout efter behov.

   ![Registreringsformuläret har slutförts](/help/edge/assets/contact-us.png)

#### Validering

- Alla obligatoriska fält finns.
- Fältegenskaperna är korrekt konfigurerade.
- Layouten är responsiv och tillgänglig.
- Valideringsregler fungerar som förväntat.

#### Nästa steg

- [Konfigurera överföringsåtgärder](/help/edge/docs/forms/universal-editor/submit-action.md) för datahantering.
- [Guide för universell redigering](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) för avancerade funktioner.

>[!TAB Adaptiv Forms Editor (kärnkomponenter)]

**Gränssnitt:** Fullständig redigering med avancerade formulärfunktioner.

#### Lägg till formulärkomponenter

1. **Access Component Library**
   - Klicka på **Infoga komponent** i avsnittet **Dra komponenter hit**.

   ![Komponentinsättningsområde](/help/forms/assets/drag-components-af-editor.png)

2. **Lägg till formulärfält**
   - Bläddra i listan **Adaptiva formulärkomponenter**.
   - Dra önskade komponenter till formuläret.
   - Använd avancerade komponenter som paneler, guider och dataintegreringar.

   ![Lägg till komponentbibliotek](/help/forms/assets/add-component-af.png)

3. **Designa formuläret**
   - Konfigurera fältegenskaper i egenskapspanelen.
   - Ange komplexa valideringsregler och affärslogik.
   - Använd teman och avancerad formatering.

   ![Registreringsformuläret har slutförts](/help/forms/assets/af-editor-form.png)

#### Validering

- Alla obligatoriska fält finns.
- Komplexa valideringsregler har konfigurerats.
- Temamallen används.
- Dataintegrering fungerar som avsett (om tillämpligt).

#### Nästa steg

- [Konfigurera skicka-åtgärder](/help/forms/configure-submit-actions-core-components.md) för avancerade arbetsflöden.
- [Guide för kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md) för företagsfunktioner.

>[!ENDTABS]

### Steg 3: Konfiguration och publicering

Konfigurera Edge Delivery Services och publicera formuläret. Processen skiljer sig åt efter malltyp.

#### Edge Delivery Services Configuration

>[!BEGINTABS]
>[!TAB Edge Delivery Services-mall (automatisk)]

**Konfiguration:** Automatisk (ingen manuell konfiguration krävs).

- GitHub-databasanslutningen och Edge Delivery Services-konfigurationen skapas när formulär skapas.
- Publiceringsslutpunkter konfigureras automatiskt.

**Verifiering:**

- Bekräfta att konfigurationen visas i formulärets inställningar.
- Kontrollera att GitHub-URL:en är korrekt länkad.

![Automatisk EDS-konfiguration](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB Kärnkomponentmall (manuell)]

**Konfiguration:** Manuell konfiguration krävs.

#### Manuella konfigurationssteg

1. **Åtkomstkonfigurationsverktyg**
   - Navigera till **Verktyg** > **Molntjänster** > **Edge Delivery Services Configuration**.

   ![EDS-konfigurationsåtkomst](/help/edge/assets/select-eds-conf.png)

1. **Skapa konfiguration**
   - Välj den mapp som matchar formulärets namn (t.ex. `forms/enrollment-form`).
   - Klicka på **Skapa** > **Konfiguration**.

   ![Skapa EDS-konfiguration](/help/forms/assets/create-eds-conf.png)

1. **Konfigurera egenskaper**
   - Klicka på **Edge Delivery Services Configuration**.
   - Välj **Egenskaper** för att öppna konfigurationsdialogrutan.

   ![Konfigurationsegenskaper](/help/forms/assets/eds-conf.png)

1. **Ange parametrar**
   - **Obligatoriskt:**
      - **Organisation**: GitHub-organisationsnamn.
      - **Platsnamn**: GitHub-databasnamn.
      - **Förgrening**: Förgreningsnamn (lämna tomt för huvudgrenen).
   - **Valfritt:**
      - **Edge-värd**: Standard (publicerar till både .page och .live).
      - **Webbplatsautentiseringstoken**: För säker autentisering (om det behövs).

1. **Spara konfiguration**
   - Klicka på **Spara och stäng**.

#### Validering

- Konfigurationen har skapats.
- GitHub-organisationen och -databasen har angetts korrekt.
- Förgreningsinställningarna matchar databasstrukturen.
- Formuläret visas i konfigurationsmappen.

>[!ENDTABS]

#### Publicera formuläret

>[!BEGINTABS]
>[!TAB Universal Editor Publishing]

**För Edge Delivery Services-mallar**

1. Klicka på knappen **Publicera** (övre högra hörnet) i Universellt redigeringsprogram.
2. Bekräfta publiceringen i dialogrutan.
3. Observera de URL:er som genereras för testversionerna och liveversionerna.

   ![Universal Editor Publish](/help/edge/assets/publish-form.png)

- [Publiceringshandbok](/help/edge/docs/forms/universal-editor/publish-forms.md)

>[!TAB Adaptiv publicering av Forms Editor]

1. På Experience Manager Forms-konsolen väljer du det formulär som ska publiceras.
2. Klicka på **[!UICONTROL Publish]** i verktygsfältet. Granska referensresurser som ska publiceras.

![Publicera formulär i anpassad formulärredigerare](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> Mer information finns i [Hantera publikation i Experience Manager Forms](/help/forms/manage-publication.md).

>[!ENDTABS]

## Formulär-URL

Publicerade formulär är tillgängliga via Edge Delivery Services URL:er.

### URL-struktur

- **Mellanlagrad (förhandsgranskning/testning):**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **Live (produktion):**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### URL-parametrar

- `<branch>`: GitHub-förgreningsnamn (t.ex. `main`, `develop`)
- `<repo>`: GitHub-databasnamn (t.ex. `my-forms-project`)
- `<owner>`: GitHub-organisation eller användarnamn (t.ex. `company-name`)
- `<form_name>`: Formuläridentifierare enligt definition i AEM (t.ex. `contact-us`)

#### Exempel

Exempel för formuläret `contact-us` i databasen `forms-project` under organisationen `acme-corp`:

- **Mellanlagrad:** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **Live:** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### Miljöskillnader

- **Mellanlagrad (.page):** De senaste ändringarna för testning.
- **Live (.live):** Publicerat innehåll för produktion.

![URL-struktur](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Uppdelning av Edge Delivery Services formulär-URL:er*

#### Visuella exempel

**Edge Delivery Services-mall:**

- Mellanlagrad: ![Registreringsformulär av mellanlagrad version](/help/forms/assets/registration-form-staged-version.png)
- Live: ![Live-version för registreringsformulär](/help/forms/assets/registration-form-live-version.png)

**Kärnkomponentmall:**

- Mellanlagrad: ![Registreringsformulär med mellanlagrad version](/help/forms/assets/enrollment-form-staged-version.png)
- Live: ![Live-version för anmälningsformulär](/help/forms/assets/enrollment-form-live-version.png)

## Felsökning

Nedan beskrivs vanliga problem och lösningar för AEM Forms med Edge Delivery Services.

+++Formuläret läses inte in

**Problem:** Formulär-URL returnerar 404 eller en tom sida.

**Upplösning:**

- Ta bort tillägget `.html` från URL:er.
- Kontrollera att formuläret är publicerat.
- Kontrollera GitHub-databasen för det adaptiva Forms-blocket.
- Kontrollera att formulärnamnet matchar URL:en (skiftlägeskänslig).

+++

+++Konfigurationsproblem

**Problem:** Edge Delivery Services-konfigurationen fungerar inte.

**Upplösning:**

- Kontrollera att GitHub-URL:en har formatet `https://github.com/owner/repository`.
- Använd rätt förgreningsnamn i konfigurationen.
- Verifiera databasåtkomst (offentlig eller autentiserad).
- Kontrollera `fstab.yaml` för korrekt GitHub-information.

+++

+++Publiceringsproblem

**Problem:** Ändringar visas inte på den publicerade webbplatsen.

**Upplösning:**

- Vänta 2-3 minuter tills CDN-cachen har uppdaterats.
- Bekräfta att publiceringsarbetsflödet har slutförts.
- Testa först i den mellanlagrade miljön (.page).
- Kontrollera att GitHub-databasen har uppdaterats.

+++

+++Universal Editor Issues

**Problem:** Det går inte att redigera formulär eller komponenter som inte läses in.

**Upplösning:**

- Använd en webbläsare som stöds (Chrome, Firefox, Safari).
- Rensa webbläsarcachen och cookies.
- Verifiera nätverksanslutningen.
- Bekräfta författarbehörighet.

+++

+++Formuläröverföringsfel

**Problem:** Formuläröverföringar fungerar inte.

**Upplösning:**

- Konfigurera skicka-åtgärden i formuläregenskaperna.
- Testa slutpunkterna för överföring manuellt.
- Kontrollera CORS-inställningarna om du bäddar in formulär.
- Kontrollera att obligatoriska fält har konfigurerats.

+++

+++Prestandaproblem

**Problem:** Långsam formulärinläsning eller dålig prestanda.

**Upplösning:**

- Optimera bilder.
- Ta bort onödiga komponenter.
- Utnyttja Edge Delivery Services CDN.
- Minimera anpassade JavaScript/CSS.

+++

+++Komma åt hjälp

Om problemen kvarstår:

1. Kontrollera status för Adobe Experience Cloud-tjänst.
2. Granska [Edge Delivery Services-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=sv-SE).
3. Besök [Adobe Experience League Community](https://experienceleaguecommunities.adobe.com/).
4. Kontakta Adobe kundtjänst.

+++

## Nästa steg

När du är klar med formulärframtagningen och publiceringen bör du tänka på följande:

### Omedelbara åtgärder

- Testa formuläret med den här guiden.
- Validera din GitHub-databas och AEM-anslutning.
- Granska exempelformulär.

### Avancerade ämnen

- [Konfigurera överföringsåtgärder](/help/edge/docs/forms/universal-editor/submit-action.md): Konfigurera datahantering och integreringar.
- [Formulärdatamodeller](/help/forms/create-form-data-models.md): Koppla formulär till backend-datakällor.

### Prestandaoptimering

- [Edge Delivery Services bästa praxis](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=sv-SE): Maximera prestanda.
- [Formuläranalys](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html): Spåra formulärprestanda och användarbeteende.

