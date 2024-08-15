---
title: Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console
description: Lär dig hur borttagning av JWT-inloggningsuppgifter påverkar AEM i Adobe Developer Console.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
feature: Security
role: Admin
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5-kunder bör referera till [den jämförbara dokumentationen för AEM 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) för mer information.

Adobe-kunder använder [Adobe Developer Console](https://developer.adobe.com/console) för att generera autentiseringsuppgifter som möjliggör åtkomst till olika API:er. Kunderna väljer mellan olika typer av autentiseringsuppgifter, från OAuth Server-to-Server till Single-Page App. En av dessa autentiseringstyper, JWT-autentiseringsuppgifter (Service Account), har ersatts med autentiseringsuppgifterna för OAuth Server-till-Server. Det går inte att skapa nya JWT-referenser (Service Account) den 3 juni 2024 eller senare, och befintliga JWT-autentiseringsuppgifter fungerar inte den 27 januari 2025 eller senare. Du kan [läsa om borttagningen](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

I den här artikeln finns ytterligare information om hur AEM as a Cloud Service ska hantera borttagningen.

Den största utmaningen är att AEM nu stöder de nya autentiseringsuppgifterna för OAuth Server-till-Server för AEM as a Cloud Service. Du kan ha fått ett e-postmeddelande med instruktioner om hur du migrerar dina JWT-autentiseringsuppgifter, och migreringen kan nu göras.

I avsnitten nedan listas de scenarier där kunderna måste (eller i vissa fall inte måste) ersätta sina JWT-referenser (Service Account) med OAuth Server-to-Server-autentiseringsuppgifter, som nu AEM stöder dem. [Läs hur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) migrerar autentiseringsuppgifterna.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observera **AEM** i namnet, som skiljer det från **Adobe** Developer Console) tillhandahåller ett verktyg för att generera [JWT-tokens](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) som används för server-till-server-API:er. Autentiseringsuppgifterna är inte föråldrade och kan fortsätta att användas.

## Integrera AEM med andra Adobe-lösningar {#integrating-aem-with-other-adobe-solutions}

**Åtgärd**: Migrera konfigurationen som AEM stöder nu OAuth-autentiseringsuppgifter.

**Relevanta AEM**: AEM as a Cloud Service

AEM använder AEM för att konfigurera integreringar med många andra Adobe-lösningar. Exempel: Adobe Target, Adobe Analytics med flera.

Mer information om hur du gör det finns i [Konfigurera IMS-integreringar för AEM as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md):

* skapa konfigurationer med OAuth-autentiseringsuppgifter
* migrera konfigurationer som har skapats med JWT-autentiseringsuppgifter för att använda OAuth-autentiseringsuppgifter

## Cloud Manager API:er {#cloud-manager-apis}

**Åtgärd**: Migrera dina JWT-autentiseringsuppgifter till OAuth-autentiseringsuppgifter, som Cloud Manager nu stöder.

**Relevanta AEM**: AEM as a Cloud Service

Kunder skapar Adobe Developer Console-projekt så att de kan anropa [Cloud Manager API:er](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Autentiseringsuppgifterna i Adobe Developer-projektet ska migreras till autentiseringstypen OAuth Server-to-Server innan de inaktuella JWT-autentiseringsuppgifterna går ut i januari 2025.

## Automatiskt genererade projekt {#autogen-projects}

**Åtgärd**: Migrera inte eftersom Adobe kommer att migrera åt dig.

**Relevanta AEM**: AEM as a Cloud Service.

När Cloud Manager etablerar AEM as a Cloud Service-miljöer genereras ett Adobe Developer Console-projekt automatiskt med JWT-referenser. Det här projektet är skrivskyddat, vilket visas i skärmbilden nedan. Kunder kan inte och bör inte försöka migrera dessa projekt till autentiseringsuppgifter för OAuth Server-till-Server. I stället kommer Adobe att migrera dessa projekt separat innan inloggningsuppgifterna inte längre är användbara.

![Automatiskt genererade projekt](/help/security/assets/jwt-deprecation-autogen-projects.png)
