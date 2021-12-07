---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.10.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.10.0
feature: Release Information
source-git-commit: 14042b45b14f2c5575fc96979579bb0aaffc9a17
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.10.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Om du vill visa den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service klickar du på [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.10.0 är 14 oktober 2021.


### Nyheter {#what-is-new}

* Som en förberedelse för vissa kommande ändringar kommer befintliga distributionsrutnät nu att refereras och märkas i användargränssnittet som **Hel hög** rörledningar.

* Pipelinekortet har uppdaterats så att det nu visas ett enda, integrerat ansikte som visar både pipelines för produktion och icke-produktion, och användaren kan välja Kör/Pausa/Fortsätt direkt på den åtgärdsmeny som är kopplad till varje pipeline.

* En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via gränssnittet.

* Lägg till och redigera rörliga upplevelser har uppdaterats för att nu använda välbekanta, moderna moduler.

* Användare av Cloud Manager kan nu skicka feedback direkt från användargränssnittet via **Feedback** överst till höger på landningssidan.

* Årliga SLA-diagram kan nu hämtas från användargränssnittet i Cloud Manager.

* Kodkvalitet och icke-produktionsrelaterade pipeline-körningar kommer nu att använda en mer effektiv, ytlig kloningsprocess under byggsteget, vilket ger en snabbare byggtid för kunder med särskilt stora Git-databaser.

* Guiden Lägg till IP Tillåtelselista informerar nu användaren om maximalt tillåtet antal IP-Tillåtelselista har uppnåtts.

* API-dokumentationen för Cloud Manager innehåller nu en interaktiv spelningsmiljö som gör att inloggade användare kan experimentera med API:t från sin webbläsare. Se [API-spelning för Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) för mer information.

* Verktygstipset på programkortet blir mer beskrivande om ett markeringsalternativ under Navigera till är inaktiverat. Nu visas&quot;En produktionsmiljö finns inte&quot;.

### Felkorrigeringar {#bug-fixes}

* I sällsynta fall, när en Adobe-personal skulle återställa en kunds miljö, ansågs återställningen vara fullständig innan miljön var helt i drift.

* Vissa interna begäranden som gjordes när miljön skapades har inte gjorts om.

* Om ett distributionsfel uppstår efter domännamnsverifiering har felmeddelandet korrigerats för att begära att kunden kontaktar sin Adobe-representant.

