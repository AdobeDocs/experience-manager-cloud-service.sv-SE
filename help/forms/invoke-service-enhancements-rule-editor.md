---
title: Vilka är förbättringarna av Invoke Service VRE för formulär baserade på kärnkomponenter?
description: Förbättringar av tjänsten Invoke för regelredigeraren
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: anropa tjänstförbättringar i VRE, fylla i listrutealternativ med hjälp av invoke-tjänst, ange repeterbar panel med hjälp av utdata från invoke-tjänst, ange panel med hjälp av utdata från invoke-tjänst, använd utdataparameter för invoke-tjänst för att validera andra fält.
exl-id: 2ff64a01-acd8-42f2-aae3-baa605948cdd
source-git-commit: 43535e52fd749cc599a4e30be25bcc0dbf20eaef
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 0%

---

# Integrera externa API:er med Visual Rule Editor i Core Component Forms

Visuell regelredigerare i ett adaptivt formulär har stöd för funktionen **Anropa tjänst** som gör att du kan ansluta till externa API:er via formulärdatamodeller (FDM) som konfigurerats för din instans. Du kan mappa formulärfält direkt till tjänstens indataparametrar och använda händelsens nyttolastalternativ för att mappa utdataparametrarna. Med Visual Rule Editor kan du också definiera regler för hanterare för lyckade och misslyckade åtgärder baserat på tjänstens svar: hanterare för lyckade API-anrop hanterar felhanterare.

På så sätt kan du enkelt skicka API-begäranden från formuläret, bearbeta API-svaren och visa eller använda returnerade data dynamiskt i formuläret. Det säkerställer en sömlös integrering mellan era adaptiva formulär och externa system eller datakällor.


## Fördelar med att använda Invoke Service i formulärets regelredigerare

Här är några fördelar med att använda Invoke Service-åtgärden i regelredigeraren för ett tilläggsformulär:

* **Effektiv API-integrering**: Visuell regelredigerare förenklar processen att integrera externa tjänster eller API:er i din adaptiva Forms. Genom att använda **Invoke Service** kan du enkelt koppla formulär till olika datakällor och tjänster utan att behöva komplex kodning, vilket gör att formulärintegreringen blir mer effektiv.

* **Dynamisk svarshantering**: Du kan hantera slutförda och felsvar baserat på utdataresvaren i **Invoke Service**, vilket gör att formulär kan reagera dynamiskt på olika scenarier. Det säkerställer att blanketterna hanterar olika förhållanden på ett korrekt sätt, vilket ger större flexibilitet och kontroll.

* **Förbättrad användarinteraktion**: Om du använder **Invoke Service** i regelredigeraren kan du validera dina formulär i realtid, vilket ger en bättre användarupplevelse. Det säkerställer också att data valideras korrekt på serversidan, vilket minskar antalet fel och förbättrar formulärens tillförlitlighet.

## Anropa tjänsthanterare för lyckade och misslyckade åtgärder

>[!NOTE]
>
> Du kan bara använda hanterarna för **Anropa tjänst** för lyckade och misslyckade formulär baserade på kärnkomponenter. Forms-baserade på grundkomponenter stöder inte hanterare för **Invoke Service** och fel.

Med den visuella regelredigeraren kan du skapa regler för hanterare för lyckade och misslyckade åtgärder för **Invoke Service** -åtgärder baserat på dess utdataresvar. Nedanstående bild visar **Invoke Service** i Visual rule editor för ett adaptivt format:

![Anropa tjänsthanterare](/help/forms/assets/invoke-service-rule-editor.png)

### Adding Success Handler and Failure Handler

Klicka på **[!UICONTROL Add Success Handler]** eller **[!UICONTROL Add Failure Handler]** om du vill lägga till en hanterare för lyckade eller misslyckade åtgärder.

När du klickar på **[!UICONTROL Add Success Handler]** visas regelredigeraren **[!UICONTROL Invoke Service Success Handler]** så att du kan ange regler eller logik för att hantera **Invoke Service** -utdatasvaret när åtgärden har slutförts. Du kan ange regler även utan att definiera villkor, men du kan lägga till villkor för hanteraren av lyckade åtgärder genom att klicka på alternativet **[!UICONTROL Add Condition]**.

