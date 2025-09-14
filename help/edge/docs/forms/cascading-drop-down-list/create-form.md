---
title: Skapa formulär med en universell redigerare
description: Skapa anpassat formulär för att testa den överlappande listrutan med API-integreringar
feature: Edge Delivery Services
role: User
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Skapa formulär med en universell redigerare

Skapa följande formulär med den universella redigeraren. Formuläret har tre nedrullningsbara listor, vars värden fylls i med API-integreringen
![adaptiv form](assets/address-form.png)

## Bosättningsland

Vid initieringen fylls den nedrullningsbara listrutan i med resultatet av API-anropet.
![initialize-event](assets/initialize-event.png)

## Processhanterare

Hanteraren för lyckade åtgärder definierades för att ställa in enum och enumNames för den nedrullningsbara listan med lämpliga värden från geonames-arrayen. Geonames-arrayen är tillgänglig under alternativet Händelsenyttolast
![event-payload](assets/event-payload.png)
![success-handler](assets/success-handler.png)

## Hämta underordnade värden

Listrutan Region fylls i när användaren gör ett val i listrutan Land. Det geonameId som är associerat med det valda landet skickas som en indataparameter till API-integreringen GetChildren

![get-children](assets/invoke-service-get-children.png)

Framgångshanteraren definierades för att ställa in enum/enumNames för listrutan StateOrRegion
![get-children-success-handler](assets/child-success-handler.png)

När du har valt stat eller provins kan du fylla i den nedrullningsbara listan genom att följa mönstret som används för att fylla i den nedrullningsbara listan.