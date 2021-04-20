---
title: Arbeta med selektiv publicering i Dynamic Media
description: Lär dig hur du arbetar med selektiv publicering i Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
topic: Business Practitioner
role: Business Practitioner
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '2535'
ht-degree: 1%

---

# Konfigurera selektiv publicering på mappnivå i Dynamic Media {#selective-publish-configure-folder}

Du kan välja att publicera eller avpublicera resurser till eller från Adobe Experience Manager eller Dynamic Media på mappnivå med antingen **[!UICONTROL Manage Publication]** eller **[!UICONTROL Quick Publish]**. Den här publiceringsmetoden är användbar eftersom den inte enbart använder **[!UICONTROL Dynamic Media Configuration]** vars inställningar är globala för alla mappar i din Dynamic Media-instans.

Med selektiv publicering kan du till exempel arbeta med resurser för produkter som ännu inte är aktiva. I så fall kan marknadsföringsteamet få tillgång till smarta beskärningsbilder och dynamiska återgivningar som synkroniseras med Dynamic Media. De kan skapa marknadsföringsmaterial utan att behöva publicera materialet på Dynamic Media för global leverans.

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Om du* kopierar resurser till och från mappar rensas publiceringstillståndet för dessa resurser. När du *flyttar*-resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]** behålls publiceringstillståndet för dessa resurser.

Om du senare bestämmer dig för att ändra **[!UICONTROL Selective Publish]**-inställningarna i en mapp påverkar de ändringarna bara nya resurser som du överför till den mappen från den punkten och framåt. Publiceringsläget för befintliga resurser i mappen ändras inte förrän du ändrar dem manuellt från antingen **[!UICONTROL Quick Publish]** eller **[!UICONTROL Manage Publication]**-dialogrutan.

Alternativet **[!UICONTROL Dynamic Media Publish mode]** på mappnivå är alltid det värde som finns i **[!UICONTROL Publish Assets]**-inställningen i **[!UICONTROL Dynamic Media Configuration]**. Följande steg i det här avsnittet visar emellertid hur du manuellt ändrar det här standardvärdet på mappnivå (vilket beskrivs i följande steg) för att åsidosätta **[!UICONTROL Dynamic Media Configuration]**-värdet.

Oavsett om du förlitar dig på:

* Värdet **[!UICONTROL Publish Assets]** har angetts i **[!UICONTROL Dynamic Media Configuration]**
* Du kan också ange **[!UICONTROL Dynamic Media Publish mode]**-värdet i mappnivåegenskaperna

Du kan fortfarande välja **[!UICONTROL Immediately]**, **[!UICONTROL Upon Activation]** eller **[!UICONTROL Selective Publish]**. Du kan till exempel ange **[!UICONTROL Publish Assets]**-värdet i **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL Upon Activation]**. Du kan också ställa in lägesvärdet **[!UICONTROL Dynamic Media Publish]** på mappnivå till **[!UICONTROL Selective Publish]**, omvänt och så vidare.

När du har konfigurerat selektiv publicering i en mapp kan du göra något av följande:

