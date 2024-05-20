---
title: Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console
description: Lär dig hur borttagning av JWT-autentiseringsuppgifter påverkar AEM i Adobe Developer Console.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: b6e26ecaa73aaee37b6b824426dc0cd65d459502
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 bör referera till [den här artikeln](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) för mer information.

Adobe-kunder använder [Adobe Developer Console](https://developer.adobe.com/console) för att generera autentiseringsuppgifter som möjliggör åtkomst till olika API:er. Kunderna väljer mellan olika typer av autentiseringsuppgifter, från OAuth Server-to-Server till Single-Page App. En av dessa autentiseringstyper, JWT-autentiseringsuppgifter (Service Account), har ersatts med autentiseringsuppgifterna för OAuth Server-till-Server. Det går inte att skapa nya JWT-referenser (Service Account) den 3 juni 2024 eller senare, och befintliga JWT-autentiseringsuppgifter fungerar inte den 27 januari 2025 eller senare. Du kan [läs om borttagningen](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

I den här artikeln finns ytterligare information om hur AEM as a Cloud Service ska hantera borttagningen.

Den största utmaningen är att AEM nu stöder de nya autentiseringsuppgifterna för OAuth Server-till-Server för AEM as a Cloud Service. Du kan ha fått ett e-postmeddelande med instruktioner om hur du migrerar dina JWT-autentiseringsuppgifter. Migreringen kan nu göras.

I avsnitten nedan listas de scenarier där kunderna måste (eller i vissa fall inte måste) ersätta sina JWT-referenser (Service Account) med OAuth Server-to-Server-autentiseringsuppgifter, som nu AEM stöder dem. [Läs om](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) för att migrera inloggningsuppgifterna.

>[!NOTE]
>
>The [**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (notera **AEM** i namnet, vilket skiljer det från **Adobe** Developer Console) innehåller ett verktyg för att generera [JWT-token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) används för server-till-server-API:er. Autentiseringsuppgifterna är inte föråldrade och kan fortsätta att användas.

## Integrera AEM med andra Adobe-lösningar {#integrating-aem-with-other-adobe-solutions}

**Åtgärd**: Migrera konfigurationen eftersom AEM nu stöder OAuth-autentiseringsuppgifter.

**Relevanta AEM**: AEM AS A CLOUD SERVICE

AEM använder AEM för att konfigurera integreringar med många andra Adobe-lösningar. Exempel: Adobe Target, Adobe Analytics med flera.

Se [Konfigurera IMS-integreringar för AEM as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) om du vill ha mer information om hur du:

* skapa konfigurationer med OAuth-autentiseringsuppgifter
* migrera konfigurationer som har skapats med JWT-autentiseringsuppgifter för att använda OAuth-autentiseringsuppgifter

## API:er för Cloud Manager {#cloud-manager-apis}

**Åtgärd**: Bekräfta när dessa kan migreras från JWT till OAuth-autentiseringsuppgifter.

**Relevanta AEM**: AEM AS A CLOUD SERVICE

Kunder skapar Adobe Developer Console-projekt så att de kan starta [API:er för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Autentiseringsuppgifterna i Adobe Developer-projektet ska migreras till autentiseringstypen OAuth Server-to-Server innan de inaktuella JWT-autentiseringsuppgifterna går ut i januari 2025.

## Automatiskt genererade projekt {#autogen-projects}

**Åtgärd**: Migrera inte eftersom Adobe ska migrera för din räkning.

**Relevanta AEM**: AEM as a Cloud Service.

När Cloud Manager etableras AEM as a Cloud Service miljöer genereras ett Adobe Developer Console-projekt automatiskt med JWT-autentiseringsuppgifter. Det här projektet är skrivskyddat, vilket visas i skärmbilden nedan. Kunder kan inte och bör inte försöka migrera dessa projekt till autentiseringsuppgifter för OAuth Server-till-Server. I stället kommer Adobe att migrera dessa projekt separat innan inloggningsuppgifterna inte längre är användbara.

![Automatiskt genererade projekt](/help/security/assets/jwt-deprecation-autogen-projects.png)
