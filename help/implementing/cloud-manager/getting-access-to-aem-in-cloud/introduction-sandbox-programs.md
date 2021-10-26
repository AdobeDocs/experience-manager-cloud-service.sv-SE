---
title: 'Introduktion till sandlådeprogram '
description: Introduktion till sandlådeprogram
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 1892900ea3f365e1b5f7d31ffae64d45256d2a3a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Introduktion till sandlådeprogram {#sandbox-programs}

## Introduktion {#introduction}

Ett sandlådeprogram är ett av de två programtyperna i AEM Cloud Service, det andra ett produktionsprogram.

En sandlåda skapas vanligtvis för utbildning, löpande demonstrationer, aktivering eller korrektur av begrepp (POC). De är inte avsedda att bära livstrafik. De omfattas inte av [AEM as a Cloud Service åtaganden](https://www.adobe.com/legal/service-commitments.html).

Miljöerna som skapas i en sandlåda är inte konfigurerade för automatisk skalning. Därför är dessa miljöer inte lämpliga för prestanda- eller belastningstestning.

Sandlådeprogram innehåller [!DNL Sites] och [!DNL Assets] och fylls automatiskt i med en Git-databas, en utvecklingsmiljö och en icke-produktionsprocess.  Git-databasen innehåller ett exempelprojekt baserat på AEM projekttyp.

>[!IMPORTANT]
>Ett sandlådeprogram har bara en utvecklingsmiljö.

>[!NOTE]
>Anpassade domäner och IP-Tillåtelselista är inte tillgängliga i sandlådeprogram.

Se [Program och programtyper](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html?lang=en) om du vill veta mer om programtyperna.

### Attribut för sandlådeprogram {#attributes-sandbox}

Sandlådeprogram har följande attribut:

1. **Skapa program:** När du skapar sandlådeprogram skapas följande automatiska funktioner:
   * konfiguration av projekt med exempelkod och innehåll
   * utvecklingsmiljö
   * Skapande av icke-produktionsförlopp för distribution till utvecklingsmiljö (överordnad filial distribuering till utvecklingsmiljö)

1. **Lösningar:** Sandlådeprogram innehåller AEM [!DNL Sites] och [!DNL Assets].

1. **AEM:** AEM uppdateringar kan tillämpas manuellt i sandlådemiljöer och skickas inte automatiskt.
Se [AEM till sandlådemiljöer](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) för mer information.

1. **Viloläge:** Miljöer i ett sandlådeprogram försätts automatiskt i viloläge om ingen aktivitet identifieras under en viss tid. Sandlådor placeras i viloläge efter 8 timmars inaktivitet, varefter de kan tas ur viloläge. Vilolägen miljöer kan avaktiveras manuellt.
Se [Viloläge och avvänjningsmiljöer för sandlådor](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) för mer information.

1. **Borttagning**: Sandlådor tas bort efter sex månader när de är i viloläge, och därefter kan de återskapas.
