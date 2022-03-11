---
title: Förinställningar för gruppuppsättning
description: Lär dig automatisera framtagning av bilduppsättningar och snurra uppsättningar med hjälp av gruppuppsättningsförinställningar i Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3200'
ht-degree: 0%

---

# Om förinställningar för gruppuppsättning {#about-bsp}

Använd **[!UICONTROL Batch Set Presets]** om du vill skapa och ordna flera resurser i en bilduppsättning eller snurra uppsättningar när du överför resursfiler till en mapp, antingen individuellt eller med gruppinläsning. Du kan låta förinställningen köras tillsammans med de resursimporteringsjobb som du schemalägger i [!DNL Dynamic Media]. Varje förinställning är en unikt namngiven, självständig uppsättning instruktioner som definierar hur bilduppsättningen eller rotationsuppsättningen ska skapas med bilder som matchar de definierade namnkonventionerna i förinställningsreceptet.

>[!IMPORTANT]
>
>Använder du gruppuppsättningsförinställningar i [!DNL Dynamic Media Classic]och migrera från [!DNL Dynamic Media Classic] till Adobe Experience Manager as a Cloud Service? I så fall måste du manuellt återskapa definitioner av gruppuppsättningar i [!DNL Adobe Experience Manager as a Cloud Service].

**Bästa praxis** - När du arbetar med gruppuppsättningsförinställningar rekommenderar Adobe följande arbetsflöde:

1. Skapa en gruppuppsättningsförinställning. Se [Skapa en förinställning för gruppuppsättning för en bilduppsättning eller en snurruppsättning](#creating-bsp).
1. Skapa en resursmapp eller använd en befintlig resursmapp och kontrollera att den synkroniseras till [!DNL Dynamic Media]. Se [Skapa mappar](/help/assets/manage-digital-assets.md#creating-folders).
1. Använd gruppuppsättningsförinställningen på resursmappen. Se [Tillämpa gruppuppsättningsförinställningar på mappar](#apply-bsp).
1. Överför bilder till resursmappen. Se [Överför resurser för bilduppsättningar](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Överför resurser för snurruppsättningar](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets), eller [Lägg till digitalt material i Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. Bilduppsättningen eller rotationsuppsättningen genereras automatiskt i den önskade mappen.
1. Publicera din bilduppsättning eller snurra. Se [Publicera Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Skapa en förinställning för gruppuppsättning för en bilduppsättning eller en snurruppsättning {#creating-bsp}

Om du vill skapa förinställningar för gruppuppsättningar bör du känna till och förstå reguljära uttryck.

Helst har ditt företag redan definierat en namngivningskonvention för hur resurser grupperas i en uppsättning.
För att du ska få en förståelse för vikten av att använda en namnkonvention kan du anta att företagets definierade namnkonvention är `<style>-<color>-<view>`. Och basnamnet för uppsättningen måste alltid vara `<style>-<color>`och set name-tillägget är `-SET`. Om du överför en bild med namnet `0123-RED-01`så skapas en uppsättning med namnet `0123-RED-SET`. Om du senare överför bilder `0123-RED-03` och `0123-BLUE-01`och sedan `RED-03` bilden läggs till i uppsättningen på den andra positionen eftersom den sorteras lägre än `01`. Men `BLUE-01` bilden skulle ingå i en ny uppsättning med namnet `0123-BLUE-SET`. För nästa överföring av resurser lägger du till filer `0123-RED-02` och `0123-BLUE-02`. Varje tillgång läggs till i sin respektive uppsättning. The `RED-02` bilden automatiskt sorteras mellan den befintliga `01` och `03` bilder, på grund av sorteringsordningen.

The **[!UICONTROL Batch Set Preset]** sida in [!DNL Dynamic Media] Med kan du skapa, redigera eller ta bort förinställningar för gruppuppsättningar och använda eller ta bort förinställningar för gruppuppsättningar i eller från resursmappar. Du kan antingen använda listrutorna i formulärfältet för att definiera en förinställning för gruppuppsättning eller använda **[!UICONTROL Raw Code]** -fält, vilket gör att du kan skriva syntax för reguljära uttryck.

Du kan skapa många gruppuppsättningsförinställningar så att du täcker alla resursinställningar du behöver.

### Om Konvention för namngivning av resurser

The **[!UICONTROL Asset Naming Convention]** området på **[!UICONTROL Batch Set Preset]** sidan har två element som du kan använda för att definiera din gruppuppsättningsförinställning: **[!UICONTROL Match]** och **[!UICONTROL Base Name]**. Med dessa element kan du definiera en namnkonvention och identifiera den del av konventionen som används för att namnge den uppsättning i vilken de finns. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

Ett företags namnkonvention använder ofta en eller flera definitionsrader för var och en av dessa två element. Du kan använda så många rader för din unika definition och gruppera dem i distinkta element, t.ex. för Huvudbild, Färgelement, Alternativa vyer och Färgruteelement.

Syntaxen för en litteral matchning av reguljära uttryck kan till exempel se ut så här:

`(\w+)-\w+-\w+`

### Om sekvensordning

Du kan också definiera i vilken ordning bilderna ska visas efter att bilduppsättningen eller rotationsuppsättningen har grupperats i [!DNL Dynamic Media]. Som standard sorteras dina resurser alfanumeriskt. Du kan dock använda en kommaavgränsad lista med reguljära uttryck för att definiera ordningen.

När det gäller automatisering av sekvensorder anger du regler för att tvinga resurser att sortera på ett visst sätt, om det behövs. Anta till exempel att din första resurs alltid har ett namn `_main` och du vill ha det följt av `_alt1`, `_alt2`, `_alt3`och så vidare. I så fall kan du skapa en sekvensordningsregel med följande syntax:

`.*_main,.*_alt[0-9]`

En sekvens med tvingad sortering är möjlig, men det är bäst att använda alfanumeriska nummer för sekvensordning så mycket som möjligt. Dessutom kan du använda verktygen för bilduppsättning eller snurrfunktion i [!DNL Dynamic Media] om du vill ändra ordningsföljden för resurser eller lägga till och ta bort nya resurser i uppsättningen genom att dra och släppa.

När du är klar med att skapa en gruppuppsättningsförinställning använder du den på en eller flera mappar som du har skapat. Se [Tillämpa gruppuppsättningsförinställningar på mappar](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Så här skapar du en gruppuppsättningsförinställning för en bilduppsättning eller en snurruppsättning:**

1. Välj logotypen för Experience Manager och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. På **[!UICONTROL Batch Set Presets]** sida, nära det övre högra hörnet, markera **[!UICONTROL Create]**.
1. I **[!UICONTROL Create Batch Set Preset]** i **[!UICONTROL Preset Name]** anger du ett beskrivande namn i textfältet. Förinställningsnamnet kan inte redigeras om du senare bestämmer dig för att ändra det.

1. I **[!UICONTROL Preset Type]** nedrullningsbar lista, välja **[!UICONTROL ImageSet]** eller **[!UICONTROL SpinSet]**. Se till att du väljer rätt förinställningstyp. går inte att redigera senare.
1. Välj **[!UICONTROL Create]**.
1. Till höger om **[!UICONTROL Edit Batch Set Preset]** ställer du in de redigeringsbara alternativ du vill ha under **[!UICONTROL Preset Details]** och **[!UICONTROL Set Naming Convention]** rubriker.
Om du vill veta mer om de redigerbara alternativen som är tillgängliga för dig kan du läsa [Förinställningsinformation, Ange namngivningskonvention och Regelresultat - RegX-alternativ](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Skapa en eller flera grupper med reguljära uttryck.

   * Till vänster om **[!UICONTROL Edit Batch Set Preset]** sida, under **[!UICONTROL Match]**, **[!UICONTROL Base Name]**, eller **[!UICONTROL Sequence Ordering]**, markera **[!UICONTROL Add Group]**.
   * The **[!UICONTROL Match]** fältet är obligatoriskt. **[!UICONTROL Base Name]** är bara obligatoriskt om **[!UICONTROL Match]** fältet anger inte redan ett basnamn med hjälp av en hakparentesgruppering. **[!UICONTROL Sequence Ordering]** är valfritt.
   * Använd listrutorna och textrutorna i gruppens formulär och ange en uttrycksgrupp som du vill använda för att definiera namnvillkoren för bilduppsättnings- eller rotationsuppsättningens resursmedlemmar.
      * När du väljer och anger uttryck för en grupp bör du lägga märke till att den faktiska syntaxen för reguljära uttryck återspeglas i det nedre högra hörnet på sidan, under **[!UICONTROL Rule Results - RegX]** rubrik. Om du vill se strängen för det reguljära uttrycket uppdateras i det nedre högra hörnet, markerar du var som helst utanför formulärområdet. De här strängarna för reguljära uttryck representerar mönstret som du vill matcha i en sökning efter [!DNL Dynamic Media] resurser för att skapa din bilduppsättning eller snurra uppsättning.
      * Om du har lagt till en grupp och vill ta bort den väljer du **[!UICONTROL X]**.
   * När du lägger till två eller flera grupper finns det i **[!UICONTROL And]** nedrullningsbar lista, välja **[!UICONTROL And]** om du vill koppla en nyligen tillagd grupp till en tidigare uttrycksgrupp som du har lagt till. Eller markera **[!UICONTROL Or]** om du vill lägga till ett alternativ mellan den föregående uttrycksgruppen och den nya gruppen som du skapar. The **[!UICONTROL Or]** operanden definieras genom användning av ett lodrätt streck `|` i syntaxen för reguljära uttryck.

1. Gör något av följande:

   * Lägga till en ny grupp under **[!UICONTROL Match]**, **[!UICONTROL Base Name]**, eller **[!UICONTROL Sequencing Order]**, markera **[!UICONTROL Add Group]**. Skapa en annan grupp med reguljära uttryck på samma sätt som i föregående steg.
   * Granska syntaxen för reguljära uttryck i **[!UICONTROL Rule Results - RegX]** område. Om du måste ändra syntaxen gör du ändringarna i respektive grupp till vänster på sidan.
   * Om du har skapat uttrycksgrupper fortsätter du till nästa steg.

1. I det övre högra hörnet på sidan väljer du **[!UICONTROL Save]**.

Du kan nu använda gruppuppsättningsförinställningen på en resursmapp. Sedan överför du resurser till den mappen. Det här arbetsflödet leder till automatisk generering av bilduppsättningen eller rotationsuppsättningen. Se [Tillämpa gruppuppsättningsförinställningar på resursmappar](#apply-bsp).

### Förinställningsinformation, Ange namngivningskonvention och Regelresultat - RegX-alternativ {#features-options-bsp}

Dessa alternativ finns på **[!UICONTROL Edit Batch Set Preset]** när du skapar eller redigerar en förinställning för gruppuppsättning.

Se [Skapa en förinställning för gruppuppsättning för en bilduppsättning eller en snurruppsättning](#creating-bsp) eller [Redigera en gruppuppsättningsförinställning](#edit-bsp).

| **[!UICONTROL Preset Details]** | Beskrivning |
| --- | --- |
| Förinställningsnamn | Skrivskyddad. Det namn du angav när du skapade gruppuppsättningen. Om du måste byta namn på förinställningen kan du kopiera den befintliga förinställningen för gruppuppsättning och ange ett nytt namn. Se [Kopiera en befintlig gruppuppsättningsförinställning](#copy-bsp). |
| Typ | Skrivskyddad. Typen angavs när du först skapade gruppuppsättningen. Om du kopierar en befintlig gruppuppsättningsförinställning kan du inte ändra dess [!UICONTROL Type]; du måste skapa en förinställning i stället. |
| Inkludera härledda tillgångar | Valfritt. Att ha [!DNL Dynamic Media]I IPS (Image Production System) ingår genererade eller&quot;härledda&quot; bilder i din snurruppsättning eller bilduppsättning. Välj **[!UICONTROL Yes]** (standard). En härledd resurs är en bild som inte har överförts direkt av en användare. I stället producerades resursen av IPS när en överordnad resurs överfördes. En bildresurs som IPS genererade från en sida i PDF när PDF överfördes i [!DNL Dynamic Media], betraktas som en härledd tillgång. |
| Målmapp | Valfritt. Om du definierar ett stort antal bilduppsättningar eller snurruppsättningar bör du hålla uppsättningarna åtskilda från de mappar som innehåller själva resurserna. Överväg därför att skapa en mapp för bilduppsättningar eller snurruppsättningar och dirigera om programmet så att gruppuppsättningsgenererade uppsättningar placeras här.<br>Ange i så fall vilken mapp i mappstrukturen för Experience Manager Assets (`/content/dam`) har gruppuppsättningsförinställningen aktiv. Kontrollera att mappen är aktiverad för [!DNL Dynamic Media] synkronisering för att tillåta det som en målmapp. Se [Konfigurera selektiv publicering på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>Mer än en mapp kan ha tilldelats en angiven gruppuppsättningsförinställning om du använder förinställningen via mappens **[!UICONTROL Properties]**. Se [Använda gruppuppsättningsförinställningar från egenskapssidan för en resursmapp](#apply-bsp-to-folders-via-properties).<br>Om du inte anger en mapp skapas den förinställda gruppuppsättningen som genereras eller rotationsuppsättningen i samma mapp som den resursmapp du överförde till. |
| **[!UICONTROL Set Naming Convention]** |  |
| Prefix<br>eller<br>Suffix | Valfritt. Ange antingen ett prefix, suffix eller båda i respektive fält.<br>Med hjälp av prefix- och suffixfälten kan du skapa många gruppuppsättningsförinställningar med hjälp av en alternativ, anpassad namnkonvention för en viss uppsättning innehåll. Den här metoden är särskilt användbar om det finns ett undantag från ett företags definierade standardnamngivningsschema.<br>Prefixet eller suffixet läggs till i **[!UICONTROL Base Name]** du definierar i dialogrutan **[!UICONTROL Asset Naming Convention]** område. Genom att lägga till ett prefix eller suffix försäkrar du dig om att din bilduppsättning eller rotationsuppsättning skapas exklusivt och oberoende av andra resurser. Den kan också hjälpa andra att identifiera filtyper ytterligare. Om du till exempel vill fastställa vilket färgläge som används kan du lägga till som prefix eller suffix `rgb` eller `cmyk`.<br>Du bör använda namnkonventionen set när du anger en namnkonvention för uppsättning som inte behöver använda funktionen för gruppuppsättningsförinställningar. Med den här metoden kan du definiera så många element i namnkonventionen som du vill gruppera i en uppsättning för att effektivisera skapandet av gruppuppsättningar. |
| **[!UICONTROL Rule Results - RegX]** |  |
| Konvention om namngivning av tillgångar - matchning | Skrivskyddad. Visar syntaxen för det reguljära uttrycket baserat på de alternativ för Matcha formulär som du har valt eller den råkod som du har angett. |
| Konvention för namngivning av tillgångar - basnamn | Skrivskyddad. Visar syntaxen för det reguljära uttrycket baserat på de alternativ för basnamn som du har valt eller den råkod som du har angett. |
| Sekvensordning - matchning | Skrivskyddad. Visar syntaxen för det reguljära uttrycket baserat på de formuläralternativ du valt eller den råkod du angett. |

## Tillämpa gruppuppsättningsförinställningar på resursmappar {#apply-bsp}

När du tilldelar gruppuppsättningsförinställningar till en eller flera resursmappar ärver alla undermappar automatiskt förinställningarna från den överordnade mappen.

Du kan använda flera gruppuppsättningsförinställningar i en resursmapp.

Mappar som har tilldelats en gruppförinställning visas i användargränssnittet med namnet på förinställningen som visas i mappen, i **[!UICONTROL Card]** vy.

Om du vill använda gruppuppsättningsförinställningar på resursmappar använder du någon av följande två metoder:

* [Använda gruppuppsättningsförinställningar på resursmappar från sidan Gruppera förinställningar](#apply-bsp-to-folders-via-bsp-page) - Den här metoden ger dig den flexibilitet du behöver. Du kan använda en eller flera förinställningar för en eller flera mappar.
* [Använda gruppuppsättningsförinställningar från egenskapssidan för en resursmapp](#apply-bsp-to-folders-via-properties) - Med den här metoden kan du använda en eller flera gruppuppsättningsförinställningar i en enda mapp.

Ett tips är att se till att resursmapparna synkroniseras [!DNL Dynamic Media]använder du sedan de förinställningar du vill använda.

Bearbeta resurser i en mapp på nytt om du upplever något av följande två scenarier:

* Du vill köra en gruppuppsättningsförinställning på en befintlig resursmapp som redan har resurser överförda till den.
* Du redigerar senare en befintlig gruppuppsättningsförinställning som tidigare använts på en mapp med resurser.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Använda gruppuppsättningsförinställningar på resursmappar från sidan Gruppera förinställningar {#apply-bsp-to-folders-via-bsp-page}

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. På **[!UICONTROL Batch Set Presets]** till vänster om **[!UICONTROL Preset Name]** markerar du kryssrutan för varje gruppuppsättningsförinställning som du vill tillämpa på mappar.
1. Välj **[!UICONTROL Apply Batch Preset to Folders]**.
1. På **[!UICONTROL Select Folders]** markerar du kryssrutan för varje mapp som du vill använda gruppuppsättningsförinställningarna på.
1. I det övre högra hörnet av **[!UICONTROL Select Folders]** sida, markera **[!UICONTROL Apply]**.

### Använda gruppuppsättningsförinställningar från egenskapssidan för en resursmapp {#apply-bsp-to-folders-via-properties}

1. Välj logotypen för Experience Manager och gå till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navigera till en mapp där du vill använda en eller flera gruppuppsättningsförinställningar.
1. På sidan, till vänster om **[!UICONTROL Name]** markerar du kryssrutan för en mapp.
1. Välj **[!UICONTROL Properties]**.
1. På mappens egenskapssida väljer du **[!UICONTROL Dynamic Media Processing]** -fliken.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. Under **[!UICONTROL Batch Set Presets]**, från **[!UICONTROL Preset Name]** markerar du namnet på den förinställning för gruppuppsättning som du vill använda. På skärmbilden ovan visas två valda gruppuppsättningsförinställningar som används i resursmappen.

   Om det inte finns några förinställda gruppuppsättningsnamn i **[!UICONTROL Preset Name]** betyder det att du ännu inte har skapat några förinställningar för gruppuppsättningar. Se [Skapa en förinställning för gruppuppsättning för en bilduppsättning eller en snurruppsättning](#creating-bsp).

   Om du vill ta bort en tillämpad gruppuppsättningsförinställning väljer du **[!UICONTROL X]** till höger om förinställningstypen.

1. I det övre högra hörnet på sidan väljer du **[!UICONTROL Save & Close]**.

## Redigera en gruppuppsättningsförinställning {#edit-bsp}

Du kan redigera en befintlig gruppuppsättningsförinställning som du har skapat. Du kan ändra alla uttrycksgrupper som du har skapat för namnkonventionen eller sekvensordningen för resursen. Om det behövs kan du även uppdatera målmappen och ange namnkonventioner.

Du kan dock inte ändra förinställningens namn eller förinställningstyp (Bilduppsättning eller Snurra uppsättning). Om det blir nödvändigt att ändra namnet på en förinställning kopierar du den befintliga förinställningen och anger ett nytt namn. Se [Kopiera en gruppuppsättningsförinställning](#copy-bsp).

Om du redigerar en gruppuppsättningsförinställning som tidigare använts på en mapp, används den nyligen redigerade gruppuppsättningsförinställningen bara på nya resurser som överförts till den mappen.

Om du vill att den nyligen redigerade förinställningen ska tillämpas på de befintliga resurserna i mappen måste du bearbeta om mappen. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->På så sätt skulle de befintliga resurserna nu kvalificeras som en del av en bilduppsättning eller en snurra och läggas till. Dessutom tas inte befintliga resurser som redan ingick i bilduppsättningen eller rotationsuppsättningen bort och visas som de är, baserat på den tidigare förinställningen för gruppuppsättning som användes. I det här scenariot antas de inte längre vara kvalificerade baserat på den nyligen redigerade förinställningen.

**Så här redigerar du en gruppuppsättningsförinställning:**

1. Välj logotypen för Experience Manager och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. På **[!UICONTROL Batch Set Presets]** till vänster om **[!UICONTROL Preset Name]** markerar du den förinställning för gruppuppsättning som du vill ändra.
1. Välj **[!UICONTROL Edit Batch Set Preset]**.
1. Redigera förinställningen efter behov.
1. I det övre högra hörnet av **[!UICONTROL Batch Set Preset]** sida, markera **[!UICONTROL Save]**.

## Kopiera en befintlig gruppuppsättningsförinställning {#copy-bsp}

Du kan kopiera en befintlig gruppuppsättningsförinställning för att undvika att behöva återskapa en komplex förinställning manuellt, eller om du bara vill byta namn på en förinställning. Du kan dock inte ändra den förinställningstyp som används (bilduppsättning eller snurra uppsättning).

Om du kopierar en befintlig förinställning som är en referens från resursmappar påverkas inte dessa mappar.

**Kopiera en befintlig gruppuppsättningsförinställning:**

1. Välj logotypen för Experience Manager och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. På **[!UICONTROL Batch Set Presets]** till vänster om **[!UICONTROL Preset Name]** markerar du kryssrutan för den gruppuppsättningsförinställning som du vill kopiera.
1. Välj **[!UICONTROL Copy]**.
1. I **[!UICONTROL Copy Batch Set Preset]** i **[!UICONTROL Title]** skriver du ett nytt namn för förinställningen.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Välj **[!UICONTROL Copy]**.

## Om att ta bort förinställningar för gruppuppsättningar från mappar {#remove-bsp-from-folder}

När du tar bort förinställningar för gruppuppsättningar från mappar tillämpas inte förinställningen för gruppuppsättningar på nya resurser som du överför till dessa mappar. Befintliga resurser i mappen som redan har lagts till i bilduppsättningen eller som har angetts i gruppuppsättningen baserat på den förinställning som användes i mappen fortsätter att visas som de är.

Om du vill *delete* förinställningar från mappar i stället, se [Ta bort förinställningar för gruppuppsättning](#delete-bsp).

Det finns två metoder som du kan använda för att ta bort gruppuppsättningsförinställningar från mappar.

* [Ta bort gruppuppsättningsförinställningar från mappar via sidan Gruppuppsättningsförinställning](#remove-bsp-from-folders-via-bsp-page) - Den här metoden ger dig den flexibilitet du behöver. Du kan ta bort en eller flera förinställningar från en eller flera mappar.
* [Ta bort gruppuppsättningsförinställningar från en mapps egenskapssida](#remove-bsp-from-folders-via-properties) - Med den här metoden kan du bara ta bort en eller flera gruppuppsättningsförinställningar från en enda mapp.

### Ta bort gruppuppsättningsförinställningar från mappar via sidan Gruppuppsättningsförinställning {#remove-bsp-from-folders-via-bsp-page}

1. Välj logotypen för Experience Manager och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. På **[!UICONTROL Batch Set Presets]** till vänster om **[!UICONTROL Preset Name]** markerar du kryssrutan för en eller flera gruppuppsättningsförinställningar som du vill ta bort från en eller flera mappar.
1. Välj **[!UICONTROL Remove Batch Preset from Folders]**.

1. På **[!UICONTROL Select Folders]** väljer du en eller flera mappar där du vill ta bort förinställningarna för gruppuppsättningar.
1. I det övre högra hörnet av **[!UICONTROL Select Folders]** sida, markera **[!UICONTROL Remove]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. I **[!UICONTROL Remove profile]** väljer **[!UICONTROL Remove]**.

### Ta bort gruppuppsättningsförinställningar från en mapps egenskapssida {#remove-bsp-from-folders-via-properties}

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navigera till en mapp där du vill ta bort en eller flera gruppuppsättningsförinställningar.
1. På sidan, till vänster om **[!UICONTROL Name]** markerar du kryssrutan för en mapp.
1. Välj **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Dynamic Media Processing]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. Under **[!UICONTROL Batch Set Presets]**, markera **[!UICONTROL X]** till höger om förinställningstypen.

1. I det övre högra hörnet på sidan väljer du **[!UICONTROL Save & Close]**.

## Ta bort förinställningar för gruppuppsättning {#delete-bsp}

Du kan ta bort gruppuppsättningsförinställningar för att ta bort dem permanent från [!DNL Dynamic Media]. De syns alltså inte längre på [!UICONTROL Batch Set Preset] eller visas de på **[!UICONTROL Batch Set Presets]** nedrullningsbar lista med **[!UICONTROL Dynamic Media Processing]** på mappens **[!UICONTROL Properties]** sida. Därför används inte förinställningen på befintliga resurser vid mappombearbetningar eller när nya resurser överförs till mappen.

Om du tar bort en förinställning som tidigare har tillämpats på en eller flera mappar kommer alla bilduppsättningar och snurruppsättningar som har skapats från resurser i de mapparna att visas som de är.

Om du vill *ta bort* förinställningar från mappar i stället, se [Ta bort gruppuppsättningsförinställningar från mappar](#remove-bsp-from-folder).

**Så här tar du bort gruppuppsättningsförinställningar:**

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. På **[!UICONTROL Batch Set Presets]** till vänster om **[!UICONTROL Preset Name]** markerar du kryssrutan för en eller flera gruppuppsättningsförinställningar som du vill ta bort.
1. Välj **[!UICONTROL Delete Batch Set Presets]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. I **[!UICONTROL Delete Batch Set Presets]** väljer **[!UICONTROL Delete]**.

   Om en resursmapp refererar till den förinställning du vill ta bort väljer du **[!UICONTROL Force Delete]** i stället.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Bilduppsättningar](/help/assets/dynamic-media/image-sets.md)
>* [Snurrande uppsättningar](/help/assets/dynamic-media/spin-sets.md)
>* [Konfigurera selektiv publicering på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) - Se Synkroniseringsläge i avsnittet om du vill veta mer om hur du synkroniserar en enskild mapp till [!DNL Dynamic Media].
>* [Skapa en Dynamic Media-konfiguration i Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) - Se&quot;Dynamic Media synkroniseringsläge&quot; i avsnittet om du vill veta mer om hur du synkroniserar alla mappar till [!DNL Dynamic Media].

