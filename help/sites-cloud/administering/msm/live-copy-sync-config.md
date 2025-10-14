---
title: Konfigurera Live Copy-synkronisering
description: Läs om de kraftfulla synkroniseringsalternativen för Live Copy och hur du kan konfigurera och anpassa dem efter dina projektbehov.
feature: Multi Site Manager
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# Konfigurera Live Copy-synkronisering {#configuring-live-copy-synchronization}

Adobe Experience Manager har flera färdiga synkroniseringskonfigurationer. Innan du använder Live-kopior bör du överväga följande för att definiera hur och när Live-kopior ska synkroniseras med sitt källinnehåll.

1. Bestäm om befintliga utrullningskonfigurationer uppfyller dina krav
1. Om befintliga utrullningskonfigurationer inte gör det, bestämmer du om du behöver skapa en egen.
1. Ange de utrullningskonfigurationer som ska användas för dina Live-kopior.

## Installerade och anpassade utrullningskonfigurationer {#installed-and-custom-rollout-configurations}

I det här avsnittet finns information om de installerade rollout-konfigurationerna och de synkroniseringsåtgärder som de använder samt hur du skapar anpassade konfigurationer om det behövs.

>[!CAUTION]
>
>Uppdatering eller ändring av en körklar utrullningskonfiguration **rekommenderas inte**. Om det finns ett krav på en anpassad live-åtgärd bör den läggas till i en anpassad rollout-konfiguration.

### Utlösare för utrullning {#rollout-triggers}

Varje utrullningskonfiguration använder en utlösare som gör att utrullningen sker. Utrullningskonfigurationer kan använda någon av följande utlösare:

* **Vid utrullning**: Kommandot **Rollout** används på den blå utskriftssidan, eller så används kommandot **Synkronisera** på sidan Live-kopia.
* **Vid ändring**: Källsidan har ändrats.
* **Vid aktivering**: Källsidan är aktiverad.
* **Vid inaktivering**: Källsidan är inaktiverad.

