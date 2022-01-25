---
title: Konfigurera ett Dynamic Media-företagskonto
description: Lär dig hur du konfigurerar ett företagalias-konto i Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
exl-id: 886063d4-71dd-48c8-a342-884ad2c111ca
source-git-commit: 494f6803967725ca04a1cc4512c1e553b9f0282c
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Konfigurera ett Dynamic Media-företagskonto {#about-dm-alias-acct}

>[!NOTE]
>
>Funktionen för att skapa ett Dynamic Media-företagskonto finns i Prerelease Channel för januari 2022. Funktionen kommer att vara allmänt tillgänglig i februari 2022-versionen.

Dynamic Media URL:er och visningsprogrammets inbäddningskod innehåller ditt företagskontonamn. Det här kontonamnet skapades när Dynamic Media etablerades. Det kan finnas scenarier där ditt företag har genomgått ett förvärv, en omprofilering eller där du bara vill använda ett mer minnesvärt namn. I sådana fall är det inte enkelt att manuellt uppdatera företagskontots namn i alla URL:er och visningsprogrammets inbäddningskod som kommer ut ur kartongen. Dessutom finns det en möjlighet att du kan påverka din befintliga Dynamic Media-databas eller påverka direktinnehåll. Du kan lösa det här problemet genom att konfigurera ett Dynamic Media-företagskonto för alias.

Ett Dynamic Media-företagskonto som alias ser till att alla färdiga Dynamic Media-URL:er och visningsprograminbäddningskod i användargränssnittet återspeglar alla uppdateringar som görs i ditt företagskontext, till exempel omprofilering. Ett aliaskonto har också en positiv effekt på SEO (sökmotoroptimering) eftersom Dynamic Media URL:er och visningsprogrammets inbäddningskod återspeglar det nya företagskontots namn.

Tänk på följande när du konfigurerar ett Dynamic Media-företagskonto:

* Alla befintliga Dynamic Media-URL:er eller visningsprogramkod på din *live* digitala egenskaper måste uppdateras manuellt för att återspegla det nya aliasnamnet. Alla URL-adresser och visningsprogram som bäddar in kod med ditt ursprungliga Dynamic Media-företagsnamn fortsätter dock att fungera för befintliga eller nya resurser.
* Dynamic Media aliaskonto är begränsat till Experience Manager Assets redigeringsläge och leverans. Företagets aliasnamn fungerar inte med Experience Manager Sites. WCM-komponenter (Web Content Management) har inte uppdaterats för den här ändringen. Dessa komponenter fortsätter att fungera med Dynamic Media ursprungliga företagsnamn för hämtning av Dynamic Media-resurser.
* Du kan bara konfigurera ett företagalias-konto på **[!UICONTROL Edit Dynamic Media Configuration]** sida. Du kan dock skapa så många alias-konton som ett supportärende och manuellt spegla det nödvändiga aliasnamnet i Dynamic Media URL:er eller visningsprogrammets inbäddningskod.
* En färdig lösning [Cacheinvalidering](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md) kan Dynamic Media göra URL:er ogiltiga med konton för både företags- och företagsalias konfigurerade på Dynamic Media konfigurationssida i Cloud Services.
* När du konfigurerar ett företagalias-konto på **[!UICONTROL Edit Dynamic Media Configuration]** sida, för att cacheminnet ska kunna ogiltigförklaras måste du göra URL:er ogiltiga för *båda* den **[!UICONTROL Company]** konto och **[!UICONTROL Company Alias]** samtidigt.

Se även [Skapa en Dynamic Media-konfiguration i Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

## Konfigurera ett Dynamic Media-företagalias Konto {#configure-dm-alias-account}

Du börjar konfigurera ett Dynamic Media-företagskonto genom att först skicka ett supportärende. Detta steg är obligatoriskt.

1. [Använd Admin Console för att skapa ett supportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. Ange följande information i ditt supportärende:

   * Det Dynamic Media-företagets aliasnamn som du vill använda. Namnet måste innehålla *endast* bokstäver (blandat skiftläge tillåts), siffror, bindestreck och understreck.
   * Din region.
   * Om [linjaler](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md) används tidigare för att leverera Dynamic Media-innehåll via ett alternativt företagskontonamn för Dynamic Media.

1. När Dynamic Media alias-kontot har skapats av Support väljer du den as a Cloud Service logotypen för Experience Manager i Experience Manager as a Cloud Service Author för att komma åt den globala navigeringskonsolen.
1. Till vänster om konsolen väljer du verktygsikonen och går till **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** (markera inte mappikonen till vänster om **[!UICONTROL global]**). Välj sedan **[!UICONTROL Edit]**.

   ![Textfältet Dynamic Media Company Alias](/help/assets/assets-dm/dm-company-alias.png)

1. På **[!UICONTROL Edit Dynamic Media Configuration]** sida, på **[!UICONTROL Company Alias]** i textfältet skriver du det Dynamic Media-alias-kontonamn som du angav i ditt supportärende tidigare.
1. I det övre högra hörnet på sidan väljer du **[!UICONTROL Save]**.
Dynamic Media alias-konto har nu sparats och aktiverats. alla URL:er och visningsprogrammets inbäddningskod för befintliga och nya resurser återspeglar nu det nya företagets aliasnamn.