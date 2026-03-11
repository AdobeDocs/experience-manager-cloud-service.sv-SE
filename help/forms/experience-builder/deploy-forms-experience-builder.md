---
title: Installera och konfigurera Forms Experience Builder
description: Lär dig använda Forms Experience Builder för att skapa och hantera formulär med progressiv publicering för alla användartyper
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Gäller AEM Forms)."
exl-id: 977f227e-e941-4797-ba74-53d5b8c60ca9
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 0%

---

# Installera och konfigurera Forms Experience Builder

>[!NOTE]
>
> Forms Experience Builder är tillgängligt via ett program för tidig åtkomst. Kontrollera att du har begärt och beviljats åtkomst innan du börjar. Fullständiga anvisningar finns i [Onboarding](product-overview.md#onboarding) -informationen.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Dokumentationen testas för närvarande mot produkten och kan uppdateras och revideras. Funktioner, kommandon och exempel kan ändras allt eftersom Forms Experience Builder fortsätter att utvecklas under programmet för tidig åtkomst.

Den här omfattande guiden hjälper dig att komma igång med att skapa och hantera formulär med hjälp av konverteringsbaserad AI-teknik. Oavsett om du är nybörjare som vill skapa ditt första formulär eller en avancerad användare som vill utnyttja avancerade funktioner hittar du detaljerad information och praktiska exempel som vägleder dig genom funktionerna i Forms Experience Builder.

## Krav och inställningar

### Åtkomstkrav

Innan du använder Forms Experience Builder måste du se till att:

* **Åtkomst till Forms Experience Builder** - tillgänglig via programmet för tidig åtkomst
* **AEM Forms as a Cloud Service** - Designmiljö för produktion med adaptiva Forms Core-komponenter
* **Grundläggande förståelse** - Förståelse med formulärkoncept och affärskrav

### Kontrollera att formulär är aktiverade

Kontrollera att [AEM Forms är aktiverat för din miljö](/help/forms/setup-forms-cloud-service.md) innan du använder Forms Experience Builder.

### Konfigurera din miljö

Konfigurationsprocessen beror på hur AEM Forms implementeras. Välj den sökväg som matchar ditt projekt.

**För Edge Delivery Services**

Om du använder Edge Delivery Services Forms och i första hand använder Universal Editor. [Förbered ditt projekt för Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md). Detta är en engångskonfiguration som aktiverar Forms Experience Builder.

**För kärnkomponentbaserade formulär**

Om du använder Adaptiv Forms baserad på kärnkomponenter i AEM-redigeringsmiljö kontrollerar du att [adaptiva Forms Core-komponenter är aktiverade](/help/forms/enable-adaptive-forms-core-components.md) för din miljö.



## Snabbstart

### Få åtkomst till formulärupplevelseverktyget

Du kan komma åt Forms Experience Builder från tre primära platser, beroende på arbetsflöde och formulärtyp.


**1. Adaptiv Forms Editor (för kärnkomponenter)**

Du kan starta verktyget direkt när du redigerar ett visst formulär.

1. Navigera till **AEM > Forms > Forms &amp; Documents**.
1. [Skapa ett nytt formulär med en Core Components-mall](/help/forms/creating-adaptive-form-core-components.md) eller öppna ett befintligt.
1. Välj ikonen **Forms Experience Builder** i redigerarens verktygsfält för att öppna konversationsgränssnittet.

   ![Ikon för AI-assistenten*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

**1. Universal Editor (för Edge Delivery Services Forms)**

För blanketter som levereras via Edge Delivery Services är verktyget integrerat i den universella redigeraren.

1. Öppna Edge Delivery Services-formuläret i Universell redigerare.
2. Välj ikonen **Forms Experience Builder** på den högra panelen för att starta konversationsgränssnittet.

### Ditt första formulär

| Exempel på konversation |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Prova den här konversationen för att skapa ett omfattande kontaktformulär (baserat på Summit-demo):**<br><br>**Du:**&quot;Skapa ett kontaktformulär för att samla in personlig information, inklusive fullständigt namn, e-postadress, telefonnummer, företagsnamn, jobbtitel och ett meddelandefält för frågor&quot;<br><br>**AI:** Välj en mall<br>    En listruta där du kan välja en mall <br><br>**AI:** Välj ett tema <br>    En listruta där du kan välja ett tema <br><br>**AI:** Skapa formulär | ![Ditt första formulär](/help/edge/docs/forms/assets/create-form.png) |
| <br>**AI:** Öppna skapat formulär | </br> Formuläret skapas och öppnas i redigeraren |


### Grundläggande kommandon

| Symbol | Syfte | Exempel på användning |
|--------|---------|---------------|
| `/` | Snabbåtgärder och genvägar | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Referera till befintliga formulärfält | `@email`, `@firstName`, `Make @phoneNumber required` |
| Oformaterad text | Naturlig konversation | &quot;Lägg till ett obligatoriskt telefonnummerfält&quot;, &quot;Skapa validering för e-post&quot; |

**Exempel på specifika kommandon:**

* `/create-form customer survey` - Skapar ett nytt kundundersökningsformulär
* `/add-field @email validation` - Lägger till validering i befintligt e-postfält
* `/create-rule show @spouse if @maritalStatus equals married` - Skapar villkorlig logik
* `/configure-submit to email support@company.com` - Konfigurera e-postinlämning
* `/help multi-step forms` - Få hjälp med att skapa formulär i flera steg

### Tips för framgång

* **Var specifik**: Det fungerar bättre att lägga till ett obligatoriskt e-postfält med validering än att lägga till e-post
* **Referera till befintliga fält**: Använd `@fieldName` när du ändrar formulär
* **Be om hjälp**: Skriv `/help` följt av din fråga
* **Upprepa**: Gör en ändring i taget för bästa resultat


## Olika sätt att börja skapa ett formulär

### Börja med naturliga språkfrågor

Beskriv dina formulärkrav på ett naturligt språk så genererar Forms Experience Builder den fullständiga formulärstrukturen:

**Exempel:**

* &quot;Skapa ett låneansökningsformulär med personlig information, ekonomisk information och dokumentöverföringar&quot;
* &quot;Bygg ett formulär för kundfeedback med betyg, kommentarer och produktkategorier&quot;
* &quot;Jag behöver ett registreringsformulär i flera steg för en konferens med betalningshantering&quot;


### Viktiga interaktioner

#### Lägga till formulärelement

**Grundläggande tillägg:**

    👤 Du: &quot;Lägg till ett avsnitt för personlig information&quot;
    👤 Du: &quot;Inkludera en filöverföring för CV&quot;
    👤 Du: &quot;Lägg till en listruta för val av land&quot;

**Detaljerade specifikationer:**

    👤 Du:&quot;Lägg till en personlig informationspanel med fält för fullständigt namn, födelsedatum, telefonnummer och e-postadress&quot;
    👤 Du:&quot;Inkludera en säker filuppladdningskomponent för dokument, begränsad till PDF-filer under 5 MB&quot;
    👤 Du:&quot;Lägg till en landsmeny med alternativ för USA, Kanada, Storbritannien och Tyskland&quot;

#### Skapa dynamiskt beteende

**Enkel logik:**

    👤 Du: &quot;Visa ytterligare fält när &quot;Annat&quot; har valts&quot;
    🤖 AI: &quot;Skapade en villkorsregel som visar ytterligare fält när &quot;Annat&quot; har valts&quot;
    
    👤 Du: &quot;Gör e-postfältet obligatoriskt&quot;
    🤖 AI: &quot;Uppdaterade e-postfältet som ska behövas med validering&quot;
    
    👤 Du: &quot;Beräkna summan automatiskt&quot;
    🤖 AI: &quot;Beräkningslogik har lagts till automatiskt för beräkning av summor&quot; 

**Komplexa affärsregler:**

    👤 Du: &quot;Visa informationsfälten för make/maka endast när äktenskapsstatus är inställd på &quot;Gift&quot; 
    🤖 AI: &quot;Skapade en villkorlig regel som visar makefält baserat på civilstånd&quot;
    
    👤 Du: &quot;Beräkna totalkostnaden genom att multiplicera kvantitet och pris och sedan lägga till 10 % skatt&quot;
    🤖 AI: &quot;Tillagd beräkningslogik med kvantitet, pris och skatteberäkning&quot;
    
    👤 Du:&quot;Aktivera bara skicka-knappen när alla obligatoriska fält har fyllts i och villkoren har accepterats&quot; 
    🤖 AI:&quot;Skapad valideringslogik som endast möjliggör sändning när alla villkor är uppfyllda&quot; 

#### Formulärlayout och design

**Layoutändringar:**

    👤 Du: &quot;Gör det här till ett flerstegsformulär&quot;
    🤖 AI: &quot;Konverterade formuläret till en progressiv layout med navigering&quot;
    
    👤 Du: &quot;Ordna fält i två kolumner&quot;
    🤖 AI: &quot;Uppdaterade layouten så att fält visas i en tvåkolumnslayout&quot;
    
    👤 Du: &quot;Konvertera till en dragspelslayout&quot;
    🤖 AI: &quot;Omformade formuläret så att det används i accordion formatavsnitt&quot;

**Designförbättringar:**

    👤 Du: &quot;Skapa ett guideliknande formulär med 3 steg: personlig information, inställningar och granskning&quot;
    🤖 AI: &quot;Skapade ett guideformulär med tre tydliga steg och navigering&quot;
    
    👤 Du: &quot;Ordna adressfälten i en kompakt layout med två kolumner&quot;
    🤖 AI: &quot;Organiserade adressfält i ett kompakt format med två kolumner&quot;
    
    👤 Du: &quot;Uppdatera layouten så att den matchar den bifogade trådramen&quot; 
    🤖 AI: &quot;Ändrade layouten så att den matchar den angivna designreferensen&quot; 

### Skicka konfiguration

Forms Experience Builder kan konfigurera olika slutpunkter för att koppla formulären till externa system och tjänster:

| Typ av överföringsåtgärd | Installationskommando | Användningsfall |
|------------------|---------------|----------|
| **E-post** | &quot;Skicka formulär till e-post&quot; | Anmälningar och bekräftelser för inskickande av formulär |
| **REST API** | &quot;Skicka till REST-slutpunkt&quot; | Anpassade program och tredjepartssystem |
| **Molnlagring** | &quot;Spara till Azure/SharePoint&quot; | Dokumentlagring och filhantering |
| **Arbetsflöde** | &quot;Anslut till Power Automate&quot; | Automatisering och godkännande av affärsprocesser |
| **Marknadsföring** | Integrera med Marketo | Leadhantering och automatiserad marknadsföring |

**Exempel på konfiguration av avancerad sändning:**

    👤 Du:&quot;Skicka formuläröverföringar till hr@company.com och skapa ett ärende i vårt CRM-system&quot;
    🤖 AI:&quot;Konfigurerad e-postöverföring och CRM-sändningsåtgärd&quot;
    
    👤 Du:&quot;Skicka data till REST API-slutpunkten och aktivera det nya kundarbetsflödet&quot;
    🤖 AI:&quot;Konfigurera REST API-sändning med arbetsflödesutlösare&quot;
    
    👤 Du:&quot;Skicka e-postsvar till säljteamet och lägg till leadet på vår plattform för marknadsföring&quot; 
    🤖 AI:&quot;Konfigurerad flerkanalsöverföring med e-post- och marknadsföringsautomatisering&quot; 





## Avancerade formuläråtgärder


### Skapa komplexa regler

Skapa sofistikerad validering och affärslogik som svarar på användarinteraktioner och säkerställer dataintegritet:

    👤 Du: &quot;Visa endast adressavsnittet om användaren väljer &quot;Leverera till annan adress&quot; 
    🤖 AI: &quot;Skapade en villkorsregel som visar/döljer adresspanelen baserat på kryssruteval&quot;

### Skapa blanketter i flera steg

    👤 Du:&quot;Skapa ett progressivt formulär med 3 steg: personlig information, inställningar, bekräftelse&quot;
    🤖 AI:&quot;Skapade ett progressivt formulär med navigering mellan steg och validering vid varje steg&quot;

### Avancerade fälttyper

* Filöverföring med validering och storleksbegränsningar för dokumenthantering
* Datumväljare med begränsningar och affärsregler för schemaläggning
* Listrutor med dynamiska alternativ som ändras baserat på användarval
* Alternativknappar med villkorlig logik för komplexa beslutsträd


### Konvertera PDF till blanketter

    👤 Du:&quot;Konvertera denna PDF till ett interaktivt formulär&quot;
    🤖 AI:&quot;Analyserade PDF och skapade ett formulär med lämpliga fälttyper och validering&quot;





## Hjälp och utbildning

Forms Experience Builder kan även lära dig mer om AEM Forms funktioner:

### Ställ frågor som:

* &quot;Hur skapar jag ett flerstegsformulär?&quot;
* &quot;Vad är skillnaden mellan paneler och avsnitt?&quot;
* &quot;Hur konfigurerar jag e-postmeddelanden?&quot;
* &quot;Vilka är de bästa sätten för mobilvänliga formulär?&quot;
* &quot;Hur använder jag teman i mina formulär?&quot;

### Få hjälp om:

* AEM Forms koncept och terminologi
* Stegvisa instruktioner för komplexa funktioner
* God praxis och rekommendationer
* Felsöka vanliga problem


Mer support finns i [Forms Experience Builder Prompt Library](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md) eller så kontaktar du systemadministratören för teknisk hjälp.
