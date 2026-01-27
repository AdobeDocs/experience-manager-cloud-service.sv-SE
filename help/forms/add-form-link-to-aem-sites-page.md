---
title: Hur lägger man till formulärlänkar på AEM Sites-sidan med Länka Forms Portal?
description: Lär dig hur du lägger till formulärlänkar på AEM Sites-sidan.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: a55d0776-8827-46cc-9625-5d6f5f6bda3b
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Lägga till formulärlänkar på webbplatssidan

I scenariot med bankwebbplatser förbättrar Forms Portal-komponenten **Link** navigeringen genom att vägleda användare till specifika formulär i olika delar av webbplatsen. Det ger direkta referenser till formulär som låneansökningar, kontoöppningsformulär eller feedbackundersökningar, som placeras ut strategiskt på hela webbplatsen. Komponenten **Link** infogar länkar som dirigerar användare till specifika adaptiva Forms på sidan Platser. På bankens webbplats kan anonyma användare till exempel få tillgång till ett allmänt frågeformulär, medan inloggade användare kan få direkt tillgång till säkrare formulär, som låneansökningar eller transaktionsauktoriseringsformulär.

![Länkikon](/help/forms/assets/link-forms.png)


## Lägg till länkkomponenten på din webbplatssida

Så här lägger du till portalkomponenten **Link** på din webbplatssida:

1. Öppna AEM Sites-sidan i **redigeringsläge**.
1. Gå till **[!UICONTROL Page Information]** > **[!UICONTROL Edit Template]**
   ![Redigera mallprincip](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Klicka på **[!UICONTROL Policy]** och markera kryssrutan **[!UICONTROL Link]** under **[Projektnamn för AEM-arkityp] - Forms och kommunikationsportal**.

   ![Principval](/help/forms/assets/add-link.png)

1. Klicka på **[!UICONTROL Done]**.
1. Öppna nu AEM Sites-sidan igen i redigeringsläget.
1. Leta reda på det avsnitt i sidredigeraren där du kan lägga till Forms Portal-komponenten.

1. Klicka på ikonen **Lägg till** . Ikonen är ett plustecken (+) som anger att du kan lägga till nya komponenter.

   Om du klickar på ikonen **Lägg till** visas dialogrutan **Infoga ny komponent** som visar olika komponenter som ska infogas.

   >[!NOTE]
   >
   > Du kan också dra och släppa komponenten.

1. Bläddra bland de tillgängliga komponenterna i dialogrutan och välj önskad komponent i listan. Välj till exempel komponenten **Link** i listan om du vill lägga till Forms Portal-komponenten **Link** .

   ![Länkkomponent](/help/forms/assets/add-link-in-sites.png)

Konfigurera egenskaperna för komponenten **Link**.

## Lär dig egenskaperna för länkkomponenten

Du kan enkelt anpassa komponentegenskaperna för **Link** med dialogrutan Konfigurera för en smidig användarupplevelse. Konfigurera genom att markera komponenten och sedan välja ikonen ![Konfigurera](assets/configure_icon.png). Dialogrutan **[!UICONTROL Link]** öppnas.

### Visa flik

![Visa flik](/help/forms/assets/link-asset-tab.png)

På fliken **[!UICONTROL Display]** anger du länkbeskrivningen och verktygstipset för att underlätta identifiering av de formulär som länken representerar.

### Fliken Resursinformation

![Assets Info Tab](/help/forms/assets/link-asset-info.png)

Ange databassökvägen där resursen lagras på fliken **[!UICONTROL Asset Info]**.

### Fliken Frågeparametrar

![Fliken Frågeparametrar](/help/forms/assets/link-query-tab.png)

På fliken **[!UICONTROL Query Params]** anger du ytterligare parametrar i nyckelvärdepar-formatet. När användaren klickar på länken skickas dessa ytterligare parametrar tillsammans med formuläret.

## Visa formulärlänkar på sidan Webbplatser med hjälp av komponenten Länk

Förhandsgranska sidan Webbplatser om du vill visa länken till ett adaptivt formulär, som anges på egenskapsfliken **Assets Info** i komponenten **Link** . När du klickar på länken visas formuläret på skärmen för användare som sedan kan komma åt det baserat på behörigheter.

![Fliken Frågeparametrar](/help/forms/assets/link-forms.png)

## Relaterade artiklar

{{forms-portal-see-also}}

## Se även {#see-also}

{{see-also}}
