---
title: Läs in alternativ för listrutor från URL
description: Alternativen i listrutan ingår i ett visst kalkylblad och importeras sedan till det primära kalkylbladet via den angivna URL:en.
feature: Edge Delivery Services
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Alternativ för listrutelistan Läs in från URL

Forms innehåller ofta listrutor där användarna kan välja bland fördefinierade alternativ. Dessa alternativ definieras vanligtvis i själva formuläret, men det kan vara besvärligt att hantera långa listor. I den här handboken beskrivs hur du kan förbättra formulärutvecklingen genom att läsa in listrutealternativ från ett separat kalkylblad via en URL.


Fördelarna med att läsa in en listruta från ett separat kalkylblad är:

* Förenklad hantering: Bibehåll listrutealternativen centralt för enklare uppdateringar och tillägg.
* Förbättrad effektivitet: Eliminera behovet av att lägga till långa alternativlistor manuellt i formulärdefinitionen.




![Alternativ för nedrullningsbara listor](/help/forms/assets/drop-down-options.png)


I slutet av den här artikeln lär du dig att:

* [Definiera alternativ i ett separat kalkylblad](#define-options)
* [Lägg till URL för att läsa in alternativ i listrutan](#add-url)

## Definiera alternativ i ett separat blad {#define-options}

Definiera alternativ i ett separat kalkylblad

1. Skapa ett kalkylblad:
   1. Leta reda på AEM projektmapp i Microsoft® SharePoint eller Google Drive.
   1. Lägg till ett nytt blad. Exempel:&quot;shared-country&quot;.
1. Definiera alternativkolumner: Lägg till två kolumner: &quot;Alternativ&quot; och &quot;Värde&quot;.
   * &quot;Option&quot; definierar den text som visas i listrutan.
   * &quot;Värde&quot; definierar det skickade värdet när en användare väljer alternativet.

   >[!NOTE]
   >
   >Om både alternativ och värde är identiska krävs bara kolumnen&quot;Alternativ&quot;.

1. Fyll i kalkylbladet: Ange dina landsalternativ i kolumnen&quot;Alternativ&quot; (och&quot;Värde&quot; om det behövs).

   Se exemplet nedan för strukturen.

   ![Listruta för land](/help/forms/assets/drop-down-country-options.png)

1. Förhandsgranska och publicera `shared-country` kalkylblad med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Se webbadressen som visar `shared-country` sheet: https://main—weFinance—wkndforms.hlx.live/inquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` är en frågeparameter som läggs till i URL:en. Den här parametern anger JSON som filtreras baserat på `shared-country` blad. Den dirigerar om till JSON-filen som innehåller information om olika länder.

## Lägg till URL för att läsa in alternativ i listrutan{#add-url}

The `Options` egenskap för en `select` fältet accepterar en URL. URL:en returnerar en JSON-array som används som alternativ för `Destination` listruta. Så här lägger du till URL:en för att läsa in listrutealternativ:

1. Gå till AEM projektmapp på Microsoft® SharePoint eller Google Drive och öppna kalkylbladet. Du kan också skapa nya kalkylblad för ett formulär.
1. Kopiera URL:en för `shared-country` bladet och klistra in det i `Options` kolumn för `Destination` fält.

   ![Kalkylblad för förfrågan](/help/forms/assets/drop-down-enquiry.png)

1. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Listruta för land](/help/forms/assets/load-dropdown-options-form.png)

Du kan se [frågekalkylblad](/help/forms/assets/enquiry-options.xlsx) om du vill lägga till alternativen för URL för att läsa in listrutor.

När du har integrerat URL:en i formulärdefinitionen för att läsa in listrutealternativen kan du välja mellan alternativen för `Destination` visas från webbadressen.

Se URL:en nedan som visar `enquiry` formulär som visar de alternativ som har sparats i det separata bladet:

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## Se även

{{see-more-forms-eds}}


