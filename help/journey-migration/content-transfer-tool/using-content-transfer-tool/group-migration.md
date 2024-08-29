---
title: Gruppmigrering
description: Översikt över gruppmigrering i AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# Gruppmigrering {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="Gruppmigrering"
>abstract="Med verktyget Innehållsöverföring kan du kopiera grupper från ditt befintliga Adobe Experience Manager-system (AEM) till AEM as a Cloud Service."

>[!NOTE]
>Tidigare versioner av verktyget för användarmappning finns i [äldre dokumentation](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduktion {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="Användarna migreras inte"
>abstract="Verktyget Innehållsöverföring migrerar inte längre användare. Användare bör hanteras i Admin Console."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEM Admin Console-dokumentation"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

Som en del av övergångsresan till Adobe Experience Manager (AEM) as a Cloud Service måste grupper migreras från befintliga AEM till AEM as a Cloud Service. Den här åtgärden utförs av verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helintegrerade användningen av Adobe ID:n för att komma åt författarnivån. Den här processen kräver att [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) används för att hantera användare och användargrupper. Användarprofilinformationen är centraliserad i Adobe Identity Management System (IMS) som gör att du kan logga in på alla molnprogram i Adobe. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). På grund av den här ändringen skapas användare automatiskt AEM när de loggar in på den via IMS.  CTT migrerar alltså inte användarna till molnsystemet.  IMS-användare måste placeras i IMS-grupper, som kan migreras eller nya grupper placeras i de AEM grupper som har behörighet att komma åt det AEM innehållet som migreras.  På så sätt får användare i molnsystemet samma åtkomst som de hade i sina AEM.

## Information om gruppmigrering {#group-migration-detail}

Verktyget Innehållsöverföring och Cloud Acceleration Manager migrerar alla grupper som är kopplade till innehållet som migreras till molnsystemet. Verktyget Innehållsöverföring gör detta genom att kopiera alla grupper från AEM under extraheringsprocessen. CAM-inmatning väljer och migrerar sedan endast vissa grupper:

* Det finns ett antal inbyggda grupper som redan finns i målmolnet. De migreras aldrig.
* Direktmedlemsgrupper i inbyggda grupper som direkt eller indirekt hänvisas till i en ACL- eller CUG-policy för migrerat innehåll migreras, så att användare som är direkt eller indirekt medlemmar i sådana grupper behåller sin åtkomst till det migrerade innehållet.
* Om en grupp använder en ACL- eller CUG-princip för migrerat innehåll migreras den gruppen.
* Andra grupper, t.ex. de som inte finns i en ACL- eller CUG-princip, de som redan finns i målsystemet och de med unika data som redan finns i målsystemet, kommer inte att migreras.

Observera att sökvägen som loggas/rapporteras för en grupp bara är den första sökvägen som utlöste den gruppen som ska migreras, och att den gruppen också kan finnas på andra innehållssökvägar.

De flesta migrerade grupper är konfigurerade att hanteras av IMS.  Detta innebär att en grupp i IMS med samma namn länkas till gruppen i AEM, och alla IMS-användare i IMS-gruppen blir AEM användare och medlemmar i gruppen i AEM.  Detta gör att dessa användare har tillgång till innehållet enligt ACL- eller CUG-profiler för gruppen.

Undantaget för den här IMS-konfigurationen gäller grupper som skapats av Assets Collections. När en samling skapas på AEM skapas grupper för åtkomst till den samlingen. Sådana grupper migreras till molnsystemet, men de är inte konfigurerade att hanteras av IMS.  Om du vill lägga till IMS-användare i dessa grupper måste de läggas till på sidan Gruppegenskaper i Assets-gränssnittet, antingen individuellt eller tillsammans som en del av en annan IMS-grupp.


## Avanmäl dig från gruppmigrering {#group-migration-option}

CTT version 3.0.20 och senare innehåller ett alternativ för att inaktivera migrering av grupper.  Detta konfigureras i OSGI-konsolen enligt följande:

* Öppna OSGI-konfigurationen `(http://<server> /system/console/configMgr)`
* Klicka på konfigurationen **Konfiguration av extraheringstjänst för innehållsöverföringsverktyg**
* Avmarkera **Inkludera grupper i migrering** om du vill inaktivera gruppmigreringar
* Klicka på **Spara** för att se till att konfigurationen sparas och är aktiv på servern

När den här inställningen är inaktiverad migreras inte grupper och det kommer inte att finnas någon huvudmigreringsrapport eller användarrapport.

## Användarrapport {#user-report}

Under migreringen migreras inte användare, men användargruppsrelationerna på källsystemet går förlorade om de inte fångas in på något sätt.  Användarrapporten innehåller en del av informationen i textformat i en användarrapport. I den rapporteras varje användare (en per rad) tillsammans med en lista över grupper som den är medlem i (men grupper som inte migrerats placeras inte i den här listan), såvida inte listan över grupper är tom, i vilket fall användaren inte visas. De grupper som rapporteras tillsammans med varje användare är de som användaren är medlem av direkt eller indirekt i källsystemet. Eftersom grupper i källsystemet kan kapslas medan de inte är det i målsystemet, har den här listan över grupper stöd för den nya förenklade gruppstrukturen i IMS.

Om användaren rensar och sedan inte svep, kommer grupperna i en användarlista att inkludera de grupper som migrerats i båda faserna.

Förutom grupperna för varje användare finns det ett fält i rapporten där anteckningar kan läggas till för användaren (och en detaljerad beskrivning av anteckningens betydelse finns också i rapporten).  Möjliga anmärkningar är:

* Användare som refereras direkt i en ACL har *Note-A* i sitt anteckningsavsnitt, eftersom detta inte är ett rekommenderat användningsexempel eller bästa praxis.
* Användare som är direktmedlemmar i en inbyggd grupp kommer att ha *Note-B* i sina anteckningsavsnitt, eftersom detta inte heller är ett rekommenderat användningsexempel eller bästa praxis.

Dessa fall kan inträffa samtidigt och samtidigt som de tidigare fallen.

Användarrapporten läggs till i slutet av (och ingår därför i) huvudmigreringsrapporten (se [Slutlig sammanfattning och rapport](#final-summary-and-report) nedan).

## Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen innan** har angetts, tas grupper som tidigare har överförts till Cloud Servicen bort tillsammans med hela den befintliga databasen. En ny databas skapas där innehåll har importerats. Den här processen återställer även alla inställningar inklusive behörigheter för målanvändarinstansen och är true för alla användare som läggs till i Cloud Servicen **administratörer** . Administratörsanvändaren måste läggas till på nytt i gruppen **administratörer** för att hämta åtkomsttoken för CTT/CAM Ingesses.
* När icke-rensningsförslag utförs (**Rensa befintligt innehåll** tas bort), och om innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, överförs inte heller grupper som är kopplade till det innehållet. Den här regeln gäller även om grupperna har ändrats i källsystemet. Detta beror på att grupper endast migreras tillsammans med innehållet som de är associerade med. På grund av detta migreras i det här fallet inte grupper som är medlemmar i en grupp i källsystemet, såvida de inte tillhör en annan grupp som migreras eller i åtkomstkontrollistan för ett annat innehåll som migreras. Om du vill migrera de här grupperna i efterhand bör du överväga att använda paket, ta bort grupper från målet och migrera det relevanta innehållet igen eller migrera om med ett svep.
* Om det finns en grupp med samma unika data (rep:PrincipalName, rep:authorizedId, jcr:uid eller rep:externalId) på både käll-AEM och mål-AEM Cloud Service-instansen under ett icke-rensningsbesök, migreras gruppen _inte_ och den tidigare gruppen på molnsystemet förblir oförändrad. Detta loggas i huvudmigreringsrapporten.
* Se [Migrera stängda användargrupper](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) om du vill ha mer information om grupper som används i en CUG-princip (Closed User Group).

## Slutlig sammanfattning och rapport

När extraheringen och intaget har slutförts genereras en rapport med information om gruppmigrering. Mer information finns i [Validera gruppmigreringen](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration).
