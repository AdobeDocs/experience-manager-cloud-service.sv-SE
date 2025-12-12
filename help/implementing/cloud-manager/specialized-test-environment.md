---
title: Lägg till en anpassad testmiljö
description: Läs om hur specialiserade testmiljöer i Cloud Manager erbjuder ett dedikerat utrymme för att validera funktioner under nära produktionsförhållanden, idealiskt för stresstestning och avancerade kontroller före driftsättning.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 815fb5c3-a171-4531-8727-b79183d85f06
source-git-commit: 837f1d0eb0bd0f8cf8c0e283db823255f4e53ae1
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Lägg till en anpassad testmiljö{#add-special-test-enviro}

<!-- badge: label="Private beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
-->

>[!NOTE]
>
>Specialiserade testmiljöer finns nu att köpa. Kontakta Adobe för att lägga en order.


Den specialiserade testmiljön är en ny typ av Cloud Manager-miljö som du kan skapa. Den är utformad för att stödja avancerade användningsfall som UAT (User Acceptance Testing) och prestandavalidering. Till skillnad från traditionella miljöer för utveckling, snabb utveckling och mellanlagring fungerar specialiserade testmiljöer utanför produktionsflödet. De ger dig större flexibilitet och strikt isolering för att förhindra störningar i produktionsflödena.

En specialiserad testmiljö är byggd för att spegla storleken, skalbarheten och konfigurationerna i en typisk mellanlagringsmiljö. Detta garanterar att tester som utförs i den specialiserade testmiljön kan ge realistiska insikter i hur kod och innehåll fungerar i produktionsliknande förhållanden. Miljön har också stöd för direkt innehållskopiering från produktion eller scenen. Dessutom upprätthålls paritet med utvecklingsmiljöer när det gäller distributionsarbetsflöden, åtkomstkontroller och nätverkskonfigurationer.

## Viktiga funktioner och konfigurationer för en specialiserad testmiljö {#key-features}

| Kategori | Beteende |
| --- | --- |
| Syfte | UAT och prestandatestning. |
| Typ av pipeline | Inte i produktionsflödet. |
| Miljöstorlek | Matchar scenmiljön. |
| Isolering | Helt isolerad från andra miljöer. |
| Kodrörledningar | Samma som utvecklingsmiljön (validering, Skapa, distribuera). |
| Kopiera innehåll | Tillåts från Production, Stage eller Specialized Testing Environment. |
| Återställning av innehåll | Samma som utvecklingsmiljön. |
| Åtkomstloggar | Samma som utvecklingsmiljön. |
| Developer Console | Samma som utvecklingsmiljön. |
| `IP Allow List` | Samma som utvecklingsmiljön. |
| Nätverksbyggande | Samma som utvecklingsmiljön (tjänster, domännamn, SSL-certifikat, avancerat nätverk). |

Se även [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md).

## Lägg till en anpassad testmiljö {#add-specialized-testing-environment}

Om du vill lägga till eller redigera en miljö måste användaren vara medlem i rollen **Affärsägare**.

**Så här lägger du till en anpassad testmiljö:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på programmet som du vill lägga till en miljö för.

1. Gör något av följande:

   * På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på **Lägg till miljö** på **miljökortet**.
Om alternativet **Lägg till miljö** är nedtonat (inaktiverat) kan det bero på att behörigheter saknas eller att de är beroende av de licensierade resurserna.

     ![Miljökort](assets/no-environments.png)

   * Klicka på ![dataikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljöer** på den vänstra panelen och klicka sedan på **Lägg till miljö** på sidan Miljöer, i det övre högra hörnet.

     ![Fliken Miljö](assets/environments-tab.png)

1. Gör följande i dialogrutan **Lägg till miljö**:

   * Klicka på **Specialiserad testmiljö**.
   * Ange miljön **Namn**. Miljönamnet kan inte ändras efter att miljön har skapats.
   * (Valfritt) Ange en **beskrivning** för miljön.
   * Välj en **primär region** i listrutan. När den har skapats är den primära regionen i den specialiserade testmiljön (till exempel *Storbritannien (syd)*) låst och kan inte ändras.

     ![Dialogrutan Lägg till miljö med alternativknappen Specialiserad testmiljö markerad](assets/specialized-test-environment.png)

1. Klicka på **Spara**.

   Sidan **Översikt** visar nu din nya miljö på kortet **Miljöer**. Nu kan du ställa in rörledningar för din nya miljö.

## Ytterligare resurser {#additional-resources}

* Video: [Miljötyper i AEM Cloud Manager](https://experienceleague.adobe.com/en/perspectives/cloud-manager-environment-types)
* [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md)

