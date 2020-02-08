---
title: Relaterade resurser
description: Lär dig hur du relaterar resurser som delar vissa gemensamma attribut. Du kan också använda funktionen för att skapa käll-/härledda relationer mellan resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Relaterade tillgångar {#related-assets}

Med Adobe Experience Manager Assets (AEM) kan ni manuellt relatera resurser baserat på organisationens behov med hjälp av funktionen Relaterade resurser. Du kan till exempel relatera en licensfil till en resurs eller en bild/video på ett liknande ämne. Du kan relatera resurser som delar vissa gemensamma attribut. Du kan också använda funktionen för att skapa käll-/härledda relationer mellan resurser. Om du till exempel har en PDF-fil som genereras från en INDD-fil kan du koppla PDF-filen till dess INDD-källfil.

På så sätt kan du dela en lågupplöst fil (t.ex. PDF/JPG) till leverantörer/byråer och bara göra högupplösta filer (t.ex. INDD) tillgängliga på begäran.

## Relatera resurser {#relating-assets}

1. I gränssnittet Resurser öppnar du egenskapssidan för en resurs som du vill relatera. Du kan också välja resursen i listvyn. Du kan också välja resursen från en samling.
1. Om du vill koppla en annan resurs till den valda resursen klickar/trycker du på ikonen **[!UICONTROL Relatera]** i verktygsfältet.
1. Gör något av följande:

   * Om du vill relatera källfilen för resursen väljer du **[!UICONTROL Källa]** i listan.
   * Om du vill relatera en härledd fil väljer du **[!UICONTROL Härledd]** i listan.
   * Om du vill skapa en dubbelriktad relation mellan resurserna väljer du **[!UICONTROL Övriga]** i listan.

1. På skärmen **[!UICONTROL Välj resurs]** navigerar du till platsen för den resurs du vill relatera till och markerar den.

1. Klicka på/tryck på ikonen **[!UICONTROL Bekräfta]** .
1. Klicka/tryck på **[!UICONTROL OK]** för att stänga dialogrutan. Beroende på ditt val av relation i steg 3 listas den relaterade resursen under en lämplig kategori i **[!UICONTROL relaterat]** avsnitt. Om den resurs du har relaterat är källfilen för den aktuella resursen visas den under **[!UICONTROL Källa]**.
1. Om du vill ta bort kopplingen för en resurs klickar/trycker du på ikonen **[!UICONTROL Ej relaterat]** i verktygsfältet.
1. Välj de mediefiler som du vill ta bort kopplingen för i dialogrutan **[!UICONTROL Ta bort relationer]** och klicka/tryck på **[!UICONTROL Ta bort relation]**.
1. Klicka/tryck på **[!UICONTROL OK]** för att stänga dialogrutan. Resurserna som du har tagit bort relationer för tas bort från listan över relaterade resurser under avsnittet **[!UICONTROL Relaterade]** .

## Översätta relaterade resurser {#translating-related-assets}

Det är också praktiskt att skapa käll-/härledda relationer mellan resurser med hjälp av funktionen Relaterade resurser i översättningsarbetsflöden. När du kör ett översättningsarbetsflöde på en härledd resurs hämtar AEM Resurser automatiskt alla resurser som källfilen refererar till och inkluderar dem för översättning. På så sätt översätts den resurs som källresursen refererar till tillsammans med källresursen och de härledda resurserna. Tänk dig till exempel ett scenario där den engelska språkkopian innehåller en härledd resurs och dess källfil som visas.

Om källfilen är relaterad till en annan resurs hämtar AEM Resurser den refererade resursen och inkluderar den för översättning.

1. Översätt resurserna i källmappen till ett målspråk genom att följa stegen i [Skapa ett nytt översättningsprojekt](/help/assets/translate-assets.md#create-a-new-translation-project). I det här fallet kan du till exempel översätta dina resurser till franska.
1. Öppna översättningsmappen på sidan Projekt.
1. Klicka/tryck på projektpanelen för att öppna informationssidan.
1. Klicka på/tryck på ellipserna under översättningsjobbkortet för att visa översättningsstatusen.
1. Markera resursen och klicka/tryck sedan på **[!UICONTROL Visa i resurser]** i verktygsfältet för att visa översättningsstatusen för resursen.
1. Om du vill kontrollera om de resurser som är relaterade till källan har översatts klickar/trycker du på källresursen.
1. Välj den resurs som är relaterad till källan och klicka/tryck sedan på **[!UICONTROL Visa i Resurser]**. Den översatta relaterade resursen visas.
