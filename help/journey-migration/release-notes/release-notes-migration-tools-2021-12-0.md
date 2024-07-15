---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.12.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.12.0
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.12.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>Klicka [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html) om du vill se den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.22 är 1 december 2021.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka och rapportera vilken version av ACS-kommandon som används.
* Möjlighet att identifiera och rapportera antalet användare och undergrupper i en grupp.
* Möjlighet att identifiera och rapportera om egenskapsvärden för noder i MongoDB som överstiger 16 MB.

### Felkorrigeringar {#bug-fixes-bpa}

* Identifieringen av Foundation-komponenter förfinades för att minska falska negativ.
* För AEM Forms-kunder har BPA-meddelanden om att `EMAIL_PDF_SUBMIT_ACTION` inte är tillgänglig på AEM as a Cloud Service korrigerats.


## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.7.10 är 8 december 2021.

### Nyheter {#what-is-new-ctt}

* Växla som lagts till i inmatningsfasen i verktyget Innehållsöverföring så att användarna kan inaktivera [pre-copy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) under importen. För optimal överföringshastighet bör pre-copy under intag inaktiveras för små migreringsuppsättningar eller om endast ett fåtal bloggar har lagts till sedan det senaste intaget.
* Användarmappning har uppdaterats för att använda ett förbättrat API för användarhantering som gör att 2 000 användare kan hämtas samtidigt, vilket avsevärt förbättrar prestandan.
