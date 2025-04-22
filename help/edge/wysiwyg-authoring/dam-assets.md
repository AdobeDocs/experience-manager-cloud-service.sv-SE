---
title: Publicera sidor med DAM Assets med Edge Delivery Services
description: Lär dig vilka inställningar som krävs för att säkerställa att dina DAM-resurser för dina sidor publiceras smidigt till Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Publicera sidor med DAM Assets med Edge Delivery Services {#dam-assets}

Lär dig vilka inställningar som krävs för att säkerställa att dina DAM-resurser för dina sidor publiceras smidigt till Edge Delivery Services.

## Universal Editor, DAM Assets och Edge Delivery {#overview}

När du redigerar innehåll för den universella redigeraren kan du förstås välja resurser från DAM. När du publicerar ditt innehåll på Edge Delivery Services publiceras även det relaterade DAM-innehållet.

För att detta ska fungera måste AEM och Edge Delivery Services ha tillgång till DAM för att kunna publicera. Detta omfattar följande:

* [Kontrollera att resursmappar är tillgängliga](#accessible).
* [Kontrollera att resursmappen har tilldelats rätt konfiguration (efter behov)](#configuration).

## Kontrollera att Assets-mappar är tillgängliga {#accessible}

När du publicerar sidor från AEM till Edge Delivery Services används [ett tekniskt konto](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md). Det här kontot, med ett namn i formatet `<hash>@techacct.adobe.com`, skapas automatiskt som en användare i AEM av Cloud Manager när du publicerar en sida som har skapats med den universella redigeraren.

![Tekniskt konto](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

Det här tekniska kontot måste ha åtkomsträttigheter till alla DAM-mappar för att kunna publicera deras innehåll. Du kan antingen:

* Använd inte privata DAM-mappar.
* Ge den tekniska kontoanvändaren åtkomst till DAM-mapparna.

## Kontrollera att Assets-mappen har tilldelats rätt konfiguration {#configuration}

I allmänhet räcker det att försäkra dig om att ditt tekniska konto har tillgång till dina resurser i DAM för att publicera dina resurser tillsammans med dina sidor på Edge Delivery Services.

Ytterligare konfiguration krävs i ytterligare två fall:

* Om du vill publicera sidor med icke-bildresurser som PDF-filer eller videor till Edge Delivery Services.
* Om du vill publicera bildresurser på Edge Delivery Services oberoende av sidor.

Om du vill ha stöd för båda dessa användningsfall måste en [konfiguration](/help/implementing/developing/introduction/configurations.md) tilldelas till DAM-mappen.

1. Logga in i AEM redigeringsmiljö.
1. Under **Webbplatser** väljer du den webbplats där du publicerar dina resurser eller den plats som resurserna ska associeras med.
1. Tryck eller klicka på **Egenskaper** i verktygsfältet.
1. Observera konfigurationen i fältet **Molnkonfiguration** på fliken **Avancerat** i egenskapsfönstret.
   * Detta skapas automatiskt när du skapar din webbplats i formatet `/conf/<site-name>`.
1. Tryck eller klicka på **Avbryt** i egenskapsfönstret och navigera till **Assets** -> **Filer** och markera din DAM-mapp.
1. Tryck eller klicka på **Egenskaper** i verktygsfältet.
1. På fliken **Molntjänster** i egenskapsfönstret väljer du samma konfiguration som du angav tidigare i fältet **Molnkonfiguration**.
1. Tryck eller klicka på **Spara och stäng**.
