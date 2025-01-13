---
title: Testning av kodkvalitet
description: Lär dig hur kodkvalitetstestning av rörledningar fungerar och hur det kan förbättra kvaliteten på dina distributioner.
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 91a1fb46d4300540eeecf38f7f049a2991513d29
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# Kodkvalitetstestning {#code-quality-testing}

Lär dig hur kodkvalitetstestning av rörledningar fungerar och hur det kan förbättra kvaliteten på dina distributioner.

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Kodkvalitetstestning"
>abstract="Kodkvalitetstestningen utvärderar din programkod baserat på en uppsättning kvalitetsregler. Det är det främsta syftet med en rörledning av kodkvalitet och genomförs omedelbart efter byggsteget i alla rörledningar för produktion och icke-produktion."

## Introduktion {#introduction}

Kodkvalitetstestningen utvärderar din programkod baserat på en uppsättning kvalitetsregler. Det är det främsta syftet med en rörledning av kodkvalitet och genomförs omedelbart efter byggsteget i alla rörledningar för produktion och icke-produktion.

Se [Konfigurera CI-CD-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) om du vill veta mer om olika typer av pipelines.

## Regler för kodkvalitet {#understanding-code-quality-rules}

Kodkvalitetstestning söker igenom källkoden för att säkerställa att den uppfyller vissa kvalitetskriterier. En kombination av SonarQube och granskning på innehållspaketnivå med OakPAL implementerar det här steget. Det finns mer än 100 regler som kombinerar allmänna Java-regler och AEM-specifika regler. Vissa AEM-specifika regler baseras på god praxis från AEM och kallas [anpassade regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md).

Du kan hämta den aktuella fullständiga listan med regler [med den här länken](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx).

>[!IMPORTANT]
>
>Från och med torsdagen den 13 februari 2025 (Cloud Manager 2025.2.0) använder Cloud Manager Code Quality en uppdaterad version av SonarQube 9.9 och en uppdaterad lista över regler som du kan [hämta här](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx).

### Tre nivåindelade omdömen {#three-tiered-gate}

Problem som identifieras med kodkvalitetstestning tilldelas en av tre kategorier.

* **Kritisk** - Problem som orsakar ett omedelbart fel i pipeline.

* **Viktigt** - Problem som gör att pipeline försätts i pausat läge. En driftsättningshanterare, projektledare eller affärsägare kan antingen åsidosätta problemen, så att pipeline kan fortsätta. Alternativt kan de acceptera problemen, vilket gör att pipelinen avbryts om ett fel uppstår.

* **Info** - Problem som tillhandahålls endast i informationssyfte och som inte påverkar pipelinekörningen

>[!NOTE]
>
>I en pipeline med enbart kodkvalitet kan viktiga fel i kodkvalitetsgaten inte åsidosättas eftersom teststeget för kodkvalitet är det sista steget i pipeline.

### Klassificeringar {#ratings}

Resultatet av det här steget levereras som **graderingar**.

I följande tabell sammanfattas klassificerings- och feltrösklarna för var och en av de kritiska, viktiga och informativa kategorierna.

| Namn | Definition | Kategori | Feltröskel |
|--- |--- |--- |--- |
| Säkerhetsbedömning | A = Ingen sårbarhet <br/>B = Minst 1 mindre sårbarhet<br/> C = Minst 1 större sårbarhet <br/>D = Minst 1 allvarlig sårbarhet <br/>E = Minst 1 blockerarsårbarhet | Kritisk | &lt; B |
| Tillförlitlighetsgrad | A = Inga buggar <br/>B = Minst ett mindre fel <br/>C = Minst ett större fel <br/>D = Minst ett kritiskt fel <br>E = Minst ett fel i en blockerare | Kritisk | &lt; D |
| Underhållskvalitet | Definieras av den utestående reparationskostnaden för kod luktar som en procentandel av den tid som redan har gått in i programmet <br/><ul><li>A = &lt;=5%</li><li>B = 6-10 %</li><li>C = 11-20 %</li><li>D = 21-50 %</li><li>E = >50 %</li></ul> | Viktigt | &lt; A |
| Täckning | Definieras av en blandning av radens täckning och villkorstäckning med formeln: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = Villkor som har utvärderats som `true` minst en gång under körning av enhetstester</li><li>`CF` = Villkor som har utvärderats som `false` minst en gång under körning av enhetstester</li><li>`LC` = Täckta rader = lines_to_cover - uncover_lines</li><li>`B` = totalt antal villkor</li><li>`EL` = totalt antal körbara rader (lines_to_cover)</li></ul> | Viktigt | &lt; 50 % |
| Överhoppade enhetstester | Antal överhoppade enhetstester | Info | > 1 |
| Öppna ärenden | Generella problemtyper - sårbarheter, fel och kodmellanslag | Info | > 0 |
| Duplicerade rader | Definieras som antalet rader som ingår i duplicerade block. Ett kodblock anses duplicerat under följande villkor.<br>Projekt som inte är Java:<ul><li>Det ska finnas minst 100 efterföljande och duplicerade tokens.</li><li>Dessa variabler bör spridas över åtminstone </li><li>30 kodrader för COBOL </li><li>20 kodrader för ABAP </li><li>10 kodrader för andra språk</li></ul>Java-projekt:<ul></li><li> Det ska finnas minst 10 efterföljande och duplicerade satser oavsett antalet tokens och rader.</li></ul>Skillnader i indrag och i stränglitteraler ignoreras när dubbletter identifieras. | Info | > 1 % |
| Kompatibilitet med Cloud Service | Antal identifierade kompatibilitetsproblem med molntjänster | Info | > 0 |

