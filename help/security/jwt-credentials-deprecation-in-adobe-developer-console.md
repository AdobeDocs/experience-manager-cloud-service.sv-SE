---
title: Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console
description: Lär dig hur borttagning av JWT-autentiseringsuppgifter påverkar AEM i Adobe Developer Console.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 802e29017d3f1e59ee1676b4172292cb3453648a
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 bör referera till [den här artikeln](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) för mer information.

Adobe-kunder använder [Adobe Developer Console](https://developer.adobe.com/console) för att generera autentiseringsuppgifter som möjliggör åtkomst till olika API:er. Kunderna väljer mellan olika typer av autentiseringsuppgifter, från OAuth Server-to-Server till Single-Page App. En av dessa autentiseringstyper, JWT-autentiseringsuppgifter (Service Account), har ersatts med autentiseringsuppgifterna för OAuth Server-till-Server. Det går inte att skapa nya JWT-referenser (Service Account) den 3 juni 2024 eller senare, och befintliga JWT-autentiseringsuppgifter fungerar inte den 27 januari 2025 eller senare. Du kan [läs om borttagningen](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

I den här artikeln finns ytterligare information om hur AEM as a Cloud Service ska hantera borttagningen.

För närvarande är huvuduppgiften att AEM funktioner ännu inte har stöd för de nya autentiseringsuppgifterna för OAuth Server-till-Server. Support kommer snart - i mitten av maj 2024 via en AEM för AEM as a Cloud Service. Du kan ha fått ett e-postmeddelande med instruktioner om hur du migrerar JWT-inloggningsuppgifterna, men du kan vara säker på att du kan och bör hålla kvar när du migrerar autentiseringsuppgifterna tills AEM har stöd för den nya autentiseringstypen OAuth Server-till-Server.

I avsnitten nedan listas de scenarier där kunderna måste (eller ibland inte måste) ersätta sina JWT-referenser (Service Account) med OAuth Server-to-Server-autentiseringsuppgifter, när AEM har stöd för dem i mitten av maj. [Läs om](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) för att ersätta inloggningsuppgifterna i framtiden.

>[!NOTE]
>
>The [**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (notera **AEM** i namnet, vilket skiljer det från **Adobe** Developer Console) innehåller ett verktyg för att generera [JWT-token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) används för server-till-server-API:er. Autentiseringsuppgifterna är inte föråldrade och kan fortsätta att användas.


## Integrera AEM med andra Adobe-lösningar {#integrating-aem-with-other-adobe-solutions}

**Åtgärd**: Vänta tills efter mitten av maj 2024, när AEM stöder det (den här artikeln uppdateras vid den tidpunkten)

**Relevanta AEM**: AEM AS A CLOUD SERVICE

AEM använder användargränssnittet AEM Author för att konfigurera integreringar med alla andra Adobe-lösningar. Exempel: Adobe Target, Adobe Analytics, Adobe Launch, AFCS och många fler.

![Integrera AEM med andra lösningar](/help/security/assets/jwt-deprecation.png)

Här är några exempel [instruktionerna](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims) för att konfigurera integrationen med Adobe Target. API-nyckeln i [Slutför IMS-konfigurationen i AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims#completing-the-ims-configuration-in-aem) -avsnittet ska migreras till autentiseringstypen OAuth Server-to-Server, när AEM har stöd för dessa autentiseringsuppgifter i mitten av maj. Dessa instruktioner kommer att uppdateras i mitten av maj för att hjälpa dig att tillämpa de nya autentiseringsuppgifterna för OAuth Server-to-Server.

## API:er för Cloud Manager {#cloud-manager-apis}

**Åtgärd**: Migrera till OAuth-autentiseringsuppgifter för server-till-server.

**Relevanta AEM**: AEM AS A CLOUD SERVICE

Kunder skapar Adobe Developer Console-projekt så att de kan starta [API:er för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Autentiseringsuppgifterna i Adobe Developer-projektet ska migreras till autentiseringstypen OAuth Server-to-Server innan de inaktuella JWT-autentiseringsuppgifterna går ut i januari 2025.

## Automatiskt genererade projekt {#autogen-projects}

**Åtgärd**: Migrera inte eftersom Adobe ska migrera för din räkning.

**Relevanta AEM**: AEM as a Cloud Service.

När Cloud Manager etablerar AEM as a Cloud Service miljö genereras ett Adobe Developer Console-projekt automatiskt med JWT-inloggningsuppgifter. Det här projektet är skrivskyddat, vilket visas i skärmbilden nedan. Kunden kan inte migrera dessa projekt till autentiseringsuppgifter för OAuth Server-till-Server, utan Adobe kommer att migrera dessa projekt separat innan autentiseringsuppgifterna inte längre är användbara.

![Automatiskt genererade projekt](/help/security/assets/jwt-deprecation-autogen-projects.png)
