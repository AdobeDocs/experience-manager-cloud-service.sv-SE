---
title: Introduktion till sandlådeprogram
description: Lär dig vilka sandlådeprogram som är och hur de skiljer sig från produktionsprogram.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Introduktion till sandlådeprogram {#sandbox-programs}

Lär dig vilka sandlådeprogram som är och hur de skiljer sig från produktionsprogram.

## Introduktion {#introduction}

Ett sandlådeprogram skapas vanligtvis för att användas för utbildning, löpande demonstrationer, aktivering eller konceptbevis (POC) och är därför inte avsett för livstrafik.

Ett sandlådeprogram är en av de två typer av program som är tillgängliga i AEM Cloud Service, och det andra är ett [produktionsprogram](introduction-production-programs.md). Mer information om programtyper finns i [Förstå program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Automatiskt skapande {#auto-creation}

I sandlådeprogram skapas automatiskt. När du [skapar ett sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md):

* Lägger till AEM Sites, Assets och Edge Delivery Services som standardlösningar i programmet.

  ![Välj lösningar och tillägg för en sandlåda](assets/sandbox-solutions-add-ons.png)

* Ställer in en projektdatabas för Git med ett exempelprojekt baserat på [AEM Project Archetype](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/overview).
* Skapar en utvecklingsmiljö.
* Skapar en icke-produktionspipeline som distribueras till utvecklingsmiljön.

Ett sandlådeprogram har bara en utvecklingsmiljö.

## Användningsnoteringar och villkor {#usage-notes-conditions}

Eftersom de inte är avsedda för direkttrafik har sandlådeprogram vissa begränsningar och villkor för användningen, vilket skiljer dem från produktionsprogrammen.

| Begränsning/villkor | Beskrivning |
| --- | --- |
| Ingen direkttrafik | Sandlådeprogram är inte avsedda att innehålla livstrafik och omfattas därför inte av [AEM as a Cloud Service-åtaganden](https://www.adobe.com/legal/service-commitments.html). |
| Ingen automatisk skalning | Miljöer som skapas i ett sandlådeprogram är inte konfigurerade för automatisk skalning. Därför är dessa miljöer inte lämpliga för prestanda- eller belastningstestning. |
| Inga anpassade domäner eller IP-Tillåtelselista | [Anpassade domäner](/help/implementing/cloud-manager/custom-domain-names/introduction.md) och [IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) är inte tillgängliga i sandlådeprogram. |
| Inga ytterligare publiceringsregioner | [Ytterligare publiceringsregioner](/help/operations/additional-publish-regions.md) är inte tillgängliga i sandlådeprogram. |
| 99,99 % SLA | [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) gäller inte för sandlådeprogram. |
| Inga avancerade nätverk | [Avancerade nätverksfunktioner](/help/security/configuring-advanced-networking.md) (t.ex. självbetjäning för VPN, portar som inte är standard, dedikerade IP-adresser för utgångar och så vidare) är inte tillgängliga i sandlådeprogram. |
| Inga automatiska AEM-uppdateringar | AEM-uppdateringar skickas inte automatiskt till sandlådeprogram, men kan tillämpas manuellt i miljöer i ditt sandlådeprogram.<br> ・ En manuell uppdatering kan bara köras när målmiljön har en korrekt konfigurerad pipeline.<br> ・ En manuell uppdatering av antingen en produktions- eller staging-miljö uppdaterar automatiskt den andra. Miljöuppsättningen Production+Stage måste finnas i samma AEM-release.<br>Mer information finns i [AEM-versionsuppdateringar](/help/implementing/deploying/aem-version-updates.md).<br>Mer information om hur du uppdaterar en miljö finns i [Uppdatera miljö](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment). |
| Ingen teknisk support | Eftersom ett sandlådeprogram vanligtvis skapas för att användas i utbildningssyfte, för att köra demos, aktivering eller POC (konceptbevis), är teknisk support inte tillgänglig för problem som uppstår i ett sandlådeprogram.<br>Om du får problem med att skapa och hantera dina sandlådeprogram omfattas de här problemen av teknisk support. |
| Viloläge och borttagning | Miljöer i ett sandlådeprogram försätts automatiskt i viloläge efter åtta timmars inaktivitet. Sandlådemiljöer tas bort efter sex sammanhängande månader i viloläge.<br>Se [Vilolägen och Fristående sandlådemiljöer](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) för mer information om hur du frigör miljöer och tar bort sandlådor automatiskt. |
