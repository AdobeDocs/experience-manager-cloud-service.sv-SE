---
title: Gruppmigrering
description: Översikt över gruppmigrering i AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 50c8dd725e20cbd372a7d7858fc67b0f53a8d6d4
workflow-type: tm+mt
source-wordcount: '1921'
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
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Dokumentation för AEM Admin Console"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

Som en del av övergångsresan till Adobe Experience Manager (AEM) as a Cloud Service måste grupper migreras från befintliga AEM-system till AEM as a Cloud Service. Den här åtgärden utförs av verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helintegrerade användningen av Adobe ID:n för att komma åt författarnivån. Den här processen kräver att [Adobe Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html) används för att hantera användare och användargrupper. Användarprofilinformationen är centraliserad i Adobe Identity Management System (IMS) som gör att du kan logga in på alla Adobe molnprogram samtidigt. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=sv-SE#identity-management). På grund av den här ändringen skapas användare automatiskt på AEM när de loggar in på den via IMS.  CTT migrerar alltså inte användarna till molnsystemet.  IMS-användare måste placeras i IMS-grupper, som kan migreras eller nya grupper placeras i AEM-grupper som har behörighet att komma åt det AEM-innehåll som migreras.  På så sätt får användare i molnsystemet samma åtkomst som de hade i sitt AEM-källsystem.

## Information om gruppmigrering {#group-migration-detail}

Verktyget Innehållsöverföring och Cloud Acceleration Manager migrerar alla grupper som är kopplade till innehållet som migreras till molnsystemet. Verktyget Innehållsöverföring gör detta genom att kopiera alla grupper från AEM-källsystemet under extraheringsprocessen. CAM-inmatning väljer och migrerar sedan endast vissa grupper:

* Om en grupp använder en ACL- eller CUG-princip för migrerat innehåll migreras den gruppen, med några undantag som anges nedan.
* Det finns ett antal inbyggda grupper som redan finns i målmolnet. De migreras aldrig.
   * Vissa inbyggda grupper kan innehålla medlemsgrupper som _inte_ är inbyggda. Alla sådana medlemsgrupper (direkta medlemmar eller medlemmar av medlemmar, osv.) som refereras i en ACL- eller CUG-princip för migrerat innehåll migreras, så att användare som är medlemmar i dessa grupper (antingen direkt eller indirekt) behåller åtkomsten till det migrerade innehållet.
* Andra grupper, t.ex. de som inte finns i en ACL- eller CUG-princip, de som redan finns i målsystemet och de med unika data som redan finns i målsystemet, kommer inte att migreras.

Observera att sökvägen som loggas/rapporteras för en grupp bara är den första sökvägen som utlöste den gruppen som ska migreras, och att den gruppen också kan finnas på andra innehållssökvägar.

De flesta migrerade grupper är konfigurerade att hanteras av IMS.  Detta innebär att en grupp i IMS med samma namn länkas till gruppen i AEM, och alla IMS-användare i IMS-gruppen blir AEM-användare och medlemmar i gruppen i AEM.  Detta gör att dessa användare har tillgång till innehållet enligt ACL- eller CUG-profiler för gruppen.

