---
title: Skapa och lägga till anpassade funktioner i ett adaptivt formulär
description: AEM Forms har stöd för anpassade funktioner, som gör att användare kan skapa och använda sina egna funktioner i regelredigeraren.
keywords: Lägg till en anpassad funktion, använd en anpassad funktion, skapa en anpassad funktion, använd anpassad funktion i regelredigeraren.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: e7ab4233-2e91-45c6-9377-0c9204d03ee9
source-git-commit: 747203ccd3c7e428e2afe27c56e47c3ec18699f6
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Skapa en anpassad funktion för ett adaptivt formulär baserat på kärnkomponenter

Adaptiv Forms baserad på kärnkomponenter ger dynamiska användarupplevelser genom att justera innehåll och beteende baserat på användarindata. Med anpassade funktioner kan utvecklare utöka funktionaliteten och säkerställa att formulären uppfyller specifika krav. Genom att integrera anpassade funktioner kan utvecklare implementera komplex logik, automatisera processer och införa unika interaktioner som passar specifika affärskrav eller användarförväntningar. Det säkerställer att blanketterna inte bara anpassar sig till olika förhållanden utan också ger en mer exakt och effektiv lösning för olika användningsområden.
I den här artikeln får du hjälp med att skapa anpassade funktioner för Adaptive Forms med hjälp av kärnkomponenter.

## Överväganden

* `parameter type` och `return type` stöder inte `None`.

* De funktioner som inte stöds i den anpassade funktionslistan är:
   * Generatorfunktioner
   * Async-/Await-funktioner
   * Metoddefinitioner
   * Klassmetoder
   * Standardparametrar
   * Restparametrar

## Krav för att skapa en anpassad funktion

Innan du börjar lägga till en anpassad funktion i din adaptiva Forms måste du se till att du har följande:

**Programvara:**

* **Vanlig textredigerare (IDE)**: En integrerad utvecklingsmiljö (IDE), som Microsoft Visual Studio Code, har avancerade funktioner för enklare redigering, även om en vanlig textredigerare kan fungera.

* **Git:** Versionskontrollsystemet krävs för att hantera kodändringar. Om du inte har det installerat hämtar du det från https://git-scm.com.


## Skapa en anpassad funktion {#create-custom-function}

