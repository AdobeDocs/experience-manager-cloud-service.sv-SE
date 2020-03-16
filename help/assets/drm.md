---
title: Digital Rights Management i Adobe Experience Manager Assets
description: Lär dig hur du hanterar förfallotillstånd för mediefiler och information om licensierade mediefiler i AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# Hantering av digitala rättigheter i Experience Manager Assets {#digital-rights-management-in-assets}

Digitala resurser är ofta kopplade till en licens, som anger användningsvillkoren och hur länge de ska användas. Eftersom Adobe Experience Manager Assets (AEM) är helt integrerat med AEM-plattformen kan ni effektivt hantera information om när mediefiler förfaller och resursstatus. Du kan även associera licensinformation med resurser.

## Resursens förfallodatum {#asset-expiration}

Att mediefiler förfaller är ett effektivt sätt att genomdriva licenskrav för mediefiler. Det säkerställer att den publicerade resursen inte publiceras när den upphör att gälla, vilket förhindrar eventuella brott mot licensen. En användare utan administratörsbehörighet kan inte redigera, kopiera, flytta, publicera och hämta en utgången resurs.

Du kan visa förfallostatusen för en resurs på följande platser:

* **Kortvy**: För en resurs som har gått ut visas en flagga på kortet som anger att den har gått ut.
* **Listvy**: För förfallna mediefiler visas bannern **[!UICONTROL Status]** i kolumnen **[!UICONTROL Förfallen]** .
* **Tidslinje**: Du kan visa förfallostatusen för en resurs på tidslinjen. Markera resursen och välj Tidslinje.
* **Referensspår**: Du kan även visa förfallostatusen för resurser på **[!UICONTROL referenslisten]** . Den hanterar förfallostatus och relationer mellan sammansatta resurser och refererade delresurser, samlingar och projekt.

1. Navigera till resursen som du vill visa referenser till webbsidor och sammansatta resurser för.
1. Markera resursen och klicka/tryck på den globala navigeringsikonen.
1. Välj **[!UICONTROL Referenser]** på menyn.
1. För förfallna mediefiler visas **[!UICONTROL mediefilens förfallostatus längst upp på referenslinjen]** . Om resursen har upphört att gälla visas statusen **[!UICONTROL Tillgång har förfallna delresurser]** i referensfältet.

### Sök efter utgångna resurser {#search-expired-assets}

Du kan söka efter utgångna resurser, inklusive underresurser som gått ut, på sökpanelen.

1. Klicka på sökikonen i verktygsfältet i resurskonsolen för att visa Omnissearch-fältet.

1. Tryck på Retur när markören är i rutan Sök så visas sökresultatsidan.

1. Klicka på ikonen GlobalNav för att visa sökpanelen.

1. Click/tap the **[!UICONTROL Expiry Status]** option to expand it.

1. Välj **[!UICONTROL Förfallen]**. De förfallna resurserna visas i sökresultaten.

När du väljer alternativet **[!UICONTROL Utgånget]** visas bara de förfallna resurserna och delresurserna som sammansatta resurser refererar till i resurskonsolen. De sammansatta resurserna som refererar till utgångna delresurser visas inte omedelbart efter att delresurserna har upphört att gälla. I stället visas de när AEM Resurser har identifierat att de refererar till utgångna delresurser nästa gång som schemaläggaren körs.

Om du ändrar förfallodatumet för en publicerad resurs till ett datum som är tidigare än den aktuella schemaläggningscykeln, identifierar schemat fortfarande den här resursen som en utgången resurs nästa gång den körs och visar dess status i enlighet med detta.

Om ett fel eller fel dessutom förhindrar att schemaläggaren upptäcker förfallna resurser i den aktuella cykeln, undersöker schemaläggaren om dessa resurser i nästa cykel och identifierar deras förfallna status.

Om du vill att resurskonsolen ska visa de sammansatta resurserna tillsammans med de delresurser som har gått ut, konfigurerar du ett arbetsflöde för **[!UICONTROL Adobe CQ DAM Expiry Notification]** i AEM Configuration Manager.

1. Öppna AEM Configuration Manager.
1. Välj **[!UICONTROL Adobe CQ DAM Expiry Notification]**. Som standard är **[!UICONTROL Tidsbaserad schemaläggare]** markerad, vilket schemalägger ett jobb att vid en viss tidpunkt kontrollera om en resurs har upphört att gälla eller inte. När jobbet har slutförts visas resurser som har upphört att gälla och refererade resurser som utgångna i sökresultaten.

1. Om du vill köra jobbet regelbundet avmarkerar du fältet **[!UICONTROL Tidsbaserad schemaläggarregel]** och ändrar tiden i sekunder i fältet **[!UICONTROL Periodisk schemaläggare]** . Exempeluttrycket ”0 0 0 &amp;ast; &amp;ast; ?” utlöser till exempel jobbet kl. 00.

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. I fältet **[!UICONTROL Förhandsmeddelande i sekunder]** anger du tiden i sekunder innan en resurs förfaller när du vill få ett meddelande om förfallotiden. Om du är administratör eller den som har skapat resursen får du ett meddelande innan resursen upphör att gälla om att resursen håller på att gå ut efter den angivna tiden.

   När resursen har gått ut får du ett meddelande som bekräftar att den har gått ut. Dessutom inaktiveras utgångna resurser.

