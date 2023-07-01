---
title: Konfigurera Live Copy-synkronisering
description: Läs om de kraftfulla synkroniseringsalternativen för Live Copy och hur du kan konfigurera och anpassa dem efter dina projektbehov.
feature: Multi Site Manager
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '2335'
ht-degree: 0%

---

# Konfigurera Live Copy-synkronisering {#configuring-live-copy-synchronization}

Adobe Experience Manager har ett antal färdiga synkroniseringskonfigurationer. Innan du använder Live-kopior bör du överväga följande för att definiera hur och när Live-kopior ska synkroniseras med sitt källinnehåll.

1. Bestäm om befintliga utrullningskonfigurationer uppfyller dina krav
1. Om befintliga utrullningskonfigurationer inte gör det, bestämmer du om du behöver skapa en egen.
1. Ange de utrullningskonfigurationer som ska användas för dina Live-kopior.

## Installerade och anpassade utrullningskonfigurationer {#installed-and-custom-rollout-configurations}

I det här avsnittet finns information om de installerade rollout-konfigurationerna och de synkroniseringsåtgärder som de använder samt hur du skapar anpassade konfigurationer om det behövs.

>[!CAUTION]
>
>Uppdatering eller ändring av en färdig driftsättningskonfiguration är **not** rekommenderas. Om det finns ett krav på en anpassad live-åtgärd bör den läggas till i en anpassad rollout-konfiguration.

### Utlösare för utrullning {#rollout-triggers}

Varje utrullningskonfiguration använder en utlösare som gör att utrullningen sker. Utrullningskonfigurationer kan använda någon av följande utlösare:

* **Vid utrullning**: The **Utrullning** -kommandot används på den blå utskriftssidan, eller **Synkronisera** kommandot används på sidan Live Copy.
* **Vid ändring**: Källsidan ändras.
* **Vid aktivering**: Källsidan aktiveras.
* **Vid inaktivering**: Källsidan är inaktiverad.

