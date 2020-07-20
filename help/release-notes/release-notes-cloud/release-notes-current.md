---
title: Adobe Experience Manager som Cloud Service Versionsinformation för 2020.7.0
description: Versionsinformation om Experience Manager för 2020.7.0
translation-type: tm+mt
source-git-commit: f96a9b89bb704b8b8b8eb94cdb5f94cc42890ec8
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Versionsinformation för AEM som Cloud Service 2020.7.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.7.0.

## Nyheter i Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM som en Cloud Service version 2020.7.0.

### Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.7.0 är 9 juli 2020.

### What&#39;s New {#what-is-new-cloud-manager}

* Miljösidan har gjorts om.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Antalet miljövariabler per miljö har ökat till 200.

* Molnhanterarens byggbehållare har nu stöd för både Java 8 och Java 11.

* Molnhanterarens pipelines har nu stöd för kundspecifika variabler och hemligheter.
Mer information finns i [Pipeline-variabler](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) .

### Bug Fixes {#bug-fixes-cm}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Alternativen **Avbryt** och **Spara** på redigeringssidan för icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.

### Kända fel {#known-issues}

* På grund av en förändring i hur kodens täckning beräknas är den _lägsta_ versionen av Jacoco-pluginprogrammet nu 0.7.5.201505241946 (släppt i maj 2015). Kunder som uttryckligen hänvisar till en äldre version får ett felmeddelande i kodkvalitetsprocessen.

## Nyheter i Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Readiness Analyzer version 1.0.2.

### Bug Fixes {#cra-bug-fixes}

* Tidigare version av CRA kunde inte köras på Adobe Experience Manager (AEM) 6.1. Explicit stöd för att tillåta användare i administratörsgruppen har lagts till.

   Mer information finns i [Installera CRA på AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) .

* Den förfallotidsstämpel som visades i sammanfattningsrapporten var felaktig.

* CRA upptäckte dubbletter av anpassade komponenter.

* På AEM 6.1 avslutades innehållsinspektionen innan den fullständiga undersökningen slutfördes. Undantagshantering har lagts till så att inspektören kan hoppa över och fortsätta tills den fullständiga inspektionen är slutförd.

