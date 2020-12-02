---
title: Digital Rights Management in [!DNL Assets]
description: Lär dig hur du hanterar förfallotillstånd för mediefiler och information för licensierade mediefiler i [!DNL Experience Manager] som en Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 7%

---


# Digital Rights Management för resurser {#digital-rights-management-in-assets}

Digitala resurser är ofta kopplade till en licens som anger användningsvillkoren och hur länge de ska användas. Eftersom [!DNL Adobe Experience Manager Assets] är helt integrerat med [!DNL Experience Manager]-plattformen kan du effektivt hantera förfalloinformation och resurstillstånd. Du kan även associera licensinformation med resurser.

## Resursens förfallodatum {#asset-expiration}

Att mediefiler förfaller är ett effektivt sätt att tillämpa licenskrav för mediefiler. Det säkerställer att den publicerade resursen inte publiceras när den upphör att gälla, vilket förhindrar eventuella brott mot licensen. En användare utan administratörsbehörighet kan inte redigera, kopiera, flytta, publicera och hämta en utgången resurs.

Du kan visa förfallostatusen för en resurs på följande platser:

* **Kortvy**: För en resurs som har gått ut visas en flagga på kortet som anger att den har gått ut.
* **Listvy**: För förfallna resurser visas  **[!UICONTROL Status]** banderollen i  **[!UICONTROL Expired]** kolumnen.
* **Tidslinje**: Du kan visa förfallostatusen för en resurs på tidslinjen. Markera resursen och välj Tidslinje.
* **Referensspår**: Du kan även visa förfallostatusen för resurser i  **[!UICONTROL References]** fältet. Den hanterar förfallostatus och relationer mellan sammansatta resurser och refererade delresurser, samlingar och projekt.

1. Navigera till resursen som du vill visa referenser till webbsidor och sammansatta resurser för.
1. Markera resursen och klicka på logotypen [!DNL Experience Manager].
1. Välj **[!UICONTROL References]** på menyn.
1. För förfallna resurser visas förfallostatusen **[!UICONTROL Asset is Expired]** högst upp på referenslinjen. Om resursen har upphört att gälla visas statusen **[!UICONTROL Asset has Expired Sub-Assets]** på referenspanelen.

### Sök efter utgångna resurser {#search-expired-assets}

Du kan söka efter utgångna resurser, inklusive underresurser som gått ut, på sökpanelen.

1. I [!DNL Assets]-konsolen klickar du på **[!UICONTROL Search]** i verktygsfältet för att visa Omnissökrutan.

1. Tryck på Retur när markören är i rutan Sök så visas sökresultatsidan.

1. Klicka på ikonen GlobalNav för att visa sökpanelen.

1. Klicka/tryck på alternativet **[!UICONTROL Expiry Status]** för att expandera det.

1. Välj **[!UICONTROL Expired]**. De förfallna resurserna visas i sökresultaten.

När du väljer alternativet **[!UICONTROL Expired]** visar [!DNL Assets]-konsolen endast de förfallna resurserna och delresurserna som sammansatta resurser refererar till. De sammansatta resurserna som refererar till utgångna delresurser visas inte omedelbart efter att delresurserna har upphört att gälla. I stället visas de när [!DNL Experience Manager] upptäcker att de refererar till utgångna delresurser nästa gång som schemaläggaren körs.

Om du ändrar förfallodatumet för en publicerad resurs till ett datum som är tidigare än den aktuella schemaläggningscykeln, identifierar schemat fortfarande den här resursen som en utgången resurs nästa gång den körs och visar dess status i enlighet med detta. Utgångsdatumet för en resurs visas olika för användare i olika tidszoner.

Om ett fel eller fel dessutom förhindrar att schemaläggaren upptäcker förfallna resurser i den aktuella cykeln, undersöker schemaläggaren om dessa resurser i nästa cykel och identifierar deras förfallna status.

Om du vill att [!DNL Assets]-konsolen ska visa de sammansatta resurserna tillsammans med de delresurser som har gått ut konfigurerar du ett **[!UICONTROL Adobe CQ DAM Expiry Notification]**-arbetsflöde i [!DNL Experience Manager] Configuration Manager.

