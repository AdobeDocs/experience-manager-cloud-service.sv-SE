---
title: Aktivera Adobe Analytics för ett adaptivt formulär
description: Experience Cloud Setup Automation kan koppla Adobe Analytics till ett adaptivt formulär för att spåra insikter om besökarinteraktioner och engagemang.
keywords: Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation, Enable Adobe Analytics in Forms, Adobe Analytics in Adaptive Forms, Forms analytics integration, Forms and Adobe Analytics
source-git-commit: 4daba42c9d8a7eff5d3ef6f9581c52c787666ed1
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---


# Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Den här artikeln |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |

Experience Cloud Setup Automation hjälper till att koppla Adobe Analytics till Adaptive Forms, som gör det enklare att spåra och analysera användarinteraktion med era formulär och erbjuder insikter om besökarinteraktioner och -engagemang. Experience Cloud Setup Automation hjälper också till att övervaka formulärprestanda, vilket innebär att utvärdera mätvärden som slutförandetider och bortfallspunkter. Denna analys hjälper till att optimera formulär för att ge en bättre användarupplevelse och särskilja användarbeteenden baserat på inloggningsstatus, t.ex. anonyma användare, för att identifiera allmänna trender och mönster.

## Fördelar med att integrera Adobe Analytics med Adaptive Forms {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **Insikter i slutanvändarnas beteende**: Adobe Analytics hjälper till att få insikter om slutanvändarnas beteende, avslöjar användaråtgärder, bortfall och slutförandefrekvens, vilket ger en djupare förståelse för hur olika användare interagerar med formulär.
* **Ge icke-tekniska affärsanvändare möjlighet att få insikter**: Adobe Analytics har ett lättanvänt gränssnitt som ger även icke-tekniska användare möjlighet att få tillgång till och tolka data om formuläranvändning, vilket främjar datadrivna beslut som förbättrar registreringsupplevelsen.
* **Optimera datainhämtningsupplevelsen baserat på användning**: Organisationer identifierar enkelt problem vid datainhämtning, vilket leder till riktade förbättringar som förbättrar formuläranvändbarheten och ökar antalet lyckade inskick.

## Omfattning av anpassade användningsmått för Forms {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics har ett omfattande utbud av adaptiva Forms-prestandamätningar som ger värdefull information om formuläranvändning. Dessa mått är:

* **Formuläråtergivning, formulärinskickning, valideringsfel och unika besökare** så att ni kan bedöma hur användbara och effektiva era formulär är.

* **Information om besökare** som omfattar besöks- och inlämningsfrekvenser och unika besökarantal, vilket ger en heltäckande bild av er formulärpublik.

* **Enhetstyp** data som informerar dig om vilka enheter användare använder för att få tillgång till dina formulär.

* **Geografisk fördelning** visar den regionala fördelningen av formuläranvändarna.

* **Trafikkällor** och **Populära formulär** mätvärden som består av de viktigaste hänvisande domänerna och de mest besökta formulären hjälper er att förstå var trafiken kommer ifrån och vilka formulär som är de populäraste.

* **Användaraktivitet i de vanligaste formulären** ger insikter om fältbesök, formuläråtergivningar, valideringsfel, övergivna formulär och inskickade formulär, så att du kan analysera användarbeteenden.

* **Tidslinje för den tid som läggs på formulär** som ger en tidslinjebaserad bild av användarinteraktionen med era formulär.

* **Områden som kräver hjälp av besökare** mätvärden som innehåller hjälpvyer, valideringsfel och besöksfrekvenser, som visar var användarna kan behöva hjälp med att fylla i formulär.

![Analysrapport](assets/analytics-report.png){width="100%"}


