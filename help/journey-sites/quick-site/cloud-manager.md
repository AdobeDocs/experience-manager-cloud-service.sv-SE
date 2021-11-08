---
title: Förstå Cloud Manager och arbetsflödet för att skapa snabbwebbplatser
description: Lär dig mer om Cloud Manager och hur det knyter ihop den nya processen för att skapa snabbwebbplatser.
source-git-commit: efeb97d4bd7e7c11ec2c0ba1244a32b8b9affdab
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---


# Förstå Cloud Manager och arbetsflödet för att skapa snabbwebbplatser {#understand-cloud-manager}

Lär dig mer om Cloud Manager och hur det knyter ihop den nya processen för att skapa snabbwebbplatser.

>[!CAUTION]
>
>Verktyget Skapa snabbwebbplats är för närvarande en förhandsgranskning av teknik. Den tillhandahålls för testning och utvärdering och är inte avsedd för användning i produktionen om inte Adobe Support har kommit överens om det.

>[!TIP]
>
>Om din roll är exklusiv frontendutveckling kan du hoppa till artikeln [Hämta åtkomstinformation för Git-databasen](retrieve-access.md) på den här resan.
>
>Om du är AEM administratör, som är Cloud Manager-administratör, är ansvarig för både frontend-utveckling och administratörsuppgifter, eller vill förstå hela processen i AEM för frontend-utveckling, fortsätter du läsa det aktuella dokumentet och fortsätter på den här resan.

## Syfte {#objective}

I det här dokumentet får du hjälp att förstå hur verktyget AEM skapa snabbwebbplats fungerar och du får en översikt över hela flödet. När du har läst bör du:

* Förstå hur AEM Sites och Cloud Manager samarbetar för att underlätta utvecklingen på frontend
* Se hur anpassningssteget i gränssnittet är helt fristående från AEM och kräver ingen AEM kunskap.

Det här dokumentet fokuserar på att förstå de här grundläggande delarna av lösningen för att skapa snabbwebbplatser innan du går vidare till nästa steg i kundresan där du börjar konfigurera.

Vi rekommenderar att du går igenom den här resan steg för steg, men om du redan förstår att AEM Sites och Cloud Manager fungerar tillsammans och vill börja direkt med konfigurationen kan du [hoppa till nästa steg på resan.](create-site.md)

## Ansvarig roll {#responsible-role}

Den här delen av resan gäller både AEM och Cloud Manager-administratören.

## Krav och krav {#requirements-prerequisites}

Det finns flera krav innan du börjar skapa och anpassa webbplatser med verktyget Skapa snabbwebbplats.

Eftersom resan är avsedd för både gränssnittsutvecklare, administratörer och kombinationer av alla roller listas kraven för båda här.

Det är viktigt att förstå att det inte krävs någon AEM eller kunskap för den som utvecklar gränssnittet.

### Kunskap {#knowledge}

| Kunskap | Roll |
|---|---|
| Förståelse av standardverktyg och processer för framtagningsutveckling | Front-End Developer |
| Grundläggande kunskap i hur man skapar och hanterar webbplatser i AEM | AEM-administratör |
| Grundläggande kunskaper i Cloud Manager | Administratör för Cloud Manager |

För den som utvecklar fronten behövs ingen AEM kunskap.

### Verktyg {#tools}

| Verktyg | Roll |
|---|---|
| Önskad utvecklingsmiljö | Front-End Developer |
| npm | Front-End Developer |
| webbpaket | Front-End Developer |
| Åtkomst till Cloud Manager | Administratör för Cloud Manager |
| Bli medlem i **Företagsägare** roll i Cloud Manager | Administratör för Cloud Manager |
| Bli systemadministratör i Cloud Manager | Administratör för Cloud Manager |
| Åtkomst till Admin Console | Administratör för Cloud Manager |
| Bli medlem i **Distributionshanteraren** roll i Cloud Manager | Administratör för Cloud Manager |
| Bli medlem i **Distributionshanteraren** roll i Cloud Manager | Front-End Developer |

För frontutvecklaren behöver AEM inte användas.

