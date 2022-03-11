---
title: Återanvända resurser med MSM
description: Använd resurser på flera sidor/mappar som är härledda från och länkade till överordnade resurser. Resurserna är synkroniserade med en primär kopia och med några klick får du uppdateringar från överordnade resurser.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: a71aebdf-8e46-4c2d-8960-d188b14aaae9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '3112'
ht-degree: 10%

---

# Återanvänd resurser med MSM för [!DNL Assets] {#reuse-assets-using-msm-for-assets}

MSM-funktionalitet (Multi Site Manager) i [!DNL Adobe Experience Manager] gör att användare kan återanvända innehåll som har skapats en gång och återanvänds på flera olika platser. Samma funktionalitet finns för digitala resurser vid namnet MSM för [!DNL Assets]. Använda MSM för [!DNL Assets]kan du:

* Skapa resurser en gång och gör sedan kopior av dessa resurser för återanvändning i andra delar av webbplatsen.
* Håll flera kopior synkroniserade och uppdatera originalkopian en gång för att överföra ändringarna till de underordnade kopiorna.
* Gör lokala ändringar genom att tillfälligt eller permanent avbryta länkningen mellan överordnade och underordnade resurser.

## Förstå fördelarna med och begreppen i MSM {#concepts}

### Så fungerar det och fördelarna {#how-it-works-and-the-benefits}

Om du vill veta mer om användningsscenarierna för återanvändning av samma innehåll (text och resurser) på flera webbplatser kan du läsa [möjliga MSM-scenarier](/help/sites-cloud/administering/msm/overview.md). [!DNL Experience Manager] behåller en länk mellan den ursprungliga resursen och dess länkade kopior, som kallas live-kopior. Tack vare den bevarade länken kan centraliserade ändringar skickas till många aktiva kopior. Detta ger snabbare uppdateringar och eliminerar samtidigt begränsningarna med att hantera duplicerade kopior. Spridningen av ändringar är felfri och centraliserad. Funktionen ger utrymme för uppdateringar som är begränsade till valda kopior. Användare kan koppla loss länken, d.v.s. bryta arv, och göra lokala redigeringar som inte skrivs över nästa gång den primära kopian uppdateras och ändringarna introduceras. Frånkopplingen kan göras för ett fåtal metadatafält eller för en hel resurs. Det ger flexibilitet att lokalt uppdatera resurser som ursprungligen ärvts från en primär kopia.

MSM upprätthåller en aktiv relation mellan källresursen och dess livekopior så att:

* Ändringar av källresurserna tillämpas (utlöses) även på live-kopior, det vill säga de live-kopior som synkroniseras med källan.
* Du kan uppdatera live-kopiorna genom att avbryta direktrelationen eller ta bort arvet för några få begränsade fält. Ändringarna i källan tillämpas inte längre på den aktiva kopian.

### Ordlista för MSM för [!DNL Assets] villkor {#glossary}

**Källa:** De ursprungliga resurserna eller mapparna. Primär kopia som live-kopior härleds från.

**Live copy:** Kopian av källresurserna/källmapparna som är synkroniserad med källan. Live-kopior kan vara en källa till fler live-kopior. Se hur du skapar LC:er.

**Arv:** En länk/referens mellan en resurs/mapp för en live-kopia och dess källa som systemet använder för att komma ihåg var uppdateringarna ska skickas. Arv finns på detaljnivå för metadatafält. Arv kan tas bort för selektiva metadatafält samtidigt som den aktiva relationen mellan källan och dess aktiva kopia bevaras.

**Utrullning:** En åtgärd som knuffar ändringar som gjorts i källan nedåt till dess aktiva kopior. Det går att uppdatera en eller flera live-kopior på en gång med en utrullningsåtgärd. Se utrullning.

**Konfiguration för utrullning:** Regler som bestämmer vilka egenskaper som ska synkroniseras, hur och när. Dessa konfigurationer används när live-kopior skapas. kan redigeras senare; och ett underordnat objekt kan ärva utrullningskonfigurationen från sin överordnade resurs. För MSM för [!DNL Assets]använder du bara standardkonfigurationen. Övriga utrullningskonfigurationer är inte tillgängliga för MSM för [!DNL Assets].

