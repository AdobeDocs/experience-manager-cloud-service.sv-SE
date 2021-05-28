---
title: Publicera resurser, mappar och samlingar på varumärkesportalen
description: Publicera resurser, mappar och samlingar på varumärkesportalen.
contentOwner: Vishabh Gupta
feature: Brand Portal,Resursdistribution,Konfiguration
role: Business Practitioner
exl-id: 1cc438bc-8cad-4421-af03-c1f6d750e0a8
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 97%

---

# Publicera resurser på varumärkesportalen {#publish-assets-to-brand-portal}

Som administratör för Adobe Experience Manager (AEM) Assets kan du publicera resurser, mappar och samlingar på varumärkesportalinstansen för AEM Assets. Du kan även schemalägga publiceringsarbetsflödet för en resurs eller mapp till ett senare datum eller en senare tid. Efter publiceringen kan varumärkesportalens användare komma åt och vidaredistribuera resurser, mappar och samlingar till andra användare.

Du måste dock först konfigurera AEM Assets med varumärkesportalen. Mer information finns i [Konfigurera AEM Assets med varumärkesportalen](configure-aem-assets-with-brand-portal.md).

Om du senare gör ändringar i den ursprungliga resursen, mappen eller samlingen i AEM Assets återspeglas inte ändringarna i varumärkesportalen förrän du publicerar resursen, mappen eller samlingen på nytt från AEM Assets. Funktionen säkerställer att pågående ändringar inte finns i varumärkesportalen. Endast godkända ändringar som publiceras av en administratör finns i varumärkesportalen.

