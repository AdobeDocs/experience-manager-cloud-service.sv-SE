---
title: Miljövariabler i Cloud Manager
description: Standardmiljövariabler kan konfigureras och hanteras via Cloud Manager och tillhandahållas i körningsmiljön, som kan användas i OSGi-konfigurationer.
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---


# Miljövariabler i Cloud Manager {#environment-variables}

Standardmiljövariabler kan konfigureras och hanteras via Cloud Manager. De tillhandahålls körtidsmiljön och kan användas i OSGi-konfigurationer.

Miljövariabler kan vara antingen miljöspecifika värden eller miljöhemligheter, baserat på vad som ändras.

## Om miljövariabler {#overview}

Miljövariabler ger en mängd fördelar för användare av AEM as a Cloud Service, till exempel följande:

* De gör att beteendet i koden och programmet kan variera beroende på sammanhang och miljö. De kan till exempel användas för att aktivera olika konfigurationer i utvecklingsmiljön jämfört med produktions- eller scenmiljöerna för att undvika kostsamma misstag.
* De behöver bara konfigureras och konfigureras en gång och kan uppdateras och tas bort vid behov.
* Deras värden kan uppdateras när som helst och börja gälla omedelbart utan att kodändringar eller -distributioner behövs.
* De kan skilja kod från konfiguration och ta bort behovet av att inkludera känslig information i versionskontrollen.
* De förbättrar säkerheten i AEM as a Cloud Service eftersom de finns utanför koden.

Exempel på vanliga användningsområden för miljövariabler är:

* Koppla ditt AEM-program till olika externa slutpunkter
* Använda en referens när du lagrar lösenord i stället för direkt i kodbasen
* När det finns flera utvecklingsmiljöer i ett program och en del konfigurationer skiljer sig från en miljö till nästa

## Lägg till en miljövariabel {#add-variables}

