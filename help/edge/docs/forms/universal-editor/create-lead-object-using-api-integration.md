---
title: Skapa Salesforce Lead-objekt med API-integrering
description: Lär dig hur du skapar ett Salesforce Lead-objekt med API-integreringen.
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: integrera API i regelredigeraren, anropa tjänstförbättringar
exl-id: 55835ffe-1b77-449b-b76d-16c0a343cf5c
hide: true
hidefromtoc: true
index: false
source-git-commit: 3a09a3fa9b8fb3dacef4c900979c4cc256551941
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Skapa Salesforce Lead-objekt med API-integrering

I det här exemplet beskrivs hur du skapar en lead i Salesforce med API-integrering. I slutet av processen kan du:

Konfigurera en [ansluten app i Salesforce](https://help.salesforce.com/s/articleView?id=platform.ev_relay_create_connected_app.htm&type=5) för att aktivera säker API-åtkomst.

Konfigurera CORS (Cross-Origin Resource Sharing) så att kod (t.ex. JavaScript) som körs i en webbläsare kan kommunicera med Salesforce från ett visst ursprung. Lägg till startpunkten i tillåtelselista enligt nedan

![färger](assets/salesforce-cors.png)

## Inställningar för anslutna appar

Följande inställningar används i det anslutna programmet. Du kan tilldela OAuth-scope beroende på dina behov.
![connected-app-settings](assets/salesforce-connected-app-settings.png)

## Skapa API-integrering

| Namn | Värde |
|--------------------------------|------------------|
| API-URL | https://`<your-domain>`d.my.salesforce.com/services/data/v32.0/sobjects/Lead |
| Klient-ID | Specifikt för din anslutna app |
| Klienthemlighet | Specifikt för din anslutna app |
| OAuth-URL | https://login.salesforce.com/services/oauth2/authorize |
| Åtkomsttoken-URL | https://`<your-domain>`/services/oauth2/token |
| Uppdatera token-URL | https://`<your-domain>`/services/oauth2/token |
| Auktoriseringsomfång | api chatter_api full id openid refresh_token visualforce web |
| Auktoriseringshuvud | Authorization Bearer |

![api-integration](assets/salesforce-api-integration-create-lead.png)

## Indata- och utdataparametrar

Definiera indataparametrarna för API-anropet och mappa utdataparametrarna med följande json

```json
{
    "id": "00QKY000001LyJR2A0",
    "success": true
}
```

![input-output](assets/create-lead-api-integration-input-output.png)

## Skapa ett formulär

Skapa ett enkelt adaptivt formulär med den universella redigeraren för att hämta information om lead-objektet enligt nedan
![lead-object-form](assets/create-lead.png)

Hantera klickhändelsen i kryssrutan Skapa lead med regelredigeraren. Mappa indataparametrarna till värdena för de relevanta formulärobjekten enligt nedan. Visa ID:t för det Lead-objekt som nyligen skapats i TextField-objektet `leadid`
![&#x200B; rule-editor &#x200B;](assets/create-leade-rule-editor.png)

## Testa integreringen

- Förhandsgranska formuläret
- Ange meningsfulla värden
- Markera kryssrutan `Create Lead` om du vill utlösa API-anropet
- Lead-ID för det nya Lead-objektet visas i textfältet `Lead ID`.
