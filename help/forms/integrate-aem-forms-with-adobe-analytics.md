---
title: Hur integrerar man AEM Forms med Adobe Analytics?
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
hidefromtoc: true
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: 64a8b363cff079aa0a6f56effd77830ac797deca
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 0%

---

# Integrera AEM Forms med [!DNL Adobe Analytics] {#integrate-aem-forms-with-adobe-analytics}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |
| AEM as a Cloud Service | Den här artikeln |

<span class="preview"> Det här dokumentet beskriver den manuella proceduren för att aktivera Adobe Analytics i ett anpassat formulär. Adobe rekommenderar dock att du använder [Aktivera Adobe Analytics för ett adaptivt formulär med Experience Cloud Setup Automation](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md). </span>

AEM Forms integreras med [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) så att du kan hämta in och spåra prestandamått för dina publicerade formulär. Syftet med att analysera dessa värden är att göra det möjligt för företagsanvändare att få insikter i slutanvändarnas beteende och optimera datainhämtningsupplevelsen. Du kan fånga in och spåra beteendet hos både inloggade och ej inloggade (anonyma) användare via Adobe Analytics för Adaptiv Forms.

När du har utfört åtgärderna som nämns i den här artikeln kan du konfigurera och visa rapporter i [!DNL Adobe Analytics], vilket visas i följande video:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Du kan använda [!DNL Adobe Analytics] för att identifiera interaktionsmönster och problem som användare stöter på när de använder adaptiva formulär. I körklart läge spårar och lagrar [!DNL Adobe Analytics] information om följande händelser:

* **Återgivning**: Antal gånger ett formulär öppnas.

* **Skicka**: Antal gånger ett formulär skickas.

* **Avbrott**: Antal gånger som användarna lämnar utan att fylla i formuläret.

* **Fel**: Antal fel som påträffats på panelen och i panelens fält.

* **Hjälp**: Antal gånger en användare öppnar hjälpen för en panel och fälten på panelen.

* **Fältbesök**: Antal gånger en användare besöker ett fält i formuläret.

* **Spara**: Antal gånger som användare sparar ett formulär på Forms Portal.

Förutom dessa out-of-box-händelser kan du definiera anpassade händelser i adaptiva formulär med en regelredigerare och mappa dessa händelser till händelser i [!DNL Adobe Analytics]

Följande bild visar vilka åtgärder du behöver utföra innan du visar rapporter i [!DNL Adobe Analytics]:

![Analysöversikt](assets/analytics-workflow.png)

## 1. Konfigurera [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Skapa:[!DNL Adobe Analytics]