* [Publicera valfritt material på Dynamic Media eller Experience Manager med Hantera publikation](#selective-publish-manage-publication).
* [Avpublicera valfritt material från Dynamic Media eller Experience Manager med Hantera publikation](#selective-unpublish-manage-publication).
* [Publicera material på Dynamic Media eller Experience Manager med Snabbpublicering](#quick-publish-aem-dm).
* [Publicera eller avpublicera resurser selektivt via sökresultat](#selective-publish-unpublish-search-results).

**Konfigurera selektiv publicering på mappnivå i Dynamic Media**

1. Tryck på Experience Manager-logotypen i Experience Manager för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen till vänster (alldeles ovanför verktygsikonen) och tryck sedan på **[!UICONTROL Assets > Files]**.
1. Gör något av följande:
   * Redigera egenskaperna för en befintlig mapp - Navigera i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** till en mapp vars egenskaper du vill redigera. Markera mappen och tryck sedan på **[!UICONTROL Properties]** i verktygsfältet.
   * Redigera egenskaperna för en ny mapp - I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**, nära sidans övre högra hörn, tryck på **[!UICONTROL Create > Folder]**. Ange en rubrik (krävs) för mappen i dialogrutan **[!UICONTROL Create Folder]** och tryck sedan på **[!UICONTROL Create]**. Markera mappen och tryck sedan på **[!UICONTROL Properties]** i verktygsfältet.

1. Välj något av följande i listrutan **[!UICONTROL Sync mode]**:

   | Synkroniseringsläge | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Inherited]** | Det finns inget explicit synkroniseringsvärde för mappen; I stället ärver mappen synkroniseringsvärdet från en av dess överordnade mappar eller det standardläge som angetts i **[!UICONTROL Dynamic Media Configuration]**. Detaljerad status för **[!UICONTROL Inherited]** visas med ett verktygstips. |
   | **[!UICONTROL Sync everything in this folder subtree to Dynamic Media]** | För att publiceringen till Dynamic Media ska lyckas måste materialet synkroniseras med Dynamic Media. Om du väljer det här alternativet inkluderas alla resurser i det här underträdet för synkronisering till Dynamic Media. De mappspecifika inställningarna åsidosätter standardinställningen i **[!UICONTROL Dynamic Media Configuration]**. |
   | **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** | Uteslut alla resurser i det här underträdet från synkronisering till Dynamic Media. |

   ![Selektiv publicering på mappnivå](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Välj ett alternativ i listrutan **[!UICONTROL Dynamic Media Publish mode]**. Alternativet **[!UICONTROL Dynamic Media Publish mode]** är alltid som standard det värde som anges i **[!UICONTROL Dynamic Media Configuration]**. Du kan dock manuellt åsidosätta det här standardvärdet för **[!UICONTROL Dynamic Media Configuration]** genom att använda något av följande alternativ.

   >[!IMPORTANT]
   >
   >Oavsett vilket alternativ för publiceringsläget i Dynamic Media du väljer publiceras uppdateringar som du senare gör på en resurs som *redan* har publicerats omedelbart utan någon ytterligare användaråtgärd.

   | Publiceringsläge för Dynamic Media | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Immediately]** | När resurser överförs till den här mappen, importeras resurserna till Experience Manager och URL:en/inbäddningen anges omedelbart. Det här alternativet är knutet till publicering i Experience Manager och det behövs inga användaråtgärder för att publicera resurser.<br>Det här alternativet är  ** inte tillgängligt om du valde  **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** i  **[!UICONTROL Sync mode]** föregående steg. |
   | **[!UICONTROL Upon Activation]** | När resurser överförs till den här mappen måste du uttryckligen publicera resursen innan en URL/Embed-länk anges. Det här alternativet är endast knutet till Experience Manager-publicering.<br>Det här alternativet är  ** inte tillgängligt om du valde  **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** i  **[!UICONTROL Sync mode]** föregående steg. |
   | **[!UICONTROL Selective Publish]** | Resurser publiceras till Experience Manager eller till Dynamic Media för att distribueras offentligt. Båda publiceringsmetoderna utesluter varandra. Det innebär att du kan publicera resurser på DMS7 så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar. Eller så kan du publicera resurser exklusivt på Experience Manager för säker förhandsgranskning. samma resurser är *inte* publicerade till DMS7 för distribution i den offentliga domänen. Det här alternativet är inte tillgängligt om du valde **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** i **[!UICONTROL Sync mode]** i föregående steg. |

1. Tryck på **[!UICONTROL Save & Close]** längst upp till höger på sidan och tryck sedan på **[!UICONTROL OK]** för att återgå till Experience Manager Assets.

## Publicera utvalda resurser på Dynamic Media eller Experience Manager som en Cloud Service med Hantera publikation{#selective-publish-manage-publication}

Innan du kan använda **[!UICONTROL Manage Publication]** för att selektivt publicera resurser till Dynamic Media eller Experience Manager måste du göra något av följande:

* Ställ in alternativet **[!UICONTROL Publish Assets]** i **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL Selective Publish]**.
* Eller konfigurerad selektiv publicering på mappnivå.

Se [Skapa en Dynamic Media-konfiguration](#configuring-dynamic-media-cloud-services) eller [Konfigurera selektiv publicering på mappnivå i Dynamic Media](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Om du* kopierar resurser till och från mappar rensas publiceringstillståndet för dessa resurser. När du *flyttar*-resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]** behålls publiceringstillståndet för dessa resurser.

**Publicera utvalda resurser på Dynamic Media eller Experience Manager som en Cloud Service med Hantera publikation**

1. Tryck på Experience Manager-logotypen i Experience Manager för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen till vänster (alldeles ovanför verktygsikonen) och tryck sedan på **[!UICONTROL Assets > Files]**.
1. Gör något av följande i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och tryck sedan på **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. Tryck på **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >Om **[!UICONTROL Manage Publication]** inte visas i verktygsfältet trycker du i stället på ellipsknappen och väljer sedan **[!UICONTROL Manage Publication]** i listrutan.

1. På sidan **[!UICONTROL Manage Publication - Options]**, under **[!UICONTROL Action]**, väljer du vilken typ av aktivering du vill använda.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Publish]** (till Experience Manager) | Markera det här alternativet om du vill publicera resurser på Experience Manager för säker förhandsvisning. |
   | **[!UICONTROL Publish to Dynamic Media]** | Välj det här alternativet om du vill publicera resurser på Dynamic Media för att distribuera dem till den offentliga domänen eller så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar.<br>Det här alternativet är bara tillgängligt om  **[!UICONTROL Dynamic Media Publish mode]** har angetts  **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Under **[!UICONTROL Schedule]** anger du tidsinställningen för publiceringen.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj att publicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill publicera resurserna ett visst datum och en viss tid. |

1. Tryck på **[!UICONTROL Next]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication]**.
1. Gör något av följande på sidan **[!UICONTROL Manage Publication - Scope]**:
   * Om det behövs väljer du en eller flera resurser som du vill ta bort från publiceringen.
   * Tryck på **[!UICONTROL Publish]** eller **[!UICONTROL Publish to Dynamic Media]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication - Scope]**.
