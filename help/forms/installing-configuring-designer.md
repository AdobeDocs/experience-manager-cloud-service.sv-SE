---
title: Hur laddar man ned och installerar Forms Designer för att skapa dokumentmallar?
description: Använd Forms Designer för att skapa XDP- och PDF-blankettmallar som fungerar som mall för ett arkivdokument.
keywords: Installera Designer, installera Forms Designer, krav för installation av Forms Designer
exl-id: d6f1cb21-c48b-406d-8d47-482d7a1b4cc3
source-git-commit: 397e7d4f23202b8ae7419b0ad5436a6a10e2efb8
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Hämta och installera Forms Designer {#installing-and-configuring-designer}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Den här artikeln |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/installing-configuring-designer.html) |

Designer är ett grafiskt formulärdesignverktyg som gör det enklare att skapa XDP- och PDF-formulärmallar. Du kan utforma en formulärmall, definiera dess logik och uppfylla strikta lagstadgade krav. Ett XDP- och PDF-formulär fungerar som en dokumentmall i ett adaptivt format. Dessa formulärmallar skiljer sig från [Adaptiva formulärmallar](template-editor.md).

## Krav {#pre-requisites}

För att kunna installera den senaste versionen av AEM Forms Designer, 64-bitars eller 32-bitars, krävs följande programvara och maskinvara för att installera och konfigurera Designer:

+++ 64-bitars Designer (rekommenderas)

* [!DNL Microsoft® Windows® 2016 Server] eller [!DNL Microsoft® Windows® 2019 Server]och [!DNL Microsoft® Windows® 10]
* Minst 2 GB RAM
* 20 GB diskutrymme
* Grafikminne - 128 MB GPU (256 MB rekommenderas)
* 2,35 GB ledigt hårddiskutrymme
* Bildskärmsupplösning på 1 024 x 768 pixlar eller högre
* Maskinvaruacceleration för video (valfritt)
* Acrobat Pro DC, Acrobat Standard DC eller Adobe Acrobat Reader DC.
* Administrativ behörighet för att installera Designer.
* [!DNL Microsoft® Visual C++ 2019] (VC 14.28 eller senare) 64-bitars runtime

+++

+++ 32-bitars Designer

* [!DNL Microsoft® Windows® 2016 Server], [!DNL Microsoft® Windows® 2019 Server], eller [!DNL Microsoft® Windows® 10]
* 1 GB RAM för 32-bitars OS eller 2 GB RAM för 64-bitars OS
* 16 GB diskutrymme för 32-bitars operativsystem eller 20 GB för 64-bitars operativsystem
* Grafikminne - 128 MB GPU (256 MB rekommenderas)
* 2,35 GB ledigt hårddiskutrymme
* Bildskärmsupplösning på 1 024 x 768 pixlar eller högre
* Maskinvaruacceleration för video (valfritt)
* Acrobat Pro DC, Acrobat Standard DC eller Adobe Acrobat Reader DC.
* Administrativ behörighet för att installera Designer.
* Microsoft® Visual C++ 2019 (VC 14.28 eller senare) 32-bitars runtime

+++

## Installera Designer {#install-designer}

>[!NOTE]
>
> Avinstallera 32-bitarsversionen av Designer innan du installerar 64-bitarsversionen av Forms Designer.

Så här installerar du Designer:

1. Hämta Designer från [Programvarudistribution](https://experience.adobe.com/downloads).
1. Dubbelklicka på setup.exe för att köra installationsprogrammet.
1. Gå vidare och ange dina uppgifter på skärmen Personalisering.
1. Om du godkänner licensavtalet klickar du på **[!UICONTROL Next]** för att fortsätta.
1. (Valfritt) ändra standardinstallationssökvägen för att installera Designer på en valfri plats. Klicka på **[!UICONTROL Next]**.
1. Klicka **[!UICONTROL Back]** om du vill ändra några inställningar. Installera Designer genom att klicka **[!UICONTROL Install]**.
1. Klicka **[!UICONTROL Finish]** när installationen är klar.

## Se även {#see-also}

* [Använda anpassade teckensnitt](/help/forms/use-custom-fonts.md)
* [Skapa en fristående grundkomponentbaserad adaptiv form](/help/forms/creating-adaptive-form-core-components.md)
* [Skapa eller lägga till ett anpassat formulär på AEM Sites-sidan](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Använd Forms Designer för att skapa DoR-mallar och formulärfragment](/help/forms/use-forms-designer.md)


<!--

>[!MORELIKETHIS]
>
>* [Use Forms Designer to create Document of Record (DoR) templates and form fragments](/help/forms/use-forms-designer.md)

-->