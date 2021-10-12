---
title: Använda verktyget för användarmappning
description: Använda verktyget för användarmappning
source-git-commit: 09ab81364f0fd45ddedcd5f918e6ab5a4bdd1f0d
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 3%

---


# Använda verktyget för användarmappning {#using-user-mapping-tool}

Användarmappningsverktyget använder ett API som gör att det kan slå upp IMS-användare (Adobe Identity Management System) via e-post och returnera sina IMS-ID:n. Denna API kräver att användaren skapar ett klient-ID för sin organisation, en klienthemlighet och en Access- eller Bearer-token.

## Konfigurera verktyget för användarmappning {#setting-up-user-mapping}

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

## Åtkomst till användargränssnittet för verktyget för användarmappning {#user-interface}

Verktyget för användarmappning är integrerat i verktyget Innehållsöverföring. Du kan hämta innehållsöverföringsverktyget från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Mer information om den senaste versionen finns i [Aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Markera Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Innehållsmigrering**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Klicka på **kortet för användarmappning**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Klicka på **Skapa konfiguration för användarmappning**.

   >[!NOTE]
   >Om du hoppar över det här steget hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Fyll i fälten i **API-konfiguration för användarhantering** enligt beskrivningen nedan.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **Organisations-ID**: Ange IMS-organisationsnumret (Adobe Identity Management System) för den organisation som användarna migreras till.

      >[!NOTE]
      >Logga in på [Admin Console](https://adminconsole.adobe.com/) och välj din organisation (i det övre högra området) om du tillhör fler än en organisation för att hämta ditt organisations-ID. Org-ID:t kommer att vara i URL:en för den sidan, i formatet `xx@AdobeOrg`, där xx är IMS Org-ID:t.  Du kan också hitta ditt organisations-ID på sidan [Adobe Developer Console](https://console.adobe.io) där du genererar åtkomsttoken.

   * **Klient-ID**: Ange det klient-ID som du sparade i konfigurationssteget.

   * **Åtkomsttoken**: Ange den åtkomsttoken som du sparade i konfigurationssteget.

      >[!NOTE]
      >Åtkomsttoken upphör att gälla var 24:e timme och en ny måste skapas. Om du vill skapa en ny token går du tillbaka till [Adobe Developer Console](https://console.adobe.io), väljer ditt projekt, klickar på **API för användarhantering** och klistrar in samma privata nyckel i rutan.

1. När du har fyllt i fälten klickar du på **Testa konfiguration** för att testa anslutningen till API-tjänsten för användarhantering. Om anslutningen lyckas kan du klicka på **Spara** för att spara konfigurationen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. När du har sparat konfigurationen markerar du konfigurationen och klickar på **Starta användarmappning**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Klicka på **Starta** i dialogrutan för att starta användarmappningsprocessen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Den visar **status** som **KÖRNING**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. När användarmappningen är klar klickar du på **Resultat** för att visa sammanfattningen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* När användarmappningen är klar kan du gå tillbaka till sidan Innehållsmigrering med hjälp av den synliga sökvägen. Kortet för användarmappning visar status och tidsstämpel. Klicka på **Innehållsöverföring** för att skapa en migreringsuppsättning som ska köras extrahering. Mer information finns i [Köra verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool).


### Återuppta användarmappningsprocessen {#resume-user-mapping-process}

Om användarmappningsprocessen stoppas på grund av någon av följande orsaker:

* Användaren valde **Stoppa användarmappning**
* åtkomsttoken upphörde att gälla under processen, eller
* annan orsak

   >[!NOTE]
   >Förloppet sparas från den plats där processen stoppades.

Så här återupptar du användarmappningsprocessen:

1. Klicka på **Visa logg** för att kontrollera den sparade förloppet i användarmappningsloggen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Klicka på knappen **Starta användarmappning** igen för att fortsätta där den slutade.

   >[!NOTE]
   >Kontrollera att åtkomsttoken fortfarande är giltig eller har uppdaterats innan du startar om den.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Klicka på **Start** i dialogrutan för att återuppta användarmappningsprocessen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   När användarmappningsprocessen har slutförts visas **Status** som **FINISHED** för den specifika konfigurationen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
