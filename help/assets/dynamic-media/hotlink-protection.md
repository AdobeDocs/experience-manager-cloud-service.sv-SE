---
title: Aktivera hotlink-skydd i Dynamic Media
description: Lär dig hur du aktiverar hotlink-skydd i Dynamic Media.
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 49302452b9544b9414ec49ce2862d9913fbfc6a6
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Aktivera hotlink-skydd i Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Aktiv länkning är när en tredjepartswebbplats använder HTML-kod för att visa en bild från din webbplats. De använder din bandbredd varje gång bilden efterfrågas eftersom besökarens webbläsare öppnar den direkt från servern. Hotlink *protection* är en metod som förhindrar att andra webbplatser direkt länkar till bilder, CSS eller JavaScript på dina webbsidor. Den här typen av skydd minskar onödig bandbreddsanvändning på ditt Dynamic Media-konto.

[Adobe Customer ](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) Support kan konfigurera ett referensfilter på CDN-nivå. På så sätt säkerställs att Dynamic Media-innehåll endast kan användas på webbplatser i din lista över tillåtna webbplatser för domänen.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager Dynamic Media. Eventuellt annat anpassat CDN stöds inte med den här funktionen. För att aktivera aktivering av hot link-skydd måste en administratör skapa en supportanmälan för att begära konfigurationsändringen av ditt Dynamic Media-konto. Det kostar inget mer att aktivera skydd av aktiva länkar.
