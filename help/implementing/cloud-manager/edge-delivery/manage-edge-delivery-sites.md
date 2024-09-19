---
title: Hantera Edge Delivery-webbplatser i Cloud Manager
description: Lär dig hur du lägger till en CDN-konfiguration på en Edge Delivery-webbplats eller tar bort en Edge Delivery-webbplats.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2b384a4233672d69de09b922fcdef6d0f84ff7df
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Hantera Edge Delivery webbplats i Cloud Manager {#manage-edge-delivery-sites}

Lär dig hur du hanterar Edge Delivery-webbplatser i Cloud Manager genom att lägga till en CDN-konfiguration till en befintlig webbplats. Du kan också ta bort en Edge Delivery-webbplats.

## Lägga till en CDN-konfiguration på en befintlig Edge Delivery-webbplats {#add-cdn-to-edge-delivery-site}

Se [Lägg till en CDN-konfiguration](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Byta namn på en Edge Delivery-webbplats (#rename-edge-delivery-site)

I Adobe Cloud Manager kan det finnas flera skäl till att byta namn på en Edge Delivery-webbplats:

* **Klarhet och organisation**: För att beskriva webbplatsens syfte bättre eller dess associerade miljö (till exempel produktion, staging).
* **Undvik förvirring**: Om flera webbplatser används kan det vara lättare att skilja dem åt genom att byta namn, vilket minskar risken för att konfigurationer eller uppdateringar används på fel plats.
* **Standardisering**: Om du vill följa en konsekvent namnkonvention som överensstämmer med organisationens riktlinjer för enklare hantering och granskning.

**Så här byter du namn på en Edge Delivery-webbplats:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med konfigurerade Edge Delivery Services där du vill lägga till en Edge Delivery-webbplats.
1. Gör något av följande:

   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka på ellipsen i slutet av en rad vars webbplats du vill byta namn på i tabellen för Edge Delivery-webbplatser.
Klicka på **Byt namn**.
   * I det övre vänstra hörnet av sidan klickar du på hamburgikonen för att visa den vänstra navigeringsmenyn. Klicka på **Edge Delivery Sites** under rubriken **Tjänster**.
Klicka på ellipsen i slutet av en rad vars webbplats du vill byta namn på i tabellen för Edge Delivery-webbplatser. Klicka på **Byt namn**.

1. I dialogrutan **Redigera Edge Delivery-webbplats** anger du platsens nya namn i textfältet **Platsnamn**.

1. Klicka på **Redigera**.

## Ta bort en Edge Delivery-webbplats {#delete-edge-delivery-site}

Om du tar bort en webbplats för Edge Delivery Services tas även alla associerade CDN-konfigurationer bort. Den här åtgärden bryter anslutningen mellan anpassade domäner och platsen. Mer information finns i CDN-konfigurationer. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Så här tar du bort en Edge Delivery-webbplats:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med konfigurerade Edge Delivery Services där du vill lägga till en Edge Delivery-webbplats.
1. Gör något av följande:

   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka på ellipsen i slutet av en rad vars webbplats du vill ta bort i tabellen för Edge Delivery-webbplatsen.
Klicka på ![Ta bort Edge Delivery-webbplats](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Ta bort** och klicka sedan på **Ta bort** igen för att bekräfta att webbplatsen har tagits bort.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * Klicka på ![Visa eller dölj sidnavigering](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidnavigeringsmenyn. Under rubriken **Tjänster** klickar du på ![Webbsida för Edge Delivery-webbplatser](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**.
Klicka på ellipsen i slutet av en rad vars webbplats du vill ta bort i tabellen för Edge Delivery-webbplatsen. Klicka på ![Ta bort Edge Delivery-webbplats](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Ta bort** och klicka sedan på **Ta bort** igen för att bekräfta att webbplatsen har tagits bort.

     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery-platser](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Logga en supportanmälan {#eds-support-ticket}

{{support-ticket}}


