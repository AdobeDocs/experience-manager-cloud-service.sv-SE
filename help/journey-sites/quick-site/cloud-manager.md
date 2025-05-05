---
title: Förstå Cloud Manager och arbetsflödet för att skapa snabbwebbplatser
description: Läs om Cloud Manager och hur det knyter ihop den nya processen för att skapa snabbwebbplatser.
exl-id: 5d264078-e552-48ca-8d82-294a646e6b1f
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 0%

---

# Förstå Cloud Manager och arbetsflödet för att skapa snabbwebbplatser {#understand-cloud-manager}

Läs om Cloud Manager och hur det knyter ihop den nya processen för att skapa snabbwebbplatser.

>[!TIP]
>
>Om din roll är exklusiv frontendutveckling kan du hoppa till artikeln [Hämta Git-databasåtkomstinformation](retrieve-access.md) under den här resan.
>
>Om du är AEM administratör, en Cloud Manager-administratör, är ansvarig för både frontend-utveckling och administratörsuppgifter, eller vill förstå hela processen i AEM för front-end-utveckling, fortsätter du att läsa det aktuella dokumentet och fortsätter på den här resan.

## Syfte {#objective}

I det här dokumentet får du hjälp att förstå hur verktyget AEM skapa snabbwebbplats fungerar och du får en översikt över hela flödet. När du har läst bör du:

* Förstå hur AEM Sites och Cloud Manager samarbetar för att underlätta framtagningen
* Se hur anpassningssteget i gränssnittet är helt fristående från AEM och kräver ingen AEM kunskap.

Det här dokumentet fokuserar på att förstå de här grundläggande delarna av lösningen för att skapa snabbwebbplatser innan du går vidare till nästa steg i kundresan där du börjar konfigurera.

Vi rekommenderar att du går igenom den här resan steg för steg, men om du redan förstår att AEM Sites och Cloud Manager arbetar tillsammans och vill börja direkt med konfigurationen kan du [hoppa till nästa steg på resan](create-site.md).

## Ansvarig roll {#responsible-role}

Den här delen av resan gäller både AEM och Cloud Manager-administratören.

## Krav och krav {#requirements-prerequisites}

Det finns flera krav innan du börjar skapa och anpassa webbplatser med verktyget Skapa snabbwebbplats.

Eftersom den här resan är avsedd för både gränssnittsutvecklare, administratörer och kombinationer av alla roller listas kraven för båda här.

Det är viktigt att förstå att det inte krävs någon AEM eller kunskap för den som utvecklar gränssnittet.

### Kunskap {#knowledge}

| Kunskap | Roll |
|---|---|
| Förståelse av standardverktyg och processer för framtagningsutveckling | Front-End Developer |
| Grundläggande kunskap i hur man skapar och hanterar webbplatser i AEM | AEM-administratör |
| Grundläggande kunskaper i Cloud Manager | Cloud Manager Administrator |

För den som utvecklar fronten behövs ingen AEM kunskap.

### verktyg {#tools}

| Verktyg | Roll |
|---|---|
| Önskad utvecklingsmiljö | Front-End Developer |
| npm | Front-End Developer |
| webbpaket | Front-End Developer |
| Tillgång till Cloud Manager | Cloud Manager Administrator |
| Bli medlem i rollen **Affärsägare** i Cloud Manager | Cloud Manager Administrator |
| Bli systemadministratör i Cloud Manager | Cloud Manager Administrator |
| Åtkomst till Admin Console | Cloud Manager Administrator |
| Bli medlem i rollen **Distributionshanteraren** i Cloud Manager | Cloud Manager Administrator |
| Bli medlem i rollen **Distributionshanteraren** i Cloud Manager | Front-End Developer |

För frontutvecklaren behöver AEM inte användas.

