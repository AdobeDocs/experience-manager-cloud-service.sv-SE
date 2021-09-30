---
title: 'Introduktion till sandlådeprogram '
description: Introduktion till sandlådeprogram
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 7e51fb98c76a5913ef237aca3b66c73a8263f4ff
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Introduktion till sandlådeprogram {#sandbox-programs}

## Introduktion {#introduction}

Ett sandlådeprogram är en av de två typer av program som finns i AEM Cloud Service, och den andra är ett produktionsprogram.

En sandlåda skapas vanligtvis för utbildning, löpande demonstrationer, aktivering eller korrektur av begrepp (POC). De är inte avsedda att bära livstrafik. De omfattas inte av [AEM som en Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Miljöerna som skapas i en sandlåda är inte konfigurerade för automatisk skalning. Därför är dessa miljöer inte lämpliga för prestanda- eller belastningstestning.

Sandlådeprogram innehåller [!DNL Sites] och [!DNL Assets] och fylls i automatiskt med en Git-databas, en utvecklingsmiljö och en icke-produktionsprocess.  Git-databasen innehåller ett exempelprojekt baserat på AEM projekttyp.

>[!NOTE]
>Anpassade domäner och IP-Tillåtelselista är inte tillgängliga i sandlådeprogram.

Mer information om programtyperna finns i [Förstå program och programtyper](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html?lang=en).

### Attribut för sandlådeprogram {#attributes-sandbox}

Sandlådeprogram har följande attribut:

1. **Skapa program:** I sandlådeprogrammet skapas automatiskt:
   * konfiguration av projekt med exempelkod och innehåll
   * utvecklingsmiljö
   * Skapande av icke-produktionsförlopp för distribution till utvecklingsmiljö (överordnad filial distribuering till utvecklingsmiljö)

1. **Lösningar:** Sandlådeprogram innehåller AEM  [!DNL Sites] och  [!DNL Assets].

1. **AEM:** AEM uppdateringar kan användas manuellt i miljöer i sandlådeprogram och skickas inte automatiskt.
Mer information finns i [AEM uppdateringar av sandlådemiljöer](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox).

1. **Viloläge:** miljöer i ett sandlådeprogram försätts automatiskt i viloläge om ingen aktivitet identifieras under en viss tid. Sandlådor placeras i viloläge efter 8 timmars inaktivitet, varefter de kan tas ur viloläge. Vilolägen miljöer kan avaktiveras manuellt.
Mer information finns i [Viloläge och Viloläge i sandlådemiljöer](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md).

1. **Borttagning**: Sandlådor tas bort efter sex månader när de är i viloläge, och därefter kan de återskapas.
