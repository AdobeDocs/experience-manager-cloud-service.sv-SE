---
title: Användarmappning och huvudmigrering
description: Översikt över användarmappning och huvudmigrering
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 3%

---

# Användarmappning och huvudmigrering {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Användarmappning"
>abstract="Med verktyget Innehållsöverföring kan du flytta användare och grupper från ditt befintliga AEM till AEM as a Cloud Service. Befintliga användare måste mappas till sina IMS-ID:n för att undvika att de dupliceras på Cloud Servicens författarinstans."

>[!NOTE]
>För tidigare versioner av verktyget för användarmappning, se [äldre dokumentation](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduktion {#introduction}

Som en del av övergången till Adobe Experience Manager (AEM) as a Cloud Service måste du flytta användare och grupper från ditt befintliga AEM till AEM as a Cloud Service. Detta görs med verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helt integrerade användningen av Adobe ID:n för åtkomst till redigeringsmiljön. Detta kräver att [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) för hantering av användare och användargrupper. Användarprofilsinformationen är centraliserad i Adobe Identity Management System (IMS) som möjliggör enkel inloggning i alla Adobe-molnprogram. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management). På grund av den här ändringen måste befintliga användare mappas till sina IMS-ID:n för att undvika dubbletter av användare i Cloud Servicens författarinstans. Eftersom grupper i traditionella AEM i grunden skiljer sig från grupper i IMS, mappas inte grupper, men de två uppsättningarna grupper måste förenas när migreringen är klar.

## Information om användarmappning och migrering {#user-mapping-detail}

Verktyget Innehållsöverföring och Cloud Acceleration Manager migrerar alla användare som är kopplade till det innehåll som migreras. Mappningen görs automatiskt och om den görs kan styras med en växlingsknapp innan extraheringen startas. Växlingens standardinställning kan åsidosättas av användaren när extraheringen startas.

* Om källsystemet är en författarinstans är standardalternativet att utföra mappningen _på_ eftersom det är den rekommenderade processen.
* Om källsystemet är en publiceringsinstans är alternativet att utföra mappningen som standard _av_ eftersom användare normalt inte migreras eller används i publiceringsinstanser.

## Viktigt att tänka på vid mappning och migrering av användare {#important-considerations}


### Exceptionella ärenden {#exceptional-cases}

Följande specialfall loggas:

1. Om en användare inte har någon e-postadress i `profile/email` fält *jcr* nod som användaren eller gruppen i fråga kan migreras men inte mappas. Detta gäller även om e-postadressen används som användarnamn för inloggning.

1. Om användaren är inaktiverad behandlas den på samma sätt som om den inte var inaktiverad. Den mappas och migreras som vanligt och inaktiveras fortfarande i molninstansen.

1. Om det finns en användare på AEM Cloud Service-målinstansen med samma användarnamn (rep:PrincipalName) som en av användarna på AEM källinstansen migreras inte användaren eller gruppen i fråga.

1. Om en användare migreras utan att först mappas via Mappning av användare, eller om e-postadressen inte matchar e-postadressen som används för att logga in i IMS, kan de inte logga in med sitt IMS-ID på målmolnsystemet. De kanske kan logga in med den traditionella AEM metoden, men tänk på att det vanligtvis inte är vad som önskas eller förväntas.


## Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen före intag** är inställt kommer redan överförda användare i Cloud Servicen att tas bort tillsammans med hela den befintliga databasen och en ny databas kommer att skapas för att importera innehåll till. Detta återställer även alla inställningar inklusive behörigheter för målanvändarinstansen och gäller för en Cloud Service som lagts till i **administratörer** grupp. Administratörsanvändaren måste läggas till på nytt i **administratörer** grupp för att hämta åtkomsttoken för CTT.
* När innehållsöverläggningar utförs och innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, överförs inte heller användare och grupper som är kopplade till det innehållet, även om användare och grupper har ändrats under tiden. Detta beror på att användare och grupper migreras tillsammans med det innehåll de är kopplade till.
* Om målinstansen av AEM Cloud Service har en användare med ett annat användarnamn men samma e-postadress som en av användarna i AEM och användarmappning är aktiverat, skrivs ett felmeddelande i loggarna och AEM-användaren inte överförs, eftersom endast en användare med en angiven e-postadress tillåts i målsystemet.
