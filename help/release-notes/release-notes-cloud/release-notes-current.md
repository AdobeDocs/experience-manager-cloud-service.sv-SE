---
title: Versionsinformation för 2020.8.0-utgåvan [!DNL Adobe Experience Manager] av en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service versionsinformation för 2020.8.0.'
translation-type: tm+mt
source-git-commit: 7f089e15deff87706e0ed3c38630b52832b277d4
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 1%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service 2020.8.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.8.0.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.8.0 är 6 augusti 2020.

### What&#39;s New {#what-is-new-cloud-manager}

* Content Audit är en funktion som är aktiverad i produktionspipelines för Cloud Manager Sites. Konfigurationen av produktionspipeline för program med platser kommer nu att innehålla en tredje flik med namnet&quot;Content Audit&quot; (Innehållsgranskning). När en produktionsprocess körs inkluderas ett nytt steg för innehållsgranskning i pipeline efter en anpassad funktionstestning som utvärderar webbplatsen mot ett antal dimensioner, inklusive prestanda, SEO (sökmotoroptimering), tillgänglighet, bästa praxis och PWA (Progressiv Web App). Miljösidan har omarbetats.

* Nyligen skapade miljöer i Assets-program konfigureras nu automatiskt med Smart Content Services.

* Vilolägen miljöer kan tas bort från viloläget via översiktssidan för Cloud Manager.

* Stöd finns nu för autentiseringsbundna privata Maven-databaser.

### Bug Fixes {#bug-fixes-cm}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Körningar av rörledningar kommer ibland att fastna på grund av interna kommunikationsproblem.

* När en ny organisation etablerades fick vissa användare med andra administrativa roller än systemadministratörer felaktigt åtkomst till Cloud Manager.

* Under vissa förhållanden startades uppdateringsindexjobbet flera gånger parallellt, vilket resulterade i ett distributionsfel.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Användargränssnittet tillät felaktigt försök att utföra åtgärder i en miljö medan det togs bort.

* Översiktssidan innehöll en färgmatchning.

### Kända fel {#known-issues}

* Ogiltiga sidor inkluderas för att få medelpoängen för innehållsgranskning under vad de ska vara.

* På fliken Innehållsgranskning visas bas-URL:en felaktigt med författardomänen i stället för publiceringsdomänen.

* För att aktivera steget Innehållsgranskning måste användarna redigera pipeline och, om så önskas, lägga till sidor. Om inga sidor läggs till granskas hemsidan.

