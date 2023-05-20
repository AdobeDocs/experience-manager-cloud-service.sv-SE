---
title: Arbeta med selektiv publicering i Dynamic Media
description: Lär dig hur du arbetar med selektiv publicering i Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '2544'
ht-degree: 0%

---

# Konfigurera selektiv publicering på mappnivå i Dynamic Media {#selective-publish-configure-folder}

Du kan välja att publicera eller avpublicera resurser till eller från Adobe Experience Manager eller Dynamic Media. Du kan göra det på mappnivå med antingen **[!UICONTROL Manage Publication]** eller **[!UICONTROL Quick Publish]**. Den här publiceringsmetoden är användbar eftersom den inte är beroende av **[!UICONTROL Dynamic Media Configuration]** vars inställningar är globala för alla mappar i din Dynamic Media-instans.

Med selektiv publicering kan du till exempel arbeta med resurser för produkter som ännu inte är aktiva. I så fall kan marknadsföringsteamet få tillgång till smarta beskärningsbilder och dynamiska återgivningar som synkroniseras med Dynamic Media. De kan skapa marknadsföringsmaterial utan att behöva publicera materialet på Dynamic Media för global leverans.

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Kopierar* resurser till och från mappar rensar publiceringstillståndet för dessa resurser. När du *move* resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]**, underhålls publiceringsstatusen för dessa tillgångar.

Om du senare bestämmer dig för att ändra **[!UICONTROL Selective Publish]** inställningarna i en mapp påverkar dessa ändringar endast nya resurser som du överför till den mappen från den punkten och framåt. Publiceringsläget för befintliga resurser i mappen ändras inte förrän du ändrar dem manuellt från **[!UICONTROL Quick Publish]** eller **[!UICONTROL Manage Publication]** -dialogrutan.

Mappnivån **[!UICONTROL Dynamic Media Publish mode]** som standard är det värde som finns i **[!UICONTROL Publish Assets]** i **[!UICONTROL Dynamic Media Configuration]**. Följande steg i det här avsnittet visar dock hur du manuellt ändrar det här standardvärdet på mappnivå (som beskrivs i följande steg) för att åsidosätta **[!UICONTROL Dynamic Media Configuration]** värde.

Oavsett om du förlitar dig på:

* The **[!UICONTROL Publish Assets]** värde angivet i **[!UICONTROL Dynamic Media Configuration]**
* Eller **[!UICONTROL Dynamic Media Publish mode]** värde angivet i egenskaper på mappnivå

Du kan fortfarande välja **[!UICONTROL Immediately]**, **[!UICONTROL Upon Activation]**, eller **[!UICONTROL Selective Publish]**. Du kan till exempel ange **[!UICONTROL Publish Assets]** på **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL On Activation]**. Och du kan ange **[!UICONTROL Dynamic Media Publish]** lägesvärde på mappnivå till **[!UICONTROL Selective Publish]**, omvänt och så vidare.

När du har konfigurerat selektiv publicering i en mapp kan du göra något av följande:

