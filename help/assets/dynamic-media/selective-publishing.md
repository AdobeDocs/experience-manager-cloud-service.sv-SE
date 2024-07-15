---
title: Arbeta med Selektiv Publish i Dynamic Media
description: Lär dig hur du arbetar med Selektiv Publish i Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Publishing,Dynamic Media
role: User
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
source-git-commit: 26afff3a39a2a80c1f730287b99f3fb33bff0673
workflow-type: tm+mt
source-wordcount: '2544'
ht-degree: 0%

---

# Konfigurera selektiv Publish på mappnivå i Dynamic Media {#selective-publish-configure-folder}

Du kan välja att publicera eller avpublicera resurser till eller från Adobe Experience Manager eller Dynamic Media. Du kan göra det på mappnivå med antingen **[!UICONTROL Manage Publication]** eller **[!UICONTROL Quick Publish]**. Den här publiceringsmetoden är användbar eftersom den inte enbart är beroende av **[!UICONTROL Dynamic Media Configuration]** vars inställningar är globala för alla mappar i din Dynamic Media-instans.

Med selektiv publicering kan du till exempel arbeta med resurser för produkter som ännu inte är aktiva. I så fall kan marknadsföringsteamet få tillgång till smarta beskärningsbilder och dynamiska återgivningar som synkroniseras med Dynamic Media. De kan skapa marknadsföringsmaterial utan att behöva publicera materialet på Dynamic Media för global leverans.

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Om du kopierar* resurser till och från mappar rensas publiceringstillståndet för dessa resurser. När du *flyttar* resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]** behålls publiceringstillståndet för dessa resurser.

Om du senare bestämmer dig för att ändra inställningarna för **[!UICONTROL Selective Publish]** i en mapp, påverkar dessa ändringar endast nya resurser som du överför till den mappen från den tidpunkten och framåt. Publiceringsläget för befintliga resurser i mappen ändras inte förrän du ändrar dem manuellt från antingen **[!UICONTROL Quick Publish]** eller dialogrutan **[!UICONTROL Manage Publication]**.

Alternativet **[!UICONTROL Dynamic Media Publish mode]** på mappnivå är alltid som standard det värde som finns i inställningen **[!UICONTROL Publish Assets]** i **[!UICONTROL Dynamic Media Configuration]**. Följande steg i det här avsnittet visar emellertid hur du manuellt ändrar det här standardvärdet på mappnivå (vilket beskrivs i följande steg) för att åsidosätta värdet **[!UICONTROL Dynamic Media Configuration]**.

Oavsett om du förlitar dig på:

* Värdet **[!UICONTROL Publish Assets]** har angetts i **[!UICONTROL Dynamic Media Configuration]**
* Du kan också ange värdet **[!UICONTROL Dynamic Media Publish mode]** i egenskaper på mappnivå

Du kan fortfarande välja **[!UICONTROL Immediately]**, **[!UICONTROL Upon Activation]** eller **[!UICONTROL Selective Publish]**. Du kan till exempel ange värdet **[!UICONTROL Publish Assets]** i **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL On Activation]**. Du kan också ange **[!UICONTROL Dynamic Media Publish]**-lägesvärdet på mappnivå till **[!UICONTROL Selective Publish]**, omvänt och så vidare.

När du har konfigurerat selektiv publicering i en mapp kan du göra något av följande:

