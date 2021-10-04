---
title: Använda verktyget för användarmappning
description: Använda verktyget för användarmappning
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: b290b402fe58d449dd85e9eaaef5b75e61ac1a74
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 3%

---

# Använda verktyget för användarmappning {#user-mapping-tool}

## Översikt {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Verktyg för användarmappning"
>abstract="Med verktyget Innehållsöverföring kan du flytta användare och grupper från ditt befintliga AEM till AEM som en Cloud Service. Befintliga användare och grupper måste mappas till sina IMS-ID:n för att undvika dubbletter av användare och grupper i Cloud Servicens författarinstans."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Viktigt att tänka på när du använder verktyget för användarmappning"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Använda verktyget för användarmappning"

Som en del av övergången till Adobe Experience Manager (AEM) som Cloud Service måste du flytta användare och grupper från ditt befintliga AEM till AEM som en Cloud Service. Detta görs med verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helt integrerade användningen av Adobe ID:n för åtkomst till redigeringsmiljön.  Detta kräver att du använder [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) för att hantera användare och användargrupper. Användarprofilsinformationen är centraliserad i Adobe Identity Management System (IMS) som möjliggör enkel inloggning i alla Adobe-molnprogram. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). På grund av den här ändringen måste befintliga användare och grupper mappas till sina IMS-ID:n för att undvika dubbletter av användare och grupper på Cloud Servicens författarinstans.

### Verktyg för användarmappning {#mapping-tool}

Verktyget Innehållsöverföring (utan användarmappning) migrerar alla användare och grupper som är kopplade till innehållet som migreras. Verktyget för användarmappning är en del av verktyget för innehållsöverföring, och dess enda syfte är att ändra användare och grupper så att de kan identifieras korrekt av IMS, den enkelinloggningsfunktion som används av AEM som en Cloud Service. När ändringarna är klara migrerar verktyget Innehållsöverföring det angivna innehållets användare och grupper som vanligt.

## Viktiga överväganden {#important-considerations}

### Exceptionella ärenden {#exceptional-cases}

Följande specialfall loggas:

1. Om en användare inte har någon e-postadress i fältet `profile/email` i noden *jcr* migreras användaren eller gruppen i fråga men mappas inte.

1. Om ett visst e-postmeddelande inte hittas i IMS-systemet (Adobe Identity Management System) för det organisations-ID som används (eller om IMS-ID inte kan hämtas av någon annan anledning) migreras användaren eller gruppen i fråga men inte mappas.

1. Om användaren är inaktiverad behandlas den på samma sätt som om den inte var inaktiverad. Den mappas och migreras som vanligt och förblir inaktiverad i molninstansen.

1. Om en användare finns på AEM Cloud Service-instansen för målet med samma användarnamn (rep:PrincipalName) som en av användarna på AEM för källan migreras inte användaren eller gruppen i fråga.

### Ytterligare överväganden {#additional-considerations}

* Om inställningen **Rensa befintligt innehåll i molninstansen innan importen** har angetts tas redan överförda användare i Cloud Servicen bort tillsammans med hela den befintliga databasen och en ny databas skapas för att importera innehåll till. Detta återställer även alla inställningar inklusive behörigheter för målanvändarinstansen och gäller för en administratörsanvändare som har lagts till i gruppen **administratörer**. Administratörsanvändaren måste läggas till på nytt i gruppen **administratörer** för att hämta åtkomsttoken för CTT.

* Vi rekommenderar att du tar bort alla befintliga användare från målinstansen AEM Cloud Servicen innan du kör CTT med användarmappning. Detta för att förhindra konflikter mellan att migrera användare från AEM till AEM. Konflikter uppstår under importen om samma användare finns på AEM och AEM.

* När innehållsöverläggningar utförs och innehållet inte överförs eftersom det inte har ändrats sedan den tidigare överföringen, kommer användare och grupper som är kopplade till det innehållet inte heller att överföras, även om användare och grupper har ändrats under tiden. Detta beror på att användare och grupper migreras tillsammans med det innehåll de är kopplade till.

* Om målinstansen AEM Cloud Servicen har en användare med ett annat användarnamn men samma e-postadress som en av användarna i AEM och användarmappning är aktiverat, kommer ett felmeddelande att skrivas i loggarna och AEM användare kommer inte att överföras eftersom endast en användare med en angiven e-postadress tillåts i målsystemet.

