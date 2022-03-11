---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.8.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.8.0
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.8.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.8.0.

>[!NOTE]
>Om du vill visa den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service klickar du på [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.8.0 är 12 augusti 2021.

### Nyheter {#what-is-new}

* Cloud Service kan nu visa serviceavtalsrapporter (SLA) i Cloud Manager. Detta kommer att göras tillgängligt stegvis under de närmaste månaderna.
Se [SLA-rapportering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) om du vill veta mer.

* Typ och allvarlighetsgrad för IndexType och `IndexDamAssetLucene` kvalitetsreglerna har ändrats. Nu finns båda Bugs of Blocker *serverity*.

* Nya kvalitetsregler för Oak-index har införts för att omfatta asynkrona konfigurationer och kodkonfigurationer.

* Öka det högsta antalet SSL-certifikat per program till 50.

* Självbetjäning som gör att användare kan skapa och hantera flera databaser via användargränssnittet i Cloud Manager.

* SonarQube läste historikdata för Git i onödan. På stora kodbaser kan detta leda till en onödig prestandaförbättring.

* Det finns nu ett API för att göra Maven-beroendecachen ogiltig per pipeline.

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 29.

### Felkorrigeringar {#bug-fixes}

* Status för tillgänglig uppdatering ska inte visas när den senaste versionen är mindre än den aktuella versionen.

* Inledande introduktion misslyckades för nya organisationer med mycket långa namn.

* När en pipeline av någon anledning aktiveras två gånger resulterar det ibland i att en av körningarna misslyckas med *det går inte att uppdatera körningsstatus för pipeline* fel.