* [Publicera utvalda resurser på Dynamic Media eller Experience Manager med Hantera publikation](#selective-publish-manage-publication).
* [Avpublicera utvalda resurser från Dynamic Media eller Experience Manager med Hantera publikation](#selective-unpublish-manage-publication).
* [Publish-resurser till Dynamic Media eller Experience Manager med hjälp av Quick Publish](#quick-publish-aem-dm).
* [Publicera eller avpublicera resurser selektivt via sökresultat](#selective-publish-unpublish-search-results).

**Så här konfigurerar du selektiv Publish på mappnivå i Dynamic Media:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går sedan till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Gör något av följande:
   * Redigera egenskaperna för en befintlig mapp - Navigera i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** till en mapp vars egenskaper du vill redigera. Markera mappen och välj **[!UICONTROL Properties]** i verktygsfältet.
   * Redigera egenskaperna för en ny mapp - i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**, nära sidans övre högra hörn, gå till **[!UICONTROL Create]** > **[!UICONTROL Folder]**. Ange en rubrik (obligatoriskt) för mappen i dialogrutan **[!UICONTROL Create Folder]** och välj sedan **[!UICONTROL Create]**. Markera mappen och välj **[!UICONTROL Properties]** i verktygsfältet.

1. Välj något av följande i listrutan **[!UICONTROL Sync mode]**:

   | Synkroniseringsläge | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Inherited]** | Det finns inget explicit synkroniseringsvärde i mappen. I stället ärver mappen synkroniseringsvärdet från en av dess överordnade mappar eller det standardläge som angetts i **[!UICONTROL Dynamic Media Configuration]**. Detaljerad status för **[!UICONTROL Inherited]** visas med ett verktygstips. |
   | **[!UICONTROL Sync everything in this folder subtree to Dynamic Media]** | För att publiceringen till Dynamic Media ska lyckas måste materialet synkroniseras med Dynamic Media. Om du väljer det här alternativet inkluderas alla resurser i det här underträdet för synkronisering till Dynamic Media. De mappspecifika inställningarna åsidosätter standardinställningen i **[!UICONTROL Dynamic Media Configuration]**. |
   | **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** | Uteslut alla resurser i det här underträdet från synkronisering till Dynamic Media. |

   ![Selektiv publicering på mappnivå](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Välj ett alternativ i listrutan **[!UICONTROL Dynamic Media Publish mode]**. Alternativet **[!UICONTROL Dynamic Media Publish mode]** är alltid som standard det värde som anges i **[!UICONTROL Dynamic Media Configuration]**. Du kan dock manuellt åsidosätta det här standardvärdet för **[!UICONTROL Dynamic Media Configuration]** genom att använda något av följande alternativ.

   >[!IMPORTANT]
   >
   >Oavsett vilket alternativ för Dynamic Media Publish-läge du väljer publiceras uppdateringar som du senare gör för en resurs som redan är *publicerad* omedelbart utan någon ytterligare användaråtgärd.

   | Dynamic Media Publish-läge | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Immediately]** | När resurser överförs till den här mappen, importeras resurserna till Experience Manager och URL:en/inbäddningen anges omedelbart. Det här alternativet är knutet till publicering i Experience Manager och det behövs inga användaråtgärder för att publicera resurser.<br>Det här alternativet är *inte* tillgängligt om du valde **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** i **[!UICONTROL Sync mode]** i föregående steg. |
   | **[!UICONTROL Upon Activation]** | När resurser överförs till den här mappen måste du uttryckligen publicera resursen innan en URL/Embed-länk anges. Det här alternativet är endast knutet till Experience Manager-publicering.<br>Det här alternativet är *inte* tillgängligt om du valde **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** i **[!UICONTROL Sync mode]** i föregående steg. |
   | **[!UICONTROL Selective Publish]** | Assets publiceras i Experience Manager eller Dynamic Media för att distribueras offentligt. Båda publiceringsmetoderna utesluter varandra. Det innebär att du kan publicera resurser på DMS7 så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar. Eller så kan du publicera resurser exklusivt på Experience Manager för säker förhandsgranskning. Samma resurser publiceras *inte* till DMS7 för leverans i den offentliga domänen. Det här alternativet är inte tillgängligt om du valde **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** i **[!UICONTROL Sync mode]** i föregående steg. |

1. I det övre högra hörnet av sidan väljer du **[!UICONTROL Save & Close]** och sedan **[!UICONTROL OK]** för att återgå till Experience Manager Assets.

## Publicera valfritt material till Dynamic Media eller Experience Manager as a Cloud Service med Hantera publikation{#selective-publish-manage-publication}

Innan du kan använda **[!UICONTROL Manage Publication]** för att selektivt publicera resurser till Dynamic Media eller Experience Manager måste du göra något av följande:

* Ange alternativet **[!UICONTROL Publish Assets]** i **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL Selective Publish]**.
* Eller konfigurerad selektiv publicering på mappnivå.

Se [Skapa en Dynamic Media-konfiguration](#configuring-dynamic-media-cloud-services) eller [Konfigurera selektiv Publish på mappnivå i Dynamic Media](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Om du kopierar* resurser till och från mappar rensas publiceringstillståndet för dessa resurser. När du *flyttar* resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]** behålls publiceringstillståndet för dessa resurser.

**Så här publicerar du resurser selektivt till Dynamic Media eller Experience Manager as a Cloud Service med hjälp av Hantera publikation:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går sedan till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Gör något av följande i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och välj **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. Välj **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

     >[!NOTE]
     >
     >Om **[!UICONTROL Manage Publication]** inte visas i verktygsfältet markerar du ellipsknappen i stället och väljer sedan **[!UICONTROL Manage Publication]** på listmenyn.

1. På sidan **[!UICONTROL Manage Publication - Options]**, under **[!UICONTROL Action]**, väljer du vilken typ av aktivering du vill använda.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Publish]** (till Experience Manager) | Markera det här alternativet om du vill publicera resurser på Experience Manager för säker förhandsvisning. |
   | **[!UICONTROL Publish to Dynamic Media]** | Välj det här alternativet om du vill publicera resurser på Dynamic Media för att distribuera dem till den offentliga domänen eller för att använda funktioner som Smart beskärning eller dynamiska återgivningar.<br>Det här alternativet är bara tillgängligt om **[!UICONTROL Dynamic Media Publish mode]** är inställt på **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Ange publiceringens tidsinställning under **[!UICONTROL Schedule]**.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj att publicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill publicera resurserna ett visst datum och en viss tid. |

1. Välj **[!UICONTROL Next]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication]**.
1. Gör något av följande på sidan **[!UICONTROL Manage Publication - Scope]**:
   * Om det behövs väljer du en eller flera resurser som du vill ta bort från publiceringen.
   * Välj **[!UICONTROL Publish]** eller **[!UICONTROL Publish to Dynamic Media]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication - Scope]**.
