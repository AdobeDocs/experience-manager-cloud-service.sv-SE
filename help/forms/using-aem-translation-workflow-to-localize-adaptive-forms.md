---
title: Hur använder man AEM översättningsarbetsflöde för att lokalisera adaptiva Forms och arkivdokument?
description: AEM översättningsarbetsflöde hjälper dig att lokalisera adaptiva Forms och deras urkunder med hjälp av maskinöversättning eller mänsklig översättning.
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Lokalisera anpassningsbara Forms och arkivdokument{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Lokaliserade formulär hjälper er att nå en större publik över alla länder. Adobe Experience Manager arbetsflöde för översättning hjälper dig att lokalisera adaptiva Forms och deras urkunder. Du kan använda **maskinöversättning** eller **mänskliga översättare** för att lokalisera ett adaptivt formulär.

I den här artikeln förklaras hur du använder AEM översättningsarbetsflöde med Adaptiv Forms och urkunder.

## Lokalisera ett adaptivt formulär och dokument med hjälp av maskinöversättning {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Maskinöversättningstjänsten översätter omedelbart ditt innehåll i Adaptiv form och Dokumentdokument. [!DNL AEM Forms] är förkonfigurerad att använda en testversion av [!DNL Microsoft Translator] för maskinöversättning. Utför följande steg för att aktivera maskinöversättning för ditt adaptiva Forms och arkivdokument:

1. På [!DNL AEM Forms] Välj ett formulär och tryck på **Lägg till ordlista** alternativ.
1. I **Lägg till ordlista i översättningsprojekt** väljer du **Skapa ett nytt översättningsprojekt** eller **Lägg till i ett befintligt översättningsprojekt** alternativ.
1. I **Projektets titel** anger du rubriken. Till exempel, `Government Reference Site - German locale.`
1. I **Målspråk** anger du nationella inställningar (till exempel `German(de)`) och klicka på **Klar**. Du kan ange flera språkinställningar. Formuläret översätts till alla språkområden som anges i **Målspråk** fält.
1. I dialogrutan Lexikon tillagd klickar du på **Öppna projekt**. Öppna det nyskapade projektet på projektskärmen.
1. Klicka på **ellipser** längst ned i **Översättningssammanfattning** platta. Skärmen Översättningssammanfattning öppnas.
1. Klicka på **Redigera** ikonen längst upp på **Översättningssammanfattning** skärm. Öppna **Översättning** och välj Maskinöversättning i **Översättningsmetod** skärm. Välj lämplig **Översättningsprovider** och **Molnkonfiguration**. Klicka på **Klar** ikonen längst upp på skärmen.
1. På **Översättningsjobb** platta, klicka på ![aem62forms_down](assets/aem62forms_downarrow.png) och klicka på **Starta**. Status för rutan ändras till Utkast. När översättningen är klar ändras statusen till **Klar för granskning**. Uppdatera sidan efter några minuter och kontrollera statusen.
1. Efter statusändringen ändras till **Klar för granskning** på **Översättningsjobb** öppnar du formuläret i ett webbläsarfönster. En lokaliserad version av formuläret visas.

   >[!NOTE]
   >
   >* Innan du öppnar den lokaliserade versionen av formuläret i webbläsarfönstret kontrollerar du att webbläsarens språkområde är inställt så att det matchar formulärets språkområde. Om formuläret t.ex. översätts till tyskt(de)-språk anger du språket för webbläsaren till tyskt(de).
   >* Adaptiva formulärkomponenter har inte stöd för RTL-språk. Till exempel hebreiska.

   Tillsammans med det adaptiva formuläret är det automatiskt genererade arkivdokumentet också lokaliserat.

   Mer information om inställningar och konfiguration för dokument för post finns i:

[Konfiguration av dokumentmall](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Dokumentinställningar](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Anpassa varumärkesinformationen i arkivdokumentet](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) och se till att webbläsarens språkområde är inställt på samma språk som du har lokaliserat det adaptiva formuläret med hjälp av datorspråket. Webbläsarens språkområde hjälper till att lokalisera varumärkesinformationen i arkivdokumentet.
1. Om du vill visa det lokaliserade postdokumentet trycker du på Generera förhandsgranskning. Dokumentet på PDF skapas och öppnas på en ny flik i webbläsaren.

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that is displayed to the end users and placeholders for the corresponding localized text.

Perform the following steps to localize a form and its Document of Record using Human Translators:

1. [Connect AEM with your translation service provider](/help/sites-administering/tc-tic.md) and [create translation integration framework configurations](/help/sites-administering/tc-tic.md).

1. [Associate the pages of your language master](/help/sites-administering/tc-tic.md) with the translation service and framework configurations.

1. [Identify the type of content](/help/sites-administering/tc-rules.md) to translate.

1. [Prepare the content for translation](/help/sites-administering/tc-prep.md) by authoring the language master and creating the root pages of language copies.

1. [Create translation projects](/help/sites-administering/tc-manage.md) to gather the content to translate and to prepare the translation process.

1. Use the translation projects to [manage the content translation process](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Adaptive Form components do not support right to left (RTL) languages. For example, Hebrew.
> -->

