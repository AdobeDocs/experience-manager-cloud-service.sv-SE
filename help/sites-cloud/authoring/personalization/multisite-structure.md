---
title: Så här struktureras hantering av flera webbplatser för riktat innehåll
description: Ett diagram visar hur stöd för flera webbplatser för riktat innehåll är strukturerat
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---


# Så här struktureras hantering av flera webbplatser för riktat innehåll {#how-multisite-management-for-targeted-content-is-structured}

I följande diagram visas hur stöd för flera webbplatser för riktat innehåll är strukturerat.

Områden visas under **/content/campaign/&lt;brand>** och som standard har varje varumärke ett överordnad område, som skapas automatiskt. Varje område innehåller egna aktiviteter, upplevelser och erbjudanden.

![Struktur för flera webbplatser](/help/sites-cloud/authoring/assets/multisite-structure.png)

Om du vill söka efter riktat innehåll kan sidorna eller platserna mappas till ett område. Om det inte finns något konfigurerat område återgår AEM till det överordnad området för det specifika varumärket.

Följande diagram är ett exempel på hur logiken fungerar för tre platser, som kallas site1, site2 och site3.

![Struktur för flera webbplatser](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 söker upp myarea1 för brand1 och other area2 för brand2 baserat på områdesmappning.
* site2 söker upp myarea1 för brand1 och överordnad area för brand2 eftersom endast områdesmappningen för brand1 har definierats.
* site3 söker upp det överordnad området för brand1 och brand2 eftersom ingen annan områdesmappning har definierats alls för den här webbplatsen.