Om du vill lägga till flera variabler rekommenderar Adobe att du lägger till den första variabeln och sedan använder du ![Lägg till ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Lägg till** i dialogrutan **Miljökonfiguration** för att lägga till ytterligare variabler. Den här metoden innebär att du kan lägga till dem med en uppdatering i miljön.

Om du vill lägga till, uppdatera eller ta bort miljövariabler måste du vara medlem i rollen [**Distributionshanteraren**](/help/onboarding/cloud-manager-introduction.md#role-based-premissions).

**Så här lägger du till en miljövariabel:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du den du vill hantera.
1. Klicka på **Miljö** på sidomenyn.
1. På sidan **Miljö** väljer du en rad i tabellen som innehåller den miljö som du vill lägga till en miljövariabel för.
1. Klicka på fliken **Konfiguration** på miljöns detaljsida.
1. Klicka på ![Lägg till/uppdatera - ikonen Lägg till cirkel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Lägg till/uppdatera**.
Om du lägger till en miljövariabel för första gången klickar du på **Lägg till konfiguration** mitt på sidan.

   ![Fliken Konfiguration](assets/configuration-tab.png)

1. Ange informationen på tabellens första rad i dialogrutan **Miljökonfiguration**.

   | Fält | Beskrivning |
   | --- | --- |
   | Namn | Ett unikt namn på konfigurationsvariabeln. Den identifierar den specifika variabeln som används i miljön. Den måste följa följande namngivningskonventioner:<ul><li>Variabler får bara innehålla alfanumeriska tecken och understreck (`_`).</li><li>Det finns en gräns på 200 variabler per miljö.</li><li>Varje namn får innehålla högst 100 tecken.</li></ul> |
   | Värde | Värdet som variabeln innehåller. |
   | Steget används | Välj vilken tjänst variabeln gäller för. Markera **Alla** om du vill att variabeln ska användas för alla tjänster.<ul><li>**Alla**</li><li>**Författare**</li><li>**Publicera**</li><li>**Förhandsgranska**</li></ul> |
   | Typ | Välj om variabeln är normal eller en hemlighet. |

   ![Lägger till en variabel](assets/add-variable.png)

1. Klicka på ![Lägg till ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)**Lägg till**.

   Lägg till ytterligare variabler efter behov.

1. Klicka på **Spara**.

   En rotationsruta med statusen **Uppdatering** visas i tabellens övre högra hörn. En snurra visas också till vänster om nya variabler som du har lagt till. Dessa statusvärden anger att miljön uppdateras med konfigurationen. När du är klar visas den nya systemvariabeln i tabellen.

![Uppdaterar variabler](assets/updating-variables.png)

## Uppdatera en miljövariabel {#update-variables}

När du har skapat miljövariabler kan du uppdatera dem med ikonen ![Lägg till/uppdatera - lägg till cirkel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Lägg till/uppdatera** för att öppna dialogrutan **Miljökonfiguration**.

Om du vill uppdatera flera variabler rekommenderar Adobe att du använder dialogrutan **Miljökonfiguration** för att uppdatera alla nödvändiga variabler samtidigt innan du klickar på **Spara**. På så sätt kan du lägga till dem med en uppdatering i miljön.

**Så här uppdaterar du en miljövariabel:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du den du vill hantera.
1. Klicka på **Miljö** på sidomenyn.
1. På sidan **Miljö** väljer du en rad i tabellen som innehåller den miljö som du vill uppdatera en variabel för.
1. Klicka på fliken **Konfiguration** på miljöns detaljsida.
1. Klicka på ![Lägg till/uppdatera - ikonen Lägg till cirkel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Lägg till/uppdatera**.
1. I dialogrutan **Miljökonfiguration** klickar du på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i den sista kolumnen i raden i variabeln som du vill ändra.
1. Klicka på **Redigera** i listrutan.

   ![Redigera eller ta bort variabel](assets/edit-delete-variable.png)

1. Uppdatera vid behov miljövariabelns värde.
När du redigerar en hemlighet kan värdet bara uppdateras, inte visas.

   ![Redigera variabel](assets/edit-variable.png)

1. Gör något av följande:

   * Klicka på ![Använd - bockmarkeringsikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) för att tillämpa ändringen.
   * Klicka på ![Ångra-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg) om du vill ångra ändringen.

1. Klicka på **Spara**.

   En rotationsruta med statusen **Uppdatering** visas i tabellens övre högra hörn. En snurra visas också till vänster om alla uppdaterade variabler. Dessa statusvärden anger att miljön uppdateras med konfigurationen. När du är klar visas den uppdaterade systemvariabeln i tabellen.

## Ta bort en miljövariabel {#delete-env-variable}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du den du vill hantera.
1. Klicka på **Miljö** på sidomenyn.
1. På sidan **Miljö** väljer du en rad i tabellen som innehåller den miljö som du vill uppdatera en variabel för.
1. Klicka på fliken **Konfiguration** på miljöns detaljsida.
1. Klicka på ![Lägg till/uppdatera - ikonen Lägg till cirkel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Lägg till/uppdatera**.
1. I dialogrutan **Miljökonfiguration** klickar du på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i den sista kolumnen i raden i variabeln som du vill ändra.
1. Klicka på **Ta bort** i listrutan om du vill ta bort variabeln direkt.
1. Klicka på **Spara**.

## Användning av miljövariabler {#using}

Miljövariabler kan göra dina `pom.xml`-konfigurationer säkrare och mer flexibla. Lösenord behöver till exempel inte vara hårdkodade och konfigurationen kan anpassas baserat på värdena i miljövariablerna.

Du kan komma åt miljövariabler och hemligheter via XML på följande sätt:

`${env.VARIABLE_NAME}`

Se [Konfigurera projekt](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories) för ett exempel på hur du använder båda typer av variabler i en `pom.xml` -fil.

Mer information finns även i den [officiella dokumentationen för Maven](https://maven.apache.org/settings.html#quick-overview).

## Tillgänglighet för miljövariabler {#availability}

Miljövariabler kan användas på flera ställen enligt följande:

| Där miljövariabler kan användas | Beskrivning |
| --- | --- |
| Skapa, förhandsgranska och publicera | Både vanliga miljövariabler och hemligheter kan användas i redigerings-, förhandsgransknings- och publiceringsmiljöer. |
| Dispatcher | Endast reguljära miljövariabler kan användas med [Dispatcher](https://experienceleague.adobe.com/sv/docs/experience-manager-dispatcher/using/dispatcher).<ul><li>Hemligheter kan inte användas.</li><li>Miljövariabler kan inte användas i `IfDefine`-direktiv.</li><li>Verifiera din användning av miljövariabler med [Dispatcher lokalt](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools) innan du distribuerar.</li></ul> |
| OSGi-konfigurationer | Både vanliga miljövariabler och hemligheter kan användas i [OSGi-konfigurationer](/help/implementing/deploying/configuring-osgi.md). |
| Rörledningsvariabler | Förutom miljövariabler finns det även variabler för pipeline som exponeras under byggfasen. Läs mer om pipeline-variabler i [Build Environment](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables). |