1. Tryck på **[!UICONTROL OK]**.

### Avpublicera valfritt material från Dynamic Media eller Experience Manager med Manage Publication {#selective-unpublish-manage-publication}

1. Tryck på Experience Manager-logotypen i Experience Manager för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen till vänster (alldeles ovanför verktygsikonen) och tryck sedan på **[!UICONTROL Assets > Files]**.
1. Gör något av följande i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**:
   * Navigera till en mapp vars resurser du vill avpublicera. Markera mappen och tryck sedan på **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill avpublicera. Öppna mappen och välj sedan en eller flera resurser. Tryck på **[!UICONTROL Manage Publication]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >Om **[!UICONTROL Manage Publication]** inte visas i verktygsfältet trycker du i stället på ellipsknappen och väljer sedan **[!UICONTROL Manage Publication]** i listrutan.

1. På sidan **[!UICONTROL Manage Publication - Options]**, under **[!UICONTROL Action]**, väljer du vilken typ av avaktivering du vill använda.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Unpublish]** (från Experience Manager) | Om du vill avpublicera resurser från Experience Manager väljer du det här alternativet. |
   | **[!UICONTROL Unpublish from Dynamic Media]** | Om du vill avpublicera resurser från Dynamic Media väljer du det här alternativet.<br>Det här alternativet är bara tillgängligt om  **[!UICONTROL Dynamic Media Publish mode]** har angetts  **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Under **[!UICONTROL Schedule]** anger du tidpunkten för avaktiveringen.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj att avpublicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill avpublicera resurserna ett visst datum och en viss tid. |

1. Tryck på **[!UICONTROL Next]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication]**.
1. Gör något av följande på sidan **[!UICONTROL Manage Publication - Scope]**:
   * Markera en eller flera resurser som du vill ta bort från avpubliceringen.
   * Tryck på **[!UICONTROL Unpublish]** eller **[!UICONTROL Unpublish from Dynamic Media]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication - Scope]**.
1. Tryck på **[!UICONTROL OK]**.

## Publicera material till Dynamic Media eller Experience Manager med Snabbpublicering {#quick-publish-aem-dm}

Du kan använda **[!UICONTROL Quick Publish]** för enkla resursaktiveringsfall. **[!UICONTROL Quick Publish]** publicerar de markerade resurserna omedelbart utan ytterligare användarinteraktion. Alla icke-publicerade referenser publiceras också automatiskt.

>[!NOTE]
>
>Om du vill använda **[!UICONTROL Quick Publish]** för att publicera resurser på Dynamic Media eller Experience Manager måste du kontrollera att **[!UICONTROL Selective Publish]** är aktiverat i **[!UICONTROL Dynamic Media Configuration]** eller i mappegenskaperna för den markerade mappen.

**Så här publicerar du material till Dynamic Media eller Experience Manager med Snabbpublicering:**

