---
title: Viktigt att tänka på för verktyget för användarmappning (äldre)
description: Viktigt att tänka på för verktyget för användarmappning (äldre)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Viktigt att tänka på för verktyget för användarmappning (äldre) {#important-considerations}

>[!INFO]
>
>Den här dokumentationen refererar till en inaktuell version av verktyget. Mer information om den senaste versionen finns i [Användarmappning och huvudmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

## Exceptionella ärenden {#exceptional-cases}

Följande specialfall loggas:

1. Om en användare inte har någon e-postadress i `profile/email` fält *jcr* -noden migreras användaren eller gruppen i fråga men mappas inte. Detta gäller även om e-postadressen används som användarnamn för inloggning.

1. Om det inte går att hitta något e-postmeddelande i IMS-systemet (Adobe Identity Management System) för det organisations-ID som används (eller, om IMS-ID:t inte kan hämtas), migreras användaren eller gruppen men inte mappas.

1. Om användaren är inaktiverad behandlas den på samma sätt som om den inte var inaktiverad. Den mappas och migreras som vanligt och förblir inaktiverad i molninstansen.

1. Om det finns en användare på AEM Cloud Service-målinstansen med samma användarnamn (rep:PrincipalName) som en av användarna på AEM-källinstansen migreras inte användaren eller gruppen.

1. Om en användare migreras utan att först mappas via Användarmappning kan de inte logga in med sitt IMS-ID på målmolnsystemet. De kanske kan logga in med den traditionella AEM metoden, men det här arbetsflödet är vanligtvis inte vad som önskas eller förväntas.

## Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen före intag** har angetts tas redan överförda användare bort från Cloud Servicen. Hela den befintliga databasen tas också bort och en ny databas skapas där innehållet hämtas. Den här åtgärden återställer även alla inställningar, inklusive behörigheter, för målanvändarinstansen och gäller för en Cloud Service som lagts till i **administratörer** grupp. Administratörsanvändaren måste läsas till **administratörer** grupp för att hämta åtkomsttoken för CTT.

* Adobe rekommenderar att du tar bort alla befintliga användare från målinstansen AEM Cloud Servicen innan du kör CTT med användarmappning. Den här åtgärden är nödvändig för att förhindra konflikter mellan att migrera användare från AEM till AEM. Konflikter kan uppstå vid förtäring om samma användare finns på AEM och AEM.

* När innehållets popup-fönster utförs, och innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, överförs inte heller användare och grupper som är kopplade till det innehållet. Den här regeln gäller även om användare och grupper har ändrats under tiden. Orsaken är att användare och grupper migreras tillsammans med det innehåll de är kopplade till.

* Om AEM Cloud Service har en användare med ett annat användarnamn men samma e-postadress som en användare i AEM och Användarmappning är aktiverat, loggas ett felmeddelande. Källanvändaren AEM inte överföras eftersom endast en användare med en angiven e-postadress tillåts i målsystemet.

* Om två användare på AEM har samma e-postadress och användarmappning är aktiverat loggas ett felmeddelande. En av AEM användare överförs också eftersom endast en användare med en viss e-postadress tillåts i målsystemet.

### What&#39;s Next {#whats-next}

När du har lärt dig viktiga saker och exceptionella saker är du nu redo att använda verktyget. Se [Använda verktyget för användarmappning](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) för mer information.
