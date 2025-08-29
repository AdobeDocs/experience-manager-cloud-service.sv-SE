---
title: I den här artikeln beskrivs olika användningsfall för regelredigeraren i ett adaptivt formulär baserat på kärnkomponenter.
description: I den här artikeln utforskas olika användningsexempel för regelredigeraren i ett adaptivt formulär baserat på kärnkomponenter. Det visar också hur anpassade funktioner kan användas för att skapa anpassade regler för formulär.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 062ed441-6e1f-4279-9542-7c0fedc9b200
source-git-commit: 85555ebe4bfa41bf01d7c5610fa5760551830b5c
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 0%

---

# Förbättringar och användningsfall i regelredigeraren

<span class="preview"> Det här är förhandsversionsfunktioner som är tillgängliga via vår <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">förhandsutgåva</a>. Dessa förbättringar gäller även för Edge Delivery Services Forms.

I den här artikeln beskrivs de senaste förbättringarna av regelredigeraren i Adaptive Forms. Uppdateringarna är utformade för att hjälpa er att enklare definiera formulärbeteende utan att behöva skriva anpassad kod, och för att skapa mer dynamiska, responsiva och personaliserade formulärupplevelser.

I tabellen nedan visas de senaste förbättringarna av regelredigeraren i Adaptive Forms, tillsammans med en kort beskrivning och de viktigaste fördelarna med varje funktion:

| Förbättring | Beskrivning | Fördelar |
|---|----|---|
| **Validering med metoden `validate()`** | Finns i funktionslistan för att validera enskilda fält, paneler eller hela formuläret. | - Detaljerad validering på panel-, fält- eller formulärnivå <br> - Bättre användarupplevelse med riktade felmeddelanden <br> - Förhindrar progression med ofullständiga data <br> - Minskar antalet formuläröverföringsfel |
| **Hämta DOR** | Körklar funktion som är tillgänglig i regelredigeraren för att hämta dokumentets (DoR) dokument. | - Ingen anpassad utveckling krävs för nedladdning av DoR <br> - konsekvent nedladdning i alla formulär |
| **Dynamiska variabler** | Skapa regler med variabler som ändras baserat på användarindata eller andra villkor. | - Aktiverar flexibla regelvillkor <br> - Minskar behovet av dubblettlogik <br> - eliminerar behovet av att skapa dolda fält |
| **Anpassade händelsebaserade regler** | Definiera regler som svarar på anpassade händelser utöver standardutlösarna. | - Stöder avancerade användningsfall <br> - Bättre kontroll över när och hur regler körs <br> - Förbättrar interaktiviteten |
| **Kontextmedveten upprepningsbar panelkörning** | Regler körs nu i rätt sammanhang för varje upprepad panel, i stället för bara för den sista instansen. | - Exakt regelprogram för varje upprepad instans <br> - Minskar antalet fel i dynamiska avsnitt <br> - Förbättrar användarupplevelsen med upprepat innehåll |
| **Stöd för frågesträng, UTM och webbläsarparametrar** | Skapa regler som anpassar formulärbeteenden baserat på URL-parametrar eller webbläsarspecifika värden. | - Aktiverar personalisering baserat på källa eller miljö <br> - användbart för marknadsförings- eller spårningsspecifika flöden <br> - Inget behov av extra skript eller anpassning |

>[!NOTE]
>
> Förbättringarna i regelredigeraren gäller även för Edge Delivery Services Forms.

Nu ska vi utforska varje metod i detalj med specifika användningsexempel för att få en förståelse för hur de här funktionerna kan användas för att leverera en personaliserad upplevelse till användarna

## Validera metod i funktionslista

Förbättrade valideringsfunktioner som gör att metoden **validate()** kan användas i funktionslistan för att validera paneler, fält eller hela formulär. I ett låneansökningsformulär i flera steg måste du till exempel validera olika avsnitt innan användarna kan gå vidare till nästa steg.

**Scenario:** Ett finansinstitut erbjuder ett flerstegsansökningsformulär där användarna måste fylla i olika avsnitt, till exempel:

* Personuppgifter
* Anställningsdetaljer
* Lånedetaljer
* Granska och skicka

Innan en användare flyttar från ett steg till nästa, får formuläret endast validera fälten i det aktuella avsnittet. Användaren bör till exempel inte tillåtas att fortsätta till &quot;Anställningsinformation&quot; såvida inte alla obligatoriska fält i &quot;Personuppgifter&quot; är korrekt ifyllda.

**Implementering med validate() i regelredigeraren**

En **Nästa**-knapp på varje panel utlöser en regel med metoden **validate()** . Regeln kontrollerar om alla fält i den aktuella panelen är giltiga. Om valideringen godkänns navigerar formuläret till nästa panel. I annat fall visas felmeddelanden som hjälper användaren att korrigera indata.

Skärmbilden nedan visar den regel som används för knappen **Nästa**:

![Validera nästa knapp](/help/forms/assets/validate-next.png)

I ovanstående regel kontrollerar knappen **Nästa** om fälten i avsnittet **Personlig information** är giltiga. Om informationen inte är giltig flyttas fokus till fältet **Namn** på panelen **Personlig information**.

![utdata](/help/forms/assets/valid-output.png)

>[!NOTE]
>
>Du kan använda metoden **validate()** i formulär, fragment eller enskilda fält. När ett fragment ingår i ett formulär visas både formuläret och fragmentet som alternativ i valideringskontexten. I det här fallet refererar fragmentet till fälten i det, medan formuläret refererar till det överordnade formulär där fragmentet är inbäddat.

## DownloadDor as OOTB function in Rule Editor

Om du använder funktionen **DownloadDor()** i körklart läge (OTB) i regelredigeraren kan användaren hämta postdokumentet om formuläret är konfigurerat för att generera dokument för återskapad.

>[!NOTE]
>
>Om formuläret inte har konfigurerats för Dokument för post visas ett felmeddelande när regeln med funktionen **downloadDoR()** används för knappen.

**Scenario**: En myndighet tillhandahåller ett digitalt ansökningsformulär för att utfärda certifikat. Efter att ha skickat in formuläret behöver de sökande ofta en kopia av det ifyllda formuläret för att kunna registrera sig eller dela det med en annan avdelning. För att förbättra användarupplevelsen vill myndigheten ge de sökande möjlighet att ladda ned en DoR-fil (Document of Record) omedelbart efter inlämningen eller i vilket skede som helst före den slutliga inlämningen.

**Implementering med DownloadDor() i regelredigeraren**

En **Hämta**-knapp läggs till i formuläret med regelredigeraren. En regel har konfigurerats för att utlösa funktionen **DownloadDor()** när användaren klickar på knappen.

Skärmbilden nedan visar den regel som används för knappen **Hämta**:

![Hämta knappregel](/help/forms/assets/download-button-rule.png)

>[!NOTE]
>
> I fältet **Indata** kan användaren ange filnamnet för ett hämtningsbart dokument. Det här är en valfri parameter.

Om formuläret är konfigurerat för DoR-generering genereras och hämtas PDF direkt, utan att någon anpassad funktion behövs.

![Postdokument](/help/forms/assets/download-dor-output.png)

## Stöd för dynamiska variabler i regler

Den förbättrade regelredigeraren har stöd för att skapa och använda dynamiska (tillfälliga) variabler. Dessa variabler kan ställas in och hämtas under hela formulärets livscykel med de inbyggda funktionerna **Ange variabelvärde** och **Hämta variabelvärde** .
Dessa variabler:

* Skickas inte tillsammans med formulärdata.
* Kan innehålla mellanliggande eller beräknade värden.
* Kan användas i villkorsstyrd logik och åtgärder.

**Scenario**: Med ett onlinebutiksformulär kan användarna välja en produkt, ange kvantitet och välja ett land att leverera. Produktpriset är ett fast värde som hämtas via ett formulärfält, medan fraktkostnaden varierar dynamiskt beroende på vilket land som valts.

