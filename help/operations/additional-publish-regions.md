---
title: Ytterligare publiceringsregioner
description: Läs om hur AEM as a Cloud Service stöder ytterligare publiceringsregioner för ökad tillgänglighet och minskad latens.
exl-id: b9ac3c6a-eb8b-461d-8f1d-a0356046a3f9
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Ytterligare publiceringsregioner {#additional-publish-regions}

Ytterligare publiceringsregioner kan licensieras och aktiveras i program som skapats med AEM Sites. När den är konfigurerad dirigeras trafik på scenen och i produktionsmiljöer till flera publiceringsmiljöer, vilket har följande fördelar:

* Minskad fördröjning - Begäranden som dirigeras från CDN till AEM publiceringsinstanser dirigeras till närmaste publiceringsområde, vilket är fördelaktigt för webbplatser och applikationer som besöks av användare i flera länder.
* Högre tillgänglighet - Om en region inte är tillgänglig dirigerar CDN trafiken till andra tillgängliga regioner.

Organisationer kan licensiera upp till tre ytterligare publiceringsregioner.

>[!NOTE]
>
>Den här funktionen är för närvarande endast tillgänglig för AEM Sites. Den kan inte heller tillämpas på sandlådeprogram. Tänk dessutom på att funktionen för ytterligare publiceringsregioner kräver att programmet uppdateras till AEM version 12142 eller senare.

## Användningsexempel {#use-cases}

Nedan följer några exempel på användningsområden där organisationer kan dra nytta av att licensiera ytterligare publiceringsregioner.

1. För organisationer som tar emot betydande eller affärskritisk trafik från användare långt bort från den primära regionen kan ytterligare publiceringsregioner minska den fördröjning som dessa besökare upplever.
1. För organisationer som kan drabbas av betydande penningskador eller anseendeskador när en webbplats inte är tillgänglig kan detta minskas genom att ytterligare publiceringsregioner används för att göra AEM publiceringsnivå mer motståndskraftig mot ett regionalt misslyckande.
1. För organisationer vars innehållsförfattare finns på en geografisk plats som ligger långt från de flesta besökare på publiceringsnivån kan den primära regionen väljas nära innehållsförfattarens plats, medan ytterligare publiceringsregioner kan konfigureras nära den publicerade sidans trafik, där båda målgrupperna drar nytta av en optimerad upplevelse.

## Aktivera och konfigurera {#enabling-and-configuring}

När du har licensierat ytterligare en publiceringsregion konfigureras regionerna med hjälp av Cloud Manager. Se [Dokumentation för Cloud Manager](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) för detaljerade anvisningar.

Ytterligare publiceringsregioner används i scen- och produktionsmiljöer, men inte i RDE- eller utvecklingsmiljöer.

Om en region blir otillgänglig behöver kunderna inte hantera dirigeringen av trafik till tillgängliga regioner eftersom den hanteras av Adobe CDN.

Så som beskrivs i avsnittet Avancerade överväganden om nätverksarbete nedan rekommenderas att kunder som använder avancerade nätverk konfigurerar det för varje ytterligare publiceringsregion så att tillgängligheten upprätthålls om en region blir otillgänglig.


## Avancerade nätverksöverväganden {#advanced-networking-considerations}

När ytterligare en publiceringsregion är aktiverad för ett program med avancerade nätverk redan konfigurerat, dirigeras trafiken i den extra publiceringsregionen som matchar de avancerade nätverksreglerna som standard genom den primära regionen. För att kunna utnyttja den ökade tillgängligheten rekommenderar vi att du aktiverar avancerade nätverk i de övriga regionerna.

Se [Avancerad nätverkskonfiguration för ytterligare publiceringsregioner](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) i dokumentationen för avancerade nätverk, där du får mer information om hur du lägger till avancerade nätverkskonfigurationer i ytterligare regioner utan att förlora anslutningen.

## Loggning {#logging}

Om ytterligare publiceringsregioner är aktiverade kommer separata loggar för varje region att göras tillgängliga via Cloud Manager. Mer information finns i [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) och [Loggar för ytterligare publiceringsregioner](/help/implementing/developing/introduction/logging.md#logs-for-additional-publish-regions).

## Begränsningar {#limitations}

Tänk på följande begränsningar när du funderar på att använda ytterligare publiceringsregioner.

* Ytterligare publiceringsregioner kan bara läggas till i AEM Sites. Ytterligare publiceringsregioner omfattar inte andra AEM lösningar eller relaterade funktioner som körs i samma program (t.ex. AEM Forms eller Adobe Learning Manager).
* Ytterligare regioner kan bara läggas till om associerade berättiganden är tillgängliga och inte används i klientorganisationen.
* Högst tre ytterligare publiceringsregioner kan läggas till i en enskild miljö.
* Ytterligare regioner är endast tillgängliga i produktionsprogram. Funktionen är inte tillgänglig i sandlådeprogram.
* Ytterligare publiceringsregioner används endast i scen- och produktionsmiljöer, inte i RDE- eller utvecklingsmiljöer.
* Ytterligare publiceringsregioner kräver att ditt program uppdateras till AEM version 12142 eller senare.
