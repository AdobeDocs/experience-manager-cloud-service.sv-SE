---
title: Hur anpassar man automatiskt genererad dokumentmall för Adaptive Forms?
description: Lär dig hur du hämtar, anpassar och överför den automatiskt genererade dokumentmallen (DoR) för Adaptive Forms med Adobe Forms Designer.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer
source-git-commit: 51ec9ef76a8f3f9b7bf2cdc25b03f72e286f586f
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# Anpassa den automatiskt genererade dokumentmallen

<span class="preview"> Den här artikeln gäller både **Core Components** och **Foundation Components**-baserade Adaptive Forms.</span>

När du genererar ett dokument för post (DoR) automatiskt för ett anpassat formulär, skapar AEM Forms en standardmall baserad på formulärstrukturen. Du kan anpassa den här automatiskt genererade mallen så att den matchar organisationens krav på varumärke och layout.

Arbetsflödet för anpassning omfattar tre steg:

1. Hämta den automatiskt genererade DoR-mallen från Forms Manager.
1. Ändra mallen med Adobe Forms Designer.
1. Ladda upp den anpassade mallen på nytt till AEM Forms och konfigurera den som en anpassad mall.

## Förutsättningar {#prerequisites}

Innan du börjar bör du kontrollera att du har följande:

* Tillgång till AEM Forms Manager med behörighet att hämta och överföra mallar.
* Adobe Forms Designer är installerat på din dator.
* Ett anpassat formulär med **[!UICONTROL Generate Document of Record]** aktiverat.

## Steg 1: Hämta den automatiskt genererade DoR-mallen {#download-auto-generated-dor-template}

Så här hämtar du den automatiskt genererade DoR-mallen (XDP-filen) för ditt adaptiva formulär:

1. Logga in på din AEM Forms-författarinstans.
1. Navigera till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj det adaptiva formulär som du vill hämta DoR-mallen för.
1. Öppna egenskaperna för det markerade adaptiva formuläret.
1. På egenskapspanelen väljer du alternativet **[!UICONTROL Download Document of Record]** för att hämta den automatiskt genererade DoR-mallen (XDP-fil).
1. Spara den hämtade XDP-filen på den lokala datorn.


## Steg 2: Anpassa mallen med Adobe Forms Designer {#customize-template-using-designer}

Öppna den hämtade XDP-mallen i Adobe Forms Designer och ändra den efter behov.

1. Öppna den hämtade XDP-filen i **Adobe Forms Designer**.
1. Anpassa mallen efter behov. Exempel på anpassningar är:

   * **Flera mallsidor**: Lägg till ytterligare mallsidor för att definiera olika layouter för specifika sidor i dokumentets arkivhandling. Använd till exempel en distinkt första sida med ett brevhuvud och efterföljande sidor med en enklare layout.
   * **Teckensnittsfärger och teckensnittsfamiljer**: Ändra teckensnittsfärg, storlek och familj så att de överensstämmer med företagets grafiska profil.
   * **Anpassade element**: Lägg till element som företagslogotyper, sidhuvuden, sidfötter och ansvarsfriskrivningstext för att skapa en enhetlig varumärkesidentitet.
   * **Sidlayout och format**: Justera marginaler, mellanrum och den övergripande sidstrukturen för att förbättra läsbarheten.
   * **Fältformat och placering**: Ändra utseendet och placeringen för formulärfält så att de matchar den önskade layouten.

1. Spara den anpassade XDP-mallen.

>[!NOTE]
>
> Ta inte bort eller ändra inga skript som finns i mallen. Om du ändrar skript kan det påverka databindningen och dokumentgenereringen.

## Steg 3: Överför den anpassade mallen till AEM igen {#reupload-customized-template}

När du har anpassat mallen överför du den till AEM Forms och konfigurerar det adaptiva formuläret så att det kan användas.

1. Överför den anpassade XDP-mallen till din AEM Forms-instans:
   * Navigera till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
   * Välj **[!UICONTROL Create]** > **[!UICONTROL File Upload]** och överför den anpassade XDP-filen.

Konfigurera sedan formuläret att använda den anpassade mallen. Stegen varierar beroende på om formuläret är baserat på kärnkomponenter eller grundkomponenter.

>[!BEGINTABS]

>[!TAB Kärnkomponenter]

För adaptiva Forms baserade på kärnkomponenter:

1. Öppna det adaptiva formuläret i redigeraren som du vill använda den anpassade mallen för.
1. Markera **[!UICONTROL Guide Container]** (rotpanelen) i innehållsträdet.
1. Öppna **[!UICONTROL Properties]** och klicka på ikonen **[!UICONTROL Document of Record]** (DoR) för att öppna egenskaperna för postdokument.
1. Öppna listrutan **[!UICONTROL Basic]** på fliken **[!UICONTROL Template]** och välj **[!UICONTROL Custom]**.
1. Bläddra och välj den överförda anpassade XDP-mallen.
1. Markera kryssrutan som ska sparas.

   ![Postdokument - mall inställd på anpassad (kärnkomponenter)](/help/forms/assets/submission-pdf-dor-custom-template.png)

>[!TAB Foundation Components]

För adaptiva Forms baserade på Foundation Components:

1. Öppna det adaptiva formuläret i redigeraren som du vill använda den anpassade mallen för.
1. Markera rotpanelen (formulärbehållaren).
1. Öppna **[!UICONTROL Document of Record Properties]** (från egenskapspanelen eller fliken DoR).
1. Öppna listrutan **[!UICONTROL Basic]** på fliken **[!UICONTROL Template]** och välj **[!UICONTROL Custom]**.
1. Bläddra och välj den överförda anpassade XDP-mallen.
1. Välj **[!UICONTROL Done]** att spara.

   ![Postdokument - mall inställd på anpassad (Foundation Components)](/help/forms/assets/dor-custom-template-foundation-components.png)

>[!ENDTABS]

Det anpassade formuläret använder nu den anpassade mallen när det genererar postdokumentet.

## Verifiera den anpassade mallen {#verify-customized-template}

Så här bekräftar du att den anpassade mallen används korrekt:

1. Skicka en testpost för det adaptiva formuläret.
1. Generera ett postdokument.
1. Kontrollera att den genererade PDF återspeglar dina anpassningar, inklusive logotyper, teckensnitt, layoutändringar och andra grafiska profiler.

## Felsökning {#troubleshooting}

| Problem | Upplösning |
|---|---|
| Den anpassade mallen överförs inte. | Kontrollera att XDP-filen är giltig och inte skadad. Kontrollera att du har behörighet att överföra filer till AEM Forms. |
| Anpassningar visas inte i det genererade postdokumentet. | Bekräfta att du har valt rätt anpassad mall i avsnittet **[!UICONTROL Document of Record Template Configuration]** i formuläregenskaperna. |
| Problem med layout eller formatering i den genererade PDF-filen. | Kontrollera att anpassningarna i Adobe Forms Designer följer [grundmallskonventionerna](/help/forms/generate-document-of-record-core-components.md#base-template-conventions). Kontrollera att alla element är korrekt placerade i mallstrukturen. |

## Se även {#see-also}

* [Generera urkunder för adaptiva Forms (kärnkomponenter)](/help/forms/generate-document-of-record-core-components.md)
* [Generera urkunder för adaptiva Forms (grundkomponenter)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Basmall för ett postdokument](/help/forms/generate-document-of-record-core-components.md#base-template-of-a-document-of-record)
* [Anpassa varumärkesinformationen i arkivdokumentet](/help/forms/generate-document-of-record-core-components.md#customize-the-branding-information-in-document-of-record)

