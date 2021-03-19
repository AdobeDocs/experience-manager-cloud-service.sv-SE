---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.8.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.8.0
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.8.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.8.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.8.0 är 6 augusti 2020.

## Nyheter {#whats-new-cloud-manager}

* Content Audit är en funktion som är aktiverad i produktionsstegen för Cloud Manager Sites. Konfigurationen av produktionspipeline för program med platser innehåller nu en tredje flik med namnet **Content Audit**. När en produktionsprocess körs inkluderas ett nytt Content Audit-steg i produktionsflödet efter anpassad funktionstestning som utvärderar webbplatsen mot ett antal dimensioner, inklusive prestanda, SEO (sökmotoroptimering), tillgänglighet, bästa praxis och PWA (Progressive Web App).


   >[!NOTE]
   >Namnet på Content Audit har ändrats till Experience Audit.

   Mer information finns i [Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md).

* Nyligen skapade miljöer i Assets-program konfigureras nu automatiskt med Smart Content Services.

* Vilolägda miljöer kan tas bort från viloläget på sidan **Översikt** i Cloud Manager.

* Möjlighet att utföra Experience Checks på sidor med Google Lighthuse som bas. Som en del av molnhanterarens pipeline kan upp till 25 sidor kontrolleras och valideras mot upplevelsenyckeltal, och poängen visas i användargränssnittet för molnhanteraren.

### Felkorrigeringar {#bug-fixes-cm}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Pipeline-körningar får ibland *fastna* på grund av interna kommunikationsproblem.

* När en ny organisation etablerades fick vissa användare med andra administrativa roller än systemadministratörer felaktigt åtkomst till Cloud Manager.

* Under vissa förhållanden startades uppdateringsindexjobbet flera gånger parallellt, vilket resulterade i ett distributionsfel.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Användargränssnittet tillät felaktigt försök att utföra åtgärder i en miljö medan det togs bort.

* Det fanns ett färgmatchningsfel på sidan **Översikt** i Cloud Manager.

### Kända fel {#known-issues-cm}

* Ogiltiga sidor inkluderas för att få medelpoängen för innehållsgranskning under vad de ska vara.

* På fliken Innehållsgranskning visas bas-URL:en felaktigt med författardomänen i stället för publiceringsdomänen.

* För att aktivera steget Innehållsgranskning måste användarna redigera pipeline och, om så önskas, lägga till sidor. Om inga sidor läggs till granskas hemsidan.