För att undvika oreda i formuläret med dolda fält bestämmer man sig för att lagra leveranskostnaden i en temporär variabel och använda den för realtidsberäkningar.

**Implementering med funktionerna Ange variabelvärde och Hämta variabelvärde i regelredigeraren**

En regel har konfigurerats på **Address**-fragmentet med funktionen **Set Variable Value** för att tilldela en temporär variabel med namnet **extracharge**. Värdet för den här variabeln ändras dynamiskt baserat på det valda landet. Till exempel:

* Om användaren väljer USA är **extracharge** inställt på 500.
* För alla andra länder är **extracharge** inställt på 100.

![Ange variabelvärde](/help/forms/assets/setvalue.png)

När sedan **Total leveranskostnad** beräknas används funktionen **Hämta variabelvärde** för att hämta värdet för **extraheringsavgift**. Det här värdet läggs till i **Produktpris × Produktkvantitet** för att beräkna det slutliga beloppet som ska betalas genom att klicka på knappen.

![Hämta variabelvärde](/help/forms/assets/getvalue.png)

Fältet **Total leveranskostnad** uppdateras dynamiskt för att återspegla både produktkostnaden och fraktkostnaden när användaren ändrar land eller kvantitet.
![utdata](/help/forms/assets/getsetvalue-output.png)

>[!NOTE]
>
> Du kan också lägga till funktionen **Hämta variabelvärde** i villkoret När.
> > ![Funktionen Hämta variabelvärde i När villkor ](/help/forms/assets/when-get-variable.png){width=50%,höjd=50%, align=center}

På så sätt kan du göra dynamiska realtidsberäkningar utan att lägga till extra fält i formuläret, vilket gör strukturen ren och användarvänlig.

## Stöd för anpassade händelsebaserade regler

Den förbättrade regelredigeraren stöder anpassad händelsehantering med funktionerna **Skicka händelse** och **Vid utlösarhändelse**. Dessa funktioner gör att olika delar av formuläret kan kommunicera genom att skicka och lyssna på anpassade händelser, vilket möjliggör en renare, modulär logik utan att knyta åtgärder till specifika fält.

**Scenario**: Ett inloggningsformulär skapas med ett återanvändbart inloggningsfragment som innehåller fälten **Ange användarnamn** och **Ange lösenord**. När en användare anger giltiga inloggningsuppgifter validerar formuläret indata och initierar processen **Hämta engångslösenord**. När användaren har angett en giltig engångslösenord omdirigeras de till rätt sida.

I stället för att binda logiken direkt till fälten, använder formuläret en händelsebaserad metod med **Dispatch Event** och **On Trigger Event** för att förbättra modulariteten och underhållet.

**Implementering med utsändningshändelse och utlösarhändelse**

Inloggningsfragmentet läggs till i formuläret och innehåller fördefinierade fält för användarnamn och lösenord. En regel har konfigurerats på knappen **Hämta engångslösenord** för att visa **valideringspanelen**, som innehåller indatafältet för att ange och validera engångslösenordet.

![Hämta regel för engångslösenord](/help/forms/assets/get-otp-rule.png)

I **valideringspanelen** har en regel konfigurerats för knappen Validera. API-integrering används för att validera engångslösenord som anges i fältet **Ange engångslösenord**. Om valideringen lyckas utlöses en **utsändningshändelse** med namnet **LoggedIn** med händelsens nyttolast som innehåller API-svaret.

![I utlösarhändelseregel](/help/forms/assets/trigger-event-rule.png)

På formulärnivå har en regel konfigurerats att lyssna efter händelsen **LoggedIn**. När den här händelsen utlöses visas omdirigeringsmeddelandet i regeln och användaren dirigeras till kontrollpanelssidan.

![skicka händelseregel](/help/forms/assets/dispatch-event-rule.png)

När användaren skickar formuläret med korrekta inloggningsuppgifter och en giltig engångslösenord, slutförs inloggningen och användaren omdirigeras till sin kontrollpanel.

Stöd för anpassade händelser som gör att utvecklare kan skapa och utlösa anpassade händelser som kan användas som villkor i regelredigeraren.

