---
title: Hur använder man asynkrona funktionsanrop i Visual rule Editor?
description: Asynkrona funktionsanrop i den visuella regelredigeraren
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---

# Använda asynkrona funktioner i ett adaptivt formulär som bygger på kärnkomponenter

Regelredigeraren [i Adaptiv Forms](/help/forms/rule-editor-core-components.md) har stöd för asynkrona funktioner, vilket gör att du kan integrera och hantera åtgärder som kräver väntan på externa processer eller datahämtning utan att användaren behöver avbryta interaktionen med formuläret.

## Vilka faktorer avgör hur asynkrona eller synkrona funktioner används?

Effektiv hantering av användarinteraktionen är avgörande för att skapa en smidig upplevelse. Två vanliga sätt att hantera åtgärder är synkrona och asynkrona funktioner.

**Synkrona funktioner** kör uppgifter efter varandra, vilket gör att programmet väntar på att varje åtgärd ska slutföras innan du fortsätter. Detta kan leda till förseningar och en mindre engagerande användarupplevelse, särskilt när det handlar om att vänta på externa resurser, som filöverföringar eller datahämtning.

Tänk dig till exempel ett scenario där en användare överför en bild stannar hela formuläret och väntar på att överföringen ska slutföras. Denna paus gör att användaren inte kan interagera med andra fält, vilket kan skapa frustration och fördröjningar. När de väntar på att bilden ska bearbetas kan all information som anges gå förlorad om de navigerar bort eller tappar tålamodet, vilket gör upplevelsen krånglig och ineffektiv.

**Asynkrona funktioner** å andra sidan tillåter att aktiviteter körs samtidigt. Detta innebär att användare kan fortsätta att interagera med programmet medan bakgrundsprocesserna körs. Asynkrona åtgärder ger snabbare svarstider, vilket gör det möjligt för användarna att få omedelbar feedback och upprätthålla engagemanget utan avbrott.

Med en asynkron metod kan användare tvärtom överföra bilder i bakgrunden och samtidigt fylla i resten av formuläret sömlöst. Gränssnittet förblir responsivt, vilket gör att det går att uppdatera i realtid och få omedelbar feedback allt eftersom överföringen fortskrider. Det förbättrar användarengagemanget och ger en smidig upplevelse utan avbrott.

![Asynkrona och synkrona funktioner](/help/forms/assets/sync-async.png){align=center}

## Implementera asynkrona funktioner för Adaptive Forms

Du kan implementera asynkrona funktioner för Adaptiv Forms med följande regeltyper i regelredigeraren:

