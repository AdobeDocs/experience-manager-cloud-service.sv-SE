---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.5.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.5.0
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.5.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.5.0.

>[!NOTE]
>Om du vill visa den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service klickar du på [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.5.0 är 6 maj 2021.

### Nyheter {#what-is-new}

* Kvalitetsregeln PackageOverlaps identifierar nu fall där samma paket har distribuerats flera gånger, dvs. på flera inbäddade platser, i samma distribuerade paketuppsättning.

* Databasslutpunkten i det offentliga API:t innehåller nu Git-URL:en.

* Distributionsloggen som hämtas av en Cloud Manager-användare blir mer insiktsfull och innehåller nu information om fel och lyckade scenarier.

* Intermittenta fel som uppstod när koden skulle skickas till Adobe Git har nu åtgärdats.

* Tillägget Commerce kan nu användas för sandlådeprogram under arbetsflödet för redigeringsprogram.

* The *Redigera program* upplevelsen har uppdaterats.

* Tabellen Domännamn på sidan Miljöinformation visar upp till 250 domännamn via sidnumrering.

* The **Lösningar och tillägg** tabba in **Lägg till program** och **Redigera program** -arbetsflöden visar lösningen, även om det bara finns en lösning för programmet.

* Felmeddelandet i byggstegsloggen när bygget inte skapade några distribuerade innehållspaket var oklart.

### Felkorrigeringar {#bug-fixes}

* Ibland kan användaren se en grön&quot;aktiv&quot; status bredvid ett IP-Tillåtelselista även när konfigurationen inte har distribuerats.

* I stället för att ta bort &quot;borttagna&quot;-variabler skulle API:t för pipelines-variabler bara markera dem med status **BORTTAGEN**.

* Vissa problem med saklig kodkvalitet påverkade felaktigt tillförlitlighetsgraderingen.

* Eftersom jokerteckendomäner inte stöds tillåter inte gränssnittet användaren att skicka in en jokerteckendomän.

* När en pipeline-körning startades mellan midnatt och kl. 1 UTC garanterades inte artefaktversionen som genererades av Cloud Manager att vara större än en version som skapades föregående dag.

* När projektet med exempelkoden har skapats visas Hantera Git som en länk från hjältekortet på sidan Översikt när sandlådeprogrammet har konfigurerats.