>[!TIP]
>
>Om du inte känner till Cloud Manager-roller och rollhantering kan du läsa dokumentet Rollbaserade behörigheter i [Ytterligare resurser](#additional-resources) -avsnitt.

## Cloud Manager {#cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för plattformen.

För att ge stöd åt kunder med företagskonfigurationer kan AEM as a Cloud Service integreras helt med Cloud Manager och dess specialbyggda CI/CD-ledningar. Med verktyget för att skapa snabbwebbplatser kan du använda de här funktionerna för att skapa särskilda rörledningar för slututveckling.

För den här resan behövs ingen fullständig förståelse för Cloud Manager. På en hög nivå består Cloud Manager av flera strukturnivåer.

![Cloud Manager-struktur](assets/cloud-manager-structure.png)

* **TENANT** - Alla kunder tillhandahålls med en klient. **WKND Resor- och äventyföretag** kanske är en hyresgäst.
* **PROGRAM** - Varje innehavare har ett eller flera program. The **WKND Resor- och äventyföretag** en innehavare kan ha **WKND Nightlife** och **WKND-eftermiddagsprojekt** program.
* **MILJÖ** - Varje program har flera miljöer, t.ex. produktion för live-innehåll samt staging och dev för utvecklingsändamål. **WKND Nightlife** och **WKND-eftermiddagsprojekt** skulle båda ha utvecklings-, scen- och produktionsmiljöer.
* **DATABAS** - Miljöerna har Git-databaser där program- och front end-kod underhålls.
* **VERKTYG OCH ARBETSFLÖDEN** - Pipelines hanterar distributionen av kod från databaserna till miljöerna.

## Det snabba utvecklingsflödet för att skapa webbplatsen {#flow}

Det övergripande flödet är enkelt och intuitivt även om du ännu inte har någon omfattande erfarenhet av Cloud Manager.

1. Den AEM administratören loggar in i en AEM miljö och skapar en ny plats med hjälp av en platsmall.
1. Cloud Manager-administratören skapar en pipeline i molnhanteraren. Pipelinen hanterar distributionen av kod från en Git-databas till en AEM.
1. Den AEM administratören exporterar webbplatstemat från den AEM instansen av programmet och skickar det till den som utvecklar webbplatsen.
1. Cloud Manager-administratören ger gränssnittsutvecklare åtkomst till AEM Git-databasen där anpassningar kan implementeras.
1. Utvecklaren hämtar åtkomstautentiseringsuppgifter för åtkomst av Git och pipeline.
1. Utvecklaren anpassar temat och testar det med det faktiska innehållet från webbplatsen med hjälp av en proxy och implementerar sedan ändringarna i Git-databasen.
1. Utvecklaren kör pipeline för att distribuera temaanpassningarna till programmets produktionsmiljö.

![Flöde för att skapa snabbwebbplats](assets/qsc-flow.png)

Den största fördelen med att använda verktyget Skapa snabbwebbplats är att den renodlade utvecklaren bara ansvarar för själva anpassningen. Utvecklaren har ingen interaktion med AEM eller behöver någon kunskap om AEM.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM snabbwebbplats:

* Förstå hur AEM Sites och Cloud Manager samarbetar för att underlätta utvecklingen på frontend
* Se hur anpassningssteget i gränssnittet är helt fristående från AEM och kräver ingen AEM kunskap.

Bygg vidare på den här kunskapen och fortsätt din AEM snabbwebbplats genom att nästa gång du granskar dokumentet [Skapa webbplats från mall,](create-site.md) där du får lära dig hur du snabbt skapar en ny AEM med hjälp av en mall.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av processen Skapa snabbwebbplats genom att granska dokumentet [Skapa webbplats från mall,](create-site.md) Nedan följer ytterligare, valfria resurser som fördjupar sig i några koncept som nämns i det här dokumentet, men som inte behöver fortsätta på resan.

* [Dokumentation för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Om du vill ha mer information om funktionerna i Cloud Manager kan du läsa de detaljerade tekniska dokumenten direkt.
* [Rollbaserade behörigheter](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Molnhanteraren har förkonfigurerade roller med lämplig behörighet. Mer information om rollerna och hur du administrerar dem finns i det här dokumentet.
* [npm](https://www.npmjs.com) - AEM teman som används för att snabbt skapa webbplatser baseras på npm.
* [webbpaket](https://webpack.js.org) - AEM teman som används för att snabbt bygga sajter bygger på webbpaket.
