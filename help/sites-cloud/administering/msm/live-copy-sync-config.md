---
title: Konfigurera Live Copy-synkronisering
description: Läs om de kraftfulla synkroniseringsalternativen för Live Copy och hur du kan konfigurera och anpassa dem efter dina projektbehov.
feature: Multi Site Manager
role: Administrator
translation-type: tm+mt
source-git-commit: fff94f476124d8a2a84c60c478fef624090192d1
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 0%

---


# Konfigurerar Live Copy-synkronisering {#configuring-live-copy-synchronization}

Adobe Experience Manager har ett antal färdiga synkroniseringskonfigurationer. Innan du använder Live-kopior bör du överväga följande för att definiera hur och när Live-kopior ska synkroniseras med sitt källinnehåll.

1. Bestäm om befintliga utrullningskonfigurationer uppfyller dina krav
1. Om befintliga utrullningskonfigurationer inte gör det, bestämmer du om du behöver skapa en egen.
1. Ange de utrullningskonfigurationer som ska användas för dina Live-kopior.

## Installerade och anpassade utrullningskonfigurationer {#installed-and-custom-rollout-configurations}

I det här avsnittet finns information om de installerade rollout-konfigurationerna och de synkroniseringsåtgärder som de använder samt hur du skapar anpassade konfigurationer om det behövs.

>[!CAUTION]
>
>Uppdatering eller ändring av en körklar utrullningskonfiguration är **inte** rekommenderas. Om det finns ett krav på en anpassad live-åtgärd bör den läggas till i en anpassad rollout-konfiguration.

### Utlösare för utrullning {#rollout-triggers}

Varje utrullningskonfiguration använder en utlösare som gör att utrullningen sker. Utrullningskonfigurationer kan använda någon av följande utlösare:

* **Vid utrullning**: Kommandot  **** Rolloutanvänds på den blå utskriftssidan eller så används kommandot  **** Synkronisera på sidan Live-kopia.
* **Vid ändring**: Källsidan ändras.
* **Vid aktivering**: Källsidan aktiveras.
* **Vid inaktivering**: Källsidan är inaktiverad.