* [Publicera valfritt material till Dynamic Media eller Experience Manager med Hantera publikation](#selective-publish-manage-publication).
* [Avpublicera valfritt material från Dynamic Media eller Experience Manager med Hantera publikation](#selective-unpublish-manage-publication).
* [Publicera material på Dynamic Media eller Experience Manager med Snabbpublicering](#quick-publish-aem-dm).
* [Publicera eller avpublicera resurser selektivt via sökresultat](#selective-publish-unpublish-search-results).

**Så här konfigurerar du selektiv publicering på mappnivå i Dynamic Media:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Gör något av följande:
   * Redigera egenskaperna för en befintlig mapp - I **[!UICONTROL Card View]**, **[!UICONTROL Column View]**, eller **[!UICONTROL List View]** navigera till en mapp vars egenskaper du vill redigera. Markera mappen och välj sedan **[!UICONTROL Properties]**.
   * Redigera egenskaperna för en ny mapp - i **[!UICONTROL Card View]**, **[!UICONTROL Column View]**, eller **[!UICONTROL List View]**, nära sidans övre högra hörn, gå till **[!UICONTROL Create]** > **[!UICONTROL Folder]**. I **[!UICONTROL Create Folder]** anger du en rubrik (obligatoriskt) för mappen och väljer **[!UICONTROL Create]**. Markera mappen och välj sedan **[!UICONTROL Properties]**.

1. I **[!UICONTROL Sync mode]** väljer du något av följande:

   | Synkroniseringsläge | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Inherited]** | Det finns inget explicit synkroniseringsvärde för mappen; i stället ärver mappen synkroniseringsvärdet från någon av dess överordnade mappar eller det standardläge som angetts i **[!UICONTROL Dynamic Media Configuration]**. Detaljerad status för **[!UICONTROL Inherited]** visas med ett verktygstips. |
   | **[!UICONTROL Sync everything in this folder subtree to Dynamic Media]** | För att publiceringen till Dynamic Media ska lyckas måste materialet synkroniseras med Dynamic Media. Om du väljer det här alternativet inkluderas alla resurser i det här underträdet för synkronisering till Dynamic Media. De mappspecifika inställningarna åsidosätter standardinställningen i **[!UICONTROL Dynamic Media Configuration]**. |
   | **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** | Uteslut alla resurser i det här underträdet från synkronisering till Dynamic Media. |

   ![Selektiv publicering på mappnivå](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. I **[!UICONTROL Dynamic Media Publish mode]** väljer du ett alternativ. The **[!UICONTROL Dynamic Media Publish mode]** som standard är det värde som anges i **[!UICONTROL Dynamic Media Configuration]**. Du kan dock manuellt åsidosätta den här standardinställningen **[!UICONTROL Dynamic Media Configuration]** genom att använda något av följande alternativ.

   >[!IMPORTANT]
   >
   >Oavsett vilket alternativ för publiceringsläget i Dynamic Media du väljer kan du göra senare uppdateringar av en mediefil som *redan* publiceras publiceras dessa uppdateringar omedelbart utan några ytterligare användaråtgärder.

   | Publiceringsläge för Dynamic Media | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Immediately]** | När resurser överförs till den här mappen, importeras resurserna till Experience Manager och URL:en/inbäddningen anges omedelbart. Det här alternativet är knutet till publicering i Experience Manager och det behövs inga användaråtgärder för att publicera resurser.<br>Det här alternativet är *not* tillgänglig om du har valt **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** in **[!UICONTROL Sync mode]** i föregående steg. |
   | **[!UICONTROL Upon Activation]** | När resurser överförs till den här mappen måste du uttryckligen publicera resursen innan en URL/Embed-länk anges. Det här alternativet är endast knutet till Experience Manager-publicering.<br>Det här alternativet är *not* tillgänglig om du har valt **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** in **[!UICONTROL Sync mode]** i föregående steg. |
   | **[!UICONTROL Selective Publish]** | Resurser publiceras till Experience Manager eller till Dynamic Media för att distribueras offentligt. Båda publiceringsmetoderna utesluter varandra. Det innebär att du kan publicera resurser på DMS7 så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar. Eller så kan du publicera resurser exklusivt på Experience Manager för säker förhandsgranskning. samma tillgångar *not* publiceras på DMS7 för att levereras offentligt. Det här alternativet är inte tillgängligt om du har valt **[!UICONTROL Exclude everything in this folder subtree from Dynamic Media sync]** in **[!UICONTROL Sync mode]** i föregående steg. |

1. I det övre högra hörnet på sidan väljer du **[!UICONTROL Save & Close]** väljer **[!UICONTROL OK]** för att återvända till Experience Manager Assets.

## Publicera utvalda resurser på Dynamic Media eller Experience Manager as a Cloud Service med hjälp av Hantera publikation{#selective-publish-manage-publication}

Innan du kan använda **[!UICONTROL Manage Publication]** Om du vill publicera mediefiler till Dynamic Media eller Experience Manager måste du göra något av följande:

* Ange **[!UICONTROL Publish Assets]** alternativ i **[!UICONTROL Dynamic Media Configuration]** till **[!UICONTROL Selective Publish]**.
* Eller konfigurerad selektiv publicering på mappnivå.

Se [Skapa en Dynamic Media-konfiguration](#configuring-dynamic-media-cloud-services) eller [Konfigurera selektiv publicering på mappnivå i Dynamic Media](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Kopierar* resurser till och från mappar rensar publiceringstillståndet för dessa resurser. När du *move* resurser till och från mappar vars mappegenskap är inställd på **[!UICONTROL Selective Publish]**, underhålls publiceringsstatusen för dessa tillgångar.

**Så här publicerar du material selektivt på Dynamic Media eller Experience Manager as a Cloud Service med hjälp av Hantera publikation:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]**, eller **[!UICONTROL List View]** gör du något av följande:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och välj sedan **[!UICONTROL Manage Publication]**. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. I verktygsfältet väljer du **[!UICONTROL Manage Publication]**. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >If **[!UICONTROL Manage Publication]** visas inte i verktygsfältet. Välj i stället ellipsknappen och markera sedan **[!UICONTROL Manage Publication]** på listmenyn.

1. I **[!UICONTROL Manage Publication - Options]** sida, under **[!UICONTROL Action]** väljer du den typ av aktivering du vill använda.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Publish]** (till Experience Manager) | Markera det här alternativet om du vill publicera resurser på Experience Manager för säker förhandsvisning. |
   | **[!UICONTROL Publish to Dynamic Media]** | Välj det här alternativet om du vill publicera resurser på Dynamic Media för att distribuera dem till den offentliga domänen eller så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar.<br>Det här alternativet är bara tillgängligt om **[!UICONTROL Dynamic Media Publish mode]** är inställd på **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Under **[!UICONTROL Schedule]**, anger publiceringens tidsinställning.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj att publicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill publicera resurserna ett visst datum och en viss tid. |

1. I det övre högra hörnet av **[!UICONTROL Manage Publication]** sida, markera **[!UICONTROL Next]**.
1. I **[!UICONTROL Manage Publication - Scope]** gör du något av följande på sidan:
   * Om det behövs väljer du en eller flera resurser som du vill ta bort från publiceringen.
   * I det övre högra hörnet av **[!UICONTROL Manage Publication - Scope]** sida, markera **[!UICONTROL Publish]** eller **[!UICONTROL Publish to Dynamic Media]**.
1. Välj **[!UICONTROL OK]**.

### Avpublicera valfritt material från Dynamic Media eller Experience Manager med Hantera publikation {#selective-unpublish-manage-publication}

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]**, eller **[!UICONTROL List View]** gör du något av följande:
   * Navigera till en mapp vars resurser du vill avpublicera. Markera mappen och välj sedan **[!UICONTROL Manage Publication]**. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill avpublicera. Öppna mappen och välj sedan en eller flera resurser. I verktygsfältet väljer du **[!UICONTROL Manage Publication]**. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >If **[!UICONTROL Manage Publication]** visas inte i verktygsfältet. Välj i stället ellipsknappen och markera sedan **[!UICONTROL Manage Publication]** på listmenyn.

1. I **[!UICONTROL Manage Publication - Options]** sida, under **[!UICONTROL Action]** väljer du vilken typ av avaktivering du vill ha.

   | Åtgärd | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Unpublish]** (från Experience Manager) | Om du vill avpublicera resurser från Experience Manager väljer du det här alternativet. |
   | **[!UICONTROL Unpublish from Dynamic Media]** | Om du vill avpublicera resurser från Dynamic Media väljer du det här alternativet.<br>Det här alternativet är bara tillgängligt om **[!UICONTROL Dynamic Media Publish mode]** är inställd på **[!UICONTROL Selective Publish]** i mappens egenskaper. |

