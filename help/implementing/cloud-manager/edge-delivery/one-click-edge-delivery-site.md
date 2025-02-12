---
title: Skapa en Edge Delivery-webbplats i Cloud Manager med ett klick
description: Lär dig hur du snabbt skapar en Edge Delivery-webbplats i Cloud Manager med en enkel musklickning.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# Skapa en Edge Delivery-webbplats i Cloud Manager med ett klick {#about-one-click-edge-delivery-site}

The One Click Edge Delivery Service (EDS) är utformad för att automatisera introduktionen och driftsättningen av Edge Delivery webbplatser inom Cloud Manager. Det förenklar processen avsevärt genom att du kan klicka på en enda knapp. Den här klickningen ger den infrastruktur som krävs, integreras med GitHub för versionskontroll och konfigurerar dokument- och materiallagring i Google Drive.

Den här automatiseringen minskar den manuella arbetsinsats som krävs för att skapa den första webbplatsen. Det ger smidiga arbetsflöden, skalbarhet och förbättrar teamets prestanda när det gäller att hantera innehåll i framkanten.

## Viktiga begrepp {#key-concepts}

Viktiga begrepp när du skapar en Edge Delivery-webbplats med ett enda klick.

| Nyckelbegrepp | Beskrivning |
| --- | --- |
| Automatiserad driftsättning av Edge | <ul><li>Användare kan skapa och konfigurera Edge Delivery-webbplatser direkt.</li><li>Det minskar eller eliminerar behovet av manuella introduktionsprocesser genom att använda Cloud Manager integrering med CI/CD-arbetsflödet.</li><li>Integrerat med Cloud Manager för smidiga arbetsflöden med CI/CD.</li></ul> |
| Integrering med Cloud Manager | <ul><li>Använder Cloud Manager användargränssnitt för att utlösa One Click Edge Delivery-processen.</li><li>Ger tillgång till automatiserad generering och driftsättning av databaser.</li></ul> |
| GitHub-baserad versionskontroll | <ul><li>Skapar en GitHub-databas inom en organisation med fördefinierade mallmallar för att standardisera distributioner.</li><li>Länkar med AEM Bot för innehållsuppdateringar.</li></ul> |
| Integrering av dokument- och resurslagring | <ul><li>Skapar en Google Drive-mapp för lagring.<li>Installerar programmet AEM Code Sync i databasen, vilket ger smidig synkronisering och driftsättning.</li></li><li>Gör det möjligt för flera medarbetare att enkelt hantera dokument.</li></ul> |
| Säkerhet och skalbarhet | <ul><li>Säkerställer att företagets säkerhetsstandarder följs.</li><li>Stöder flera Edge Delivery Sites under olika Cloud Manager-klienter.</li></ul> |



## Skapa en Edge Delivery-webbplats i Cloud Manager med ett klick {#one-click-edge-delivery-site}

För att kunna skapa en Adobe Edge Delivery-webbplats med ett enda klick måste ni ha en Edge Delivery Services-licens. Licensen ingår i Adobe Experience Manager (AEM) och är nödvändig för att skapa Edge Delivery Services i Cloud Manager.

När det gäller behörigheter måste du vara medlem i rollen Affärsägare eller ha fått behörighet att lägga till eller redigera program i Cloud Manager. Med den här åtkomstnivån kan du hantera integreringen av Edge Delivery Services i dina program.

Se även [Introduktion till Edge Delivery Services i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

RÄTT AEM BOT-KONFIGURATIONER MÅSTE VARA PÅ PLATS FÖRST FÖR AUTOMATISKA INNEHÅLLSUPPDATERINGAR? SANT? FALSE?

**Så här skapar du en Edge Delivery-webbplats i Cloud Manager med ett enda klick:**

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn.
1. Klicka på ikonen ![Webbsida](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites** på den vänstra menyn under rubriken **Tjänster**.
1. På Edge Delivery-sidan i dialogrutan **Edge Delivery att göra-lista** klickar du i grupprutan **Slutför krav** på **Tillhandahåll**.
1. Ange namnet på din webbplats i textfältet **Projektnamn** i dialogrutan **Etablera Edge Delivery-plats** och klicka sedan på **Etablera**.
En popup visas nära skärmens övre mitt och du ser att Edge Delivery platsetablering har startats.
När etableringen är klar och webbplatsen har verifierats visas platsnamnet i området **Edge Delivery-platser** på Edge Delivery-sidan.

### Utforska en ny Edge Delivery-webbplats


1. Klicka på länken Git-databas till höger om webbplatsens namn.

Publicera.

Klicka på Platsnamn,

göra några ändringar och sedan publicera

Visa sidan i Förhandsgranska och ändra sedan URL:en för att visa Live-versionen.

Lägg till medarbetare.


## Förhandsgranska en Edge Delivery-webbplats med ett enda klick

## Publicera en Edge Delivery-webbplats med ett enda klick





## Lägga till medarbetare på en Edge Delivery-webbplats med ett enda klick


































Dessa förbättringar syftar till att förbättra automatiseringen, förenkla installationsprocesserna och förbättra samarbetet för Edge Delivery Services-användare. <!-- CMGR-59362 -->

![Skapa en Edge Delivery-webbplats med ett klick](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![Dialogrutan etablerar Edge Delivery-webbplats](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)