1. Click **[!UICONTROL Save]**.

## Tillgångstillstånd {#asset-states}

Resurskonsolen för Adobe Experience Manager-resurser (AEM) kan visa olika lägen för resurser. Beroende på det aktuella tillståndet för en viss resurs visas en etikett som beskriver dess tillstånd, till exempel Utgången, Publicerad, Godkänd, Avvisad och så vidare, i kortvyn.

1. Välj en resurs i användargränssnittet Resurser.

1. Tap/click the **[!UICONTROL Publish]** icon from the toolbar. If you can&#39;t see the **Publish** icon on the toolbar, tap/click **[!UICONTROL More]** on the toolbar and locate the **[!UICONTROL Publish]** icon.

1. Välj **[!UICONTROL Publicera]** på menyn och stäng sedan bekräftelsedialogrutan.
1. Avsluta markeringsläget. Publiceringsstatusen för resursen visas längst ned på miniatyrbilden av resursen i kortvyn. I listvyn visar kolumnen Publicerad den tidpunkt då resursen publicerades.

1. I resursgränssnittet markerar du en resurs och trycker/klickar på ikonen **[!UICONTROL Egenskaper]** för att visa sidan med resursinformation.

1. På fliken Avancerat anger du ett förfallodatum för resursen i fältet **[!UICONTROL Förfaller]** under.

1. Klicka på **[!UICONTROL Spara]** och sedan på **[!UICONTROL Stäng]** för att visa resurskonsolen.
1. Publiceringsstatusen för resursen anger att den har upphört att gälla längst ned på miniatyrbilden av resursen i kortvyn. I listvyn visas resursens status som **[!UICONTROL Förfallen]**.

1. I resurskonsolen väljer du en mapp och skapar en granskningsåtgärd för mappen.
1. Granska och godkänn/avvisa resurserna i granskningsaktiviteten och klicka på **[!UICONTROL Slutför]**.
1. Navigera till mappen som du skapade granskningsaktiviteten för. Statusen för de mediefiler som du har godkänt/avvisat visas längst ned i kortvyn. I listvyn visas status för godkännande och förfallodatum i lämpliga kolumner.

1. Om du vill söka efter resurser baserat på deras status klickar/trycker du på **[!UICONTROL sökikonen]** för att visa omsökningsfältet.

1. Tryck på Enter och klicka/tryck sedan på AEM-ikonen för att visa sökpanelen.
1. In the Search panel, tap/click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in AEM Assets.

1. Tap/click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

1. To search for assets based on their expiration status, select **[!UICONTROL Expiry Status]** in the Search panel and choose the appropriate option.

1. Du kan också söka efter resurser baserat på en kombination av statusvärden under olika sökfaktorer. Du kan till exempel söka efter publicerade resurser som har godkänts i en granskningsåtgärd och ännu inte har förfallit genom att välja lämpliga alternativ i sökfunktionerna.

## Hantering av digitala rättigheter i Experience Manager Assets {#digital-rights-management-in-assets-1}

Den här funktionen tvingar dig att godkänna licensavtalet innan du kan hämta en licensierad mediefil från Adobe Experience Manager (AEM) Assets.

Om du väljer en skyddad resurs och klickar på ikonen **[!UICONTROL Hämta]** omdirigeras du till en licenssida där du godkänner licensavtalet. Om du inte godkänner licensavtalet inaktiveras knappen **[!UICONTROL Hämta]** .

Om markeringen innehåller flera skyddade resurser markerar du en resurs i taget, godkänner licensavtalet och fortsätter att hämta resursen.

En tillgång anses vara skyddad om något av dessa villkor är uppfyllt:

* Metadataegenskapen för resursen `xmpRights:WebStatement` pekar på sökvägen till CQ-sidan som innehåller licensavtalet för resursen.
* Värdet för resursens metadataegenskap `adobe_dam:restrictions` är en rå HTML-kod som anger licensavtalet.

>[!NOTE]
>
>Platsen `/etc/dam/drm/licences` som användes för att lagra licenser i tidigare versioner av AEM är föråldrad.
>
>Om du skapar eller ändrar licenssidor, eller importerar dem från tidigare AEM-versioner, rekommenderar Adobe att du lagrar sidorna på `/apps/settings/dam/drm/licenses` eller `/conf/*/settings/dam/drm/licenses`.

### Hämta DRM-resurser {#downloading-drm-assets}

1. I kortvyn väljer du de resurser du vill hämta och klickar på **[!UICONTROL hämtningsikonen]** .
1. In the **[!UICONTROL Copyright Management]** page, select the asset you want to download from the list.
1. Välj **[!UICONTROL Godkänn]** i licensfönstret. En bock visas bredvid den mediefil som du godkänner licensavtalet för. Tryck/klicka på knappen **[!UICONTROL Hämta]** .

   >[!NOTE]
   >
   >The **[!UICONTROL Download]** button is enabled only when you choose to agree to the license agreement for a protected asset. However, if your selection comprises both protected and unprotected assets, only the protected assets are listed in the left pane and the **[!UICONTROL Download]** button is enabled to download the unprotected assets. To simultaneously accept license agreements for multiple protected assets, select the assets from the list and then choose **[!UICONTROL Agree]**.

1. I dialogrutan trycker/klickar du på **[!UICONTROL Hämta]** för att hämta resursen eller dess återgivningar.
