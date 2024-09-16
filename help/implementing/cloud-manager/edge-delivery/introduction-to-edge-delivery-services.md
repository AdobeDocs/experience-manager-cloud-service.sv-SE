---
title: Introduktion till Edge Delivery Services i Cloud Manager
description: Lär dig hur du kan leverera dina Cloud Manager-projekt med hjälp av Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 1%

---

# Introduktion till Edge Delivery Services i Cloud Manager {#edge-delivery-services}

Edge Delivery Services är en sammanslagen uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Med den här funktionen kan du göra följande:

* Skapa snabba sajter med en perfekt Lightroom-bakgrundsmusik.
* Kontinuerlig övervakning av prestanda via RUM (Real Use Monitoring).
* Öka redigeringseffektiviteten genom att frikoppla innehållskällor.

Du kan använda både AEM och WYSIWYG-redigering med Universal Editor och dokumentbaserad redigering.

Med Cloud Manager i AEM as a Cloud Service kan du aktivera Edge Delivery Service för ditt projekt.

>[!TIP]
>
>Mer information om Edge Delivery Services och hur de kan användas med AEM finns i [Översikt över Edge Delivery Services](/help/edge/overview.md).

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->


## Om Edge Delivery Services i Cloud Manager {#edge-in-cloud-manager}

Om du har licensierat Edge Delivery Services som en del av Adobe Experience Manager Sites kan du publicera din webbplats med Edge Delivery Services direkt i Cloud Manager och gå live [med hjälp av en guidad självbetjäningsupplevelse](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Dessutom får ni tillgång till en enhetlig upplevelse för att hantera alla era AEM samtidigt som ni säkerställer enhetlighet i alla viktiga arbetsflöden. Dessa omfattar domännamnshantering, SSL-certifikathantering och CDN-mappningar.

## Lägga till Edge Delivery Services i ett produktionsprogram eller sandlådeprogram

Om du vill lägga till eller redigera program måste du vara medlem i rollen **Affärsägare** eller ha behörighet att göra det.

Organisationen måste ha en licens för oanvända Edge Delivery Services innan den kan tillämpas på ett produktionsprogram.

>[!NOTE]
>
>När licensavtalet för Edge Delivery Services har tillämpats på eller tagits bort från ett program börjar ändringen gälla omedelbart utan att någon pipeline behöver köras. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

Gör något av följande beroende på hur du använder dem:

| Använd skiftläge | Beskrivning |
| --- | --- |
| Jag vill lägga till Edge Delivery Services i ett nytt produktionsprogram. | Se [Skapa produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>Välj **Edge Delivery Services** på fliken **Lösningar och tillägg** i guiden. |
| Jag vill lägga till Edge Delivery Services i ett befintligt produktionsprogram. | Se [Redigera program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Välj **Edge Delivery Services** i dialogrutan **Redigera program** på fliken **Lösningar och tillägg**. |
| Jag vill lägga till en Edge Delivery-webbplats i Cloud Manager | Se [Lägg till en Edge Delivery-webbplats](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Jag vill lägga till Edge Delivery Services i ett nytt eller befintligt sandlådeprogram. | Se [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>När du skapar ett sandlådeprogram läggs Edge Delivery Services till i programmet som standard. Du behöver inte markera det.<br>Befintliga sandlådeprogram innan Edge Delivery är allmänt tillgängligt ärver Edge Delivery Services automatiskt. |

## Adobe rekommenderade väg för avtalade kunder {#recommended-path-eds}

Som avtalskund kan du se till att du får ut mesta möjliga av Adobe genom att få tillgång till och använda din Edge Delivery Services-licens via Cloud Manager. Med den här metoden kan du använda [hanterat CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) i Adobe och dra nytta av viktiga fördelar som CDN-hantering för självbetjäning, inklusive konfiguration och tillägg av DV-certifikat. När ett DV-certifikat har skapats förnyas det dessutom automatiskt var tredje månad i Adobe, om det inte tas bort. Om ni inte har någon Edge Delivery Services licens hos Adobe och bestämmer er för att kringgå dessa förmåner, kan ni bara använda ett kundhanterat CDN. Den här konfigurationen måste finnas på plattformen `aem.live`.

Om du har avtal med licenser för AEM as a Cloud Service Sites Edge Delivery Services loggar du in på Cloud Manager för att kontrollera att du kan göra följande:

* Förbruka licensen i det program du valt.
* Utnyttja fördelarna med [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) för att utföra CRUD-åtgärder (Skapa, Läs, Uppdatera, Ta bort).
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* Åtkomst till SLA-rapportering (*kommer snart*) <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* Få stöd från Adobe. Se till att era Edge Delivery Services är registrerade genom ett produktionsprogram i Cloud Manager för korrekt igenkänning och support från Adobe.


## Om att göra-listan för Edge Delivery {#ed-todo-list}

**Edge Delivery att göra-listan** är en kontrollista för introduktionsaktiviteter som är avsedd att vägleda dig genom introduktionen och hantera din Edge Delivery webbplats hela vägen till [Go-Live](/help/journey-onboarding/go-live-checklist.md).

![Edge Delivery-lista med att göra-uppgifter för webbplats](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|  | Uppgift | Beskrivning |
| --- | --- | --- |
| 1 | Gå med i produktsamarbetskanalen | Om du klickar på **Skicka begäran nu** skickas en begäran till Adobe om att skapa en kanal för ditt företag. Om kanalen redan finns vidarebefordras du till företagets kanal. |
| 2 | Kompletta krav | Om du klickar på **Visa självstudiekursen Komma igång** dirigeras du till självstudiekursen [Komma igång - Utvecklare](https://www.aem.live/developer/tutorial). |
| 3 | Lägg till Edge Delivery-webbplats | Se [Lägg till en Edge Delivery-webbplats](#eds-add-site). |
| 4 | Lägg till domän | Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Lägg till SSL-certifikat | Se [Lägg till SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Konfigurera CDN för din Edge Delivery-webbplats | Se [Lägg till en CDN-konfiguration](#add-cdn). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
