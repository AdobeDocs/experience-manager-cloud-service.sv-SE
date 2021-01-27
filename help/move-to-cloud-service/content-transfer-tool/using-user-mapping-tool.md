---
title: Använda verktyget för användarmappning
description: Använda verktyget för användarmappning
translation-type: tm+mt
source-git-commit: a5129eac9f8032de5931b75c83eea62e480c1847
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 4%

---


# Använda verktyget för användarmappning {#user-mapping-tool}

## Översikt {#overview}

Som en del av övergången till AEM som Cloud Service måste du flytta användare och grupper från ditt befintliga AEM till AEM som en Cloud Service. Detta görs med verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helt integrerade användningen av Adobe ID:n för åtkomst till redigeringsmiljön.  Detta kräver att Adobe Admin Console används för att hantera användare och användargrupper. Användarprofilsinformationen är centraliserad i Adobe Identity Management System (IMS) som möjliggör enkel inloggning i alla Adobe-molnprogram. Mer information finns i Identity Management. På grund av den här ändringen måste befintliga användare och grupper mappas till sina IMS-ID:n för att undvika dubbletter av användare och grupper på Cloud Servicens författarinstans.

## Viktiga överväganden {#important-considerations}

Det finns ett fåtal exceptionella fall som behöver övervägas. Följande specialfall loggas och användaren eller gruppen i fråga mappas inte:

1. Om en användare inte har någon e-postadress i fältet `profile/email` för sin jcr-nod.

1. Om det inte går att hitta någon e-postadress i IMS-systemet för det organisations-ID som används (eller om IMS-ID inte kan hämtas av någon annan anledning).

1. Om användaren är inaktiverad behandlas den på samma sätt som om den inte var inaktiverad.  Den mappas och migreras som vanligt och förblir inaktiverad i molninstansen.

## Använda verktyget för användarmappning {#using-user-mapping-tool}

Användarmappningsverktyget använder ett API som gör att det kan söka efter IMS-användare via e-post och returnera deras IMS-ID. Denna API kräver att användaren skapar ett klient-ID för sin organisation, en klienthemlighet och en åtkomsttoken/Bearer-token.

Så här konfigurerar du det:

1. Navigera till [Adobe Developer Console](https://console.adobe.io) med din Adobe ID.
1. Skapa ett nytt projekt eller öppna ett befintligt projekt
1. Lägg till ett API
1. Välj API för användarhantering
1. Skapa en JWT-autentiseringsuppgift
1. Skapa ett nyckelpar eller Överför en offentlig nyckel (rsa är inte bra)
1. Generera en åtkomsttoken (JWT-token eller innehavartoken).
1. Spara all den här informationen (klient-ID, klienthemlighet, tekniskt konto-ID, e-post för tekniskt konto, organisations-ID, åtkomsttoken) på en säker plats.

## Användargränssnitt {#user-interface}

Verktyget för användarmappning är integrerat i verktyget Innehållsöverföring. Du kan hämta innehållsöverföringsverktyget från portalen för distribution av programvara. Mer information om den senaste versionen finns i Versionsinformation.

1. Markera Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Innehållsöverföring**.
1. Klicka på **Skapa konfiguration för användarmappning**.

   >[!NOTE]
   >Om du hoppar över det här steget hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   Fyll i fälten i API-konfiguration för användarhantering enligt beskrivningen nedan:

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **Organisations-ID**: Ange IMS-organisations-ID för den organisation som användarna migreras till.

      >[!NOTE]
      >Logga in på [Admin Console](https://adminconsole.adobe.com/) och välj din organisation (i det övre högra området) om du tillhör fler än en organisation för att hämta ditt organisations-ID. Org-ID:t kommer att vara i URL:en för den sidan, i formatet `xx@AdobeOrg`, där xx är IMS Org-ID:t.  Du kan också hitta ditt organisations-ID på sidan [Adobe Developer Console](https://console.adobe.io) där du genererar åtkomsttoken.

   * **Klient-ID**: Ange det klient-ID som du sparade i konfigurationssteget

   * **Åtkomsttoken**: Ange den åtkomsttoken som du har sparat från konfigurationssteget

      >[!NOTE]
      >Åtkomsttoken upphör att gälla var 24:e timme och en ny måste skapas. Om du vill skapa en ny token går du tillbaka till [Adobe Developer Console](https://console.adobe.io), väljer ditt projekt, klickar på API:t för användarhantering och klistrar in samma privata nyckel i rutan.

1. När du har angett ovanstående information klickar du på **Spara**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. Skapa en migreringsuppsättning genom att klicka på **Skapa migreringsuppsättning** och fylla i fälten och sedan klicka på **Spara**. Mer information finns i Köra verktyget Innehållsöverföring.

   >[!NOTE]
   >Växlingsväxeln som tar med Mappningsanvändare från IMS-användare och -grupper är som standard PÅ. Med den här inställningen körs användarmappningsverktyget som en del av extraheringsfasen när extraheringen utförs på den här migreringsuppsättningen. Detta är det rekommenderade sättet att köra extraheringsfasen av verktyget Innehållsöverföring. Om den här växeln är inaktiverad och/eller konfigurationen för användarmappning inte skapas, hoppas användare och grupper över under extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. Mer information om hur du kör extraheringsfasen finns i [Köra verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool).



