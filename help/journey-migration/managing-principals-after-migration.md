---
title: Hantera huvudkonton efter migrering
description: Lär dig hur du konfigurerar användare och grupper i IMS och AEM
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Hantera huvudkonton efter migrering {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Hantera huvudkonton efter migrering"
>abstract="Lär dig hur du konfigurerar användare och grupper i IMS och AEM"

I det här dokumentet beskrivs de åtgärder på hög nivå som kunder bör vidta för att konfigurera användare och grupper i IMS och AEM för att arbeta med sin AEM as a Cloud Service-miljö.

## Hantera huvudkonton {#managing-principals}

För AEM as a Cloud Service måste användare och grupper i första hand hanteras med Admin Console.  När du funderar på en migrering kan vissa av dessa åtgärder utföras innan innehållsmigreringen sker.  De viktigaste uppgiftsgrupperna

* Skapa användare och grupper i IMS
* Tilldela användare till grupper i IMS
* Tilldela IMS-grupper till AEM (om det behövs)

de första två kan utföras före eller efter innehållsmigreringen.  Detta är steg som endast påverkar användare och grupper i IMS, eventuellt även integrering med en extern IDP som Active Directory eller LDAP.  De här stegen beskrivs i [Hantera huvudkonton i IMS med Admin Console](/help/journey-migration/managing-principals.md).

När innehållet har migrerats till AEM as a Cloud Service-miljön kan det tredje steget utföras.

### Migrerar grupper

Under migreringens insatsfas migreras grupper om de krävs för att uppfylla ACL:er eller CUG-principer för det migrerade innehållet.  Mer information finns i [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Migrerade grupper (de som inte har skapats när Assets Collection skapades - se Samlingar nedan) konfigureras som IMS-grupper.  Detta innebär att alla grupper med samma namn som skapas i IMS (till exempel via Admin Console) kommer att länkas till gruppen i AEM, och användare som är medlemmar i IMS-gruppen kommer också att bli medlemmar i AEM.  För att den här länken ska fungera måste gruppen också skapas i IMS först.  Använd Admin Console för att skapa grupper, individuellt eller gruppvis, i din AEM, enligt beskrivningen i [Hantera huvudkonton i IMS med Admin Console](/help/journey-migration/managing-principals.md).

Använd AEM säkerhetsgränssnitt för att tilldela IMS-grupper till lokala AEM.  Se [Skapa och konfigurera grupper](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group).  Även om det här dokumentet är för AEM 6.5 gäller det även för att lägga till grupper i andra grupper i AEM as a Cloud Service.

### IMS-användare

Eftersom användare inte migreras måste de skapas i IMS så att de kan användas i AEM.  Det finns flera sätt att uppnå detta, men det är viktigt att de skapade användarna tilldelas rätt IMS-grupper så att användarna har samma åtkomst till innehållet som de hade i det tidigare AEM systemet.  Ett av verktygen som kan användas för detta är massöverföring i Admin Console. Använd massöverföring för att överföra användare tillsammans med grupper som de måste vara medlemmar i.  Innan du gör detta måste grupperna först skapas i IMS enligt beskrivningen ovan.

Om du vill veta vilka grupper varje användare ska tillhöra kan du använda användarrapporten (se [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  I den här rapporten visas de grupper som varje användare ska vara medlem i, och den här listan kan inkluderas i indatafilen för Admin Console-massöverföringsfunktionen.

### Samlingar

När du skapar en Assets Collection skapas också automatiskt vissa grupper som du kan använda för att hantera åtkomsten till den samlingen.  De här grupperna migreras om de nämns i migrerade samlingar, men de är inte konfigurerade att länka direkt till IMS-grupper. I AEM förblir de&quot;lokala grupper&quot; och kan inte hanteras via IMS.

Eftersom de här grupperna inte finns i IMS kan inte verktyget för massöverföring användas för att skapa användare som direktmedlemmar.  IMS-användare som också finns i AEM kan läggas till i de här grupperna separat, men om du gör detta i grupp krävs ett extra steg.  Så här kan du göra:
* Skapa en ny grupp eller grupper i Admin Console/IMS för åtkomst till samlingar och konfigurera dem för AEM.
* Logga in som medlem i gruppen/grupperna så att grupperna skapas i AEM.
* Använd användargränssnittet för Assets Collections för att lägga till den nya gruppen som redigerare/ägare/visningsprogram för de migrerade samlingarna.
* Lägg till (eller massöverföring) användare i de nya grupperna i Admin Console.
* När användaren loggar in för första gången skapas IMS-användaren i AEM och bör ha åtkomst till de nya grupperna och därmed till de ursprungliga samlingsgrupperna.

Obs! För grupptilldelning av användare måste ovanstående steg användas för att skapa användare i IMS. Användare som redan finns i IMS kan inte skapas igen via massöverföring.


