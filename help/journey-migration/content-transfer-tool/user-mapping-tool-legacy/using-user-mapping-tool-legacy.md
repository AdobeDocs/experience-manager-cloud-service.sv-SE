---
title: Använda verktyget för användarmappning (äldre)
description: Använda verktyget för användarmappning (äldre)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 3%

---

# Använda verktyget för användarmappning (äldre) {#using-user-mapping-tool}

>[!INFO]
>
>Den här dokumentationen refererar till en inaktuell version av verktyget. Mer information om den senaste versionen finns i [Användarmappning och huvudmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

Användarmappningsverktyget använder ett API som gör att det kan slå upp IMS-användare (Adobe Identity Management System) via e-post och returnera sina IMS-ID:n. Denna API kräver att användaren skapar ett klient-ID för sin organisation, en klienthemlighet och en Access- eller Bearer-token.

## Konfigurera verktyget för användarmappning {#setting-up-user-mapping}

**Krav:** Användarmappning kräver att varje användare mappas till sitt IMS-ID har en e-postadress i profilen i AEM och i IMS.  Observera att även om användaren använder en e-postadress som användar-ID för inloggning, fungerar inte mappningen för den användaren om inte e-postadressen också finns i profilen, och även i IMS.

Följ stegen nedan för att konfigurera detta:

1. Navigera till [Adobe Developer Console](https://console.adobe.io) med din Adobe ID.
1. Skapa ett nytt projekt eller öppna ett befintligt projekt.
1. Lägg till ett API - klicka **Lägg till i projekt** och markera **API**
1. Välj API för användarhantering.  Du måste ha behörighet som systemadministratör för att det här alternativet ska vara tillgängligt.
1. Skapa en JWT-autentiseringsuppgift.
1. Skapa ett nyckelpar eller Överför en offentlig nyckel (rsa är inte bra).  Det finns en knapp, **Generera ett offentligt/privat nyckelpar**, som kommer att göra det här åt dig.  Se till att du sparar både offentliga och privata nycklar.
1. Navigera till API:t för användarhantering.
1. Generera en åtkomsttoken (eller innehavartoken) genom att klistra in innehållet i den privata nyckeln i textrutan och klicka på **Generera token**.
1. Spara all denna information, t.ex. **Klient-ID**, **Klienthemlighet**, **ID för tekniskt konto**, **E-post för tekniskt konto**, **Organisations-ID** och **Åtkomsttoken** säkert.

## Åtkomst till användargränssnittet för verktyget för användarmappning {#user-interface}

Verktyget för användarmappning är integrerat i verktyget Innehållsöverföring. Du kan hämta verktyget Innehållsöverföring från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Mer information om den senaste versionen finns i [Aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Markera Adobe Experience Manager och gå till verktygen -> **Operationer** -> **Innehållsmigrering**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Klicka på **Användarmappning** kort.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Klicka på **Skapa konfiguration för användarmappning**.

   >[!NOTE]
   >Om du hoppar över det här steget hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Fyll i fälten i **API-konfiguration för användarhantering**, enligt beskrivningen nedan.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **Organisations-ID**: Ange IMS-organisationsnumret (Adobe Identity Management System) för den organisation som användarna migreras till.

     >[!NOTE]
     >Logga in på [Admin Console](https://adminconsole.adobe.com/) och välj organisation (i det övre högra området) om du tillhör fler än en. Org-ID:t kommer att vara i URL:en för den sidan, i ett format som `xx@AdobeOrg`, där xx är IMS Org ID.  Du kan också hitta ditt Org ID i [Adobe Developer Console](https://console.adobe.io) sidan där du genererar åtkomsttoken.

   * **Klient-ID**: Ange det klient-ID som du sparade i konfigurationssteget.

   * **Åtkomsttoken**: Ange den åtkomsttoken som du sparade i konfigurationssteget.

     >[!NOTE]
     >Åtkomsttoken upphör att gälla var 24:e timme och en ny måste skapas. Om du vill skapa en ny token går du tillbaka till [Adobe Developer Console](https://console.adobe.io), väljer projektet, klickar på **API för användarhantering** och klistra in samma privata nyckel i rutan.

1. När du har fyllt i fälten klickar du på **Testa konfiguration** för att testa anslutningen till API-tjänsten för användarhantering. Om anslutningen lyckas kan du klicka på **Spara** för att spara konfigurationen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. När du har sparat konfigurationen väljer du konfigurationen och klickar på **Starta användarmappning**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Klicka på **Starta** i dialogrutan för att starta användarmappningsprocessen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Den visar **Status** as **KÖRS**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. När användarmappningen är klar klickar du på **Resultat** för att visa sammanfattningen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* När användarmappningen är klar kan du gå tillbaka till sidan Innehållsmigrering med hjälp av den synliga sökvägen. Kortet för användarmappning visar status och tidsstämpel. Klicka på **Innehållsöverföring** för att skapa en migreringsuppsättning för att köra extraheringen. Se [Använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) för mer information.

### Återuppta användarmappningsprocessen {#resume-user-mapping-process}

Om användarmappningsprocessen stoppas på grund av någon av följande orsaker:

* Användaren valde **Stoppa användarmappning**
* åtkomsttoken upphörde att gälla under processen, eller
* annan orsak

  >[!NOTE]
  >Förloppet sparas från den plats där processen stoppades.

Så här återupptar du användarmappningsprocessen:

1. Klicka **Visa logg** om du vill granska användarmappningsloggen för att kontrollera den sparade förloppet.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Klicka **Starta användarmappning** för att fortsätta där det slutade.

   >[!NOTE]
   >Kontrollera att åtkomsttoken fortfarande är giltig eller har uppdaterats innan du startar om den.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Klicka **Starta** i dialogrutan för att återuppta användarmappningsprocessen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   När användarmappningen är klar kan du visa **Status** as **SLUTFÖRD** för just den konfigurationen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
