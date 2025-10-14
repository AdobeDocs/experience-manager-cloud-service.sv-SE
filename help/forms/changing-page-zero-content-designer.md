---
title: Hur ändrar man Page Zero-innehåll i Designer?
description: Ändra meddelandet som visas på sidnoll i en XFA-PDF för visningsprogram som inte kommer från Adobe PDF.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Ändra sidans nollinnehåll i Designer {#changing-page-zero-content-in-designer}

Sidnollinnehåll visas som standard när ett visningsprogram som inte är från Adobe PDF, t.ex. PDF i [!DNL Chrome] eller [!DNL Firefox] som är standard, inte kan läsa innehållet i formuläret PDF/XFA. Standardmeddelandet Sidan är noll visas nedan.

![standardsida0meddelande](assets/defaultpage0message.png)

[!DNL AEM Forms]-versionen av Designer låter dig ändra meddelandet som visas på sidan noll. Gör så här om du vill ändra sidans nollmeddelande:

1. Kontrollera att du har [!DNL AEM Forms]-versionen av Designer installerad. Du kan kontrollera versionen från Om-skärmen i Designer.

1. Öppna formuläret som du vill ändra sidans nollinnehåll för.

1. Klicka på **[!UICONTROL File]** > **[!UICONTROL Form Properties]**.

1. I dialogrutan [!UICONTROL Form Properties] klickar du på ![&#x200B; plus](assets/plus.png) (plusikonen) för att lägga till en anpassad egenskap.

1. Ange **_pagezerocontent** som egenskapens namn.
1. Lägg till det nya sidans nollmeddelande i RTF-format som värde. Till exempel:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download_se.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Spara formuläret som PDF.

1. Visa formuläret PDF i webbläsaren för att bekräfta att meddelandet har uppdaterats. Exempelvärdet ovan ser ut så här:

   ![ändrat meddelande](assets/changedmessage.png)

>[!NOTE]
>
>Den anpassade egenskap som du skapade kanske inte visas korrekt i dialogrutan Formuläregenskaper när du öppnar formuläret igen. Det fungerar dock bra och formuläret visar det uppdaterade sidnollmeddelandet.

>[!MORELIKETHIS]
>
>* [Hämta och installera Forms Designer för att skapa dokumentmallar](/help/forms/installing-configuring-designer.md)
>* [Använd Forms Designer för att skapa DoR-mallar (Document of Record) och formulärfragment?](/help/forms/use-forms-designer.md)