* Om två användare på AEM källinstansen har samma e-postadress och användarmappning är aktiverat, skrivs ett felmeddelande i loggarna och en av AEM-användarna kommer inte att överföras, eftersom endast en användare med en given e-postadress tillåts på måldatorn.


## Använda verktyget för användarmappning {#using-user-mapping-tool}

Användarmappningsverktyget använder ett API som gör att det kan slå upp IMS-användare (Adobe Identity Management System) via e-post och returnera sina IMS-ID:n. Denna API kräver att användaren skapar ett klient-ID för sin organisation, en klienthemlighet och en Access- eller Bearer-token.

Följ stegen nedan för att konfigurera detta:

1. Navigera till [Adobe Developer Console](https://console.adobe.io) med din Adobe ID.
1. Skapa ett nytt projekt eller öppna ett befintligt projekt.
1. Lägg till ett API - klicka på **Lägg till i projekt** och välj **API**
1. Välj API för användarhantering.  Du kanske måste få behörighet för att kunna använda det här alternativet.
1. Skapa en JWT-autentiseringsuppgift.
1. Skapa ett nyckelpar eller Överför en offentlig nyckel (rsa är inte bra).  Det finns en knapp, **Generera ett offentligt/privat nyckelpar**, som gör detta åt dig.  Se till att du sparar både offentliga och privata nycklar.
1. Navigera till API:t för användarhantering.
1. Generera en åtkomsttoken (eller innehavartoken) genom att klistra in innehållet i den privata nyckeln i textrutan och klicka på **Generera token**.
1. Spara all den här informationen, till exempel **klient-ID**, **Klienthemlighet**, **ID för tekniskt konto**, **E-post för tekniskt konto**, **Org ID** och **Åtkomsttoken** säkert.

## Användargränssnitt {#user-interface}

Verktyget för användarmappning är integrerat i verktyget Innehållsöverföring. Du kan hämta innehållsöverföringsverktyget från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Mer information om den senaste versionen finns i [Aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Markera Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Användarmappning**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing1.png)

1. Klicka på **Skapa konfiguration för användarmappning**.

   >[!NOTE]
   >Om du hoppar över det här steget hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing2.png)

   Fyll i fälten i **API-konfiguration för användarhantering** enligt beskrivningen nedan.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing3.png)

   * **Organisations-ID**: Ange IMS-organisationsnumret (Adobe Identity Management System) för den organisation som användarna migreras till.

      >[!NOTE]
      >Logga in på [Admin Console](https://adminconsole.adobe.com/) och välj din organisation (i det övre högra området) om du tillhör fler än en organisation för att hämta ditt organisations-ID. Org-ID:t kommer att vara i URL:en för den sidan, i formatet `xx@AdobeOrg`, där xx är IMS Org-ID:t.  Du kan också hitta ditt organisations-ID på sidan [Adobe Developer Console](https://console.adobe.io) där du genererar åtkomsttoken.

   * **Klient-ID**: Ange det klient-ID som du sparade i konfigurationssteget.

   * **Åtkomsttoken**: Ange den åtkomsttoken som du sparade i konfigurationssteget.

      >[!NOTE]
      >Åtkomsttoken upphör att gälla var 24:e timme och en ny måste skapas. Om du vill skapa en ny token går du tillbaka till [Adobe Developer Console](https://console.adobe.io), väljer ditt projekt, klickar på **API för användarhantering** och klistrar in samma privata nyckel i rutan.

1. När du har fyllt i fälten klickar du på **Testa konfiguration** för att testa anslutningen till API-tjänsten för användarhantering. Om anslutningen lyckas kan du klicka på **Spara** för att spara konfigurationen.

1. När du har sparat konfigurationen markerar du konfigurationen och klickar på **Starta användarmappning**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. När användarmappningen är klar klickar du på **Resultat** för att visa sammanfattningen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >När användarmappningen är klar kan du gå tillbaka till sidan Innehållsmigrering med hjälp av den synliga sökvägen. Kortet för användarmappning visar status och tidsstämpel. Klicka på **Innehållsöverföring** för att skapa en migreringsuppsättning som ska köras extrahering. Mer information finns i [Köra verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool).
