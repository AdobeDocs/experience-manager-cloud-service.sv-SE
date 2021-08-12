---
title: Digital Rights Management in [!DNL Assets]
description: Lär dig hur du hanterar förfallotillstånd för mediefiler och information för licensierade mediefiler i [!DNL Experience Manager] som en [!DNL Cloud Service].
contentOwner: AG
feature: Resurshantering, DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 2%

---

# Digital Rights Management för digitala resurser {#digital-rights-management-in-assets}

Digitala resurser är ofta kopplade till en licens som anger användningsvillkoren och hur länge de ska användas. Med [!DNL Experience Manager]-plattformen kan du effektivt hantera information om när mediefiler förfaller och licensieringsinformation.

## Resursens förfallodatum {#asset-expiration}

Använd information om när mediefiler förfaller för att framtvinga licenskrav. Med förfalloinformationen kan du vara säker på att den publicerade resursen inte publiceras när den går ut, vilket förhindrar brott mot licensen. En användare utan administratörsbehörighet kan inte redigera, kopiera, flytta, publicera och hämta en utgången resurs.

Du kan visa förfallostatusen för en resurs på följande platser:

* **Kortvy**: För en resurs som har gått ut visas en flagga på kortet som anger att den har gått ut.
* **Listvy**: För en resurs som har gått ut visas  **[!UICONTROL Status]** banderollen i  **[!UICONTROL Expired]** kolumnen.
* **Tidslinje**: Du kan visa förfallostatusen för en resurs på tidslinjen. Markera resursen och välj Tidslinje.
* **Referensspår**: Du kan även visa förfallostatusen för resurser i  **[!UICONTROL References]** fältet. Den hanterar förfallostatus och relationer mellan sammansatta resurser och refererade delresurser, samlingar och projekt.

Så här visar du referenser till webbsidor och sammansatta resurser för en resurs:

1. Navigera till resursen, markera resursen och klicka på ![ikonen ](assets/do-not-localize/content-rail-icon.png) för referenser till innehåll till vänster. Den vänstra listen öppnas.
1. Välj **[!UICONTROL References]** i den vänstra listen.
1. För förfallna resurser visar [!UICONTROL References] förfallostatusen som **[!UICONTROL Asset is Expired]**. Om resursen har upphört att gälla visas statusen [!UICONTROL References] på **[!UICONTROL Asset has Expired Sub-Assets]**-listen.

### Sök efter utgångna resurser {#search-expired-assets}

Så här söker du efter en utgången resurs, inklusive underresurser som har gått ut:

1. Klicka på **[!UICONTROL Search]** i verktygsfältet i [!DNL Assets]-konsolen och tryck på `Enter`.

1. Klicka på ikonen GlobalNav och välj alternativet **[!UICONTROL Expiry Status]**.

1. Välj **[!UICONTROL Expired]**. Sökresultaten visar utgångna resurser.

När du väljer alternativet **[!UICONTROL Expired]** visar [!DNL Assets]-konsolen endast de förfallna resurserna och delresurserna som sammansatta resurser refererar till. De sammansatta resurserna som refererar till utgångna delresurser visas inte omedelbart efter att delresurserna har upphört att gälla. I stället visas de när [!DNL Experience Manager] upptäcker att de refererar till utgångna delresurser nästa gång som schemaläggaren körs.

Det går att ändra förfallodatumet för en publicerad tillgång till ett datum som är tidigare än den aktuella schemaläggningscykeln. Men schemat identifierar fortfarande en sådan resurs som en utgången resurs när den körs nästa gång och [!DNL Experience Manager] visar statusen i sin rapport. Utgångsdatumet för en resurs visas olika för användare i olika tidszoner.

Om ett fel dessutom hindrar schemaläggaren från att identifiera förfallna resurser i den aktuella cykeln, undersöker schemaläggaren om dessa resurser i nästa cykel och identifierar deras utgångna status.

Om du vill att [!DNL Assets]-konsolen ska visa de sammansatta resurserna tillsammans med de delresurser som har gått ut konfigurerar du arbetsflödet **[!UICONTROL Adobe CQ DAM Expiry Notification]** i [!DNL Experience Manager]. Den tidsbaserade schemaläggaren schemalägger ett jobb att vid en viss tidpunkt kontrollera om en resurs har upphört att gälla för deltillgångar. När jobbet har slutförts visas resurser som har upphört att gälla och refererade resurser som utgångna i sökresultaten.