Observera att migrerade grupper inte längre betraktas som&quot;lokala AEM-grupper&quot;. De är IMS-klara grupper i AEM även om de ännu inte finns i IMS.  De måste återskapas separat i IMS så att de kan synkroniseras mellan AEM och IMS.  Grupper kan skapas i IMS via Admin Console, bland annat på egen hand eller gruppvis.  Mer information om hur du skapar grupper individuellt eller gruppvis i Admin Console finns i [Hantera användargrupper](https://helpx.adobe.com/se/enterprise/using/user-groups.html).

Undantaget för den här IMS-konfigurationen gäller grupper som har skapats av Assets Collections och Privata mappar. När en samling eller en privat mapp skapas på AEM skapas grupper för åtkomst till det innehållet. Sådana grupper migreras till molnsystemet, men de är inte konfigurerade att hanteras av IMS.  Om du vill lägga till IMS-användare i dessa grupper måste de läggas till på sidan Gruppegenskaper i Assets-gränssnittet, antingen individuellt eller tillsammans som en del av en annan IMS-grupp.


## Avanmäl dig från gruppmigrering {#group-migration-option}

CTT version 3.0.20 och senare innehåller ett alternativ för att inaktivera migrering av grupper.  Detta konfigureras i OSGI-konsolen enligt följande:

* Öppna OSGI-konfigurationen `(http://<server>/system/console/configMgr)`
* Klicka på konfigurationen **Konfiguration av extraheringstjänst för innehållsöverföringsverktyg**
* Avmarkera **Inkludera grupper i migrering** om du vill inaktivera gruppmigreringar
* Klicka på **Spara** för att se till att konfigurationen sparas och är aktiv på servern

När den här inställningen är inaktiverad migreras inte grupper, och det kommer inte att finnas någon huvudmigreringsrapport eller användarrapport (se nedan).

## Rapport om huvudmigrering och användarrapport {#principal-migration-report}

När grupper inkluderas under migreringen (standard) sparas en huvudmigreringsrapport som visar vad som händer med varje grupp under migreringen.  Så här laddar du ned den här rapporten när du har lagt till den:
* I CAM går du till Innehållsöverföring och väljer Inmatningsjobb.
* Klicka på ellipsen (..) på raden för det aktuella intrycket och välj &quot;Visa huvudsammanfattning&quot;.
* I den dialogruta som visas väljer du&quot;Principal Migration Report&quot; i listrutan under&quot;Download a file...&quot; och klickar på knappen Download.
* Spara den resulterande CSV-filen.

En del information per grupp är:
* Om den migreras, sökvägen till den första ACL eller CUG som gjorde att gruppen migrerades.
* Om gruppen har migrerats tidigare. Om det aktuella intaget var ett icke-rensat intag kan vissa grupper ha migrerats under ett tidigare intag.
* Om gruppen är en inbyggd grupp, migreras inte dessa grupper eftersom de alltid finns i AEMaaCS-målmiljön.
* Om gruppen inte var en del av en ACL eller en CUG för det migrerade innehållet skulle den inte ha migrerats.
* Om gruppen var en lokal grupp, t.ex. en grupp som har skapats av en Assets Collection, kan den ha migrerats, och i det här fallet läggs ordet&quot;local&quot; till i rapporten för den gruppen.

Under migreringen migreras inte användare, men användargruppsrelationerna på källsystemet skulle gå förlorade om de inte fångades in på något sätt. Inmatningsprocessen hämtar en del av informationen i textformat i en användarrapport, som finns i slutet av huvudmigreringsrapporten.

### Användarrapport {#user-report}

I avsnittet Användarrapport rapporteras användare (en per rad) tillsammans med deras e-postadress och en lista över IMS-aktiverade grupper som migrerats under det här intaget.  Grupper som inte har migrerats, migrerats under ett tidigare intag eller som är lokala grupper tas inte med i listan.   Om en användare inte finns i någon migrerad IMS-aktiverad grupp och det inte finns några extra anteckningar som anger att det är ett specialfall (se **Anteckningar** nedan) visas den användaren _inte_ i rapporten. De grupper som rapporteras tillsammans med varje användare är de som användaren är medlem av, direkt eller indirekt, i källsystemet. Eftersom grupper i källsystemet kan kapslas medan de inte är det i målsystemet, har den här listan över grupper stöd för den nya förenklade gruppstrukturen i IMS.

Om en svepning inträffar och sedan ett icke-svepande intag, kommer grupperna i en användarlista från det icke-svepta intaget endast att vara de grupper som migreras under icke-svepningsfasen.

#### Anteckningar {#user-report-notes}

Förutom grupperna för varje användare finns det ett fält i användarrapporten där anteckningar om användaren kan anges (och en detaljerad beskrivning av anteckningens betydelse finns också i rapporten) i informationssyfte.  Möjliga anteckningar:

* **Anteckning-A** Användare som refereras direkt i en åtkomstkontrollista har *Anteckning-A* i sin anteckningssektion, eftersom detta inte är ett rekommenderat användningsfall eller bästa praxis.
* **Obs!-B** Användare som är direktmedlemmar i en inbyggd grupp kommer att ha *Anteckning-B* i sina anteckningsavsnitt, eftersom detta inte heller är ett rekommenderat användningsfall eller bästa praxis.
* **Obs!-C** Användare som är direkt från indirekta medlemmar i en migrerad lokal grupp (till exempel en grupp som har skapats av en Assets-samling) kommer att ha *Obs!-C* i sina anteckningsavsnitt, eftersom lokala grupper inte har konfigurerats för att hanteras av IMS.

Dessa fall kan inträffa samtidigt och samtidigt som de tidigare fallen.  _Om du vill ha mer information om vilka grupper varje anteckning refererar till för varje användare ska du kontrollera matningsloggen. Informationen rapporteras för varje användare._

Användarrapporten läggs till i slutet av (och är därför en del av) huvudmigreringsrapporten (se [Slutlig sammanfattning och rapport](#final-summary-and-report) nedan) för att ge kunderna en mer fullständig förståelse för grupperna och användarna och deras relationer.

## Överför filer gruppvis {#bulk-upload-files}

Eftersom grupper endast migreras till AEM as a Cloud Service måste de även läggas till i IMS så att de fungerar korrekt med AEM i molnet. Dessutom migreras inte användare, så de måste också läggas till i IMS. CTT/CAM-migreringsverktygen utför inte det här steget, men överföringsprocessen skapar två massöverföringsfiler, en för grupper och en för användare. Dessa filer kan redigeras och sedan användas tillsammans med Admin Console funktion för massöverföring för att skapa IMS-grupper och -användare baserat på dina AEM-grupper och -användare.

Mer information om hur du använder massöverföring av filer för att skapa användare och grupper med Admin Console finns i [Gruppöverföring och användaröverföring till IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md).

Se även [Hantera användare](https://helpx.adobe.com/ca/enterprise/using/users.html) för mer information om hur du hanterar AEM as a Cloud Service-användare.

## Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen innan** har angetts tas grupper som tidigare har överförts till Cloud Service-instansen bort tillsammans med hela den befintliga databasen. En ny databas skapas i vilken innehåll hämtas. Den här processen återställer även alla inställningar, inklusive behörigheter, för Cloud Service-målinstansen och gäller för alla användare som läggs till i gruppen **administratörer**. Administratörsanvändaren måste läggas till på nytt i gruppen **administratörer** för att hämta åtkomsttoken för CTT/CAM Ingesses.
* När icke-rensningsförslag utförs (**Rensa befintligt innehåll** tas bort), och om innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, överförs inte heller grupper som är kopplade till det innehållet. Den här regeln gäller även om grupperna har ändrats i källsystemet. Detta beror på att grupper endast migreras tillsammans med innehållet som de är associerade med. På grund av detta migreras i det här fallet inte grupper som är medlemmar i en grupp i källsystemet, såvida de inte tillhör en annan grupp som migreras eller i åtkomstkontrollistan för ett annat innehåll som migreras. Om du vill migrera de här grupperna i efterhand bör du överväga att använda paket, ta bort grupper från målet och migrera det relevanta innehållet igen eller migrera om med ett svep.
* Om det finns en grupp med samma unika data (rep:PrincipalName, rep:authorizedId, jcr:uid eller rep:externalId) på både AEM-källinstansen och AEM Cloud-målinstansen under ett icke-rensningsbesök, migreras den aktuella gruppen _inte_ och den tidigare gruppen på molnsystemet ändras inte. Detta loggas i huvudmigreringsrapporten.
* Se [Migrera stängda användargrupper](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) om du vill ha mer information om grupper som används i en CUG-princip (Closed User Group).

## Slutlig sammanfattning och rapport

När extraheringen och intaget har slutförts genereras en rapport med information om gruppmigrering. Mer information finns i [Validera gruppmigreringen](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration).
