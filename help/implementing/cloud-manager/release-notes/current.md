---
title: Versionsinformation för Cloud Manager 2024.10.0 i Adobe Experience Manager as a Cloud Service
description: Läs mer om versionsinformationen för Cloud Manager 2024.10.0 i AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: b90ace2250277005d8ac250c841104c93298a605
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2024.10.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

På den här sidan visas versionsinformation för Cloud Manager version 2024.10.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager version 2024.10.0 i AEM as a Cloud Service är 3 oktober 2024.

Nästa version är planerad till 14 november 2024.

## Nyheter {#what-is-new}

* <!-- BOTH CS & AMS --> Den AEM Archetype-versionen som används i Cloud Manager har nu uppdaterats till version 26. Se [https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> När du lägger till eller redigerar nätverksinfrastruktur valideras värdena i fälten för IP-adress och nätverksmask enligt följande regler:

   * Adressutrymmet får inte överlappa adresserna som är definierade i anslutningsadressutrymmet.
   * DNS-adresser måste antingen tillhöra den nätverksmask som definieras i anslutningsadressutrymmet eller vara offentliga.

  ![Dialogrutan Lägg till nätverksinfrastruktur](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> Ändringar görs i formatet för miljödistributionsloggar för indexering, installation av ändringsbart innehåll och transformeringsjobb.

  >[!NOTE]
  >
  >Den här ändringen planeras att genomföras stegvis med ett förväntat slutdatum i december 2024.

  ![Distribuera till produktionskort](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  Loggens format kommer att ändras från en enkel post som visas i följande:

  ![Loggfil med enkla poster](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  Till en JSON-post som visas i följande:

  ![Loggfil som visar json-poster](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## Program för tidigt antagande {#early-adoption}

Bli en del av Cloud Manager program för tidig användning och få möjlighet att testa kommande funktioner.

### Använd din egen Git - nu med stöd för GitLab och Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

Funktionen **Hämta egen Git** har utökats med stöd för externa databaser som GitLab och Bitbucket. Det nya stödet är utöver det stöd som redan finns för privata och företags GitHub-databaser. När du lägger till dessa nya rapporter kan du även länka dem direkt till dina rörledningar. Du kan lagra dessa databaser på publika molnplattformar eller i ditt privata moln eller din privata infrastruktur. Den här integreringen eliminerar också behovet av konstant kodsynkronisering med databasen Adobe och ger möjlighet att validera pull-begäranden innan de slås samman till en huvudgren.

Se [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>För närvarande gäller kvalitetskontrollerna av koden för pull-begäran som är klar endast för GitHub-värdbaserade databaser, men en uppdatering som utökar den här funktionen till andra Git-leverantörer finns i arbetsflödet.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.


<!-- ## Bug fixes




## Known Issues {#known-issues} -->
