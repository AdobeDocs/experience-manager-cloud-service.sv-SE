---
title: Alternativ för listrutealternativ från en URL eller ett annat blad för Edge Delivery Services för AEM Forms as a Cloud Service
description: Alternativen i listrutan ingår i ett visst kalkylblad och importeras sedan till det primära kalkylbladet via den angivna URL:en.
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Alternativ från en URL eller ett annat blad för Edge Delivery Services för AEM Forms as a Cloud Service

Forms innehåller ofta listrutor där användarna kan välja bland fördefinierade alternativ. Dessa alternativ definieras vanligtvis i själva formuläret, men det kan vara besvärligt att hantera långa listor. I den här handboken beskrivs hur du kan förbättra formulärutvecklingen genom att läsa in listrutealternativ från ett separat kalkylblad via en URL.


Fördelarna med att läsa in en listruta från ett separat kalkylblad är:

- Förenklad hantering: Bibehåll listrutealternativen centralt för enklare uppdateringar och tillägg.
- Förbättrad effektivitet: Eliminera behovet av att lägga till långa alternativlistor manuellt i formulärdefinitionen.

![Listrutealternativ](/help/forms/assets/drop-down-options.png)


I slutet av den här artikeln lär du dig att:

- [Definiera alternativ i ett separat kalkylblad](#define-options)
- [Lägg till URL för att läsa in alternativ i listrutan](#add-url)

## Definiera alternativ i ett separat blad {#define-options}

Definiera alternativ i ett separat kalkylblad

1. Skapa ett kalkylblad:
   1. Leta upp projektmappen för AEM i Microsoft® SharePoint eller Google Drive.
   1. Lägg till ett nytt blad. Exempel:&quot;shared-country&quot;.
1. Definiera alternativkolumner:
Lägg till två kolumner:&quot;Alternativ&quot; och&quot;Värde&quot;.
   - &quot;Option&quot; definierar den text som visas i listrutan.
   - &quot;Värde&quot; definierar det skickade värdet när en användare väljer alternativet.

   >[!NOTE]
   >
   >Om både alternativ och värde är identiska krävs bara kolumnen&quot;Alternativ&quot;.

1. Fyll i kalkylblad:
Ange dina landsalternativ i kolumnen&quot;Alternativ&quot; (och&quot;Värde&quot; om det behövs).

   Se exemplet nedan för strukturen.

   ![Listruta för land](/help/forms/assets/drop-down-country-options.png)

1. Förhandsgranska och publicera `shared-country`-bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Om projektdatabasen till exempel heter&quot;weFinance&quot; finns den under kontoägaren&quot;wkndform&quot; och du använder huvudgrenen, den URL som visar bladet `shared-country`:
   `https://main--wefinance--wkndform.aem.live/enquiry.json?sheet=country`
   <!--(https://main--wefinance--wkndform.aem.live/enquiry.json?sheet=country)  -->

>[!NOTE]
>
> `?sheet=country` är en frågeparameter som har lagts till i URL:en. Den här parametern anger den JSON som filtreras baserat på bladet `shared-country`. Den dirigerar om till JSON-filen som innehåller information om olika länder.

## Lägg till URL för att läsa in alternativ i listrutan{#add-url}

Egenskapen `Options` för ett `select`-fält accepterar en URL. URL:en returnerar en JSON-matris som används som alternativ för den nedrullningsbara listan `Destination`. Så här lägger du till URL:en för att läsa in listrutealternativ:

1. Gå till AEM Project-mappen i Microsoft® SharePoint eller Google Drive och öppna kalkylbladet. Du kan också skapa nya kalkylblad för ett formulär.
1. Kopiera URL:en för bladet `shared-country` och klistra in den i kolumnen `Options` för fältet `Destination`.

   ![Kalkylblad för förfrågan](/help/forms/assets/drop-down-enquiry.png)

1. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Listruta för land](/help/forms/assets/load-dropdown-options-form.png)

Du kan referera till [frågekalkylbladet](/help/edge/assets/enquiry.xlsx) för att lägga till URL:en för att läsa in listrutealternativ.

När du har integrerat URL:en i formulärdefinitionen för att läsa in listrutealternativen visas alternativen för listrutan `Destination` från URL:en.

Om projektdatabasen till exempel heter&quot;weFinance&quot;, finns den under kontoägaren&quot;wkndform&quot; och du använder huvudgrenen, visar URL:en nedan formuläret `enquiry` med de alternativ som har sparats i det separata bladet:

`https://main--wefinance--wkndform.aem.live/enquiry-form`