* [Async Function-anrop](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [Funktionsutdata](#how-to-use-function-output-rule-type)

## Hur använder man regeltypen Async Function Call?

Du kan skriva [anpassade funktioner](/help/forms/custom-function-core-component-create-function.md) för asynkrona åtgärder och konfigurera asynkrona funktioner med regeltypen **[!UICONTROL Async Function Call]** i regelredigeraren.

### Utforska regeltypen Async Function Call via ett användningsfall

Ta till exempel ett registreringsformulär på en webbplats där användarna anger ett engångslösenord. Panelen för att lägga till användarinformation visas först när du har angett korrekt engångslösenord. Om engångslösenordet är felaktigt döljs panelen och ett felmeddelande visas på skärmen.

![Inloggningsformulär](/help/forms/assets/rule-editor-login-form.png) {width-50%}

När användaren klickar på knappen **Bekräfta** i ett registreringsformulär anropas funktionen `matchOTP()` asynkront för att verifiera den angivna engångslösenordet. Funktionen `matchOTP()` implementeras som en [anpassad funktion](/help/forms/custom-function-core-component-create-function.md). Med regeltypen **[!UICONTROL Async Function Call]** i regelredigeraren kan du konfigurera funktionen `matchOTP()` i regelredigeraren i ett anpassat formulär. Du kan också implementera återanrop om lyckade och misslyckade i regelredigeraren.

I följande bild visas stegen som används för att använda regeltypen **[!UICONTROL Async Function Call]** för att anropa asynkrona funktioner för Adaptiv Forms:

![Arbetsflöde för att lägga till asynkrona funktioner](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1. Skriv en anpassad funktion för den asynkrona åtgärden i JS-filen.

>[!NOTE]
>
> * Regelredigeraren för ett formulär visar bara funktioner med returtypen `Promise` när du väljer regeltypen **Async Function Call** .
> * Mer information om hur du skapar en anpassad funktion finns i artikeln [Skapa en anpassad funktion för ett adaptivt formulär baserat på kärnkomponenter](/help/forms/custom-function-core-component-create-function.md).

Funktionen `matchOTP()` implementeras som en anpassad funktion. Koden nedan läggs till i JS-filen för den anpassade funktionen:

```JavaScript
/**
 * generates the otp for success use case
 * @param {string} otp
 * @return {PROMISE}
 */
function matchOTP(otp) {
     return new Promise((resolve, reject) => {
        // Perform some asynchronous operation here
         asyncOperationForOTPMatch(otp, (error, result) => {
            if (error) {
                // On failure, call reject(error)
                reject(error);
            } else {
                // On success, call resolve(result)
                resolve(result);
            }
        });
    });
}

/**
 * generates the otp
 */
function asyncOperationForOTPMatch(otp, callback) {
    setTimeout(() => {
        if(otp === '111') {
            callback( null, {'valid':'true'});    
        } else {
            callback( {'valid':'false'}, null);
        }
    }, 1000);
}
```

Koden definierar funktionen `matchOTP()` som genererar ett löfte att validera ett engångslösenord asynkront. Den använder funktionen `asyncOperationForOTPMatch()` för att simulera matchningsprocessen för engångslösenord. Funktionen kontrollerar om angiven engångslösenord är lika med `111`. Om den angivna engångslösenordet är korrekt anropas återanropet med null för felet och ett objekt som anger att engångslösenordet är giltigt `({'valid':'true'})`. Om engångslösenordet inte är giltigt anropas återanropet med felobjektet `({'valid':'false'})` och null för resultatet.

### 2. Konfigurera den asynkrona funktionen i regelredigeraren

Utför följande steg för att konfigurera asynkron funktion i regelredigeraren:

1. [Skapa en regel som ska använda asynkron funktion med anropsregeltypen för asynkron funktion](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [Implementera återanrop för den asynkrona funktionen](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1 Skapa en regel som ska använda asynkron funktion med anropsregeltypen Async Function

Så här skapar du en regel som ska använda asynkron åtgärd med regeltypen **[!UICONTROL Async Function Call]**:

1. Öppna ett adaptivt formulär i redigeringsläge, markera en formulärkomponent och välj **[!UICONTROL Rule Editor]** för att öppna regelredigeraren.
1. Välj **[!UICONTROL Create]**.
1. Skapa ett villkor i avsnittet **När** i regeln om du vill klicka på en knapp. Till exempel **När användaren klickar på [Bekräfta]**.
1. I avsnittet **Sedan** väljer du **[!UICONTROL Async Function call]** i listrutan **Välj åtgärd** .
När du väljer **[!UICONTROL Async Function call]** och funktionerna med returtypen `Promise` visas.
1. Välj den asynkrona funktionen i listan. Välj till exempel funktionen `matchOTP()` och dess återanrop som `Add success callback` och `add failure callback` visas.
1. Välj **[!UICONTROL Input]**-bindningarna. Välj till exempel **[!UICONTROL Input]** som `Form Object` och jämför det med fältet `OTP`.

Skärmbilden nedan visar regeln:

![regeltyp](/help/forms/assets/asyn-function-rule-type.png)

Nu kan du fortsätta med implementeringen av återanropen: `Success` och `Failure` för funktionen `matchOTP`.

#### 2.2 Implementera återanrop för den asynkrona funktionen

Implementera callback-metoderna för lyckade och misslyckade för den asynkrona funktionen med den visuella regelredigeraren.

**Skapa en regel för `Add Success callback` method**

Låt oss skapa en regel som visar panelen `userdetails` om engångslösenordet matchar värdet `111`.

1. Klicka på **[!UICONTROL Add success callback]**.
1. Klicka på **[!UICONTROL Add Statement]** för att skapa regeln.
1. Skapa ett villkor i avsnittet **När** i regeln.
1. Välj **[!UICONTROL Function Output]** > **[!UICONTROL Get Event Payload]**.

   >[!NOTE]
   >
   > Funktionen **[!UICONTROL Get Event Payload]** hämtar data som är kopplade till en specifik händelse för dynamisk hantering av användarinteraktioner.

1. Välj motsvarande bindningar i avsnittet **Indata**. Välj till exempel **[!UICONTROL String]** och ange `valid`. Jämför angiven sträng med `true`.
1. I avsnittet **Sedan** väljer du **[!UICONTROL Show]** i listrutan **Välj åtgärd** . Visa till exempel panelen `userdetails`.
1. Klicka på **[!UICONTROL Add Statement]**.
1. Välj **[!UICONTROL Hide]** i listrutan **Välj åtgärd**. Dölj till exempel textrutan `error message`.
1. Klicka på **[!UICONTROL Done]**.

![Slutfört anrop](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

Se skärmbilden nedan, där användaren anger engångslösenordet som `111`, och `User Details`-panelen visas när användaren klickar på knappen `Confirm`.

![Lyckades](/help/forms/assets/success.gif)

**Skapa en regel för `Add Failure callback` method**

Låt oss skapa en regel för att visa ett felmeddelande om engångslösenordet inte matchar värdet `111`.

1. Klicka på **[!UICONTROL Add failure callback]**.

1. Klicka på **[!UICONTROL Add Statement]** för att skapa regeln.
1. Skapa ett villkor i avsnittet **När** i regeln.
1. Välj **[!UICONTROL Function Output]** > **[!UICONTROL Get Event Payload]**.
1. Välj motsvarande bindningar i avsnittet **Indata**. Välj till exempel **[!UICONTROL String]** och ange `valid`. Jämför angiven sträng med `false`.
1. I avsnittet **Sedan** väljer du **[!UICONTROL Show]** i listrutan **Välj åtgärd** . Visa till exempel textrutan `error message`.
1. Klicka på **[!UICONTROL Add Statement]**.
1. Välj **[!UICONTROL Hide]** i listrutan **Välj åtgärd**. Dölj till exempel panelen `userdetails`.
1. Klicka på **[!UICONTROL Done]**.

![Återanropsmetod för fel](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

Se skärmbilden nedan där användaren anger engångslösenordet som `123` och felmeddelandet visas när användaren klickar på knappen `Confirm`.

![Fel](/help/forms/assets/failure.gif)

På skärmbilden nedan visas den fullständiga regeln för hur **[!UICONTROL Async Function Call]** används för att implementera en asynkron funktion:

![Regel för asynkront funktionsanrop](/help/forms/assets/rule-editor-async-callbacks.png)

Du kan också redigera återanropen genom att klicka på **[!UICONTROL Edit success callback]** och **[!UICONTROL Edit failure callback]**.

## Hur du använder funktionens utdataregeltyp?

Du kan också anropa de asynkrona funktionerna indirekt med synkrona funktioner. De synkrona funktionerna körs med regeltypen **[!UICONTROL Function Output]** i regelredigeraren i ett anpassat formulär.

Titta på koden nedan för att se hur du anropar asynkrona funktioner med regeltypen **[!UICONTROL Function Output]**:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

I ovanstående exempel är funktionen asyncFunction en `asynchronous function`. Den utför en asynkron åtgärd genom att göra en `GET`-begäran till `https://petstore.swagger.io/v2/store/inventory`. Det väntar på svar med `await`, tolkar svarstexten som JSON med `response.json()` och returnerar sedan data. Funktionen `callAsyncFunction` är en synkron anpassad funktion som anropar funktionen `asyncFunction` och visar svarsdata i konsolen. Även om funktionen `callAsyncFunction` är synkron anropar den asynkrona funktionen asyncFunction och hanterar resultatet med programsatserna `then` och `catch`.

För att se hur den fungerar lägger vi till en knapp och skapar en regel för knappen som anropar den asynkrona funktionen när en knapp klickas.

![skapar regel för asynkron funktion](/help/forms/assets/rule-for-async-funct.png){width=50%}

Titta på skärmbilden i konsolfönstret nedan för att visa att när användaren klickar på knappen `Fetch` anropas den anpassade funktionen `callAsyncFunction`, som i sin tur anropar en asynkron funktion `asyncFunction`. Kontrollera konsolfönstret för att se svaret på knappen genom att klicka:

![Konsolfönstret](/help/forms/assets/async-custom-funct-console.png)

## Se även

{{see-also-rule-editor}}
