---
title: Publicera resurser, mappar och samlingar på varumärkesportalen
seo-title: Publicera resurser, mappar och samlingar på varumärkesportalen
description: Lär dig hur du publicerar och avpublicerar resurser, mappar och samlingar på varumärkesportalen.
seo-description: Lär dig hur du publicerar och avpublicerar resurser, mappar och samlingar på varumärkesportalen.
uuid: null
contentOwner: Vishabh Gupta
products: SG_EXPERIENCEMANAGER/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: null
translation-type: tm+mt
source-git-commit: abc98974f5507c71e75cdd864a98281f7cdba7f3

---


# Publicera resurser, mappar och samlingar på varumärkesportalen {#publish-aem-assets-to-brand-portal}

Som administratör för Adobe Experience Manager-resurser (AEM) kan du publicera resurser, mappar och samlingar till instansen AEM Assets Brand Portal. Du kan också schemalägga publiceringsarbetsflödet för en resurs eller mapp till ett senare datum eller en senare tidpunkt. Efter publiceringen kan Brand Portal-användarna komma åt och vidaredistribuera resurser, mappar och samlingar till andra användare.

Du måste dock först konfigurera AEM Assets med Brand Portal. Mer information finns i [Konfigurera AEM-resurser med varumärkesportalen](configure-aem-assets-with-brand-portal.md).

Om du gör senare ändringar i den ursprungliga resursen, mappen eller samlingen i AEM Resurser återspeglas inte ändringarna i varumärkesportalen förrän du publicerar om från AEM Resurser. Den här funktionen ser till att pågående ändringar inte är tillgängliga i varumärkesportalen. Endast godkända ändringar som publiceras av en administratör är tillgängliga i varumärkesportalen.

