---
title: Hur kan man aktivera Adobe Analytics för snabb spåranalys av ett adaptivt formulär?
description: Experience Cloud Setup Automation kan koppla Adobe Analytics till ett adaptivt formulär för att få snabba analyser och insikter om besökarinteraktioner och -engagemang.
keywords: Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation, Enable Adobe Analytics in Forms, Adobe Analytics in Adaptive Forms, Forms analytics integration, Forms and Adobe Analytics
feature: Adaptive Forms
role: Admin, User
exl-id: 0e1aa040-08b4-4c1a-b247-ad6fff410187
source-git-commit: 56a3d50d7cc8db532097b97f0898f87fc6ba0b3d
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

>[!CAUTION]
>
>Experience Cloud Setup Automation-funktionen är föråldrad.

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Den här artikeln |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html?lang=sv-SE) |

Experience Cloud Setup Automation hjälper till att koppla Adobe Analytics till Adaptive Forms, som hjälper till att snabbt analysera användarinteraktionen med era formulär och ger insikter i besökarinteraktioner och -engagemang. Experience Cloud Setup Automation hjälper dig också att övervaka formulärprestanda genom att utvärdera mätvärden som slutförandetider och bortfallspunkter. Denna analys hjälper till att optimera formulär för att ge en bättre användarupplevelse och särskilja användarbeteenden baserat på inloggningsstatus, t.ex. anonyma användare, för att identifiera allmänna trender och mönster.

## Fördelar med att integrera Adobe Analytics med Adaptive Forms {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **Insikter i slutanvändarnas beteende**: Adobe Analytics hjälper till att få insikter i slutanvändarnas beteende, avslöjar användaråtgärder, bortfall och slutförandefrekvens, vilket ger en djupare förståelse för hur individer interagerar med formulär.
* **Möjliggör för icke-tekniska affärsanvändare att få insikter**: Adobe Analytics genom sitt lättanvända gränssnitt ger även icke-tekniska användare möjlighet att få åtkomst till och tolka formuläranvändningsdata, vilket främjar datadrivna beslut för att förbättra registreringsupplevelsen.
* **Optimera datainhämtningen baserat på användning**: Organisationer kan enkelt identifiera problem vid datainhämtning, vilket leder till målinriktade förbättringar som förbättrar formuläranvändbarheten och ökar antalet lyckade inskickade data.

## Omfattning av anpassade användningsmått för Forms {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics har en omfattande uppsättning av adaptiva Forms-prestandamätningar som utformats för att ge värdefulla insikter om formuläranvändning och erbjuder snabba analysverktyg. Dessa mått är:

* **Formuläråtergivningar, formulärinskickningar, valideringsfel och unika besökare** som gör att du kan bedöma hur användbara och effektiva dina formulär är.

* **Besökarinsikter** som omfattar besöks- och överföringsfrekvenser och unika besökarantal, vilket ger en heltäckande bild av formulärens målgrupp.

* **Enhetstyp** data som informerar dig om vilka enheter som användarna använder för att komma åt formulären.

* **Geografisk fördelning** visar den regionala fördelningen för formuläranvändarna.

* **Trafikkällor** och **Populära formulärvärden** som består av de mest refererande domänerna och de mest besökta formulären hjälper dig att förstå var trafiken kommer ifrån och vilka formulär som är de mest populära.

* **Användaraktivitet på de vanligaste formulären** ger insikter om fältbesök, formuläråtergivningar, valideringsfel, övergivna formulär och formulärinskickade formulär, så att du kan analysera användarens beteende.

* **Tidslinje för den tid som läggs på formulär** som ger en tidslinjebaserad vy över användarinteraktionen med formulären.

* **Områden som kräver besökarhjälp**, som innehåller hjälpvyer, valideringsfelinstanser och frekvenser för fältbesök, där användarna kan behöva hjälp med att fylla i formulär.

![Analysrapport](assets/analytics-report.png){width="100%"}


