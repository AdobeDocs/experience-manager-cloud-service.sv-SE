---
title: Skydda din Forms med reCAPTCHA - en visuell guide
description: Lär dig hur du enkelt kan lägga till Google reCAPTCHA i dina Edge Delivery Services-formulär för att förhindra skräppost och robotmaterial
feature: Edge Delivery Services
keywords: reCAPTCHA in forms, Using reCAPTCHA in Universal Editor, Add reCAPTCHA in forms, form security, spam protection
role: Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---


# Skydda din Forms mot skräppost med Google reCAPTCHA

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> med ditt GitHub-organisationsnamn och databasnamn.</span>



## Varför ska du använda reCAPTCHA i formulären?

| ![Säkerhet](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Punktskydd](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Användarupplevelse](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Förbättrat skydd** | **Förebyggande av skräppost** | **Smidig användarupplevelse** |
| Skydda era formulär mot bedrägliga aktiviteter och skadliga attacker | Slipp automatiserade bollar från att översvämma era formulär med irrelevant eller skadligt innehåll | Den osynliga reCAPTCHA-funktionen fungerar bakom kulisserna utan att störa berättigade användare |

Ett skatteberäkningsformulär med känslig ekonomisk information behöver till exempel skyddas mot missbruk. reCAPTCHA verifierar att inskickade data kommer från verkliga användare, inte från automatiserade system.

## Välj din reCAPTCHA-lösning

Edge Delivery Services Forms har stöd för två Google reCAPTCHA-alternativ:

| ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/enterprise.svg) | ![reCAPTCHA Standard](/help/edge/docs/forms/universal-editor/assets/standard.svg) |
|:-------------:|:-------------:|
| [**reCAPTCHA Enterprise**](#set-up-recaptcha-enterprise) | [**reCAPTCHA Standard**](#set-up-recaptcha-standard) |
| Förstklassig upptäckt av bedrägeri i företagsklass med ytterligare funktioner och anpassningar | Kostnadsfri tjänst med poängbaserad identifiering som fungerar osynligt i bakgrunden |
| Bäst för: Stora organisationer med komplexa säkerhetsbehov | Bäst för: Små till medelstora projekt med grundläggande skyddsbehov |

Båda alternativen använder poängbaserad identifiering (0,0 till 1,0) för att identifiera mänsklig interaktion jämfört med robotinteraktion utan att störa användarupplevelsen.

## Konfigurera reCAPTCHA Enterprise

### Steg 1: Hämta dina Google Cloud-autentiseringsuppgifter

Innan du konfigurerar reCAPTCHA Enterprise behöver du:

- Ett [Google Cloud-projekt](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) med ditt [projekt-ID](https://support.google.com/googleapi/answer/7014113)
- [reCAPTCHA Enterprise API aktiverat](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) för ditt projekt
- En [API-nyckel](https://console.cloud.google.com/apis/credentials) för autentisering
- En [webbplatsnyckel](https://console.cloud.google.com/security/recaptcha) för din domän

### Steg 2: Skapa en molnkonfigurationsbehållare

![Stegvis konfiguration av molnet](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Logga in på din AEM-författarinstans
2. Navigera till **Verktyg** > **Allmänt** > **Konfigurationsläsaren**
3. Hitta ditt formulär och välj **Egenskaper**
4. Aktivera **molnkonfigurationer** i dialogrutan
5. Spara och publicera konfigurationen

### Steg 3: Konfigurera reCAPTCHA Enterprise Service

![reCAPTCHA Enterprise configuration screen](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Gå till **Verktyg** > **Molntjänster** > **reCAPTCHA**
2. Navigera till formuläret och klicka på **Skapa**
3. I dialogrutan:
   - Välj **ReCAPTCHA Enterprise**-version
   - Ange en titel och ett namn
   - Lägg till ditt projekt-ID, webbplatsnyckel och API-nyckel
   - Välj **Poängbaserad webbplatsnyckel** som nyckeltyp
   - Ange ett tröskelvärde (0-1) för att skilja människor från bottnar
4. Klicka på **Skapa** och publicera konfigurationen

## Konfigurera reCAPTCHA Standard

### Steg 1: Hämta API-nycklar

Innan du startar [hämtar du ett API-nyckelpar för reCAPTCHA](https://www.google.com/recaptcha/admin) (platsnyckel och hemlig nyckel) från Google reCAPTCHA-konsolen.

>[!IMPORTANT]
>
>Edge Delivery Services Forms stöder endast **reCAPTCHA Score-baserad** version.

### Steg 2: Skapa en molnkonfigurationsbehållare

Följ samma steg som i Enterprise-versionen för att skapa och publicera en molnkonfigurationsbehållare.

### Steg 3: Konfigurera standardtjänsten reCAPTCHA

![reCAPTCHA Standard configuration screen](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Gå till **Verktyg** > **Molntjänster** > **reCAPTCHA**
2. Navigera till formuläret och klicka på **Skapa**
3. I dialogrutan:
   - Välj version **ReCAPTCHA v2**
   - Ange en titel och ett namn
   - Lägg till din webbplatsnyckel och hemlig nyckel
4. Klicka på **Skapa** och publicera konfigurationen

## Lägg till reCAPTCHA i formuläret

Nu när du har konfigurerat reCAPTCHA är det dags att lägga till det i formuläret:

![Lägger till komponenten reCAPTCHA i ett formulär](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

1. Öppna formuläret i Universal Editor
2. Navigera till sektionen Adaptivt formulär i innehållsträdet
3. Klicka på ikonen **Lägg till** och välj **Captcha (osynlig)** i listan med adaptiva formulärkomponenter
   - *Du kan också dra och släppa komponenten i formuläret*
4. Klicka på **Publicera** för att uppdatera formuläret med reCAPTCHA-skydd

Formuläret är nu skyddat! Se den här:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name>`

![Formulär med reCAPTCHA-skydd aktiverat](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Validerar din reCAPTCHA-integrering

När du har lagt till reCAPTCHA i formuläret är det viktigt att verifiera att det fungerar som det ska. Så här validerar du implementeringen:

### Visual verification

Medan reCAPTCHA v2 (Score-based) fungerar osynligt kan du bekräfta dess närvaro genom att:

1. **Inspektera sidkällan**: Högerklicka på formulärsidan och välj Visa sidan Source.
   - Leta efter om skriptet reCAPTCHA ingår i webbplatsnyckeln
   - Exempel: `<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>`

2. **Kontrollera nätverksförfrågningar**: Använda verktyg för webbläsarutvecklare (F12)
   - Skicka formuläret och sök efter nätverksförfrågningar till `google.com/recaptcha`
   - Dessa förfrågningar indikerar att reCAPTCHA är aktivt i ditt formulär

### Funktionstestning

Så här kontrollerar du att reCAPTCHA faktiskt skyddar ditt formulär:

1. **Normalt sändningstest**:
   - Fyll i formuläret med giltiga data
   - Skicka in formuläret i normal mänsklig takt
   - Verifiera att formuläret har skickats

2. **Punktliknande beteendetest**:
   - Öppna formuläret i ett inkognito/privat fönster
   - Fyll i formuläret extremt snabbt (automatiserat beteende)
   - Skicka flera gånger i snabb följd
   - Om reCAPTCHA fungerar kan dessa inskickade data vara blockerade eller flaggade

3. **Kontrollera inskickningsposter för formulär**:
   - Granska inskickade data
   - Varje tävlingsbidrag ska innehålla en reCAPTCHA-poäng
   - Poäng närmare 1.0 indikerar troliga användare
   - Poäng närmare 0.0 indikerar möjlig robotaktivitet

### Använda administratörskonsolen för Google reCAPTCHA

För Enterprise-användare innehåller Google Cloud Console detaljerade analyser:

1. Gå till [Google Cloud Console](https://console.cloud.google.com/)
2. Navigera till **Säkerhet** > **reCAPTCHA**
3. Välj webbplatsnyckel
4. Granska bedömningsdiagrammen och statistiken
5. Leta efter:
   - Trafikmönster
   - Poängfördelningar
   - Potentiellt bedrägliga aktiviteter

För användare av Standard reCAPTCHA finns grundläggande statistik i [reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin/).

### Justera implementeringen

Baserat på dina valideringsresultat:

- Om berättigade användare blockeras bör du överväga att sänka tröskelvärdet
- Om du fortfarande får skräppost bör du överväga att öka tröskelvärdet
- Kontrollera konfigurationen av reCAPTCHA och se till att alla nycklar är korrekt angivna för beständiga problem

Kom ihåg att reCAPTCHA använder maskininlärning för att förbättra bilden över tiden, så att effektiviteten kan öka när man lär sig platsens trafikmönster.

## Felsökning och vanliga frågor

| ![Fråga](/help/edge/docs/forms/universal-editor/assets/question.svg) | ![Svar](/help/edge/docs/forms/universal-editor/assets/answer.svg) |
|:-------------:|:-------------:|
| **Vad händer om jag inte skapar någon reCAPTCHA-konfiguration?** | Systemet söker efter en konfiguration i den globala behållaren. Om det inte finns något fel får du ett felmeddelande. |
| **Vad händer om jag skapar flera konfigurationer?** | Systemet använder automatiskt den första konfigurationen som skapas. |
| **Varför syns inte mina ändringar på den publicerade URL:en?** | Kontrollera att du publicerar om formuläret när du har gjort ändringarna. |
| **Vilka reCAPTCHA-tjänster stöds?** | Edge Delivery Services Forms stöder endast poängbaserade reCAPTCHA-tjänster. |

## Nästa steg

Nu när du har skyddat formuläret med reCAPTCHA:

- **Verifiera implementeringen**: Följ [valideringsstegen](#-validating-your-recaptcha-integration) för att säkerställa att reCAPTCHA fungerar korrekt
- **Övervakningsprestanda**: Kontrollera regelbundet om Google reCAPTCHA-instrumentpanelen innehåller misstänkta aktiviteter och poängfördelningar
- **Finjustera inställningarna**: Justera tröskelvärdet baserat på dina säkerhetsbehov och feedback från användarupplevelsen
- **Håll dig uppdaterad**: Håll din reCAPTCHA-implementering aktuell med Google senaste säkerhetsrekommendationer
- **Undervisa ditt team**: Dela kunskap om hur reCAPTCHA fungerar och hur analyserna kan tolkas
- **Samla in feedback**: Övervaka användarupplevelsen för att säkerställa att berättigade användare inte blockeras

Kom ihåg att effektivt formulärskydd är en pågående process som kräver regelbunden övervakning och justeringar.


