---
title: Micro-FrontEnd Content Fragment Selector för Adobe Experience Manager as a Cloud Service
description: Använd Micro-Frontend Content Fragment Selector för att söka, hitta och hämta innehållsfragment från programmet.
role: Admin, User
source-git-commit: 426e958444446174bf90a13ad831c8604fddecc4
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---


# Micro-Frontend Content Fragment Selector {#micro-frontend-content-fragment-selector}

Micro-Front Content Fragment Selector är ett användargränssnitt som enkelt kan integreras med Adobe Experience Manager (AEM) as a Cloud Service-databasen. I gränssnittet kan du bläddra bland eller söka efter innehållsfragment i databasen och använda dem i programmet.

Användargränssnittet Micro-Frontend är tillgängligt i programmet med hjälp av paketet Content Fragment Selector. Alla uppdateringar av paketet importeras automatiskt och läses in i programmet.

![Mikrofon-end Content Fragment Selector - Översikt](/help/headless/assets/content-fragment-selector-overview.png)

Väljaren för innehållsfragment har många fördelar, till exempel:

* Enkel integrering med alla Adobe-program.
* Enkelt att underhålla eftersom uppdateringar av paketet för innehållsfragmentväljare automatiskt distribueras till den innehållsfragmentväljare som är tillgänglig för ditt program. Det innebär att ditt program inte behöver vidta åtgärder för att läsa in de senaste ändringarna.
* Enkel anpassning med hjälp av egenskaper som styr visningen av väljaren för innehållsfragment i programmet.
* Fulltextsökning, tillsammans med anpassningsbara filter, gör att du snabbt kan navigera i innehållsfragment i redigeringsmiljön.
* Möjlighet att växla databaser inom en IMS-organisation för val av innehållsfragment.
* Möjlighet att sortera innehållsfragment och visa dem i den valda vyn.

## Förutsättningar {#prerequisites}

### IMS-autentisering {#ims-authentication}

Om du behöver arbetsflödet för IMS-autentisering måste du se till att:

* Programmet körs på `HTTPS`.
* Programmets URL finns i listan över tillåtna omdirigerings-URL:er för IMS-klienten.
* Inloggningsflödet för IMS konfigureras och återges med hjälp av en popup-meny i webbläsaren. Därför bör popup-fönster vara aktiverade eller tillåtna i målwebbläsaren.

Om ditt program redan är autentiserat med IMS-arbetsflödet kan du lägga till lämplig IMS-information i stället.

## Installation {#installation}

Använd komponenten `ContentFragmentSelector`. Det finns flera installationsalternativ:

1. NPM-register (privat Adobe-register)

   * Lägg till följande i `.npmrc`:

     ```html
     @aem-sites:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-sites-release/
     ```

   * Installera sedan

     ```html
     npm install @aem-sites/content-fragment-selector
     ```

1. Git-databas

   * Lägg till följande i `package.json` beroenden:

     ```html
     "@aem-sites/content-fragment-selector": "git+https://github.com/adobe/<your-private-repo-url>.git#version"
     ```

## Använda väljaren för innehållsfragment {#using-the-Content-Fragment-selector}

När väljaren för innehållsfragment har konfigurerats och autentiserats för att använda väljaren för innehållsfragment med ditt AEM as a Cloud Service-program kan du välja Innehållsfragment eller utföra olika andra åtgärder för att söka efter dina fragment i databasen:

![Innehållsfragmentväljaren](/help/headless/assets/content-fragment-selector-using.png)

* Med väljaren **Databas** överst till höger kan du välja den databas som du vill använda
* I panelen längst till vänster kan du:
   * Dölja eller visa mappar från den valda databasen
   * Välj en specifik mapp för att visa innehållsfragment i den mappen
* På huvudpanelen kan du:
   * Markera innehållsfragment
   * Sök efter innehållsfragment
   * Sortera den aktuella listan efter olika kolumner, både stigande och fallande
   * Se indikatorn för visningsformat
   * Visa, dölja och ange filter

### Visa/dölj panelen {#hide-show-panel}

Om du vill dölja mappar i den vänstra navigeringen klickar du på ikonen **Dölj mappar** . Om du vill ångra ändringarna klickar du på ikonen **Dölj mappar** igen.

### Databasväxlare {#repository-switcher}

Med väljaren för innehållsfragment kan du välja en databas för fragmentval.

Du kan välja vilken databas du vill använda i listrutan **Databas**, som finns högst upp på huvudpanelen.

![Innehållsfragmentväljaren](/help/headless/assets/content-fragment-repository-selector.png)

De databasalternativ som är tillgängliga i listrutan baseras på egenskapen `repositoryId` som är definierad i filen `index.html`. Den här egenskapen baseras på miljön från den valda IMS-organisationen som användaren är inloggad på.

Konsumenterna kan skicka en föredragen `repositoryID` för att återge fragment från en viss databas och sluta återge databasväljaren.

### Mappar för innehållsfragment {#content-fragments-folders}

Databasen för innehållsfragment är en samling med mappar för innehållsfragment som du kan använda för att utföra åtgärder.

### Filter {#filters}

Med väljaren för innehållsfragment kan du också förfina sökresultaten med färdiga filteralternativ. Det finns olika filter, bland annat:

* **Fragmentmodell**
* **Lokalisering**
* **Status**: fragmentets aktuella tillstånd; `New`, `Draft`, `Published`, `Modified`, `Unpublished`
* Taggar
* Användare
* Tidpunkter och datum

![Filteralternativ](/help/headless/assets/content-selector-filters.png)

Du kan också skapa ett standardsökfilter för att spara för framtida bruk. Om du vill skapa anpassade sökfilter för dina innehållsfragment kan du använda egenskapen `filterSchema`.

### Sökfältet {#search-bar}

Med väljaren för innehållsfragment kan du utföra en fullständig textsökning av fragment i den valda databasen. Om du till exempel skriver nyckelordet `wave` i sökfältet visas alla fragment med nyckelordet `wave` som nämns i någon av metadataegenskaperna.

### Sortering {#sorting}

Du kan sortera fragment i väljaren för innehållsfragment efter olika egenskaper. Du kan också sortera fragmenten i stigande eller fallande ordning.

### Vytyp {#view-type}

Med väljaren för innehållsfragment kan du visa fragmentet i:

* **Tabellvy**
