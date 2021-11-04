---
title: Kodkvalitetstestning - Cloud Services
description: Kodkvalitetstestning - Cloud Services
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: f8695dd8fdc9ffb203bab943c335ab2957df6251
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Testning av kodkvalitet {#code-quality-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Testning av kodkvalitet"
>abstract="Kodkvalitetstestningen utvärderar kvaliteten på programkoden. Det är huvudmålet för en rörledning med enbart kodkvalitet och genomförs omedelbart efter byggsteget i alla rörledningar för icke-produktion och produktion."

Kodkvalitetstestningen utvärderar kvaliteten på programkoden. Det är huvudmålet för en rörledning med enbart kodkvalitet och genomförs omedelbart efter byggsteget i alla rörledningar för icke-produktion och produktion.

Se [Konfigurera CI-CD-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) om du vill veta mer om olika typer av rörledningar.

## Förstå regler för kodkvalitet {#understanding-code-quality-rules}

I Kodkvalitetstestning skannas källkoden så att den uppfyller vissa kvalitetskriterier. För närvarande implementeras detta genom en kombination av SonarQube och granskning på innehållspaketnivå med hjälp av OakPAL. Det finns över 100 regler som kombinerar allmänna Java-regler och AEM-specifika regler. Vissa av de AEM specifika reglerna har skapats baserat på bästa praxis från AEM och kallas för [Anpassade regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>Du kan hämta den fullständiga listan med regler [här](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx).

**Treskiktsgrind**

Det finns en struktur på tre nivåer i det här steget för kodkvalitetstestning för de identifierade problemen:

* **Kritisk**: Detta är frågor som identifieras av porten och som orsakar ett omedelbart fel i rörledningen.

* **Viktigt**: Det här är problem som identifieras av porten och som gör att pipeline försätts i pausläge. Distributionshanteraren, projektledaren eller företagsägaren kan antingen åsidosätta problemen, i vilket fall pipeline fortsätter, eller så kan de acceptera problemen. I så fall upphör pipeline med ett fel.

* **Info**: Detta är frågor som identifieras av porten och som endast tillhandahålls i informationssyfte och som inte har någon inverkan på genomförandet av pipelinen

Resultatet av det här steget levereras som *Klassificeringar*.

I följande tabell sammanfattas betygs- och feltrösklarna för var och en av kategorierna Kritisk, Viktig och Information:

| Namn | Definition | Kategori | Feltröskel |
|--- |--- |--- |--- |
| Säkerhetsklassificering | A = 0 Sårbarhet <br/>B = minst 1 mindre sårbarhet<br/> C = minst 1 allvarlig sårbarhet <br/>D = minst 1 allvarlig sårbarhet <br/>E = minst 1 Blockerbarhets - sårbarhet | Kritisk | &lt; B |
| Tillförlitlighetsklassificering | A = 0 fel <br/>B = minst 1 mindre fel <br/>C = minst 1 större fel <br/>D = minst 1 kritiskt fel E = minst 1 blockeringsfel | Viktigt | &lt; C |
| Underhållbarhetsklassificering | Oöverträffade reparationskostnader för illaluktande kod är: <br/><ul><li>&lt;=5 % av tiden som redan har gått in i programmet är klassificeringen A </li><li>Betyg 6-10 % är B </li><li>Betyg mellan 11 och 20 % är ett C </li><li>Betyg mellan 21 och 50 % är ett D</li><li>över 50 % är ett E</li></ul> | Viktigt | &lt; A |
| Täckning | En blandning av radens disponering och villkorstäckning med denna formel: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>där: CT = villkor som har utvärderats till &#39;true&#39; minst en gång under enhetstester <br/>CF = villkor som har utvärderats till &quot;false&quot; minst en gång under körning av enhetstester <br/>LC = täckta linjer = linjer_till_täckning - ej täckta_linjer <br/><br/> B = totalt antal villkor <br/>EL = totalt antal körbara rader (lines_to_cover) | Viktigt | &lt; 50 % |
| Överhoppade enhetstester | Antal överhoppade enhetstester. | Information | > 1 |
| Öppna ärenden | Generella problemtyper - sårbarheter, fel och kodmellanslag | Information | > 0 |
| Duplicerade rader | Antal rader som ingår i duplicerade block. <br/>För att ett kodblock ska betraktas som duplicerat: <br/><ul><li>**Projekt som inte är Java:**</li><li>Det ska finnas minst 100 efterföljande och duplicerade tokens.</li><li>Dessa tokens bör spridas åtminstone på: </li><li>30 kodrader för COBOL </li><li>20 kodrader för ABAP </li><li>10 kodrader för andra språk</li><li>**Java-projekt:**</li><li> Det ska finnas minst 10 efterföljande och duplicerade satser oavsett antalet tokens och rader.</li></ul> <br/>Skillnader i indrag och i stränglitteraler ignoreras när dubbletter identifieras. | Information | > 1% |
| Cloud Service-kompatibilitet | Antal identifierade kompatibilitetsproblem för Cloud Service. | Information | > 0 |

>[!NOTE]
>
>Se [Måttdefinitioner](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) för mer detaljerade definitioner.


>[!NOTE]
>
>Mer information om anpassade regler för kodkvalitet som körs av [!UICONTROL Cloud Manager], se [Anpassade regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Hantera med falskt positiva {#dealing-with-false-positives}

Kvalitetsskanningsprocessen är inte perfekt och kan ibland felaktigt identifiera problem som inte är problematiska. Detta kallas *falskt positivt*.

I dessa fall kan källkoden kommenteras med Java-standarden `@SuppressWarnings` anteckning som anger regel-ID som anteckningsattribut. Ett vanligt problem är att regeln SonarQube för att identifiera hårdkodade lösenord kan vara aggressiv om hur ett hårdkodat lösenord identifieras.

Om du vill titta på ett specifikt exempel är koden ganska vanlig i ett AEM projekt som har kod att ansluta till en extern tjänst:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube kommer då att öka en blockerbarhets - sårbarhet. När du har granskat koden identifierar du att detta inte är en sårbarhet och kan kommentera detta med rätt regel-ID.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Om koden i själva verket var så här:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Den rätta lösningen är sedan att ta bort det hårdkodade lösenordet.

>[!NOTE]
>
>Även om det är en bra rutin att göra `@SuppressWarnings` Anteckningen är så specifik som möjligt, d.v.s. kommenterar bara den specifika programsats eller det block som orsakar problemet. Det går att anteckna på klassnivå.

>[!NOTE]
>Även om det inte finns något explicit steg för säkerhetstestning finns det fortfarande säkerhetsrelaterade regler för kodkvalitet som utvärderas under steget för kodkvalitet. Se [Säkerhetsöversikt för AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) om du vill veta mer om säkerhet i Cloud Service.
