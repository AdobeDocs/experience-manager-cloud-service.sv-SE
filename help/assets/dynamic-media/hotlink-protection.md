---
title: Aktivera hotlink-skydd i Dynamic Media
description: Lär dig hur du aktiverar hotlink-skydd i Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Aktivera hotlink-skydd i Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Aktiv länkning är när en tredjepartswebbplats använder HTML-kod för att visa en bild från din webbplats. De använder din bandbredd varje gång bilden efterfrågas eftersom besökarens webbläsare öppnar den direkt från servern. Hotlink *protection* är en metod som förhindrar att andra webbplatser direkt länkar till bilder, CSS eller JavaScript på dina webbsidor. Den här typen av skydd minskar onödig bandbreddsanvändning under ditt Dynamic Media-konto.

[Adobe kundsupport](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) kan konfigurera ett referensfilter på CDN-nivå. På så sätt säkerställs att Dynamic Media-innehåll endast kan användas på webbplatser i din lista över tillåtna webbplatser för domänen.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager Dynamic Media. Andra anpassade CDN stöds inte med den här funktionen. För att aktivera aktivering av hot link-skydd måste en administratör skapa en supportbiljett för att begära konfigurationsändringen av ditt Dynamic Media-konto. Det kostar inget mer att aktivera skydd av aktiva länkar.
