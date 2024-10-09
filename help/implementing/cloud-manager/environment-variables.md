---
title: Cloud Manager miljövariabler
description: Standardmiljövariabler kan konfigureras och hanteras via Cloud Manager och tillhandahållas i körningsmiljön, som används i OSGi-konfigurationen.
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---


# Cloud Manager miljövariabler {#environment-variables}

Standardmiljövariabler kan konfigureras och hanteras via Cloud Manager. De tillhandahålls körtidsmiljön och kan användas i OSGi-konfigurationer. Miljövariabler kan vara antingen miljöspecifika värden eller miljöhemligheter, baserat på vad som ändras.

## Ökning {#overview}

Miljövariabler ger en mängd fördelar för användare av AEM as a Cloud Service:

* De gör att beteendet i koden och programmet kan variera beroende på sammanhang och miljö. De kan till exempel användas för att aktivera olika konfigurationer för utvecklingsmiljön jämfört med produktions- eller scenmiljöerna för att undvika kostsamma misstag.
* De behöver bara konfigureras och konfigureras en gång och kan uppdateras och tas bort vid behov.
* Deras värden kan uppdateras när som helst och börja gälla omedelbart utan att kodändringar eller -distributioner behövs.
* De kan skilja kod från konfiguration och ta bort behovet av att inkludera känslig information i versionskontrollen.
* De förbättrar säkerheten i AEM as a Cloud Service eftersom de finns utanför koden.

Exempel på vanliga användningsområden är:

* Ansluta AEM med olika externa slutpunkter
* Använda en referens när du lagrar lösenord i stället för direkt i kodbasen
* När det finns flera utvecklingsmiljöer i ett program och en del konfigurationer skiljer sig från en miljö till nästa

## Lägga till miljövariabler {#add-variables}

>[!NOTE]
>
>Du måste vara medlem i rollen [**Distributionshanteraren**](/help/onboarding/cloud-manager-introduction.md#role-based-premissions) för att kunna lägga till eller ändra miljövariabler.

1. Logga in på Adobe Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du den du vill hantera.
1. Välj fönstret **Miljö** för det valda programmet i navigeringsfältet och välj sedan den miljö som du vill skapa en miljövariabel för.
1. Markera fliken **Konfiguration** i detaljerna för miljön och välj sedan **Lägg till** för att öppna dialogrutan **Miljökonfiguration**.
   * Om du lägger till en miljövariabel för första gången kan du se knappen **Lägg till konfiguration** mitt på sidan. Du kan använda den här knappen eller **Lägg till** för att öppna dialogrutan **Miljökonfiguration** .

   ![Fliken Konfiguration](assets/configuration-tab.png)

1. Ange variabelinformationen.
   * **Namn**
   * **Värde**
   * **Tjänsten används** - Definierar för vilken tjänst (Författare/Publish/Förhandsgranska) variabeln gäller eller om den gäller för alla tjänster
   * **Typ** - Definierar om variabeln är normal eller hemlig

   ![Lägger till en variabel](assets/add-variable.png)

1. När du har angett den nya variabeln måste du välja **Lägg till** i den sista kolumnen i raden som innehåller den nya variabeln.
   * Du kan ange flera variabler samtidigt genom att ange en ny rad och välja **Lägg till**.

   ![Spara variabler](assets/save-variables.png)

1. Välj **Spara** om du vill behålla variablerna.

En indikator med statusen **Uppdatering** visas högst upp i tabellen och bredvid den nyligen tillagda variabeln för att ange att miljön uppdateras med konfigurationen. När du är klar visas den nya systemvariabeln i tabellen.

![Uppdaterar variabler](assets/updating-variables.png)

>[!TIP]
>
>Om du vill lägga till flera variabler bör du lägga till den första variabeln och sedan använda knappen **Lägg till** i dialogrutan **Miljökonfiguration** för att lägga till ytterligare variabler. På så sätt kan du lägga till dem med en uppdatering i miljön.

## Uppdaterar miljövariabler {#update-variables}

När du har skapat miljövariabler kan du uppdatera dem med knappen **Lägg till/uppdatera** för att öppna dialogrutan **Miljökonfiguration** .

1. Logga in på Adobe Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Cloud Manager listar de olika program som är tillgängliga. Markera den du vill hantera.
1. Välj fönstret **Miljö** för det valda programmet i navigeringspanelen och välj sedan den miljö som du vill ändra en miljövariabel för.
1. Markera fliken **Konfiguration** och välj sedan **Lägg till/uppdatera** i det övre högra hörnet för att öppna dialogrutan **Miljökonfiguration**.
1. Använd ellipsknappen i den sista kolumnen i raden i variabeln som du vill ändra och välj **Redigera** eller **Ta bort**.

   ![Redigera eller ta bort variabel](assets/edit-delete-variable.png)

1. Redigera systemvariabeln efter behov.
   * När du redigerar ändras ellipsknappen till alternativ för att återgå till det ursprungliga värdet eller bekräfta ändringen.
   * När du redigerar hemligheter kan värdena bara uppdateras, inte visas.

   ![Redigera variabel](assets/edit-variable.png)

1. När du har gjort de nödvändiga konfigurationsändringarna väljer du **Spara**.

[Som när du lägger till variabler](#add-variables) visas en indikator med statusen **Uppdatering** högst upp i tabellen och bredvid de nyligen uppdaterade variabelerna för att ange att miljön uppdateras med konfigurationen. När du är klar visas de uppdaterade miljövariablerna i tabellen.

>[!TIP]
>
>Om du vill uppdatera flera variabler bör du använda dialogrutan **Miljökonfiguration** för att uppdatera alla nödvändiga variabler samtidigt innan du trycker eller klickar på **Spara**. På så sätt kan du lägga till dem med en uppdatering i miljön.

## Använda miljövariabler {#using}

Miljövariabler kan göra dina `pom.xml`-konfigurationer säkrare och mer flexibla. Lösenord behöver till exempel inte vara hårdkodade och konfigurationen kan anpassas baserat på värdena i miljövariablerna.

Du får åtkomst till miljövariabler och hemligheter via XML enligt följande.

* `${env.VARIABLE_NAME}`

I dokumentet [Konfigurera projekt](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories) finns ett exempel på hur du använder båda typerna av variabler i en `pom.xml` -fil.

Mer information finns i den [officiella dokumentationen för Maven](https://maven.apache.org/settings.html#quick-overview).

## Miljövariabel tillgänglighet {#availability}

Miljövariabler kan användas på flera ställen.

### Författare, Förhandsgranska och Publish {#author-preview-publish}

Både vanliga miljövariabler och hemligheter kan användas i redigerings-, förhandsgransknings- och publiceringsmiljöer.

### Dispatcher {#dispatcher}

Endast reguljära miljövariabler kan användas med [det går inte att använda dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) Secrets.

Miljövariabler kan dock inte användas i `IfDefine`-direktiv.

>[!TIP]
>
>Du bör validera din användning av miljövariabler med [dispatchern lokalt](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html) innan du distribuerar.

### OSGi-konfigurationer {#osgi}

Både vanliga miljövariabler och hemligheter kan användas i [OSGi-konfigurationer](/help/implementing/deploying/configuring-osgi.md).

### Rörledningsvariabler {#pipeline}

Förutom miljövariabler finns det även variabler för pipeline som exponeras under byggfasen. Läs mer om pipeline-variabler under [Build Environment](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables).
