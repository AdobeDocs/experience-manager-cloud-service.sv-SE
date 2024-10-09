---
title: Integrering av
description: som är integrerade i AEM Assets och som finns i Assets View kan erbjuda kontext i en tillgångs historia, inklusive hur den har skapats och vem som har deltagit i skapandet av den. Like a nutrition label for digital content, Content Credentials can help increase transparency and build trust with audiences.
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Content Credentials {#content-credentials}

| [Bästa praxis för sökning](/help/assets/search-best-practices.md) | [Bästa praxis för metadata](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets utvecklardokumentation](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Varumärken bryr sig mer än någonsin om innehållstransparens, AI-avslöjande och att förhindra manipulering av resurser. CAI (Content Authenticity Initiative) på Adobe bygger verktyg som är med den [Koalitionen för innehållets ursprung och äkthet](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). , som är en ny typ av krypterade, manipuleringssäkra metadata, kan hjälpa tittarna att förstå innehållets härkomst och säkerställa varumärkestillgångarnas integritet. De kan innehålla ett brett urval av härkomstdata som ger insikter i en digital resursers historia.

Denna information kan omfatta

* **Utfärdare eller signerare:** Information om enheten eller företaget som utfärdade den digitala signaturen för att certifiera eller signera resursen.
* **Utgivningsdatum:** Datumet då Content Credential tillämpades på resursen.
* **Kredit och användning:** Information om resursens tillverkare, inklusive namn, referenser till sociala medier eller annan identitetsrelaterad information.
* **Process:** Poster för redigeringar eller ändringar som gjorts i resursen.
* **Enhetsinformation:** Information om appen eller enheten som användes för att skapa eller redigera resursen.
* **AI-verktyg som används:** Om generativ AI användes för att redigera eller skapa resursen kan namnet på den modell som användes inkluderas.
* **Annan relevant information:** Ytterligare data kan också inkluderas för att ge mer kontext om en resurs historik.

Om du vill visa en fullständig bild kan [Verify](https://contentcredentials.org/verify) ge en mer omfattande inblick i resurshistoriken.

Adobe Experience Manager Assets har nu stöd för , vilket gör att användare kan se  direkt i Assets-vyn av AEM. När du tittar på resursinformationen visas manifestinformationen på en dedikerad panel i en bild med  (till exempel de som skapats med GenAI-tjänster). Om resursen hämtas, publiceras eller delas förblir  intakta med resursen.

![resurser](/help/assets/assets/content-credentials.png)

## Åtkomst till  {#access-content-credentials}

1. Gå till gränssnittet för Assets View och klicka på **Assets** i den vänstra rutan.
1. Navigate to a folder, and select the desired asset.
1. Klicka på **Information** och välj `Cr pin` i rutan längst till höger. The Content Credentials tab displays the following information about the asset.
   1. **Genererad avbildning:** Datum och tid då  tillämpades.
   1. **Innehållssammanfattning:** Anger om resursen delvis eller helt genereras av AI eller hur den redigerades.
      ![](/help/assets/assets/content-credentials1.png)
   1. **Process:** Information om programmet, enheten och AI-verktyget (t.ex. Adobe Firefly) som användes för att generera resursen, samt om ändringar som gjordes senare.
      ![process](/help/assets/assets/CR-Process.png)
   1. **Om de här :** Utfärdarens namn tillsammans med datum och tid för utfärdande.
      ![utfärdare](/help/assets/assets/CR-issuer.png)