**Synkronisera:** En annan åtgärd, förutom utrullning, är att skapa paritet mellan källan och dess livekopia genom att skicka uppdateringarna från källan till livekopior. En synkronisering initieras för en viss live-kopia och åtgärden hämtar ändringarna från källan. Om du använder den här åtgärden kan du bara uppdatera en av live-kopiorna. Se synkroniseringsåtgärd.

**Gör uppehåll:** Ta tillfälligt bort den aktiva relationen mellan en live-kopia och dess källresurs/mapp. Du kan återuppta relationen. Se göra uppehåll i åtgärd.

**Återuppta:** Återuppta direktrelationen så att en live-kopia får uppdateringarna från källan igen. Se åtgärd för att återuppta.

**Återställ:** Återställ-åtgärden gör live-kopian en gång till till en replik av källan genom att alla lokala ändringar skrivs över. Den tar också bort arvsannulleringar och återställer arv i alla metadatafält. Om du vill göra lokala ändringar i framtiden måste du ångra arvet av specifika fält. Se lokala ändringar i LC.

**Koppla loss:** Ta oåterkalleligt bort den aktiva relationen mellan en resurs/mapp för en live-kopia. Efter att ha frigjort en åtgärd kan live-kopiorna aldrig få uppdateringar från källan och de slutar vara en live-kopia längre. Se Ta bort relation.

## Skapa en live-kopia av en resurs {#create-livecopy}

Om du vill skapa en live-kopia av en eller flera källresurser eller mappar gör du något av följande:

* Metod 1: Välj källresurserna och klicka på **[!UICONTROL Create]** > **[!UICONTROL Live Copy]** i verktygsfältet högst upp.
* Metod 2: I [!DNL Experience Manager] användargränssnitt, klicka **[!UICONTROL Create]** > **[!UICONTROL Live Copy]** i gränssnittets övre högra hörn.

Du kan skapa live-kopior av en resurs eller en mapp åt gången. Du kan skapa live-kopior som är härledda från en resurs eller en mapp som är en live-kopia. Content Fragments (CF) stöds inte för användningsfallet. När de försöker skapa sina live-kopior kopieras CF-filer som de är utan någon relation. De kopierade CF:erna är en ögonblicksbild i tid och uppdateras inte när ursprungliga CF:er uppdateras.

Så här skapar du live-kopior med den första metoden:

1. Välj källmaterial eller mappar. I verktygsfältet klickar du på **[!UICONTROL Create]** > **[!UICONTROL Live Copy]**.

   ![Skapa live-kopia från [!DNL Experience Manager] gränssnitt](assets/create_lc1.png)

   *Bild: Skapa live-kopia från [!DNL Experience Manager] gränssnitt.*

1. Välj en målmapp. Klicka på **[!UICONTROL Next]**.
1. Ange titel och namn. Resurserna har inga underordnade. När du skapar en live-kopia av mappar kan du välja att ta med eller exkludera underordnade.
1. Välj en utrullningskonfiguration. Klicka på **[!UICONTROL Create]**.

Så här skapar du live-kopior med den andra metoden:

1. I [!DNL Experience Manager] gränssnitt, från det övre högra hörnet, klicka **[!UICONTROL Create]** > **[!UICONTROL Live Copy]**.

   ![Skapa live-kopia från [!DNL Experience Manager] gränssnitt](assets/create_lc2.png)

   *Bild: Skapa live-kopia från [!DNL Experience Manager] gränssnitt.*

1. Välj källresurs eller källmapp. Klicka på **[!UICONTROL Next]**.
1. Välj målmapp. Klicka på **[!UICONTROL Next]**.
1. Ange titel och namn. Resurserna har inga underordnade. När du skapar en live-kopia av mappar kan du välja att ta med eller exkludera underordnade.
1. Välj en utrullningskonfiguration. Klicka på **[!UICONTROL Create]**.

>[!NOTE]
>
>När en källa eller en live-kopia flyttas behålls relationerna. När en live-kopia tas bort tas relationerna bort.

## Visa olika egenskaper och statusvärden för käll- och livekopia {#properties}

Du kan visa information och MSM-relaterade statusar för en live-kopia som relation, synkronisering, rollouts med mera från de olika områdena i [!DNL Experience Manager] användargränssnitt.

Följande två metoder fungerar för resurser och mappar:

* Välj en live-kopia och hitta informationen på sidan Egenskaper.
* Välj källmapp och hitta detaljerad information om varje live-kopia på menyn [!UICONTROL Live Copy Console].