1. Under **[!UICONTROL Schedule]**, ange tidpunkten för avaktiveringen.

   | Schema | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Now]** | Välj att avpublicera resurserna direkt. |
   | **[!UICONTROL Later]** | Välj det här alternativet om du vill avpublicera resurserna ett visst datum och en viss tid. |

1. I det övre högra hörnet av **[!UICONTROL Manage Publication]** sida, markera **[!UICONTROL Next]**.
1. I **[!UICONTROL Manage Publication - Scope]** gör du något av följande på sidan:
   * Markera en eller flera resurser som du vill ta bort från avpubliceringen.
   * I det övre högra hörnet av **[!UICONTROL Manage Publication - Scope]** sida, markera **[!UICONTROL Unpublish]** eller **[!UICONTROL Unpublish from Dynamic Media]**.
1. Välj **[!UICONTROL OK]**.

## Publicera material på Dynamic Media eller Experience Manager med Snabbpublicering {#quick-publish-aem-dm}

Du kan använda **[!UICONTROL Quick Publish]** för enkel tillgångsaktivering. **[!UICONTROL Quick Publish]** publicerar de markerade resurserna omedelbart utan ytterligare användarinteraktion. Alla icke-publicerade referenser publiceras också automatiskt.

>[!NOTE]
>
>Används **[!UICONTROL Quick Publish]** om du vill publicera mediefiler på Dynamic Media eller Experience Manager måste du vara säker på att **[!UICONTROL Selective Publish]** är aktiverat antingen i **[!UICONTROL Dynamic Media Configuration]** eller i mappegenskaperna för den markerade mappen.

