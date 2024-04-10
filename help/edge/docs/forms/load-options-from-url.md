---
title: Läs in alternativ för listrutor från URL
description: Alternativen i listrutan ingår i ett visst kalkylblad och importeras sedan till det primära kalkylbladet via den angivna URL:en.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Alternativ för listrutelistan Läs in från URL

I Edge Delivery Services kan användare välja ett värde bland en fördefinierad uppsättning med alternativ. Formulärförfattare använder `select` -element, som innehåller en lista med alternativ.
Till exempel `enquiry` -formuläret har en nedrullningsbar meny där du kan välja länder och där du kan välja bland ett antal fördefinierade länder. Den här listan innehåller en lång lista med länder avgränsade med kommatecken.

![Alternativ för nedrullningsbara listor](/help/forms/assets/drop-down-options.png)

Det kan vara besvärligt att hantera långa listor med alternativ för rullgardinsmenyer när de läggs till direkt i det blad som innehåller formulärdefinitionen. Om du skapar ett separat blad där du kan lagra de här alternativen kan du förenkla och effektivisera processen. Det här bladet fungerar som en central lagringsplats för alla alternativ i listrutan, ordnade i ett strukturerat format. Varje alternativ listas på sin egen rad, vilket underlättar hantering och uppdatering.

Låt oss utforska hur formulärutvecklingen kan förbättras genom att läsa in alternativlistan från ett annat kalkylblad via en URL.

I slutet av den här artikeln lär du dig att:

* [Definiera alternativ i ett separat kalkylblad](#define-options)
* [Lägg till URL för att läsa in alternativ i listrutan](#add-url)

## Definiera alternativ i ett separat blad {#define-options}

Skapa ett blad med två kolumner:`Option` och `Value`, för att definiera alternativen:

1. Gå till AEM projektmapp i Microsoft® SharePoint- eller Google Drive-mappen.
2. Lägg till ett blad med namnet `shared-country` i Microsoft® SharePoint Site eller i din Google Drive-mapp och lägg till följande:

   * **Alternativ**: Representerar visningsvärdena för alternativen i listrutan.
   * **Värde**: Representerar det skickade värdet när en användare väljer alternativet.

   >[!NOTE]
   >
   > Om värdet och alternativet för ett nedrullningsbart alternativ är desamma, kan kalkylbladet bara innehålla **Alternativ** kolumn.

   Vi lägger till ett nytt blad, [delat land](/help/forms/assets/enquiry-options.xlsx) för alternativen som visas i `Destination` nedrullningsbar lista i `enquiry` formulär.

   Se bilden nedan som visar `shared-country` kalkylblad:

   ![Listruta för land](/help/forms/assets/drop-down-country-options.png)
3. Förhandsgranska och publicera `shared-country` kalkylblad med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

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