1. Välj **[!UICONTROL OK]**.

### Avpublicera valfritt material från Dynamic Media eller Experience Manager med Hantera publikation {#selective-unpublish-manage-publication}

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går sedan till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Gör något av följande i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**:
   * Navigera till en mapp vars resurser du vill avpublicera. Markera mappen och välj **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill avpublicera. Öppna mappen och välj sedan en eller flera resurser. Välj **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

     >[!NOTE]
     >
     >Om **[!UICONTROL Manage Publication]** inte visas i verktygsfältet markerar du ellipsknappen i stället och väljer sedan **[!UICONTROL Manage Publication]** på listmenyn.

1. På sidan **[!UICONTROL Manage Publication - Options]**, under **[!UICONTROL Action]**, väljer du vilken typ av avaktivering du vill ha.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Unpublish]** (från Experience Manager) | Om du vill avpublicera resurser från Experience Manager väljer du det här alternativet. |
   | **[!UICONTROL Unpublish from Dynamic Media]** | Om du vill avpublicera resurser från Dynamic Media väljer du det här alternativet.<br>Det här alternativet är bara tillgängligt om **[!UICONTROL Dynamic Media Publish mode]** är inställt på **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Under **[!UICONTROL Schedule]** anger du tidpunkten för avaktiveringen.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj det här alternativet om du vill avpublicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill avpublicera resurserna ett visst datum och en viss tid. |

1. Välj **[!UICONTROL Next]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication]**.
1. Gör något av följande på sidan **[!UICONTROL Manage Publication - Scope]**:
   * Markera en eller flera resurser som du vill ta bort från avpubliceringen.
   * Välj **[!UICONTROL Unpublish]** eller **[!UICONTROL Unpublish from Dynamic Media]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication - Scope]**.
1. Välj **[!UICONTROL OK]**.

## Publish-material till Dynamic Media eller Experience Manager med Quick Publish {#quick-publish-aem-dm}

Du kan använda **[!UICONTROL Quick Publish]** för enkla resursaktiveringsärenden. **[!UICONTROL Quick Publish]** publicerar de valda resurserna omedelbart utan ytterligare användarinteraktion. Alla icke-publicerade referenser publiceras också automatiskt.

>[!NOTE]
>
>Om du vill använda **[!UICONTROL Quick Publish]** för att publicera resurser på Dynamic Media eller Experience Manager måste **[!UICONTROL Selective Publish]** vara aktiverat i **[!UICONTROL Dynamic Media Configuration]** eller i mappegenskaperna för den markerade mappen.

