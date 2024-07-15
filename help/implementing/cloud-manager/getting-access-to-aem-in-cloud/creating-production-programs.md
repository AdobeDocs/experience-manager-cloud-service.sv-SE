---
title: Skapa produktionsprogram
description: Lär dig hur du använder Cloud Manager för att skapa ett eget produktionsprogram för livstrafik.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---


# Skapa produktionsprogram {#create-production-program}

Ett produktionsprogram är avsett för en användare som är bekant med AEM och Cloud Manager och som är redo att börja skriva, bygga och testa kod i syfte att driftsätta den för livstrafik.

Läs mer om programtyper i dokumentet [Om program- och programtyper.](program-types.md)

## Skapa ett produktionsprogram {#create}

Följ de här stegen för att skapa ett produktionsprogram. Observera att beroende på organisationens rättigheter kan du se [ytterligare alternativ](#options) när du lägger till ditt program.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** trycker eller klickar du på **Lägg till program** i skärmens övre högra hörn.

   ![Startsida för molnhanteraren](assets/log-in.png)

1. Välj **Konfigurera för produktion** i guiden Skapa program för att skapa ett produktionsprogram och ange ett programnamn.

   ![Skapar programguiden](assets/create-production-program.png)

1. Du kan också lägga till en bild i programmet genom att dra och släppa en bildfil till målet **Lägg till en programbild** eller genom att klicka på den och välja en bild i en filläsare. Välj **Fortsätt**.

1. På fliken **Lösningar och tillägg** väljer du de lösningar som ska ingå i programmet.

   * Om du är osäker på om du behöver ett eller flera program för de olika lösningar du har tillgängliga väljer du det som intresserar dig mest. Du kan aktivera ytterligare lösningar genom att [redigera programmet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) senare. Se dokumentet [Introduktion till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) för fler rekommendationer för programkonfiguration.
   * Minst en lösning krävs för att skapa ett program.
   * Om du valde alternativet **[Aktivera förbättrat skydd](#security)** får du bara välja så många lösningar som det finns tillgängliga HIPAA-berättiganden för.

   ![Välj lösningar](assets/setup-prod-select.png)

1. Klicka på nedtryckningen före lösningsnamnen för att visa valfria tillägg, som att välja tilläggsprogrammet **Commerce** under **Webbplatser**.

   ![Välj tillägg](assets/setup-prod-commerce.png)

1. Välj lösningar och tillägg och klicka på **Fortsätt**.

1. På fliken **Go-Live Date** anger du det datum då du planerar att publicera ditt produktionsprogram.

   ![Definiera planerat publiceringsdatum](assets/set-up-go-live.png)

   * Det här datumet kan redigeras när som helst.
   * Det här datumet är endast avsett som information och aktiverar Go Live-widgeten på [**sidan Programöversikt**](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) för att tillhandahålla länkar till AEM as a Cloud Service dokumentation om bästa praxis i god tid för att passa in din resa och skapa en lyckad och smidig Go Live-upplevelse.

1. Klicka på **Skapa**.

Ditt program skapas av Cloud Manager och visas och kan markeras på landningssidan.

![Översikt över molnhanteraren](assets/navigate-cm.png)

## Fler alternativ för produktionsprogram {#options}

Beroende på vilka berättiganden som är tillgängliga för din organisation kan du ha ytterligare alternativ tillgängliga när du skapar ett produktionsprogram.

### Dokumentskydd {#security}

Om du har de nödvändiga rättigheterna visas fliken **Säkerhet** som den första fliken i dialogrutan **Konfigurera för produktion** .

Fliken **Säkerhet** innehåller alternativ för att aktivera **HIPAA** och/eller **WAF-DDOS-skydd** för ditt produktionsprogram.

Adobe HIPAA-kompatibel och Web Application Firewall (WAF) underlättar molnbaserad säkerhet som en del av ett flerskiktat tillvägagångssätt för att skydda mot sårbarheter.

* **HIPAA** - Med det här alternativet aktiveras en Adobe HIPPA-klar lösningsimplementering.
   * [Läs mer](https://www.adobe.com/go/hipaa-ready) om implementering av Adobe HIPAA-klar lösning.
   * HIPAA kan inte aktiveras eller inaktiveras efter att programmet har skapats.
* **WAF-DDOS-skydd** - Det här alternativet aktiverar webbprogrammets brandvägg via regler för att skydda ditt program.
   * När den har aktiverats kan WAF-DDOS-skyddet sedan konfigureras genom att en [icke-produktionspipeline skapas.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * Se dokumentet [Trafikfilterregler inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md) för att lära dig hur du hanterar trafikfilterregler i din databas så att de distribueras korrekt.

![Säkerhetsalternativ](assets/create-production-program-security.png)

### SLA {#sla}

Om du har de nödvändiga rättigheterna visas fliken **SLA** som den andra eller tredje fliken i dialogrutan **Konfigurera för produktion** .

AEM Sites erbjuder 99,9 % standardavtal för servicenivå (SLA). Alternativet **99,99 % servicenivåavtal** ger en procentandel på minst 99,99 % aktiv tid för produktionsmiljöerna.

99,99 % SLA ger fördelar, inklusive högre tillgänglighet och lägre latens, och kräver att ytterligare [en publiceringsregion](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) används i produktionsmiljön i programmet.

![SLA-alternativ](assets/create-production-program-sla.png)

När [kraven](#sla-requirements) för aktivering av 99,99 % SLA är uppfyllda måste du köra en [fullständig stackpipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för att kunna aktivera den.

#### Krav för 99,99 % SLA {#sla-requirements}

Utöver de obligatoriska rättigheterna har 99,99 % SLA ytterligare krav för användning.

* Både 99,99 % SLA och ytterligare rättigheter för publiceringsregioner måste vara tillgängliga för organisationen när 99,99 % SLA tillämpas på programmet.
* Om du vill tillämpa 99,99 % SLA på programmet kontrollerar Cloud Manager att ett oförbrukat [ytterligare tillstånd för publiceringsregionen](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) också är tillgängligt och kan tillämpas på programmet.
* När du redigerar ett program och det redan innehåller en produktionsmiljö med minst en extra publiceringsregion, kontrollerar Cloud Manager endast om det finns ett 99,99 % SLA-berättigande.
* För att 99,99 % SLA och rapportering ska kunna aktiveras måste [produktions-/scenmiljön](/help/implementing/cloud-manager/manage-environments.md#adding-environments) ha skapats och minst en ytterligare publiceringsregion måste ha tillämpats på produktions-/scenmiljön.
   * Om du använder [avancerat nätverk](/help/security/configuring-advanced-networking.md) bör du kontrollera att dokumentet [Lägga till flera Publish-regioner i en ny miljö](/help/implementing/cloud-manager/manage-environments.md#adding-regions) innehåller rekommendationer så att anslutningen upprätthålls i händelse av ett regionalt fel.
* Minst en extra publiceringsregion måste finnas kvar i ditt 99,99 % SLA-program. Användare får inte ta bort den sista ytterligare publiceringsregionen från ditt 99,99 % SLA-program.
* 99,99 % SLA stöds för produktionsprogram där Sites-lösningen är aktiverad.
* Du måste köra en [fullständig stackpipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för att kunna aktivera (eller, när du redigerar ett program, inaktivera) SLA-filen på 99,99 %.

## Använd ditt program {#accessing}

1. När du ser ditt programkort på landningssidan väljer du ellipsknappen för att visa de menyalternativ som är tillgängliga för dig.

   ![Programöversikt](assets/program-overview.png)

1. Välj **Programöversikt** om du vill gå till sidan **Översikt** för Cloud Manager.

1. Huvudkortet på översiktssidan hjälper dig att skapa en miljö, en produktionsprocess och slutligen en produktionsprocess.

   ![Programöversikt](assets/set-up-prod5.png)

>[!TIP]
>
>Dokumentet [Navigera i Cloud Manager-gränssnittet](/help/implementing/cloud-manager/navigation.md) innehåller information om hur du navigerar i Cloud Manager och förstår **Mina program**-konsolen.

>[!NOTE]
>
>Till skillnad från ett [sandlådeprogram](introduction-sandbox-programs.md#auto-creation) kräver ett produktionsprogram att användaren har rätt Cloud Manager-roll för att skapa projektet och lägga till en miljö via självbetjäningsgränssnittet.