Detaljerad information om varje mätvärde finns på [Visa och förstå AEM Forms Analytics-rapporter](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Förutsättningar {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud Setup Automation kräver en **Adobe Analytics-licens**, **Datainsamling (tidigare Adobe Launch)** för att hantera spårningsskript och **Experience Manager Forms-licens** för smidig datainsamling och generering av insikter.

Om du har en aktiv licens för **Adobe Analytics** och **Experience Manager Forms** och du kan integrera med **Datainsamling (tidigare Adobe Launch)** bör du verifiera deras tillgänglighet i utvecklarkonsolen.

Du kan kontrollera att det som nämns ovan finns för din as a Cloud Service Forms-miljö på [utvecklarkonsol](https://developer.adobe.com/console/projects), navigera till projektet och söka efter projektet med program-ID - miljö-ID, till exempel, för miljön med URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, program-id - miljö-id är `p45913-e175111`. Kontrollera att Experience Cloud Setup Automation, Adobe Analytics och Experience Platform Launch är listade. Om de här listas kan du aktivera Adobe Analytics för din adaptiva Forms.

![Forms Analytics-integrering krävs](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html)
-->

## Konfigurera Adobe Analytics {#configure-adobe-analytics}

Följ stegen nedan för att aktivera och konfigurera Adobe Analytics för din adaptiva Forms:

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
   1. Tryck **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.
1. Gå till på din AEM **[Forms]** >> **[Forms och dokument]**.
1. Välj **[!UICONTROL Form]** >> **[!UICONTROL Properties]**, i **[!UICONTROL Configuration Container]** väljer du konfigurationsbehållaren som du skapade eller markerade i dialogrutan **[!UICONTROL Configuration Browser]** i steg 1.
1. Välj aktivitetspanelen i det vänstra fältet och klicka på **Konfigurationsanalys** och **Aktivera Adobe Analytics**.
1. Ange det namn du föredrar för rapportsviten, klicka på **[!UICONTROL Next]** och **[!UICONTROL Save]**.
1. När du har sparat projektet körs inställningarna en tid tills Adobe Analytics har integrerats med ditt adaptiva formulär. Du kan även kontrollera **integreringsstatus**.

   >[!NOTE]
   >
   >Om konfigurationen tar längre tid än 15 minuter kan du försöka att aktivera analyser för formulären igen.

1. Gå till på din AEM **[!UICONTROL Forms]** >> **[Forms och dokument]** och väljer **[!UICONTROL Form]** ser du att Adobe Analytics är integrerat i ditt formulär så som visas i bilden nedan.
1. Nu kan du se [Adaptiv form Adobe Analytics-rapport](#view-adobe-analytics-report).

![Integrerad AEM Analytics](assets/analytics-aem-integrated.png){width="100%"}


### Aktivera Adobe Analytics med adaptiv Forms för kärnkomponenter {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. Gå till på din AEM **[!UICONTROL Forms]** >> **[!UICONTROL Forms and Document]** och väljer **[!UICONTROL Form]**.
1. Välj aktivitetspanelen till vänster och klicka på **Konfigurationsanalys** och **Aktivera Adobe Analytics**.
1. Ange det namn du föredrar för rapportsviten, klicka på **[!UICONTROL Next]** och **[!UICONTROL Save]**.
1. När du har sparat projektet körs inställningarna en tid tills Adobe Analytics har integrerats med ditt adaptiva formulär. Du kan även kontrollera **integreringsstatus**.

   >[!NOTE]
   >
   >Om konfigurationen tar längre tid än 15 minuter kan du försöka att aktivera analyser för formulären igen.

1. Gå till på din AEM **[!UICONTROL Forms]** >> **[!UICONTROL Forms and Document]** och väljer **[!UICONTROL Form]** ser du att Adobe Analytics är integrerat i ditt formulär.
1. Nu kan du se [Adaptiv form Adobe Analytics-rapport](#view-adobe-analytics-report).

## Visa rapporten Adaptiv Forms Adobe Analytics {#view-adobe-analytics-report}

1. Gå till på din AEM **[!UICONTROL Forms]** >> **[!UICONTROL Forms and Document]**.
1. Markera formuläret så ser du att Adobe Analytics är integrerat, som det visas till vänster, med Forms som har aktiverats för Adobe Analytics.

   ![Visa rapport](assets/activ-aa.png){width="100%"}

1. Klicka **Adobe Analytics** för att visa rapporten och analysera prestandadata.

Om du vill koppla ett adaptivt formulär till Adobe Analytics med hjälp av manuella metoder går du till [Integrera AEM Forms med Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Aktivera Analytics för adaptiv Forms i Sites {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

Om du konfigurerar analyser för ditt adaptiva formulär i AEM Sites kan du spåra användarinteraktioner och formulärinskickade formulär på din formulärsida. Genom att smidigt integrera analyser i era Sites Forms får ni värdefulla insikter om användarbeteende, konverteringsgrader och områden som kan förbättra ert formulär.

### Förutsättningar {#Prerequisites-to-connect-forms-analytics-to-sites}

För att kunna ansluta och aktivera analyser i Adaptive Forms for AEM Sites måste du se till att din AEM Sites har en aktiv Adobe Analytics.

### Ansluta adaptiva Forms i Sites för att aktivera Analytics {#Connect-analytics-to-adaptive-forms}

Om du vill ansluta adaptivt formulär på en AEM Sites-sida för att aktivera Analytics, inkluderar du `customfooterlibs` klientbibliotek till AEM Sites-sidan med hjälp av AEM Archetype/Git Repository och distributionskanalen.

1. Öppna [AEM Forms Archetype eller Klonad Git-databas](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) i en textredigerare. Exempel: Visual Studio Code.

1. Navigera till den sida i webbplatserna där det adaptiva formuläret finns, till exempel I det här demoprojektet har vi `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. Kopiera värdet för `sling:resourceSuperType`. Värdet är till exempel `core/wcm/components/page/v3/page`.

   ![försäljningsresurs](/help/forms/assets/slingresource.png){width="100%"}

1. Skapa en liknande struktur på platsen `ui.apps/src/main/content/jcr_root/apps` samma som `core/wcm/components/page/v3/page`.

   ![övertäckningsstruktur](/help/forms/assets/overlaystructure.png){width="100%"}

1. Lägg till en `customfooterlibs.html` -fil.

       &quot;
       // customheaderlibs.html
       &lt;sly data-sly-use.page=&quot;com.adobe.cq.wcm.core.components.models.Page&quot;>
       &lt;sly data-sly-test=&quot;${page.data &amp;&amp; page.dataLayerClientlibIncluded}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.commons.v1.datalayer&amp;#39;, async=true}&quot;>&lt;/sly>
       &lt;/sly>
       
       &quot;
   
   The `customfooterlibs.html` används för JavaScript.

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) för att distribuera ändringarna.

### Aktivera Form Analytics-regler för Forms på Sites {#bind-forms-analytics-rules-to-forms-in-sites}

1. Besök **Adobe Experience Platform Data Collection**.
1. Klicka **Taggar** till vänster.
1. Sök i ditt projekt med program-ID:t som visas i bilden nedan, t.ex. efter miljön med URL:en `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`, program-ID är `45921`.

   ![Söka-formulär-in-data-samling](/help/forms/assets/aep-data-collection.png){width="100%"}

1. Lägg till konfiguration för **Formulärregler** och **Dataelement** enligt nedan:

#### Lägg till formulärregler {#form-rules}

1. Markera formuläret och lägg till **Ny egenskap** längst upp till höger eller klicka på formuläret.
1. Klicka på egenskapssidan **Regler** och välj händelser för formuläret. I exempelbilden nedan är det **Formulärevenemang**.

   ![Söka-formulär-in-data-samling](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. Markera alla händelser i formuläret och **copy** som finns på den övre högra listen.
1. När du har kopierat en **Kopiera regel** visas där du söker på din webbplatssida med projekt-id:t för att klistra in formulärreglerna.

   ![Copy-form-rules](/help/forms/assets/copy-form-rules.png){width="100%"}

1. Klicka **copy** om du vill klistra in formulärreglerna på sidan Webbplatser.

#### Lägg till dataelement {#data-elements}

1. Markera formuläret och lägg till **Ny egenskap** längst upp till höger eller klicka på formuläret.
1. Klicka på egenskapssidan **Dataelement** och välj händelser för formuläret.
1. Markera alla händelser i formuläret och **copy** på den övre högra listen.
1. När du har kopierat en **Kopiera regel** visas där du söker på din webbplatssida med projekt-id:t för att klistra in formulärreglerna.
1. Klicka **copy** om du vill klistra in formulärreglerna på sidan Webbplatser.

   ![Form-data-elements](/help/forms/assets/form-data-elements.png){width="100%"}

När du har kopplat form- och webbplatsreglerna genom de ovannämnda stegen utför du följande steg för att aktivera Analytics för ditt adaptiva formulär på sidan Platser:

1. Klicka **Publiceringsflöde** till vänster.
1. Klicka **Lägg till bibliotek** och ange det namn du föredrar.
1. I **Miljö** nedrullningsbar meny till höger, välj **utveckling**.
1. Klicka **Lägg till alla ändrade resurser**.
1. Klicka **Spara och bygg till utveckling**.

![publicera-till-utveckling](/help/forms/assets/publish-to-dev.png){width="100%"}


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
