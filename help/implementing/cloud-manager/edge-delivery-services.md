---
title: Stöd för Edge Delivery Services i Cloud Manager
description: Lär dig hur du kan leverera dina Cloud Manager-projekt med hjälp av Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bc9aa376a402a55191e153f662262ff65df32f5e
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---

# Stöd för Edge Delivery Services i Cloud Manager {#edge-delivery-services}

Lär dig hur du använder din Edge Delivery Services-licens för att skapa en Edge Delivery Services-webbplats.

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->

## Edge Delivery Services i korthet {#edge-overview}

Edge Delivery Services är en sammanslagen uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Med den här funktionen kan du göra följande:

* Skapa snabba sajter med en perfekt Lightroom-bakgrundsmusik.
* Kontinuerlig övervakning av prestanda via RUM (Real Use Monitoring).
* Öka redigeringseffektiviteten genom att frikoppla innehållskällor.

Du kan använda både AEM och WYSIWYG-redigering med Universal Editor och dokumentbaserad redigering.

Med Cloud Manager i AEM as a Cloud Service kan du aktivera Edge Delivery Service för ditt projekt.

>[!TIP]
>
>Mer information om Edge Delivery Services och hur de kan användas med AEM finns i dokumentets översikt [Edge Delivery Services](/help/edge/overview.md).

## EDGE DELIVERY SERVICES i CLOUD MANAGER {#edge-in-cloud-manager}

