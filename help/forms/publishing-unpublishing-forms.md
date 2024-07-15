---
title: Hur publicerar och avpublicerar man blanketter och dokument i AEM?
description: Schemalägg publicering och avpublicering av din adaptiva Forms. Publicerade formulär replikeras på publiceringsinstansen.
content-type: reference
topic-tags: publish
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65s
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 0%

---


# Publicera och avpublicera formulär och dokument{#publishing-and-unpublishing-forms-and-documents}

Med [!DNL AEM Forms] kan du enkelt skapa, publicera och avpublicera formulär. Servern [!DNL AEM Forms] innehåller två instanser: Författare och Publish. Författarinstans används för att skapa och hantera formulärresurser och resurser. Publish-instans används för att hålla resurser och relaterade resurser tillgängliga för slutanvändare.

## Resurser som stöds   {#supported-assets-nbsp}

[!DNL AEM Forms] har stöd för följande typer av resurser:

* Adaptiv Forms
* Anpassningsbara dokument
* Adaptiva formulärfragment
* Teman
* Formulärmallar <!-- (XFA forms) -->
* PDF forms
* Dokument (dokument i PDF)
* Formuläruppsättningar
* Resurs (bilder, scheman och formatmallar)

Till att börja med är alla resurser bara tillgängliga i Author-instansen. En administratör eller formulärförfattare kan publicera alla resurser utom resurser.

När du markerar ett formulär och publicerar det publiceras även dess relaterade resurser och resurser. Beroende resurser publiceras dock inte. I det här sammanhanget är relaterade resurser och resurser resurser som en publicerad tillgång använder eller refererar till. Beroende resurser är resurser som refererar till en publicerad resurs.

Din adaptiva Forms kan använda vissa konfigurationer, inställningar och anpassningar som inte publiceras automatiskt. Vi rekommenderar att du publicerar eller aktiverar dessa resurser innan du publicerar ett adaptivt formulär.

* Redigerbara adaptiva formulärmallar
* Cloud Service för Adobe Sign, Typekit, reCAPTCHA och Form Data Model (FDM)
* Andra konfigurationer av molntjänster aktiveras bara om användaren har administratörsbehörighet.
* Anpassningar. Dessa omfattar, men är inte begränsade till:

   * Anpassade layouter
   * Anpassade utseenden
   * CSS-fil - används som indata i dialogrutan med egenskaper för adaptiv formulärbehållare
   * Kategori för klientbibliotek - tas som indata i dialogrutan med egenskaper för behållare för adaptiva formulär
   * Alla andra klientbibliotek som kan ingå i mallen för adaptiva formulär.
   * Designbanor

## Tillgångstillstånd {#asset-states}

En resurs kan ha följande lägen:

* **Opublicerad:** En resurs som aldrig har publicerats (det opublicerade läget gäller endast för Forms-resurser. Resurser för korrespondenshantering har inte ett opublicerat läge.)
* **Publicerad**: En resurs som har publicerats och är tillgänglig på Publish-instansen
* **Ändrad**: En resurs som har ändrats efter att ha publicerats

## Publish en mediefil {#publish-an-asset}

1. Logga in på servern [!DNL AEM Forms].
1. Använd något av följande för att välja och publicera en resurs.

   1. Flytta pekaren över en resurs och välj **[!UICONTROL Publish]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. Gör något av följande och välj sedan Publish:

      * Om du är i kortvyn väljer du **[!UICONTROL Enter Selection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png) och väljer resursen. Resursen har valts.
      * Om du är i listvyn markerar du kryssrutan för en resurs. Resursen har valts.
      * Välj en resurs om du vill visa information om den.
      * Visa egenskaperna för en resurs genom att trycka på Visa egenskaper ![visningsegenskaper](assets/viewproperties.png).

      >[!NOTE]
      >
      >Markera inte flera resurser. Det går inte att publicera flera resurser samtidigt.

1. När Publish-processen startar visas en bekräftelsedialogruta med alla relaterade resurser och resurser. Välj **[!UICONTROL Publish]** i dialogrutan som innehåller relaterade resurser. Resursen publiceras och dialogrutan Publish Assets Success visas.

   >[!NOTE]
   >
   >Sidnamnet Adaptiv form visas även för den adaptiva Forms tillsammans med de relaterade resurserna.

   ![En bekräftelsedialogruta med alla relaterade resurser och resurser](assets/p4.png)

   En bekräftelsedialogruta med alla relaterade resurser och resurser.

   >[!NOTE]
   >
   >För Forms Manager är Publish-åtgärden inaktiverad om användaren inte har behörighet att publicera resurserna i listan. En resurs som kräver extra behörigheter visas i rött.

   När en resurs har publicerats kopieras resursens metadataegenskaper till Publish-instansen och resursens status ändras till Publicerad. Statusen för beroende resurser som publiceras ändras också till Publicerad.

   <!-- After publishing an asset, you can use the Forms Portal to display all the assets on a web page. For more information, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md).-->

## Publish all Correspondence Management Assets {#publish-all-the-correspondence-management-assets}

Med [!DNL AEM Forms] kan du publicera alla Correspondence Management-resurser på en server på en gång. De publicerade resurserna innehåller alla Correspondence Management-resurser och relaterade beroenden.

Följ de här stegen för att publicera alla Correspondence Management-resurser på en server:

1. Logga in på servern [!DNL AEM Forms].
1. Välj **Adobe Experience Manager** i det globala navigeringsfältet.
1. Välj ![verktyg](assets/tools.png) och sedan **Forms**.
1. Välj **Publish Correspondence Management Assets**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   Assets-sidan Publish All Correspondence Management visas och innehåller information om den senaste gången Publish Correspondence Management Assets-processen gjordes.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Välj **Publish** och välj **OK** i bekräftelsemeddelandet.

   När en gruppbearbetning är klar kan du visa information om den senaste körningen. Detta inkluderar information som administratörsinloggning och om batchkörningen lyckades eller misslyckades.

   >[!NOTE]
   >
   >Publish-processen kan inte avbrytas när den väl har initierats. När Publish-åtgärden pågår ska du inte skapa, ta bort, ändra eller publicera något material eller initiera Assets-åtgärden Exportera all korrespondenshantering.

## Automatisera publicering och avpublicering för Forms &amp; Documents {#automate-publishing-and-unpublishing-for-forms-amp-documents}

I [!DNL AEM Forms] kan du schemalägga publicering och avpublicering av resurser för Forms &amp; Documents. Du kan ange schemat i metadataredigeraren. Mer information om hur du hanterar metadata för formulär finns i [Hantera metadata för formulär.](manage-form-metadata.md)

Följ de här stegen för att schemalägga datum och tid för publicering och avpublicering av Forms- och dokumentresurser:

1. Välj en resurs och välj **[!UICONTROL View Properties]**. Sidan Metadataegenskaper öppnas.
1. På sidan Metadataegenskaper väljer du **[!UICONTROL Advanced]** och sedan **[!UICONTROL Edit]** ![illustrator_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. Välj datum och tid i fälten **[!UICONTROL Publish On Time]** och **[!UICONTROL Publish Off Time]**.\
   Välj **[!UICONTROL Done]** ![aem6forms_check](assets/aem6forms_check.png).

## Avpublicera en resurs {#unpublish-an-asset}

1. Välj en publicerad resurs och välj **[!UICONTROL Unpublish]** ![unpublish](assets/unpublish.png).
1. Använd något av följande för att välja och avpublicera en resurs.

   1. Flytta pekaren över en resurs och välj **[!UICONTROL Unpublish]** ![unpublish](assets/unpublish.png).
   1. Gör något av följande och välj sedan Avpublicera:

      * Om du är i kortvyn väljer du **[!UICONTROL Enter Selection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png) och väljer resursen. Resursen har valts.

      * Om du är i listvyn håller du pekaren över en resurs och väljer ![selectAssetCheckMark](assets/selectassetcheckmark.png) . Resursen har valts.

      * Välj en resurs om du vill visa information om den.
      * Visa egenskaperna för en resurs genom att trycka på Visa egenskaper ![visningsegenskaper](assets/viewproperties.png).

1. När avpubliceringsprocessen startar visas en bekräftelsedialogruta. Välj **[!UICONTROL Unpublish]**.

   >[!NOTE]
   >
   >Endast den markerade resursen avpubliceras och dess underordnade och refererade resurser, om det finns några, avpubliceras inte.

## Återställa en resurs eller ett brev till den tidigare publicerade versionen {#revert-an-asset-or-letter-to-the-previously-published-version}

Varje gång du publicerar en resurs eller ett brev efter att ha redigerat den skapas en version av resursen eller brevet. Du kan återställa en resurs eller ett brev till en tidigare publicerad version. Du kan behöva göra det om något blir fel med den aktuella versionen av resursen eller dokumentet.

>[!NOTE]
>
>Återställ inte ett brev till ett senast publicerat tillstånd om någon beroende resurs som används i det publicerade brevet tas bort från systemet.

1. Markera en resurs och välj **[!UICONTROL Revert to Previously Published Version]** ![omvända, publicerade versioner](assets/reverttopreviouslypublishedversion.png).
1. Innan resursen återställs visas en bekräftelsedialogruta. Välj **[!UICONTROL Revert]**.

   Resursen eller bokstaven återställs till den tidigare publicerade versionen.

## Ta bort en resurs {#delete-an-asset}

>[!NOTE]
>
>Om du tar bort en resurs tas den bort från publiceringsinstansen. När du tar bort ett objekt tas även dess versionshistorik bort, förutom basversionen.

1. Markera en resurs och välj **[!UICONTROL Delete]** ![delete](assets/delete.png).

   >[!NOTE]
   >
   >Alternativet Ta bort är också tillgängligt när du visar resursinformation genom att trycka på en resurs eller genom att trycka på ![Visa egenskaper](assets/viewproperties.png) för en resurs.

1. Innan resursen tas bort visas en bekräftelsedialogruta. Välj **[!UICONTROL Delete]**.

   >[!NOTE]
   >
   >Endast den markerade resursen tas bort och de beroende resurserna tas inte bort. Om du vill kontrollera referenser till en resurs väljer du ![referenser](assets/references.png) och sedan en resurs.
   >
   >
   >Om den resurs du försöker ta bort är underordnad en annan resurs tas den inte bort. Om du vill ta bort en sådan resurs tar du bort referenser till den från andra resurser och försöker sedan igen.

## Skyddad adaptiv Forms {#protected-adaptive-forms}

Du kan aktivera autentisering för formulär som du vill att valda användare ska ha åtkomst till. När du aktiverar autentisering för dina formulär visas en inloggningsskärm innan användarna kan komma åt dem. Endast användare med autentiseringsuppgifter som är behöriga kan komma åt formulären.

Så här aktiverar du autentisering för dina formulär:

1. Öppna configMgr i publiceringsinstansen i webbläsaren.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Klicka på **Apache Sling Authentication Service** i Adobe Experience Manager Web Console Configuration för att konfigurera den.
1. I dialogrutan Apache Sling Authentication Service som visas använder du knappen **+** för att lägga till sökvägar.\
   När du lägger till en sökväg aktiveras autentiseringstjänsten för formulär i den sökvägen.
