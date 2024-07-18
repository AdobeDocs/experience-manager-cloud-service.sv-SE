---
title: Introduktion till sandlådeprogram
description: Lär dig vilka sandlådeprogram som skiljer sig från produktionsprogram.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 88b0479c44f6431a9f254551e51b1ce86af91d0f
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# Introduktion till sandlådeprogram {#sandbox-programs}

Lär dig vilka sandlådeprogram som skiljer sig från produktionsprogram.

## Introduktion {#introduction}

Ett sandlådeprogram skapas vanligtvis för att användas för utbildning, löpande demonstrationer, aktivering eller konceptbevis (POC) och är därför inte avsett för livstrafik.

Ett sandlådeprogram är en av de två typer av program som är tillgängliga i AEM Cloud Service, och det andra är ett [produktionsprogram.](introduction-production-programs.md) Mer information om programtyper finns i [Förstå program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Automatiskt skapande {#auto-creation}

I sandlådeprogram skapas automatiskt. När du skapar ett sandlådeprogram gör Cloud Manager automatiskt följande:

* Lägger till AEM Sites och AEM Assets som lösningar i programmet.
* Ställer in en projekt-Git-databas med ett exempelprojekt baserat på [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* Skapar en utvecklingsmiljö.
* Skapar en icke-produktionspipeline som distribueras till utvecklingsmiljön.

Ett sandlådeprogram har bara en utvecklingsmiljö.

## Begränsningar och villkor {#limitations}

Eftersom de inte är avsedda för direkttrafik har sandlådeprogram vissa begränsningar och villkor för användningen, vilket skiljer dem från produktionsprogrammen.

### Ingen Live-trafik {#live-traffic}

Sandlådeprogram är inte avsedda att innehålla livstrafik och omfattas därför inte av [AEM as a Cloud Service-åtaganden.](https://www.adobe.com/legal/service-commitments.html)

### Ingen autoskalning {#auto-scaling}

Miljöer som skapas i ett sandlådeprogram är inte konfigurerade för automatisk skalning. Därför är dessa miljöer inte lämpliga för prestanda- eller belastningstestning.

### Inga anpassade domäner eller IP-Tillåtelselista {#ip-allow}

[Anpassade domäner](/help/implementing/cloud-manager/custom-domain-names/introduction.md) och [IP tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) är inte tillgängliga i sandlådeprogram.

### Inga ytterligare Publish-regioner {#additional-publish-regions}

[Ytterligare publiceringsregioner](/help/operations/additional-publish-regions.md) är inte tillgängliga i sandlådeprogram.

### No 99.99% SLA {#999-sla}

[99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) gäller inte för sandlådeprogram.

### Inget avancerat nätverk {#advanced-networking}

[Avancerade nätverksfunktioner](/help/security/configuring-advanced-networking.md) (t.ex. självbetjäning för VPN, portar som inte är standard, dedikerade IP-adresser för utgångar och så vidare) är inte tillgängliga i sandlådeprogram.

### Manuella AEM {#updates}

AEM uppdateras inte automatiskt i sandlådeprogram, men kan tillämpas manuellt i miljöer i ditt sandlådeprogram.

* En manuell uppdatering kan bara köras när målmiljön har en korrekt konfigurerad pipeline.
* En manuell uppdatering av antingen en produktions- eller staging-miljö uppdaterar automatiskt den andra. Miljöuppsättningen Production+Stage måste finnas i samma AEM.

Mer information finns i [AEM versionsuppdateringar](/help/implementing/deploying/aem-version-updates.md).

Mer information om hur du uppdaterar en miljö finns i [Uppdatera miljö](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).

### Viloläge och borttagning {#hibernation}

Miljöer i ett sandlådeprogram försätts automatiskt i viloläge efter åtta timmars inaktivitet. Sandlådemiljöer tas bort efter sex sammanhängande månader i viloläge.

Se [Vilolägen och Fristående sandlådemiljöer](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) om du vill ha mer information om hur du frigör miljöer och tar bort sandlådor automatiskt.

### Ingen teknisk support {#no-support}

Eftersom ett sandlådeprogram vanligtvis skapas för att användas i utbildningssyfte, för att köra demonstrationer, aktivering eller konceptbevis (POC), är teknisk support inte tillgänglig för problem som uppstår i ett sandlådeprogram.

Om du får problem med att skapa och hantera dina sandlådeprogram omfattas detta fortfarande av teknisk support.