* [Publicera resurser på varumärkesportalen](#publish-assets-to-bp)
* [Publicera mappar på varumärkesportalen](#publish-folders-to-brand-portal)
* [Publicera samlingar på varumärkesportalen](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe rekommenderar stegvis publicering, helst vid tidpunkter med låg belastning, för att AEM-författaren inte ska uppta för mycket resurser.

## Publicera resurser på varumärkesportalen {#publish-assets-to-bp}

Så här publicerar du resurser från AEM Assets till varumärkesportalen:

1. Öppna den överordnade mappen i Assets-konsolen och markera alla resurser som du vill publicera och klicka på alternativet **[!UICONTROL Quick Publish]** i verktygsfältet.

   ![publish2bp-2](assets/publish2bp.png)

1. Du kan publicerar resurser på följande två sätt:
   * [Publicera nu](#publish-to-bp-now) (publicera resurser direkt)
   * [Publicera senare](#publish-to-bp-later) (schemalägg publicering av resurser)

### Publicera resurser nu {#publish-to-bp-now}

Gör något av följande för att publicera de markerade resurserna på varumärkesportalen:

* Välj **[!UICONTROL Quick Publish]** i verktygsfältet. Klicka sedan på **[!UICONTROL Publish to Brand Portal]** i menyn.

* Välj **[!UICONTROL Manage Publication]** i verktygsfältet.

   1. Välj **[!UICONTROL Publish to Brand Portal]** från **[!UICONTROL Action]**.

      Välj **[!UICONTROL Now]** från **[!UICONTROL Scheduling]**.

      Klicka på **[!UICONTROL Next]**.

   2. Bekräfta ditt val i **[!UICONTROL Scope]** och klicka på **[!UICONTROL Publish to Brand Portal]**.

Ett meddelande visas som anger att resurserna har placerats i kö för publicering på varumärkesportalen. Logga in på gränssnittet för varumärkesportalen för att visa de publicerade resurserna.

### Publicera resurser senare {#publish-to-bp-later}

Gör så här för att schemalägga publicering av resurser på varumärkesportalen till ett senare datum eller en senare tid:

1. Välj de resurser som du vill schemalägga för publicering och klicka på **[!UICONTROL Manage Publication]** i verktygsfältet högst upp.

1. Välj **[!UICONTROL Publish to Brand Portal]** från **[!UICONTROL Action]** på sidan **[!UICONTROL Manage Publication]**.

   Välj **[!UICONTROL Later]** från **[!UICONTROL Scheduling]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Markera en **[!UICONTROL Activation date]** och ange en tid. Klicka på **[!UICONTROL Next]**.

1. Välj ett **aktiveringsdatum** och ange en tid. Klicka på **Nästa**.

1. Ange en **[!UICONTROL Workflow title]** i **[!UICONTROL Workflows]**. Klicka på **[!UICONTROL Publish Later]**.

   ![publishworkflow](assets/publishworkflow.png)

Logga in på gränssnittet för varumärkesportalen för att visa de publicerade resurserna (beroende på schemalagt datum eller tid).

![bp_landing_page](assets/bp_landing_page.png)


## Publicera mappar på varumärkesportalen {#publish-folders-to-brand-portal}

Du kan publicera eller avpublicera resursmappar direkt eller schemalägga åtgärden till ett senare datum eller en senare tid.

### Publicera mappar på varumärkesportalen {#publish-folders-to-bp}

1. Markera mapparna som du vill publicera från Assets-konsolen och klicka på **[!UICONTROL Quick Publish]**-alternativet i verktygsfältet.

   ![publish2bp](assets/publish2bp.png)

1. **Publicera mappar nu**

   Gör något av följande för att publicera de markerade mapparna på varumärkesportalen:

   * Välj **[!UICONTROL Quick Publish]** i verktygsfältet.

      Välj **[!UICONTROL Publish to Brand Portal]** i menyn.

   * Välj **[!UICONTROL Manage Publication]** i verktygsfältet.

      1. Välj **[!UICONTROL Publish to Brand Portal]** från **[!UICONTROL Action]**.

         Välj **[!UICONTROL Now]** från **[!UICONTROL Scheduling]**.

         Klicka på **Nästa.**

      1. Bekräfta ditt val i **[!UICONTROL Scope]** och klicka på **[!UICONTROL Publish to Brand Portal]**.

   Ett meddelande visas som anger att mappen har placerats i kö för publicering på varumärkesportalen. Logga in på gränssnittet för varumärkesportalen för att visa den publicerade resursen.

1. **Publicera mappar senare**

   Gör så här för att schemalägga publicering av resursmappar till ett senare datum eller en senare tid:

   1. Välj de mappar som du vill schemalägga för publicering och välj sedan **[!UICONTROL Manage Publication]** i verktygsfältet högst upp.
   1. Välj **[!UICONTROL Publish to Brand Portal]** från **[!UICONTROL Action]**.

      Välj **[!UICONTROL Later]** från **[!UICONTROL Scheduling]**.

   1. Markera en **[!UICONTROL Activation date]** och ange en tid. Klicka på **[!UICONTROL Next]**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Bekräfta ditt val i **[!UICONTROL Scope]**. Klicka på **[!UICONTROL Next]**.

   1. Ange en arbetsflödestitel under **[!UICONTROL Workflows]**. Klicka på **[!UICONTROL Publish Later]**.

      ![manageschedulepub](assets/manageschedulepub.png)

### Avpublicera mappar från varumärkesportalen {#unpublish-folders-from-brand-portal}

Du kan ta bort alla resursmappar som publicerats på varumärkesportalen genom att avpublicera dem från instansen av AEM Assets. När du har avpublicerat originalmappen har varumärkesportalens användare har inte längre tillgång till kopian.

Du kan avpublicera resursmappar från varumärkesportalen direkt eller schemalägga avpublicering till ett senare datum och en senare tid.

Gör så här för att avpublicerar resursmappar från varumärkesportalen:

1. Markera resursmapparna som du vill avpublicera i Assets-konsolen och klicka på alternativet **[!UICONTROL Manage Publication]** i verktygsfältet.

   ![publish2bp-1](assets/publish2bp.png)

1. **Avpublicera resursmappar nu**

   Gör så här för att avpublicera den valda resursmappen från varumärkesportalen direkt:

   1. Välj **[!UICONTROL Manage Publication]** i verktygsfältet.

   1. Välj **[!UICONTROL Unpublish from Brand Portal]** från **[!UICONTROL Action]**.

      Välj **[!UICONTROL Now]** från **[!UICONTROL Scheduling]**.

      Klicka på **[!UICONTROL Next]**.

   1. Bekräfta ditt val i **[!UICONTROL Scope]** och klicka på **[!UICONTROL Unpublish from Brand Portal]**.

      ![confirm-unpublish](assets/confirm-unpublish.png)

1. **Avpublicera resursmappar senare**

   Gör så här för att schemalägga avpublicering av en resursmapp till ett senare datum eller en senare tid:

   1. Välj **[!UICONTROL Manage Publication]** i verktygsfältet.

   1. Välj **[!UICONTROL Unpublish from Brand Portal]** från **[!UICONTROL Action]**.

      Välj **[!UICONTROL Later]** från **[!UICONTROL Scheduling]**.

   1. Markera ett **[!UICONTROL Activation date]** och ange tiden. Klicka på **[!UICONTROL Next]**.

   1. Bekräfta ditt val i **[!UICONTROL Scope]** och klicka på **[!UICONTROL Next]**.

   1. Ange en **[!UICONTROL Workflow title]** i **[!UICONTROL Workflows]**. Klicka på **[!UICONTROL Unpublish Later]**.

      ![unpublishworkflows](assets/unpublishworkflows.png)

## Publicera samlingar på varumärkesportalen {#publish-collections-to-brand-portal}

Du kan publicera eller avpublicera samlingar från molninstansen AEM Assets.

>[!NOTE]
>
>Det går inte att publicera innehållsfragment på varumärkesportalen. Därför är åtgärden **[!UICONTROL Publish to Brand Portal]** inte tillgänglig om du väljer innehållsfragment i AEM Assets.
>
>Om samlingar som innehåller innehållsfragment publiceras från AEM Assets till varumärkesportalen, replikeras allt innehåll i mappen förutom innehållsfragmenten till varumärkesportalens gränssnitt.

### Publicera samlingar {#publish-collections}

Gör så här för att publicera samlingar från AEM Assets till varumärkesportalen:

1. Klicka på AEM-logotypen i användargränssnittet för AEM Assets.

1. Gå till **[!UICONTROL Assets]** > **[!UICONTROL Collections]** från **navigeringssidan**.

1. Välj de samlingar som du vill publicera på varumärkesportalen från **samlingskonsolen**.

   ![select_collection](assets/select_collection.png)

1. Klicka på **[!UICONTROL Publish to Brand Portal]** i verktygsfältet.

1. Klicka på **[!UICONTROL Publish]** i bekräftelsedialogrutan.

1. Stäng bekräftelsemeddelandet.

   Logga in på varumärkesportalen som administratör. Den publicerade samlingen är tillgänglig i samlingskonsolen.

   ![published collection](assets/published_collection.png)

### Avpublicera samlingar {#unpublish-collections}

Du kan ta bort en samling som publicerats på varumärkesportalen genom att avpublicera den från instansen av AEM Assets. När du har avpublicerat originalsamlingen har varumärkesportalens användare inte längre tillgång till kopian.

Gör så här för att avpublicera en samling:

1. Välj den samling som du vill avpublicera från **samlingskonsolen** för instansen av AEM Assets.

   ![select_collection](assets/select_collection-1.png)

1. Klicka på ikonen **[!UICONTROL Remove from Brand Portal]** i verktygsfältet.
1. Klicka på **[!UICONTROL Unpublish]** i dialogrutan.
1. Stäng bekräftelsemeddelandet. Samlingen tas bort från varumärkesportalens gränssnitt.

Förutom ovanstående kan du även publicera metadatascheman, bildförinställningar, sökfasetter och taggar från AEM Assets till varumärkesportalen.

* [Publicera förinställningar, scheman och fasetter på varumärkesportalen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicera taggar på varumärkesportalen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Mer information finns i [dokumentationen till varumärkesportalen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html).


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
