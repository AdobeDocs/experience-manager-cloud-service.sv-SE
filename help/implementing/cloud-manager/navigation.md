---
title: Navigera i användargränssnittet i Cloud Manager
description: Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4b09357276be8b57c72f830a39d98ab0a593efb1
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---


# Navigera i användargränssnittet i Cloud Manager {#navigation}

Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.


Användargränssnittet för molnhantering består huvudsakligen av två grafiska gränssnitt:

* [På konsolen Mina program](#my-programs-console) kan du visa och hantera alla program.
* [I fönstret Programöversikt](#program-overview) kan du se information om och hantera ett enskilt program.

>[!TIP]
>
>Se även [introduktionsdokumentationsresan](/help/journey-onboarding/overview.md) för en fullständig översikt över hur du kommer igång med AEM as a Cloud Service med Cloud Manager.


## AI Assistant i AEM

För kunder som har [uppfyllt villkoren](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access) är AI Assistant i AEM tillgängligt för användare i organisationen. Se [AI-assistenten i AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).


## My Programs Console {#my-programs-console}

När du loggar in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och väljer lämplig organisation, kommer du till konsolen **Mina program**.

![Konsolen Mina program](assets/my-programs-console.png)

Konsolen Mina program ger en översikt över alla program som du har tillgång till i den valda organisationen. Den består av flera delar.

1. [Verktygsfält](#toolbars-my-programs-toolbars) för organisationsval, aviseringar och kontoinställningar
1. Flikar som gör att du kan växla den aktuella vyn av dina program.
   * Vyn **Hem** (standard) som väljer vyn **Mina program** med en översikt över alla program
   * **Licens** som har åtkomst till [licensinstrumentpanelen](/help/implementing/cloud-manager/license-dashboard.md).
   * Observera att flikarna som standard stängs och att de kan visas med ![Visa menyikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i [Cloud Manager-rubriken](#cloud-manager-header).
1. [Statistik och call-to-action](#statistics) för en översikt över din senaste aktivitet
1. [**Mina program** avsnitt](#my-programs-section) med en översikt över alla dina program
1. [Snabblänkar](#quick-links-section) gör det enkelt att komma åt relaterade resurser.

>[!TIP]
>
>Mer information om program finns i [Program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

### Verktygsfält {#my-programs-toolbars}

Det finns två verktygsfält ovanpå varandra.

#### Experience Platform övre navigeringsfält {#cloud-manager-header}

Det första är det övre navigeringsfältet i Experience Platform, som är beständigt när du navigerar i Cloud Manager. Det är en ankarpunkt som ger dig tillgång till inställningar och information som gäller för alla Cloud Manager-program.

![Experience Platform övre navigeringsfält](assets/experience-cloud-header.png)

* Med ![Visa menyikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) (visa eller dölj sidomenyn) får du tillgång till en mängd olika flikar som kan ta dig till specifika delar av ett enskilt program. Eller så kan du växla mellan [licensöversikten](/help/implementing/cloud-manager/license-dashboard.md) och konsolen **[Mina program](#my-programs-console)** beroende på sammanhanget.
* Med ikonen ![Bell](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) ([Notifications](/help/implementing/cloud-manager/notifications.md)) får du bland annat tillgång till meddelanden och meddelanden.

Mer information om Experience Platform övre navigeringsfält finns i [Adobe Experience Platform användargränssnittshandbok.](https://experienceleague.adobe.com/sv/docs/experience-platform/landing/platform-ui/ui-guide#top-navigation-bar)

#### Verktygsfältet Program {#program-toolbar}

Verktygsfältet Program innehåller länkar för att växla mellan Cloud Manager-program och åtgärder som passar just det sammanhanget.

![Verktygsfältet Program](assets/program-toolbar.png)

1. Väljaren **Mina program** öppnar en listruta där du snabbt kan välja andra program eller vidta lämpliga åtgärder, t.ex. skapa ett nytt program
1. Länken **Komma igång** ger dig tillgång till dokumentationsresan [för introduktion](/help/journey-onboarding/overview.md) så att du kan komma igång med Cloud Manager.
1. Åtgärdsknappen innehåller sammanhangsberoende åtgärder som att lägga till ett program.

### Statistik och uppmaning {#statistics}

Statistik och call-to-action-avsnitt innehåller sammanställda data för din organisation, t.ex. om du har konfigurerat dina program, kan statistik över dina aktiviteter under de senaste 90 dagarna visa, inklusive:

* Antal [distributioner](/help/implementing/cloud-manager/deploy-code.md)
* Antal [kodkvalitetsproblem](/help/implementing/cloud-manager/code-quality-testing.md) som identifierats
* Antal byggen

Eller om du just har börjat konfigurera organisationen kan det finnas tips om nästa steg eller dokumentationsresurser.

### Avsnittet Mina program {#my-programs-section}

Huvudinnehållet i konsolen **Mina program** är listan med program i avsnittet **Mina program**.

I avsnittet **Mina program** visas kort för varje program. Klicka på ett kort för att komma åt sidan **Programöversikt** för mer information om programmet.

>[!NOTE]
>
>Beroende på vilka behörigheter du har kanske du inte kan välja vissa program.


Använd sorteringsalternativen för att enklare hitta det program du behöver.

![Sorteringsalternativ](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Sortera efter:
   * **Skapad** (standard)
   * **Programnamn**
   * **Status**
* ![Ikon för sorteringsordning nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderDown_18_N.svg) Stigande (standard) / ![Ikon för sorteringsordning uppåt &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderUp_18_N.svg) Fallande
* ![Ikon för klassisk stödrastervy](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ClassicGridView_18_N.svg) Stödrastervisning (standard)
* ![Ikon för visningslista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)

#### Programkort {#program-cards}

Ett kort (eller en rad i en tabell) representerar alla program och ger en översikt över programmet och snabblänkar för att vidta åtgärder.

![Programkort](assets/program-card.png)

* Bild som är associerad med programmet, om den är konfigurerad. Bilden ovan är&quot;WKND&quot;.
* Namn som tilldelats programmet. I bilden ovan visas&quot;SecurBank Sample&quot; som programnamn.
* Tjänsttyp:
   * **Experience Manager Cloud** - för AEM as a Cloud Service-program
   * **Experience Manager** - för [AMS-program (Adobe Managed Services)](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-manager/content/introduction)
* [Programtyp](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md):
   * Sandbox
   * Produktion
* Status. I bilden ovan är statusen Klar med en bock.
* Konfigurerade lösningar. I bilden ovan är Sites och Assets konfigurerade lösningar.
* Skapad den.

Ett produktionsprogram kan märkas om du vill visa ytterligare funktioner som du valde när du lade till det, till exempel följande:

* ![HIPAA-märke](assets/hipaa.png) [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* ![WAF-DDOS-märke](assets/waf-ddos-protection.png) [WAF-DDOS-skydd](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* [99,99 % SLA (Service level agreement)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

Informationsikonen ger dig även snabb åtkomst till ytterligare information om programmet (användbart i listvyn).

![Information](assets/information-list-view.png)

Ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_22/Smock_More_22_N.svg) ger dig tillgång till ytterligare åtgärder som du kan vidta i programmet.

![Ellipsknappen för program](assets/program-ellipsis.png)

* Navigera till en viss ![dataikon](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Data_22_N.svg) [Miljö](/help/implementing/cloud-manager/manage-environments.md) i programmet
* Öppna ikonen ![Programöversikt](/help/implementing/cloud-manager/assets/program-overview.svg) [Programöversikt](#program-overview)
* ![Ikonen Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) [Redigera programmet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* ![Ta bort ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) [Ta bort ett sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>Mer information om program samt hur du lägger till och hanterar program finns i:
>
>* [Program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [Skapa produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
>* [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)


### Snabblänkar {#quick-links-section}

I avsnittet med snabblänkar får du tillgång till resurser som du använder ofta och som är relaterade till dem.

## Översikt över programmet {#program-overview}

När ett program har valts i konsolen **[Mina program](#my-programs-console)** dirigeras du till sidan **Programöversikt** .

![Programöversikt](assets/program-overview.png)

Programöversikten ger dig tillgång till alla detaljer i ett Cloud Manager-program. Precis som konsolen **Mina program** består den av flera delar.

1. [Verktygsfält](#program-overview-toolbar) om du snabbt vill gå tillbaka till konsolen Mina program och navigera i programmet
1. [Tabbar](#program-tabs) för att växla mellan olika aspekter av programmet
1. En [call-to-action](#cta) baserad på de senaste åtgärderna i programmet
1. En [översikt över programmets miljöer](#environments)
1. En [översikt över programmets pipelines](#pipelines)
1. En [översikt över programmets prestanda](#performance)
1. Länkar till [användbara resurser](#useful-resources)

### Verktygsfält {#program-overview-toolbar}

Verktygsfälten för programöversikten liknar verktygsfälten i [Min programkonsol](#my-programs-toolbars). Här illustreras bara skillnaderna.

#### Cloud Manager header {#cloud-manager-header-2}

I sidans övre vänstra hörn finns rubriken Adobe Cloud Manager. Du kan klicka på ![Side menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) om du vill visa eller dölja sidomenyn med flikar till andra områden i programmet.

![Cloud Manager sidmeny](assets/cloud-manager-hamburger.png)

Klicka på Adobe Cloud Manager för att återgå till hemmet.

#### Verktygsfältet Program {#program-toolbar-2}

Verktygsfältet för program ger dig fortfarande möjlighet att snabbt växla till andra program, men ger dessutom tillgång till sammanhangsberoende åtgärder som att lägga till och redigera programmet.

![Verktygsfältet Program](assets/cloud-manager-program-toolbar.png)

Verktygsfältet visar alltid den flik som du för tillfället är på, även om du har dolt flikarna med ![Visa menyikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg).

### Programflikar {#program-tabs}

Varje program har flera alternativ och data kopplade till sig. Dessa alternativ och data samlas in på flikar för att göra det enklare att navigera i programmet. Flikarna ger dig tillgång till:

**Program**

* ![Ikon för modern stödrastervy](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ModernGridView_18_N.svg) Översikt - Programöversikt enligt beskrivningen i det aktuella dokumentet
* ![Bell-ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) [Aktivitet](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) - Historiken för programmets pipeline-körningar
* ![Ikon för arbetsflöde](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) [Pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) - Alla pipelines har konfigurerats för programmet
* ![Mappikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) [Databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - Alla databaser har konfigurerats för programmet
* ![Diagramcirkelsymbol](https://spectrum.adobe.com/static/icons/workflow_18/Smock_GraphPie_18_N.svg) [Rapporter](/help/implementing/cloud-manager/reports/report-sla.md) - Mätvärden som SLA-data

**Tjänster**

* ![Dataikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) [Miljö](/help/implementing/cloud-manager/manage-environments.md) - Alla miljöer som konfigurerats för programmet
* ![Ikon för webbsidor](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) [Edge Delivery Sites](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) - Hantera Edge Delivery webbplatser
* ![Ikon för inställningar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) [Domäninställningar](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - Hantera anpassade domännamn för programmet
* ![Lås stängd ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) - Hantera SSL-certifikat för programmet
* ![Ikon för sociala nätverk](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) [Domänmappningar](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - Hantera domänmappningar
* ![Ikon för uppgiftslista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) [`IP Allow Lists`](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) - Definiera tillåtelselista för vissa IP-adresser
* ![Ruteikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) [Innehållsuppsättningar](/help/implementing/developing/tools/content-copy.md) - Innehållsuppsättningar som skapats i kopieringssyfte
* ![Ikonen Historik](https://spectrum.adobe.com/static/icons/workflow_18/Smock_History_18_N.svg) [Kopiera innehållsaktivitet](/help/implementing/developing/tools/content-copy.md) - aktiviteter för innehållskopiering
* ![Kanalikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Channel_18_N.svg) [Nätverksinfrastrukturer](/help/security/configuring-advanced-networking.md) - Hantera avancerade nätverksalternativ för programmet

**Resurser**

* ![Book icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Book_18_N.svg) Learning Paths - Additional learning resources about Cloud Manager

Som standard visas fliken **Översikt** när du öppnar ett program. Den aktuella fliken markeras. Välj en annan flik om du vill visa information om den.

Klicka på [Visa menyikon](#cloud-manager-header-2) i det övre vänstra hörnet av ![Cloud Manager-sidhuvudet](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) om du vill visa eller dölja sidomenyn med flikar.

### Call-to-action {#cta}

I call-to-action-avsnittet finns information som du kan använda beroende på programmets status. För ett nytt program kan du se nästa steg och en påminnelse om ett publiceringsdatum, [angivet när programmet skapades](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).

![Call-to-action för ett nytt program](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

För ett live-program, status för den senaste distributionen med länkar för information och start av en ny distribution.

![Call-to-action](/help/implementing/cloud-manager/assets/info-banner.png)

### Miljökort {#environments}

Kortet **Environment** ger dig en översikt över dina miljöer och länkar för snabba åtgärder.

Kortet **Environment** innehåller endast tre miljöer. Klicka på ikonen ![Arbetsflöde](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Visa alla** om du vill visa alla miljöer i programmet.

Se även [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md).

### Förloppskort {#pipelines}

Kortet **Pipelines** ger dig en översikt över dina pipelines och länkar för snabba åtgärder.

Kortet **Pipelines** innehåller endast tre pipelines. Klicka på ikonen ![Arbetsflöde](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Visa alla** om du vill visa alla rörledningar för programmet.

Se även [Hantera pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) för mer information om hur du hanterar dina pipelines.

### Prestandakort {#performance}

Kortet **Performance** ger en översikt över **[CDN-instrumentpanelen](/help/implementing/cloud-manager/cdn-performance.md)**.

![Prestandakort](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### Användbara resurser {#useful-resources}

Avsnittet **Användbara resurser** innehåller länkar till ytterligare utbildningsresurser för Cloud Manager.
