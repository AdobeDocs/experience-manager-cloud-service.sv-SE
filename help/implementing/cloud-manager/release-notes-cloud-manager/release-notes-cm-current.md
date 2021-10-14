---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.10.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.10.0
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 62e9466fdfd6d6ac63dad9a2bc19693f7dc8d098
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.10.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Klicka [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html) om du vill se den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.10.0 är 14 oktober 2021.
Nästa version är planerad till den 4 november 2021.

### Nyheter {#what-is-new}

* Som förberedelse för vissa kommande ändringar kommer befintliga distributionsledningar nu att refereras och märkas i användargränssnittet som **fullständiga stackrörledningar**.

* Pipelinekortet har uppdaterats så att det nu visas ett enda, integrerat ansikte som visar både pipelines för produktion och icke-produktion, och användaren kan välja Kör/Pausa/Fortsätt direkt på den åtgärdsmeny som är kopplad till varje pipeline.

* En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via gränssnittet.

* Lägg till och redigera rörliga upplevelser har uppdaterats för att nu använda välbekanta, moderna moduler.

* Användare av Cloud Manager kan nu skicka feedback direkt från användargränssnittet via knappen **Feedback** längst upp till höger på landningssidan.

* Årliga SLA-diagram kan nu hämtas från användargränssnittet i Cloud Manager.

* Kodkvalitet och icke-produktionsrelaterade pipeline-körningar kommer nu att använda en mer effektiv, ytlig kloningsprocess under byggsteget, vilket ger en snabbare byggtid för kunder med särskilt stora Git-databaser.

* Guiden Lägg till IP Tillåtelselista informerar nu användaren om maximalt tillåtet antal IP-Tillåtelselista har uppnåtts.

* API-dokumentationen för Cloud Manager innehåller nu en interaktiv spelningsmiljö som gör att inloggade användare kan experimentera med API:t från sin webbläsare. Mer information finns i [API-spelningsvyn för Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/).

* Verktygstipset på programkortet blir mer beskrivande om ett markeringsalternativ under Navigera till är inaktiverat. Nu visas&quot;En produktionsmiljö finns inte&quot;.

### Felkorrigeringar {#bug-fixes}

* I sällsynta fall, när en Adobe-personal skulle återställa en kunds miljö, ansågs återställningen vara fullständig innan miljön var helt i drift.

* Vissa interna begäranden som gjordes när miljön skapades har inte gjorts om.

