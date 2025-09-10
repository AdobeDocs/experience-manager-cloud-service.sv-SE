---
title: Lägg till Google reCAPTCHA i Forms i Universal Editor
description: Guide till hur man implementerar Google reCAPTCHA-skydd i Edge Delivery Services-formulär för att förhindra skräppost och automatiska attacker
feature: Edge Delivery Services
keywords: reCAPTCHA in forms, Using reCAPTCHA in Universal Editor, Add reCAPTCHA in forms, form security, spam protection
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---


# Lägg till Google reCAPTCHA i Forms i Universal Editor

Google reCAPTCHA hjälper till att skydda formulär genom att skilja mellan människor och automatiserade affärssystem. Den här guiden förklarar hur du implementerar både reCAPTCHA Enterprise- och Standard-versioner i Universal Editor.

**Mål:**

- Välj lämplig reCAPTCHA-lösning
- Konfigurera reCAPTCHA Enterprise eller Standard
- Lägg till reCAPTCHA i formulären
- Validera och testa implementeringen
- Övervaka och optimera prestanda

## Förutsättningar

Innan du börjar bör du kontrollera följande:

### Åtkomstkrav

- Åtkomst till redigering i AEM as a Cloud Service
- Universell redigeringsåtkomst med formulärredigeringsbehörigheter

### Tekniska krav

- Aktivt Google-konto
- För företag: Google Cloud Platform-projekt med fakturering aktiverad
- Standard: Google reCAPTCHA-konto
- Bekräftat domänägarskap för formulären

### Kunskapskrav

- Grundläggande förståelse för AEM Forms och Universal Editor
- Förtrogenhet med molntjänstkonfigurationer
- Förståelse av säkerhetsbegrepp för formulär

## Varför ska du använda reCAPTCHA i din Forms?