>[!NOTE]
>
>Användning av **Vid ändring** -utlösaren kan påverka prestanda. Se [Bästa praxis för MSM](best-practices.md#onmodify) för mer information.

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
| Skjut vid ändring | Flyttar innehållet till Live-kopian när källan ändras<br>Använd den här utrullningskonfigurationen sparsamt när den använder utlösaren Vid ändring. | Vid ändring | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| Skjut på ändring (grund) | Flyttar innehåll till Live Copy när sidan med utkast ändras, utan att referenser uppdateras (t.ex. för ytliga kopior)<br>Använd den här utrullningskonfigurationen sparsamt när den använder utlösaren Vid ändring. | Vid ändring | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| Promote Launch | Standardutrullningskonfiguration för att marknadsföra startsidor. | Vid utrullning | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### Synkroniseringsåtgärder {#synchronization-actions}

I följande tabell visas de synkroniseringsåtgärder som medföljer AEM.

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| Åtgärdsnamn | Beskrivning | Egenskaper |
|---|---|---|
| `contentCopy` | När det inte finns några noder i källan i Live Copy kopieras noderna till Live Copy. [Konfigurera **CQ MSM Content Copy-åtgärd** service](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `contentDelete` | Den här åtgärden tar bort noder i Live-kopian som inte finns i källan. [Konfigurera **CQ MSM Content Delete Action** service](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `contentUpdate` | Den här åtgärden uppdaterar Live Copy-innehållet med ändringarna från källan. [Konfigurera **CQ MSM Content Update Action** service](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `editProperties` | Den här åtgärden redigerar egenskaper för Live-kopian. The `editMap` egenskapen avgör vilka egenskaper som redigeras och deras värde. Värdet för `editMap` -egenskapen måste ha följande format:<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` och `new_value` är reguljära uttryck och `n` är ett stegvis heltal.<br>Tänk dig följande värde för `editMap`:<br>`sling:resourceType#/(contentpage`○`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>Det här värdet redigerar egenskaperna för Live Copy-noderna enligt följande:<br>The `sling:resourceType` egenskaper som är inställda på `contentpage` eller till `homepage` är inställda på `mobilecontentpage`.<br>The `cq:template` egenskaper som är inställda på `contentpage` är inställda på `mobilecontentpage`. | `editMap: (String)` identifierar egenskapen, det aktuella värdet och det nya värdet. Mer information finns i beskrivningen. |
| `notify` | Den här åtgärden skickar en sidhändelse om att sidan har rullats ut. För att kunna meddelas måste man först prenumerera på utrullningshändelser. |  |
| `orderChildren` | Den här åtgärden ordnar de underordnade noderna baserat på ordningen i ritningen. |  |
| `referencesUpdate` | Den här synkroniseringsåtgärden uppdaterar referenser på Live-kopian.<br>Söker efter sökvägar på Live Copy-sidorna som pekar på en resurs i planen. När den hittas uppdateras sökvägen till den relaterade resursen i Live Copy. Referenser som har mål utanför planen ändras inte. <br>[Konfigurera **Uppdateringsåtgärd för CQ MSM-referenser** service](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas. |  |
| `targetVersion` | Den här åtgärden skapar en version av Live-kopian.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `targetActivate` | Den här åtgärden aktiverar Live-kopian.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `targetDeactivate` | Den här åtgärden inaktiverar Live Copy.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. |  |
| `workflow` | Den här åtgärden startar arbetsflödet som definieras av egenskapen target (endast för sidor) och tar Live Copy som nyttolast.<br>Målsökvägen är modellnodens sökväg. | `target: (String)` är sökvägen till arbetsflödesmodellen. |
| `mandatory` | Den här åtgärden anger behörigheten för flera åtkomstkontrollistor på sidan Live-kopia till skrivskyddad för en viss användargrupp. Följande åtkomstkontrollistor är konfigurerade:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Använd den här åtgärden endast för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `mandatoryContent` | Den här åtgärden anger behörigheten för flera åtkomstkontrollistor på sidan Live-kopia till skrivskyddad för en viss användargrupp. Följande åtkomstkontrollistor är konfigurerade:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Använd den här åtgärden endast för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `mandatoryStructure` | Den här åtgärden anger behörighet för `ActionSet.ACTION_NAME_REMOVE` ACL på Live Copy-sidan som ska vara skrivskyddad för en viss användargrupp.<br>Använd den här åtgärden endast för sidor. | `target: (String)` är ID:t för gruppen som du anger behörigheter för. |
| `VersionCopyAction` | Om planen/källsidan har publicerats minst en gång skapas en Live Copy-sida med den publicerade versionen. Obs! den här åtgärden är endast tillgänglig för att skapa en Live Copy-sida baserad på en publicerad källsida, inte för att uppdatera en befintlig Live Copy-sida. |  |
| `PageMoveAction` | The `PageMoveAction` används när en sida har flyttats i utkastet.<br>Åtgärden kopierar i stället för att flytta (relaterad) Live Copy-sidan från platsen före flytten till platsen efter.<br>The `PageMoveAction` ändrar inte Live Copy-sidan på platsen före flyttningen. Därför har den status som aktiv relation utan en plan för efterföljande utrullningskonfigurationer.<br>[Konfigurera **CQ MSM Sidflyttningsåtgärd** service](#excluding-properties-and-node-types-from-synchronization) för att ange vilka nodtyper, styckeobjekt och sidegenskaper som ska uteslutas.<br>Den här åtgärden måste vara den enda synkroniseringsåtgärden som ingår i en utrullningskonfiguration. | Ange `prop_referenceUpdate: (Boolean)` till true (standard) för att uppdatera referenser. |
| `markLiveRelationship` | Den här åtgärden anger att det finns en aktiv relation för startskapat innehåll. |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### Exkludera egenskaper och nodtyper från synkronisering {#excluding-properties-and-node-types-from-synchronization}

Du kan konfigurera flera OSGi-tjänster som stöder motsvarande synkroniseringsåtgärder så att de inte påverkar specifika nodtyper och egenskaper. Många egenskaper och delnoder som hör till AEM interna funktion bör till exempel inte tas med i en Live-kopia. Endast det innehåll som är relevant för sidans användare ska kopieras.

När du arbetar med AEM finns det flera sätt att hantera konfigurationsinställningarna för sådana tjänster. Se [Konfigurerar OSGi](/help/implementing/deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

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
| Ignorerade Mixin NodeTypes | `cq.wcm.msm.action.ignoredMixin` | Ett reguljärt uttryck som matchar namnen på de mixin-nodtyper som ska uteslutas från synkroniseringsåtgärden (endast tillgängligt för `contentUpdate` åtgärd) |

#### CQ MSM Content Update Action - Exclusions {#cq-msm-content-update-action-exclusions}

Flera egenskaper och nodtyper exkluderas som standard, de definieras i OSGi-konfigurationen av **CQ MSM Content Update Action**, under **Uteslutna sidegenskaper**.

Som standard är egenskaper som matchar följande reguljära uttryck exkluderade (d.v.s. inte uppdaterade) vid utrullning:

![Exkluderingsregler för Live Copy](../assets/live-copy-exclude.png)

Du kan ändra uttrycken som definierar exkluderingslistan efter behov.

Om du till exempel vill ha sidan **Titel** som ska ingå i de ändringar som övervägs för utrullning, ta bort `jcr:title` från undantagen. Med regex:

`jcr:(?!(title)$).*`

### Konfigurerar synkronisering för uppdatering av referenser {#configuring-synchronization-for-updating-references}

Du kan konfigurera flera OSGi-tjänster som stöder motsvarande synkroniseringsåtgärder som är relaterade till uppdatering av referenser.

När du arbetar med AEM finns det flera sätt att hantera konfigurationsinställningarna för sådana tjänster. Se [Konfigurerar OSGi](/help/implementing/deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

I följande tabell visas de synkroniseringsåtgärder som du kan ange referensuppdatering för. Tabellen innehåller namnen på tjänsterna som ska konfigureras med webbkonsolen och PID:t för konfigurering med en databasnod.

| Webbkonsolegenskap | OSGi-egenskap | Beskrivning |
|---|---|---|
| Uppdatera referens i kapslade LiveCopies | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | Välj det här alternativet i webbkonsolen eller ställ in den här booleska egenskapen på `true` använder databaskonfigurationen för att ersätta referenser som är avsedda för en resurs som finns i grenen i den översta Live Copy-kopian. Endast tillgängligt för `referencesUpdate` åtgärd. |
| Uppdatera referenssidor | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | Välj det här alternativet i webbkonsolen eller ställ in den här booleska egenskapen på `true` använder databaskonfigurationen för att uppdatera referenser till att använda originalsidan för att i stället referera till Live Copy-sidan. Endast tillgängligt för `PageMoveAction`. |

## Ange vilka utrullningskonfigurationer som ska användas {#specifying-the-rollout-configurations-to-use}

Med MSM kan du ange uppsättningar av utrullningskonfigurationer som används generellt, och när det behövs kan du åsidosätta dem för specifika Live-kopior. MSM erbjuder flera platser för att ange vilka rollout-konfigurationer som ska användas. Platsen avgör om konfigurationen gäller för en viss Live-kopia.

I följande lista över platser där du kan ange vilka rollout-konfigurationer som ska användas beskrivs hur MSM avgör vilka rollout-konfigurationer som ska användas för en Live-kopia:

* **[Egenskaper för Live Copy-sida](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** När en Live Copy-sida är konfigurerad att använda en eller flera utrullningskonfigurationer, använder MSM dessa utrullningskonfigurationer.
* **[Egenskaper för designsida](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** När en Live Copy baseras på en plan och Live Copy-sidan inte är konfigurerad med en utrullningskonfiguration, används den utrullningskonfiguration som är associerad med den plana källsidan.
* **Egenskaper för överordnad sida i Live Copy:** När varken Live Copy-sidan eller den blå källsidan har konfigurerats med en utrullningskonfiguration, används den utrullningskonfiguration som gäller för Live Copy-sidans överordnade sida.
* **[Systemstandard](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** När det inte går att fastställa utrullningskonfigurationen för Live Copy-filens överordnade sida, används systemets standardkonfiguration.

En ritning använder till exempel [WKND, genomgång](/help/implementing/developing/introduction/develop-wknd-tutorial.md) -plats som källinnehåll. En webbplats skapas utifrån planen. Varje post i följande lista beskriver olika scenarier för användning av utrullningskonfigurationer:

* Ingen av ritningssidorna eller Live Copy-sidorna är konfigurerade att använda en utrullningskonfiguration. MSM använder systemets standardkonfiguration för utrullning av alla Live Copy-sidor.
* WKND-platsens rotsida är konfigurerad med flera utrullningskonfigurationer. MSM använder dessa utrullningskonfigurationer för alla Live Copy-sidor.
* Rotsidan för WKND-webbplatsen är konfigurerad med flera rollout-konfigurationer och rotsidan för Live Copy-webbplatsen är konfigurerad med en annan uppsättning rollout-konfigurationer. MSM använder de utrullningskonfigurationer som är konfigurerade på Live Copy-webbplatsens rotsida.

### Ange utrullningskonfigurationer för en Live Copy-sida {#setting-the-rollout-configurations-for-a-live-copy-page}

Konfigurera en Live Copy-sida med de utrullningskonfigurationer som ska användas när källsidan rullas ut. Underordnade sidor ärver konfigurationen som standard. När du konfigurerar utrullningskonfigurationen att använda åsidosätter du konfigurationen som Live Copy-sidan ärver från sin överordnade sida.

Du kan också konfigurera utrullningskonfigurationerna för en Live Copy-sida när du [skapa Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page).

1. Använd **Webbplatser** för att välja Live Copy-sidan.
1. Välj **Egenskaper** i verktygsfältet.
1. Öppna **Live Copy** -fliken.

   The **Konfiguration** visas de utrullningskonfigurationer som sidan ärver.

   ![Live Copy-arv från överordnad sida](../assets/live-copy-inherit.png)

1. Justera **Live Copy-arv** flagga. Om du markerar det här alternativet gäller Live Copy-konfigurationen alla underordnade.

1. Rensa **Ärv utrullningskonfiguration från överordnad** väljer du sedan en eller flera utrullningskonfigurationer i listan.

   De valda rollout-konfigurationerna visas under listrutan.

   ![Åsidosätter Live Copy-konfigurationsarv](../assets/live-copy-inherit-override.png)

1. Klicka eller tryck **Spara och stäng**.

### Ställa in utrullningskonfiguration för en blåtryckssida {#setting-the-rollout-configuration-for-a-blueprint-page}

Konfigurera en ritningssida med de utrullningskonfigurationer som ska användas när ritningssidan rullas ut.

Observera att de underordnade sidorna för den blå sidan ärver konfigurationen. När du konfigurerar utrullningskonfigurationen att använda kan du åsidosätta konfigurationen som sidan ärver från sin överordnade.

1. Använd **Webbplatser** för att välja rotsidan för ritningen.
1. Välj **Egenskaper** i verktygsfältet.
1. Öppna **Blueprint** -fliken.
1. Markera en eller flera **Konfigurationer för utrullning** med hjälp av den nedrullningsbara väljaren.
1. Behåll uppdateringarna med **Spara**.

### Ange systemets standardkonfiguration för utrullning {#setting-the-system-default-rollout-configuration}

Konfigurera följande OSGi-tjänst om du vill ange en utrullningskonfiguration som ska användas som systemstandard.

* **Day CQ WCM Live Relationship Manager** med tjänst-PID `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Konfigurera tjänsten med hjälp av [webbkonsol](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller en [databasnod](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* I webbkonsolen är namnet på egenskapen som ska konfigureras **Standardkonfiguration för utrullning**.
* Med en databasnod är namnet på egenskapen som ska konfigureras `liverelationshipmgr.relationsconfig.default`.

Ange det här egenskapsvärdet som sökvägen till den utrullningskonfiguration som ska användas som systemstandard. Standardvärdet är `/libs/msm/wcm/rolloutconfigs/default`, vilket är **Standardkonfiguration för utrullning**.
