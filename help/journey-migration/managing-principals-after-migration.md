---
title: Hantera huvudkonton efter migrering
description: Lär dig konfigurera användare och grupper i IMS och AEM
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: 50c8dd725e20cbd372a7d7858fc67b0f53a8d6d4
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# Hantera huvudkonton efter migrering {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Hantera huvudkonton efter migrering"
>abstract="Lär dig konfigurera användare och grupper i IMS och AEM"

I det här dokumentet beskrivs de åtgärder som kunder bör vidta för att konfigurera användare och grupper i IMS och AEM så att de kan arbeta med sin AEM as a Cloud Service-miljö.

Mer information om gruppmigrering och huvudmigreringsrapporten som är tillgänglig för varje enskilt förtäring finns i [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

En guide om hur du använder gruppgrupper och användarfiler i Admin Console finns i [Massöverföring av huvudkonton till IMS efter användning av CTT](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md).

## Hantera huvudkonton {#managing-principals}

För AEM as a Cloud Service måste användare och grupper i första hand hanteras med Admin Console.  När du funderar på en migrering kan vissa av dessa åtgärder utföras innan innehållsmigreringen sker.  De viktigaste uppgiftsgrupperna

* Skapa användare och grupper i IMS
* Tilldela användare till grupper i IMS
* Tilldela IMS-grupper till AEM-grupper (om det behövs)

De första två kan utföras före eller efter innehållsmigreringen.  Detta är steg som endast påverkar användare och grupper i IMS, eventuellt även integrering med en extern IDP som Active Directory eller LDAP.  De här stegen beskrivs i [Hantera huvudkonton i IMS med Admin Console](/help/journey-migration/managing-principals.md).

När innehållet har migrerats till AEM as a Cloud Service-miljön kan det tredje steget utföras.

### Migrerar grupper

Under migreringens insatsfas migreras grupper om de krävs för att uppfylla ACL:er eller CUG-principer för det migrerade innehållet.  Mer information finns i [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Migrerade grupper (de som inte har skapats av Assets Collection eller Skapa privata mappar - se Samlingar och Privata mappar nedan) konfigureras som IMS-grupper.  Detta innebär att alla grupper med samma namn som skapats i IMS (t.ex. via Admin Console) kommer att länkas till gruppen i AEM, och användare som är medlemmar i IMS-gruppen kommer också att bli medlemmar i gruppen i AEM.  För att den här länken ska fungera måste gruppen också skapas i IMS först.  Använd Admin Console för att skapa grupper, individuellt eller gruppvis, i din AEM-instans enligt beskrivningen i [Hantera huvudkonton i IMS med Admin Console](/help/journey-migration/managing-principals.md).

Använd AEM säkerhetsgränssnitt för att tilldela IMS-grupper till lokala AEM-grupper. Det gör du genom att gå till sidan Verktyg i AEM, klicka på Säkerhet och välja Grupper.

### IMS-användare

Eftersom användare inte migreras måste de skapas i IMS så att de kan användas i AEM.  Det finns flera sätt att uppnå detta, men det är viktigt att de användare som har skapats tilldelas rätt IMS-grupper så att användarna har samma åtkomst till innehållet som de hade i det tidigare AEM-systemet.  Ett av verktygen som kan användas för detta är massöverföring i Admin Console. Använd massöverföring för att överföra användare tillsammans med grupper som de måste vara medlemmar i.  Innan du gör detta måste grupperna först skapas i IMS enligt beskrivningen ovan.

Om du vill veta vilka grupper varje användare ska tillhöra kan du använda användarrapporten (se [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  I den här rapporten visas de grupper som varje användare ska vara medlem i, och den här listan inkluderas normalt i indatafilen för gruppanvändare för användning med Admin Console-funktionen för massöverföring.

### Samlingar och privata mappar

När du skapar en Assets Collection eller en privat mapp skapas också grupper automatiskt för att hantera åtkomsten till det Assets-innehållet.  Dessa grupper migreras om de nämns i det migrerade innehållet, men de är inte konfigurerade att länka direkt till IMS-grupper. I AEM förblir de&quot;lokala grupper&quot; och kan inte hanteras via IMS.

Eftersom de här grupperna inte finns i IMS kan inte verktyget för massöverföring användas för att skapa användare som direktmedlemmar.  IMS-användare som också finns i AEM kan läggas till i de här grupperna separat, men om du gör detta i grupp krävs ett extra steg.  Så här kan du göra:
* Skapa en ny grupp eller grupper i Admin Console/IMS för åtkomst till samlingar/privata mappar och konfigurera dem för AEM.
* Logga in som medlem i gruppen/grupperna så att grupperna skapas i AEM.
* För migrerade samlingar eller privata mappar använder du Assets-gränssnittet för att lägga till den nya gruppen som redigerare/ägare/visningsprogram.
* Lägg till (eller massöverföring) användare i de nya grupperna i Admin Console.
* När användaren loggar in för första gången skapas IMS-användaren i AEM och bör ha tillgång till de nya grupperna och därmed till den ursprungliga samlingen eller privata mappgrupper.

Obs! För grupptilldelning av användare måste ovanstående steg användas för att skapa användare i IMS. Användare som redan finns i IMS kan inte skapas igen via massöverföring, men massredigeraren kan användas för att göra den typen av ändringar (Se [Admin Console Bulk User Upload](https://helpx.adobe.com/se/enterprise/using/bulk-upload-users.html) under **Redigera användarinformation**).
