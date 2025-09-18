---
title: Content Fragments och Content Fragment Models OpenAPIs
description: Lär dig mer om OpenAPI:er för Content Fragments och Content Fragment Models.
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 1fb1201fa976e4c0e3c87f22bd9327a55828efef
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Content Fragments and Content Fragment Models Management OpenAPIs {#content-fragments-and-content-fragment-models-management-openapis}

Med den moderniserade OpenAPI-implementeringen av API:t för hantering av innehållsfragment kan utvecklare programmässigt skapa, läsa, uppdatera och ta bort åtgärder på AEM Author för hantering av innehållsfragmentmodeller och innehållsfragment som lagras i AEM. Dessa API:er har stöd för ett antal användningsfall.

Fullständig dokumentation finns i [API för hantering av innehållsfragment](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/).

>[!NOTE]
>
>Den befintliga användningen av [Assets HTTP API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) för innehållsfragment bör migreras till det nya OpenAPI:t för hantering av innehållsfragment.

>[!NOTE]
>
>Behörighet krävs för att få åtkomst till OpenAPI när du inte är inloggad på AEM, till exempel när OpenAPI används från en annan produkt som en del av en integrering.
>
>Mer information om hur du godkänner åtkomst till OpenAPI finns i [OpenAPI-baserade API:er](/help/implementing/developing/open-api-based-apis.md).

>[!CAUTION]
>
>Som standard är OpenAPI för Content Fragment Management inaktiverat vid publicering. För leveransorienterade användningsfall rekommenderar vi att du använder [OpenAPI:t för innehållsfragmentleverans](/help/headless/aem-content-fragment-delivery-with-openapi.md).

>[!NOTE]
>
>Se [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) för en översikt över de olika tillgängliga API:erna och en jämförelse av några av de koncept som ingår.