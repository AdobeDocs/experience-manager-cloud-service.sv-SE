---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.5.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.5.0
feature: Versionsinformation
source-git-commit: d30f81b8d12a4136d96cdfd1fb8c3e9927c015d1
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2021.6.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.6.0.

>[!NOTE]
>Om du vill visa den aktuella versionsinformationen för Adobe Experience Manager som en Cloud Service klickar du [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.6.0 är 10 juni 2021.
Nästa version är planerad till 15 juli 2021.

### Nyheter {#what-is-new}

* Förhandsgranskningstjänsten kommer att distribueras rullande till alla program. Kunder meddelas i produkten när deras program är aktiverat för förhandsgranskningstjänsten. Mer information finns i [Åtkomst till förhandsgranskningstjänsten](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

* Maven Dependencies som laddas ned under byggfasen cachelagras nu mellan pipeline-körningar. Den här funktionen kommer att aktiveras för kunderna under de kommande veckorna.

* Namnet på programmet kan nu redigeras via dialogrutan Redigera program.

* Det standardförgreningsnamn som används både när projektet skapas och i det förvalda push-kommandot via Hantera Git-arbetsflöden har ändrats till `main`.

* Redigera programupplevelser i användargränssnittet har uppdaterats.

* Kvalitetsregeln `ImmutableMutableMixCheck` har uppdaterats för att klassificera `/oak:index`-noder som oföränderliga.

* Kvalitetsreglerna `CQBP-84` och `CQBP-84--dependencies` har konsoliderats till en enda regel.

* För att undvika problem har segmentraderna Publicera AEM och Publicera dispatcher på sidan Miljöinformation konsoliderats.

* En ny regel för kodkvalitet har lagts till för att validera strukturen för `damAssetLucene`-index. Mer information finns i [Anpassade DAM-resursindex Luceneak-index](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check).

* Sidan med miljöinformation visar nu flera domännamn för tjänsterna Publicera och Förhandsgranska (beroende på vad som är tillämpligt). Mer information finns i [Miljöinformation](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Felkorrigeringar {#bug-fixes}

* JCR-noddefinitioner som innehåller en ny rad efter att rotelementnamnet inte tolkades korrekt.

* API för listdatabaser filtrerar inte borttagna databaser.

* Ett felaktigt felmeddelande visades när ett ogiltigt värde angavs för schemasteget.

* Ibland kan användaren se en grön *aktiv*-status bredvid ett IP-Tillåtelselista även när konfigurationen inte har distribuerats.

* Vissa programredigeringssekvenser kan leda till att produktionsflödet inte kan skapas eller redigeras.

* Vissa programredigeringssekvenser kan resultera i att sidan **Översikt** visar ett missvisande meddelande om att köra programkonfigurationen igen.
