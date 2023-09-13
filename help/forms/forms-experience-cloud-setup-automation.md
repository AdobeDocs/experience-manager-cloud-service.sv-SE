---
title: Aktivera Adobe Analytics för ett adaptivt formulär
description: Experience Cloud Setup Automation kan koppla Adobe Analytics till ett adaptivt formulär för att spåra insikter om besökarinteraktioner och engagemang.
source-git-commit: 39ea959cb0a0568fd94ca455be935228479c0415
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---


# Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

<span class="preview"> Det här är en förhandsversion som du kommer åt via vår [kanal för förhandsversion](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

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

Experience Cloud Setup Automation i Adobe Experience Manager Forms kräver en **Adobe Analytics-licens**, **Datainsamling (tidigare Adobe Launch)** för att hantera spårningsskript och integrering med **Experience Platform Launch (API)** för smidig datainsamling och generering av insikter.

Om du har en aktiv licens för Experience Cloud Setup Automation, Adobe Analytics och Experience Platform Launch API bör du kontrollera att de är tillgängliga i din utvecklarkonsol.

Du kan kontrollera att det som nämns ovan finns för din as a Cloud Service Forms-miljö på [utvecklarkonsol](https://developer.adobe.com/console/projects), navigera till projektet och söka efter projektet med program-id:t, till exempel för miljön med URL:en `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, program-ID är `p45913-e175111`. Kontrollera att Experience Cloud Setup Automation, Adobe Analytics och Experience Platform Launch är listade. Om de här listas kan du aktivera Adobe Analytics för din adaptiva Forms.

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
