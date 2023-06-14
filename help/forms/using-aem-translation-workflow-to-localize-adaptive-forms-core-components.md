---
title: Översätt en huvudkomponentbaserad adaptiv form
description: Använd maskinöversättning eller mänsklig översättning för att översätta en grundläggande komponentbaserad adaptiv form
feature: Adaptive Forms
source-git-commit: a33b380570210a32f4a4a1f26c9a2fe37c885bb1
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Använd maskinöversättning eller mänsklig översättning för att översätta en grundläggande komponentbaserad adaptiv form {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Lokaliserade formulär hjälper er att nå en större publik över alla länder. Adobe Experience Manager arbetsflöde för översättning hjälper dig att lokalisera adaptiva Forms och deras urkunder. Du kan använda **maskinöversättning** eller **mänskliga översättare** för att lokalisera ett adaptivt formulär.

## Översätta ett anpassat formulär och dokument med hjälp av maskinöversättning {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Maskinöversättningstjänsten översätter omedelbart ditt innehåll i adaptiv form och [Dokument](/help/forms/generate-document-of-record-core-components.md). AEM Forms as a Cloud Service är förkonfigurerat för att använda en testversion av Microsoft Translator för maskinöversättning. Utför följande steg för att aktivera maskinöversättning för ditt adaptiva Forms och arkivdokument:

1. I AEM Forms-gränssnittet väljer du ett formulär och trycker på **[!UICONTROL Add Dictionary]** alternativ.
1. På skärmen Lägg till ordlista i översättningsprojekt finns följande i **[!UICONTROL Project]** option

   * Om du vill skapa ett översättningsprojekt väljer du **[!UICONTROL Create a new translation project]** och i **Projektets titel** anger du rubriken. Till exempel, `Government Reference Site - German locale.`
   * Om du vill lägga till en ny ordlista i ett befintligt översättningsprojekt väljer du **[!UICONTROL Add to an existing translation project]** och välja **[!UICONTROL Existing translation project]**.
1. I **Målspråk** anger du nationella inställningar (till exempel `German(de)`). Du kan ange flera språkinställningar. Formuläret översätts till alla språkområden som anges i **Målspråk** fält. Klicka **Klar**.
1. I dialogrutan Lexikon tillagd klickar du på **Öppna projekt**.
1. Klicka på det nyligen skapade projektet på skärmen Projekt. Klicka till exempel på **Statlig referenswebbplats - tyska språk** platta.
1. På **Översättningsjobb** platta, klicka på ![aem62forms_down](assets/aem62forms_downarrow.png) och klicka **Starta**. Status för rutan ändras till Utkast. När översättningen är klar ändras statusen till **Godkänd**. Uppdatera sidan efter några minuter och kontrollera statusen.

   ![Starta översättning](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. Efter statusändringen ändras till **Godkänd** på **Översättningsjobb** platta, klicka på ![aem62forms_down](assets/aem62forms_downarrow.png) och klicka **Slutförd**.

1. Om du vill förhandsgranska det lokaliserade formuläret väljer du det lokaliserade formuläret i användargränssnittet i AEM Forms. Klicka på **[!UICONTROL Preview]** >**[!UICONTROL Preview as HTML]**. Öppna formuläret igen när du har lagt till `afAcceptLang=<locale code>` till formulärets URL. Lägg till exempel `afAcceptLang=de`för att öppna den tyska versionen av formuläret.


   >[!NOTE]
   >
   >* Innan du öppnar den lokaliserade versionen av formuläret i webbläsarfönstret kontrollerar du att webbläsarens språkområde är inställt så att det matchar formulärets språkområde. Om formuläret t.ex. översätts till tyskt(de)-språk anger du språket för webbläsaren till tyskt(de).
   >* Adaptiva formulärkomponenter har inte stöd för RTL-språk. Till exempel hebreiska.

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, tap Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## Lokalisera en anpassningsbar form och dess urkunder med mänsklig översättning {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

I Personlig översättning skickas innehållet till en översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.

För översättning delas en ordlista som innehåller filer i XLIFF-format med de professionella översättarna. Ordlistan innehåller en separat XLIFF-fil för varje språkområde. Varje XLIFF-fil innehåller text som visas för slutanvändarna och platshållarna för motsvarande lokaliserad text.

Utför följande steg för att lokalisera ett formulär och dess urkunder med personalöversättare:

1. I AEM Forms-gränssnittet väljer du ett formulär och trycker på **[!UICONTROL Add Dictionary]** alternativ.
1. På skärmen Lägg till ordlista i översättningsprojekt finns följande i **[!UICONTROL Project]** option

   * Om du vill skapa ett översättningsprojekt väljer du **[!UICONTROL Create a new translation project]** och i **Projektets titel** anger du rubriken. Till exempel, `Government Reference Site - German locale.`
   * Om du vill lägga till en ny ordlista i ett befintligt översättningsprojekt väljer du **[!UICONTROL Add to an existing translation project]** och välja **[!UICONTROL Existing translation project]**.
1. I **Målspråk** anger du nationella inställningar (till exempel `German(de)`). Du kan ange flera språkinställningar. Formuläret översätts till alla språkområden som anges i **Målspråk** fält. Klicka **Klar**.
1. I dialogrutan Lexikon tillagd klickar du på **Öppna projekt**.
1. Klicka på det nyligen skapade projektet på skärmen Projekt. Klicka till exempel på **Statlig referenswebbplats - tyska språk** platta.
1. Längst ned på **Sammanfattning** platta, klicka på **ellipser**. Skärmen Egenskaper för översättningsprojekt öppnas.
1. Öppna **[!UICONTROL Advanced]** överst på **Egenskaper för översättningsprojekt** skärm. För **[!UICONTROL Translation field]**, markera **[!UICONTROL Human Translation]**. Klicka **Spara och stäng** längst upp på skärmen.
1. På **Översättningsjobb** platta, klicka på ![aem62forms_down](assets/aem62forms_downarrow.png) och klicka **Exportera**. I dialogrutan Exportera klickar du på alternativet Hämta exporterad fil. Den hämtar en ZIP-fil.
   ![](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. Extrahera den hämtade ZIP-filen. Den extraherade mappen har två filer:
   * translation_export_summary.xml
   * [form-fields-file].xml.
1. Öppna [form-fields-file].xml för redigering. Lägg till översatta strängar och meddelanden för formulärfält. Spara och stäng filen.
1. Zippa filerna som translation_export_summary.xml och [form-fields-file].xml.
1. På **Översättningsjobb** platta, klicka på ![aem62forms_down](assets/aem62forms_downarrow.png) och klicka **Importera**. Välj arkivet som innehåller [form-fields-file].xml. med lokaliserade strängar och meddelanden för formulärfält.

   ![](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. Om du vill förhandsgranska det lokaliserade formuläret väljer du det lokaliserade formuläret i användargränssnittet i AEM Forms. Klicka på **[!UICONTROL Preview]** >**[!UICONTROL Preview as HTML]**. Öppna formuläret igen när du har lagt till `afAcceptLang=<locale code>` till formulärets URL. Lägg till exempel `afAcceptLang=de`för att öppna den tyska versionen av formuläret.