## Kontextbaserad regelkörning för upprepningsbara paneler

Den anpassningsbara Forms-funktionen stöder sammanhangsberoende regelkörning för repeterbara paneler. Detta gör att regler kan tillämpas specifikt på den panelinstans där användaren interagerar, i stället för att påverka alla instanser eller standardinställningen för den sista.

**Scenario**: Med ett produktorderformulär kan användare lägga till flera produkter i separata paneler. Varje panel innehåller fältet **Antal produkter** och fältet **Totalkostnad**. När en användare uppdaterar kvantiteten för en produkt bör formuläret beräkna om det totala priset, men bara för den specifika panelen, inte för alla andra.

**Implementering med kontextmedvetna regler i regelredigeraren**

En regel har konfigurerats i fältet **Antal produkter** i den repeterbara produktpanelen.

Skärmbilden nedan visar regeln för fältet **Antal produkter** i den repeterbara produktpanelen:

![antal produktregler](/help/forms/assets/number-of-product-rule.png)

När kvantiteten ändras hämtar regeln enhetspriset för den valda produkten och beräknar den totala kostnaden endast för den panelen.

![Kontextmedvetna regelutdata](/help/forms/assets/context-aware-rule-output.png)

## URL och parameterbaserade regler för webbläsare i Adaptiv Forms

Adaptiv Forms stöder dynamisk regelkörning med hjälp av externa parametrar som skickas via formulärets URL eller som härleds från användarens webbläsarmiljö. Detta möjliggör personaliserade och sammanhangsberoende formulärupplevelser som bygger på var besökaren kom ifrån eller vilken enhet de använder.

## Tillåtna parametertyper

| Parametertyp | Alternativ som stöds | Beskrivning | Exempelvärde |
| --- | --- | --- | ---|
| Frågeparameter | `ref` (endast strängvärden) | Allmänt nyckelvärdepar i URL:en efter `?` | `?ref=partner123` |
| UTM-parameter | UTM Source<br>UTM Medium<br>UTM Campaign<br>UTM Term<br>UTM Content | Särskilda frågeparametrar som används för kampanjspårning | `?utm_source=google&utm_medium=email` |
| URL-parameter | Värdnamn<br>Sökväg | Extraherar strukturella komponenter i formulärets URL | `hostname=www.example.com`, `path=/signup` |
| Webbläsarparameter | Webbläsaragent<br>Webbläsarspråk<br>Webbläsarplattform | Värden härledda från användarens webbläsare eller enhet | `Browser Agent=Mozilla`, `Language=en-US` |

**Scenario**: Ett formulär för leadgenerering måste anpassa sitt välkomstmeddelande beroende på trafikkällan. När en användare når formuläret via en annonskampanj från Google (med utm_source=google i URL:en) bör formuläret visa en anpassad hälsning.

**Implementering med UTM-parameter**

En regel har konfigurerats för ett textfält som visar anpassade meddelanden för Google-användare och använder parametern **utm_source**.

Skärmbilden nedan visar den regel som är konfigurerad för textmeddelandet:

![regel för textmeddelande](/help/forms/assets/utm-param-rule.png)

Om parametervärdet **utm_source** är lika med &quot;google&quot; visas ett anpassat meddelande som &quot;Hello Google users, welcome to the Campaign Ad!&quot; visas.

![utm-param-output](/help/forms/assets/utm-param-output.png)

På så sätt kan marknadsförarna leverera relevant innehåll till användarna baserat på kampanjen som förde dem till formuläret utan att det krävs manuell fältinmatning eller anpassade skript.

Dessa förbättringar utökar funktionerna i den adaptiva regelredigeraren i Forms och ger utvecklare kraftfulla verktyg för att skapa mer dynamiska, interaktiva och intelligenta formulär. Varje förbättring tillgodoser specifika affärsbehov samtidigt som den är enkel att använda och gör regelredigeraren tillgänglig för både tekniska och icke-tekniska användare.

## Ytterligare resurser

{{see-also-rule-editor}}