>[!NOTE]
>
>Mer detaljerade definitioner finns i [SonarQube metric Definitions](https://docs.sonarsource.com/sonarqube-server/latest/user-guide/code-metrics/metrics-definition/).

>[!NOTE]
>
>Mer information om anpassade regler för kodkvalitet som körs av [!UICONTROL Cloud Manager] finns i [Anpassade regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Hantera med falskt positiva {#dealing-with-false-positives}

Kvalitetsskanningsprocessen är inte perfekt och identifierar ibland felaktigt problem som egentligen inte är problem. Det här läget kallas **falskt positivt**.

I dessa fall kan källkoden antecknas med Java `@SuppressWarnings`-standardanteckningen som anger regel-ID som anteckningsattribut. En vanlig positiv sak är att SonarQube-regeln för att identifiera hårdkodade lösenord kan vara aggressiv om hur ett hårdkodat lösenord identifieras.

Följande kod är ganska vanlig i ett AEM projekt, som har kod för att ansluta till en extern tjänst.

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube har en sårbarhet som gör det möjligt att blockera. Men när du har granskat koden inser du att det här problemet inte är någon sårbarhet och kan kommentera koden med rätt regel-ID.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Om koden i själva verket var följande:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Den rätta lösningen är sedan att ta bort det hårdkodade lösenordet.

>[!NOTE]
>
>Även om det är en god vana att göra `@SuppressWarnings`-anteckningen så specifik som möjligt - som att bara anteckna den programsats eller det block som orsakar problemet - är det också möjligt att anteckna på klassnivå.

>[!NOTE]
>Även om det inte finns något uttryckligt steg för säkerhetstestning finns det säkerhetsrelaterade regler för kodkvalitet som utvärderas under steget för kodkvalitet. Se [Säkerhetsöversikt för AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) om du vill veta mer om säkerhet i Cloud Servicen.

## Optimering av skanning av innehållspaket {#content-package-scanning-optimization}

Som en del av kvalitetsanalysprocessen gör Cloud Manager en analys av de innehållspaket som skapats av Maven-bygget. Cloud Manager erbjuder optimeringar som snabbar upp denna process, som är effektiv när vissa paketeringsbegränsningar iakttas. Den viktigaste optimeringen avser projekt som producerar ett enda&quot;allt&quot;-paket, som innehåller flera innehållspaket från bygget, som markeras som överhoppade. När Cloud Manager identifierar detta scenario, i stället för att packa upp&quot;all&quot;-paketet, skannas de enskilda innehållspaketen direkt och sorteras baserat på beroenden. Ta till exempel följande byggutdata.

* `all/myco-all-1.0.0-SNAPSHOT.zip` (innehållspaket)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (överhoppat innehållspaket)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (överhoppat innehållspaket)

Om de enda objekten i `myco-all-1.0.0-SNAPSHOT.zip` är de två överhoppade innehållspaketen skannas de två inbäddade paketen i stället för innehållspaketet &quot;all&quot;.

För projekt som producerar dussintals inbäddade paket har den här optimeringen visat sig spara upp till 10 minuter per pipeline-körning.

Ett specialfall kan inträffa när innehållspaketet &quot;all&quot; innehåller en kombination av överhoppade innehållspaket och OSGi-paket. Om `myco-all-1.0.0-SNAPSHOT.zip` till exempel innehåller de två inbäddade paketen som nämndes tidigare och ett eller flera OSGi-paket, skapas ett nytt, minimalt innehållspaket med endast OSGi-paketen. Det här paketet har alltid namnet `cloudmanager-synthetic-jar-package` och de inkluderade paketen placeras i `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
>
>* Optimeringen påverkar inte de paket som distribueras till AEM.
>* Matchningen mellan inbäddade innehållspaket och överhoppade innehållspaket beror på filnamn. Den här optimeringen kan inte utföras om flera överhoppade paket delar samma filnamn eller om filnamnet ändras under inbäddningen.