>[!TIP]
>
>Om du vill kontrollera status för några separata live-kopior använder du den första metoden för att kontrollera **[!UICONTROL Properties]** sida. Om du vill kontrollera status för många live-kopior använder du den andra metoden för att kontrollera **[!UICONTROL Relationship Status]** sida.

### Information om och status för en live-kopia {#status-lc-asset}

Följ de här stegen för att kontrollera information och status för en live-kopia-resurs eller en mapp.

1. Välj en live-kopia eller en mapp. Klicka på **[!UICONTROL Properties]** i verktygsfältet. Du kan även använda kortkommandot `p`.
1. Klicka på **[!UICONTROL Live Copy]**. Du kan kontrollera sökvägen till källan, avbrottsstatus, synkroniseringsstatus, det senaste utrullningsdatumet och den användare som gjorde den senaste utrullningen.

   ![Live-kopieringsinformation och status visas i en konsol i Egenskaper](assets/lcfolder_info_properties.png)

   *Bild: Live copy-information och status.*

1. Du kan aktivera eller inaktivera om underordnade resurser lånar konfigurationen för live-kopia.

1. Du kan välja att live-kopian ska ärva utrullningskonfigurationen från den överordnade kopian eller ändra konfigurationen.

### Information om och status för alla live-kopior av en mapp {#status-lc-folder}

[!DNL Experience Manager] innehåller en konsol för att kontrollera status för alla live-kopior av en källmapp. Den här konsolen visar status för alla underordnade resurser.

1. Välj en källmapp. Klicka på **[!UICONTROL Properties]** i verktygsfältet. Du kan även använda kortkommandot `p`.
1. Klicka på **[!UICONTROL Live Copy Source]**. Klicka på **[!UICONTROL Live Copy Overview]** för att öppna konsolen. På den här kontrollpanelen visas status på den översta nivån för alla underordnade resurser.

   ![Visa status för live-kopior i Live Copy-konsolen](assets/livecopy-statuses.png)

   *Bild: Visa status för live-kopior i [!UICONTROL Live Copy Console] för källan.*

1. Om du vill visa detaljerad information om alla resurser i mappen med live-kopian markerar du en resurs och klickar på **[!UICONTROL Relationship Status]** i verktygsfältet.

   ![Detaljerad information om och status för en underordnad live-kopia i en mapp](assets/livecopy_relationship_status.png)

   Detaljerad information om och status för en underordnad live-kopia i en mapp

>[!TIP]
>
>Du kan snabbt se status för live-kopior av andra mappar utan att behöva bläddra för mycket. Ändra mappen från den övre mittersta delen av **[!UICONTROL Live Copy Overview]** gränssnitt.

### Snabbåtgärder från referensfältet för källan {#ref-rail-source}

För en källresurs eller källmapp kan du se följande information och utföra följande åtgärder direkt från referensfältet:

* Se sökvägarna för live-kopior.
* Öppna eller visa en viss live-kopia i [!DNL Experience Manager] användargränssnitt.
* Synkronisera uppdateringarna till en specifik live-kopia.
* Pausa relationen eller ändra utrullningskonfiguration för en specifik live-kopia.
* Få åtkomst till översiktskonsolen för live-kopian.

Välj källresurs eller källmapp, öppna den vänstra listen och klicka på **[!UICONTROL References]**. Du kan också markera en resurs eller mapp och använda kortkommandot `Alt + 4`.

![Åtgärder och information som är tillgänglig i referensfältet för den valda källan](assets/referencerail_source.png)

*Bild: Åtgärder och information som finns i referensfältet för den valda källan.*

För en viss live-kopia klickar du på **[!UICONTROL Edit Live Copy]** om du vill göra uppehåll i relationen eller ändra utrullningskonfiguration.

![För en specifik live-kopia är alternativet att pausa relationen eller ändra utrullningskonfiguration tillgängligt från referenslisten när källresurs har valts](assets/referencerail_editlc_options.png)

*Bild: Pausa relationen eller ändra utrullningskonfigurationen för en specifik live-kopia.*

### Snabbåtgärder från referensfältet för live-kopia {#ref-rail-lc}

För en resurs eller mapp för en live-kopia kan du se följande information och utföra följande åtgärder direkt från referenslisten:

* Se källans sökväg.
* Öppna eller visa en viss live-kopia i [!DNL Experience Manager] användargränssnitt.
* Fyll i uppdateringarna.

