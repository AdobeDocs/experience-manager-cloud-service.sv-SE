---
title: Komma igång med redigeraren för interaktiv kommunikation
description: Med interaktiv kommunikation kan organisationer utforma och leverera personaliserad, datadriven kommunikation.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Komma igång med redigeraren för interaktiv kommunikation

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

Med **Interactive Communication (IC) Editor** i Adobe Experience Manager (AEM) Forms kan organisationer utforma och leverera personaliserade, datadrivna dokument som kontoutdrag, fakturor och brev i digitala och tryckta kanaler. Den här guiden ger dig en översikt över hur du kommer igång - från introduktion till navigering i gränssnittet för IC Editor.


## Onboarding och Access

### Åtkomstkrav

Om du vill använda interaktiv kommunikation måste du kontrollera att AEM Forms as a Cloud Service-miljön innehåller **AEM Forms-tillägget** och att ditt konto har rätt behörighet.

### Verifiera webbläsaren

Om du vill veta vilka webbläsare och klientplattformar som stöds kan du följa den länkade artikeln [Klientplattformar som stöds](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/supported-platforms)

>[!NOTE]
>
> **Stöd för webbläsare med snabba releasecykler:**
> Uppdateringar av Firefox, Chrome och Edge regelbundet. Adobe vill behålla den supportnivå som anges ovan för kommande versioner av dessa webbläsare.

### Konfigurera användarroller och behörigheter

Åtkomsten till IC Editor-funktioner styrs av [användarroller i AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions). Nedan följer de viktigaste rollerna för att skapa och hantera interaktiv kommunikation:

| **Roll** | **Beskrivning** | **Nyckelbehörigheter** |
| --------------------- | ---------------------------------------------------------- | -------------------------------------------- |
| **Formulärförfattare** | Skapa och redigera interaktiv kommunikation. | Skapa, redigera, förhandsgranska och publicera IC:er. |
| **Mallförfattare** | Utformar återanvändbara mallar för interaktiv kommunikation. | Skapa och lås mallar, definiera layouter. |
| **Administratör** | Hanterar användaråtkomst, behörigheter och konfigurationer. | Tilldela roller, hantera mallar, publicera konc. |
| **FDM-författare** | [Skapar och hanterar FDM (Form Data Models)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models) för dataintegrering. | Skapa, redigera och konfigurera datakällor och modeller. |

>[!NOTE]
>
> Se till att användarna ingår i rätt AEM-grupper (t.ex. `forms-user`, `fdm-author`, `template-authors`) för att få tillgång till motsvarande funktioner.

## Åtkomst till IC Editor

1. Logga in på din **AEM Forms as a Cloud Service**-instans.
2. Navigera till **Forms > Interaktiv kommunikation**.
3. Klicka på **Skapa** → **Interaktiv kommunikation**.
4. Välj en **mall**, konfigurera datakällor och klicka på **Skapa** för att öppna den **interaktiva kommunikationsredigeraren**.

Redigeraren har en enhetlig miljö för att utforma, förhandsgranska och hantera både tryck- och webbversioner av kommunikation.

## Navigera i gränssnittet

Gränssnittet **Interactive Communication Editor** är utformat för att ge författare intuitiv åtkomst till alla designverktyg och konfigurationsalternativ.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/navigate-the-interface.png)

### &#x200B;1. Övre verktygsfält

![Sök efter IC Docu](/help/forms/interactive-communication/assets/tool-bar.png)

**Plats:** Avsnittet längst upp

**Syfte:** Tillhandahåller miljöåtkomst och globala åtgärder.

**Innehåller:**

Visar **Adobe Experience Cloud-miljön** (t.ex. Förproduktion) tillsammans med **projekttiteln**, **Beta feedback**, **meddelanden** och **profilkontroller** för hantering av användarinställningar och miljöåtkomst.

### &#x200B;2. Flikfält (Design-/mallflikar och filkontroller)

![Sök efter IC Docu](/help/forms/interactive-communication/assets/tab-bar.png)

**Plats:** Under den övre rubriken

**Syfte:** Hantera vyer och kommunikationsfiler.

**Innehåller:**

**Tabbar:** Växla mellan **Designvy** och **Mallsidvy** för layout och återanvändbar elementdesign

**Filnamn:** Visar den aktuella kommunikationens rubrik (t.ex. ic-11)

**Visningskontroller:** Alternativ som regel, skapa, zooma (85 %), ångra/gör om, ta bort, PDF-förhandsvisa och spara

### &#x200B;3. Vänster panel (navigerings- och komponentverktyg)

![Sök efter IC Docu](/help/forms/interactive-communication/assets/left-panel.png)

**Plats:** Gränssnittets vänstra sida

**Syfte:** Få åtkomst till projektstruktur, återanvändbara resurser och databindningar.

**Innehåller:**

* **Hemsida:** Tar användaren till huvudstartskärmen för Interactive Communication (IC), där du kan visa och hantera befintliga IC:er och mappar.

* **Menypanelen:** Visar visningsrelaterade alternativ som linjaler, objektgränser, Fäst mot rutnät, Fäst mot funktionsobjekt och funktionen Importera XDP.

* **Hierarkivy:** Visar komponentstrukturen i kommunikationen och visar ordningen för sidor, paneler och delformulär.

* **Komponentbibliotek:** Innehåller designelement som text, bild, delformulär och streckkod som kan dras till arbetsytan.

* **Fragment:** Möjliggör återanvändning av fördefinierade design- och innehållsblock i flera olika kommunikationer.

* **Datamodell:** Ansluter kommunikationen till underliggande FDM-modeller (Form Data Models) för bindning av dynamiska data.

### &#x200B;4. Central Workspace (arbetsyta för design)

![Sök efter IC Docu](/help/forms/interactive-communication/assets/canvas.png)

**Plats:** Gränssnittets mitt

**Syfte:** Primär arbetsyta för design av interaktiv kommunikation.

**Funktioner:**

* Dra och släpp komponenter från biblioteket

* Ordna och formatera visuell layout

* Lägga till eller redigera sidor, delformulär och fält

* Navigera mellan sidor (t.ex. &quot;1 av 1&quot;) med kontrollerna längst ned till vänster

* Förhandsgranska den slutliga layouten före publicering

### &#x200B;5. Högerpanel (egenskapspanelen)

![Sök efter IC Docu](/help/forms/interactive-communication/assets/right-panel.png)

**Plats:** Skärmens högra sida

**Syfte:** Anpassa komponentens beteende och stil.

**Innehåller:**

* Allmänna inställningar (Namn, Typ, Flödat/Placerat)

* Alternativ för layout och utseende

* Kontroller för sidnumrering, position, närvaro och databindning