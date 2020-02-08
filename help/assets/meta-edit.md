---
title: Redigera eller lägga till metadata
description: Lär dig mer om metadata för resurser i AEM Resurser och olika sätt att redigera metadata för resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Redigera eller lägga till metadata {#how-to-edit-or-add-metadata}

Metadata är ytterligare information om resursen som kan sökas igenom. Den extraheras automatiskt när du överför en bild. Du kan redigera befintliga metadata eller lägga till nya metadataegenskaper i befintliga fält (till exempel när ett metadatafält är tomt).

Eftersom företag behöver kontrollerade och tillförlitliga metadata-ordlistor går det inte att lägga till nya metadataegenskaper i AEM Resurser. Även om författare inte kan lägga till nya metadatafält för resurser kan utvecklare göra det. Se [Skapa ny metadataegenskap för resurser](meta-edit.md#editing-metadata-schema).

## Redigera metadata för en resurs {#editing-metadata-for-an-asset}

Så här redigerar du metadata:

1. Gör något av följande:

   * I resursgränssnittet markerar du resursen och klickar/trycker på ikonen **[!UICONTROL Visa egenskaper]** i verktygsfältet.
   * Välj snabbåtgärden **[!UICONTROL Visa egenskaper]** i miniatyrbilden av resursen.
   * Klicka/tryck på **[!UICONTROL Visa egenskaper]** i verktygsfältet på resurssidan.
   Resurssidan visar alla metadata för resursen. Dessa metadata extraherades automatiskt när de överfördes (överfördes) till AEM Assets.

1. Redigera metadata på de olika flikarna efter behov och klicka/tryck sedan på **[!UICONTROL Spara]** i verktygsfältet när du är klar. Klicka/tryck på **[!UICONTROL Stäng]** för att återgå till webbgränssnittet Resurser.

   >[!NOTE]
   >
   >Om ett textfält är tomt finns det ingen befintlig metadatauppsättning. Du kan ange ett värde i fältet och spara det för att lägga till metadataegenskapen.

Alla ändringar av metadata för en resurs skrivs tillbaka till den ursprungliga binärfilen som en del av dess XMP-data. Detta görs via arbetsflödet för återskrivning av AEM-metadata. Ändringar som görs i befintliga egenskaper (t.ex. `dc:title`) skrivs över och nya egenskaper (inklusive anpassade egenskaper som `cq:tags`) läggs ihop med schemat.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Redigerar metadataschema {#editing-metadata-schema}

Mer information om hur du redigerar metadatamatchema finns i [Redigera metadatamatchformulär](metadata-schemas.md#edit-metadata-schema-forms).

## Registrera ett anpassat namnutrymme i AEM {#registering-a-custom-namespace-within-aem}

Du kan lägga till egna namnutrymmen i AEM. Precis som det finns fördefinierade namnutrymmen som cq, jcr och sling kan du ha ett namnutrymme för databasens metadata och XML-bearbetning.

1. Gå till administrationssidan för nodtypen *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Klicka eller tryck på **[!UICONTROL Namnutrymmen]** högst upp på sidan. Namnutrymmesadministrationssidan visas i ett fönster.

1. Om du vill lägga till ett namnutrymme klickar eller trycker du på **[!UICONTROL Nytt]** längst ned.
1. Ange ett anpassat namnutrymme i XML-namnutrymmeskonventionen (ange id:t i form av en URI och ett associerat prefix för id:t) och klicka eller tryck på **[!UICONTROL Spara]**.