* En Adobe ID att logga in på [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* En [rapportserie](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Installera AEM Forms och [!DNL Adobe Analytics] tillägg {#install-extensions}

Så här konfigurerar du AEM Forms- och [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html)-tillägg:

1. Logga in på Adobe Experience Cloud och välj ett namn för företaget.

1. Välj **[!UICONTROL Launch/Data Collection]** och välj **[!UICONTROL Go to Launch/Data Collection]**.

1. Välj **[!UICONTROL New property]** och ange ett namn för konfigurationen.

1. Ange ett domännamn och välj **[!UICONTROL Save]** för att spara egenskapen.

1. Välj det konfigurationsnamn som finns i listan Taggegenskaper.

1. Välj **[!UICONTROL Extensions]** i avsnittet **[!UICONTROL Authoring]**.

1. Välj **[!UICONTROL Catalog]** och välj **[!UICONTROL Install]** som **[!UICONTROL Adobe Experience Manager Forms]**-tillägg. **[!UICONTROL Adobe Experience Manager Forms]** visas i listan över installerade tillägg på fliken **Installed**.

1. Välj **[!UICONTROL Install]** som **[!UICONTROL Adobe Analytics]**-tillägg.
1. Välj rapportsvitens namn i listrutorna **[!UICONTROL Development Report Suites]**, **[!UICONTROL Staging Report Suites]** och **[!UICONTROL Product Report Suites]** och välj **[!UICONTROL Save]** för att spara tillägget.

### Konfigurera dataelement {#configure-data-elements}

Du kan välja vilket som helst av de konfigurerade dataelementen i en regel som skapas för en händelse. När en händelse inträffar i ett anpassat formulär skickar AEM Forms dessa dataelement till [!DNL Adobe Analytics].

När du har installerat tillägget **[!UICONTROL Adobe Experience Manager Forms]** kan du skapa följande dataelement:

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Utför följande steg för att konfigurera dataelement:

1. Välj **[!UICONTROL Data Elements]** i avsnittet **[!UICONTROL Authoring]**.

1. Välj **[!UICONTROL Create New Data Element]**.

1. Ange ett namn för dataelementet. Exempel: Formulärtitel för dataelementtypen FormTitle.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Data Element Type]**.

1. Välj **[!UICONTROL Save]** om du vill spara dataelementet.

>[!VIDEO](https://video.tv.adobe.com/v/337472)

### Konfigurera regler {#configure-rules}

Utför följande steg för att skapa regler baserade på tillägget **[!UICONTROL Adobe Experience Manager Forms]**:

1. Välj **[!UICONTROL Rules]** i avsnittet **[!UICONTROL Authoring]**.

1. Välj **[!UICONTROL Create New Rule]**.

1. Ange ett namn för regeln. Till exempel Skicka formulär för att registrera formulärinskickade formulär.

1. Välj **[!UICONTROL Add]** i avsnittet **[!UICONTROL Events]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj händelsetyp. Indata för fältet **[!UICONTROL Name]** fylls i automatiskt baserat på den valda händelsetypen.

1. Välj **[!UICONTROL Keep Changes]** om du vill spara händelsen.

1. Välj **[!UICONTROL Add]** i avsnittet **[!UICONTROL Actions]**.

1. Ange **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Set Variables]** som åtgärdstyp. De alternativ som är tillgängliga i listrutan är bland annat:

   * **[!UICONTROL Set Variables]**: Använd den här åtgärdstypen för att definiera händelsetypen som de markerade dataelementen skickas från AEM Forms till [!DNL Adobe Analytics].

   * **[!UICONTROL Send Beacon]**: Använd den här åtgärdstypen för att skicka data från AEM Forms till [!DNL Adobe Analytics].

   * **[!UICONTROL Clear Variables]**: Använd den här åtgärdstypen för att rensa dataspårningen så att händelsen bara registreras en gång i [!DNL Adobe Analytics].

     Rekommenderat tillvägagångssätt är att använda åtgärdstypen **[!UICONTROL Set Variables]** för att konfigurera händelsen och dataelementen, sedan använda **[!UICONTROL Send Beacon]** för att skicka data och sedan använda **[!UICONTROL Clear Variables]** för att rensa dataspårningen.

1. I avsnittet **[!UICONTROL Props]** mappar du de rapportrutealternativ som är tillgängliga i listrutan med dataelementen som har definierats med [Konfigurera dataelement](#configure-data-elements).

   Om du till exempel vill skicka dataelementet **Formulärtitel** från AEM Forms till [!DNL Adobe Analytics] när du skickar ett formulär:
   1. I avsnittet **[!UICONTROL Props]** väljer du ett utkast för Formulärtitel som är tillgängligt i rapportsviten och sedan ![Databasikon](assets/database-icon.svg) för att mappa det till Formulärtitel som har skapats i [Konfigurera dataelement](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Välj **[!UICONTROL Add Another]** om du vill lägga till fler dataelement i listan.

1. I avsnittet **[!UICONTROL Events]** väljer du en händelse bland de tillgängliga alternativen i rapportsviten och väljer **[!UICONTROL Keep Changes]**.

1. I avsnittet **[!UICONTROL Actions]** väljer du + och anger **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Send Beacon]** som åtgärdstyp. I den högra rutan väljer du **[!UICONTROL s.t()]** för att skicka data till [!DNL Adobe Analytics] och behandla dem som en sidvy eller **[!UICONTROL s.tl()]** för att skicka data till [!DNL Adobe Analytics] och inte som en sidvy. Välj **[!UICONTROL Keep Changes]**.

1. I avsnittet **[!UICONTROL Actions]** väljer du + och anger **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Clear Variables]** som åtgärdstyp. Välj **[!UICONTROL Keep Changes]**. När du har utfört de här stegen visas avsnittet **[!UICONTROL Actions]** som:
   ![Åtgärdskonfiguration](assets/actions-config.png)

   Anpassa avsnittet **[!UICONTROL Actions]** enligt dina krav. Du kan till exempel definiera två **Skicka Beacon**-steg i ett åtgärdsflöde för att skicka data till [!DNL Adobe Analytics] och behandla dem som en sidvy i ett enda steg och skicka data till [!DNL Adobe Analytics] och inte behandla dem som en sidvy i det andra steget.

   ![Åtgärdskonfiguration](assets/actions-config-2.png)

1. Välj **[!UICONTROL Save]** om du vill spara regeln.

   Du kan skapa regler för alla händelsetyper, till exempel överge, Fel, fältbesök, Hjälp, Återge, Spara och Skicka.

>[!VIDEO](https://video.tv.adobe.com/v/337425)


### Publish {#publish-flow}

När du har skapat dataelementen och använt dem i regler publicerar du konfigurationen för att samla in formulärdata i [!DNL Adobe Analytics].

Utför följande steg för att publicera konfigurationen:

1. Välj **[!UICONTROL Publishing Flow]** i avsnittet **[!UICONTROL Publishing]**.

1. Välj **[!UICONTROL Add Library]**, ange ett namn och markera miljön för biblioteket.

1. Välj **[!UICONTROL Add All Changed Resources]** och sedan **[!UICONTROL Save & Build to Development]**.

1. I avsnittet **[!UICONTROL Development]** väljer du ![Fler alternativ](assets/more-options-icon.svg) och sedan **[!UICONTROL Approve & Publish to Production]**.

1. Bekräfta att ändringarna och publiceringsflödet snart visas i avsnittet **[!UICONTROL Published]**.

![Publish Flow](assets/publish-flow.png)

## 2. Konfigurera AEM Forms {#configure-aem-forms}

Skapa en [Adobe IMS-konfiguration med Adobe Launch som molnlösning](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html) innan du skapar en startkonfiguration för Adobe.

### Skapa startkonfiguration för Adobe {#create-adobe-launch-configuration}

Så här skapar du en konfiguration för Adobe Launch:

1. I AEM Forms Author-instansen går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Launch Configurations]**.

1. Välj en mapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.

1. Ange en rubrik för konfigurationen i fältet **[!UICONTROL Title]**.

1. Välj den [associerade Adobe IMS-konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Välj namnet på företaget som användes när [Adobe Analytics](#Configure-adobe-analytics) konfigurerades.

1. Markera namnet på den egenskap som skapades när [Adobe Analytics](#install-extensions) konfigurerades.

1. Välj **[!UICONTROL Save & Close]**.

1. Publish konfigurationen.

### Aktivera [!DNL Adobe Analytics] för ett anpassat formulär {#enable-analytics-adaptive-form}

Så här använder du konfigurationen [!DNL Adobe Launch] i ett befintligt adaptivt formulär:

1. I AEM Forms Author-instansen går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och välj **[!UICONTROL Properties]**.
1. På fliken **[!UICONTROL Basic]** väljer du den [konfigurationsbehållare](#create-adobe-launch-configuration) som används när konfigurationen för Adobe Launch skapas.
1. Välj **[!UICONTROL Save & Close]**. Det adaptiva formuläret har aktiverats för [!DNL Adobe Analytics].
1. Publish blanketten.

När du har aktiverat [!DNL Adobe Analytics] för ett anpassat formulär kan du [validate](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) om det finns ett lämpligt datahändelseflöde mellan AEM Forms och [!DNL Adobe Analytics]. Integreringen av AEM Forms med Adobe Analytics är klar. Nu kan du [konfigurera och visa rapporter i Adobe Analytics](#view-reports-adobe-analytics).

### Skapa regler för att hämta anpassade händelser (valfritt) {#capture-custom-events}

Skapa regler för specifika fält i ett adaptivt formulär med en regelredigerare för att skicka analysdata från ett adaptivt formulär till [!DNL Adobe Analytics].

I en tvåstegsprocess definierar du en regel för ett fält i ett anpassningsbart format. Regeln skickar en händelse. Namnet på händelsen mappas till en anpassad inspelningshändelse i Adobe Launch.

Så här skapar du regler med en regelredigerare i ett anpassat format:

1. Markera fältet och välj ![Regelredigeraren](assets/rule-editor-icon.svg) för att öppna regelredigeringssidan.
1. Definiera ett villkor i regelns [!UICONTROL When]-avsnitt.
1. Välj **[!UICONTROL Dispatch Event]** i listrutan **[!UICONTROL Select Action]** i regelns [!UICONTROL Then]-avsnitt.
1. Ange namnet på händelsen i fältet **[!UICONTROL Type Event Name]**.

Om födelsedatumet till exempel är före ett visst datum skickar AEM Forms **Security** -händelsen.

![Utsändningshändelse](assets/security-event.png)

Så här mappar du händelsen till en anpassad fångsthändelse i [!DNL Adobe Analytics]:

1. [Skapa en regel](#configure-rules).

1. Välj **[!UICONTROL Add]** i avsnittet **[!UICONTROL Events]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Capture Custom Event]** i listrutan **[!UICONTROL Event Type]**.

1. Ange namnet på händelsen som du angav i steg 4 när du skapade en regel med regelredigeraren.

1. Välj **Behåll ändringar** och utför resten av åtgärderna som anges i [Konfigurera regler](#configure-rules).

## 3. Konfigurera och visa rapporter i [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

När du har konfigurerat ett adaptivt formulär för att skicka händelsedata till [!DNL Adobe Analytics] kan du börja visa rapporter i [!DNL Adobe Analytics]:

1. Välj ![Välj Produkt](assets/select-analytics.png) och välj **[!UICONTROL Analytics]**.

1. Välj **[!UICONTROL Create Project]** och välj **[!UICONTROL Blank project]**.

1. Välj rapportsvitens namn i listrutan högst upp till höger på frihandsformuläret.

1. Ange **Formulärtitel** i texten **[!UICONTROL Search dimension items]** om du vill visa alla formulärtitlar.

1. Släpp den anpassningsbara formulärtiteln i textrutan **[!UICONTROL Drop a segment here (or any other component)]**.

1. I avsnittet **[!UICONTROL Metrics]** släpper du de händelser som ska spåras i textrutan **[!UICONTROL Drop a metric here (or any other component)]**.

1. Välj ![Visualiseringar](assets/visualization-icon.svg) och släpp en diagramtyp i avsnittet Frihand. På samma sätt kan du lägga till flera diagramtyper i avsnittet Frihand.

1. Markera Ctrl + S och ange ett namn för att spara projektet.

<!--

## Add AEM Forms and Adobe Analytics integration specific rules to Dispatcher {#forms-specific-rules-to-dispatcher}

Add AEM Forms and Adobe Analytics integration specific rules to filter the data traffic that is sent to the backend.

Perform the following steps to add AEM Forms and Adobe Analytics integration specific rules to Dispatcher for Experience Manager Forms as a Cloud Service:

1. Open your AEM Project and navigate to `\src\conf.dispatcher.d\filters`.
1. Open `filters.any` file for editing and add the following rule at the end of the file:

     ```json
     /00XX { /type "allow" /path "/content/forms/af/*" /method "POST" /selectors '(analyticsconfigparser)' /extension '(jsp|json)' }
     ```

1. Save and close the file.
1. Compile and deploy the project to your [!DNL AEM Forms] as a Cloud Service environment.



## Limitations {#limitations}

* Adobe Analytics can track form metrics only for authenticated users.

-->

>[!MORELIKETHIS]
>
>*[Aktivera Adobe Analytics för ett anpassat formulär](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)