>[!TIP]
>
>Om du inte känner till Cloud Manager roller och rollhantering kan du läsa dokumentet Rollbaserade behörigheter i avsnittet [Ytterligare resurser](#additional-resources).

## Cloud Manager {#cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för plattformen.

För att stödja kunder med Enterprise Development Setup, är AEM as a Cloud Service helt integrerat med Cloud Manager och dess specialbyggda CI/CD-ledningar. Med verktyget för att skapa snabbwebbplatser kan du använda de här funktionerna för att skapa särskilda rörledningar för slututveckling.

För denna resa behövs ingen fullständig förståelse av Cloud Manager. På en hög nivå består Cloud Manager av flera strukturnivåer.

![Cloud Manager-struktur](assets/cloud-manager-structure.png)

* **TENANT** - Alla kunder etableras med en klientorganisation.
* **PROGRAM** - Varje klientorganisation har ett eller flera program som ofta återspeglar kundens licensierade lösningar.
* **MILJÖER** - Varje program har flera miljöer, till exempel produktion för direktinnehåll, en för mellanlagring och en för utvecklingsändamål.
* **REPOSITORY** - Miljöerna har Git-databaser där program- och front end-kod bevaras.
* **VERKTYG OCH ARBETSFLÖDEN** - Pipelines hanterar distributionen av kod från databaserna till miljöerna.

Ett exempel är ofta användbart när hierarkin ska sammanställas.

* WKND Travel and Adventure Enterprises kan vara en **tenant** som fokuserar på reserelaterade medier.
* WKND Travel and Adventure Enterprises-klienten kan ha två **program**: ett Sites-program för WKND Magazine och ett Assets-program för WKND Media.
* Programmen WKND Magazine och WKND Media skulle båda ha **miljöerna dev, stage och production**.

## Det snabba utvecklingsflödet för att skapa webbplatsen {#flow}

Det övergripande flödet är enkelt och intuitivt även om du ännu inte har någon omfattande erfarenhet av Cloud Manager.

1. Den AEM administratören loggar in i en AEM miljö och skapar en ny plats med hjälp av en platsmall.
1. Cloud Manager-administratören skapar en pipeline i Cloud Manager. Pipelinen hanterar distributionen av kod från en Git-databas till en AEM.
1. Den AEM administratören exporterar webbplatstemat från den AEM instansen av programmet och skickar det till den som utvecklar webbplatsen.
1. Cloud Manager-administratören ger gränssnittsutvecklare åtkomst till AEM Git-databasen där anpassningar kan implementeras.
1. Utvecklaren hämtar åtkomstautentiseringsuppgifter för åtkomst av Git och pipeline.
1. Utvecklaren anpassar temat och testar det med det faktiska innehållet från webbplatsen med hjälp av en proxy och implementerar sedan ändringarna i Git-databasen.
1. Utvecklaren kör pipeline för att distribuera temaanpassningarna till programmets produktionsmiljö.

![Skapa webbplats snabbt](assets/qsc-flow.png)

Den största fördelen med att använda verktyget Skapa snabbwebbplats är att den renodlade utvecklaren bara ansvarar för själva anpassningen. Utvecklaren har ingen interaktion med AEM eller behöver någon kunskap om AEM.

{{add-cm-allowlist-frontend-pipeline}}

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM snabbwebbplats:

* Förstå hur AEM Sites och Cloud Manager samarbetar för att underlätta framtagningen
* Se hur anpassningssteget i gränssnittet är helt fristående från AEM och kräver ingen AEM kunskap.

Bygg vidare på den här kunskapen och fortsätt din resa med att skapa AEM snabbwebbplats genom att gå igenom dokumentet [Skapa webbplats från mall](create-site.md), där du får lära dig hur du snabbt skapar en ny AEM med hjälp av en mall.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av processen för att skapa snabbwebbplats genom att granska dokumentet [Skapa webbplats från mall](create-site.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på resan.

* [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=sv-SE) - Om du vill ha mer information om Cloud Manager funktioner kan det vara bra att läsa den detaljerade tekniska dokumentationen.
* [Rollbaserade behörigheter](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html?lang=sv-SE) - Cloud Manager har förkonfigurerade roller med lämpliga behörigheter. I det här dokumentet finns mer information om de här rollerna och hur du administrerar dem.
* [npm](https://www.npmjs.com) - AEM teman som används för att snabbt skapa webbplatser baseras på npm.
* [webpack](https://webpack.js.org) - AEM teman som används för att snabbt skapa webbplatser är beroende av webbpaket.
