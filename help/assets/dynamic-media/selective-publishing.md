---
title: Arbeta med selektiv publicering i Dynamic Media
description: Information om hur du arbetar med selektiv publicering i dynamiska media.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 04f40452ca89bc5298341b4338bc1d7762b908c2
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 1%

---


# Konfigurera selektiv publicering på mappnivå i Dynamic Media {#selective-publish-configure-folder}

Du kan välja att publicera eller avpublicera resurser till eller från AEM eller Dynamic Media på mappnivå, antingen **[!UICONTROL Manage Publication]** eller **[!UICONTROL Quick Publish]** istället för att förlita dig enbart på **[!UICONTROL Dynamic Media Configuration]** vars inställningar är globala för alla mappar i din Dynamic Media-instans.

Med selektiv publicering kan du till exempel arbeta med resurser för produkter som ännu inte är aktiva. I så fall kan marknadsföringsteamet få tillgång till smarta beskärningsbilder och dynamiska renderingar som synkroniseras med Dynamic Media så att de kan skapa marknadsföringsmaterial, utan att behöva publicera dessa resurser på Dynamic Media för global leverans.

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Om du kopierar* resurser till och från mappar rensas publiceringstillståndet för dessa resurser. Men när du *flyttar* resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]** bevaras publiceringsläget för resurserna.

Om du senare bestämmer dig för att ändra **[!UICONTROL Selective Publish]** inställningarna i en mapp påverkar ändringarna bara nya resurser som du överför till den mappen från den punkten och framåt. Publiceringsläget för befintliga resurser i mappen ändras inte förrän du ändrar dem manuellt från antingen **[!UICONTROL Quick Publish]** eller **[!UICONTROL Manage Publication]** dialogrutan.

Alternativet på mappnivå **[!UICONTROL Dynamic Media Publish mode]** är som standard det värde som finns i **[!UICONTROL Publish Assets]** inställningen i **[!UICONTROL Dynamic Media Configuration.]** följande steg i det här avsnittet, men visa hur du manuellt ändrar det här standardvärdet på mappnivå (vilket beskrivs i följande steg) för att åsidosätta **[!UICONTROL Dynamic Media Configuration]** värdet.

Oavsett om du förlitar dig på det **[!UICONTROL Publish Assets]** värde som anges i **[!UICONTROL Dynamic Media Configuration]**, eller det **[!UICONTROL Dynamic Media Publish mode]** värde som anges i egenskaper på mappnivå, kan du fortfarande välja **[!UICONTROL Immediately]**, **[!UICONTROL Upon Activation]** eller till **[!UICONTROL Selective Publish.]** exempel ange **[!UICONTROL Publish Assets]** värdet i dina foton **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL Upon Activation]**, men ange **[!UICONTROL Dynamic Media Publish]** **[!UICONTROL Selective Publish]** lägesvärdet på mappnivå till¥, vice versa och så vidare.

När du har konfigurerat selektiv publicering i en mapp kan du göra något av följande:

* [Publicera valfritt material till Dynamic Media eller AEM med Manage Publication.](#selective-publish-manage-publication)
* [Avpublicera utvalda resurser från Dynamic Media eller AEM med Hantera publikation.](#selective-unpublish-manage-publication)
* [Publicera material till Dynamic Media eller AEM med Snabbpublicering.](#quick-publish-aem-dm)
* [Publicera eller avpublicera resurser selektivt via sökresultat.](#selective-publish-unpublish-search-results)

**Konfigurera selektiv publicering på mappnivå i Dynamic Media**

1. I AEM trycker du på AEM logotyp för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (alldeles ovanför verktygsikonen) till vänster och tryck sedan på **[!UICONTROL Assets > Files.]**
1. Gör något av följande:
   * Redigera egenskaperna för en befintlig mapp - I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** navigera till en mapp vars egenskaper du vill redigera. Markera mappen och tryck sedan på **[!UICONTROL Properties.]**
   * Redigera egenskaperna för en ny mapp - I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** i det övre högra hörnet av sidan trycker du på **[!UICONTROL Create > Folder.]** I **[!UICONTROL Create Folder]** dialogrutan, anger en rubrik (krävs) för mappen och trycker sedan på **[!UICONTROL Create.]** Markera mappen och trycker sedan på i verktygsfältet **[!UICONTROL Properties.]**

1. In the **[!UICONTROL Sync mode]** drop-down list, select one of the following:

   | Synkroniseringsläge | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Inherited]** | Det finns inget explicit synkroniseringsvärde för mappen; I stället ärver mappen synkroniseringsvärdet från en av de överordnade mapparna eller det standardläge som är angivet i **[!UICONTROL Dynamic Media Configuration.]** Detaljerad status för **[!UICONTROL Inherited]** visning som ett verktygstips. |
   | **[!UICONTROL Sync everything in this folder sub-tree to dynamicmedia]** | För att publicering till Dynamic Media ska lyckas måste materialet synkroniseras till Dynamic Media. Om du väljer det här alternativet inkluderas alla resurser i det här underträdet för synkronisering till dynamiska media. De mappspecifika inställningarna åsidosätter standardinställningen i **[!UICONTROL Dynamic Media Configuration.]** |
   | **[!UICONTROL Exclude everything in this folder sub-tree from dynamicmedia sync]** | Uteslut alla resurser i det här underträdet från synkronisering till Dynamic Media. |

   ![Selektiv publicering på mappnivå](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Välj ett alternativ i den **[!UICONTROL Dynamic Media Publish mode]** nedrullningsbara listan. Observera att det **[!UICONTROL Dynamic Media Publish mode]** här alternativet alltid är standardvärdet som anges i **[!UICONTROL Dynamic Media Configuration.]** Du kan dock manuellt åsidosätta det här **[!UICONTROL Dynamic Media Configuration]** standardvärdet genom att använda något av följande alternativ.

   >[!IMPORTANT]
   >
   >Observera att alla uppdateringar som du gör i en resurs som *redan* är publicerade, oavsett vilket läge för publicering av dynamiska media du väljer, publiceras omedelbart utan några ytterligare användaråtgärder.

   | Alternativet Publicera dynamiska media | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Immediately]** | När resurser överförs till den här mappen, importeras resurserna till AEM och URL/Embed anges omedelbart. Det här alternativet är knutet till AEM publicering och det behövs ingen användaråtgärd för att publicera resurser.<br>Det här alternativet är *inte* tillgängligt om du valde **[!UICONTROL Exclude everything in this folder sub-tree from dynamicmedia sync]** i **[!UICONTROL Sync mode]** föregående steg. |
   | **[!UICONTROL Upon Activation]** | När resurser överförs till den här mappen måste du uttryckligen publicera resursen innan en URL/Embed-länk anges. Det här alternativet är endast kopplat AEM publicering.<br>Det här alternativet är *inte* tillgängligt om du valde **[!UICONTROL Exclude everything in this folder sub-tree from dynamicmedia sync]** i **[!UICONTROL Sync mode]** föregående steg. |
   | **[!UICONTROL Selective Publish]** | Resurserna publiceras antingen AEM eller till Dynamic Media för att distribueras offentligt. Båda publiceringsmetoderna utesluter varandra.  Det innebär att du kan publicera resurser på DMS7 så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar. Eller så kan du publicera resurser exklusivt till AEM för säker förhandsgranskning. samma resurser *inte* publiceras till DMS7 för att levereras offentligt. Det här alternativet är inte tillgängligt om du valde **[!UICONTROL Exclude everything in this folder sub-tree from dynamicmedia sync]** i **[!UICONTROL Sync mode]** föregående steg. |

1. I det övre högra hörnet av sidan trycker du på **[!UICONTROL Save & Close]** och sedan på **[!UICONTROL OK]** för att återgå till AEM Assets.

## Publicera valfritt material till Dynamic Media eller AEM som en Cloud Service med Hantera publikation{#selective-publish-manage-publication}

Innan du kan använda **[!UICONTROL Manage Publication]** för att selektivt publicera resurser på dynamiska media eller för att AEM måste du antingen ange **[!UICONTROL Publish Assets]** alternativet i **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL Selective Publish]** eller konfigurera selektiv publicering på mappnivå.

Se [Skapa en dynamisk mediekonfiguration](#configuring-dynamic-media-cloud-services) eller [Konfigurera selektiv publicering på mappnivå i Dynamic Media](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Om du kopierar* resurser till och från mappar rensas publiceringstillståndet för dessa resurser. Men när du *flyttar* resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]** bevaras publiceringsläget för resurserna.

**Publicera selektivt material till Dynamic Media eller AEM som en Cloud Service med Hantera publikation**

1. I AEM trycker du på AEM logotyp för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (alldeles ovanför verktygsikonen) till vänster och tryck sedan på **[!UICONTROL Assets > Files.]**
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** gör du något av följande:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och tryck sedan på **[!UICONTROL Manage Publication.]** You may find it help **[!UICONTROL List View]** so you can easily check the publish status of a particular folder.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. Tryck på **[!UICONTROL Manage Publication.]** Du kan ha nytta av det i verktygsfältet så **[!UICONTROL List View]** att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >Om **[!UICONTROL Manage Publication]** inte visas i verktygsfältet trycker du i stället på ellipsknappen och väljer sedan **[!UICONTROL Manage Publication]** i listrutan.

1. På **[!UICONTROL Manage Publication - Options]** sidan, under **[!UICONTROL Action]**, väljer du vilken typ av aktivering du vill använda.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Publish]** (till AEM) | Välj det här alternativet om du vill publicera resurser AEM för säker förhandsvisning. |
   | **[!UICONTROL Publish to Dynamic Media]** | Välj det här alternativet om du vill publicera resurser på dynamiska medier för att distribueras i den offentliga domänen eller så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar.<br>Det här alternativet är bara tillgängligt om **[!UICONTROL Dynamic Media Publish mode]** är inställt **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Under **[!UICONTROL Schedule]** anger du tidsinställningen för publiceringen.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj att publicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill publicera resurserna ett visst datum och en viss tid. |

1. Tryck på i det övre högra hörnet på **[!UICONTROL Manage Publication]** sidan **[!UICONTROL Next.]**
1. Gör något av följande på **[!UICONTROL Manage Publication - Scope]** sidan:
   * Om det behövs väljer du en eller flera resurser som du vill ta bort från publiceringen.
   * In the upper-right corner of the **[!UICONTROL Manage Publication - Scope]** page, tap **[!UICONTROL Publish]** or **[!UICONTROL Publish to Dynamic Media.]**
1. Tryck på **[!UICONTROL OK.]**

### Avpublicera utvalda resurser från Dynamic Media eller AEM med Hantera publikation {#selective-unpublish-manage-publication}

1. I AEM trycker du på AEM logotyp för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (alldeles ovanför verktygsikonen) till vänster och tryck sedan på **[!UICONTROL Assets > Files.]**
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** gör du något av följande:
   * Navigera till en mapp vars resurser du vill avpublicera. Markera mappen och tryck sedan på **[!UICONTROL Manage Publication.]** You may find it help **[!UICONTROL List View]** so you can easily check the publish status of a particular folder.
   * Navigera till en mapp vars resurser du vill avpublicera. Öppna mappen och välj sedan en eller flera resurser. Tryck på **[!UICONTROL Manage Publication.]** Du kan ha nytta av det i verktygsfältet så **[!UICONTROL List View]** att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >Om **[!UICONTROL Manage Publication]** inte visas i verktygsfältet trycker du i stället på ellipsknappen och väljer sedan **[!UICONTROL Manage Publication]** i listrutan.

1. På **[!UICONTROL Manage Publication - Options]** sidan, under **[!UICONTROL Action]**, väljer du vilken typ av avaktivering du vill ha.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Unpublish]** (från AEM) | Välj det här alternativet om du vill avpublicera resurser från AEM. |
   | **[!UICONTROL Unpublish from Dynamic Media]** | Välj det här alternativet om du vill avpublicera resurser från Dynamic Media.<br>Det här alternativet är bara tillgängligt om **[!UICONTROL Dynamic Media Publish mode]** är inställt **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Under **[!UICONTROL Schedule]** anger du tidpunkten för avaktiveringen.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj att avpublicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill avpublicera resurserna ett visst datum och en viss tid. |

1. Tryck på i det övre högra hörnet på **[!UICONTROL Manage Publication]** sidan **[!UICONTROL Next.]**
1. Gör något av följande på **[!UICONTROL Manage Publication - Scope]** sidan:
   * Markera en eller flera resurser som du vill ta bort från avpubliceringen.
   * In the upper-right corner of the **[!UICONTROL Manage Publication - Scope]** page, tap **[!UICONTROL Unpublish]** or **[!UICONTROL Unpublish from Dynamic Media.]**
1. Tryck på **[!UICONTROL OK.]**

## Publicera material till Dynamic Media eller AEM med Snabbpublicering {#quick-publish-aem-dm}

Du kan använda **[!UICONTROL Quick Publish]** för enkel aktivering av resurser. **[!UICONTROL Quick Publish]** publicerar de markerade resurserna omedelbart utan ytterligare användarinteraktion. Därför publiceras alla icke-publicerade referenser automatiskt.

>[!NOTE]
>
>Om du vill använda **[!UICONTROL Quick Publish]** för att publicera resurser till Dynamic Media eller AEM måste du se till att **[!UICONTROL Selective Publish]** det är aktiverat i din **[!UICONTROL Dynamic Media Configuration]** eller i mappegenskaperna för den valda mappen.

**Publicera material till Dynamic Media eller AEM med Snabbpublicering**

1. I AEM trycker du på AEM logotyp för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (precis ovanför verktygsikonen) till vänster på sidan och tryck sedan på sidans högra sida **[!UICONTROL Assets > Files.]**
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** gör du något av följande:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och tryck sedan på **[!UICONTROL Quick Publish.]** You may find it help **[!UICONTROL List View]** so you can easily check the publish status of a particular folder.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. Tryck på **[!UICONTROL Quick Publish.]** Du kan ha nytta av det i verktygsfältet så **[!UICONTROL List View]** att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >Om **[!UICONTROL Quick Publish]** inte visas i verktygsfältet trycker du i stället på ellipsknappen och väljer sedan **[!UICONTROL Quick Publish]** i listrutan.

      ![Snabbpublicering på mappnivå till dynamiska media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Välj något av följande alternativ i **[!UICONTROL Quick Publish]** menylistan.

   | Snabbpublicering, alternativ | Vad det gör |
   | --- | --- | 
   | Publicera till AEM | Publicerar de markerade resurserna direkt till AEM. |
   | Publicera på varumärkesportal | Publicerar de markerade resurserna direkt till **[!UICONTROL Brand Portal.]**<br>Det här alternativet är endast tillgängligt om din AEM Assets-instans **[!UICONTROL Brand Portal]**redan har konfigurerats. |
   | Publicera till Dynamic Media | Publicerar de valda resurserna direkt till Dynamic Media.<br>En resurs måste redan vara synkroniserad till Dynamic Media. Om det behövs kontrollerar du att egenskaperna **[!UICONTROL Sync mode]** i en mapp redan är inställda på **[!UICONTROL Sync everything in this folder sub-tree to dynamicmedia.]** |

1. Tryck **[!UICONTROL OK,]** och tryck sedan **[!UICONTROL Close,]**

## Publicera eller avpublicera resurser selektivt via sökresultat {#selective-publish-unpublish-search-results}

Sökresultaten kan visa resurser från olika resursmappar med olika publiceringsinställningar för Dynamic Media. Om du har valt en eller flera resurser från sökresultaten och resurserna har olika inställningar för publiceringsläget för dynamiska media, kan du aktivera **[!UICONTROL Manage Publication]** från verktygsfältet för att publicera eller avpublicera.

Se även [Söka efter resurser i AEM.](/help/assets/search-assets.md)

**Publicera eller avpublicera resurser selektivt via sökresultat**

1. I AEM, i det övre vänstra hörnet av sidan, trycker du på AEM logotyp för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (precis ovanför verktygsikonen) till vänster på sidan och tryck sedan på **[!UICONTROL Assets > Files.]**
1. I verktygsfältet, i det övre högra hörnet på sidan, trycker du på ikonen Sök (förstoringsglas).
1. Ange ett nyckelord i **[!UICONTROL Type to search]** textfältet och tryck sedan på **[!UICONTROL Enter.]**
1. Tryck på **[!UICONTROL List View]** ikonen i det övre högra hörnet på sidan.
1. Near the upper-left corner of the page, tap the **[!UICONTROL Filters]** icon.

   ![Listvy och filter i sökresultat](/help/assets/assets-dm/select-publish-search-result.png)

1. Expandera **[!UICONTROL Status]** och expandera sedan sökpredikatet i den vänstra panelen **[!UICONTROL Dynamic Media]** .
1. Använd kryssrutorna **[!UICONTROL Published]** och **[!UICONTROL Unpublished]** för att förfina sökresultaten ytterligare baserat på det publicerade läget för Dynamic Media-resurser.
Du kan också använda de här kryssrutorna tillsammans med **[!UICONTROL Publish]** sökpredikatet för att förfina sökresultaten för **[!UICONTROL Published]** - och **[!UICONTROL Unpublished]** AEM resurser.
1. Gör något av följande:
   * Markera en eller flera resurser som du vill publicera eller avpublicera.
   * Near the upper-right corner of the **[!UICONTROL Search Results]** page, tap **[!UICONTROL Select All.]**
1. Tryck på **[!UICONTROL Manage Publication.]** Du kan behöva trycka på ellipsikonen i verktygsfältet för att se **[!UICONTROL Manage Publication.]**
1. Välj önskad åtgärd på **[!UICONTROL Manage Publication - Options]** sidan.

   | Markerad åtgärd | Inställningen Publicera resurser i Dynamic Media Configuration | Resurserna är |
   | --- | --- | --- |
   | Publicera | Omedelbart eller vid aktivering | Publicerat till AEM och Dynamic Media. |
   | Publicera | Selektiv publicering | Endast publicerad till AEM. |
   | Avpublicera | Omedelbart eller vid aktivering | Opublicerat från AEM och Dynamic Media. |
   | Avpublicera | Selektiv publicering | Endast opublicerad från AEM. |
   | Publicera till Dynamic Media | Omedelbart eller vid aktivering | Publiceras inte till AEM, Dynamic Media eller både och. |
   | Publicera till Dynamic Media | Selektiv publicering | Publiceras endast till Dynamic Media. |
   | Avpublicera från Dynamic Media | Omedelbart eller vid aktivering | Inte opublicerat från AEM, Dynamic Media eller båda. |
   | Avpublicera från Dynamic Media | Selektiv publicering | Endast opublicerade från Dynamic Media. |

1. Under **[!UICONTROL Schedule]** anger du tidpunkten för avaktiveringen.

   | Valt schema | Vad händer |
   | --- | --- |
   | Nu | Den valda åtgärden utförs omedelbart. |
   | Senare | Den valda åtgärden körs på det valda datumet och den valda tiden. |

1. Tryck på i det övre högra hörnet på **[!UICONTROL Manage Publication - Options]** sidan **[!UICONTROL Next.]**
1. (Valfritt) På **[!UICONTROL Manage Publication - Scope]** sidan granskar du **[!UICONTROL Publish Target]** kolumnen i tabellen för de valda resurserna.

   | Inställningen Publicera resurser i Dynamic Media Configuration | Markerad åtgärd | Publicera mål |
   | --- | --- | --- |
   | Omedelbart eller <br>vid aktivering | Publicera | AEM och Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Publicera till Dynamic Media | Inget |
   | Selektiv publicering | Publicera | AEM |
   | Selektiv publicering | Publicera till Dynamic Media | Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Avpublicera | AEM och Dynamic Media |
   | Omedelbart eller <br>vid aktivering | Avpublicera från Dynamic Media | Inget |
   | Selektiv publicering | Avpublicera | AEM |
   | Selektiv publicering | Avpublicera från Dynamic Media | Dynamic Media |

1. Gör något av följande på **[!UICONTROL Manage Publication - Scope]** sidan:
   * Markera en eller flera resurser som du vill ta bort från publicering eller avpublicering.
   * In the upper-right corner of the **[!UICONTROL Manage Publication - Scope]** page, tap **[!UICONTROL Publish]** or **[!UICONTROL Unpublish]** to begin the action.
1. Tryck på **[!UICONTROL OK.]**

## Kontrollera publiceringsstatus för en resurs {#check-publish-status-of-asset}

Du kan använda **[!UICONTROL Timeline]** med **[!UICONTROL Card view]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** i AEM för att snabbt kontrollera publiceringsläget för en resurs.

**Kontrollera publiceringsstatus för en resurs**

1. I AEM, i det övre vänstra hörnet av sidan, trycker du på AEM logotyp för att komma åt den globala navigeringskonsolen. Tryck på navigeringsikonen (precis ovanför verktygsikonen) till vänster på sidan och tryck sedan på **[!UICONTROL Assets > Files.]**
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]** eller **[!UICONTROL List View]** (skärmbilden nedan visar **[!UICONTROL List View]**) öppnar du en mapp som innehåller resurser som du har publicerat eller opublicerat.
1. Markera en resurs så att den visas med en bock. Se skärmbilden nedan.
1. I den nedrullningsbara menyn i det övre vänstra hörnet av sidan väljer du **[!UICONTROL Timeline.]** Området i den vänstra **[!UICONTROL Status]** panelen visar publiceringsläget för den valda resursen.
När du använder **[!UICONTROL List View]** visas ytterligare en kolumn för **[!UICONTROL Dynamic Media]** publiceringsläget.
   * En mapp som är konfigurerad att synkronisera till Dynamic Media visar **[!UICONTROL Dynamic Media]** kolumnen som standard.
   * En mapp som *inte* är konfigurerad att synkronisera till dynamiska media kommer inte att visa kolumnen Dynamiska media.
      ![Listvy och tidslinje](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Felsöka selektiv publicering {#selective-publish-troubleshoot}

En resurs som inte synkroniseras till Dynamic Media men som har en publiceringsåtgärd för Dynamic Media aktiverad resulterar i följande felmeddelande och lösning:

![Selektivt publiceringsfel](/help/assets/assets-dm/selective-publish-error.png)

