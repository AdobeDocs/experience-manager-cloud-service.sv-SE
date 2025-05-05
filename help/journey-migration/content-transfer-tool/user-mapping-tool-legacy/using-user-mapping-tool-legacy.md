---
title: Använda verktyget för användarmappning (äldre)
description: Använda verktyget för användarmappning (äldre)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---


# Använda verktyget för användarmappning (äldre) {#using-user-mapping-tool}

>[!INFO]
>
>Den här dokumentationen refererar till en inaktuell version av verktyget. Mer information om den senaste versionen finns i [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Användarmappningsverktyget använder ett API som gör att det kan slå upp IMS-användare (Adobe Identity Management System) via e-post och returnera sina IMS-ID:n. Denna API kräver att användaren skapar ett klient-ID för sin organisation, en klienthemlighet och en Access- eller Bearer-token.

## Konfigurera verktyget för användarmappning {#setting-up-user-mapping}

**Krav:** Användarmappning kräver att varje användare som ska mappas till sitt IMS-ID har en e-postadress i profilen i AEM och i IMS. Även om användaren använder en e-postadress som ett användar-ID för inloggning fungerar inte mappning för den användaren om inte e-postadressen också finns i profilen, och även i IMS.

Följ stegen nedan för att konfigurera detta:

1. Navigera till [Adobe Developer Console](https://developer.adobe.com/console/) med din Adobe ID.
1. Skapa ett projekt eller öppna ett befintligt projekt.
1. Lägg till ett API - klicka på **Lägg till i projekt** och välj **API**
1. Välj API för användarhantering. Du måste ha behörighet som systemadministratör för att det här alternativet ska vara tillgängligt.
1. Skapa en JWT-autentiseringsuppgift.
1. Skapa ett nyckelpar eller Överför en offentlig nyckel (rsa är inte bra). Det finns en knapp, **Generera ett offentligt/privat nyckelpar**, som skapar detta nyckelpar åt dig. Se till att du sparar både offentliga och privata nycklar.
1. Navigera till API:t för användarhantering.
1. Generera en åtkomsttoken (eller innehavartoken) genom att klistra in innehållet i den privata nyckeln i textrutan och klicka på **Generera token**.
1. Spara all den här informationen säkert, till exempel **Klient-ID**, **Klienthemlighet**, **ID för tekniskt konto**, **E-post för tekniskt konto**, **Org-ID** och **Åtkomsttoken**.

## Åtkomst till användargränssnittet för verktyget för användarmappning {#user-interface}

Verktyget för användarmappning är integrerat i verktyget Innehållsöverföring. Du kan hämta innehållsöverföringsverktyget från [portalen för programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Mer information om den senaste versionen finns i [Aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Markera Adobe Experience Manager och navigera till verktyg > **Åtgärder** > **Innehållsmigrering**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Klicka på kortet **Användarmappning**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Klicka på **Skapa konfiguration för användarmappning**.

   >[!NOTE]
   >Om du hoppar över det här steget hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Fyll i fälten i **API-konfiguration för användarhantering**, enligt beskrivningen nedan.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **Organisations-ID**: Ange Adobe Identity Management System (IMS)-organisations-ID för organisationen som användarna migreras till.

     >[!NOTE]
     >Logga in på [Admin Console](https://adminconsole.adobe.com/) och välj din organisation (i det övre högra hörnet) om du tillhör fler än en. Org-ID:t finns i URL:en för den sidan, i formatet som `xx@AdobeOrg`, där xx är IMS Org-ID:t. Du kan också hitta ditt organisations-ID på sidan [Adobe Developer Console](https://developer.adobe.com/console/) där du genererar åtkomsttoken.

   * **Klient-ID**: Ange klient-ID:t som du sparade i konfigurationssteget.

   * **Åtkomsttoken**: Ange den åtkomsttoken som du sparade i konfigurationssteget.

     >[!NOTE]
     >Åtkomsttoken upphör att gälla var 24:e timme och en ny måste skapas. Om du vill skapa en token går du tillbaka till [Adobe Developer Console](https://developer.adobe.com/console/), väljer ditt projekt, klickar på **API för användarhantering** och klistrar in samma privata nyckel i rutan.

1. När du har fyllt i fälten klickar du på **Testa konfiguration** för att testa anslutningen till API-tjänsten för användarhantering. Om anslutningen lyckas kan du klicka på **Spara** för att spara konfigurationen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. När du har sparat konfigurationen markerar du konfigurationen och klickar på **Starta användarmappning**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Klicka på **Start** i dialogrutan så att du startar användarmappningsprocessen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   **Status** visas som **KÖRNING**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. När användarmappningen är klar klickar du på **Resultat** för att visa sammanfattningen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* När användarmappningen är klar kan du gå tillbaka till sidan Innehållsmigrering med hjälp av den synliga sökvägen. Kortet för användarmappning visar status och tidsstämpel. Klicka på **Innehållsöverföring** så att du kan skapa en migreringsuppsättning för att köra extraheringen. Mer information finns i [Köra verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=sv-SE#running-tool).

### Återuppta användarmappningsprocessen {#resume-user-mapping-process}

Om användarmappningsprocessen stoppas på grund av någon av följande orsaker:

* Alternativet **Stoppa användarmappning** har valts av användaren.
* Åtkomsttoken upphörde att gälla under processen.
* Eller någon annan orsak.

  >[!NOTE]
  >Förloppet sparas från den plats där processen stoppades.

Så här återupptar du användarmappningsprocessen:

1. Klicka på **Visa logg** om du vill granska användarmappningsloggen så att du kan kontrollera den sparade förloppet.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Klicka på knappen **Starta användarmappning** igen för att fortsätta där den slutade.

   >[!NOTE]
   >Kontrollera att åtkomsttoken fortfarande är giltig eller har uppdaterats innan du startar om den.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Klicka på **Start** i dialogrutan så att du återupptar användarmappningsprocessen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   När användarmappningsprocessen har slutförts kan du visa **Status** som **FINISHED** för den specifika konfigurationen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