Mer information om varje mätvärde finns på [Visa och förstå AEM Forms Analytics-rapporter](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Förutsättningar {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud Setup Automation kräver en **Adobe Analytics-licens**, **datainsamling (tidigare Adobe Launch)** för att hantera spårningsskript, och en **Experience Manager Forms-licens** för smidig datainsamling och insikterna.

Om du har en aktiv licens för **Adobe Analytics** och **Experience Manager Forms**, och du har integrering med **Datainsamling (tidigare Adobe Launch)**, bör du verifiera deras tillgänglighet i din utvecklarkonsol.

Om du vill verifiera att ovanstående är tillgängligt för din Forms as a Cloud Service-miljö går du till [utvecklarkonsolen](https://developer.adobe.com/console/projects), går till projektet och söker efter ditt projekt med program-ID:t - program-ID:t, till exempel för miljön med URL:en `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, program-ID:t för miljön är `p45913-e175111`. Kontrollera att API:t för Experience Cloud Setup Automation, Adobe Analytics och Experience Platform Launch finns med i listan. Om de listas kan du aktivera Adobe Analytics för att få en snabb spåranalys av din adaptiva Forms.

![Nödvändig integrering med Forms Analytics](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html?lang=sv-SE)
-->

## Konfigurera Adobe Analytics {#configure-adobe-analytics}

Utför följande steg för att aktivera och konfigurera Adobe Analytics för en snabbspårsanalys av din adaptiva Forms:

* [Aktivera Adobe Analytics för Adaptiv Forms baserat på grundkomponenter](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [Aktivera Adobe Analytics för adaptiv Forms baserat på kärnkomponenter](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### Aktivera Adobe Analytics med adaptiv Forms for Foundation-komponent {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. Skapa en konfigurationsbehållare för molntjänster:
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   1. Välj eller skapa en konfigurationsbehållare och aktivera mappen för **[!UICONTROL Cloud Configurations]**.
   1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.
1. På din AEM-instans går du till **[Forms]** >> **[Forms och Document]**.
1. Välj **[!UICONTROL Form]** >> **[!UICONTROL Properties]** i **[!UICONTROL Configuration Container]** och markera den konfigurationsbehållare som du skapade eller markerade i **[!UICONTROL Configuration Browser]** i steg 1.
1. Markera aktivitetspanelen till vänster och klicka på **Konfigurera analys** och **Aktivera Adobe Analytics**.
1. Ange det namn du föredrar för rapportsviten, klicka på **[!UICONTROL Next]** och **[!UICONTROL Save]**.
1. När du har sparat projektet körs inställningarna en tid tills Adobe Analytics har integrerats med ditt adaptiva formulär. Du kan även kontrollera **integreringsstatusen**.

   >[!NOTE]
   >
   >Om konfigurationen tar längre tid än 15 minuter kan du försöka att aktivera analyser för formulären igen.

1. På din AEM-instans går du till **[!UICONTROL Forms]** >> **[Forms och Document]** och väljer din **[!UICONTROL Form]**. Då ser du att Adobe Analytics är integrerat med ditt formulär, vilket visas i bilden nedan.
1. Nu kan du visa din [anpassade formulär-Adobe Analytics-rapport](#view-adobe-analytics-report).

![Integrerad AEM Analytics](assets/analytics-aem-integrated.png){width="100%"}


### Aktivera Adobe Analytics med adaptiv Forms för kärnkomponenter {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. Gå till **[!UICONTROL Forms]** >> **[!UICONTROL Forms and Document]** på din AEM-instans och markera din **[!UICONTROL Form]**.
1. Markera aktivitetspanelen till vänster och klicka på **Konfigurera analys** och **Aktivera Adobe Analytics**.
1. Ange det namn du föredrar för rapportsviten, klicka på **[!UICONTROL Next]** och **[!UICONTROL Save]**.
1. När du har sparat projektet körs inställningarna en tid tills Adobe Analytics har integrerats med ditt adaptiva formulär. Du kan även kontrollera **integreringsstatusen**.

   >[!NOTE]
   >
   >Om konfigurationen tar längre tid än 15 minuter kan du försöka att aktivera analyser för formulären igen.

1. På din AEM-instans går du till **[!UICONTROL Forms]** >> **[!UICONTROL Forms and Document]** och väljer din **[!UICONTROL Form]**. Du ser att Adobe Analytics är integrerad i ditt formulär.
1. Nu kan du visa din [anpassade formulär-Adobe Analytics-rapport](#view-adobe-analytics-report).

## Visa rapporten Adaptiv Forms Adobe Analytics {#view-adobe-analytics-report}

1. Gå till **[!UICONTROL Forms]** >> **[!UICONTROL Forms and Document]** på din AEM-instans.
1. Markera formuläret så ser du att Adobe Analytics är integrerat, som det visas till vänster, med Forms som har aktiverats för Adobe Analytics.

   ![Visa rapport](assets/activ-aa.png){width="100%"}

1. Klicka på **Adobe Analytics** om du vill visa rapporten och analysera prestandadata.

Om du vill ansluta ett adaptivt formulär till Adobe Analytics med den manuella metoden går du till [Integrera AEM Forms med Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Aktivera Analytics för adaptiv Forms i Sites {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

Genom att konfigurera snabbspårsanalyser för ditt adaptiva formulär i AEM Sites kan du spåra användarinteraktioner och formulärinskickade formulär på din Formulär-sida. Genom att smidigt integrera analyser i era Sites Forms får ni värdefulla insikter om användarbeteende, konverteringsgrader och områden som kan förbättra ert formulär.

### Förutsättningar {#Prerequisites-to-connect-forms-analytics-to-sites}

För att kunna ansluta och aktivera analyser i Adaptive Forms for AEM Sites måste du se till att din AEM Sites har en aktiv Adobe Analytics.

### Ansluta adaptiva Forms i Sites för att aktivera Analytics {#Connect-analytics-to-adaptive-forms}

Om du vill ansluta adaptivt formulär på en AEM Sites-sida för att aktivera Analytics för en snabbspårsanalys inkluderar du klientbiblioteket `customfooterlibs` till AEM Sites-sidan med hjälp av AEM Archetype/Git Repository och distributionsflödet.

1. Öppna ditt [AEM Forms-projekt Archetype eller Klonad Git-databas](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE) i en textredigerare. Exempel: Visual Studio Code.

1. Navigera till sidan med webbplatserna där det adaptiva formuläret finns, till exempel I det här demoprojektet har vi `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. Kopiera värdet för `sling:resourceSuperType`. Värdet är till exempel `core/wcm/components/page/v3/page`.

   ![avlutningsresurs](/help/forms/assets/slingresource.png){width="100%"}

1. Skapa en liknande struktur på platsen `ui.apps/src/main/content/jcr_root/apps` som `core/wcm/components/page/v3/page`.

   ![övertäckningsstruktur](/help/forms/assets/overlaystructure.png){width="100%"}

1. Lägg till en `customfooterlibs.html`-fil.

   ```
   // customheaderlibs.html
   <sly data-sly-use.page="com.adobe.cq.wcm.core.components.models.Page">
   <sly data-sly-test="${page.data && page.dataLayerClientlibIncluded}" data-sly-call="${clientlib.js @ categories='core.forms.components.commons.v1.datalayer', async=true}"></sly>
   </sly>
   ```

   `customfooterlibs.html` används för JavaScript.

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=sv-SE) för att distribuera ändringarna.

### Aktivera Form Analytics-regler för Forms på Sites {#bind-forms-analytics-rules-to-forms-in-sites}

1. Gå till **Adobe Experience Platform datainsamling**.
1. Klicka på **Taggar** till vänster.
1. Sök i ditt projekt med program-ID enligt bilden nedan, till exempel för miljön med URL `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`, är program-ID `45921`.

   ![Söka-formulär-in-data-samling](/help/forms/assets/aep-data-collection.png){width="100%"}

1. Lägg till konfiguration för **formulärregler** och **dataelement** enligt nedan:

#### Lägg till formulärregler {#form-rules}

1. Markera formuläret och lägg till **Ny egenskap** i det övre högra hörnet eller klicka på formuläret.
1. Klicka på **Regler** på egenskapssidan och välj händelser för formuläret. I exempelbilden nedan är det **Formulärevenemang**.

   ![Söka-formulär-in-data-samling](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. Markera alla händelser i formuläret och **kopiera** som finns i det övre högra fältet.
1. När du har kopierat visas ett popup-fönster med namnet **Kopieringsregel** där du kan klistra in formulärreglerna på webbplatssidan med projekt-id:t.

   ![Kopiera-form-rules](/help/forms/assets/copy-form-rules.png){width="100%"}

1. Klicka på **kopiera** för att klistra in formulärreglerna på sidan Webbplatser.

#### Lägg till dataelement {#data-elements}

1. Markera formuläret och lägg till **Ny egenskap** i det övre högra hörnet eller klicka på formuläret.
1. Klicka på **Dataelement** på egenskapssidan och välj händelser för formuläret.
1. Markera alla händelser i formuläret och **kopiera** som finns i det övre högra fältet.
1. När du har kopierat visas ett popup-fönster med namnet **Kopieringsregel** där du kan klistra in formulärreglerna på webbplatssidan med projekt-id:t.
1. Klicka på **kopiera** för att klistra in formulärreglerna på sidan Webbplatser.

   ![Form-data-elements](/help/forms/assets/form-data-elements.png){width="100%"}

När du har kopplat form- och webbplatsreglerna genom de ovannämnda stegen utför du följande steg för att aktivera Analytics för ditt adaptiva formulär på sidan Platser:

1. Klicka på **Publiceringsflöde** till vänster.
1. Klicka på **Lägg till bibliotek** och ange det namn du vill ha.
1. I listrutan **Miljö** till höger väljer du **utveckling**.
1. Klicka på **Lägg till alla ändrade resurser**.
1. Klicka på **Spara och skapa till utveckling**.

![publicera till utveckling](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## Se även {#see-also}

* [Visa och förstå analysrapporter för adaptiva Forms](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [Lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Integrera AEM Forms med Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
