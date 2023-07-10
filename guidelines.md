---
source-git-commit: 8d8e5ba548c13d3d908a549f52a8b91946b35361
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---
# Riktlinjer för att bidra till Adobe Experience Manager-dokumentation

## Dokumentationsfilosofi

Adobe Experience Manager-användare arbetar i konkurrensutsatta miljöer och strävar efter att skapa digitala upplevelser som skiljer dem från konkurrenternas. Därför är det viktigt att Adobe när de tillhandahåller avancerade nya verktyg i AEM kompletteras med korrekt och tydlig dokumentation som gör det möjligt för kunden att omedelbart använda sin AEM och maximera avkastningen på investeringen.

Målet med den AEM dokumentationen är att ge AEM tillgång till dokumentation så snart som möjligt. Därför prioriterar AEM dokumentationsgrupp korrekt, användbar dokumentation och strävar efter att kontinuerligt uppdatera och förbättra den.

## Dokumentationsbidrag

För att ständigt förbättra AEM dokumentation är AEM välkommen att bidra till dokumentationen. Vare sig det gäller förfrågningar eller frågor kan förbättringar av dokumentationen vara korrigeringar, förtydliganden, tillägg och ytterligare exempel.

## Dokumentationsstandarder

Dokumentationsteamet i Experience Manager välkomnar bidrag till Adobe dokumentation, men alla bidrag till AEM - antingen i form av en pull-begäran eller ett problem - bör överensstämma med teamets bidrag och dokumentationsstandarder.

Bidrag som inte uppfyller dessa standarder kan avvisas.

### Experience Manager dokumentationsteam dokumenterar standardanvändningsfall.

AEM dokumentation täcker standardanvändningsfall. Användningsfall som inte omfattas av standardinstallation och -användning ingår inte i AEM.

### Dokumentationsteamet i Experience Manager dokumenterar vanligtvis inte buggar eller deras tillfälliga lösningar.

AEM dokumentation täcker standardanvändningsfall. Av den anledningen dokumenteras inte buggar, effekter orsakade av buggar och tillfälliga lösningar för buggar.

Undantag från den här regeln gäller versionsinformationen där kända problem kan listas med möjliga lösningar som har godkänts av AEM produkthantering.

### Dokumentationsbidragen är inte till för att besvara tekniska frågor.

Alla idéer du kan behöva förbättra AEM dokumentation är välkomna som bidrag. Kommentarer, problem och pull-förfrågningar är dock avsedda för *avgifter* endast. De är inte avsedda att användas för att besvara frågor om hur du använder AEM, implementerar ditt AEM eller löser tekniska problem.

Om du har frågor om hur AEM eller tekniska fel har använts ska du rapportera via den normala supportprocessen via [Experience Manager supportportal](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) eller diskuteras i [Experience Manager community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community).

***AEM ska inte ersätta Adobe kundsupport*** och alla sådana bidrag som söker svar på frågor som rör stöd avvisas.

### Bidragen ska tydligt hänvisa till berörda dokumentationssidor.

Om du skapar ett problem som kan föreslå förbättringar av dokumentationen måste du inkludera länkar till de sidor som påverkas. Om du skapar ett ärende genom att använda länken **Redigera den här sidan** på en dokumentationssida skapas ärendet automatiskt med en länk till sidan.

Detta gäller inte för pull-begäranden eftersom pull-begäranden till sin natur refererar till de berörda sidorna.

## Riktlinjer för dokumentation

Alla bidrag till AEM dokumentation måste följa vissa riktlinjer för format.

Genom att följa dessa riktlinjer blir det enklare att granska ditt bidrag och det går därför snabbare att integrera det i AEM.

### Språk och format

#### Språk

* AEM dokumentation skrivs och underhålls på amerikansk engelska.
* Håll meningar så enkla som möjligt.
* Se till att språket är klart och koncist.

Kom ihåg att läsarna av AEM är från hela världen och inte kan förväntas vara inbyggda eller flytande engelska. Undvik kollokvialism och håll språket så tydligt och enkelt som möjligt.

#### Följ Microsoft® Manual of Style

[The Microsoft® Manual of Style](https://learn.microsoft.com/en-us/style-guide/welcome/) är en kostnadsfri handbok för dokumentationsformat som fokuserar på programvarudokumentation och AEM dokumentation följer den här handboken när det är möjligt.

### Formatering

| Objekt | Stil |
|---|---|
| Element eller alternativ i användargränssnittet | **fet** |
| Filnamn, sökväg, användarindata, parametervärden | `monospaced` |
| Kod, kommandorad | ```Code Block``` |

### Skärmbilder

Skärmbilder ska användas med omdöme och endast när en textbeskrivning är otillräcklig.

Markörer eller andra anteckningar i skärmbilder (som röda ramar, pilar eller text) bör inte användas. På så sätt är skärmbilderna enklare att återanvända eller replikera i lokaliserade versioner av dokumentationen.

### Versionsspecifika referenser

Undvik om möjligt direkta referenser till en viss version i dokumentationsinnehållet. Detta gör dokumentationen mer flexibel och utbyggbar för framtida versioner.

### Användning av dag, AEM, CQ, CRX

The product should always be called by its full name **Adobe Experience Manager** för första gången i en artikel och kan därefter kallas **AEM**.

Day, Day Software, CQ och CRX bör inte användas utom när det är oundvikligt, t.ex. i klassnamn eller med hänvisning till AEM.