>[!NOTE]
>
>Användning av **On Modification**-utlösaren kan påverka prestandan. Mer information finns i [MSM best practices](best-practices.md#onmodify).

### Konfigurationer för utrullning {#rollout-configurations}

I följande tabell visas de utrullningskonfigurationer som medföljer AEM. Tabellen innehåller utlösar- och synkroniseringsåtgärderna för varje utrullningskonfiguration.

<!--
If the installed rollout configuration actions do not meet your requirements, you can [create a new rollout configuration](#creating-a-rollout-configuration).
-->

| Namn | Beskrivning | Utlösare | [Synkroniseringsåtgärder](#synchronization-actions) |
|---|---|---|---|
| Standardkonfiguration för utrullning | Standardkonfiguration för utrullning som gör det möjligt att starta en process vid utlösare för utrullning och kör åtgärder: skapa, uppdatera, ta bort innehåll och beställa underordnade noder | Vid utrullning | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| Aktivera vid aktivering av utkast | Publicerar Live-kopian när källan publiceras | Vid aktivering | `targetActivate` |
| Inaktivera vid inaktivering av utkast | Inaktiverar Live-kopian när källan inaktiveras | Vid inaktivering | `targetDeactivate` |
| Skjut vid ändring | Flyttar innehållet till Live Copy när källan ändras<br>Använd den här rollout-konfigurationen sparsamt när den använder On Modification-utlösaren. | Vid ändring | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| Skjut på ändring (grund) | Flyttar innehåll till Live Copy när ritningssidan ändras, utan att uppdatera referenser (t.ex. för grund kopior)<br>Använd den här utrullningskonfigurationen sparsamt när den använder utlösaren Vid ändring. | Vid ändring | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| Promote Launch | Standardutrullningskonfiguration för att marknadsföra startsidor. | Vid utrullning | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### Synkroniseringsåtgärder {#synchronization-actions}

I följande tabell visas de synkroniseringsåtgärder som medföljer AEM.

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| Åtgärdsnamn | Beskrivning | Egenskaper |
|---|---|---|
| `contentCopy` | När det inte finns några noder i källan i Live Copy kopieras noderna till Live Copy. [Konfigurera  **CQ MSM Content Copy** ](#excluding-properties-and-node-types-from-synchronization) Action Services för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `contentDelete` | Den här åtgärden tar bort noder i Live-kopian som inte finns i källan. [Konfigurera  **CQ MSM Content Delete** ](#excluding-properties-and-node-types-from-synchronization) Action Services för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `contentUpdate` | Den här åtgärden uppdaterar Live Copy-innehållet med ändringarna från källan. [Konfigurera  **CQ MSM Content Update** ](#excluding-properties-and-node-types-from-synchronization) Action Services för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `editProperties` | Den här åtgärden redigerar egenskaper för Live-kopian. Egenskapen `editMap` avgör vilka egenskaper som redigeras och deras värde. Värdet för egenskapen `editMap` måste ha följande format:<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` och `new_value` är reguljära uttryck och `n` är ett stegvis heltal.<br>Tänk dig följande värde för  `editMap`:<br>`sling:resourceType#/(contentpage` ‖ `homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>Det här värdet redigerar egenskaperna för Live Copy-noderna enligt följande:<br>De  `sling:resourceType` egenskaper som antingen är inställda på  `contentpage` eller  `homepage` är inställda på  `mobilecontentpage`.<br>De  `cq:template` egenskaper som är inställda på  `contentpage` ställs in på  `mobilecontentpage`. | `editMap: (String)` identifierar egenskapen, det aktuella värdet och det nya värdet. Mer information finns i beskrivningen. |
| `notify` | Den här åtgärden skickar en sidhändelse om att sidan har rullats ut. För att kunna meddelas måste du först prenumerera på utrullningshändelser. |  |
| `orderChildren` | Den här åtgärden ordnar de underordnade noderna baserat på ordningen i ritningen. |  |
| `referencesUpdate` | Den här synkroniseringsåtgärden uppdaterar referenser på Live-kopian.<br>Söker efter sökvägar på Live Copy-sidorna som pekar på en resurs i planen. När den hittas uppdateras sökvägen till den relaterade resursen i Live Copy. Referenser som har mål utanför planen ändras inte. <br>[Konfigurera  **CQ MSM Reference Update** ](#excluding-properties-and-node-types-from-synchronization) Action Services för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `targetVersion` | Den här åtgärden skapar en version av Live-kopian.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `targetActivate` | Den här åtgärden aktiverar Live-kopian.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `targetDeactivate` | Den här åtgärden inaktiverar Live Copy.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `workflow` | Den här åtgärden startar arbetsflödet som definieras av egenskapen target (endast för sidor) och tar Live Copy som nyttolast.<br>Målsökvägen är modellnodens sökväg. | `target: (String)` är sökvägen till arbetsflödesmodellen. |
| `mandatory` | Den här åtgärden anger behörigheten för flera åtkomstkontrollistor på sidan Live-kopia till skrivskyddad för en viss användargrupp. Följande ACL:er är konfigurerade:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Använd endast den här åtgärden för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `mandatoryContent` | Den här åtgärden anger behörigheten för flera åtkomstkontrollistor på sidan Live-kopia till skrivskyddad för en viss användargrupp. Följande ACL:er är konfigurerade:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Använd endast den här åtgärden för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `mandatoryStructure` | Den här åtgärden ställer in behörigheten för åtkomstkontrollistan `ActionSet.ACTION_NAME_REMOVE` på sidan Live Copy till skrivskyddad för en viss användargrupp.<br>Använd den här åtgärden endast för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `VersionCopyAction` | Om planen/källsidan har publicerats minst en gång skapas en Live Copy-sida med den publicerade versionen. Obs! den här åtgärden är endast tillgänglig för att skapa en Live Copy-sida baserad på en publicerad källsida, inte för att uppdatera en befintlig Live Copy-sida. |  |
| `PageMoveAction` | `PageMoveAction` gäller när en sida har flyttats i ritningen.<br>Åtgärden kopierar i stället för att flytta (relaterad) Live Copy-sidan från platsen före flytten till platsen efter.<br>Sidan Live Copy ändras  `PageMoveAction` inte på platsen före flyttningen. Därför har den status som aktiv relation utan en plan för efterföljande utrullningskonfigurationer.<br>[Konfigurera  **CQ MSM Page Move** ](#excluding-properties-and-node-types-from-synchronization) Action Services för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. | Ange `prop_referenceUpdate: (Boolean)` till true (standard) om du vill uppdatera referenser. |
| `markLiveRelationship` | Den här åtgärden anger att det finns en aktiv relation för startskapat innehåll. |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### Exkluderar egenskaper och nodtyper från synkronisering {#excluding-properties-and-node-types-from-synchronization}

Du kan konfigurera flera OSGi-tjänster som stöder motsvarande synkroniseringsåtgärder så att de inte påverkar specifika nodtyper och egenskaper. Många egenskaper och delnoder som hör till AEM interna funktion bör till exempel inte tas med i en Live-kopia. Endast det innehåll som är relevant för sidans användare ska kopieras.

När du arbetar med AEM finns det flera sätt att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommenderade tillvägagångssätt finns i [Konfigurera OSGi](/help/implementing/deploying/configuring-osgi.md).

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
| Ignorerade Mixin NodeTypes | `cq.wcm.msm.action.ignoredMixin` | Ett reguljärt uttryck som matchar namnen på de mixin-nodtyper som ska uteslutas från synkroniseringsåtgärden (endast tillgängligt för åtgärden `contentUpdate`) |

#### CQ MSM Content Update Action - Exclusions {#cq-msm-content-update-action-exclusions}

Flera egenskaper och nodtyper exkluderas som standard, de definieras i OSGi-konfigurationen av **CQ MSM Content Update Action**, under **Exkluderade sidegenskaper**.

Som standard är egenskaper som matchar följande reguljära uttryck exkluderade (dvs. inte uppdaterade) vid utrullning:

![Exkluderingsregler för Live Copy](../assets/live-copy-exclude.png)

Du kan ändra uttrycken som definierar exkluderingslistan efter behov.

Om du till exempel vill att sidan **Rubrik** ska inkluderas i ändringarna som gäller för utrullning, tar du bort `jcr:title` från undantagen. Med regex:

`jcr:(?!(title)$).*`

### Konfigurerar synkronisering för uppdatering av referenser {#configuring-synchronization-for-updating-references}

Du kan konfigurera flera OSGi-tjänster som stöder motsvarande synkroniseringsåtgärder som är relaterade till uppdatering av referenser.

När du arbetar med AEM finns det flera sätt att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommenderade tillvägagångssätt finns i [Konfigurera OSGi](/help/implementing/deploying/configuring-osgi.md).

I följande tabell visas de synkroniseringsåtgärder som du kan ange referensuppdatering för. Tabellen innehåller namnen på tjänsterna som ska konfigureras med webbkonsolen och PID:t för konfigurering med en databasnod.

| Webbkonsolegenskap | OSGi-egenskap | Beskrivning |
|---|---|---|
| Uppdatera referens i kapslade LiveCopies | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | Välj det här alternativet i webbkonsolen eller ange den här booleska egenskapen till `true` med hjälp av databaskonfigurationen för att ersätta referenser som är avsedda för resurser som finns i grenen i den översta Live Copy-klienten. Endast tillgängligt för åtgärden `referencesUpdate`. |
| Uppdatera referenssidor | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | Välj det här alternativet i webbkonsolen eller ställ in den här booleska egenskapen på `true` med hjälp av databaskonfigurationen för att uppdatera referenser som använder originalsidan till att i stället referera till Live Copy-sidan. Endast tillgängligt för `PageMoveAction`. |

## Ange vilka utrullningskonfigurationer som ska användas {#specifying-the-rollout-configurations-to-use}

Med MSM kan du ange uppsättningar av utrullningskonfigurationer som används generellt, och när det behövs kan du åsidosätta dem för specifika Live-kopior. MSM erbjuder flera platser för att ange vilka utrullningskonfigurationer som ska användas. Platsen avgör om konfigurationen gäller för en viss Live-kopia.

I följande lista över platser där du kan ange vilka rollout-konfigurationer som ska användas beskrivs hur MSM avgör vilka rollout-konfigurationer som ska användas för en Live-kopia:

* **[Live Copy-sidegenskaper](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** När en Live Copy-sida är konfigurerad att använda en eller flera utrullningskonfigurationer, använder MSM dessa utrullningskonfigurationer.
* **[Egenskaper](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page) för**  designsidor:När en Live-kopia baseras på en ritning och Live-kopia-sidan inte har konfigurerats med en utrullningskonfiguration används den rolloutkonfiguration som är associerad med källsidan för utkast.
* **Egenskaper för den överordnade sidan för Live Copy:** När varken Live Copy-sidan eller den överordnade sidan för utkast har konfigurerats med en utrullningskonfiguration, används den utrullningskonfiguration som gäller för den överordnade sidan för Live Copy-sidan.
* **[Systemstandard](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** När det inte går att fastställa utrullningskonfigurationen för Live Copy:s överordnade sida används systemets standardkonfiguration.

I en plan används till exempel självstudiekursen [WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) som källinnehåll. En webbplats skapas utifrån planen. Varje post i följande lista beskriver olika scenarier för användning av utrullningskonfigurationer:

* Ingen av ritningssidorna eller Live Copy-sidorna är konfigurerade att använda en utrullningskonfiguration. MSM använder systemets standardkonfiguration för utrullning av alla Live Copy-sidor.
* WKND-platsens rotsida är konfigurerad med flera utrullningskonfigurationer. MSM använder dessa utrullningskonfigurationer för alla Live Copy-sidor.
* Rotsidan för WKND-webbplatsen är konfigurerad med flera rollout-konfigurationer och rotsidan för Live Copy-webbplatsen är konfigurerad med en annan uppsättning rollout-konfigurationer. MSM använder de utrullningskonfigurationer som är konfigurerade på Live Copy-webbplatsens rotsida.

### Ange utrullningskonfigurationer för en Live Copy-sida {#setting-the-rollout-configurations-for-a-live-copy-page}

Konfigurera en Live Copy-sida med de utrullningskonfigurationer som ska användas när källsidan rullas ut. Underordnade sidor ärver konfigurationen som standard. När du konfigurerar utrullningskonfigurationen att använda åsidosätter du konfigurationen som Live Copy-sidan ärver från sin överordnade sida.

Du kan också konfigurera utrullningskonfigurationerna för en Live Copy-sida när du [skapar Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page).

1. Använd konsolen **Platser** för att välja sidan Live-kopia.
1. Välj **Egenskaper** i verktygsfältet.
1. Öppna fliken **Live Copy**.

   Avsnittet **Konfiguration** visar de rollout-konfigurationer som sidan ärver.

   ![Live Copy-arv från överordnad sida](../assets/live-copy-inherit.png)

1. Justera flaggan **Live Copy-arv** om det behövs. Om du markerar det här alternativet gäller Live Copy-konfigurationen alla underordnade.

1. Rensa egenskapen **Ärv utrullningskonfiguration från överordnad** och välj sedan en eller flera utrullningskonfigurationer i listan.

   De valda rollout-konfigurationerna visas under listrutan.

   ![Åsidosätter Live Copy-konfigurationsarv](../assets/live-copy-inherit-override.png)

1. Klicka eller tryck på **Spara och stäng**.

### Ställa in utrullningskonfiguration för en blå sida {#setting-the-rollout-configuration-for-a-blueprint-page}

Konfigurera en ritningssida med de utrullningskonfigurationer som ska användas när ritningssidan rullas ut.

Observera att de underordnade sidorna för den blå sidan ärver konfigurationen. När du konfigurerar utrullningskonfigurationen att använda kan du åsidosätta konfigurationen som sidan ärver från sin överordnade.

1. Använd konsolen **Platser** för att välja rotsidan i planen.
1. Välj **Egenskaper** i verktygsfältet.
1. Öppna fliken **Blå**.
1. Välj en eller flera **utrullningskonfigurationer** med den nedrullningsbara väljaren.
1. Behåll uppdateringarna med **Spara**.

### Anger systemets standardkonfiguration för utrullning {#setting-the-system-default-rollout-configuration}

Konfigurera följande OSGi-tjänst om du vill ange en utrullningskonfiguration som ska användas som systemstandard.

* **Day CQ WCM Live Relationship** Manager med tjänst-PID  `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Konfigurera tjänsten med antingen [webbkonsolen](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller en [databasnod](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* I webbkonsolen är namnet på egenskapen som ska konfigureras **Standardrollout config**.
* Med hjälp av en databasnod är namnet på egenskapen som ska konfigureras `liverelationshipmgr.relationsconfig.default`.

Ange det här egenskapsvärdet som sökvägen till den utrullningskonfiguration som ska användas som systemstandard. Standardvärdet är `/libs/msm/wcm/rolloutconfigs/default`, som är **standardkonfigurationen för utrullning**.