Skapa ett klientbibliotek för att anropa anpassade funktioner i regelredigeraren. Mer information finns i [Använda klientbibliotek](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

Steg för att skapa anpassade funktioner är:
1. [Skapa ett klientbibliotek](#create-client-library)
1. [Lägga till klientbibliotek i ett adaptivt formulär](#use-custom-function)

### Skapa ett klientbibliotek {#create-client-library}

Du kan lägga till anpassade funktioner genom att lägga till ett klientbibliotek. Så här skapar du ett klientbibliotek:

**Klona databasen**

Klona din [AEM Forms as a Cloud Service-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git):

1. Öppna kommandoraden eller terminalfönstret.

1. Navigera till önskad plats på datorn där du vill lagra databasen.

1. Kör följande kommando för att klona databasen:

   `git clone [Git Repository URL]`

Det här kommandot hämtar databasen och skapar en lokal mapp för den klonade databasen på din dator. I hela den här handboken ser vi den här mappen som [AEMaaCS-projektkatalog].

**Lägg till en klientbiblioteksmapp**

Så här lägger du till en ny biblioteksmapp för klienten i [AEMaaCS-projektkatalogen]:

1. Öppna [AEMaaCS-projektkatalogen] i en redigerare.

   ![anpassad struktur för funktionsmapp](/help/forms/assets/custom-library-folder-structure.png)

1. Sök efter `ui.apps`.
1. Lägg till ny mapp. Lägg till exempel till en mapp med namnet `experience-league`.
1. Navigera till mappen `/experience-league/` och lägg till en `ClientLibraryFolder`. Skapa till exempel en klientbiblioteksmapp med namnet `customclientlibs`.

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Lägg till filer och mappar i mappen Klientbibliotek**

Lägg till följande i den tillagda klientbiblioteksmappen:

* .content.xml-fil
* js.txt, fil
* js-mapp

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. Lägg till följande kodrader i `.content.xml`:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Du kan välja vilket namn som helst för egenskapen `client library folder` och `categories`.

1. Lägg till följande kodrader i `js.txt`:

   ```javascript
         #base=js
       function.js
   ```
1. Lägg till javascript-filen som `function.js` i mappen `js` som innehåller de anpassade funktionerna:

   ```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */
   
    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();
   
    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();
   
    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }
   
    return age;
    }
   ```
1. Spara filerna.

![anpassad struktur för funktionsmapp](/help/forms/assets/custom-function-added-files.png)

**Inkludera den nya mappen i filter.xml**:

1. Navigera till filen `/ui.apps/src/main/content/META-INF/vault/filter.xml` i [AEMaaCS-projektkatalogen].

1. Öppna filen och lägg till följande rad i slutet:

   `<filter root="/apps/experience-league" />`
1. Spara filen.

![XML för anpassat funktionsfilter](/help/forms/assets/custom-function-filterxml.png)

**Distribuera den nyligen skapade biblioteksmappen för klienter till AEM**

Distribuera AEM as a Cloud Service, [AEMaaCS-projektkatalogen], till din Cloud Service. Så här distribuerar du till din Cloud Service:

1. Verkställ ändringarna

   1. Lägg till, implementera och skicka ändringarna i databasen med följande kommandon:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Distribuera den uppdaterade koden:

   1. Utlösa en distribution av koden via den befintliga pipeline-funktionen för hela stackar. Detta skapar och distribuerar automatiskt den uppdaterade koden.

Om du inte redan har konfigurerat en pipeline kan du läsa guiden [Konfigurera en pipeline för AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).

När pipeline har körts blir den anpassade funktion som lagts till i klientbiblioteket tillgänglig i regelredigeraren [Adaptiv form](/help/forms/rule-editor-core-components.md).

### Lägga till klientbibliotek i ett adaptivt formulär{#use-custom-function}

När du har distribuerat klientbiblioteket till Forms CS-miljön kan du använda funktionerna i ditt adaptiva formulär. Lägga till klientbiblioteket i ditt adaptiva formulär

1. Öppna formuläret i redigeringsläge. Om du vill öppna ett formulär i redigeringsläge markerar du ett formulär och väljer **[!UICONTROL Edit]**.
1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna fliken **[!UICONTROL Basic]** och välj namnet på **[!UICONTROL client library category]** i listrutan (välj i det här fallet `customfunctionscategory`).

   ![Lägger till klientbiblioteket för anpassade funktioner](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > Du kan lägga till flera kategorier genom att ange en kommaavgränsad lista i fältet **[!UICONTROL Client library category]**.

1. Klicka på **[!UICONTROL Done]**.

Du kan använda den anpassade funktionen i [regelredigeraren för ett adaptivt formulär](/help/forms/rule-editor-core-components.md) med [JavaScript-anteckningar](##js-annotations).

## Använda en anpassad funktion i ett adaptivt formulär

I ett anpassat formulär kan du använda [anpassade funktioner i regelredigeraren](/help/forms/rule-editor-core-components.md). Låt oss lägga till följande kod i JavaScript-filen (`Function.js`) för att beräkna ålder baserat på födelsedatum (ÅÅÅÅ-MM-DD). Skapa en anpassad funktion som `calculateAge()` som tar födelsedatumet som indata och returnerar ålder:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

I ovanstående exempel anropas den anpassade funktionen `calculateAge` när användaren anger födelsedatumet i formatet (ÅÅÅÅ-MM-DD) och sedan returnerar ålder.

![Anpassad funktion för beräkningsagenten i regelredigeraren](/help/forms/assets/custom-function-calculate-age.png)

Låt oss förhandsgranska formuläret för att se hur de anpassade funktionerna implementeras via regelredigeraren:

![Anpassad funktion för beräkning av agens i regelredigerarens formulärförhandsgranskning](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Du kan referera till följande [anpassade funktionsmapp](/help/forms/assets//customfunctions.zip). Hämta och installera den här mappen i AEM med hjälp av [Package Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

## Funktioner för anpassade funktioner

Anpassade funktioner i AEM erbjuder en robust lösning för att utöka och personalisera funktionaliteten i era formulär. Du kan använda anpassade funktioner för att tillgodose organisationens specifika behov.

Dessa funktioner har stöd för olika funktioner, bland annat att arbeta med specifika fält, använda globala fält och asynkrona åtgärder samt att införliva cachningsmekanismer. Tack vare den här flexibiliteten kan blanketterna anpassas efter komplexa krav och ge en effektiv, skräddarsydd användarupplevelse. Genom att utnyttja dessa avancerade funktioner kan ni förbättra interaktionen med formulär och optimera prestanda, vilket gör AEM formulär både mer funktionella och responsiva.

Låt oss dyka upp i funktionerna för anpassade funktioner.

### Asynkront stöd i anpassade funktioner {#support-of-async-functions}

Du kan implementera asynkrona funktioner i regelredigeraren med anpassade funktioner. Mer information om hur du gör detta finns i artikeln [Använda asynkrona funktioner i ett adaptivt formulär](/help/forms/using-async-funct-in-rule-editor.md).

### Field- och Global scope-objekt har stöd för anpassade funktioner {#support-field-and-global-objects}

Fältobjekt refererar till de enskilda komponenterna eller elementen i ett formulär, t.ex. textfält och kryssrutor. Globals-objektet innehåller skrivskyddade variabler som formulärinstans, målfältsinstans och metoder för att göra formulärändringar i anpassade funktioner.

>[!NOTE]
>
> `param {scope} globals` måste vara den sista parametern och visas inte i regelredigeraren för ett anpassat formulär.

Mer information om omfångsobjekt finns i artikeln [Omfångsobjekt i anpassade funktioner](/help/forms/custom-function-core-component-scope-function.md).

### Cachelagring stöds i anpassad funktion

Adaptiv Forms implementerar cachning för anpassade funktioner för att förbättra svarstiden samtidigt som den anpassade funktionslistan hämtas i regelredigeraren. Ett meddelande som `Fetched following custom functions list from cache` visas i filen `error.log`.

![anpassad funktion med cachestöd](/help/forms/assets/custom-function-cache-error.png)

Om de anpassade funktionerna ändras blir cachningen ogiltig och den tolkas.

## Felsökning

* Om det uppstår ett fel i JavaScript-filen som innehåller kod för anpassade funktioner visas inte de anpassade funktionerna i regelredigeraren i ett anpassat formulär. Om du vill kontrollera listan med anpassade funktioner kan du navigera till filen `error.log` för felet. Om ett fel uppstår visas listan med anpassade funktioner tom:

  ![felloggfil](/help/forms/assets/custom-function-list-error-file.png)

  Om det inte finns något fel hämtas den anpassade funktionen och visas i filen `error.log`. Ett meddelande som `Fetched following custom functions list` visas i filen `error.log`:

  ![felloggfil med rätt anpassad funktion](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Nästa steg

Låt oss nu se olika [exempel på anpassade funktioner för ett adaptivt formulär baserat på kärnkomponenter](/help/forms/custom-function-core-components-use-cases.md).

## Se även

{{see-also-rule-editor}}
