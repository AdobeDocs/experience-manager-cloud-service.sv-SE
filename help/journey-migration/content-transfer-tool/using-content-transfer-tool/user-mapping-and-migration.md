---
title: Användarmappning och huvudmigrering
description: Översikt över användarmappning och migrering av huvudnamn på AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 2fdfb65543fa2942e809aa5d379f4000e40bd517
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 2%

---

# Användarmappning och huvudmigrering {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Användarmappning"
>abstract="Med verktyget Innehållsöverföring kan du flytta användare och grupper från ditt befintliga Adobe Experience Manager-system (AEM) till AEM as a Cloud Service. Befintliga användare måste mappas till sina IMS-ID:n för att undvika att de dupliceras på Cloud Servicens författarinstans."

>[!NOTE]
>För tidigare versioner av verktyget för användarmappning, se [äldre dokumentation](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduktion {#introduction}

Som en del av övergångsresan till Adobe Experience Manager (AEM) as a Cloud Service måste användare och grupper (eller Principal) migreras från befintliga AEM till AEM as a Cloud Service. Den här åtgärden utförs av verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helt integrerade användningen av Adobe ID:n för åtkomst till redigeringsmiljön. Den här processen kräver att [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) för hantering av användare och användargrupper. Användarprofilinformationen är centraliserad i Adobe Identity Management System (IMS) som gör att du kan logga in på alla molnprogram i Adobe. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). På grund av den här ändringen måste befintliga användare mappas till sina IMS-ID:n för att undvika att duplicerade användare skapas i Cloud Servicens författarinstans. Eftersom grupper i traditionella AEM i grunden skiljer sig från grupper i IMS, mappas inte grupper, men de två uppsättningarna grupper måste förenas när migreringen är klar.

## Information om huvudmigrering {#principal-migration-detail}

Verktyget Innehållsöverföring och Cloud Acceleration Manager migrerar alla objekt som är associerade med det innehåll som migreras till molnsystemet.  Verktyget Innehållsöverföring gör detta genom att kopiera alla objekt från AEM under extraheringsprocessen.  CAM Ingestion väljer och migrerar sedan endast de objekt som är associerade med innehållet som ska importeras.

## Information om användarmappning {#user-mapping-detail}

AEM användare kan mappas till motsvarande Adobe IMS-användare med samma e-postadress.  Denna mappning kan göras automatiskt i CTT (under extraheringssteget) och oavsett om den är klar eller inte kan styras med en växlingsknapp innan extraheringen startas. Växlingens standardinställning kan åsidosättas av användaren när extraheringen startas.

* Om källsystemet är en författarinstans är standardalternativet att utföra mappningen _på_, eftersom det är den rekommenderade processen.
* Om källsystemet är en publiceringsinstans är alternativet att utföra mappningen som standard _av_, eftersom användare normalt inte migreras eller används i publiceringsinstanser, eller om de används, används ett annat autentiseringssystem (dvs. inte IMS) vanligtvis för dem.

Oavsett om användare mappas under extraheringen migreras de, tillsammans med grupperna, till molnsystemet under importen om de är kopplade till innehåll som migreras.

## Viktigt att tänka på vid mappning och migrering av användare {#important-considerations}

### Exceptionella ärenden {#exceptional-cases}

Följande specialfall loggas:

1. Om en användare inte har någon e-postadress `profile/email` fält för *jcr* kan användaren eller gruppen i fråga migreras men inte mappas. Detta gäller även om e-postadressen används som användarnamn för inloggning.
2. Om användaren är inaktiverad behandlas den på samma sätt som andra användare. Den mappas och migreras som vanligt och inaktiveras fortfarande i molninstansen.
3. Om det finns ett huvudnamn med samma namn (rep:mainName) på både källinstansen AEM och målinstansen av AEM Cloud Service migreras inte huvudkontot och det tidigare befintliga huvudkontot i molnet ändras inte.
4. Om en användare migreras utan att mappas via Användarmappning kan användaren inte logga in med sitt IMS-ID på målmolnsystemet. Om e-postadressen inte matchar e-postadressen som användes för att logga in i IMS, kan de inte heller logga in med sitt IMS-ID i målmolnet. De kanske kan logga in med den traditionella AEM metoden (lokal inloggning), men den här metoden är vanligtvis inte vad som önskas eller förväntas.

## Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen före intag** är inställt, tas redan överförda användare i Cloud Servicen bort tillsammans med hela den befintliga databasen. En ny databas skapas i vilken innehåll hämtas. Den här processen återställer även alla inställningar inklusive behörigheter för målanvändarinstansen och gäller för en Cloud Service som lagts till i **administratörer** grupp. Administratörsanvändaren måste läggas till på nytt i **administratörer** grupp för att hämta åtkomsttoken för CTT/CAM-inmatning.
* När innehållets popup-fönster utförs, och innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, överförs inte heller användare och grupper som är kopplade till det innehållet. Den här regeln gäller även om användare och grupper har ändrats i källsystemet. Orsaken är att användare och grupper bara migreras tillsammans med det innehåll de är kopplade till.
* Om målinstansen av AEM Cloud Service har en användare med ett annat användarnamn men samma e-postadress som en av användarna i AEM och användarmappning är aktiverat, registrerar loggarna ett felmeddelande. Källanvändaren AEM inte överföras eftersom endast en användare med en angiven e-postadress tillåts i målsystemet.
* Se [Migrerar stängda användargrupper](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) om du vill ha mer information om huvudkonton som används i en CUG-princip (Closed User Group).

## Slutlig sammanfattning och rapport {#final-report}

När extraheringen och intaget har slutförts genereras en rapport med information om huvudmigreringen. Se [Validera huvudmigreringen](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) för mer information.
