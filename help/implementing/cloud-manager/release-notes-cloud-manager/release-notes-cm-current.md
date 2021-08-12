---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service 2021.8.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service 2021.8.0
feature: Versionsinformation
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: d5e7354cb76369c36ee64866bcf8aa0c148ec472
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2021.8.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.8.0.

>[!NOTE]
>Om du vill visa den aktuella versionsinformationen för Adobe Experience Manager som en Cloud Service klickar du [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.8.0 är 12 augusti 2021.
Nästa version är planerad till 9 september 2021.

### Nyheter {#what-is-new}

* Cloud Service kan nu visa serviceavtalsrapporter (SLA) i Cloud Manager. Detta kommer att göras tillgängligt stegvis under de närmaste månaderna.
Mer information finns i [SLA-rapportering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html).

* Typen och allvarlighetsgraden för kvalitetsreglerna IndexType och `IndexDamAssetLucene` har ändrats. Dessa är nu båda Bugs of Blocker *serverity*.

* Nya kvalitetsregler för Oak-index har införts för att omfatta asynkrona konfigurationer och kodkonfigurationer.

* Öka det högsta antalet SSL-certifikat per program till 50.

* Självbetjäning som gör att användare kan skapa och hantera flera databaser via användargränssnittet i Cloud Manager.

* SonarQube läste historikdata för Git i onödan. På stora kodbaser kan detta leda till en onödig prestandaförbättring.

* Det finns nu ett API för att göra Maven-beroendecachen ogiltig per pipeline.

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 28.

### Felkorrigeringar {#bug-fixes}

* Status för tillgänglig uppdatering ska inte visas när den senaste versionen är mindre än den aktuella versionen.

* Inledande introduktion misslyckades för nya organisationer med mycket långa namn.

* När en pipeline aktiveras två gånger av någon anledning resulterar det i att en av körningarna misslyckas med *det går inte att uppdatera pipelinekörningsstatus*-fel.