**Så här publicerar du resurser till Dynamic Media eller Experience Manager med Quick Publish:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster på sidan väljer du navigeringsikonen (precis ovanför verktygsikonen) och till höger på sidan går du till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Gör något av följande i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och välj **[!UICONTROL Quick Publish]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. Välj **[!UICONTROL Quick Publish]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

     >[!NOTE]
     >
     >Om **[!UICONTROL Quick Publish]** inte visas i verktygsfältet markerar du ellipsknappen i stället och väljer sedan **[!UICONTROL Quick Publish]** på listmenyn.

     ![Snabb Publish på mappnivå till Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Välj något av följande alternativ i menylistan **[!UICONTROL Quick Publish]**.

   | Snabb Publish-alternativ | Vad det gör |
   | --- | --- | 
   | Publish till Experience Manager | Publicerar de markerade resurserna direkt till Experience Manager. |
   | Publish till Brand Portal | Publicerar de markerade resurserna direkt till **[!UICONTROL Brand Portal]**.<br>Det här alternativet är bara tillgängligt om din Experience Manager Assets-instans redan har konfigurerat **[!UICONTROL Brand Portal]**. |
   | Publish till Dynamic Media | Publicerar de markerade resurserna direkt till Dynamic Media.<br>En resurs måste redan synkroniseras till Dynamic Media. Om det behövs kontrollerar du att **[!UICONTROL Sync mode]** i en mapps egenskaper redan är inställda på **[!UICONTROL Sync everything in this folder subtree to Dynamic Media]**. |

1. Välj **[!UICONTROL OK]** och sedan **[!UICONTROL Close]**.

## Publicera eller avpublicera resurser selektivt via sökresultat {#selective-publish-unpublish-search-results}

Sökresultaten kan visa resurser från olika resursmappar med olika publiceringsinställningar för Dynamic Media. Om du har valt en eller flera resurser från sökresultaten och resurserna har olika publiceringslägesinställningar för Dynamic Media, kan du utlösa **[!UICONTROL Manage Publication]** från verktygsfältet för att publicera eller avpublicera.

Se även [Söka efter resurser i Experience Manager](/help/assets/search-assets.md).

**Om du vill publicera eller avpublicera resurser selektivt via sökresultat:**

1. I Experience Manager i det övre vänstra hörnet av sidan väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster på sidan väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går sedan till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. I verktygsfältet, i det övre högra hörnet på sidan, väljer du ikonen Sök (förstoringsglas).
1. Ange ett nyckelord i textfältet **[!UICONTROL Type to search]** och tryck sedan på **[!UICONTROL Enter]**.
1. I närheten av sidans övre högra hörn väljer du ikonen **[!UICONTROL List View]**.
1. I närheten av sidans övre vänstra hörn väljer du ikonen **[!UICONTROL Filters]**.

   ![Listvy och filter i sökresultat](/help/assets/assets-dm/select-publish-search-result.png)

1. Expandera **[!UICONTROL Status]** i den vänstra panelen och expandera sedan **[!UICONTROL Dynamic Media]**-sökpredikatet.
1. Använd kryssrutorna **[!UICONTROL Published]** och **[!UICONTROL Unpublished]** om du vill förfina sökresultaten ytterligare baserat på det publicerade läget för Dynamic Media-resurser.
Du kan också använda de här kryssrutorna med **[!UICONTROL Publish]**-sökpredikatet för att förfina sökresultaten för **[!UICONTROL Published]**- och **[!UICONTROL Unpublished]** Experience Manager-resurser.
1. Gör något av följande:
   * Markera en eller flera resurser som du vill publicera eller avpublicera.
   * Välj **[!UICONTROL Select All]** i det övre högra hörnet på sidan **[!UICONTROL Search Results]**.
1. Välj **[!UICONTROL Manage Publication]** i verktygsfältet. Om det behövs väljer du ellipsikonen i verktygsfältet för att visa **[!UICONTROL Manage Publication]**.
1. Välj önskad åtgärd på sidan **[!UICONTROL Manage Publication - Options]**.

   | Markerad åtgärd | Inställningen Publish Assets i Dynamic Media Configuration | Assets är |
   | --- | --- | --- |
   | Publish | Omedelbart eller vid aktivering | Publicerat i Experience Manager och Dynamic Media. |
   | Publish | Selektiv Publish | Publicerat endast i Experience Manager. |
   | Avpublicera | Omedelbart eller vid aktivering | Opublicerat från Experience Manager och Dynamic Media. |
   | Avpublicera | Selektiv Publish | Endast opublicerad från Experience Manager. |
   | Publish till Dynamic Media | Omedelbart eller vid aktivering | Publiceras inte till Experience Manager, Dynamic Media eller båda. |
   | Publish till Dynamic Media | Selektiv Publish | Endast publicerat till Dynamic Media. |
   | Avpublicera från Dynamic Media | Omedelbart eller vid aktivering | Inte opublicerat från Experience Manager, Dynamic Media eller båda. |
   | Avpublicera från Dynamic Media | Selektiv Publish | Endast opublicerad från Dynamic Media. |

1. Under **[!UICONTROL Schedule]** anger du tidpunkten för avaktiveringen.

   | Valt schema | Vad händer |
   | --- | --- |
   | Nu | Den valda åtgärden utförs omedelbart. |
   | Senare | Den valda åtgärden körs på det valda datumet och den valda tiden. |

1. Välj **[!UICONTROL Next]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication - Options]**.
1. (Valfritt) Granska kolumnen **[!UICONTROL Publish Target]** i tabellen på sidan **[!UICONTROL Manage Publication - Scope]** för de valda resurserna.

   | Inställningen Publish Assets i Dynamic Media Configuration | Markerad åtgärd | Publish target |
   | --- | --- | --- |
   | Omedelbart eller <br>vid aktivering | Publish | Experience Manager och Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Publish till Dynamic Media | Ingen |
   | Selektiv Publish | Publish | Experience Manager |
   | Selektiv Publish | Publish till Dynamic Media | Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Avpublicera | Experience Manager och Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Avpublicera från Dynamic Media | Ingen |
   | Selektiv Publish | Avpublicera | Experience Manager |
   | Selektiv Publish | Avpublicera från Dynamic Media | Dynamic Media |