| ![Säkerhet](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Punktskydd](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Användarupplevelse](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Förbättrat skydd** | **Förebyggande av skräppost** | **Smidig användarupplevelse** |
| Skydda blanketterna mot bedrägliga aktiviteter och attacker | Förhindra att automatiska starter skickar in formulär | Invisible reCAPTCHA stör inte berättigade användare |

**Nyckelbegrepp:** reCAPTCHA använder maskininlärning för att analysera användarbeteende och tilldelar ett poängvärde (0,0 till 1,0) som anger sannolikheten för mänsklig interaktion. Högre poäng visar på humana användare, lägre poäng tyder på boter.

**Exempel:** En formulärhantering för momsberäkning som hanterar känsliga data kräver skydd mot automatiserade attacker. reCAPTCHA verifierar att inskickade data kommer från verkliga användare, inte från början.

## Välj din reCAPTCHA-lösning

Edge Delivery Services Forms har stöd för två Google reCAPTCHA-alternativ. Använd följande kriterier för att välja rätt lösning:

### Snabbbeslutshandbok

**Använd reCAPTCHA Enterprise om du har:**

- Formulär för högtrafik (>10 000 förfrågningar/månad)
- Strikta kompatibilitetskrav (GDPR, SOX, HIPAA)
- Behovet av avancerad analys och rapportering
- Budget för premiumsäkerhetsfunktioner
- Komplexa driftsättningar i flera domäner

**Använd reCAPTCHA-standard om du har:**

- Låg till måttlig trafik (&lt;10 000 förfrågningar/månad)
- Grundläggande säkerhetsbehov
- Begränsad budget (kostnadsfri nivå)
- Enkel konfiguration med en domän
- Är nytt för reCAPTCHA

### Detaljerad jämförelse

| **Funktion** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **Kostnad** | Betald (användarbaserad prissättning) | Kostnadsfritt |
| **Begärandegräns** | Obegränsad | 1 miljon förfrågningar/månad |
| **Avancerad analys** | Detaljerad rapportering | Endast grundläggande statistik |
| **Anpassade regler** | Kontospecifika regler | Endast globala regler |
| **Stöd för flera domäner** | Avancerad hantering | Grundläggande support |
| **SLA** | 99,9 % garanti för drifttid | Bästa försök |
| **Support** | Företagssupport | Community-stöd |
| **Efterlevnad** | Företag | Standardiserad kompatibilitet |

**Båda lösningarna innehåller:**

- Poängbaserad detektering (skala 0,0 till 1,0)
- Osynlig åtgärd (ingen användarinteraktion krävs)
- Maskinininlärningsdriven robotavkänning
- Riskbedömning i realtid

## Konfigurera reCAPTCHA Enterprise


+++ Steg 1: Förbered Google Cloud-miljön

**Krav:**

1. Google Cloud Project med fakturering aktiverad
2. Projekt-ID (från GCP-kontrollpanelen)
3. Domänverifiering för formulär
4. Administratörsåtkomst till GCP och AEM

**Inställningar:**

1. Skapa eller välja ett Google Cloud-projekt
   - Gå till [Google Cloud Console](https://console.cloud.google.com/)
   - Skapa ett nytt projekt eller välj ett befintligt
   - Anteckna ditt projekt-ID

2. Aktivera reCAPTCHA Enterprise API
   - Gå till API:er och tjänster > Bibliotek
   - Sök efter&quot;reCAPTCHA Enterprise API&quot;
   - Klicka på Aktivera

3. Skapa API-autentiseringsuppgifter
   - Gå till API:er och tjänster > Autentiseringsuppgifter
   - Klicka på Skapa autentiseringsuppgifter > API-nyckel
   - Kopiera och lagra API-nyckeln

4. Skapa webbplatsnyckel
   - Gå till Security > reCAPTCHA Enterprise
   - Klicka på Skapa nyckel
   - Välj poängbaserad nyckeltyp
   - Lägg till dina domäner
   - Ange tröskelpoäng (rekommenderas: 0,5)

**Kontrollpunkt för validering:** Kontrollera att du har:

- Projekt-ID
- API-nyckel
- Webbplatsnyckel
- Verifierad domän i Google Cloud

+++

+++ Steg 2: Konfigurera AEM Cloud Configuration Container

![Stegvis konfiguration av molnet](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*Bild: Aktivera molnkonfigurationer för formulärbehållaren*

**Inställningar:**

1. Åtkomst till konfigurationsläsaren
   - Logga in på din AEM-författarinstans
   - Gå till Verktyg > Allmänt > Konfigurationsläsaren

2. Aktivera molnkonfigurationer
   - Hitta formulärets konfigurationsbehållare
   - Välj egenskaper
   - Kontrollera molnkonfigurationer
   - Klicka på Spara och stäng

3. Verifiera konfiguration
   - Bekräfta att molnkonfigurationer visas i behållaregenskaperna

**Kontrollpunkt för validering:**

- Molnkonfigurationer aktiverade för din behållare
- Behållaren visas i Configuration Browser
- Egenskaperna visar att molnkonfigurationer är aktiverade

+++

+++ Steg 3: Konfigurera reCAPTCHA Enterprise Service i AEM

![reCAPTCHA Enterprise configuration screen](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*Bild: reCAPTCHA Enterprise-konfigurationsgränssnittet i AEM*

**Konfiguration:**

1. Åtkomst till konfiguration av reCAPTCHA
   - Gå till Verktyg > Molntjänster > reCAPTCHA
   - Välj formulärets konfigurationsbehållare
   - Klicka på Skapa

2. Konfigurera företagsinställningar
   - Titel: beskrivande namn (t.ex. &quot;Production reCAPTCHA&quot;)
   - Namn: Systemnamn (autogenererat eller anpassat)
   - Version: Välj ReCAPTCHA Enterprise
   - Projekt-ID: Ange ditt projekt-ID för Google Cloud
   - Webbplatsnyckel: Ange webbplatsnyckeln från Google Cloud
   - API-nyckel: Ange din Google Cloud API-nyckel
   - Nyckeltyp: Välj poängbaserad webbplatsnyckel

3. Ange säkerhetströskel
   - Tröskelpoäng: Ange mellan 0,0 och 1,0
   - Rekommenderade värden:
      - 0.7-0.9: Hög säkerhet (kan blockera vissa berättigade användare)
      - 0.5-0.7: Balanserad säkerhet (rekommenderas)
      - 0.1-0.5: Lägre säkerhet (tillåter fler användare)

4. Spara och publicera
   - Klicka på Skapa för att spara konfigurationen
   - Klicka på Publicera för att göra den tillgänglig

**Kontrollpunkt för validering:**

- Konfigurationen har sparats
- Alla obligatoriska fält har slutförts
- Konfiguration publicerad och synlig
- Inga felmeddelanden

+++

## Konfigurera reCAPTCHA Standard

+++Steg 1: Hämta API-nycklar för reCAPTCHA (se information)

>[!IMPORTANT]
>
> Edge Delivery Services Forms stöder endast reCAPTCHA v2 (Score-based). Använd inte kryssrutans version.

**Nyckelgenerering:**

1. Öppna Google reCAPTCHA-konsolen

   - Gå till [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin)
   - Logga in med ditt Google-konto

2. Skapa ny plats

   - Klicka på + för att lägga till en ny plats
   - Etikett: Ange ett beskrivande namn
   - reCAPTCHA-typ: Välj reCAPTCHA v2 > &quot;Jag är inte en robot&quot; Osynlig
   - Domäner: Lägg till formulärdomäner
   - Acceptera villkoren och klicka på Skicka

3. Samla in dina nycklar

   - Platsnyckel: Kopiera webbplatsnyckeln (offentlig nyckel)
   - Hemlig nyckel: Kopiera den hemliga nyckeln (privat nyckel)

**Kontrollpunkt för validering:**

- Webbplatsen har skapats i reCAPTCHA-konsolen

- Webbplatsnyckeln har hämtats

- Hemlig nyckel har hämtats

- Domäner har lagts till och verifierats

+++

+++Steg 2: Konfigurera AEM Cloud Configuration Container (se information)

Följ samma procedur som i Enterprise-konfigurationen:

1. Aktivera molnkonfigurationer i Configuration Browser

2. Verifiera behållarkonfiguration

3. Bekräfta att inställningarna sparas

+++

+++Steg 3: Konfigurera standardtjänsten reCAPTCHA i AEM (se information)

![reCAPTCHA Standard configuration screen](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*Bild: konfigurationsgränssnittet reCAPTCHA Standard i AEM*

**Konfiguration:**

1. Åtkomst till konfiguration av reCAPTCHA

   - Gå till Verktyg > Molntjänster > reCAPTCHA
   - Välj formulärets konfigurationsbehållare
   - Klicka på Skapa

2. Konfigurera standardinställningar

   - Titel: beskrivande namn (t.ex. &quot;Standard reCAPTCHA&quot;)
   - Namn: Systemnamn (autogenererat eller anpassat)
   - Version: Välj ReCAPTCHA v2
   - Webbplatsnyckel: Ange din Google reCAPTCHA-webbplatsnyckel
   - Hemlig nyckel: Ange din hemliga nyckel för Google reCAPTCHA

3. Spara och publicera

   - Klicka på Skapa för att spara konfigurationen
   - Klicka på Publicera för att göra den tillgänglig

**Kontrollpunkt för validering:**

- Konfiguration skapad utan fel

- Båda nycklarna har angetts korrekt

- Konfigurationen har publicerats

- Konfigurationen visas i listan

+++

## Lägg till reCAPTCHA i ditt formulär

När du har konfigurerat tjänsten reCAPTCHA lägger du till skydd i formuläret enligt följande:

![Lägger till komponenten reCAPTCHA i ett formulär](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*Figur: Lägga till komponenten Osynlig Captcha i formuläret*

+++&#x200B;1. Öppna formulär i Universal Editor
Gå till formuläret i AEM Sites och klicka på Redigera för att öppna det i Universell redigerare. Vänta tills redigeraren har lästs in.

- Gå till ditt formulär i AEM Sites
- Klicka på Redigera för att öppna i Universal Editor
- Vänta tills redigeraren har lästs in
+++

+++&#x200B;2. Leta reda på formulärstrukturen
I innehållsträdet (den vänstra panelen) hittar du avsnittet Adaptivt formulär och expanderar formulärstrukturen så att insättningspunkter visas.

- I innehållsträdet (den vänstra panelen) hittar du sektionen Adaptiv form
- Expandera formulärstrukturen så att insättningspunkter visas
+++

+++&#x200B;3. Lägg till reCAPTCHA-komponent
Lägg till komponenten Captcha (osynlig) i formuläret.

- Klicka på ikonen Lägg till (+) i formuläravsnittet
- Välj Captcha (osynlig) i komponentlistan
- Du kan också dra och släppa komponenten från komponentpanelen
+++

+++&#x200B;4. Konfigurera komponent (valfritt)
Markera den nya Captcha-komponenten och verifiera att den använder din reCAPTCHA-konfiguration.

- Markera den nya Captcha-komponenten
- Verifiera på egenskapspanelen att den använder din reCAPTCHA-konfiguration
- Ingen ytterligare konfiguration krävs för grundläggande konfiguration
+++

+++&#x200B;5. Publicera dina ändringar
Publicera ändringarna och verifiera att det inte finns några fel.

- Klicka på Publicera i Universal Editor
- Vänta på bekräftelse
- Kontrollera att inga fel visas
+++

### Verifiera implementering

Ditt skyddade formulär finns nu på:

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**Exempel-URL:**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-us-form
```