>[!NOTE]
>
>Användning av utlösaren **Vid ändring** kan påverka prestandan. Mer information finns i [Bästa praxis för MSM](best-practices.md#onmodify).

### Utrullningskonfigurationer {#rollout-configurations}

I följande tabell visas de utrullningskonfigurationer som medföljer AEM. Tabellen innehåller utlösar- och synkroniseringsåtgärderna för varje utrullningskonfiguration.

Om de installerade rollout-konfigurationsåtgärderna inte uppfyller dina krav kan du [skapa en rollout-konfiguration](#creating-a-rollout-configuration).

| Namn | Beskrivning | Utlösare | [Synkroniseringsåtgärder](#synchronization-actions) |
|---|---|---|---|
| Standardkonfiguration för utrullning | Standardkonfiguration för utrullning som gör det möjligt att starta en process vid utlösare för utrullning och kör åtgärder: skapa, uppdatera, ta bort innehåll och beställa underordnade noder | Vid utrullning | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| Aktivera vid aktivering av utkast | Publicerar Live-kopian när källan publiceras | Vid aktivering | `targetActivate` |
| Inaktivera vid inaktivering av utkast | Inaktiverar Live-kopian när källan inaktiveras | Vid inaktivering | `targetDeactivate` |
| Skjut vid ändring | Flyttar innehållet till Live Copy när källan ändras<br>Använd den här rollout-konfigurationen sparsamt när den använder On Modification-utlösaren. | Vid ändring | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| Skjut på ändring (grund) | Flyttar innehåll till Live-kopian när ritningssidan ändras, utan att uppdatera referenser (till exempel för ytliga kopior)<br>Använd den här utrullningskonfigurationen sparsamt när den använder utlösaren Vid ändring. | Vid ändring | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| Promote Launch | Standardkonfiguration för lansering av startsidor. | Vid utrullning | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### Synkroniseringsåtgärder {#synchronization-actions}

I följande tabell visas de synkroniseringsåtgärder som medföljer AEM.

Om de installerade åtgärderna inte uppfyller dina krav kan du [skapa en ny synkroniseringsåtgärd](/help/implementing/developing/extending/msm.md#creating-a-new-synchronization-action).

| Åtgärdsnamn | Beskrivning | Egenskaper |
|---|---|---|
| `contentCopy` | När det inte finns några noder i källan i Live Copy kopieras noderna till Live Copy. [Konfigurera **CQ MSM Content Copy Action** &#x200B;](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `contentDelete` | Den här åtgärden tar bort noder i Live-kopian som inte finns i källan. [Konfigurera **CQ MSM Content Delete Action**-tjänsten](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `contentUpdate` | Den här åtgärden uppdaterar Live Copy-innehållet med ändringarna från källan. [Konfigurera **CQ MSM Content Update Action**-tjänsten](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `editProperties` | Den här åtgärden redigerar egenskaper för Live-kopian. Egenskapen `editMap` avgör vilka egenskaper som redigeras och deras värde. Värdet för egenskapen `editMap` måste ha följande format: <br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` och `new_value` är reguljära uttryck och `n` är ett inkrementellt heltal.<br>Tänk dig till exempel följande värde för `editMap`:<br>`sling:resourceType#/(contentpage` ‖`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>Det här värdet redigerar egenskaperna för Live Copy-noderna enligt följande:<br>Egenskaperna `sling:resourceType` som är inställda på `contentpage` eller `homepage` är inställda på `mobilecontentpage`.<br>Egenskaperna `cq:template` som är inställda på `contentpage` är inställda på `mobilecontentpage`. | `editMap: (String)` identifierar egenskapen, det aktuella värdet och det nya värdet. Mer information finns i beskrivningen. |
| `notify` | Den här åtgärden skickar en sidhändelse om att sidan har rullats ut. För att kunna meddelas måste man först prenumerera på utrullningshändelser. |  |
| `orderChildren` | Den här åtgärden ordnar de underordnade noderna baserat på ordningen i ritningen. |  |
| `referencesUpdate` | Den här synkroniseringsåtgärden uppdaterar referenser på Live-kopian.<br>Söker efter sökvägar på Live Copy-sidorna som pekar på en resurs i planen. När den hittas uppdateras sökvägen till den relaterade resursen i Live Copy. Referenser som har mål utanför planen ändras inte. <br>[Konfigurera **CQ MSM References Update Action** service](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `targetVersion` | Den här åtgärden skapar en version av Live-kopian.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `targetActivate` | Den här åtgärden aktiverar Live-kopian.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `targetDeactivate` | Den här åtgärden inaktiverar Live-kopian.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `workflow` | Den här åtgärden startar arbetsflödet som definieras av egenskapen target (endast för sidor) och tar Live Copy som nyttolast.<br>Målsökvägen är sökvägen till modellnoden. | `target: (String)` är sökvägen till arbetsflödesmodellen. |
| `mandatory` | Den här åtgärden anger behörigheten för flera åtkomstkontrollistor på sidan Live-kopia till skrivskyddad för en viss användargrupp. Följande ACL:er är konfigurerade:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Använd endast den här åtgärden för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `mandatoryContent` | Den här åtgärden anger behörigheten för flera åtkomstkontrollistor på sidan Live-kopia till skrivskyddad för en viss användargrupp. Följande ACL:er är konfigurerade:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Använd endast den här åtgärden för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `mandatoryStructure` | Den här åtgärden ställer in behörigheten för `ActionSet.ACTION_NAME_REMOVE` ACL på Live Copy-sidan till skrivskyddad för en viss användargrupp.<br>Använd bara den här åtgärden för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `VersionCopyAction` | Om planen/källsidan har publicerats minst en gång skapas en Live Copy-sida med den publicerade versionen. Obs! Den här åtgärden är endast tillgänglig när du skapar en Live Copy-sida baserad på en publicerad källsida, inte när du uppdaterar en befintlig Live Copy-sida. |  |
| `PageMoveAction` | `PageMoveAction` används när en sida har flyttats i ritningen.<br>Åtgärden kopierar i stället för att flytta den (relaterade) Live Copy-sidan från platsen före flytten till platsen efter.<br>`PageMoveAction` ändrar inte Live Copy-sidan på platsen före flytten. Därför har den status som aktiv relation utan en plan för efterföljande utrullningskonfigurationer.<br>[Konfigurera tjänsten **CQ MSM Page Move Action**](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. | Ange `prop_referenceUpdate: (Boolean)` som true (standard) för att uppdatera referenser. |
| `markLiveRelationship` | Den här åtgärden anger att det finns en aktiv relation för startskapat innehåll. |  |

### Skapa en utrullningskonfiguration {#creating-a-rollout-configuration}

Du kan [skapa en utrullningskonfiguration](/help/implementing/developing/extending/msm.md#creating-a-new-rollout-configuration) när de installerade utrullningskonfigurationerna inte uppfyller dina programkrav genom att utföra följande steg.

1. [Skapa utrullningskonfiguration-](/help/implementing/developing/extending/msm.md#create-the-rollout-configuration)
1. [Lägg till synkroniseringsåtgärder i utrullningskonfigurationen](/help/implementing/developing/extending/msm.md#add-synchronization-actions-to-the-rollout-configuration).

Den nya rollout-konfigurationen är sedan tillgänglig för dig när du konfigurerar rollout-konfigurationer på en plan- eller Live Copy-sida.

### Exkludera egenskaper och nodtyper från synkronisering {#excluding-properties-and-node-types-from-synchronization}

Du kan konfigurera flera OSGi-tjänster som stöder motsvarande synkroniseringsåtgärder så att de inte påverkar specifika nodtyper och egenskaper. Många egenskaper och delnoder som hör till AEM interna funktion bör till exempel inte tas med i en Live-kopia. Endast det innehåll som är relevant för sidans användare ska kopieras.

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Se [Konfigurera OSGi](/help/implementing/deploying/configuring-osgi.md) för mer information och rekommenderade rutiner.

I följande tabell visas de synkroniseringsåtgärder som du kan ange vilka noder som ska uteslutas för. Tabellen innehåller namnen på tjänsterna som ska konfigureras med webbkonsolen och PID:t för konfigurering med en databasnod.

| Synkroniseringsåtgärd | Tjänstnamn i webbkonsolen | Tjänst-PID |
|---|---|---|
| `contentCopy` | CQ MSM Content Copy-åtgärd | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | CQ MSM Content Delete Action | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | CQ MSM Content Update Action | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | CQ MSM Sidflyttningsåtgärd | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | Uppdateringsåtgärd för CQ MSM-referenser | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

I följande tabell beskrivs egenskaperna som du kan konfigurera:

| Webbkonsolegenskap | OSGi-egenskap | Beskrivning |
|---|---|---|
| Exkluderade nodtyper | `cq.wcm.msm.action.excludednodetypes` | Ett reguljärt uttryck som matchar de nodtyper som ska uteslutas från synkroniseringsåtgärden |
| Exkluderade styckeobjekt | `cq.wcm.msm.action.excludedparagraphitems` | Ett reguljärt uttryck som matchar styckeobjekten som ska uteslutas från synkroniseringsåtgärden |
| Uteslutna sidegenskaper | `cq.wcm.msm.action.excludedprops` | Ett reguljärt uttryck som matchar sidegenskaperna som ska uteslutas från synkroniseringsåtgärden |
| Ignorerade Mixin NodeType | `cq.wcm.msm.action.ignoredMixin` | Ett reguljärt uttryck som matchar namnen på de mixin-nodtyper som ska uteslutas från synkroniseringsåtgärden (endast tillgängligt för åtgärden `contentUpdate`) |

#### CQ MSM Content Update Action - Exclusions {#cq-msm-content-update-action-exclusions}

Flera egenskaper och nodtyper exkluderas som standard, de definieras i OSGi-konfigurationen för **CQ MSM Content Update Action** under **Exkluderade sidegenskaper**.

Som standard är egenskaper som matchar följande reguljära uttryck exkluderade (d.v.s. inte uppdaterade) vid utrullning:

![Exkluderingsregler för Live-kopia](../assets/live-copy-exclude.png)

Du kan ändra uttrycken som definierar exkluderingslistan efter behov.

Om du till exempel vill att sidan **Rubrik** ska inkluderas i ändringarna som gäller för utrullning tar du bort `jcr:title` från undantagen. Med regex:

`jcr:(?!(title)$).*`

### Konfigurerar synkronisering för uppdatering av referenser {#configuring-synchronization-for-updating-references}

Du kan konfigurera flera OSGi-tjänster som stöder motsvarande synkroniseringsåtgärder som är relaterade till uppdatering av referenser.

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Se [Konfigurera OSGi](/help/implementing/deploying/configuring-osgi.md) för mer information och rekommenderade rutiner.

I följande tabell visas de synkroniseringsåtgärder som du kan ange referensuppdatering för. Tabellen innehåller namnen på tjänsterna som ska konfigureras med webbkonsolen och PID:t för konfigurering med en databasnod.

| Webbkonsolegenskap | OSGi-egenskap | Beskrivning |
|---|---|---|
| Uppdatera referens i kapslade LiveCopies | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | Välj det här alternativet i webbkonsolen eller ange den här booleska egenskapen till `true` med hjälp av databaskonfigurationen för att ersätta referenser som är avsedda för alla resurser som finns i grenen i den översta Live Copy-klienten. Endast tillgängligt för åtgärden `referencesUpdate`. |
| Uppdatera referenssidor | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | Välj det här alternativet i webbkonsolen eller ange den här booleska egenskapen till `true` med hjälp av databaskonfigurationen för att uppdatera referenser som använder originalsidan till att i stället referera till Live Copy-sidan. Endast tillgängligt för `PageMoveAction`. |

## Ange vilka utrullningskonfigurationer som ska användas {#specifying-the-rollout-configurations-to-use}

Med MSM kan du ange uppsättningar av utrullningskonfigurationer som används generellt, och när det behövs kan du åsidosätta dem för specifika Live-kopior. MSM erbjuder flera platser för att ange vilka utrullningskonfigurationer som ska användas. Platsen avgör om konfigurationen gäller för en viss Live-kopia.

I följande lista över platser där du kan ange vilka rollout-konfigurationer som ska användas beskrivs hur MSM avgör vilka rollout-konfigurationer som ska användas för en Live-kopia:

* **[Live Copy-sidegenskaper](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** När en Live Copy-sida är konfigurerad att använda en eller flera utrullningskonfigurationer, använder MSM dessa rollout-konfigurationer.
* **[Egenskaper för desktopsida](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** När en Live-kopia baseras på en ritning och Live-kopia-sidan inte har konfigurerats med en utrullningskonfiguration, används den rollout-konfiguration som är associerad med den blå källsidan.
* **Egenskaper för den överordnade sidan för Live Copy:** När varken Live Copy-sidan eller den överordnade sidan för utkast har konfigurerats med en utrullningskonfiguration, används den utrullningskonfiguration som gäller för den överordnade sidan för Live Copy-sidan.
* **[Systemstandard](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** När utrullningskonfigurationen för Live Copy:s överordnade sida inte kan bestämmas, används systemets standardkonfiguration för utrullning.

I en plan används till exempel [WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md) som källinnehåll. En webbplats skapas utifrån planen. Varje post i följande lista beskriver olika scenarier för användning av utrullningskonfigurationer:

* Ingen av ritningssidorna eller Live Copy-sidorna är konfigurerade att använda en utrullningskonfiguration. MSM använder systemets standardkonfiguration för utrullning av alla Live Copy-sidor.
* WKND-platsens rotsida är konfigurerad med flera utrullningskonfigurationer. MSM använder dessa rollout-konfigurationer för alla Live Copy-sidor.
* Rotsidan för WKND-webbplatsen är konfigurerad med flera rollout-konfigurationer och rotsidan för Live Copy-webbplatsen är konfigurerad med en annan uppsättning rollout-konfigurationer. MSM använder de utrullningskonfigurationer som är konfigurerade på Live Copy-webbplatsens rotsida.

### Ställa in utrullningskonfigurationer för en Live Copy-sida {#setting-the-rollout-configurations-for-a-live-copy-page}

Konfigurera en Live Copy-sida med de utrullningskonfigurationer som ska användas när källsidan rullas ut. Underordnade sidor ärver konfigurationen som standard. När du konfigurerar utrullningskonfigurationen att använda åsidosätter du konfigurationen som Live Copy-sidan ärver från sin överordnade sida.

Du kan också konfigurera utrullningskonfigurationerna för en Live-kopia-sida när du [skapar Live-kopian](creating-live-copies.md#creating-a-live-copy-of-a-page).

1. Använd konsolen **Webbplatser** för att välja sidan Live-kopia.
1. Välj **Egenskaper** i verktygsfältet.
1. Öppna fliken **Live-kopia**.

   Avsnittet **Konfiguration** visar de utrullningskonfigurationer som sidan ärver.

   ![Live Copy-arv från överordnad sida](../assets/live-copy-inherit.png)

1. Justera flaggan **Live Copy Arv** om det behövs. Om du markerar det här alternativet gäller Live Copy-konfigurationen alla underordnade.

1. Rensa egenskapen **Ärv utrullningskonfiguration från överordnad** och välj sedan en eller flera utrullningskonfigurationer i listan.

   De valda rollout-konfigurationerna visas under listrutan.

   ![Åsidosätter Live Copy-konfigurationsarv](../assets/live-copy-inherit-override.png)

1. Välj **Spara och stäng**.

### Ställa in utrullningskonfiguration för en blåtryckssida {#setting-the-rollout-configuration-for-a-blueprint-page}

Konfigurera en ritningssida med de utrullningskonfigurationer som ska användas när ritningssidan rullas ut.

De underordnade sidorna för ritningssidan ärver konfigurationen. När du konfigurerar utrullningskonfigurationen att använda kan du åsidosätta konfigurationen som sidan ärver från sin överordnade.

1. Använd konsolen **Platser** för att välja rotsidan i planen.
1. Välj **Egenskaper** i verktygsfältet.
1. Öppna fliken **Utskrift**.
1. Välj en eller flera **utrullningskonfigurationer** med den nedrullningsbara väljaren.
1. Behåll uppdateringarna med **Spara**.

### Ställa in systemets standardkonfiguration för utrullning {#setting-the-system-default-rollout-configuration}

Konfigurera följande OSGi-tjänst om du vill ange en utrullningskonfiguration som ska användas som systemstandard.

* **Dag CQ WCM Live Relationship Manager** med tjänst-PID `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Konfigurera tjänsten med [webbkonsolen](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller en [databasnod](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* I webbkonsolen är namnet på den egenskap som ska konfigureras **Standardrollout-konfiguration**.
* Med en databasnod är namnet på egenskapen som ska konfigureras `liverelationshipmgr.relationsconfig.default`.

Ange det här egenskapsvärdet som sökvägen till den utrullningskonfiguration som ska användas som systemstandard. Standardvärdet är `/libs/msm/wcm/rolloutconfigs/default`, som är **standardkonfigurationen för utrullning**.
