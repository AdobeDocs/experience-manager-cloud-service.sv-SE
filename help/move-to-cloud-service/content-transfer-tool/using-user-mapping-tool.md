---
title: Använda verktyget för användarmappning
description: Använda verktyget för användarmappning
translation-type: tm+mt
source-git-commit: 664c278494a5ac88362b994946060ab3baa846d8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 6%

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