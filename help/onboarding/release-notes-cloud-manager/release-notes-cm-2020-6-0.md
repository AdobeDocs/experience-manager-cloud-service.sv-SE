---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.6.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.6.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.6.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.6.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.6.0 är 4 juni 2020.

## Nyheter {#whats-new-cloud-manager}

* En användare i rollen *Business Owner* i Cloud Manager kan nu ta bort ett sandlådeprogram från landningssidan (via snabbåtgärdsknappen på programkortet) eller inifrån programmet.

   Mer information finns i [Ta bort ett sandlådeprogram](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) .

* En sandlådeprogramanvändare i *Business Owner* eller *Deployment Manager* -rollen i Cloud Manager kan nu ta bort sin produktions- och scenmiljö som angetts via användargränssnittet i Cloud Manager. Alternativet Ta bort finns nu både på miljökortet på sidan **Programöversikt** och på sidan **Miljö** . Om du väljer borttagningsalternativet för antingen produktion eller scen tas även det andra bort i uppsättningen.

   Mer information finns i [Ta bort ett sandlådeprogram](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) .

* Tips på landningssidan som informerar och instruerar användaren om grundläggande navigering.

* Tips på sidan **Programöversikt** för att informera och instruera användaren om grundläggande navigering i Cloud Manager för att komma igång.

* En **LEARN** -sida är nu tillgänglig i Cloud Manager, som du når via den övre navigeringen. Den här sidan innehåller resurser som hjälper användare att lära sig mer om de mest använda arbetsflödena som är relevanta för deras roller i Cloud Manager.

* Sandlådeprogram identifieras nu med ett **sandlådemärke** som visas på programkortet på landningssidan samt bredvid programnamnet på sidan **Programöversikt** .

* En användare i rollen SysAdmin har nu tillgång till den plats i Admin Console där användarroller eller behörigheter till Cloud Manager kan hanteras med ett enda klick. En **Hantera åtkomst** -knapp är nu tillgänglig på landningssidan bredvid knappen **Lägg till program** .

   Mer information finns i [SysAdmin-uppgifter](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) .

* En användare i rollen SysAdmin har nu tillgång till författarinstansen med ett klick direkt från Cloud Manager.

   Mer information finns i [Hantera åtkomst till författarinstansen](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) .

* Build-loggen innehåller nu en lista över identifierade artefakter, inklusive överhoppade innehållspaket.

* I steget Skapa valideras nu att alla genererade innehållspaket innehåller alla obligatoriska egenskaper - namn, grupp och version.

* Bygget verifierar nu att bygget producerade minst ett innehållspaket.

### Bug Fixes {#bug-fixes-cm}

* I vissa situationer var ikonerna i dialogrutan **Skapa program** feljusterade.

* Den AEM releaseidentifieraren visades inte konsekvent på sidan **Programöversikt** .

* När produktionsflödet konfigurerades var alternativet **Schemalagd distribution** inte synligt för vissa kunder.

### Kända fel {#known-issues-cm}

* Miljöer i ett sandlådeprogram försätts i viloläge när ingen aktivitet identifieras under en viss tid. Den här statusen visas inte i Cloud Manager. Status kan dock observeras via Developer Console. Detta kommer att åtgärdas i en kommande version.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö. För att åtgärda detta lägger du till mönstret i slutet av URL:en på Developer Console, där `#release-cm-p1234-e5678` 1234 *är program-ID och* 5678 ** är miljö-ID. Detta kommer att åtgärdas i en kommande version.