Välj en resurs eller mapp med en live-kopia, öppna den vänstra rutan och klicka på **[!UICONTROL References]**. Du kan också markera en resurs eller mapp och använda kortkommandot `Alt + 4`.

![Åtgärder som är tillgängliga i referensrutan för den valda live-kopian](assets/referencerail_livecopy.png)

*Bild: Åtgärder som är tillgängliga i referensfältet för den markerade live-kopian.*

## Sprid ändringar från källa till live-kopior {#rollout-sync}

När en källa har ändrats kan ändringarna spridas till live-kopiorna med antingen en synkroniseringsåtgärd eller en utrullningsåtgärd. Mer information om skillnaden mellan de båda åtgärderna finns i [ordlista](#glossary).

### Åtgärd för utrullning {#rollout}

Du kan initiera en utrullningsåtgärd från källresursen och uppdatera alla eller några utvalda live-kopior.

1. Välj en live-kopia eller en mapp. Klicka på **[!UICONTROL Properties]** i verktygsfältet. Du kan även använda kortkommandot `p`.
1. Klicka på **[!UICONTROL Live Copy Source]**. Klicka på **[!UICONTROL Rollout]** i verktygsfältet.
1. Markera de live-kopior som du vill uppdatera. Klicka på **[!UICONTROL Rollout]**.
1. Om du vill ta med uppdateringarna som gjorts för de underordnade resurserna väljer du **[!UICONTROL Rollout Source and all Children]**.

   ![Fyll ut ändringarna av källan till några eller alla live-kopior](assets/livecopy_rollout_page.png)

   *Bild: Fyll ut ändringarna av källan till några eller alla live-kopior.*

>[!NOTE]
>
>Ändringar som görs i en källresurs rullas endast ut till direkt relaterade live-kopior. Om en live-kopia kommer från en annan live-kopia, rullas inte ändringarna ut till den härledda live-kopian.

Du kan också starta en utrullningsåtgärd från referenslinjen när du har valt en specifik live-kopia. Mer information finns i [Snabbåtgärder från referensfältet för live-kopia](#ref-rail-lc). I den här metoden för utrullning uppdateras endast den markerade live-kopian och eventuellt dess underordnade.

![Rulla ut ändringarna av källan till den markerade live-kopian](assets/livecopy_rollout_dialog.png)

*Bild: Rulla ut ändringarna av källan till den markerade live-kopian.*

### Om synkroniseringsåtgärd {#about-sync}

Med en synkroniseringsåtgärd hämtas ändringarna från en källa endast till den markerade Live-kopian. Synkroniseringsåtgärden respekterar och underhåller lokala ändringar som gjorts efter att arv har annullerats. De lokala ändringarna skrivs inte över och arvet som avbryts återupprättas inte. Du kan initiera en synkroniseringsåtgärd på tre sätt.

| Var finns [!DNL Experience Manager] gränssnitt | När och varför ska du använda | Så här använder du |
|---|---|---|
| [!UICONTROL References] järnväg | Synkronisera snabbt när du redan har markerat källan. | Se [Snabbåtgärder från referensfältet för källan](#ref-rail-source) |
| Verktygsfältet i [!UICONTROL Properties] page | Starta en synkronisering när du redan har live-kopieringsegenskaperna öppna. | Se [Synkronisera en live-kopia](#sync-lc) |
| [!UICONTROL Live Copy Overview] konsol | Synkronisera snabbt flera resurser (inte nödvändigtvis alla) när källmappen är markerad eller [!UICONTROL Live Copy Overview] konsolen är redan öppen. Synkroniseringsåtgärden initieras för en resurs i taget men är ett snabbare sätt att synkronisera flera resurser på en gång. | Se [Åtgärder för många resurser i en dynamisk kopiamapp](#bulk-actions) |

### Synkronisera en live-kopia {#sync-lc}

Om du vill starta en synkroniseringsåtgärd öppnar du sidan **[!UICONTROL Properties]** för en live-kopia, klickar på **[!UICONTROL Live Copy]** och klickar sedan på önskad åtgärd i verktygsfältet.

Om du vill se status och information om en synkroniseringsåtgärd läser du [Information om och status för en live-kopia](#status-lc-asset) samt [Information och status för alla live-kopior av en mapp](#status-lc-folder).

![Synkroniseringsåtgärden hämtar de ändringar som gjorts i källan](assets/livecopy_sync.png)

*Bild: Funktionen Synkronisera drar in de ändringar som har gjorts i källan.*

>[!NOTE]
>
>Om relationen är inaktiverad är synkroniseringsåtgärden inte tillgänglig i verktygsfältet. Synkroniseringsåtgärden är tillgänglig i referensfältet, men ändringarna sprids inte ens när en lyckad utrullning har slutförts.

## Pausa och återuppta relation {#suspend-resume}

Du kan tillfälligt inaktivera relationen för att förhindra att en live-kopia tar emot ändringar som gjorts i källresursen eller källmappen. Relationen kan även återupptas för live-kopiering för att börja ta emot ändringarna från källan.

Om du vill pausa eller återuppta öppnar du sidan **[!UICONTROL Properties]** för en live-kopia, klickar på **[!UICONTROL Live Copy]** och klickar sedan på önskad åtgärd i verktygsfältet.

Du kan också snabbt pausa eller återuppta relationer för flera resurser i en mapp med live-kopior på konsolen **[!UICONTROL Live Copy Overview]**. Se [Utföra åtgärder för många resurser i mappar med live-kopior](#bulk-actions).

## Göra lokala ändringar i en live-kopia {#local-mods}

En live-kopia är en kopia av den ursprungliga källan när den skapas. Metadatavärdena för en live-kopia ärvs från källan. Metadatafälten behåller enskilt arv med respektive fält i källresursen.

Du kan dock göra lokala ändringar i en live-kopia för att ändra vissa egenskaper. Om du vill göra lokala ändringar avbryter du arvet av den önskade egenskapen. När arvet efter ett eller flera metadatafält avbryts behålls resursens live-relation och arvet efter de andra metadatafälten. Synkronisering eller utrullning skriver inte över lokala ändringar. Öppna **[!UICONTROL Properties]** sidan med en live-kopia klickar du på **[!UICONTROL cancel inheritance]** bredvid ett metadatafält.

Du kan ångra alla lokala ändringar och återställa resursen till källans läge. Återställ åtgärd oåterkalleligt och omedelbart åsidosätter alla lokala ändringar och återupprättar arv på alla metadatafält. Om du vill återgå går du till **[!UICONTROL Properties]** sidan med en live-kopia, klicka på **[!UICONTROL Reset]** i verktygsfältet.

![Återställ-åtgärden skriver över lokala redigeringar och delar av den aktiva kopian med källan.](assets/livecopy_reset.png)

*Bild: Återställ-åtgärden skriver över lokala redigeringar och delar av den aktiva kopian med källan.*

## Ta bort direktrelation {#detach}

Du kan ta bort relationen mellan en källa och en live-kopia helt med åtgärden Koppla loss. Den aktiva kopian blir en fristående resurs eller mapp när den har kopplats loss. Den visas som en ny resurs i [!DNL Experience Manager] -gränssnittet, omedelbart efter frånkoppling. Följ de här stegen för att koppla loss en live-kopia från källan.

1. Välj en resurs eller mapp för en live-kopia. Klicka på **[!UICONTROL Properties]** i verktygsfältet. Du kan även använda kortkommandot `p`.

1. Klicka på **[!UICONTROL Live Copy]**. Klicka **[!UICONTROL Detach]** i verktygsfältet. Klicka **[!UICONTROL Detach]** i den dialogruta som visas.

   ![Koppla loss-åtgärden tar helt bort relationen mellan källa och live-kopia](assets/livecopy_detach.png)

   *Bild: Kopplingsåtgärden tar bort relationen mellan källan och den aktiva kopian helt.*

   >[!CAUTION]
   >
   >Relationen tas bort omedelbart när du klickar **[!UICONTROL Detach]** i dialogrutan. Du kan inte ångra den genom att klicka på **[!UICONTROL Cancel]** på sidan Egenskaper.

Du kan också snabbt frigöra flera resurser i en live-kopieringsmapp från **[!UICONTROL Live Copy Overview]** konsol. Se [Utföra åtgärder för många resurser i mappar med live-kopior](#bulk-actions).

## Massåtgärder i en mapp för live-kopior {#bulk-actions}

Om du har flera resurser i en live-kopieringsmapp kan initieringsåtgärder för varje resurs vara långsamma. Du kan snabbt initiera grundläggande åtgärder för många resurser från [!UICONTROL Live Copy Console]. Ovanstående metoder fortsätter att fungera för enskilda resurser.

1. Välj en källmapp. Klicka på **[!UICONTROL Properties]** i verktygsfältet. Du kan även använda kortkommandot `p`.
1. Klicka på **[!UICONTROL Live Copy Source]**. Klicka på **[!UICONTROL Live Copy Overview]** för att öppna konsolen.
1. På den här kontrollpanelen väljer du en live-resurs från en live-mapp. Klicka på önskade åtgärder i verktygsfältet. De tillgängliga åtgärderna är **[!UICONTROL Synchronize]**, **[!UICONTROL Reset]**, **[!UICONTROL Suspend]** och **[!UICONTROL Detach]**. Du kan snabbt initiera dessa åtgärder för alla resurser i valfritt antal kopiamappar som finns i en direktrelation med den valda källmappen.

   ![Uppdatera enkelt många resurser i kopiemappar från Live Copy Overview-konsolen](assets/livecopyconsole_update_many_assets.png)

   *Bild: Uppdatera enkelt mycket material i kopiemappar från [!UICONTROL Live Copy Overview] konsol.*

<!-- TBD: Can MSM be extended using Java APIs in CS?

## Extend MSM for [!DNL Assets] {#extend-api}

[!DNL Experience Manager] lets you extend the functionality using the MSM Java APIs. For [!DNL Assets], the extending works just the same as it works with MSM for [!DNL Sites]. For details, see [Extending the MSM](/help/sites-developing/extending-msm.md) and the following for information about specific tasks:

* [Overview of APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [Create a synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [Create and use a simple LiveActionFactory class](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

-->

## Effekter av tillgångshanteringsåtgärder på live-kopior {#manage-assets}

Live-kopior och källor är resurser eller mappar som i viss utsträckning kan hanteras som digitala resurser. Vissa resurshanteringsuppgifter i [!DNL Experience Manager] har en specifik inverkan på live-kopiorna.

* När du kopierar en live-kopia skapas en live-kopia med samma källa som den första live-kopian.
* När du flyttar en källa eller dess aktiva kopia behålls den aktiva relationen.
* Redigeringsåtgärden fungerar inte för live-kopieringsresurser. Om källan till en live-kopia är en live-kopia i sig, fungerar inte redigeringsåtgärden för den.
* Utcheckningsåtgärden är inte tillgänglig för livekopieringsresurser.
* För källmappen är alternativet att skapa granskningsåtgärder tillgängligt.
* När du visar resursexemplet i listvyn och kolumnvyn visas live-kopia av en resurs eller mapp. Det gör det enklare att identifiera live-kopior i en mapp.

## Jämför MSM för [!DNL Assets] och [!DNL Sites] {#comparison}

I fler scenarier, MSM för [!DNL Assets] matchar MSM för Sites-funktionaliteten. Några viktiga skillnader är:

* Blueprint in MSM for [!DNL Sites] kallas Live Copy-källa i MSM för [!DNL Assets].
* I Sites kan du jämföra en plan och dess live-kopia, men det är inte möjligt i [!DNL Assets] för att jämföra en källa med dess livekopia.
* Du kan inte redigera en live-kopia i [!DNL Assets].
* Platserna har vanligtvis underordnade, men [!DNL Assets] inte. Alternativet att inkludera eller exkludera underordnade objekt finns inte när du skapar direktkopior av enskilda resurser.
* Det går inte att ta bort kapitelsteget i guiden Skapa plats i MSM för [!DNL Assets].
* Det går inte att konfigurera MSM-lås på sidegenskaper i MSM för [!DNL Assets].
* För MSM för [!DNL Assets], använd bara **[!UICONTROL Standard rollout config]**. Övriga utrullningskonfigurationer är inte tillgängliga för MSM för [!DNL Assets].

## Begränsningar och kända problem med MSM för [!DNL Assets] {#limitations}

Följande begränsningar gäller för MSM för [!DNL Assets].

* Innehållsfragment stöds inte. När du försöker skapa live-kopior kopieras innehållsfragment som de är utan någon relation. De kopierade innehållsfragmenten är en ögonblicksbild i tid och uppdateras inte när du uppdaterar de ursprungliga innehållsfragmenten.

* MSM fungerar inte när återkoppling av metadata är aktiverat. Vid tillbakaskrivning avbryts arvet.
