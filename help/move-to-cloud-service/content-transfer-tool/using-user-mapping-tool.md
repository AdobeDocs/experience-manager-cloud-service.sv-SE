---
title: Använda verktyget för användarmappning
description: Använda verktyget för användarmappning
translation-type: tm+mt
source-git-commit: 7c7ae680932849cf2ed0be3dc10618d55acc8366
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 5%

---


# Använda verktyget för användarmappning {#user-mapping-tool}

## Översikt {#overview}

Som en del av övergången till Adobe Experience Manager (AEM) som Cloud Service måste du flytta användare och grupper från ditt befintliga AEM till AEM som en Cloud Service. Detta görs med verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helt integrerade användningen av Adobe ID:n för åtkomst till redigeringsmiljön.  Detta kräver att du använder [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) för att hantera användare och användargrupper. Användarprofilsinformationen är centraliserad i Adobe Identity Management System (IMS) som möjliggör enkel inloggning i alla Adobe-molnprogram. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). På grund av den här ändringen måste befintliga användare och grupper mappas till sina IMS-ID:n för att undvika dubbletter av användare och grupper på Cloud Servicens författarinstans.

## Viktiga överväganden {#important-considerations}

### Undantag {#exceptional-cases}

Följande specialfall loggas:

1. Om en användare inte har någon e-postadress i fältet `profile/email` i noden *jcr* migreras användaren eller gruppen i fråga men mappas inte.

1. Om ett visst e-postmeddelande inte hittas i IMS-systemet (Adobe Identity Management System) för det organisations-ID som används (eller om IMS-ID inte kan hämtas av någon annan anledning) migreras användaren eller gruppen i fråga men inte mappas.

1. Om användaren är inaktiverad behandlas den på samma sätt som om den inte var inaktiverad. Den mappas och migreras som vanligt och förblir inaktiverad i molninstansen.

1. Om en användare finns på AEM Cloud Service-instansen för målet med samma användarnamn (rep:PrincipalName) som en av användarna på AEM för källan migreras inte användaren eller gruppen i fråga.

### Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen innan importen** har angetts tas redan överförda användare i Cloud Servicen bort tillsammans med hela den befintliga databasen och en ny databas skapas för att importera innehåll till. Detta återställer även alla inställningar inklusive behörigheter för målanvändarinstansen och gäller för en administratörsanvändare som har lagts till i gruppen **administratörer**. Administratörsanvändaren måste läggas till på nytt i gruppen **administratörer** för att hämta åtkomsttoken för CTT.

* Vi rekommenderar att du tar bort alla befintliga användare från målinstansen AEM Cloud Servicen innan du kör CTT med användarmappning. Detta för att förhindra konflikter mellan att migrera användare från AEM till AEM. Konflikter uppstår under importen om samma användare finns på AEM och AEM.

* När innehållsöverläggningar utförs och innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, kommer användare och grupper som är kopplade till det innehållet inte heller att överföras, även om användare och grupper har ändrats under tiden. Detta beror på att användare och grupper migreras tillsammans med det innehåll de är kopplade till.

* Inmatning misslyckas i följande scenarier:

1. Om målinstansen AEM Cloud Servicen har en användare med ett annat användarnamn men samma e-postadress som en av användarna i AEM.

1. Om det finns två användare i AEM med olika användarnamn men samma e-postadress. AEM som en Cloud Service tillåter inte att två användare har samma e-postadress.

## Använda verktyget för användarmappning {#using-user-mapping-tool}

Användarmappningsverktyget använder ett API som gör att det kan slå upp IMS-användare (Adobe Identity Management System) via e-post och returnera sina IMS-ID:n. Denna API kräver att användaren skapar ett klient-ID för sin organisation, en klienthemlighet och en Access- eller Bearer-token.

Följ stegen nedan för att konfigurera detta:

1. Navigera till [Adobe Developer Console](https://console.adobe.io) med din Adobe ID.
1. Skapa ett nytt projekt eller öppna ett befintligt projekt.
1. Lägg till ett API.
1. Välj API för användarhantering.
1. Skapa en JWT-autentiseringsuppgift.
1. Skapa ett nyckelpar eller Överför en offentlig nyckel (rsa är inte bra).
1. Generera en åtkomsttoken (JWT-token eller innehavartoken).
1. Spara all den här informationen, till exempel **klient-ID**, **Klienthemlighet**, **ID för tekniskt konto**, **E-post för tekniskt konto**, **Org ID** och **Åtkomsttoken** säkert.

## Användargränssnitt {#user-interface}

Verktyget för användarmappning är integrerat i verktyget Innehållsöverföring. Du kan hämta innehållsöverföringsverktyget från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Mer information om den senaste versionen finns i [Aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Välj Adobe Experience Manager och navigera till tools -> **Operations** -> **Content Transfer**.
1. Klicka på **Skapa konfiguration för användarmappning**.

   >[!NOTE]
   >Om du hoppar över det här steget hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   Fyll i fälten i API-konfiguration för användarhantering enligt beskrivningen nedan:

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **Organisations-ID**: Ange IMS-organisationsnumret (Adobe Identity Management System) för den organisation som användarna migreras till.

      >[!NOTE]
      >Logga in på [Admin Console](https://adminconsole.adobe.com/) och välj din organisation (i det övre högra området) om du tillhör fler än en organisation för att hämta ditt organisations-ID. Org-ID:t kommer att vara i URL:en för den sidan, i formatet `xx@AdobeOrg`, där xx är IMS Org-ID:t.  Du kan också hitta ditt organisations-ID på sidan [Adobe Developer Console](https://console.adobe.io) där du genererar åtkomsttoken.

   * **Klient-ID**: Ange det klient-ID som du sparade i konfigurationssteget.

   * **Åtkomsttoken**: Ange den åtkomsttoken som du sparade i konfigurationssteget.

      >[!NOTE]
      >Åtkomsttoken upphör att gälla var 24:e timme och en ny måste skapas. Om du vill skapa en ny token går du tillbaka till [Adobe Developer Console](https://console.adobe.io), väljer ditt projekt, klickar på **API för användarhantering** och klistrar in samma privata nyckel i rutan.

1. När du har angett ovanstående information klickar du på **Spara**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. Skapa en migreringsuppsättning genom att klicka på **Skapa migreringsuppsättning** och fylla i fälten och sedan klicka på **Spara**. Mer information finns i [Köra verktyget innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool).

   >[!NOTE]
   >Växlingsväxeln som tar med Mappningsanvändare från IMS-användare och -grupper är som standard PÅ. Med den här inställningen körs användarmappningsverktyget som en del av extraheringsfasen när extraheringen utförs på den här migreringsuppsättningen. Detta är det rekommenderade sättet att köra extraheringsfasen av verktyget Innehållsöverföring. Om den här växeln är inaktiverad och/eller konfigurationen för användarmappning inte skapas, hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. Mer information om hur du kör extraheringsfasen finns i [Köra verktyget Innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool).

