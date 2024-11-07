---
title: Versionsinformation för Cloud Manager 2024.11.0 i Adobe Experience Manager as a Cloud Service
description: Läs om Cloud Manager 2024.11.0 i AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 87293526ca9c10a142bc1d1d3a35562b171da385
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2024.11.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Läs om Cloud Manager 2024.11.0 i AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Se [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2024.11.0 i AEM as a Cloud Service är 7 november 2024.

Nästa planerade version är 5 december 2024.

## Nyheter {#what-is-new}

* Upplev det senaste inom Edge Delivery Services-innovation med AEM Cloud Service - nu tillgängligt att utforska i ditt Sandbox-program. [Läs mer](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md#auto-creation) <!-- (CMGR-62319) -->
* På sidan Domäninställningar i AEM Cloud Manager finns nu en sökfunktion som gör att du snabbt kan hitta domäner efter namn. Du kan ange nyckelord i sökfältet för att filtrera och visa matchande domäner, vilket gör det enklare att hantera flera domäner effektivt. Dessutom innehåller sidan statusfilter, till exempel **Verifierad** och **Inte verifierad**, för att förfina sökresultaten ytterligare. <!-- (CMGR-62615) -->

![Sökfält i domäninställningar](/help/implementing/cloud-manager/assets/domain-settings-search.png)

## Program för tidigt antagande {#early-adoption}

Bli en del av Cloud Manager program för tidig användning och få möjlighet att testa kommande funktioner.

### AEM {#aem-home}

AEM Home introducerar en central startpunkt för hantering av innehåll, resurser och webbplatser i Adobe Experience Manager. AEM Home är utformat för att leverera en personaliserad upplevelse och du kan navigera i det AEM ekosystemet sömlöst efter dina roller och mål. Det är en guide som ger viktiga insikter och rekommenderade åtgärder som hjälper er att uppnå era mål på ett effektivt sätt. Med en tydlig, personstyrd layout ger AEM Home snabb åtkomst till viktiga verktyg, vilket ger en smidig och effektiv upplevelse i alla AEM funktioner.

AEM Home erbjuder en optimerad upplevelse som fokuserar på att förbättra arbetsflöden, prioritera mål och leverera resultat. Genom att välja in kan du påverka AEM Hem:s utveckling genom att ge feedback som hjälper till att forma dess framtid och ökar värdet för hela AEM.

Om du är intresserad av att testa den nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Var noga med att inkludera följande information:

* Den roll som bäst passar din profil: Innehållsförfattare, Utvecklare, Affärsägare, Administratör eller Annan (ange en beskrivning).
* Din primära AEM: AEM Sites, AEM Assets, AEM Forms, Cloud Manager eller annan (ange en beskrivning).

### Använd din egen Git - nu med stöd för GitLab och Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

Funktionen **Hämta egen Git** har utökats med stöd för externa databaser som GitLab och Bitbucket. Det nya stödet är utöver det stöd som redan finns för privata och företags GitHub-databaser. När du lägger till dessa nya rapporter kan du även länka dem direkt till dina rörledningar. Du kan lagra dessa databaser på publika molnplattformar eller i ditt privata moln eller din privata infrastruktur. Den här integreringen eliminerar också behovet av konstant kodsynkronisering med databasen Adobe och ger möjlighet att validera pull-begäranden innan de slås samman till en huvudgren.

Se [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>För närvarande gäller kvalitetskontrollerna av koden för pull-begäran som är klar endast för GitHub-värdbaserade databaser, men en uppdatering som utökar den här funktionen till andra Git-leverantörer finns i arbetsflödet.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur. —>


## Felkorrigeringar

* En uppdatering åtgärdade ett problem i SonarQube där hårdkodade lösenord inte upptäcktes i vissa fall. Korrigeringen innehåller nu en utökad mönsterkontroll och anpassar sig till standardstandarder för identifiering i SonarQube. <!-- CMGR-62682 -->
* När du försöker uppdatera ett SSL-certifikat i Cloud Manager visas ett okänt fel efter att du klickat på **[!UICONTROL Update]** i dialogrutan **[!UICONTROL View & Update SSL Certificate]**. <!-- CMGR-62848 -->
* I Cloud Manager misslyckas uppdateringen av SSL-certifikat med felet&quot;Det nya certifikatet matchar inte befintliga domäner&quot;, även när domänerna är identiska men har skillnader i versaler (gemener och versaler). Uppdateringen identifierar nu domäner som skiftlägeskänsliga, i enlighet med RFC-standarder. <!-- CMGR-62844 -->
* I Cloud Manager fastnade IP-bindningar för Tillåtelselista i ett körningsläge eftersom länkar för främmande nycklar till domänkonfigurationer saknades. Korrigeringen säkerställer nu att bindningar för IP-Tillåtelselista länkar korrekt till associerade domänkonfigurationer. <!-- CMGR-62838 -->
* Cloud Manager validerar OCSP-statusen (Online Certificate Status Protocol) för ett SSL-certifikat. Adobe rekommenderar att du även validerar integriteten för ditt certifikat lokalt med ett verktyg som `openssl verify -untrusted intermediate.pem certificate.pem` innan du installerar det via Cloud Manager. Mer information finns i [dokumentationen om SSL-certifikatkrav](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates#requirements). <!-- CMGR-62341  -->



<!-- ## Known issues {#known-issues} -->