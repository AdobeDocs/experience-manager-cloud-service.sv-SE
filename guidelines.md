---
source-git-commit: 87306ae90f6411d2d4e48f3afdb66e5e848073fe
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 4%

---
# Riktlinjer för att bidra till Adobe Experience Manager-dokumentation

## Dokumentationsfilosofi

Vi vet att Adobe Experience Manager-användare arbetar i mycket konkurrensutsatta miljöer och strävar efter att skapa digitala upplevelser som skiljer dem från deras konkurrenter. Därför är det viktigt att Adobe när de tillhandahåller avancerade nya verktyg i AEM kompletteras med korrekt och tydlig dokumentation som gör det möjligt för kunden att omedelbart utnyttja sin AEM och maximera avkastningen.

Målet med den AEM dokumentationen är att ge AEM tillgång till dokumentation så snart som möjligt. Därför prioriterar vi korrekt, användbar dokumentation och strävar efter att kontinuerligt uppdatera och förbättra den.

## Dokumentationsbidrag

För att ständigt förbättra AEM dokumentation är AEM välkommen att bidra till dokumentationen. Vare sig det gäller förfrågningar eller frågor kan förbättringar av dokumentationen vara korrigeringar, förtydliganden, tillägg och ytterligare exempel.

## Dokumentationsstandarder

Vi välkomnar bidrag till vår dokumentation, men alla bidrag till AEM, antingen i form av en begäran om att tjänsten ska kunna hämtas eller ett problem, bör överensstämma med våra standarder för bidrag och dokumentation.

Bidrag som inte uppfyller dessa standarder kan avvisas.

### Vi dokumenterar standardanvändningsexempel.

AEM dokumentation täcker standardanvändningsfall. Användningsfall som inte omfattas av standardinstallation och -användning ingår inte i AEM.

### Vi dokumenterar vanligtvis inte buggar eller deras tillfälliga lösningar.

AEM dokumentation täcker standardanvändningsfall. Av den anledningen är buggar, effekter orsakade av buggar och tillfälliga lösningar för buggar i allmänhet inte dokumenterade.

Undantag från den här regeln gäller versionsinformationen där kända problem kan listas med möjliga lösningar som har godkänts av AEM produkthantering.

### Dokumentationsbidragen är inte till för att besvara tekniska frågor.

Alla idéer du kan behöva förbättra AEM dokumentation är välkomna som bidrag. Kommentarer, utgåvor och pull-begäranden är dock endast avsedda för *bidrag*. De är inte avsedda att användas för att besvara frågor om hur du använder AEM, implementerar ditt AEM eller löser tekniska problem.

Frågor om hur du använder AEM eller tekniska fel som du kan ha gjort ska rapporteras via den normala supportprocessen via [Experience Manager supportportal](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) eller diskuteras i [Experience Manager community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community).

***AEM är inte en ersättning för Adobe*** kundsupport och eventuella bidrag som söker svar på supportrelaterade frågor kommer att refuseras.

### Bidragen ska tydligt hänvisa till berörda dokumentationssidor.

Om du skapar ett problem som kan föreslå förbättringar av dokumentationen måste du inkludera länkar till de sidor som påverkas. Om du skapar ett ärende genom att använda länken **Redigera den här sidan** på en dokumentationssida skapas ärendet automatiskt med en länk till sidan.

Detta gäller inte för pull-begäranden eftersom pull-begäranden till sin natur refererar till den eller de berörda sidorna.

## Riktlinjer för dokumentation

Vi ber att eventuella bidrag till vår dokumentation följer vissa riktlinjer för format.

Genom att följa dessa riktlinjer blir det enklare att granska ditt bidrag och det går därför snabbare att integrera det i vår dokumentation.

### Språk och format

#### Språk:

* AEM dokumentation skrivs och underhålls på amerikansk engelska.
* Håll meningar så enkla som möjligt.
* Se till att språket är klart och koncist.

Kom ihåg att läsare AEM dokumentation finns i hela världen och inte kan förväntas vara inbyggda eller flytande engelska. Undvik kollokvialism och håll språket så tydligt och enkelt som möjligt.

#### Följ Microsoft formathandbok

[Microsoft Manual of ](https://docs.microsoft.com/en-us/style-guide/welcome/) Style är en kostnadsfri handbok för dokumentationsformat som fokuserar på programvarudokumentation och AEM dokumentation som följer den här handboken när det är möjligt.

### Formatering

| Objekt | Format |
|---|---|
| Element eller alternativ i användargränssnittet | **fet** |
| Filnamn, sökväg, användarindata, parametervärden | `monospaced` |
| Kod, kommandorad | ```Code Block``` |

### Skärmbilder

Skärmbilder ska användas med omdöme och endast när en textbeskrivning är otillräcklig.

Markörer eller andra anteckningar i skärmbilder (som röda ramar, pilar eller text) bör inte användas. På så sätt är skärmbilderna enklare att återanvända eller att replikera i lokaliserade versioner av dokumentationen.

### Versionsspecifika referenser

Undvik om möjligt direkta referenser till en viss version i dokumentationsinnehållet. Detta gör dokumentationen mer flexibel och utbyggbar för framtida versioner.

### Användning av dag, AEM, CQ, CRX

Produkten ska alltid refereras till med sitt fullständiga namn **Adobe Experience Manager** för första gången i en artikel och kan därefter kallas **AEM**.

Day, Day Software, CQ och CRX bör inte användas utom när det är oundvikligt, t.ex. i klassnamn eller med hänvisning till AEM.
