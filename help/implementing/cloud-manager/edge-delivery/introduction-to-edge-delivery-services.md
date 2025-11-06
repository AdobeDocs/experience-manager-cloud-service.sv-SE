---
title: Introduktion till Edge Delivery Services i Cloud Manager
description: Lär dig hur du kan leverera dina Cloud Manager-projekt med Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 1%

---


# Introduktion till Edge Delivery Services i Cloud Manager {#edge-delivery-services}

Edge Delivery Services är en sammansättningsbar uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Med den här funktionen kan du göra följande:

* Skapa snabba sajter med en perfekt Lightroom-bakgrundsmusik.
* Kontinuerlig övervakning av prestanda via drifttelemetri.
* Öka redigeringseffektiviteten genom att frikoppla innehållskällor.

Du kan använda både AEM innehållshantering och WYSIWYG-redigering med den universella redigeraren och dokumentbaserad redigering.

Med Cloud Manager i AEM as a Cloud Service kan du aktivera Edge Delivery Service för ditt projekt.

>[!TIP]
>
>Mer information om Edge Delivery Services och hur det kan användas med AEM finns i [Edge Delivery Services-översikten](/help/edge/overview.md).

## Om Edge Delivery Services i Cloud Manager {#edge-in-cloud-manager}

Om du har licensierat Edge Delivery Services som en del av Adobe Experience Manager Sites kan du publicera din webbplats med Edge Delivery Services direkt i Cloud Manager och gå live [med hjälp av en guidad självbetjäningsupplevelse](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

Dessutom får ni tillgång till en enhetlig upplevelse för att hantera alla era AEM-egenskaper samtidigt som ni säkerställer enhetlighet i alla viktiga arbetsflöden. Dessa arbetsflöden omfattar domännamnshantering, SSL-certifikathantering och CDN-mappningar.

## Fördelar med att använda Adobe rekommenderade väg för Edge Delivery Services {#recommended-path-eds}

Maximera fördelarna med Adobe genom att skaffa och använda din Edge Delivery Services-licens via Cloud Manager. På så sätt kan du dra nytta av flera viktiga fördelar.

* [Förbruka din licens för ditt valda program](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [uppdatera andra program](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) eller båda.
* Utnyttja fördelarna med [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) för att utföra CRUD-åtgärder (Skapa, Läs, Uppdatera, Ta bort).
* [Öppna SLA-rapporter](/help/implementing/cloud-manager/reports/report-sla.md)
* [Få tillgång till Adobe support](/help/edge/overview.md#support-ticket) för dina registrerade produktionsprogram.

Om du har en Edge Delivery Services-licens (EDS) kan du använda ett [Adobe-hanterat CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) för din Edge Delivery-webbplats. Om du gör det aktiveras självbetjäning för CDN-hantering och DV-certifikat som förnyas automatiskt var tredje månad om du inte tar bort certifikatet.

Om du väljer att använda ditt CDN (dvs. ett icke-Adobe-hanterat CDN), oavsett din Edge Delivery Services-licens, måste du konfigurera det på `aem.live`-plattformen. Se [BYO CDN-konfiguration](https://www.aem.live/docs/byo-cdn-setup).


## Om att lägga till Edge Delivery Services i ett produktionsprogram eller sandlådeprogram

En Edge Delivery Services kan läggas till på flera olika sätt beroende på hur du påbörjade projektet eller när du vill skapa webbplatsen.

| Använd skiftläge | Beskrivning |
| --- | --- |
| Jag vill lägga till Edge Delivery Services i ett nytt produktionsprogram. | Se [Skapa produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>Välj **Edge Delivery Services** på fliken **Lösningar och tillägg** i guiden. |
| Jag vill lägga till Edge Delivery Services i ett befintligt produktionsprogram. | Se [Redigera program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Välj **Edge Delivery Services** i dialogrutan **Redigera program** på fliken **Lösningar och tillägg**. |
| Jag vill lägga till en Edge Delivery-webbplats i Cloud Manager | Se [Lägg till en Edge Delivery-webbplats](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Jag vill skapa en Edge Delivery-webbplats nu | Se [Skapa en Edge Delivery-webbplats snabbt i Cloud Manager med en enkel musklickning](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| Jag vill lägga till Edge Delivery Services i ett nytt eller befintligt sandlådeprogram. | Se [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>När du skapar ett sandlådeprogram läggs Edge Delivery Services till i programmet som standard. Du behöver inte markera det.<br>Befintliga sandlådeprogram innan Edge Delivery är allmänt tillgängligt ärver Edge Delivery Services automatiskt. |

>[!NOTE]
>
>* Om du vill lägga till eller redigera program måste du vara medlem i rollen **Affärsägare** eller ha behörighet att göra det.
>* Din organisation måste ha en oanvänd Edge Delivery Services-licens innan den kan tillämpas på ett produktionsprogram.
>* När Edge Delivery Services-licensen har tillämpats på eller tagits bort från ett program börjar ändringen gälla omedelbart utan att man behöver göra en pipeline.


## Om att göra-listan för Edge Delivery i Cloud Manager {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

**Edge Delivery att göra-listan** i Cloud Manager är en boardinguppgiftschecklista som är avsedd att vägleda dig genom introduktionen och hantera din Edge Delivery-webbplats hela vägen till [Go-Live](/help/journey-onboarding/go-live-checklist.md).

![Edge Delivery-lista med att göra-uppgifter för webbplatser i Cloud Manager.](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | Uppgift | Beskrivning |
| --- | --- | --- |
| 1 | Gå med i produktsamarbetskanalen | Om du klickar på **Skicka begäran nu** skickas en begäran till Adobe om att skapa en kanal för ditt företag. Om kanalen redan finns vidarebefordras du till företagets kanal. |
| 2 | Kompletta krav | Se [Visa självstudien Komma igång](https://www.aem.live/developer/tutorial). |
| 3 | Lägg till Edge Delivery-webbplats ELLER <br>Skapa en webbplats nu | Se [Lägg till en Edge Delivery-webbplats](#eds-add-site).<br>Se [Skapa en Edge Delivery-webbplats i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| 4 | Konfigurera en Edge Delivery-webbplats att använda en extern Git-databas | Se [Konfigurera en Edge Delivery-webbplats så att den använder en extern Git-databas](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md). |
| 5 | Lägg till domän | Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 6 | Lägg till SSL-certifikat | Se [Lägg till SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 7 | Konfigurera CDN för din Edge Delivery-webbplats | Se [Lägg till en domänmappning](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md). |
| 8 | Konfigurera push-validering | Se [Konfigurera push-validering för en Edge Delivery-plats](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md). |
| 9 | GoLive | Se [Go-Live-checklista](https://www.aem.live/docs/go-live-checklist). |

>[!VIDEO](https://video.tv.adobe.com/v/3441565?captions=swe&learn=on)

## Logga en supportanmälan {#eds-support-ticket}

{{support-ticket}}