![Hanteraren för lyckade anrop av tjänsten](/help/forms/assets/invoke-service-success-handler.png)

Du kan lägga till flera regler för att hantera lyckade svar för åtgärden **Anropa tjänst**:

![Hanteraren för flera lyckade åtgärder](/help/forms/assets/invoke-service-multiple-success-handlers.png){width=50%, height=50%}

På samma sätt kan du lägga till regler för att hantera **Invoke Service** -utdataresvaret när åtgärden inte lyckas. Bilden nedan visar regelredigeraren **[!UICONTROL Invoke Service Failure Handler]**:

![Anropa hanteraren för tjänstfel](/help/forms/assets/invoke-service-failue-handler.png)

Du kan också lägga till flera regler för att hantera misslyckade svar från åtgärden **Anropa tjänst**.

Funktionen **Aktivera felvalidering på servern** tillåter validering som lagts till av författaren när ett adaptivt formulär utformas för att köras på servern också.

## Krav för att använda Invoke Service i regelredigeraren

Nedan visas de krav du måste uppfylla innan du kan använda **Anropa tjänst** i regelredigeraren:

* Kontrollera att du har konfigurerat en datakälla. [Klicka här](/help/forms/configure-data-sources.md) om du vill ha anvisningar om hur du konfigurerar en datakälla.
* Skapa en formulärdatamodell med den konfigurerade datakällan. [Klicka här](/help/forms/create-form-data-models.md) om du vill ha hjälp med att skapa en formulärdatamodell.
* Kontrollera att kärnkomponenterna är aktiverade för din miljö. Installera den senaste versionen för att aktivera adaptiva Forms Core-komponenter för din AEM Cloud-tjänstmiljö.

## Utforska Invoke Service via olika användningsfall

Med den visuella regelredigerarens **Anropa tjänst** kan du utföra flera användbara åtgärder. Du kan använda den för att fylla i listrutealternativ, ange repeterbara eller enkla paneler och validera formulärfält, allt baserat på utdatasvaret för **Anropa tjänst**. Detta gör formulären mer flexibla och interaktiva.

Tabellen nedan beskriver några scenarier där **Invoke Service** kan användas:

