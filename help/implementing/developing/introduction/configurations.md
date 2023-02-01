---
title: Konfigurationer och Configuration Browser
description: Förstå AEM konfigurationer och hur de hanterar arbetsyteinställningar i AEM.
exl-id: 0ade04df-03a9-4976-a4b7-c01b4748474d
source-git-commit: 8f94d7ee3cfe436b5d41f2428b901ee1a5002993
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 0%

---

# Konfigurationer och Configuration Browser {#configuration-browser}

AEM konfigurationer används för att hantera inställningar i AEM och fungerar som arbetsytor.

## Vad är en konfiguration? {#what-is-a-configuration}

En konfiguration kan övervägas från två olika vypunkter.

* [En administratör](#configurations-administrator) använder konfigurationer som arbetsytor i AEM för att definiera och hantera grupper av inställningar.
* [Utvecklare](#configurations-developer) använder den underliggande konfigurationsmekanismen som implementerar konfigurationer för att behålla och slå upp inställningar i AEM.

Sammanfattning: ur administratörens synvinkel är konfigurationer hur du skapar arbetsytor för att hantera inställningar i AEM, medan utvecklaren bör förstå hur AEM använder och hanterar dessa konfigurationer i databasen.

Oavsett perspektiv har konfigurationerna två huvudsyften AEM:

* Konfigurationer möjliggör vissa funktioner för vissa användargrupper.
* Konfigurationer definierar åtkomsträttigheter för dessa funktioner.

## Konfigurationer som administratör {#configurations-administrator}

AEM administratör och författare kan betrakta konfigurationer som arbetsytor. De här arbetsytorna kan användas för att samla ihop grupper av inställningar samt tillhörande innehåll för organisering genom att implementera åtkomsträttigheter för dessa funktioner.

Du kan skapa konfigurationer för många olika funktioner i AEM.

* [Kontextnavsegment](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [Redigerbara mallar](/help/sites-cloud/authoring/features/templates.md)
* olika molnkonfigurationer

### Exempel {#administrator-example}

En administratör kan till exempel skapa två konfigurationer för redigerbara mallar.

* WKND-General
* WKND-Magazine

Administratören kan sedan skapa allmänna sidmallar med WKND-General-konfigurationen och sedan använda mallar som är specifika för tidskriften under WKND-Magazine.

Administratören kan sedan koppla WKND-general till allt innehåll på WKND-webbplatsen. Konfigurationen av WKND-Magazine skulle bara kopplas till tidskriftswebbplatsen.

Genom att göra detta:

* När en skribent skapar en ny sida för tidningen kan han eller hon välja bland allmänna mallar (WKND-General) eller tidskriftsmallar (WKND-Magazine).
* När en innehållsförfattare skapar en ny sida för en annan del av webbplatsen som inte är tidskriften, kan författaren bara välja bland de allmänna mallarna (WKND-General).

Liknande inställningar kan göras inte bara för redigerbara mallar utan även för molnkonfigurationer, ContextHub-segment och Content Fragment-modeller.

### Använda Konfigurationsläsaren {#using-configuration-browser}

Med Configuration Browser kan en administratör enkelt skapa, hantera och konfigurera åtkomsträttigheter för konfigurationer i AEM.

>[!NOTE]
>
>Det går bara att skapa konfigurationer med hjälp av Konfigurationsläsaren om användaren har `admin` rättigheter. `admin` Rättigheter krävs också för att tilldela behörighet till konfigurationen eller på annat sätt ändra en konfiguration.

#### Skapa en konfiguration {#creating-a-configuration}

Det är mycket enkelt att skapa en ny konfiguration i AEM med hjälp av Configuration Browser.

1. Logga in AEM as a Cloud Service och välj **verktyg** -> **Allmänt** -> **Konfigurationsläsaren**.
1. Tryck eller klicka **Skapa**.
1. Ange en **Titel** och **Namn** för din konfiguration.

   ![Skapa en konfiguration](assets/configuration-create.png)

   * The **Titel** ska vara beskrivande.
   * The **Namn** blir nodnamnet i databasen.
      * Det genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](naming-conventions.md)
      * Den kan vid behov justeras.
1. Kontrollera vilken typ av konfigurationer du vill tillåta.
   * [Kontextnavsegment](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
   * [Redigerbara mallar](/help/sites-cloud/authoring/features/templates.md)
   * olika molnkonfigurationer
1. Tryck eller klicka **Skapa**.

>[!TIP]
>
>Konfigurationer kan vara kapslade.

#### Redigera konfigurationer och deras åtkomsträttigheter {#access-rights}

Om du tänker på konfigurationer som arbetsytor kan åtkomsträttigheter anges för dessa konfigurationer för att framtvinga vem som får och inte får komma åt dessa arbetsytor.

1. Logga in AEM as a Cloud Service och välj **verktyg** -> **Allmänt** -> **Konfigurationsläsaren**.
1. Välj den konfiguration som du vill ändra och tryck eller klicka sedan på **Egenskaper** i verktygsfältet.
1. Välj eventuella ytterligare funktioner som du vill lägga till i konfigurationen
   >[!NOTE]
   >
   >Det går inte att avmarkera en funktion när konfigurationen har skapats.
1. Använd **Effektiva behörigheter** om du vill visa en matris med roller och vilka behörigheter de för närvarande har för konfigurationer.
   ![Fönstret Effektiva behörigheter](assets/configuration-effective-permissions.png)
1. Om du vill tilldela nya behörigheter anger du användar- eller gruppnamnet i dialogrutan **Välj användare eller grupp** i **Lägg till nya behörigheter** -avsnitt.
   * The  **Välj användare eller grupp** fält erbjuder automatisk komplettering baserat på befintliga användare och roller.
1. Välj lämplig användare eller roll bland resultaten för automatisk komplettering.
   * Du kan markera flera användare eller roller.
1. Markera de åtkomstalternativ som de valda användarna eller rollerna ska ha och klicka på **Lägg till**.
   ![Lägga till åtkomsträttigheter till en konfiguration](assets/configuration-edit.png)
1. Upprepa stegen för att välja användare eller roller och tilldela ytterligare åtkomsträttigheter efter behov.
1. Tryck eller klicka **Spara och stäng** när du är klar.

## Konfigurationer som utvecklare {#configurations-developer}

Som utvecklare är det viktigt att du vet hur AEM as a Cloud Service fungerar med konfigurationer och hur den bearbetar konfigurationsupplösningen.

### Separation av konfiguration och innehåll {#separation-of-config-and-content}

Även om [administratörer och användare kan tänka sig konfigurationer som arbetsplatser](#configurations-administrator) om du vill hantera olika inställningar och innehåll är det viktigt att förstå att konfigurationer och innehåll lagras och hanteras separat av AEM i databasen.

* `/content` är hemma i allt innehåll.
* `/conf` är startsida för all konfiguration.

Innehållet refererar till den associerade konfigurationen via en `cq:conf` -egenskap. AEM utför en sökning baserat på innehållet och dess kontextuella `cq:conf` för att hitta rätt konfiguration.

### Exempel {#developer-example}

I det här exemplet antar vi att du har programkod som är intresserad av DAM-inställningar.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

Startpunkten för all konfigurationssökning är en innehållsresurs, vanligtvis någonstans under `/content`. Det kan vara en sida, en komponent på en sida, en resurs eller en DAM-mapp. Det här är det innehåll som vi letar efter rätt konfiguration för i det här sammanhanget.

Nu med `Conf` -objekt kan vi hämta det specifika konfigurationsobjekt som vi är intresserade av. I detta fall är det `dam/imageserver`, som är en samling inställningar som är relaterade till `imageserver`. The `getItem` anrop returnerar `ValueMap`. Sedan läser vi en `bgkcolor` string-egenskap och ange standardvärdet FFFFFF om egenskapen (eller hela config-objektet) inte finns.

Nu ska vi titta på motsvarande JCR-innehåll:

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wknd
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

I det här exemplet antar vi en WKND-specifik DAM-mapp här och en motsvarande konfiguration. Från den mappen `/content/dam/wknd`ser vi att det finns en strängegenskap med namnet `cq:conf` som refererar till konfigurationen som ska användas för underträdet. Egenskapen ställs vanligtvis in på `jcr:content` för en resursmapp eller -sida. Dessa `conf` länkar är explicita, så det är enkelt att följa dem genom att bara titta på innehållet i CRXDE.

Hoppa inuti `/conf`, följer vi referensen och ser att det finns en `/conf/wknd` nod. Detta är en konfiguration. Observera att sökningen är helt genomskinlig för programkoden. Exempelkoden har aldrig någon dedikerad referens till den, den döljs bakom `Conf` -objekt. Vilken konfiguration som tillämpas styrs helt av JCR-innehållet.

Vi ser att konfigurationen innehåller ett fast namn `settings` nod som innehåller de faktiska objekten, inklusive `dam/imageserver` vi behöver i vårt fall. Ett sådant objekt kan tolkas som ett inställningsdokument och representeras vanligtvis av en `cq:Page` inkluderar `jcr:content` som innehåller det faktiska innehållet.

Äntligen ser vi egendomen `bgkcolor` som vår exempelkod behöver. The `ValueMap` vi kommer tillbaka från `getItem` baseras på sidans `jcr:content` nod.

### Konfigurationsupplösning {#configuration-resolution}

I det grundläggande exemplet ovan visades en enda konfiguration. Men det finns många fall där du vill ha olika konfigurationer, till exempel en global standardkonfiguration, en som skiljer sig åt för varje varumärke och kanske en specifik konfiguration för dina delprojekt.

Som stöd för detta har konfigurationssökningen i AEM arv- och reservmekanism i följande prioritetsordning:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Specifik konfiguration som refereras från `cq:conf` någonstans i `/content`
   * Hierarkin är godtycklig och kan utformas precis som webbplatsstrukturen, det är inte programkodens sak att veta detta
   * Kan ändras vid körning av användare med konfigurationsprivilegier
1. `/conf/<siteconfig>/<parentconfig>`
   * Bläddra bland föräldrar efter reservkonfigurationer
   * Kan ändras vid körning av användare med konfigurationsprivilegier
1. `/conf/<siteconfig>`
   * Bläddra bland föräldrar efter reservkonfigurationer
   * Kan ändras vid körning av användare med konfigurationsprivilegier
1. `/conf/global`
   * Systemglobala inställningar
   * Vanligtvis globala standardinställningar för din installation
   * Uppsättning med `admin` roll
   * Kan ändras vid körning av användare med konfigurationsprivilegier
1. `/apps`
   * Standardinställningar för program
   * Korrigerat med programdistribution
   * Skrivskyddad vid körning
1. `/libs`
   * AEM
   * Endast ändringsbar av Adobe, projektåtkomst tillåts inte
   * Korrigerat med programdistribution
   * Skrivskyddad vid körning

### Använda konfigurationer {#using-configurations}

Konfigurationer i AEM baseras på Sling Context-Aware Configurations. Sling-paketen innehåller ett tjänst-API som kan användas för att få kontextmedvetna konfigurationer. Kontextmedvetna konfigurationer är konfigurationer som är relaterade till en innehållsresurs eller ett resursträd som de var [som beskrivs i föregående exempel.](#developer-example)

Mer information om Context-Aware Configurations, exempel och hur du använder dem finns i [se Sling-dokumentationen.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr-webbkonsol {#confmgr-web-console}

Det finns en **ConfMgr** webbkonsol på `https://<host>:<port>/system/console/conf`, som kan visa konfigurationer för en viss sökväg/ett visst objekt.

![ConfMgr](assets/configuration-confmgr.png)

Ange bara:

* **Innehållsbana**
* **Objekt**
* **Användare**

Klicka **Lös** för att se vilka konfigurationer som är lösta och få exempelkod som löser dessa konfigurationer.

### Kontextmedveten webbkonsol för konfiguration {#context-aware-web-console}

Det finns en **Kontextmedveten konfiguration** webbkonsol på `https://<host>:<port>/system/console/slingcaconfig`, som gör det möjligt att fråga efter kontextmedvetna konfigurationer i databasen och visa deras egenskaper.

![Kontextmedveten konfigurationskonsol](assets/configuration-context-aware-console.png)

Ange bara:

* **Innehållsbana**
* **Konfigurationsnamn**

Klicka **Lös** för att hämta associerade kontextsökvägar och egenskaper för den valda konfigurationen.
