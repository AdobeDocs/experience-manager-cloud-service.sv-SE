---
title: Versionsinformation för 2020.8.0-utgåvan [!DNL Adobe Experience Manager] av en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service versionsinformation för 2020.8.0.'
translation-type: tm+mt
source-git-commit: 85f5262c2af7502e98fcb60b51b9b13d2c2c0f2c
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service 2020.8.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.8.0.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### What&#39;s New {#what-is-new-commerce}

* Funktionen produktkonsol är nu tillgänglig. Detta gör att marknadsförare/författare i AEM kan visa och navigera bland kategorier och produkter som lagras i e-handelsservern. Det finns även stöd för egenskaper för kategorier och produkter i produktkonsolen.

* Produkt- och kategoriväljarna har förbättrats så att marknadsförarna kan välja produkt via SKU eller välja kategori via kategori-ID.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.8.0 är 6 augusti 2020.

### What&#39;s New {#what-is-new-cloud-manager}

* Content Audit är en funktion som är aktiverad i produktionsstegen för Cloud Manager Sites. Konfigurationen av produktionspipeline för program med platser innehåller nu en tredje flik med namnet **Content Audit**. När en produktionsprocess körs inkluderas ett nytt Content Audit-steg i produktionsflödet efter anpassad funktionstestning som utvärderar webbplatsen mot ett antal dimensioner, inklusive prestanda, SEO (sökmotoroptimering), tillgänglighet, bästa praxis och PWA (Progressive Web App).

   Refer to [Content Audit Testing](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) for more details.

* Nyligen skapade miljöer i Assets-program konfigureras nu automatiskt med Smart Content Services.

* Vilolägda miljöer kan tas bort från vänteläget på sidan **Översikt** i Cloud Manager.

* Stöd finns nu för autentiseringsbundna privata Maven-databaser.

### Bug Fixes {#bug-fixes-cm}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Körningar av rörledningar *fastnar* ibland på grund av interna kommunikationsproblem.

* När en ny organisation etablerades fick vissa användare med andra administrativa roller än systemadministratörer felaktigt åtkomst till Cloud Manager.

* Under vissa förhållanden startades uppdateringsindexjobbet flera gånger parallellt, vilket resulterade i ett distributionsfel.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Användargränssnittet tillät felaktigt försök att utföra åtgärder i en miljö medan det togs bort.

* Det fanns ett färgmatchningsfel på sidan **Översikt** i Cloud Manager.

### Kända fel {#known-issues-cm}

* Ogiltiga sidor inkluderas för att få medelpoängen för innehållsgranskning under vad de ska vara.

* På fliken Innehållsgranskning visas bas-URL:en felaktigt med författardomänen i stället för publiceringsdomänen.

* För att aktivera steget Innehållsgranskning måste användarna redigera pipeline och, om så önskas, lägga till sidor. Om inga sidor läggs till granskas hemsidan.