**Så här publicerar du material till Dynamic Media eller Experience Manager med Snabbpublicering:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster på sidan väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och sedan går till höger på sidan **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]**, eller **[!UICONTROL List View]** gör du något av följande:
   * Navigera till en mapp vars resurser du vill publicera. Markera mappen och välj sedan **[!UICONTROL Quick Publish]**. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss mapp.
   * Navigera till en mapp vars resurser du vill publicera. Öppna mappen och välj sedan en eller flera resurser. I verktygsfältet väljer du **[!UICONTROL Quick Publish]**. Använd **[!UICONTROL List View]** så att du enklare kan kontrollera publiceringsstatusen för en viss resurs.

      >[!NOTE]
      >
      >If **[!UICONTROL Quick Publish]** visas inte i verktygsfältet. Välj i stället ellipsknappen och markera sedan **[!UICONTROL Quick Publish]** på listmenyn.

      ![Snabbpublicering på mappnivå till Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Välj något av följande alternativ från **[!UICONTROL Quick Publish]** menylista.

   | Snabbpublicering, alternativ | Vad det gör |
   | --- | --- | 
   | Publicera i Experience Manager | Publicerar de markerade resurserna direkt till Experience Manager. |
   | Publicera till Brand Portal | Publicerar de markerade resurserna direkt till **[!UICONTROL Brand Portal]**.<br>Det här alternativet är bara tillgängligt om din Experience Manager Assets-instans har **[!UICONTROL Brand Portal]** redan konfigurerad. |
   | Publicera till Dynamic Media | Publicerar de markerade resurserna direkt till Dynamic Media.<br>En resurs måste redan synkroniseras till Dynamic Media. Om det behövs, se till att **[!UICONTROL Sync mode]** i en mapps egenskaper är redan inställda på **[!UICONTROL Sync everything in this folder subtree to Dynamic Media]**. |

1. Välj **[!UICONTROL OK]** väljer **[!UICONTROL Close]**.

## Publicera eller avpublicera resurser selektivt via sökresultat {#selective-publish-unpublish-search-results}

Sökresultaten kan visa resurser från olika resursmappar med olika publiceringsinställningar för Dynamic Media. Där du har valt en eller flera resurser från sökresultaten och resurserna har olika publiceringslägesinställningar för Dynamic Media kan du aktivera **[!UICONTROL Manage Publication]** från verktygsfältet för att publicera eller avpublicera.

Se även [Söka efter resurser i Experience Manager](/help/assets/search-assets.md).

**Så här publicerar eller avpublicerar du resurser selektivt via sökresultat:**

1. I Experience Manager, i det övre vänstra hörnet av sidan, väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster på sidan väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. I verktygsfältet, i det övre högra hörnet på sidan, väljer du ikonen Sök (förstoringsglas).
1. I **[!UICONTROL Type to search]** textfält, ange ett nyckelord och tryck sedan på **[!UICONTROL Enter]**.
1. I det övre högra hörnet av sidan väljer du **[!UICONTROL List View]** ikon.
1. I närheten av det övre vänstra hörnet av sidan väljer du **[!UICONTROL Filters]** ikon.

   ![Listvy och filter i sökresultat](/help/assets/assets-dm/select-publish-search-result.png)

1. Expandera på den vänstra panelen **[!UICONTROL Status]** och sedan expandera **[!UICONTROL Dynamic Media]** sökpredikat.
1. Använd **[!UICONTROL Published]** och **[!UICONTROL Unpublished]** om du vill förfina sökresultaten ytterligare baserat på det publicerade läget för Dynamic Media-resurser.
Du kan också använda de här kryssrutorna med **[!UICONTROL Publish]** sökpredikat för att förfina sökresultaten för **[!UICONTROL Published]** och **[!UICONTROL Unpublished]** Experience Manager resurser.
1. Gör något av följande:
   * Markera en eller flera resurser som du vill publicera eller avpublicera.
   * Nära det övre högra hörnet av **[!UICONTROL Search Results]** sida, markera **[!UICONTROL Select All]**.
1. I verktygsfältet väljer du **[!UICONTROL Manage Publication]**. Om det behövs väljer du ellipsikonen i verktygsfältet för att se **[!UICONTROL Manage Publication]**.
1. På **[!UICONTROL Manage Publication - Options]** väljer du önskad åtgärd.

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

1. Under **[!UICONTROL Schedule]**, ange tidpunkten för avaktiveringen.

   | Valt schema | Vad händer |
   | --- | --- |
   | Nu | Den valda åtgärden utförs omedelbart. |
   | Senare | Den valda åtgärden körs på det valda datumet och den valda tiden. |

1. I det övre högra hörnet av **[!UICONTROL Manage Publication - Options]** sida, markera **[!UICONTROL Next]**.
1. (Valfritt) I dialogrutan **[!UICONTROL Manage Publication - Scope]** sida, granska **[!UICONTROL Publish Target]** i tabellen för de valda resurserna.

   | Inställningen Publicera resurser i Dynamic Media Configuration | Markerad åtgärd | Publicera mål |
   | --- | --- | --- |
   | Omedelbart eller <br>Vid aktivering | Publicera | Experience Manager och Dynamic Media |
   | Omedelbart eller <br>Vid aktivering | Publicera till Dynamic Media | Ingen |
   | Selektiv publicering | Publicera | Experience Manager |
   | Selektiv publicering | Publicera till Dynamic Media | Dynamic Media |
   | Omedelbart eller <br>Vid aktivering | Avpublicera | Experience Manager och Dynamic Media |
   | Omedelbart eller <br>Vid aktivering | Avpublicera från Dynamic Media | Ingen |
   | Selektiv publicering | Avpublicera | Experience Manager |
   | Selektiv publicering | Avpublicera från Dynamic Media | Dynamic Media |

1. I **[!UICONTROL Manage Publication - Scope]** gör du något av följande på sidan:
   * Markera en eller flera resurser som du vill ta bort från publicering eller avpublicering.
   * I det övre högra hörnet av **[!UICONTROL Manage Publication - Scope]** sida, markera **[!UICONTROL Publish]** eller **[!UICONTROL Unpublish]** för att påbörja åtgärden.
1. Välj **[!UICONTROL OK]**.

## Kontrollera publiceringsstatus för en resurs {#check-publish-status-of-asset}

Du kan använda **[!UICONTROL Timeline]** med **[!UICONTROL Card view]**, **[!UICONTROL Column View]**, eller **[!UICONTROL List View]** i Experience Manager för att snabbt kontrollera publiceringsstatus för en resurs.

**Så här kontrollerar du publiceringsstatusen för en resurs:**

1. I Experience Manager, i det övre vänstra hörnet av sidan, väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen. Till vänster på sidan väljer du navigeringsikonen (alldeles ovanför verktygsikonen) och går till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. I **[!UICONTROL Card View]**, **[!UICONTROL Column View]**, eller **[!UICONTROL List View]** (skärmbilden nedan visar **[!UICONTROL List View]**) öppnar du en mapp som innehåller resurser som du har publicerat eller opublicerat.
1. Markera en resurs så att den visas med en bock. Se skärmbilden nedan.
1. I den nedrullningsbara menyn nära sidans övre vänstra hörn väljer du **[!UICONTROL Timeline]**. The **[!UICONTROL Status]** i den vänstra panelen visas den valda resursens publiceringstillstånd.
När du använder **[!UICONTROL List View]**, en extra kolumn för **[!UICONTROL Dynamic Media]** publiceringsstatus visas.
   * En mapp som är konfigurerad att synkroniseras till Dynamic Media visar **[!UICONTROL Dynamic Media]** kolumn som standard.
   * En mapp som *not* Dynamic Media-kolumnen visas inte om du har konfigurerat att synkronisera med Dynamic Media.
      ![Listvy och tidslinje](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Felsök selektiv publicering {#selective-publish-troubleshoot}

En resurs som inte synkroniseras med Dynamic Media men som har en publiceringsåtgärd från Dynamic Media aktiverad resulterar i följande felmeddelande och lösning:

![Selektivt publiceringsfel](/help/assets/assets-dm/selective-publish-error.png)