1. Gör något av följande på sidan **[!UICONTROL Manage Publication - Scope]**:
   * Markera en eller flera resurser som du vill ta bort från publicering eller avpublicering.
   * I det övre högra hörnet på sidan **[!UICONTROL Manage Publication - Scope]** väljer du **[!UICONTROL Publish]** eller **[!UICONTROL Unpublish]** för att påbörja åtgärden.
1. Välj **[!UICONTROL OK]**.

## Kontrollera publiceringsstatus för en resurs {#check-publish-status-of-asset}

Du kan använda **[!UICONTROL Timeline]** med **[!UICONTROL Card view]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** i Experience Manager för att snabbt kontrollera publiceringstillståndet för en resurs.

**Så här kontrollerar du publiceringsstatusen för en resurs:**

1. I Experience Manager i det övre vänstra hörnet av sidan väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster på sidan väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går sedan till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Öppna en mapp som innehåller resurser som du har publicerat eller opublicerat i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** (skärmbilden nedan visar **[!UICONTROL List View]**).
1. Markera en resurs så att den visas med en bock. Se skärmbilden nedan.
1. Välj **[!UICONTROL Timeline]** i listrutan nära sidans övre vänstra hörn. Regionen **[!UICONTROL Status]** i den vänstra panelen visar den valda resursens publiceringstillstånd.
När du använder **[!UICONTROL List View]** visas en extra kolumn för publiceringstillståndet **[!UICONTROL Dynamic Media]**.
   * En mapp som är konfigurerad att synkronisera till Dynamic Media visar kolumnen **[!UICONTROL Dynamic Media]** som standard.
   * En mapp som *inte* är konfigurerad att synkronisera till Dynamic Media visar inte Dynamic Media-kolumnen.
     ![Listvy och tidslinje](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Felsöka selektiv Publish {#selective-publish-troubleshoot}

En resurs som inte synkroniseras med Dynamic Media men som har en publiceringsåtgärd från Dynamic Media aktiverad resulterar i följande felmeddelande och lösning:

![Selektivt Publish-fel](/help/assets/assets-dm/selective-publish-error.png)