| **Använd skiftläge** | **Beskrivning** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Fyll i listrutealternativ med hjälp av utdata från Invoke Service** | Fyller i listrutealternativ dynamiskt baserat på data som hämtats från Invoke Service-utdata. [Klicka här](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service) för att se implementeringen. |
| **Ange repeterbar panel med utdata från Invoke Service** | Konfigurerar en repeterbar panel genom att använda data från Invoke Service-utdata, vilket möjliggör dynamiska paneler. [Klicka här](#use-case-2-set-repeatable-panel-using-output-of-invoke-service) för att se implementeringen. |
| **Ange panel med utdata från Invoke Service** | Anger innehållet eller synligheten för en panel med specifika värden från Invoke Service-utdata. [Klicka här](#use-case-3-set-panel-using-output-of-invoke-service) för att se implementeringen. |
| **Använd utdataparametern för Invoke Service för att validera andra fält** | Använder specifika utdataparametrar från Anropa-tjänsten för att validera formulärfälten. [Klicka här](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields) för att se implementeringen. |
| **Använd händelsenyttolast i Navigera till åtgärd i anropstjänsten** | Använder händelsens nyttolast för att hantera lyckade och misslyckade svar och för att skicka data till åtgärden Navigera till under navigeringen. [Klicka här](#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service) för att se implementeringen. |

Skapa ett `Get Information`-formulär som hämtar värden baserat på indata som anges i textrutan `Pet ID`. Skärmbilden nedan visar det formulär som används i dessa fall:

![Hämta informationsformulär](/help/forms/assets/get-information-form.png)

**Formulärfält**

Lägg till följande fält i formuläret:

* **Ange husdjurs-ID**: Textruta
* **Välj foto-URL:er**: Listruta
* **Taggar**: Panel
   * Namn: Textruta
   * ID: Textruta
* **Kategori**: Panel
   * Namn: Textruta
* **Skicka**: Skicka-knapp

>[!NOTE]
>
> I fältet **Bindningsreferens** i dialogrutan **Egenskaper** i formulärfälten väljer du ![foldersearch_18](assets/folder-search-icon.svg) och navigerar till den binära egenskap som du har lagt till i formulärdatamodellen (FDM).

**Konfigurerar paneler**

Ange panelerna som repetitiva med följande begränsningar:

* Minsta värde: 1
* Högsta värde: 4

Du kan justera värdena för de upprepade panelerna så att de passar dina behov.

**Datakälla**

I det här exemplet används API:t [Swagger Petstore](https://petstore.swagger.io/) för att konfigurera en datakälla. [Formulärdatamodellen](/help/forms/create-form-data-models.md) har konfigurerats för tjänsten [getPetById](https://petstore.swagger.io/#/pet/getPetById), som hämtar information om djur baserat på det angivna ID:t.

Låt oss publicera följande JSON med tjänsten [addPet](https://petstore.swagger.io/#/pet/addPet) i [Swagger Petstore](https://petstore.swagger.io/) API:

```
{
        "id": 101,
        "category": {
            "id": 1,
            "name": "Labrador"
        },
        "name": "Lisa",
        "photoUrls": [
            "https://example.com/photos/lisa1.jpg",
            "https://example.com/photos/lisa2.jpg"
        ],
        "tags": [
            {
                "id": 1,
                "name": "vaccinated"
            },
            {
                "id": 2,
                "name": "friendly"
            },
            {
                "id": 3,
                "name": "house-trained"
            }
        ],
        "status": "available"
    }
```

Regler och logik implementeras med åtgärden **Anropa tjänst** i regelredigeraren i textrutan `Pet ID` för att visa de angivna användningsexemplen.

Nu ska vi gå igenom implementeringen av varje användningsfall i detalj.

### Användningsfall 1: Fyll i listrutevärden med hjälp av utdata från Invoke Service

Det här användningsexemplet visar hur du fyller i listrutealternativ dynamiskt baserat på utdata för en `Invoke Service`.

#### Implementering

För att uppnå detta skapar du en regel i textrutan `Pet ID` som anropar tjänsten `getPetById`. I regeln anger du egenskapen `enum` för listrutan `photo-url` till `photoUrls` i **[!UICONTROL Add Success Handler]**.

![Ange nedrullningsbart värde](/help/forms/assets/set-dropdownoption.png)

>[!NOTE]
>
> Mer information om hur du anger hanterare för lyckade och misslyckade åtgärder finns i avsnittet [Lägga till hanterare för lyckade och misslyckade åtgärder](#adding-success-handler-and-failure-handler).

#### Utdata

Ange `101` i textrutan `Pet ID` för att dynamiskt fylla i listrutealternativen baserat på det angivna värdet.

![Resultat](/help/forms/assets/output1.png)

### Användningsfall 2: Ange upprepningsbar panel med utdata från Invoke Service

Det här användningsexemplet visar hur du fyller i repeterbara paneler dynamiskt baserat på utdata från en **Invoke Service**.

#### Överväganden

* Kontrollera att namnet på den repeterbara panelen matchar parametern för den **Invoke Service** som du vill ange panelen för.
* Panelen upprepas för antalet värden som returneras av motsvarande **Anropa tjänst**-fält.

#### Implementering

Skapa en regel i textrutan `Pet ID` för att anropa tjänsten `getPetById`. I **[!UICONTROL Add Success Handler]** lägger du till ett annat svar från en hanterare. Ange värdet `tags` för panelen `tags` i regeln.

![Skapa regel för repeterbar panel](/help/forms/assets/create-rule-repeatable-panel.png)

>[!NOTE]
>
> Mer information om hur du anger hanterare för lyckade och misslyckade åtgärder finns i avsnittet [Lägga till hanterare för lyckade och misslyckade åtgärder](#adding-success-handler-and-failure-handler).

#### Utdata

Ange `101` i textrutan `Pet ID` om du vill fylla i den repeterbara panelen dynamiskt baserat på indatavärdet.

![Utdata](/help/forms/assets/output2.png)

### Användningsfall 3: Ange panel med utdata från Invoke Service

Det här användningsexemplet visar hur du dynamiskt anger värdet för en panel baserat på utdata från en **Invoke Service**.

#### Överväganden

* Kontrollera att panelens namn matchar parametern för den **Anropa tjänst** som du vill ange panelen för.
* Panelen upprepas för antalet värden som returneras av motsvarande Invoke Service-fält.

#### Implementering

Skapa en regel i textrutan `Pet ID` för att anropa tjänsten `getPetById`. I **[!UICONTROL Add Success Handler]** lägger du till ett annat svar från en hanterare. Ange värdet `categoryname` för textrutan `category.name` i regeln.

>[!NOTE]
>
> Mer information om hur du anger hanterare för lyckade och misslyckade åtgärder finns i avsnittet [Lägga till hanterare för lyckade och misslyckade åtgärder](#adding-success-handler-and-failure-handler).

![Skapa regel för repeterbar panel](/help/forms/assets/set-panel-values.png)

#### Utdata

Ange `101` i textrutan `Pet ID` för att fylla i panelen dynamiskt baserat på indatavärdet.

![Utdata](/help/forms/assets/output3.png)

### Använd fall 4: Använd utdataparametern för Invoke Service för att validera andra fält

Det här användningsexemplet visar hur du använder utdata från en **Anropa tjänst** för att dynamiskt validera andra formulärfält.

#### Implementering

Skapa en regel i textrutan `Pet ID` för att anropa tjänsten `getPetById`. I **[!UICONTROL Add Failure Handler]** lägger du till ett felhanterarsvar. Dölj knappen **Skicka** om en felaktig `Pet ID` anges.

![Felhanterare](/help/forms/assets/create-rule-failure-handler.png)

#### Utdata

Ange `102` i textrutan `Pet ID` och knappen **Skicka** är dold.

![Utdata](/help/forms/assets/output4.png)

### Använd fall 5: Använd händelsenyttolast i Navigera till åtgärd i Anropa tjänst

Det här användningsexemplet visar hur du konfigurerar en regel på knappen **Skicka** som anropar en **Invoke Service** och sedan dirigerar om användaren till en annan sida med åtgärden **Navigera till** .

#### Implementering

Skapa en regel på knappen **Skicka** för att anropa API-tjänsten `redirect-api`. Den här tjänsten ansvarar för att dirigera om användaren till formuläret **Kontakta oss**.

Du kan direkt integrera ett API som API-tjänst för `redirect-api` i regelredigeraren med JSON-data som anges nedan:

```json
{
  "id": "1",
  "path": "/content/dam/formsanddocuments/contact-detail/jcr:content?wcmmode=disabled"
}
```

>[!NOTE]
>
> [Klicka här](/help/forms/api-integration-in-rule-editor.md) utan att använda en fördefinierad formulärdatamodell om du vill lära dig hur du integrerar API direkt i regelredigeringsgränssnittet.

I **[!UICONTROL Add Success Handler]** konfigurerar du åtgärden **Navigera till** så att användaren dirigeras om till sidan **Kontakta oss** med parametern `Event Payload`. Här kan användaren skicka sin kontaktinformation.

![Händelsenyttolast](/help/edge/docs/forms/assets/navigate-to-eventpayload.png)

Du kan också konfigurera en felhanterare så att ett felmeddelande visas om anropet till tjänsten misslyckas.

#### Utdata

När du klickar på knappen **Skicka** anropas API-tjänsten `redirect-api`. Användaren omdirigeras till sidan **Kontakta oss** när åtgärden har slutförts.

![Utdata för händelsenyttolast](/help/forms/assets/output5.gif)

## Frågor och svar

**F: Vad händer om jag har skapat en regel med Invoke Service och sedan uppgraderar till den senaste versionen av kärnkomponenterna?**

**A:** När du uppgraderar till den senaste versionen av kärnkomponenterna uppdateras regeln **Anropa tjänst** automatiskt till det senaste användargränssnittet eftersom den är bakåtkompatibel.

**F: Kan jag lägga till flera regler för att hantera lyckade eller misslyckade svar för Invoke Service-åtgärden?**

**S:** Ja, du kan lägga till flera regler för att hantera slutförda eller misslyckade svar för åtgärden **Anropa tjänst**.

## Relaterade artiklar

* [Konfigurera datakällor](configure-data-sources.md)
* [Skapa formulärdatamodell (FDM)](create-form-data-models.md)
* [Arbeta med formulärdatamodell (FDM)](work-with-form-data-model.md)
* [Använd formulärdatamodell (FDM)](using-form-data-model.md)


## Ytterligare resurser

{{see-also-rule-editor}}