Om du har licensierat Edge Delivery Services som en del av Adobe Experience Manager Sites kan du publicera din webbplats med Edge Delivery Services direkt i Cloud Manager och gå live [med hjälp av en guidad självbetjäningsupplevelse](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Dessutom får ni tillgång till en enhetlig upplevelse för att hantera alla era AEM samtidigt som ni säkerställer enhetlighet i alla viktiga arbetsflöden. Dessa omfattar domännamnshantering, SSL-certifikathantering och CDN-mappningar.

## Lägga till Edge Delivery Services i ett produktions- eller sandlådeprogram

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
| Jag vill lägga till Edge Delivery Services i ett nytt eller befintligt sandlådeprogram. | Se [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>När du skapar ett sandlådeprogram läggs Edge Delivery Services till i programmet som standard. Du behöver inte markera det.<br>Befintliga sandlådeprogram ärver Edge Delivery Services automatiskt. |

## Adobe rekommenderade väg för avtalade kunder {#recommended-path-eds}

Som avtalskund kan du se till att du får ut mesta möjliga av Adobe genom att få tillgång till och använda din Edge Delivery Services-licens via Cloud Manager. Med den här metoden kan du använda [hanterat CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) i Adobe och dra nytta av viktiga fördelar som CDN-hantering för självbetjäning, inklusive konfiguration och tillägg av DV-certifikat. När ett DV-certifikat har skapats förnyas det dessutom automatiskt var tredje månad i Adobe, om det inte tas bort. Om ni inte har någon Edge Delivery Services licens hos Adobe och bestämmer er för att kringgå dessa förmåner, kan ni bara använda ett kundhanterat CDN. Den här konfigurationen måste finnas på plattformen `aem.live`.

Om du har avtal med licenser för AEM as a Cloud Service Sites Edge Delivery Services loggar du in på Cloud Manager för att kontrollera att du kan göra följande:

* Förbruka licensen i det program du valt.
* Utnyttja fördelarna med [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) för att utföra CRUD-åtgärder (Skapa, Läs, Uppdatera, Ta bort).
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* Åtkomst till SLA-rapportering (*kommer snart*) <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* Få stöd från Adobe. Se till att era Edge Delivery Services är registrerade genom ett produktionsprogram i Cloud Manager för korrekt igenkänning och support från Adobe.

## Lägg till en Edge Delivery-webbplats {#eds-add-site}

När du har lagt till Edge Delivery Services i ett produktionsprogram tillämpas din Edge Delivery Services på det.

En klickbar flik med namnet **Edge Delivery** visas på sidan Översikt. När du klickar på fliken visas en tabell med en lista över alla Edge Delivery-webbplatser som du har lagt till. Lägg märke till menyalternativet **Edge Delivery Sites** i den vänstra navigeringspanelen under grupperingen **Tjänster**.

![Översiktssida med Edge Delivery Sites i den vänstra navigeringspanelen och fliken Edge Delivery till höger om fliken Publish Delivery ](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Så här lägger du till en Edge Delivery-webbplats:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med konfigurerade Edge Delivery Services där du vill lägga till en Edge Delivery-webbplats.
1. Gör något av följande:
   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka sedan på **Lägg till Edge Delivery-webbplats** nära sidans nedre högra hörn.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     **Edge Delivery att göra-listan**, som visas i bilden ovan, är en valfri guide till att komma igång med Edge Delivery. Se [Om att göra-listan för Edge Delivery](#ed-todo-list).

   * I det övre vänstra hörnet av sidan klickar du på hamburgikonen för att visa den vänstra navigeringsmenyn. Klicka på **Edge Delivery Sites** under rubriken **Tjänster**. Klicka på **Lägg till plats** i sidans övre högra hörn.

     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery-platser](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Gör följande i dialogrutan **Lägg till Edge Delivery-webbplats**:

   | Textfält | Vad du ska göra |
   | --- | --- |
   | Platsnamn | Ange namnet på den Edge Delivery-webbplats som du lägger till. Namnet fungerar som en unik identifierare för webbplatsen inom Cloud Manager. |
   | Databas-URL | Det här fältet hänvisar till Git-databasen där webbplatsens kod lagras.<br>Ange URL:en för Git-databasen som innehåller de filer och resurser som krävs (till exempel HTML, CSS, JavaScript och andra webbresurser) för din Edge Delivery-webbplats. På så sätt kan Cloud Manager hämta koden från databasen under distributionsprocessen. |
   | Platsbeskrivning (valfritt) | Ange en kort beskrivning av den Edge Delivery-webbplats som du lägger till.<br>Den här beskrivningen hjälper till att identifiera och skilja ut webbplatsen, vilket gör det enklare att hantera och identifiera andra webbplatser som du har lagt till. Du kanske vill inkludera information om webbplatsens syfte, innehåll eller annan relevant information som kan göra det lättare att klargöra dess funktion eller omfattning. |

1. Klicka på **Lägg till** i dialogrutans nedre högra hörn.

1. Gör något av följande i dialogrutan **Verifiera databasägarskap**:

   | Steg | Beskrivning |
   | --- | --- |
   | 1 | Lägg till en fil med platssökvägen till grenen `main` i Git-databasen som visas i fältet **Databas-URL**. Klicka vid behov på ikonen Kopiera för att kopiera sökvägen till Urklipp.<br> Platssökvägen är:<br>`well-known/adobe/cloudmanager-challenge.txt`.<br><br>Lägg *inte* till en punkt i början av platssökvägen, finns i:<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | Lägg till den genererade koden i filen som du skapade i steg 1. Klicka vid behov på ikonen Kopiera för att kopiera koden till Urklipp. |
   | 3 | I Git-databasen skapar du en pull-begäran och sammanfogar den för att implementera koden. |

1. Klicka på **Verifiera**. När databasen har verifierats ändras dess status i tabellen Edge Deliver Sites till en grön cirkel med en vit bock inuti.

## Om att göra-listan för Edge Delivery {#ed-todo-list}

**Edge Delivery att göra-listan** är en kontrollista för introduktionsaktiviteter som är avsedd att vägleda dig genom introduktionen och hantera din Edge Delivery webbplats hela vägen till [Go-Live](/help/journey-onboarding/go-live-checklist.md).

|  | Uppgift | Beskrivning |
| --- | --- | --- |
| 1 | Gå med i produktsamarbetskanalen | Om du klickar på **Skicka begäran nu** skickas en begäran till Adobe om att skapa en kanal för ditt företag. Om kanalen redan finns vidarebefordras du till företagets kanal. |
| 2 | Kompletta krav | Om du klickar på **Visa självstudiekursen Komma igång** dirigeras du till självstudiekursen [Komma igång - Utvecklare](https://www.aem.live/developer/tutorial). |
| 3 | Lägg till Edge Delivery-webbplats | Se [Lägg till en Edge Delivery-webbplats](#eds-add-site). |
| 4 | Lägg till domän | Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Lägg till SSL-certifikat | Se [Lägg till SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Konfigurera CDN för din Edge Delivery-webbplats | Se [Lägg till en CDN-konfiguration](#add-cdn). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## Lägga till en CDN-konfiguration på din Edge Delivery-webbplats {#add-cdn}

Se [Lägg till en CDN-konfiguration](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Ta bort en Edge Delivery-webbplats {#eds-site-delete}

>[!IMPORTANT]
>
>Om du tar bort en webbplats för Edge Delivery Services tas även alla associerade CDN-konfigurationer bort. Den här åtgärden bryter anslutningen mellan anpassade domäner och platsen. Mer information finns i CDN-konfigurationer. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Så här tar du bort en Edge Delivery-webbplats:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med konfigurerade Edge Delivery Services där du vill lägga till en Edge Delivery-webbplats.
1. Gör något av följande:
   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka på ellipsen i slutet av en rad vars webbplats du vill ta bort i tabellen för Edge Delivery-webbplatsen. Klicka på **Ta bort** och sedan på **Ta bort** igen för att bekräfta att webbplatsen har tagits bort.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * I det övre vänstra hörnet av sidan klickar du på hamburgikonen för att visa den vänstra navigeringsmenyn. Klicka på **Edge Delivery Sites** under rubriken **Tjänster**. Klicka på ellipsen i slutet av en rad vars webbplats du vill ta bort i tabellen för Edge Delivery-webbplatsen. Klicka på **Ta bort** och sedan på **Ta bort** igen för att bekräfta att webbplatsen har tagits bort.


     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery-platser](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)


<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
