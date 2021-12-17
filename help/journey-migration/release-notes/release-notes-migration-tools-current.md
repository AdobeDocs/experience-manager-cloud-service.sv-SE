---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.12.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.12.0
feature: Release Information
source-git-commit: a1c57a9d8165c9e67ce270a3f0c2ad80c75b7196
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 2%

---


# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.12.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>Om du vill visa den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service klickar du på [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.22 är 1 december 2021.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka och rapportera vilken version av ACS-kommandon som används.
* Möjlighet att identifiera och rapportera antalet användare och undergrupper i en grupp.
* Möjlighet att identifiera och rapportera om egenskapsvärden för noder i MongoDB som överstiger 16 MB.

### Felkorrigeringar {#bug-fixes-bpa}

* Identifieringen av Foundation-komponenter förfinades för att minska falska negativ.
* För AEM Forms-kunder gäller BPA-meddelanden `EMAIL_PDF_SUBMIT_ACTION` som inte är tillgänglig på AEM as a Cloud Service har åtgärdats.


## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.7.10 är 8 december 2021.

### Nyheter {#what-is-new-ctt}

* Växla som lagts till i inmatningsfasen i verktyget Innehållsöverföring så att användarna kan inaktivera [förkopia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) under intag. För optimal överföringshastighet bör pre-copy under intag inaktiveras för små migreringsuppsättningar eller om endast ett fåtal bloggar har lagts till sedan det senaste intaget.
* Användarmappning har uppdaterats för att använda ett förbättrat API för användarhantering som gör att 2 000 användare kan hämtas samtidigt, vilket avsevärt förbättrar prestandan.
