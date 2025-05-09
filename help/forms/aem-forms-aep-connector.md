---
title: Anslut AEM Forms till Adobe Experience Platform (AEP) | Dataintegreringsguide
description: Lär dig hur du integrerar AEM Forms med Adobe Experience Platform för att utnyttja kundprofiler, skicka in formulärdata och skapa personaliserade upplevelser. Stegvisa guider.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
source-git-commit: 052f8425c3c7bc2c12882af4f7b88d559ea34fb3
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 0%

---


# AEM Forms-integrering med Adobe Experience Platform (AEP) {#aem-forms-aep-integration}

<span class="preview"> Möjligheten att ansluta Adaptive Forms (AEM Forms) till Adobe Experience Platform (AEP) är under programmet för tidig åtkomst. Om du vill begära åtkomst till funktionen skickar du ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D). Du kan även gå till sidan <a href="/help/forms/early-access-ea-features.md">Tidig åtkomst-program </a> och upptäcka alla tillgängliga innovationer och funktioner. . </span>

## Ökning {#overview}

Ni kan koppla AEM Forms till Adobe Experience Platform för att omvandla era formulärupplevelser. Tack vare den här kraftfulla integreringen kan organisationer utnyttja kundprofiler i realtid för personaliserade formulärupplevelser, effektivisera inlämningen av data från **AEM Forms till Experience Platform** och skapa enhetliga kundprofiler i hela Adobe ekosystem. Genom att koppla ihop era adaptiva formulär med Experience Platform robusta datahanteringsfunktioner kan ni skapa mer relevanta upplevelser och förbättra konverteringsgraden samtidigt som ni behåller en enda informationskälla för kunddata.

### Vad är AEM Forms Connector for Adobe Experience Platform (AEP)? {#what-is-connector}

AEM Forms Connector for Adobe Experience Platform (AEP) är en OOTB-anslutning som tillhandahålls av AEM Forms som möjliggör smidig integrering mellan AEM Forms och Adobe Experience Platform (AEP). Integreringen gör att du kan skapa formulär med XDM-scheman som finns i AEP och skicka tillbaka data till AEP för personalisering och profilhydrering.

## Varför ska jag ansluta AEM Forms till Adobe Experience Platform (AEP)? {#benefits}

Att knyta ihop en adaptiv Forms med Adobe Experience Platform ger avsevärda fördelar för både er organisation och era kunder:

* **Enhetliga kundprofiler** - Förbättra kundprofiler med data från inskickning av formulär, skapa en heltäckande bild av kundinteraktioner och -inställningar
* **Personaliserade formulärupplevelser** - Använd befintliga profildata för att fylla i fält i förväg och anpassa formulär baserat på känd kundinformation
* **Effektiv datainsamling** - Hämta formulärdata direkt till AEP datamängder utan att skapa anpassade anslutningar eller integreringskod
* **Aktivering av data i realtid** - Skicka formulärdata till andra Adobe-program via Real-Time CDP för omedelbar aktivering
* **Förenklad efterlevnadshantering** - Hantera policyer för samtycke och datastyrning centralt via AEP
* **Minskad utvecklingstid** - Eliminera anpassat integrationsarbete med en färdig anslutning som följer vedertagna standarder
* **Förbättra kundprofiler med formulärdata** - Uppdatera och förbättra kundprofiler automatiskt vid varje formulärinlämning, vilket ger djupare kundinsikter

## Viktiga funktioner {#key-features}

* Skapa formulär med AEP XDM-scheman
* Skicka formulärdata till AEP för personalisering
* Stöd för inmatning av strömmande data
* Aktivera profilhydrering för bättre användarupplevelser
* Integrering med AEP profilsystem
* XDM-schemaintegrering med adaptiva formulär för standardiserad datainsamling
* AEP direktuppspelningsanslutning för formulär som möjliggör databearbetning i realtid

I videon nedan visas steg-för-steg-anvisningar om förutsättningarna (som att skapa ett schema, konfigurera datakonfiguration och autentisering) och hur man skapar och ansluter adaptiva Forms till Adobe Experience Platform (AEP)

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

## Förutsättningar {#prerequisites}

Innan du konfigurerar AEP Connector i AEM Forms måste du kontrollera att du har slutfört följande i Adobe Experience Platform:

1. Schemainställningar
   * [Skapa ett XDM-schema](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [Aktivera schema för profilering](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [Definiera identitetsfält](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. Datakonfiguration
   * [Skapa en datauppsättning](https://experienceleague.adobe.com/sv/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [Konfigurera direktuppspelningsanslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/tutorials/create-streaming-connection) (Du behöver URL:en för direktuppspelningsslutpunkten senare, så notera det nu.)

3. Autentisering
   * [Generera API-autentiseringsuppgifter](https://experienceleague.adobe.com/sv/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials) (klient-ID och klienthemlighet) från Adobe Developer Console


## Implementeringssteg

### 1. Skapa AEP Cloud-konfiguration

1. Navigera till din **Adobe Experience Manager-instans** > **Verktyg** > **Cloud-tjänster** > **Adobe Experience Platform**.
1. Välj en **konfigurationsbehållare** för att lagra konfigurationen.
1. Klicka på **Skapa** för att öppna konfigurationsguiden för AEP
1. Ange följande information:
   * Titel
   * Klient-ID (hämtas från utvecklarkonsolen)
   * Klienthemlighet (hämtas från utvecklarkonsolen)
   * OAuth-URL (Det finns en standardURL, men den kan också hämtas från utvecklarkonsolen)

1. Klicka på **Anslut** för att upprätta anslutningen. När du har upprättat anslutningen konfigurerar du följande ytterligare inställningar:
   * Bas-URL: platform.adobe.io (Det här är en standard-URL och kan hämtas från utvecklarkonsolen. URL:erna för autentisering och plattform används som standard för att producera URL:er. Om du måste ansluta till scenen måste du använda URL:er för scenen.)
   * Organisations-ID (detta hämtas från utvecklarkonsolen tillsammans med klient-ID/hemlighet)
   * Namn på sandlåda (krävs för både utvecklings- och produktionsmiljöer)

### 2. Skapa formulär med integrering av XDM-schema {#form-creation}

1. Öppna guiden Skapa formulär:
   * Navigera till din **Adobe Experience Manager-instans** > **Forms** > **Forms &amp; Documents**.
   * Klicka på **Skapa** > **Adaptivt formulär**.
1. Välj en mall på fliken **källa**
1. Markera alternativet **Adobe Experience Platform** på fliken **Data** .

1. Välj din molnkonfiguration i egenskapspanelen. Systemet läser in alla tillgängliga scheman från Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Endast profilaktiverade och icke-systemgenererade scheman hämtas.
   > * Inläsning av inledande schema kan ta en stund vid första konfigurationen.
1. Välj lämpliga/obligatoriska fält i schemat. (Se videon för detaljerade steg.)
1. På fliken Skicka:
   * Välj åtgärden **Skicka till Adobe Experience Platform**
   * Konfigurera inställningar för formulärsändning för **AEM Forms-dataöverföring till Experience Platform**
1. I egenskapspanelen:
   * Lägg till strömnings-URL (hämtas från AEP Sources > Streaming Connection)
   * Lägg till dataflödes-ID (finns i AEP-källor > Flöde > API-användningsinformation)
1. Klicka på **Spara**. Ange formulärinformationen:
   * Titel
   * Namn
   * Lagringssökväg
1. Lägg till knappen Skicka i formuläret. Formuläret kan nu skickas till AEP.


## Viktiga anteckningar {#important-notes}

* Data som skickas via formulär blir synliga i AEP efter cirka 10-15 minuter
* Som standard visas endast profilaktiverade scheman
* Medan inlämning av data fungerar för alla scheman är förifyllningsfunktionen begränsad till profilaktiverade scheman
* Data i scheman som inte är profilaktiverade kommer inte att användas för att skapa profiler, även om schemat senare aktiveras för profilering
* **Kundprofilenrikning med formulärdata** kräver korrekt konfiguration av identitetsfält i XDM-schemat
* **AEM Forms-data som skickas till Experience Platform** använder **AEP-direktuppspelningsanslutning för formulär** för att säkerställa dataflöde i realtid

## Bästa praxis {#best-practices}

1. Planera schemastrukturen noggrant innan du aktiverar profilering
1. Tänk på datavolym och systemskalningskrav när du konfigurerar **AEP-direktuppspelningsanslutning för formulär**
1. Testa integrationen noggrant innan produktionen distribueras
1. Övervaka processer för datainmatning och skapande av profiler
1. Utforma **XDM-schemaintegreringen med adaptiva formulär** så att endast nödvändiga data samlas in
1. Använd **kundprofilsberikning med formulärdata** strategiskt för att förbättra personaliseringen

## Tekniska överväganden {#technical-considerations}

* Kopplingen använder API:er för offentlig direktuppspelning för att skicka data
* Skapandet av profiler baseras på identitetsfältet
* Datainsamling sker automatiskt i AEP
* Integreringen stöder både framtagning av nya formulär och befintliga formulärändringar
* Integrering av XDM-schema med adaptiva formulär standardiserar datastrukturen över olika kontaktytor
* AEP direktuppspelningsanslutning för blanketter ger möjlighet till datainmatning i realtid

## Vanliga frågor och svar {#faq}

### Allmänna frågor {#general-questions}

**F: &quot;Är den här kopplingen tillgänglig med flera erbjudanden av AEM Forms?**
S: Nej, den här integreringen är bara tillgänglig för AEM Forms as a Cloud Service och ingår i programmet för tidig åtkomst.

**Q: Fungerar den här kopplingen med både adaptiva Forms Core-komponenter och Foundation-komponenter?**
S: Den här kopplingen fungerar med både adaptiva Forms Core-komponenter och adaptiva Forms Foundation-komponenter.

**F: Kan jag skicka data till flera AEP-datauppsättningar från ett och samma formulär?**
S: För närvarande kan varje formulär bara skicka till en datauppsättning.

**F: Finns det någon gräns för hur många formulärinskickade formulär som kan behandlas?**
S: Inlämningar av formulär omfattas av ditt AEP direktuppspelade [kvoter och rabattbegränsningar](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/api/quota) .

<!-- >
**Q: Can form attachments be sent to AEP?**
A: No, form attachments cannot be directly sent to AEP. You would need to store attachments separately and only send metadata to AEP. -->

### Implementeringsfrågor {#implementation-questions}

**F: Hur felsöker jag anslutningsproblem mellan AEM Forms och AEP?**
S: Verifiera molnkonfigurationsinställningarna, kontrollera att API-autentiseringsuppgifterna är korrekta och kontrollera att URL:en för direktuppspelningsslutpunkten är korrekt konfigurerad.

**F: Kan jag använda anpassade XDM-scheman med den här integreringen?**
S: Ja, du kan använda valfritt anpassat XDM-schema så länge det är korrekt konfigurerat i AEP och, för förifyllningsfunktioner, aktiverat för profiler.

**F: Hur aktiverar jag formulärifyllning med AEP-profildata?**
S: Kontrollera att ditt schema är profilaktiverat och att formuläret är konfigurerat att använda samma identitetsfält som är definierat i ditt schema.

**F: Vad händer om jag behöver omvandla data innan jag skickar dem till AEP?**
S: Du kan använda formulärregler eller anpassade funktioner för att omforma data innan de skickas. För komplexa omformningar bör du överväga att använda en anpassad skicka-åtgärd.

**F: Kan jag använda den här integreringen i en hybriddistributionsmodell?**
S: Nej, den här integreringen gäller endast AEM Forms as a Cloud Service.

## Sammanfattning och nästa steg {#summary-next-steps}

Tack vare AEM Forms Integration med Adobe Experience Platform kan man skapa ett smidigt dataflöde mellan blanketter och Experience Platform större ekosystem. Tack vare den här integreringen kan ni skapa mer personaliserade formulärupplevelser, effektivisera datainsamlingen och förbättra kundprofilerna med värdefulla data för att skicka in formulär.

Så här kommer du igång med den här integreringen:

1. **Begär åtkomst** - Om du inte redan har det kan du gå med i programmet för tidig åtkomst genom att kontakta [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)
2. **Förbered din miljö** - Kontrollera att du har de behörigheter och konfigurationer som krävs i både AEM Forms och Adobe Experience Platform
3. **Följ implementeringsstegen** - Använd guiden ovan för att konfigurera din molnkonfiguration och skapa ditt första AEP-anslutna formulär med XDM-schemaintegrering
4. **Testa noggrant** - Verifiera både inskickning av data och förifyllning i en utvecklingsmiljö
5. **Planera för produktion** - Samarbeta med implementeringsteamet för att schemalägga distributionen av AEM Forms-data som skickas till Experience Platform i produktion

## Relaterade resurser {#related-resources}

* [AEM Forms as a Cloud Service-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=sv-SE)
* [Adobe Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=sv-SE)
* [Översikt över XDM-systemet](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv-SE)
* [Direktuppspelning i Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=sv-SE)
* [Kundprofil i realtid - översikt](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=sv-SE)
* [AEM Forms Tidiga åtkomstfunktioner](/help/forms/early-access-ea-features.md)
* [Skapa adaptiv Forms med kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md)
* [Använda formulärdatamodeller i AEM Forms](/help/forms/using-form-data-model.md)

<!--
Schema markup for technical documentation
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Connect AEM Forms with Adobe Experience Platform (AEP) | Data Integration Guide",
  "description": "Learn how to integrate AEM Forms with Adobe Experience Platform to leverage customer profiles, submit form data, and create personalized experiences.",
  "datePublished": "2025-05-28",
  "author": {
    "@type": "Corporation",
    "name": "Adobe"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adobe Experience League",
    "logo": {
      "@type": "ImageObject",
      "url": "https://experienceleague.adobe.com/assets/img/favicons/apple-touch-icon.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/aem-forms-aep-connector.html"
  },
  "articleSection": "AEM Forms",
  "keywords": "AEM Forms, Adobe Experience Platform, XDM schema, data integration, form submission, customer profiles, personalization"
}
-->