1. Tryck på Experience Manager-logotypen i Experience Manager för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (precis ovanför verktygsikonen) till vänster på sidan och tryck sedan på **[!UICONTROL Assets > Files]** till höger på sidan.
1. Gör något av följande i **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]**:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och tryck sedan på **[!UICONTROL Quick Publish]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. Tryck på **[!UICONTROL Quick Publish]** i verktygsfältet. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >Om **[!UICONTROL Quick Publish]** inte visas i verktygsfältet trycker du i stället på ellipsknappen och väljer sedan **[!UICONTROL Quick Publish]** i listrutan.

      ![Snabbpublicering på mappnivå till Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Välj något av följande alternativ i menylistan **[!UICONTROL Quick Publish]**.

   | Snabbpublicering, alternativ | Vad det gör |
   | --- | --- | 
   | Publicera i Experience Manager | Publicerar de markerade resurserna direkt till Experience Manager. |
   | Publicera på varumärkesportal | Publicerar de markerade resurserna direkt till **[!UICONTROL Brand Portal]**.<br>Det här alternativet är bara tillgängligt om du  **[!UICONTROL Brand Portal]** redan har konfigurerat instansen Experience Manager Assets. |
   | Publicera till Dynamic Media | Publicerar de markerade resurserna direkt till Dynamic Media.<br>En resurs måste redan synkroniseras till Dynamic Media. Om det behövs kontrollerar du att **[!UICONTROL Sync mode]** i en mapps egenskaper redan är inställda på **[!UICONTROL Sync everything in this folder subtree to Dynamic Media]**. |

1. Tryck på **[!UICONTROL OK,]** och sedan på **[!UICONTROL Close]**.

## Publicera eller avpublicera resurser selektivt via sökresultat {#selective-publish-unpublish-search-results}

Sökresultaten kan visa resurser från olika resursmappar med olika publiceringsinställningar för Dynamic Media. Om du har valt en eller flera resurser från sökresultaten och resurserna har olika publiceringslägesinställningar för Dynamic Media, kan du aktivera **[!UICONTROL Manage Publication]** från verktygsfältet för att publicera eller avpublicera.

Se även [Sök efter resurser i Experience Manager](/help/assets/search-assets.md).

**Publicera eller avpublicera resurser selektivt via sökresultat**

1. I Experience Manager i det övre vänstra hörnet av sidan trycker du på Experience Manager-logotypen för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (precis ovanför verktygsikonen) till vänster på sidan och tryck sedan på **[!UICONTROL Assets > Files]**.
1. I verktygsfältet, i det övre högra hörnet på sidan, trycker du på ikonen Sök (förstoringsglas).
1. Ange ett nyckelord i textfältet **[!UICONTROL Type to search]** och tryck sedan på **[!UICONTROL Enter]**.
1. I det övre högra hörnet av sidan trycker du på ikonen **[!UICONTROL List View]**.
1. I närheten av sidans övre vänstra hörn trycker du på ikonen **[!UICONTROL Filters]**.

   ![Listvy och filter i sökresultat](/help/assets/assets-dm/select-publish-search-result.png)

1. Expandera **[!UICONTROL Status]** i den vänstra panelen och expandera sedan **[!UICONTROL Dynamic Media]**-sökpredikatet.
1. Använd kryssrutorna **[!UICONTROL Published]** och **[!UICONTROL Unpublished]** om du vill förfina sökresultaten ytterligare baserat på det publicerade läget för Dynamic Media-resurser.
Du kan också använda de här kryssrutorna med **[!UICONTROL Publish]**-sökpredikatet för att förfina sökresultaten för **[!UICONTROL Published]**- och **[!UICONTROL Unpublished]**-Experience Manager-resurser.
1. Gör något av följande:
   * Markera en eller flera resurser som du vill publicera eller avpublicera.
   * I det övre högra hörnet av sidan **[!UICONTROL Search Results]** trycker du på **[!UICONTROL Select All]**.
1. Tryck på **[!UICONTROL Manage Publication]** i verktygsfältet. Om det behövs kan du trycka på ellipsikonen i verktygsfältet för att visa **[!UICONTROL Manage Publication]**.
1. Välj önskad åtgärd på sidan **[!UICONTROL Manage Publication - Options]**.

   | Markerad åtgärd | Inställningen Publicera resurser i Dynamic Media Configuration | Resurserna är |
   | --- | --- | --- |
   | Publicera | Omedelbart eller vid aktivering | Publicerat i Experience Manager och Dynamic Media. |
   | Publicera | Selektiv publicering | Publicerat endast i Experience Manager. |
   | Avpublicera | Omedelbart eller vid aktivering | Opublicerat från Experience Manager och Dynamic Media. |
   | Avpublicera | Selektiv publicering | Endast opublicerad från Experience Manager. |
   | Publicera till Dynamic Media | Omedelbart eller vid aktivering | Publiceras inte till Experience Manager, Dynamic Media eller båda. |
   | Publicera till Dynamic Media | Selektiv publicering | Endast publicerat till Dynamic Media. |
   | Avpublicera från Dynamic Media | Omedelbart eller vid aktivering | Inte opublicerat från Experience Manager, Dynamic Media eller båda. |
   | Avpublicera från Dynamic Media | Selektiv publicering | Endast opublicerad från Dynamic Media. |

1. Under **[!UICONTROL Schedule]** anger du tidpunkten för avaktiveringen.

   | Valt schema | Vad händer |
   | --- | --- |
   | Nu | Den valda åtgärden utförs omedelbart. |
   | Senare | Den valda åtgärden körs på det valda datumet och den valda tiden. |

1. Tryck på **[!UICONTROL Next]** i det övre högra hörnet på sidan **[!UICONTROL Manage Publication - Options]**.
1. (Valfritt) På sidan **[!UICONTROL Manage Publication - Scope]** granskar du kolumnen **[!UICONTROL Publish Target]** i tabellen för de valda resurserna.

   | Inställningen Publicera resurser i Dynamic Media Configuration | Markerad åtgärd | Publicera mål |
   | --- | --- | --- |
   | Omedelbart eller <br>vid aktivering | Publicera | Experience Manager och Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Publicera till Dynamic Media | Inget |
   | Selektiv publicering | Publicera | Experience Manager |
   | Selektiv publicering | Publicera till Dynamic Media | Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Avpublicera | Experience Manager och Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Avpublicera från Dynamic Media | Inget |
   | Selektiv publicering | Avpublicera | Experience Manager |
   | Selektiv publicering | Avpublicera från Dynamic Media | Dynamic Media |

1. Gör något av följande på sidan **[!UICONTROL Manage Publication - Scope]**:
   * Markera en eller flera resurser som du vill ta bort från publicering eller avpublicering.
   * Tryck på **[!UICONTROL Publish]** eller **[!UICONTROL Unpublish]** i det övre högra hörnet av **[!UICONTROL Manage Publication - Scope]**-sidan för att påbörja åtgärden.
1. Tryck på **[!UICONTROL OK]**.

## Kontrollera publiceringsstatus för en resurs {#check-publish-status-of-asset}

Du kan använda **[!UICONTROL Timeline]** med **[!UICONTROL Card view]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** i Experience Manager för att snabbt kontrollera publiceringstillståndet för en resurs.

**Kontrollera publiceringsstatus för en resurs**

1. I Experience Manager i det övre vänstra hörnet av sidan trycker du på Experience Manager-logotypen för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (precis ovanför verktygsikonen) till vänster på sidan och tryck sedan på **[!UICONTROL Assets > Files]**.
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** (skärmbilden nedan visar **[!UICONTROL List View]**) öppnar du en mapp som innehåller resurser som du har publicerat eller opublicerat.
1. Markera en resurs så att den visas med en bock. Se skärmbilden nedan.
1. Välj **[!UICONTROL Timeline]** i den nedrullningsbara menyn nära sidans övre vänstra hörn. Regionen **[!UICONTROL Status]** i den vänstra panelen visar den valda resursens publiceringstillstånd.
När du använder **[!UICONTROL List View]** visas en extra kolumn för **[!UICONTROL Dynamic Media]**-publiceringstillstånd.
   * En mapp som är konfigurerad att synkronisera till Dynamic Media visar kolumnen **[!UICONTROL Dynamic Media]** som standard.
   * En mapp som är *inte* konfigurerad att synkronisera till Dynamic Media visar inte Dynamic Media-kolumnen.
      ![Listvy och tidslinje](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Felsökning av selektiv publicering {#selective-publish-troubleshoot}

En resurs som inte synkroniseras med Dynamic Media men som har en publiceringsåtgärd från Dynamic Media aktiverad resulterar i följande felmeddelande och lösning:

![Selektivt publiceringsfel](/help/assets/assets-dm/selective-publish-error.png)
