---
title: Skapa produktionsprogram
description: Lär dig hur du använder Cloud Manager för att skapa ett eget produktionsprogram för livstrafik.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8ca3546725f2a95d233497a899afe3b4f6036775
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---


# Skapa produktionsprogram {#create-production-program}

Ett produktionsprogram är avsett för användare som är bekanta med Adobe Experience Manager (AEM) och Cloud Manager, som är redo att skriva, bygga och testa kod, med målet att distribuera den för att hantera livatrafik.

Läs mer om programtyper i dokumentet [Om program- och programtyper](program-types.md).

## Skapa ett produktionsprogram {#create}

Beroende på organisationens rättigheter kan ytterligare alternativ för produktionsprogram visas när du lägger till programmet.
Se [Fler alternativ för produktionsprogram](#options).

**Så här skapar du ett produktionsprogram:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på **Lägg till program** i det övre högra hörnet.

   ![Cloud Manager landningssida](assets/log-in.png)

1. I *Programguiden* skriver du det namn du vill använda för programmet i textfältet **Programnamn**.

1. Under **Programmål** väljer du ![Global ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg)**Konfigurera för produktion**.

   ![Skapar programguiden](assets/create-production-program.png)

1. (Valfritt) Gör något av följande i det nedre högra hörnet i dialogrutan för guiden:

   * Dra och släpp en bildfil till ![bildikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg) **Lägg till ett programbildsmål** .
   * Klicka på ![Bildikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg) **Lägg till en programbild** och välj sedan en bild i en filläsare.
   * Klicka på ikonen ![Ta bort](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) för att ta bort en bild som du har lagt till.

1. Klicka på **Fortsätt**.

1. I listrutan **Lösningar och tillägg** väljer du en eller flera lösningar som ska ingå i programmet.

   * Om du är osäker på om du behöver ett eller flera program för de olika lösningar du har tillgängliga väljer du det som intresserar dig mest. Du kan aktivera ytterligare lösningar genom att [redigera programmet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) senare. Se dokumentet [Introduktion till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) för fler rekommendationer för programkonfiguration.
   * Du måste välja minst en lösning för att skapa ett program. Du kan t.ex. välja **Edge Delivery Services** som en helt hanterad CDN-lösning som optimerar digitala upplevelser. Se [Använda Edge Delivery Services för att leverera ditt Cloud Manager-projekt](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)

   ![Välj lösningar](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/add-production-program-with-edge-v2.png)




   <!-- * If you selected the **[Enable Enhanced Security](#security)** option, you can select only as many solutions for which HIPAA entitlements are available. -->



   * Klicka på ikonen ![Sparrstorlek 300](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize300.svg) till vänster om ett lösningens namn för att visa valfria tillägg. <!-- such as the **Commerce** add-on option under **Sites**. -->

   ![Välj tillägg](assets/setup-prod-commerce.png)

1. När du är klar med att välja lösningar och tillägg klickar du på **Fortsätt**.

1. På fliken **Go-Live Date** anger du det datum då du vill att ditt produktionsprogram ska vara live.

   ![Definiera planerat publiceringsdatum](assets/set-up-go-live.png)

   * Du kan redigera det här datumet när som helst.
   * Datumet används som informationssyfte och utlöser widgeten Go Live på sidan [**Programöversikt**](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview). Den här funktionen ger länkar till AEM as a Cloud Service bästa praxis för att ge en smidig Go Live-upplevelse.

1. Klicka på **Skapa**. Cloud Manager skapar programmet och visar det på landningssidan för markering.

   ![Översikt över molnhanteraren](assets/navigate-cm.png)

## Fler alternativ för produktionsprogram {#options}

Beroende på vilka berättiganden som är tillgängliga för din organisation kan du ha tillgång till följande alternativ när du skapar ett produktionsprogram.

### Dokumentskydd {#security}

Om du har de nödvändiga rättigheterna visas fliken **Säkerhet** som den första fliken i dialogrutan **`Set up for production`** .

![Säkerhetsalternativ](assets/create-production-program-security.png)

Fliken **Säkerhet** innehåller alternativ för att aktivera **HIPAA**, **WAF-DDOS-skydd**, eller båda, för ditt produktionsprogram.

Adobe HIPAA-kompatibel och WAF-DDOS (Web Application Firewall - Distributed Denial of Service) underlättar molnbaserad säkerhet som en del av en lösning med flera nivåer för att skydda mot sårbarheter.

* **HIPAA** - Det här alternativet aktiverar Adobe HIPPA-förberedda lösningsimplementering.
   * [Läs mer](https://www.adobe.com/trust/compliance/hipaa-ready.html) om Adobe HIPAA-förberedda implementering av lösningar.
   * HIPAA kan inte aktiveras eller inaktiveras efter att programmet har skapats.
* **WAF-DDOS-skydd** - Med det här alternativet aktiveras Brandväggen för webbaserade program som regler för att skydda ditt program.
   * När detta har aktiverats kan WAF-DDOS-skyddet sedan konfigureras genom att en [icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) konfigureras.
   * Se [Trafikfilterregler inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md) om du vill veta mer om hur du hanterar trafikfilterregler i din databas så att de distribueras på rätt sätt.

### SLA {#sla}

Om du har de nödvändiga rättigheterna visas fliken **SLA** som den andra eller tredje fliken i dialogrutan **`Set up for production`** .

![SLA-alternativ](assets/create-production-program-sla.png)

Webbplatser och Forms erbjuder 99,9 % service level agreement (SLA) som standard. Med alternativet **99,99 % Service level agreement** garanteras en drifttid på minst 99,99 % för produktionsmiljöerna, oavsett om det gäller Sites, Forms, Edge Delivery Services eller alla tre.

99,99 % av SLA erbjuder fördelar, inklusive högre tillgänglighet och lägre latens.

För Sites- och Forms-program kräver 99,99 % SLA att en ytterligare [publiceringsregion](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) används i produktionsmiljön i programmet. När [kraven](#sla-requirements) för aktivering av 99,99 % SLA uppfylls måste du köra en [fullständig stackpipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för att aktivera den.

För Edge Delivery Services finns det *inga* krav förutom att konfigurera SLA-licensen på 99,99 % i programmet.

#### Krav för 99,99 % SLA {#sla-requirements}

Utöver de rättigheter som krävs har SLA 99,99 % för Sites eller Forms följande ytterligare krav:

* Organisationen måste ha 99,99 % SLA och ytterligare rättigheter för publiceringsregioner tillgängliga när 99,99 % SLA tillämpas på programmet.
* Cloud Manager verifierar att ett oanvänt [ytterligare tillstånd för publiceringsregionen](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) är tillgängligt innan 99,99 % SLA har tillämpats på programmet.
* När du redigerar ett program och det redan innehåller en produktionsmiljö med minst en extra publiceringsregion, kontrollerar Cloud Manager endast om det finns ett berättigande för 99,99 % SLA.
* För aktivering av 99,99 % SLA och rapportering måste [produktions-/scenmiljön](/help/implementing/cloud-manager/manage-environments.md#adding-environments) ha skapats och minst en ytterligare publiceringsregion måste ha tillämpats på produktions-/scenmiljön.
   * Om du använder [avancerat nätverk](/help/security/configuring-advanced-networking.md) bör du kontrollera om dokumentet [Lägga till flera publiceringsregioner i en ny miljö](/help/implementing/cloud-manager/manage-environments.md#adding-regions) innehåller rekommendationer så att anslutningen upprätthålls om det uppstår ett regionalt fel.
* Ditt 99,99 % SLA-program måste alltid innehålla minst en extra publiceringsregion. Användare får inte ta bort den sista återstående ytterligare publiceringsområdet från programmet.
* Din SLA på 99,99 % stöds för produktionsprogram där Sites eller Forms är aktiverat.
* Kör en [fullständig stackpipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för att aktivera eller - när du redigerar ett program - inaktivera SLA 99,99 %.

## Få åtkomst till ditt program {#accessing}

1. När du ser ditt programkort på landningssidan klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för att visa de menyalternativ som är tillgängliga för dig.

   ![Programöversikt](assets/program-overview.png)

1. Välj **Programöversikt** om du vill gå till sidan **Översikt** för Cloud Manager.

1. Call-to-action-kortet på översiktssidan vägleder dig genom att skapa en miljö, en produktionsprocess och slutligen en produktionsprocess.

   ![Programöversikt](assets/set-up-prod5.png)

>[!TIP]
>
>Gå till [Navigera i användargränssnittet för Cloud Manager](/help/implementing/cloud-manager/navigation.md) om du vill ha mer information om hur du navigerar i Cloud Manager och förstå konsolen **Mina program**.

>[!NOTE]
>
>Till skillnad från ett [sandlådeprogram](introduction-sandbox-programs.md#auto-creation) kräver ett produktionsprogram att användaren har rätt Cloud Manager-roll för att skapa projektet och lägga till en miljö via självbetjäningsgränssnittet.


