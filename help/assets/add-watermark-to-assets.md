---
title: Lägg till vattenstämpel i dina digitala resurser
description: Lär dig hur du använder funktionen Vattenstämpel för att lägga till en digital vattenstämpel till resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Vattenstämpel {#watermarking}

Med funktionen för vattenstämplar i Adobe Experience Manager-resurser (AEM) kan du lägga till en digital vattenstämpel i resurserna, som hjälper användarna att verifiera autenticiteten och upphovsrätten till resurserna. AEM Resurser stöder text som ska användas som vattenstämpel i PNG- och JPEG-filer.

Om du vill kunna använda vattenstämpel på resurser lägger du till steget Vattenstämpel i arbetsflödet för DAM-uppdatering av resurser.

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Modeller]**.
1. På sidan Arbetsflödesmodeller väljer du arbetsflödet **[!UICONTROL DAM-uppdatering av resurs]** och klickar på **[!UICONTROL Redigera]**.

1. Dra steget **[!UICONTROL Lägg till vattenstämpel]** från sidopanelen till arbetsflödet för DAM-uppdatering av resurser.

<!--  ![Darg add watermark step in the DAM update asset workflow](assets/add_watermark_step_aem_assets.png) -->

>[!NOTE]
>
>Placera steget Lägg till vattenstämpel var som helst före steget Bearbeta miniatyrbild.

1. Öppna steget **[!UICONTROL Lägg till vattenstämpel]** för att visa dess egenskaper.
1. På fliken **[!UICONTROL Argument]** anger du giltiga värden i de olika fälten, inklusive text, teckensnittstyp, storlek, färg, position, orientering och så vidare. Bekräfta ändringarna genom att trycka/klicka på ikonen Klar.

<!--   ![Provide the arguments in the add watermark step in Assets](assets/arguments_add_watermark_aem_assets.png) -->

1. Spara arbetsflödet för **[!UICONTROL DAM-uppdatering av resurser]** med steget Vattenstämpel.
1. Ladda upp en exempelresurs från Assets-användargränssnittet. Vattenstämpeln visas med teckensnittsstorlek, färg o.s.v. på den plats som du konfigurerade i ovanstående steg.