* [Publicera resurser på varumärkesportalen](#publish-assets-to-bp)
* [Publicera mappar på varumärkesportalen](#publish-folders-to-brand-portal)
* [Publicera samlingar på varumärkesportalen](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe rekommenderar att publiceringen staggats, helst under icke-topp-timmar, så att AEM-författaren inte tar upp för mycket resurser.


## Publicera resurser på varumärkesportalen {#publish-assets-to-bp}

Så här publicerar du resurser från AEM Assets till varumärkesportalen:

1. I resurskonsolen öppnar du den överordnade mappen och väljer alla resurser som du vill publicera. Klicka sedan på **[!UICONTROL Snabbpublicering]** i verktygsfältet.


   ![publish2bp-2](assets/publish2bp.png)

1. Här följer två sätt att publicera resurser:
   * [Publicera nu](#publish-to-bp-now) (publicera resurser direkt)
   * [Publicera senare](#publish-to-bp-now) (schemalägg publiceringsresurser)

### Publicera resurser nu {#publish-to-bp-now}

Gör något av följande om du vill publicera de markerade resurserna på varumärkesportalen:

* Välj **[!UICONTROL Snabbpublicering]** i verktygsfältet. På menyn klickar du på **[!UICONTROL Publicera på varumärkesportalen]**.

* Välj **[!UICONTROL Hantera publikation]** i verktygsfältet.

   1. I **[!UICONTROL Åtgärd]** väljer du **[!UICONTROL Publicera på varumärkesportal]** och i **[!UICONTROL Schemaläggning]** väljer du **[!UICONTROL nu]**. Click **[!UICONTROL Next]**.

   2. Bekräfta ditt val i **[!UICONTROL Omfång]** och klicka på **[!UICONTROL Publicera på varumärkesportal]**.

Ett meddelande visas som anger att resurserna har placerats i kö för publicering på varumärkesportalen. Logga in på gränssnittet för varumärkesportalen för att se de publicerade resurserna.

### Publicera resurser senare {#publish-to-bp-later}

Så här schemalägger du publicering av resurser på varumärkesportalen till ett senare datum eller en senare tidpunkt:

1. Välj de resurser som du vill schemalägga för publicering och välj **[!UICONTROL Hantera publikation]** i verktygsfältet högst upp.

1. På sidan **[!UICONTROL Hantera publikation]** väljer du **[!UICONTROL Publicera på varumärkesportal]** från **[!UICONTROL åtgärd]** och sedan **[!UICONTROL senare]** från **[!UICONTROL Schemaläggning]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Välj ett **aktiveringsdatum** och ange tid. Click **Next**.

1. Ange en **[!UICONTROL arbetsflödesrubrik]** i **[!UICONTROL arbetsflöden]**. Klicka på **[!UICONTROL Publicera senare]**.

   ![publicerat arbetsflöde](assets/publishworkflow.png)

Logga in på gränssnittet för varumärkesportalen för att se vilka publicerade resurser som finns tillgängliga.

![bp_landing_page](assets/bp_landing_page.png)

<!--

End - Publish assets to Brand Portal
Start- Publish folders to Brand Portal
-->


## Publicera mappar på varumärkesportalen{#publish-folders-to-brand-portal}

Du kan publicera eller avpublicera resursmappar direkt eller schemalägga till ett senare datum eller en senare tidpunkt.

### Publicera mappar på varumärkesportalen {#publish-folders-to-brand-portal-1}

1. I resurskonsolen markerar du de mappar som du vill publicera och klickar på **[!UICONTROL Snabbpublicering]** i verktygsfältet.

   ![publish2bp](assets/publish2bp.png)

1. **Publicera mappar nu**

   Om du vill publicera de markerade mapparna på varumärkesportalen gör du något av följande:

   * Välj **[!UICONTROL Snabbpublicering]** i verktygsfältet. På menyn väljer du **[!UICONTROL Publicera på varumärkesportal]**.

   * Välj **[!UICONTROL Hantera publikation]** i verktygsfältet.

      1. I **[!UICONTROL Åtgärd]** väljer du **[!UICONTROL Publicera på varumärkesportal]**. Välj **[!UICONTROL Nu]** i **[!UICONTROL Schemaläggning]**. Click **[!UICONTROL Next]**.
      1. Bekräfta ditt val i **[!UICONTROL Omfång]** och klicka på **[!UICONTROL Publicera på varumärkesportal]**.
   Det visas ett meddelande om att mappen har placerats i kö för publicering på varumärkesportalen. Logga in i gränssnittet för varumärkesportalen för att visa den publicerade mappen.

1. **Publicera mappar senare**

   Om du vill schemalägga publicering av resursmappar till ett senare datum eller en senare tidpunkt.

   1. Markera de mappar som du vill schemalägga för publicering och välj **[!UICONTROL Hantera publikation]** i verktygsfältet högst upp.
   1. I **[!UICONTROL Åtgärd]** väljer du **[!UICONTROL Publicera på varumärkesportal]** och i **[!UICONTROL Schemaläggning]** väljer du **[!UICONTROL Senare]**.

      ![publiclaterbp](assets/publishlaterbp.png)

   1. Välj ett **[!UICONTROL aktiveringsdatum]** och ange tid. Click **[!UICONTROL Next]**.
   1. Bekräfta ditt val i **[!UICONTROL Omfång]**. Click **[!UICONTROL Next]**.
   1. Ange en arbetsflödesrubrik under **[!UICONTROL Arbetsflöden]**. Klicka på **[!UICONTROL Publicera senare]**.

      ![manageschedulepub](assets/manageschedulepub.png)

### Avpublicera mappar från varumärkesportalen {#unpublish-folders-from-brand-portal}

Du kan ta bort alla resursmappar som publicerats på varumärkesportalen genom att avpublicera dem från din AEM Resurser-instans. När du har avpublicerat originalmappen är dess kopia inte längre tillgänglig för Brand Portal-användarna.

Du kan avpublicera resursmappar från varumärkesportalen direkt eller schemalägga dem för ett senare datum och en senare tidpunkt.

Så här avpublicerar du resursmappar från varumärkesportalen:

1. I AEM Assets-konsolen väljer du den mapp som du vill avpublicera.

   ![publish2bp-1](assets/publish2bp.png)

1. Klicka på **[!UICONTROL Hantera publikation]** i verktygsfältet.

1. **Avpublicera från varumärkesportalen nu**

   Så här avpublicerar du omedelbart den valda mappen från varumärkesportalen:

   1. Välj **Hantera publikation** i verktygsfältet.
   1. I **Åtgärd** väljer du **Avpublicera från varumärkesportalen** och i **Schemaläggning** väljer du **nu**. Click **Next.**
   1. Bekräfta ditt val i **Omfång** och klicka på **Avpublicera från varumärkesportalen**.
   ![bekräfta-avpublicera](assets/confirm-unpublish.png)

1. **Avpublicera från varumärkesportalen senare**

   Så här schemalägger du avpublicering av en mapp från varumärkesportalen till ett senare datum och en senare tidpunkt:

   1. Välj **Hantera publikation** i verktygsfältet.
   1. I **Åtgärd** väljer du **Avpublicera från varumärkesportalen** och i **Schemaläggning** väljer du **Senare**.
   1. Välj ett **aktiveringsdatum** och ange tid. Click **Next**.
   1. Bekräfta ditt val i **Omfång** och klicka på **Nästa**.
   1. Ange en **arbetsflödesrubrik** i **arbetsflöden**. Klicka på **Avpublicera senare.**

      ![ej publicerade arbetsflöden](assets/unpublishworkflows.png)


<!--
End - Publish folders to Brand Portal
Start- Publish Collections to Brand Portal

-->

## Publicera samlingar på varumärkesportalen {#publish-collections-to-brand-portal}

Du kan publicera eller avpublicera samlingar från din AEM Resurser-instans.

>[!NOTE]
>
>Det går inte att publicera innehållsfragment till varumärkesportalen. Om du väljer innehållsfragment i AEM Resurser är därför åtgärden **[!UICONTROL Publicera på]** varumärkesportalen inte tillgänglig.
>
>Om samlingar som innehåller innehållsfragment publiceras från AEM Assets till Brand Portal, replikeras allt innehåll i mappen, förutom innehållsfragment, till gränssnittet Brand Portal.

### Publicera samlingar {#publish-a-collection-to-brand-portal}

Så här publicerar du samlingar från AEM Assets till varumärkesportalen:

1. Klicka på AEM-logotypen i användargränssnittet för AEM-resurser.
1. Från **navigeringssidan** går du till **[!UICONTROL Resurser]** > **[!UICONTROL Samlingar]**.
1. På **samlingskonsolen** väljer du de samlingar du vill publicera på varumärkesportalen.

   ![select_collection](assets/select_collection.png)

1. Klicka på **[!UICONTROL Publicera till varumärkesportal]** i verktygsfältet.
1. Klicka på **[!UICONTROL Publicera]** i bekräftelsedialogrutan.
1. Stäng bekräftelsemeddelandet.

   Logga in på varumärkesportalen som administratör. Den publicerade samlingen är tillgänglig i **[!UICONTROL samlingskonsolen]** .

   ![publicerad samling](assets/published_collection.png)

## Avpublicera samlingar {#unpublish-collections}

Du kan ta bort alla samlingar som publicerats på varumärkesportalen genom att avpublicera dem från din AEM Assets-instans. När du har avpublicerat den ursprungliga samlingen är dess kopia inte längre tillgänglig för Brand Portal-användarna.

Så här avpublicerar du samlingar:

1. Välj den samling som du vill avpublicera från Samlingar-konsolen för din AEM Resurser-instans.

   ![select_collection-1](assets/select_collection-1.png)

1. Klicka på ikonen **[!UICONTROL Ta bort från varumärkesportalen]** i verktygsfältet.
1. Klicka på **[!UICONTROL Avpublicera]** i dialogrutan.
1. Stäng bekräftelsemeddelandet. Samlingen tas bort från gränssnittet för varumärkesportalen.

Mer information om distribution av resurser, mappar och samlingar till slutanvändarna finns i dokumentationen [för](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) varumärkesportalen.

<!--

End - Publish Collections to Brand Portal

-->

