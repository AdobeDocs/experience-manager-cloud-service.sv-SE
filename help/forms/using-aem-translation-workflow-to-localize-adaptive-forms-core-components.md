---
title: Hur kan vi översätta en grundkomponentbaserad adaptiv form?
description: Lär dig skapa en formulärdatamodell (FDM) i AEM Forms, testa modellen med exempeldata och tjänster och konfigurera olika alternativ för en modell.
feature: Adaptive Forms, Core Components
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Använd maskinöversättning eller mänsklig översättning för att översätta en grundläggande komponentbaserad adaptiv form {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Lokaliserade formulär hjälper er att nå en större publik över alla länder. Adobe Experience Manager arbetsflöde för översättning hjälper dig att lokalisera adaptiva Forms och deras urkunder. Du kan använda **maskinöversättning** eller **mänskliga översättare** för att lokalisera ett adaptivt formulär.

## Översätta ett anpassat formulär och dokument med hjälp av maskinöversättning {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Maskinöversättningstjänsten översätter ditt innehåll omedelbart i Adaptiv form och [Postdokument](/help/forms/generate-document-of-record-core-components.md). AEM Forms as a Cloud Service är förkonfigurerat att använda en testversion av Microsoft Translator för maskinöversättning. Utför följande steg för att aktivera maskinöversättning för ditt adaptiva Forms och arkivdokument:

1. Markera ett formulär i användargränssnittet för AEM Forms och välj alternativet **[!UICONTROL Add Dictionary]**.
1. På skärmen Lägg till ordlista i översättningsprojekt finns alternativet **[!UICONTROL Project]**

   * Om du vill skapa ett översättningsprojekt väljer du alternativet **[!UICONTROL Create a new translation project]** och anger titeln i fältet **Projektnamn**. Exempel: `Government Reference Site - German locale.`
   * Om du vill lägga till en ny ordlista i ett befintligt översättningsprojekt markerar du alternativet **[!UICONTROL Add to an existing translation project]** och väljer **[!UICONTROL Existing translation project]**.
1. I fältet **Målspråk** anger du en språkinställning (till exempel `German(de)`). Du kan ange flera språkinställningar. Formuläret översätts till alla språk som anges i fältet **Målspråk**. Klicka på **Klar**.
1. Klicka på **Öppna projekt** i dialogrutan Lexikon tillagd.
1. Klicka på det skapade projektet på skärmen Projekt. Klicka till exempel på **Referenswebbplats för myndigheter - tyska språkområdet**.
1. Klicka på ikonen ![aem62forms_down](assets/aem62forms_downarrow.png) på panelen **Översättningsjobb** och klicka sedan på **Start** . Status för rutan ändras till Utkast. När översättningen är klar ändras statusen till **Godkänd**. Uppdatera sidan efter några minuter och kontrollera statusen.

   ![Starta översättning](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. När statusen har ändrats till **Godkänd** på panelen **Översättningsjobb** klickar du på ikonen ![aem62forms_download](assets/aem62forms_downarrow.png) och sedan på **Fullständig** .

1. Om du vill förhandsgranska det lokaliserade formuläret väljer du det lokaliserade formuläret i användargränssnittet i AEM Forms. Klicka på **[!UICONTROL Preview]** >**[!UICONTROL Preview as HTML]**. Öppna formuläret igen när du har lagt till `afAcceptLang=<locale code>` i formulärets URL. Lägg till exempel till `afAcceptLang=de` för att öppna den tyska versionen av formuläret.


   >[!NOTE]
   >
   >* Innan du öppnar den lokaliserade versionen av formuläret i webbläsarfönstret kontrollerar du att webbläsarens språkområde är inställt så att det matchar formulärets språkområde. Om formuläret t.ex. översätts till tyskt(de)-språk anger du språket för webbläsaren till tyskt(de).
   >* Anpassade formulärkomponenter har inte stöd för RTL-språk (right to left). Till exempel hebreiska.

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, select Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## Lokalisera en anpassningsbar form och dess urkunder med mänsklig översättning {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

I Personlig översättning skickas innehållet till en översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.

För översättning delas en ordlista som innehåller filer i XLIFF-format med de professionella översättarna. Ordlistan innehåller en separat XLIFF-fil för varje språkområde. Varje XLIFF-fil innehåller text som visas för slutanvändarna och platshållarna för motsvarande lokaliserad text.

Utför följande steg för att lokalisera ett formulär och dess urkunder med personalöversättare:

1. Markera ett formulär i användargränssnittet för AEM Forms och välj alternativet **[!UICONTROL Add Dictionary]**.
1. På skärmen Lägg till ordlista i översättningsprojekt finns alternativet **[!UICONTROL Project]**

   * Om du vill skapa ett översättningsprojekt väljer du alternativet **[!UICONTROL Create a new translation project]** och anger titeln i fältet **Projektnamn**. Exempel: `Government Reference Site - German locale.`
   * Om du vill lägga till en ny ordlista i ett befintligt översättningsprojekt markerar du alternativet **[!UICONTROL Add to an existing translation project]** och väljer **[!UICONTROL Existing translation project]**.
1. I fältet **Målspråk** anger du en språkinställning (till exempel `German(de)`). Du kan ange flera språkinställningar. Formuläret översätts till alla språk som anges i fältet **Målspråk**. Klicka på **Klar**.
1. Klicka på **Öppna projekt** i dialogrutan Lexikon tillagd.
1. Klicka på det skapade projektet på skärmen Projekt. Klicka till exempel på **Referenswebbplats för myndigheter - tyska språkområdet**.
1. Klicka på **ellipserna** längst ned i rutan **Sammanfattning**. Skärmen Egenskaper för översättningsprojekt öppnas.
1. Öppna fliken **[!UICONTROL Advanced]** högst upp på skärmen **Egenskaper för översättningsprojekt**. För **[!UICONTROL Translation field]** väljer du **[!UICONTROL Human Translation]**. Klicka på **Spara och stäng** längst upp på skärmen.
1. Klicka på ikonen ![aem62forms_down](assets/aem62forms_downarrow.png) på panelen **Översättningsjobb** och klicka på **Exportera**. I dialogrutan Exportera klickar du på alternativet Hämta exporterad fil. Den hämtar en ZIP-fil.
   ![Exportera översättningsfil](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. Extrahera den hämtade ZIP-filen. Den extraherade mappen har två filer:
   * translation_export_summary.xml
   * [form-fields-file].xml.
1. Öppna [form-fields-file].xml för redigering. Lägg till översatta strängar och meddelanden för formulärfält. Spara och stäng filen.
1. Zippa upp filerna som translation_export_summary.xml och [form-fields-file].xml.
1. Klicka på ikonen ![aem62forms_down](assets/aem62forms_downarrow.png) på panelen **Översättningsjobb** och klicka på **Importera**. Markera arkivet som innehåller [form-fields-file].xml. med lokaliserade strängar och meddelanden för formulärfält.

   ![Importera översättningsfil](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. Om du vill förhandsgranska det lokaliserade formuläret väljer du det lokaliserade formuläret i användargränssnittet i AEM Forms. Klicka på **[!UICONTROL Preview]** >**[!UICONTROL Preview as HTML]**. Öppna formuläret igen när du har lagt till `afAcceptLang=<locale code>` i formulärets URL. Lägg till exempel till `afAcceptLang=de` för att öppna den tyska versionen av formuläret.

## Se även {#see-also}

{{see-also}}