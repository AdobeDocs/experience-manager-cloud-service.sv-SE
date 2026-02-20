---
title: Konfigurera en Edge Delivery-webbplats att använda en extern Git-databas
description: Lär dig hur du länkar en Edge Delivery-webbplats till en privat eller företags Git-databas.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: 2ea076c42a6406548bf48cd246227fc8ddb3a080
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Konfigurera en Edge Delivery-webbplats att använda en extern Git-databas

Du kan konfigurera din Edge Delivery-webbplats så att koden hämtas från alla privata Git-databaser som redan är inbyggda i Cloud Manager.

<!--
**Supported Git Vendors**

| Support level | Vendors | Notes |
| --- | --- | --- |
| General availability | &bull; GitHub Enterprise (self-hosted version)<br>&bull; Bitbucket (Cloud version)<br>&bull; GitLab (Cloud and self-hosted version) | Connect without enablement requests |
| Alpha program | Azure DevOps (Cloud version) | [Request access](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta program | Adobe-hosted repository (created in Cloud Manager) | [Request access](mailto:grp-cloudmanager_byog@adobe.com) |
-->

**Så här konfigurerar du en Edge Delivery-webbplats att använda en extern Git-databas:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med Edge Delivery Services konfigurerat, där du vill konfigurera en Edge Delivery-webbplats så att den använder ett externt Git-svar.
1. Klicka på ikonen **Översikt** Översikt **![i den vänstra listen under rubriken &#x200B;](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg)Program**.
1. Klicka på fliken **Edge Delivery** på sidan **Programöversikt**.
1. Klicka på ikonen **Mer** i slutet av en rad vars webbplats du vill konfigurera för att använda ett externt svar i tabellen ![Edge Delivery-webbplatser](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och klicka sedan på **Hämta ett eget Git**.
1. I dialogrutan Hämta din egen Git väljer du en Git-repo med statusen **i listrutan** Databasnamn`READY` och klickar sedan på **Bekräfta**.

   Cloud Manager returnerar en engångshemlig token. Om du konfigurerar om webbplatsen genererar Cloud Manager en ny hemlig token.

1. Kopiera token och lägg till den i platskonfigurationen i **helix-admin**, enligt beskrivningen i [BYO Git-guiden](https://www.aem.live/developer/byo-git).
1. Gå tillbaka till Cloud Manager och klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars webbplats du just konfigurerade att använda ett externt svar. Klicka sedan på **Synkronisera kod**.
1. Välj grenen som ska synkroniseras och klicka på **Synkronisera**.

Varje implementering på en gren utlöser nu en automatisk synkronisering. Använd **Synkronisera kod** igen när en fullständig manuell synkronisering krävs.
