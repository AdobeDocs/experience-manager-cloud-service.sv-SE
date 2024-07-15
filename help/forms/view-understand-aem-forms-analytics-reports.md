---
title: Visa och förstå analysrapporter för adaptiva Forms
description: Adaptiv Forms integreras smidigt med Adobe Analytics för att hämta in och spåra prestandamått för era publicerade formulär och dokument.
keywords: Visa och förstå adaptiva Forms-analysrapporter, analysrapport för Adobe, Forms Analytics-rapport
topic-tags: develop
feature: Adaptive Forms
role: Admin, User
level: Intermediate
exl-id: 756dee1f-4685-4783-961d-b172a5bd0692
source-git-commit: 975f767e75a268a1638227ae20a533f82724c80a
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---

# Visa och förstå analysrapporter för adaptiva Forms {#viewing-and-understanding-aem-forms-analytics-reports}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Den här artikeln |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html) |

I det snabbt föränderliga landskapet med digital analys är det av största vikt att vi fortsätter att engagera oss i globala trender för att fatta välgrundade beslut och optimera digitala upplevelser. Adaptive Forms integreras smidigt med Adobe Analytics för att hämta in och spåra prestandamått för era publicerade formulär och dokument. Syftet med att analysera dessa värden är att fatta databaserade beslut med hjälp av statistik och analyser för att förbättra formulärens användbarhet och effektivitet.

Genom att samla in och spåra nyckeltal för prestandaindikatorer kan företag identifiera områden med förbättringar, optimera användarupplevelser och i slutänden få bättre resultat för att skapa exceptionella kundupplevelser.

## Konfigurera Adobe Analytics till Adaptiv Forms {#setup-adobe-analytics-to-aem-forms}

För AEM Forms Analytics-rapporten integrerar du först Adobe Analytics till AEM Forms via Experience Cloud Setup Automation. Experience Cloud Setup Automation i Adaptive Forms kräver en Adobe Analytics-licens, Data Collection (tidigare Adobe Launch) för att hantera spårningsskript och integrering med Experience Platform Launch API för smidig datainsamling och generering av insikter. Gå till [Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md) om du vill ha fullständig installationsinformation.

## Visa rapporten Adaptiv Forms Adobe Analytics {#view-adobe-analytics-report}

1. Gå till **[!UICONTROL Forms]** >> **[!UICONTROL Forms and Document]** på din AEM.
1. Markera formuläret så ser du att Adobe Analytics är integrerat, som det visas till vänster, med Forms som har aktiverats för Adobe Analytics.

   ![Visa rapport](assets/activ-aa.png){width="100%"}

1. Klicka på **Adobe Analytics** om du vill visa rapporten och analysera prestandadata.

## Analysrapport om adaptiva Forms {#understanding-aem-forms-analytics-reports}

Adobe Analytics har ett omfattande utbud av adaptiva Forms-prestandamätningar som ger värdefull information om formuläranvändning. Dessa mått är:

### **Hur fungerar Adaptiv Forms?** {#how-your-adaptive-form-is-performing}

Här finns mätvärden för formuläråtergivning, formulärinskickning, valideringsfel och unika besökare, som gör att du kan bedöma hur användbara och effektiva dina formulär är:

* **Formuläråtergivningar**: Formuläråtergivningar visar hur många gånger formuläret har återgetts eller öppnats.

* **Formuläröverföringar**: Formuläröverföringar anger hur många gånger anpassningsbara formulär har fyllts i och skickats av användarna.

* **Valideringsfel**: Valideringsfel visar det totala antalet valideringsrelaterade fel som inträffade i formulärfälten.

* **Unika besökare**: Unika besökare representerar det antal gånger som formuläret återges av en besökare. Mer information om unika besökare finns i [Unika besökare, besök och kundbeteende](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).

  ![Forms-prestanda](assets/forms-performance.png){width="100%"}

### **Besökare i formulären** {#visitors-to-your-forms}

Det hjälper er att få värdefulla insikter om besökaraktiviteten i era formulär:

* **Besök och inskickade formulär**: Här beskrivs hur ofta du besöker formulär i ett datumintervall och hur många formulär som skickas. Mer information om detta finns på [Besök](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).
* **Unika besökare och deras totala besök**: Det skiljer mellan nya och återkommande användare. En besökare kan till exempel komma till din webbplats varje dag i en månad, men de räknas ändå som en unik besökare. Besök [unika besökare](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html) om du vill ha mer information.

  ![Forms Visitors](assets/forms-visitors.png){width="100%"}

### **Enhetstyp** {#device-type}

Enhetstypen hjälper dig att identifiera vilken typ av enhet som används för att komma åt dina formulär. Den kategoriserar enhetstypen som Mobilenhetstyp. I det här fallet är det till exempel Mobilenhetstyp: Annan och Mobilenhetstyp: Mobiltelefon. De olika typerna av mobila enheter är bland annat mobiltelefon, surfplatta, mediespelare och spelkonsol.

![Enhetstyp](assets/device-type.png){width="100%"}

### **Geografisk uppdelning** {#geographical-breakdown}

Här visas den plats där du har åtkomst till Forms. Här finns regionspecifik information om formuläranvändare. Du kan till exempel se att en regionspecifik information om en formuläranvändare är Indien, vilket visas i bilden.

![Geografisk uppdelning](assets/geographical-breakdown.png){width="100%"}

### **De viktigaste trafikkällorna och de populära formulären** {#top-sources-of-traffic-and-popular-forms}

Detta hjälper dig att identifiera den primära källan eller länken till den plats där formulären refereras. I den angivna bilden nedan visas till exempel sökinstanser för dina adaptiva formulär där 18,9 % är **Typed/Bookmarked**, 70,49 % baseras på **sökmotorer** och 24 % kommer från **Andra webbplatser**. Du kan definiera dimensionsobjekt baserat på dina behov. Dessutom kan ni ta reda på vilka som är de mest besökta eller populära formulären.

![Refererade webbplatser](assets/referred-sites.png){width="100%"}

### **Användaraktivitet i de vanligaste formulären** {#user-activity-on-top-forms}

En heltäckande bild av användarengagemanget med fältbesök, formuläråtergivningar, valideringsfel, övergivna formulär och inskickade formulär ger insikter om de formulär som är mest aktiva. I bilden nedan ser du att ansökningsformuläret är det mest aktiva baserat på formulärhändelsestatistik.

![Användaraktivitet](assets/user-activity.png){width="100%"}

### **Tidslinje för tid i formulär** {#timeline-for-time-spent-on-forms}

Det är den tid användarna lägger på era formulär över tiden, vilket hjälper er att identifiera engagemangsmönster.

![Tidsåtgång för formulär](assets/time-spent-on-forms.png){width="100%"}

### **Områden där besökare behöver hjälp med att fylla i formuläret** {#areas-requiring-assistance}

Mätvärden som hjälpvyer, valideringsfel och fältbesök visar var användarna behöver hjälp eller hur vi kan spåra fel i fält. I bilden nedan ser du till exempel det i ett formulär med fält som **Fullständigt namn**, **Telefonnummer**, **DoB**. Fältet **Fullständigt namn** har 12 besök, av 12 besök har 8 besök valideringsfel och 1 klickad på hjälpikon för att få hjälp med det här fältet. Du kan se mätdata för andra formulärfält.

![Hjälpområden](assets/assisting-areas.png){width="100%"}

### **Det sista formulärfältet som besökarna visade innan de övergav formuläret** {#last-form-field-that-visitors-viewed}

Det hjälper dig att analysera formulärfälten där användarna har tillbringat tid innan du överger formuläret. I bilden nedan finns t.ex. 5 övergivna formulär, 2 kvar i fältet **Fullständigt namn**, 2 kvar i fältet **Telefonnummer** och 1 kvar i fältet **Textindata**.

![Fältbesökare](assets/field-visitors.png){width="100%"}

## Se även {#see-also}

* [Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)
* [Lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Integrera AEM Forms med Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
