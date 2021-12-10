---
title: Hur integrerar man AEM Forms med Adobe Analytics?
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---

# Integrera med [!DNL Adobe Analytics] {#integrate-aem-forms-with-adobe-analytics}

AEM Forms kan integreras med [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) så att ni kan samla in och spåra resultatvärden för era publicerade formulär. Syftet med att analysera dessa värden är att göra det möjligt för företagsanvändare att få insikter i slutanvändarnas beteende och optimera datainhämtningsupplevelsen. Du kan fånga in och spåra beteenden hos både inloggade och ej inloggade (anonyma) användare via Adobe Analytics för Adaptiv Forms.

När du har utfört de åtgärder som nämns i den här artikeln kan du konfigurera och visa rapporter i [!DNL Adobe Analytics], vilket visas i följande video:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Du kan använda [!DNL Adobe Analytics] för att upptäcka interaktionsmönster och problem som användare möter när de använder adaptiva formulär. Ut ur lådan, [!DNL Adobe Analytics] spårar och lagrar information om följande händelser:

* **Återgivning**: Antal gånger ett formulär öppnas.

* **Skicka**: Antal gånger ett formulär skickas.

* **Abandon**: Antal gånger som användarna lämnar utan att fylla i formuläret.

* **Fel**: Antal fel som påträffats på panelen och i panelens fält.

* **Hjälp**: Antal gånger en användare öppnar hjälpen för en panel och fälten på panelen.

* **Fältbesök**: Antal gånger en användare besöker ett fält i formuläret.

* **Spara**: Antal gånger som användare sparar ett formulär på Forms Portal.

Förutom dessa out-of-box-händelser kan du definiera anpassade händelser i adaptiva formulär med hjälp av regelredigeraren och mappa dessa händelser till händelser i [!DNL Adobe Analytics]

Följande bild visar vilka åtgärder du behöver utföra innan du visar rapporter i [!DNL Adobe Analytics]:

![Analytics - översikt](assets/analytics-workflow.png)

## 1. Konfigurera [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Före konfigurering [!DNL Adobe Analytics], skapa:

* En Adobe ID att logga in på [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [rapportsvit](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Installera AEM Forms och [!DNL Adobe Analytics] tillägg {#install-extensions}

Utför följande steg för att konfigurera AEM Forms och [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) tillägg:

1. Logga in på Adobe Experience Cloud och välj ett namn för företaget.

1. Tryck **[!UICONTROL Launch/Data Collection]** och trycka **[!UICONTROL Go to Launch/Data Collection]**.

1. Tryck **[!UICONTROL New property]** och ange ett namn för konfigurationen.

1. Ange ett domännamn och tryck på **[!UICONTROL Save]** för att spara egenskapen.

1. Tryck på konfigurationsnamnet som finns i listan Taggegenskaper.

1. I **[!UICONTROL Authoring]** sektion, trycka **[!UICONTROL Extensions]**.

1. Tryck **[!UICONTROL Catalog]** och trycka **[!UICONTROL Install]** för **[!UICONTROL Adobe Experience Manager Forms]** tillägg. **[!UICONTROL Adobe Experience Manager Forms]** visas i listan över installerade tillägg som är tillgängliga i **Installerad** -fliken.

1. Tryck **[!UICONTROL Install]** för **[!UICONTROL Adobe Analytics]** tillägg.
1. Välj rapportsvitens namn i dialogrutan **[!UICONTROL Development Report Suites]**, **[!UICONTROL Staging Report Suites]** och **[!UICONTROL Product Report Suites]** nedrullningsbara listor och trycka **[!UICONTROL Save]** för att spara tillägget.

### Konfigurera dataelement {#configure-data-elements}

Du kan välja vilket som helst av de konfigurerade dataelementen i en regel som skapas för en händelse. När en händelse inträffar i ett adaptivt formulär skickar AEM Forms dessa dataelement till [!DNL Adobe Analytics].

När du har installerat **[!UICONTROL Adobe Experience Manager Forms]** kan du skapa följande dataelement:

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

1. I **[!UICONTROL Authoring]** sektion, trycka **[!UICONTROL Data Elements]**.

1. Tryck på **[!UICONTROL Create New Data Element]**.

1. Ange ett namn för dataelementet. Exempel: Formulärtitel för dataelementtypen FormTitle.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Data Element Type]**.

1. Tryck **[!UICONTROL Save]** för att spara dataelementet.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Konfigurera regler {#configure-rules}

Utför följande steg för att skapa regler baserade på **[!UICONTROL Adobe Experience Manager Forms]** tillägg:

1. I **[!UICONTROL Authoring]** sektion, trycka **[!UICONTROL Rules]**.

1. Tryck på **[!UICONTROL Create New Rule]**.

1. Ange ett namn för regeln. Till exempel Skicka formulär för att registrera formulärinskickade formulär.

1. I **[!UICONTROL Events]** sektion, trycka **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj händelsetyp. Indata för **[!UICONTROL Name]** fylls i automatiskt baserat på den valda händelsetypen.

1. Tryck **[!UICONTROL Keep Changes]** för att spara händelsen.

1. I **[!UICONTROL Actions]** sektion, trycka **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Set Variables]** som åtgärdstyp. De alternativ som är tillgängliga i listrutan är bland annat:

   * **[!UICONTROL Set Variables]**: Använd den här åtgärdstypen för att definiera händelsetypen som de markerade dataelementen skickas från AEM Forms till [!DNL Adobe Analytics].

   * **[!UICONTROL Send Beacon]**: Använd den här åtgärdstypen för att skicka data från AEM Forms till [!DNL Adobe Analytics].

   * **[!UICONTROL Clear Variables]**: Använd den här åtgärdstypen för att rensa dataspårningen så att händelsen bara registreras en gång i [!DNL Adobe Analytics].

      Rekommenderad metod är att använda **[!UICONTROL Set Variables]** åtgärdstyp för att konfigurera händelsen och dataelementen och sedan använda **[!UICONTROL Send Beacon]** för att skicka data och sedan använda **[!UICONTROL Clear Variables]** för att rensa dataspårningen.

1. I **[!UICONTROL Props]** mappa de alternativ för rapportsviten som finns i listrutan med dataelementen som definieras med [Konfigurera dataelement](#configure-data-elements).

   Till exempel att skicka **Formulärtitel** dataelement från AEM Forms till [!DNL Adobe Analytics] när du skickar in ett formulär:
   1. I **[!UICONTROL Props]** väljer du ett utkast för Formulärtitel i rapportsviten och trycker sedan på ![Databasikon](assets/database-icon.svg) för att mappa det till formulärtiteln som skapades i [Konfigurera dataelement](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Tryck **[!UICONTROL Add Another]** om du vill lägga till fler dataelement i listan.

1. I **[!UICONTROL Events]** väljer du en händelse bland de tillgängliga alternativen i rapportsviten och trycker på **[!UICONTROL Keep Changes]**.

1. I **[!UICONTROL Actions]** -sektion, tryck på + och ange **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Send Beacon]** som åtgärdstyp. Välj **[!UICONTROL s.t()]** skicka data till [!DNL Adobe Analytics] och hantera det som en sidvy eller **[!UICONTROL s.tl()]** skicka data till [!DNL Adobe Analytics] och behandla det inte som en sidvy. Tryck på **[!UICONTROL Keep Changes]**.

1. I **[!UICONTROL Actions]** -sektion, tryck på + och ange **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Clear Variables]** som åtgärdstyp. Tryck på **[!UICONTROL Keep Changes]**. När du har utfört dessa steg **[!UICONTROL Actions]** visas som:
   ![Åtgärdskonfiguration](assets/actions-config.png)

   Anpassa **[!UICONTROL Actions]** enligt dina krav. Du kan till exempel definiera två **Skicka Beacon** steg i ett åtgärdsflöde för att skicka data till [!DNL Adobe Analytics] och behandla det som en sidvy i ett enda steg och skicka data till [!DNL Adobe Analytics] och behandla det inte som en sidvy i det andra steget.

   ![Åtgärdskonfiguration](assets/actions-config-2.png)

1. Tryck **[!UICONTROL Save]** för att spara regeln.

   Du kan skapa regler för alla händelsetyper, till exempel överge, Fel, fältbesök, Hjälp, Återge, Spara och Skicka.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Publiceringsflöden {#publish-flow}

När du har skapat dataelementen och använt dem i regler publicerar du konfigurationen för att samla in formulärdata i [!DNL Adobe Analytics].

Utför följande steg för att publicera konfigurationen:

1. I **[!UICONTROL Publishing]** sektion, trycka **[!UICONTROL Publishing Flow]**.

1. Tryck **[!UICONTROL Add Library]** och ange ett namn och välj miljö för biblioteket.

1. Tryck **[!UICONTROL Add All Changed Resources]** och sedan trycka **[!UICONTROL Save & Build to Development]**.

1. I **[!UICONTROL Development]** sektion, trycka ![Fler alternativ](assets/more-options-icon.svg) och sedan trycka **[!UICONTROL Approve & Publish to Production]**.

1. Bekräfta ändringarna och publiceringsflödet visas snart i **[!UICONTROL Published]** -avsnitt.

![Publiceringsflöde](assets/publish-flow.png)

## 2. Konfigurera AEM Forms {#configure-aem-forms}

Skapa en [Adobe IMS-konfiguration med Adobe Launch som molnlösning](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Skapa startkonfiguration för Adobe {#create-adobe-launch-configuration}

Så här skapar du en konfiguration för Adobe Launch:

1. I AEM Forms Author går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Launch Configurations]**.

1. Välj en mapp för att skapa konfigurationen och tryck på **[!UICONTROL Create]**.

1. Ange en rubrik för konfigurationen i dialogrutan **[!UICONTROL Title]** fält.

1. Välj [associerad Adobe IMS-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Välj namnet på företaget som användes när [konfigurera Adobe Analytics](#Configure-adobe-analytics).

1. Markera namnet på den egenskap som skapades när [konfigurera Adobe Analytics](#install-extensions).

1. Tryck på **[!UICONTROL Save & Close]**.

1. Publicera konfigurationen.

### Aktivera [!DNL Adobe Analytics] för en anpassningsbar blankett {#enable-analytics-adaptive-form}

Används [!DNL Adobe Launch] i en befintlig adaptiv form:

1. I AEM Forms Author går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och tryck på **[!UICONTROL Properties]**.
1. I **[!UICONTROL Basic]** väljer du [konfigurationsbehållare](#create-adobe-launch-configuration) används när konfigurationen för Adobe Launch skapas.
1. Tryck på **[!UICONTROL Save & Close]**. Det adaptiva formuläret är aktiverat för [!DNL Adobe Analytics].
1. Publicera formuläret.

När du har aktiverat [!DNL Adobe Analytics] för ett anpassningsbart formulär kan du [validera](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) om det finns ett lämpligt datahändelseflöde mellan AEM Forms och [!DNL Adobe Analytics]. Integreringen av AEM Forms med Adobe Analytics är klar. Nu kan du [konfigurera och visa rapporter i Adobe Analytics](#view-reports-adobe-analytics).

### Skapa regler för att hämta anpassade händelser (valfritt) {#capture-custom-events}

Skapa regler för specifika fält i ett adaptivt formulär med regelredigeraren för att skicka analysdata från ett adaptivt formulär till [!DNL Adobe Analytics].

I en tvåstegsprocess definierar du en regel för ett fält i ett anpassningsbart format. Regeln skickar en händelse. Namnet på händelsen mappas till en anpassad hämtningshändelse i Adobe Launch.

Så här skapar du regler med hjälp av regelredigeraren i ett anpassat format:

1. Tryck på fältet och välj ![Regelredigeraren](assets/rule-editor-icon.svg) för att öppna sidan för regelredigeraren.
1. Definiera ett villkor i [!UICONTROL When] -delen av regeln.
1. I [!UICONTROL Then] regelavsnitt, markera **[!UICONTROL Dispatch Event]** från **[!UICONTROL Select Action]** nedrullningsbar lista.
1. Ange namnet på händelsen i **[!UICONTROL Type Event Name]** fält.

Om födelsedatumet till exempel är före ett visst datum skickar AEM Forms **Säkerhet** -händelse.

![Utsändningshändelse](assets/security-event.png)

Mappa händelsen till en anpassad hämtningshändelse i [!DNL Adobe Analytics]:

1. [Skapa en regel](#configure-rules).

1. I **[!UICONTROL Events]** sektion, trycka **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Capture Custom Event]** från **[!UICONTROL Event Type]** nedrullningsbar lista.

1. Ange namnet på händelsen som du angav i steg 4 när du skapade en regel med regelredigeraren.

1. Tryck **Behåll ändringar** och utför resten av åtgärderna som anges i [Konfigurera regler](#configure-rules).

## 3. Konfigurera och visa rapporter i [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

När ett adaptivt formulär har konfigurerats för att skicka händelsedata till [!DNL Adobe Analytics]kan du börja visa rapporter i [!DNL Adobe Analytics]:

1. Tryck ![Välj produkt](assets/select-analytics.png) och markera **[!UICONTROL Analytics]**.

1. Tryck **[!UICONTROL Create Project]** och markera **[!UICONTROL Blank project]**.

1. Välj rapportsvitens namn i listrutan högst upp till höger på frihandsformuläret.

1. Ange **Formulärtitel** i **[!UICONTROL Search dimension items]** text för att visa alla formulärtitlar.

1. Släpp den anpassningsbara formulärtiteln på **[!UICONTROL Drop a segment here (or any other component)]** textruta.

1. Från **[!UICONTROL Metrics]** -avsnitt, släppa händelser att spåra till **[!UICONTROL Drop a metric here (or any other component)]** textruta.

1. Tryck ![Visualiseringar](assets/visualization-icon.svg) och släpp en diagramtyp i avsnittet Frihand. På samma sätt kan du lägga till flera diagramtyper i avsnittet Frihand.

1. Tryck på Ctrl + S och ange ett namn för att spara projektet.

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