1. Öppna [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. Som standard är **[!UICONTROL Time based Scheduler]** markerat, vilket schemalägger ett jobb att vid en viss tidpunkt kontrollera om en resurs har upphört att gälla för delresurser. När jobbet har slutförts visas resurser som har upphört att gälla och refererade resurser som utgångna i sökresultaten.

1. Om du vill köra jobbet regelbundet avmarkerar du fältet **[!UICONTROL Time Based Scheduler Rule]** och ändrar tiden i sekunder i fältet **[!UICONTROL Periodic Scheduler]**. Exempeluttrycket ”0 0 0 &amp;ast; &amp;ast; ?” utlöser till exempel jobbet kl. 00.

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. I fältet **[!UICONTROL Prior notification in seconds]** anger du tiden i sekunder innan en resurs förfaller när du vill få ett meddelande om förfallotiden. Om du är administratör eller den som har skapat resursen får du ett meddelande innan resursen upphör att gälla om att resursen håller på att gå ut efter den angivna tiden.

   När resursen har gått ut får du ett meddelande som bekräftar att den har gått ut. Dessutom inaktiveras utgångna resurser.

1. Klicka på **[!UICONTROL Save]**.

## Tillgångstillstånd {#asset-states}

Konsolen [!DNL Assets] kan visa olika lägen för resurser. Beroende på det aktuella tillståndet för en viss resurs visas en etikett som beskriver dess tillstånd, till exempel Utgången, Publicerad, Godkänd, Avvisad och så vidare, i kortvyn.

1. Välj en resurs i [!DNL Assets]-användargränssnittet.

1. Klicka på **[!UICONTROL Publish]** i verktygsfältet. Om du inte ser **Publicera** i verktygsfältet klickar du på **[!UICONTROL More]** i verktygsfältet och letar upp alternativet **[!UICONTROL Publish]**.

1. Välj **[!UICONTROL Publish]** på menyn och stäng sedan bekräftelsedialogrutan.
1. Avsluta markeringsläget. Publiceringsstatusen för resursen visas längst ned på miniatyrbilden av resursen i kortvyn. I listvyn visar kolumnen Publicerad den tidpunkt då resursen publicerades.

1. Om du vill visa sidan med resursinformation väljer du en resurs i gränssnittet [!DNL Assets] och klickar på **[!UICONTROL Properties]**.

1. På fliken [!UICONTROL Advanced] anger du ett förfallodatum för resursen från fältet **[!UICONTROL Expires]**.

1. Klicka på **[!UICONTROL Save]** och sedan på **[!UICONTROL Close]** för att visa resurskonsolen.
1. Publiceringsstatusen för resursen anger att den har upphört att gälla längst ned på miniatyrbilden av resursen i kortvyn. I listvyn visas resursens status som **[!UICONTROL Expired]**.

1. I [!DNL Assets]-konsolen väljer du en mapp och skapar en granskningsåtgärd för mappen.
1. Granska och godkänn/avvisa resurserna i granskningsaktiviteten och klicka på **[!UICONTROL Complete]**.
1. Navigera till mappen som du skapade granskningsaktiviteten för. Statusen för de mediefiler som du har godkänt/avvisat visas längst ned i kortvyn. I listvyn visas status för godkännande och förfallodatum i lämpliga kolumner.

1. Om du vill söka efter resurser baserat på deras status klickar du på **[!UICONTROL Search]** för att visa omsökningsfältet.

1. Tryck på Retur och klicka på [!DNL Experience Manager] för att visa sökpanelen.
1. Klicka på **[!UICONTROL Publish Status]** i sökpanelen och välj **[!UICONTROL Published]** för att söka efter publicerade resurser i [!DNL Assets].

1. Klicka på **[!UICONTROL Approval Status]** och klicka på lämpligt alternativ för att söka efter godkända eller avvisade resurser.

1. Om du vill söka efter resurser baserat på deras förfallostatus markerar du **[!UICONTROL Expiry Status]** på sökpanelen och väljer lämpligt alternativ.

1. Du kan också söka efter resurser baserat på en kombination av statusvärden under olika sökfaktorer. Du kan till exempel söka efter publicerade resurser som har godkänts i en granskningsåtgärd och ännu inte har förfallit genom att välja lämpliga alternativ i sökfunktionerna.

## Digital Rights Management i [!DNL Assets] {#digital-rights-management-in-assets-1}

Den här funktionen tvingar till godkännande av licensavtalet innan du kan hämta en licensierad mediefil från [!DNL Adobe Experience Manager Assets].

Om du väljer en skyddad resurs och klickar på **[!UICONTROL Download]** omdirigeras du till en licenssida för att godkänna licensavtalet. Om du inte godkänner licensavtalet är alternativet **[!UICONTROL Download]** inte tillgängligt.

Om markeringen innehåller flera skyddade resurser markerar du en resurs i taget, godkänner licensavtalet och fortsätter att hämta resursen.

En tillgång anses vara skyddad om något av dessa villkor är uppfyllt:

* Metadataegenskapen `xmpRights:WebStatement` för resursen pekar på sökvägen till sidan som innehåller licensavtalet för resursen.
* Värdet för resursens metadataegenskap `adobe_dam:restrictions` är en rå HTML-kod som anger licensavtalet.

>[!NOTE]
>
>Platsen `/etc/dam/drm/licences` som används för att lagra licenser i tidigare versioner av [!DNL Experience Manager] är föråldrad.
>
>Om du skapar eller ändrar licenssidor, eller importerar dem från tidigare [!DNL Experience Manager]-versioner, rekommenderar Adobe att du lagrar dem under `/apps/settings/dam/drm/licenses` eller `/conf/*/settings/dam/drm/licenses`.

### Hämta DRM-skyddade resurser {#downloading-drm-assets}

1. I kortvyn väljer du de resurser du vill hämta och klickar på **[!UICONTROL Download]**.
1. På sidan **[!UICONTROL Copyright Management]** väljer du den resurs du vill hämta i listan.
1. Välj **[!UICONTROL Agree]** i rutan [!UICONTROL License]. En bock visas bredvid resursen. Klicka på alternativet **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Alternativet **[!UICONTROL Download]** är bara aktiverat när du väljer att godkänna licensavtalet för en skyddad tillgång. Om markeringen omfattar både skyddade och oskyddade resurser visas endast de skyddade resurserna i rutan och alternativet **[!UICONTROL Download]** aktiveras för att hämta de oskyddade resurserna. Om du vill acceptera licensavtal för flera skyddade resurser samtidigt markerar du resurserna i listan och väljer sedan **[!UICONTROL Agree]**.

1. Klicka på **[!UICONTROL Download]** i dialogrutan för att hämta resursen eller dess återgivningar.
