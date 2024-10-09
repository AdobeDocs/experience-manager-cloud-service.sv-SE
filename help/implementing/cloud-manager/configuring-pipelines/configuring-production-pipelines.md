---
title: Lägg till en produktionspipeline
description: Lär dig hur du lägger till en produktionsprocess för att skapa och distribuera kod till produktionsmiljöer.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 0%

---


# Lägg till en produktionspipeline {#configure-production-pipeline}

Lär dig hur du konfigurerar produktionspipelines för att skapa och distribuera kod till produktionsmiljöer. En produktionspipeline distribuerar kod först till scenmiljön. Vid godkännande distribueras samma kod till produktionsmiljön.

En användare måste ha rollen **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** för att kunna konfigurera produktionspipelines.

>[!NOTE]
>
>Det går inte att konfigurera en produktionspipeline förrän följande har inträffat:
>
>* Programmet skapas.
>* Git-databasen har minst en gren.
>* Produktions- och mellanlagringsmiljöerna skapas.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

## Lägg till en ny produktionspipeline {#adding-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med användargränssnittet för [!UICONTROL Cloud Manager] kan du lägga till en produktionspipeline genom att följa de här stegen.

>[!TIP]
>
>Innan du konfigurerar en pipeline för framtagning bör du läsa [AEM Quick Site Creation Journey](/help/journey-sites/quick-site/overview.md) för att få en heltäckande guide med hjälp av det lättanvända AEM Quick Site Creation-verktyget. Den här resan kan hjälpa er att effektivisera utvecklingen av AEM sajt, så att ni snabbt kan anpassa sajten utan någon AEM kunskap om bakomliggande behov.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på **Lägg till** för att välja **Lägg till produktionspipeline**.

   ![Rörledningskortet i programhanteraren - översikt](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Dialogrutan **Lägg till produktionspipeline** visas. Ange ett **Pipelinenamn** som identifierar din pipeline tillsammans med följande alternativ. Klicka på **Fortsätt**.

   **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

   * **Manuell** - Starta pipelinen manuellt.
   * **Vid Git-ändringar** - Startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

   **Beteende vid viktiga måttfel** - Under pipeline-konfiguration eller redigering kan **Distributionshanteraren** definiera pipelinens beteende när ett viktigt fel påträffas i någon av kvalitetsportarna. De tillgängliga alternativen är:

   * **Fråga varje gång** - Standardinställning. Det kräver manuell åtgärd vid varje viktigt fel.
   * **Misslyckades omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Den här processen emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipelinen automatiskt när ett viktigt fel inträffar. Den här processen emulerar i princip en användare som manuellt godkänner varje fel.

   ![Konfiguration av produktionspipeline](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. På fliken **Source Code** väljer du vilken typ av kod som pipeline ska bearbeta.

   * **[Konfigurera en fullständig stackkodspipeline](#full-stack-code)**
   * **[Konfigurera en riktad distributionsprocess](#targeted-deployment)**

Mer information om olika typer av pipelines finns i [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Stegen för att slutföra skapandet av produktionsflödet varierar beroende på vilken typ av källkod du har valt. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet så att du kan slutföra konfigurationen av din pipeline.

### Konfigurera en fullständig stackkodspipeline {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och i framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfiguration.

>[!NOTE]
>
>Om det redan finns en kodrapport med fullständig stapel för den valda miljön inaktiveras den här markeringen.

**Så här konfigurerar du en fullständig stackkodspipeline:**

1. Ange följande alternativ på fliken **Source-kod**.

   * **Databas** - Definierar från vilken Git-databas som pipeline ska hämta koden.

   >[!TIP]
   > 
   >Mer information om hur du lägger till och hanterar databaser i Cloud Manager finns i [Lägg till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

   * **Git-grenen** - Definierar från vilken gren den valda pipelinen ska hämta koden.
Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de matchande förgreningarna som du kan använda för att välja.
   * **Ignorera webbnivåkonfiguration** - När det här alternativet är markerat distribueras inte webbnivåkonfigurationen.
   * **Pausa innan du distribuerar till produktion** - Pausar pipeline innan du distribuerar till produktion.
   * **Schemalagd** - Gör att användaren kan aktivera den schemalagda produktionsdistributionen.

   ![Fullständig stackkod](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Klicka på **Fortsätt** om du vill gå vidare till fliken **Experience Audit** där du kan definiera sökvägarna som alltid ska inkluderas i Experience Audit.

   ![Lägg till Experience Audit](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Ange sökvägar som ska inkluderas i Experience Audit.

   * Mer information finns i [Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-dashboard.md#configuration).

1. Klicka på **Spara** för att spara din pipeline.

När pipeline körs skickas och utvärderas sökvägar som konfigurerats för Experience Audit baserat på prestanda, tillgänglighet, SEO, bästa praxis och PWA-tester. Mer information finns i [Om Experience Audit Results](/help/implementing/cloud-manager/experience-audit-dashboard.md).

Pipelinen sparas och du kan nu [hantera dina pipelines](managing-pipelines.md) på kortet **Pipelines** på sidan **Programöversikt**.

### Konfigurera ett riktat distributionsflöde {#targeted-deployment}

En riktad distribution distribuerar bara kod för utvalda delar av AEM. I en sådan distribution kan du välja att **Inkludera** ska vara en av följande typer av kod:

* **Konfig** - Konfigurera inställningar för olika funktioner i AEM.
   * Se [Använda konfigurationsförlopp](/help/operations/config-pipeline.md) för en lista över konfigurationer som stöds, som omfattar vidarebefordran av loggar, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer, och för att hantera dem i din databas så att de distribueras korrekt.
   * När en riktad distributionsprocess körs distribueras konfigurationer, förutsatt att de sparats i den miljö, databas och gren som definierats i pipeline.
   * Det kan bara finnas en konfigurationspipeline per miljö.
* **Front End Code** - Konfigurera JavaScript och CSS för frontdelen av AEM.
   * Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.
   * I dokumentet [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) finns information om hur den här processen fungerar tillsammans med vissa överväganden som du bör vara medveten om för att få ut mesta möjliga av processen.
* **Webbnivåkonfiguration** - Konfigurera Dispatcher-egenskaper för att lagra, bearbeta och leverera webbsidor till klienten.
   * Mer information finns i dokumentet [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).
   * Om det finns en kodrapport på webbnivå för den valda miljön är det här valet inaktiverat.
   * Om du skapar en webbskiktskonfigurationspipeline för en miljö med en befintlig pipeline med en hel hög ignoreras webbskiktskonfigurationen i pipeline med en hel hög. Den här ändringen påverkar bara webbnivåkonfigurationen i den miljön.

>[!NOTE]
>
>Rörledningar för webbnivå och konfiguration stöds inte i privata databaser. Mer information och en fullständig lista över begränsningar finns i [Lägga till privata databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

**Så här konfigurerar du en riktad distributionspipeline:**

1. Välj vilken distributionstyp du behöver.

![Målinriktade distributionsalternativ](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. Definiera **berättigade distributionsmiljöer**.

   * Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.

1. Ange följande alternativ under **Source Code**:

   * **Databas** - Det här alternativet definierar från vilken Git-repo som pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) så att du kan lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-grenen** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet. Här hittas de matchande grenar som du kan välja.
   * **Kodplats** - Det här alternativet definierar sökvägen i grenen för den valda rapporten från vilken pipelinen ska hämta koden.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipelinen innan den distribueras till produktion.
   * **Schemalagd** - Gör att användaren kan aktivera den schemalagda produktionsdistributionen. Endast tillgängligt för riktade distributioner på webbnivå.

   ![Konfigurera pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Klicka på **Spara**.

Pipelinen sparas och du kan nu [hantera dina pipelines](managing-pipelines.md) på kortet **Pipelines** på sidan **Programöversikt**.

## Hoppa över Dispatcher-paket {#skip-dispatcher-packages}

Om du vill skapa Dispatcher-paket i pipeline utan att publicera dem för att bygga lagring kan du inaktivera publiceringsalternativet. Om du gör det kan det hjälpa till att minska körtiden.

Följande konfiguration för att inaktivera publicering av Dispatcher-paket måste läggas till via projektfilen `pom.xml`. En miljövariabel fungerar som en flagga som du anger i Cloud Manager byggbehållare för att avgöra när Dispatcher-paket ska ignoreras.

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
