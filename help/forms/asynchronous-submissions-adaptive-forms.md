---
title: Hur konfigurerar jag asynkron sändning för AEM Adaptive Forms?
description: Lär dig hur du konfigurerar asynkron överföring för Adaptive Forms. Läs mer om hur asynkron inlämning fungerar för Adaptive Forms.
feature: Adaptive Forms, Foundation Components
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: eaab351460363b83c7d3667e048235506cc71c41
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---

# Konfigurera asynkron sändning av AEM Adaptiv Forms {#asynchronous-submission-of-adaptive-forms}


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/asynchronous-submissions-adaptive-forms.html) |
| AEM as a Cloud Service | Den här artikeln |


Som standard är webbformulär konfigurerade att skicka synkront. När användare skickar ett formulär omdirigeras de i synkront skick till en bekräftelsesida, en tacksida eller en felsida om det uppstår ett överföringsfel. Moderna webbupplevelser som single page-applikationer blir dock allt populärare, där webbsidan är statisk medan klient-server-interaktion sker i bakgrunden. Du kan konfigurera asynkron sändning för att ge den här upplevelsen med Adaptive Forms.

När en användare skickar in ett formulär i asynkron form plugin-program för formulärutvecklare, som omdirigering till ett annat formulär eller till ett separat avsnitt på webbplatsen. Författaren kan också plugin-program för olika tjänster, som att skicka data till ett annat datalager eller lägga till en anpassad analysmotor. Om formuläret skickas asynkront fungerar ett adaptivt formulär som ett program med en sida, eftersom det inte läses in igen eller dess URL inte ändras när skickade formulärdata valideras på servern.

Läs vidare om du vill ha mer information om asynkron överföring i Adaptive Forms.

## Konfigurera asynkron överföring {#configure}

Så här konfigurerar du asynkron överföring för ett adaptivt formulär:

1. I redigeringsläget Adaptivt formulär markerar du objektet Formulärbehållare och väljer ![cmppr1](assets/configure-icon.svg) för att öppna dess egenskaper.
1. I **[!UICONTROL Submission]** egenskapsavsnittet, aktivera **[!UICONTROL Use asynchronous submission]**.
1. I **[!UICONTROL On Submit]** väljer du något av följande alternativ när formuläret har skickats.

   * **[!UICONTROL Redirect to URL]**: Omdirigerar till angiven URL eller sida när formulär skickas. Du kan ange en URL-adress eller bläddra för att välja sökvägen till en sida i dialogrutan **[!UICONTROL Redirect URL/Path]** fält.
   * **[!UICONTROL Show Message]**: Visar ett meddelande när formulär skickas. Du kan skriva ett meddelande i textfältet under **[!UICONTROL Show Message]** alternativ. Textfältet har stöd för RTF-formatering.

1. Välj ![check-button1](assets/save_icon.svg) för att spara egenskaperna.

## Hur asynkron inlämning fungerar {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] innehåller färdiga funktioner och felhanterare för att skicka formulär. Hanterare är funktioner på klientsidan som körs baserat på serversvaret. När ett formulär skickas skickas data till servern för validering, som returnerar ett svar till klienten med information om om huruvida överföringen lyckades eller inte. Informationen skickas som parametrar till den relevanta hanteraren för att köra funktionen.

Dessutom kan formulärförfattare och utvecklare skriva regler på formulärnivå för att åsidosätta standardhanterare. Mer information finns i [Åsidosätta standardhanterare med regler](#custom).

Låt oss först granska serversvaret för att se om det har lyckats eller inte.

### Serversvar för lyckad sändning {#server-response-for-submission-success-event}

Strukturen för serversvaret för händelsen att överföringen lyckades är följande:

```json
{oneOf: [
{  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouOption : {type : "string"}
   }},
  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouContent: {type: "string"}
   }
]

}
```

Serversvaret vid lyckad formulärsändning innehåller:

* Typ av formulärdataformat: XML eller JSON
* Formulärdata i XML- eller JSON-format
* Markerat alternativ för omdirigering till en sida eller för att visa ett meddelande som konfigurerats i formuläret
* Sidans URL- eller meddelandeinnehåll som konfigurerats i formuläret

Hanteraren för lyckade åtgärder läser serversvaret och dirigerar därför om till den konfigurerade sidans URL eller visar ett meddelande.

### Serversvar för en felhändelse för överföring {#server-response-for-submission-error-event}

Strukturen för serversvaret för en felhändelse vid överföring är följande:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

Serversvaret vid fel när formulär skickas innehåller:

* Orsak till felet, misslyckades med CAPTCHA eller validering på serversidan
* Lista över felobjekt, som innehåller SOM-uttrycket för fältet som inte kunde valideras och motsvarande felmeddelande

Felhanteraren läser serversvaret och visar därför felmeddelandet i formuläret.

## Åsidosätta standardhanterare med regler {#custom}

Formulärutvecklare och författare kan skriva regler på formulärnivå för att åsidosätta standardhanterare. Serversvaret för lyckade händelser och felhändelser visas på formulärnivå, som utvecklare kan komma åt med `$event.data` i regler.

Utför följande steg för att skriva regler för att hantera lyckade och felade händelser.

1. Öppna det adaptiva formuläret i redigeringsläge, markera ett formulärobjekt och välj ![edit-rules1](assets/edit-rules-icon.svg) för att öppna regelredigeraren.
1. Välj **[!UICONTROL Form]** i trädet Formulärobjekt och välj **[!UICONTROL Create]**.
1. Välj **[!UICONTROL is submitted successfully]** eller **[!UICONTROL submission fails]** från **[!UICONTROL Select state]** listruta.
1. Definiera en **[!UICONTROL Then]** åtgärd för det markerade läget. Välj till exempel **[!UICONTROL Navigate To]** och skriv eller klistra in en URL. Du kan också dra valfri funktion med **[!UICONTROL Functions]** till regeln.

   ![hanterare för skickad överföring](assets/form-submission-handler.png)

1. Välj **[!UICONTROL Done]** för att spara regeln.