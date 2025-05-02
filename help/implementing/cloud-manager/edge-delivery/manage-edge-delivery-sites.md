---
title: Hantera Edge Delivery-webbplatser i Cloud Manager
description: Lär dig hur du lägger till en CDN-konfiguration på en Edge Delivery-webbplats eller tar bort en Edge Delivery-webbplats.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: 8e4d988934b927ecbbb29277acdd373a87193ea9
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Hantera Edge Delivery webbplats i Cloud Manager {#manage-edge-delivery-sites}

Lär dig hur du hanterar Edge Delivery-webbplatser i Cloud Manager genom att lägga till en CDN-konfiguration till en befintlig webbplats. Du kan också ta bort en Edge Delivery-webbplats.

## Lägga till en CDN-konfiguration på en befintlig Edge Delivery-webbplats {#add-cdn-to-edge-delivery-site}

Se [Lägg till en CDN-konfiguration](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Byta namn på en Edge Delivery-webbplats (#rename-edge-delivery-site)

I Adobe Cloud Manager kan det finnas flera orsaker till varför du vill byta namn på en Edge Delivery-webbplats:

* **Klarhet och organisation**: För att beskriva webbplatsens syfte bättre eller dess associerade miljö (till exempel produktion, staging).
* **Undvik förvirring**: Om flera webbplatser används kan det vara lättare att skilja dem åt genom att byta namn, vilket minskar risken för att konfigurationer eller uppdateringar används på fel plats.
* **Standardisering**: Om du vill följa en konsekvent namnkonvention som överensstämmer med organisationens riktlinjer för enklare hantering och granskning.

**Så här byter du namn på en Edge Delivery-webbplats:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med Edge Delivery Services konfigurerat, där du vill lägga till en Edge Delivery-webbplats.
1. Gör något av följande:

   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka på ellipsen i slutet av en rad vars webbplats du vill byta namn på i tabellen för Edge Delivery-webbplatser.
Klicka på **Byt namn**.
   * Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn. Klicka på ikonen ![Webbsidor](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites** under rubriken **Tjänster**.
Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars webbplats du vill byta namn på i Edge Delivery-webbplatstabellen. Klicka på **Byt namn**.

1. I dialogrutan **Redigera Edge Delivery-webbplats** anger du platsens nya namn i textfältet **Platsnamn**.

1. Klicka på **Redigera**.

## Ta bort en Edge Delivery-webbplats {#delete-edge-delivery-site}

Om du tar bort en Edge Delivery Services-plats tas även alla associerade CDN-konfigurationer bort. Den här åtgärden bryter anslutningen mellan anpassade domäner och platsen. Mer information finns i CDN-konfigurationer. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Så här tar du bort en Edge Delivery-webbplats:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med Edge Delivery Services konfigurerat, där du vill lägga till en Edge Delivery-webbplats.
1. Gör något av följande:

   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars webbplats du vill ta bort i tabellen för Edge Delivery-webbplatsen.
Klicka på ikonen ![Ta bort Edge Delivery-plats](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Ta bort** och klicka sedan på **Ta bort** igen för att bekräfta att webbplatsen har tagits bort.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn. Under rubriken **Tjänster** klickar du på ikonen ![Webbsida för Edge Delivery-webbplatser](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**.
Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars webbplats du vill ta bort i tabellen för Edge Delivery-webbplatsen. Klicka på ikonen ![Ta bort Edge Delivery-plats](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Ta bort** och klicka sedan på **Ta bort** igen för att bekräfta att webbplatsen har tagits bort.

     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery-platser](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Hantera en Edge Delivery-webbplats mellan Helix 4 och Helix 5

Använd API-slutpunkten `/program/{programId}/site/{siteId}` för att migrera en Edge Delivery-webbplats mellan Helix 4 och Helix 5.

CDN-konfigurationer för Helix 4-webbplatser kan inte migreras automatiskt till Helix 5. Begränsningen gäller eftersom kundens produktionsanläggningar fortfarande kan köras på Helix 4 medan deras Helix 5-versioner fortfarande är under utveckling.

**Förutsättningar**

* `sitename` måste redan finnas.
* Lär dig vilka värden som är lämpliga för `branchName`, Helix `version` och `repo`.
* Migreringen ändrar bara `branchName`, Helix `version` och `repo`. Ägarfältet kan inte ändras.

**API-format**

```http
PUT /api/program/{programId}/site/{siteId}
```

**Begär textparametrar**
Skapar en åsidosättning för en Edge Delivery-plats för att framtvinga det ursprung som anges i begärandetexten.

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### Exempel 1: Migrera till Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix5",
  "branchName": "branch",
  "version": "v5",
  "repo": "my-website"
}
```

**Resultat av ursprungs-URL**
Returnerar en Edge Delivery-webbplats med följande ursprungliga URL-adress:

`"origin": "branch--my-website–Teo48.aem.live"`


### Exempel 2: Migrera till Helix 4

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix4",
  "branchName": "branch",
  "version": "v4",
  "repo": "my-website"
}
```

**Resultat av ursprungs-URL**
Returnerar en Edge Delivery-webbplats med följande ursprungliga URL-adress:

`"origin": "branch--my-website--Teo48.hlx.live"`

### Exempel 3: Migrera den trådlösa webbplatsen till Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-reposless-website",
  "branchName": "main",
  "version": "v5",
  "repo": "my-reposless-website"
}
```

**Resultat av ursprungs-URL**
Returnerar en Edge Delivery-webbplats med följande ursprungliga URL-adress:

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## Logga en supportanmälan {#eds-support-ticket}

{{support-ticket}}
