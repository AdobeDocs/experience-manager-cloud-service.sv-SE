---
title: Integrering med Content Credentials
description: Content Credentials, som är integrerat i AEM Assets och finns i Assets View, kan erbjuda kontext i en tillgångs historia, inklusive hur den har skapats och vem som har deltagit i skapandet av den. Som en näringsetikett för digitalt innehåll kan Content Credentials bidra till att öka transparensen och bygga förtroende hos målgrupperna.
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: fb7ce7dbb58be9fef5ab087441457770828d73c8
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Content Credentials {#content-credentials}

Varumärken är mer oroade än någonsin över innehållets transparens, AI-exponering och förhindrande av manipulering av tillgångar. Content Authenticity Initiative (CAI) på Adobe bygger verktyg som är kompatibla med den tekniska standarden [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). Content Credentials, som är en ny typ av krypterade, manipuleringssäkra metadata, kan hjälpa tittarna att förstå innehållet och säkerställa varumärkesmaterialets integritet. De kan innehålla ett brett urval av härkomstdata som ger insikter i en digital resursers historia.

Denna information kan omfatta

* **Utfärdare eller signerare:** Information om enheten eller företaget som utfärdade den digitala signaturen för att certifiera eller signera resursen.
* **Utgivningsdatum:** Det datum då Content Credential tillämpades på tillgången.
* **Kredit och användning:** Information om tillverkaren av resursen, inklusive namn, handtag för sociala medier eller annan identitetsrelaterad information.
* **Process:** Registrerar ändringar som gjorts i resursen.
* **Enhetsinformation:** Information om programmet eller enheten som används för att skapa eller redigera resursen.
* **AI-verktyg som används:** Om generativ AI användes för att redigera eller skapa resursen kan namnet på den modell som används inkluderas.
* **Annan relevant information:** Ytterligare data kan också inkluderas för att ge mer kontext om en tillgångs historik.

För en fullständig vy kan [Verifiera](https://contentcredentials.org/verify) ge en mer heltäckande inblick i resurshistoriken.

Adobe Experience Manager Assets har nu stöd för Content Credentials så att användare kan se Content Credentials direkt i Assets-vyn i AEM. När du tittar på resursinformationen visar alla bilder med Content Credentials (till exempel de som har skapats med GenAI-tjänster) manifestinformationen i en dedikerad panel. Om resursen hämtas, publiceras eller delas förblir Content Credentials intakt med resursen.

![resurser](/help/assets/assets/content-credentials.png)

## Använd Content Credentials {#access-content-credentials}

1. Gå till användargränssnittet för Assets-vyn och klicka på **Assets** i den vänstra rutan.
1. Navigera till en mapp och markera önskad resurs.
1. Klicka på **Detaljer** och välj `Cr pin` i rutan längst till höger. På fliken Content Credentials visas följande information om resursen.
   1. **Genererad bild:** Datum och tid då Content Credentials tillämpades.
   1. **Innehållssammanfattning:** Anger om resursen har genererats delvis eller helt av AI, eller hur den har redigerats.
      ![innehållsautentiseringsuppgifter](/help/assets/assets/content-credentials1.png)
   1. **Process:** Anger vilket program, vilken enhet och vilket AI-verktyg (till exempel Adobe Firefly) som används för att generera resursen samt vilka ändringar som görs senare.
      ![process](/help/assets/assets/CR-Process.png)
   1. **Om denna Content Credentials:** Utfärdarens namn tillsammans med datum och tid för utfärdande.
      ![utfärdare](/help/assets/assets/CR-issuer.png)
