---
title: Versionsinformation för Cloud Manager 2025.4.0 i Adobe Experience Manager as a Cloud Service
description: Läs om Cloud Manager 2025.4.0 i AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6dc92a0f824ca9bc3726b48581ace232302691e5
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.4.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Läs om Cloud Manager 2025.4.0 i AEM (Adobe Experience Manager) as a Cloud Service.


Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2025.4.0 i AEM as a Cloud Service är torsdagen den 10 april 2025.

Nästa planerade version är torsdagen den 8 maj 2025.

## Nyheter {#what-is-new}

* **(UI) Förbättrad synlighet för distribution**

  Sidan med information om pipeline-körning i Cloud Manager visar nu ett statusmeddelande (*Väntar - annan pågående uppdatering*) när en distribution väntar på att en annan distribution ska slutföras. Det här arbetsflödet gör det enklare att förstå sekvensering under miljödistributionen.  <!-- CMGR-66890 -->

  ![Dialogrutan för utvecklingsdistribution med detaljer och uppdelning](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **(UI) Förbättrad domänvalidering**

  När du lägger till en domän visas nu ett fel i Cloud Manager om domänen redan är installerad på ett snabbkonto: *Domänen är redan installerad på ett snabbkonto. Ta bort det först från den platsen innan du lägger till i Cloud Service.*&quot;

## Program för tidigt antagande {#early-adoption}

Delta i Cloud Manager tidiga Adobe-program och få exklusiv tillgång till kommande funktioner innan de släpps.

Följande tidiga introduktionsmöjligheter finns för närvarande:

### Använd din egen Git - nu med stöd för GitLab och Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

Funktionen **Hämta egen Git** har utökats med stöd för externa databaser, som GitLab och Bitbucket. Det nya stödet är utöver det stöd som redan finns för privata och företags GitHub-databaser. När du lägger till dessa nya rapporter kan du även länka dem direkt till dina rörledningar. Du kan lagra dessa databaser på publika molnplattformar eller i ditt privata moln eller din privata infrastruktur. Integreringen eliminerar också behovet av konstant kodsynkronisering med Adobe-databasen och ger möjlighet att validera pull-begäranden innan de slås samman till en huvudgren.

Pipelinjer som använder externa databaser (utom GitHub-värddatabaser) och **Distributionsutlösaren** som är inställd på **Vid Git-ändringar** startar nu automatiskt.

Se [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>För närvarande gäller kvalitetskontrollerna av koden för pull-begäran som är klar endast för GitHub-värdbaserade databaser, men en uppdatering som utökar den här funktionen till andra Git-leverantörer finns i arbetsflödet.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.

### AEM Home {#aem-home}

AEM Home har nu en central startpunkt för hantering av innehåll, resurser och webbplatser i Adobe Experience Manager. AEM Home är utformat för att leverera en personaliserad upplevelse och du kan navigera smidigt i AEM ekosystem efter dina roller och mål. Det är en guide som ger viktiga insikter och rekommenderade åtgärder som hjälper er att uppnå era mål på ett effektivt sätt. Med en tydlig, personstyrd layout får AEM Home snabb tillgång till viktiga verktyg, vilket ger en smidig och effektiv upplevelse för alla AEM-funktioner.

AEM Home är tillgängligt för användare som är tidiga och har en optimerad upplevelse som fokuserar på att förbättra arbetsflöden, prioritera mål och leverera resultat. Genom att välja in kan du påverka utvecklingen av AEM Home genom att ge feedback som hjälper dig att forma framtiden och som ökar värdet för hela AEM community.

Om du är intresserad av att testa den nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Var noga med att inkludera följande information:

* Den roll som bäst passar din profil: Innehållsförfattare, Utvecklare, Affärsägare, Administratör eller Annan (ange en beskrivning).
* Din primära AEM-åtkomstyta: AEM Sites, AEM Assets, AEM Forms, Cloud Manager eller annan (ange en beskrivning).

## Felkorrigeringar

* **Problem med certifikat som saknar fält för eget namn (CN)**

  Cloud Manager ger inte längre NullPointerException (NPE) och 500 HTTP-svar vid bearbetning av EV-/OV-certifikat som inte innehåller något Common Name (CN) i ämnesfältet. Moderna certifikat utelämnar ofta CN och använder i stället det alternativa ämnesnamnet (SAN). Den här korrigeringen säkerställer att frånvaron av CN inte längre orsakar ett fel under konfigurationsbyggprocessen när SAN finns. <!-- CMGR-67548 -->

* **Domänverifieringsproblem med felaktig certifikatmatchning**

  Cloud Manager verifierar inte längre domäner felaktigt med fel certifikat. Tidigare använde valideringslogiken mönsterbaserad matchning i stället för exakt matchning, vilket gjorde att domäner som `should-not-be-verified.example.com` visas som verifierade på grund av överlappning med giltiga certifikat för `example.com`. Den här korrigeringen ser till att domänverifieringen nu söker efter exakta matchningar och förhindrar felaktiga certifikatassociationer. <!-- CMGR-67225 -->

* **Kräv unikhet för framåtnamn för porten för avancerat nätverk**

  Cloud Manager använder nu unika namn för porten Advanced Networking framåt. Tidigare tilläts dubblettnamn, vilket kan leda till konflikter. Med den här korrigeringen säkerställs att varje post för porten framåt har ett distinkt namn som är anpassat till bästa praxis för nätverkskonfigurationens integritet. <!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

