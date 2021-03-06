---
title: Viktigt att tänka på när du ska mappa användare
description: Viktigt att tänka på när du ska mappa användare
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Viktigt att tänka på när du ska mappa användare {#important-considerations}


## Exceptionella ärenden {#exceptional-cases}

Följande specialfall loggas:

1. Om en användare inte har någon e-postadress i `profile/email` fält *jcr* den nod som användaren eller gruppen i fråga migreras men inte mappas.

1. Om ett visst e-postmeddelande inte hittas i IMS-systemet (Adobe Identity Management System) för det organisations-ID som används (eller om IMS-ID inte kan hämtas av någon annan anledning) migreras användaren eller gruppen i fråga men inte mappas.

1. Om användaren är inaktiverad behandlas den på samma sätt som om den inte var inaktiverad. Den mappas och migreras som vanligt och förblir inaktiverad i molninstansen.

1. Om det finns en användare på AEM Cloud Service-målinstansen med samma användarnamn (rep:PrincipalName) som en av användarna på AEM källinstansen migreras inte användaren eller gruppen i fråga.

## Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen före intag** är inställt kommer redan överförda användare i Cloud Servicen att tas bort tillsammans med hela den befintliga databasen och en ny databas kommer att skapas för att importera innehåll till. Detta återställer även alla inställningar inklusive behörigheter för målanvändarinstansen och gäller för en Cloud Service som lagts till i **administratörer** grupp. Administratörsanvändaren måste läggas till på nytt i **administratörer** grupp för att hämta åtkomsttoken för CTT.

* Vi rekommenderar att du tar bort alla befintliga användare från målinstansen AEM Cloud Servicen innan du kör CTT med användarmappning. Detta för att förhindra konflikter mellan att migrera användare från AEM till AEM. Konflikter uppstår under importen om samma användare finns på AEM och AEM.

* När innehållsöverläggningar utförs och innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, kommer användare och grupper som är kopplade till det innehållet inte heller att överföras, även om användare och grupper har ändrats under tiden. Detta beror på att användare och grupper migreras tillsammans med det innehåll de är kopplade till.

* Om målinstansen av AEM Cloud Service har en användare med ett annat användarnamn men samma e-postadress som en av användarna i AEM och användarmappning är aktiverat, kommer ett felmeddelande att skrivas i loggarna och AEM-användaren kommer inte att överföras eftersom endast en användare med en angiven e-postadress tillåts i målsystemet.

* Om två användare på AEM-källinstansen har samma e-postadress och användarmappning är aktiverat, skrivs ett felmeddelande i loggarna och en av AEM-användarna kommer inte att överföras, eftersom endast en användare med en angiven e-postadress tillåts på måldatorn.

### What’s Next {#whats-next}

När du har lärt dig viktiga saker och exceptionella saker är du nu redo att använda verktyget. Se [Använda verktyget för användarmappning](/help/journey-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.md) för mer information.