1. Använd den [!DNL Cloud Manager] Git-databas som är kopplad till din miljö.
1. Spara en fil med namnet `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` i databasen med följande innehåll.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Följ instruktionerna i [hur du gör OSGi-konfiguration i [!DNL Experience Manager] som en [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Du kan konfigurera schemaläggaren med följande egenskaper:

* Ett `true`-värde för egenskapen `cq.dam.expiry.notification.scheduler.istimebased` initierar schemaläggaren. * Värdet för egenskapen `cq.dam.expiry.notification.scheduler.timebased.rule` är det reguljära uttrycket som definierar tiden. I exemplet ovan initieras schemaläggarjobbet vid 00 timmar.
* Om `send_email` är `true` får den som skapade resursen (den person som överför en viss resurs till [!DNL Assets]) ett e-postmeddelande när resursen förfaller.
* Det maximala antalet tillgångar som har gått ut i en iteration i schemaläggaren är värdet för egenskapen `asset_expired_limit`.
* Om du vill köra jobbet periodiskt anger du värdet för egenskapen `cq.dam.expiry.notification.scheduler.istimebased` som `false` och anger värdet för egenskapen `cq.dam.expiry.notification.scheduler.period.rule` med tiden i sekunder.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Tillgångstillstånd {#asset-states}

Konsolen [!DNL Assets] kan visa olika lägen för resurser. Beroende på det aktuella tillståndet för en viss resurs visas en etikett som beskriver dess tillstånd, till exempel Utgången, Publicerad, Godkänd, Avvisad och så vidare, i kortvyn.

1. Välj en resurs i [!DNL Assets]-användargränssnittet.

1. Välj **[!UICONTROL Publish]** i verktygsfältet. Om du inte ser alternativet [!UICONTROL Publish] i verktygsfältet klickar du på **[!UICONTROL More]** i verktygsfältet och letar upp alternativet **[!UICONTROL Publish]**.

1. Välj **[!UICONTROL Publish]** på menyn och stäng sedan bekräftelsedialogrutan.

1. Avsluta markeringsläget. Publiceringsstatusen för resursen visas längst ned på miniatyrbilden av resursen i kortvyn. I listvyn visar kolumnen Publicerad den tidpunkt då resursen publicerades.

1. Om du vill visa sidan med resursinformation väljer du en resurs i gränssnittet [!DNL Assets] och klickar på **[!UICONTROL Properties]**.

1. På fliken [!UICONTROL Advanced] anger du ett förfallodatum för resursen från fältet **[!UICONTROL Expires]**.

1. Klicka på **[!UICONTROL Save]** och sedan på **[!UICONTROL Close]** för att visa resurskonsolen.

1. Publiceringsstatusen för resursen anger att den har upphört att gälla längst ned på miniatyrbilden av resursen i kortvyn. I listvyn visas resursens status som **[!UICONTROL Expired]**.

1. I [!DNL Assets]-konsolen väljer du en mapp och skapar en granskningsåtgärd för mappen.

1. Granska och godkänn/avvisa resurserna i granskningsaktiviteten och klicka på **[!UICONTROL Complete]**.

1. Navigera till mappen som du skapade granskningsaktiviteten för. Statusen för de mediefiler som du har godkänt/avvisat visas längst ned i kortvyn. I listvyn visas status för godkännande och förfallodatum i lämpliga kolumner.

1. Om du vill söka efter resurser baserat på deras status klickar du på **[!UICONTROL Search]** för att visa sökfältet.

1. Välj `Return` och klicka på [!DNL Experience Manager].

1. Klicka på **[!UICONTROL Publish Status]** i sökpanelen och välj **[!UICONTROL Published]** för att söka efter publicerade resurser i [!DNL Assets].

1. Om du vill söka efter godkända eller avvisade resurser väljer du **[!UICONTROL Approval Status]** och väljer lämpligt alternativ.

1. Om du vill söka efter resurser baserat på deras förfallostatus väljer du **[!UICONTROL Expiry Status]** i sökpanelen och väljer lämpligt alternativ.

1. Du kan också söka efter resurser baserat på en kombination av statusvärden under olika sökfaktorer. Du kan till exempel söka efter publicerade resurser som har godkänts i en granskningsåtgärd och som inte har förfallit. Om du vill söka efter sådana resurser väljer du lämpliga alternativ i sökmetoderna.

## Digital Rights Management i [!DNL Assets] {#digital-rights-management-in-assets-1}

DRM-funktionaliteten framtvingar ett godkännande av licensavtalet innan du kan hämta en licensierad mediefil från [!DNL Assets].

Om du väljer en skyddad resurs och klickar på **[!UICONTROL Download]** omdirigeras du till en licenssida för att godkänna licensavtalet. Om du inte godkänner licensavtalet är alternativet **[!UICONTROL Download]** inte tillgängligt.

Om markeringen innehåller flera skyddade resurser markerar du en resurs i taget, godkänner licensavtalet och fortsätter att hämta resursen.

En tillgång anses vara skyddad om något av dessa villkor är uppfyllt:

* Metadataegenskapen `xmpRights:WebStatement` för resursen pekar på sökvägen till sidan som innehåller licensavtalet för resursen.
* Värdet för resursens metadataegenskap `adobe_dam:restrictions` är en rå HTML-kod som anger licensavtalet.

>[!NOTE]
>
>Platsen `/etc/dam/drm/licences` användes för att lagra licenser i de tidigare versionerna av [!DNL Experience Manager]. Platsen är nu inaktuell. Om du skapar eller ändrar licenssidor, eller porterar sidor från tidigare [!DNL Experience Manager]-versioner, rekommenderar Adobe att du lagrar sådana resurser på platserna `/apps/settings/dam/drm/licenses` eller `/conf/*/settings/dam/drm/licenses`.

### Hämta DRM-skyddade resurser {#downloading-drm-assets}

1. I kortvyn väljer du de resurser du vill hämta och väljer **[!UICONTROL Download]**.
1. På sidan **[!UICONTROL Copyright Management]** väljer du den resurs du vill hämta i listan.
1. Välj **[!UICONTROL Agree]** i rutan [!UICONTROL License]. En bock visas bredvid resursen. Välj alternativet **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Alternativet **[!UICONTROL Download]** är bara aktiverat när du väljer att godkänna licensavtalet för en skyddad tillgång. Om markeringen omfattar både skyddade och oskyddade resurser visas endast de skyddade resurserna i rutan och alternativet **[!UICONTROL Download]** är tillgängligt för att hämta de oskyddade resurserna. Om du vill acceptera licensavtal för flera skyddade resurser samtidigt markerar du resurserna i listan och väljer sedan **[!UICONTROL Agree]**.

1. Om du vill hämta resursen eller dess återgivningar väljer du **[!UICONTROL Download]** i dialogrutan.
