---
title: Vanliga frågor om Dynamic Media med OpenAPI-funktioner
description: Vanliga frågor om Dynamic Media med OpenAPI-funktioner
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Vanliga frågor om Dynamic Media med OpenAPI-funktioner {#new-dynaminc-media-apis-frequently-asked-questions}

+++**Finns alla resurser i Experience Manager Assets as a Cloud Service-databasen tillgängliga för sökning och leverans med Dynamic Media med OpenAPI-funktioner?**

Nej, bara [godkända och senaste versionen av resurserna](/help/assets/approved-assets.md) finns för sökning och leverans med Dynamic Media med OpenAPI-funktioner, vilket ger ett enhetligt varumärke i alla kanaler och tillämpningar.

+++

+++**Hur kan administratörer markera nya och befintliga resurser som lagts till i en mapp som godkända?**

Statusen för en resurs i Experience Manager Assets styrs av `jcr:content/metadata/dam:status` -egenskap. Den här egenskapens värden kan vara:

* Godkänd

* Avvisad

* Begärda ändringar

Experience Manager Assets anger statusen Godkänd med ![Godkänn resurser](assets/thumbs-up-icon.svg) som finns på resurskortet, enligt bilden nedan:

![Ikon för Godkända resurser](/help/assets/assets/approved-assets-thumbs-up.png)

Information om hur du godkänner alla resurser i en mapp finns i instruktionerna på [Så här godkänner du resurser i en mapp gruppvis](/help/assets/approved-assets.md#bulk-approve-assets). Det finns också en video som visar hela processen.

När du har konfigurerat en mapp för gruppgodkännande godkänns alla nya resurser som läggs till i mappen automatiskt. Alla befintliga resurser godkänns efter att de har bearbetats om. Se [Bearbetar digitala resurser](/help/assets/reprocessing.md) för instruktioner om hur du bearbetar resurser på nytt. Om du kopierar eller flyttar ej godkända resurser från någon annan mapp måste du [bearbeta om resurserna](/help/assets/reprocessing.md).

Resursen är markerad som `Rejected`, om administratören anger `Rejected` eller `Changes requested` värden. Experience Manager Assets anger statusen Avvisat med ![Avvisa resurser](/help/assets/assets/do-not-localize/reject-assets.svg) finns på tillgångskortet.

+++

+++**Hur kan du få användar- eller grupp-ID:n för Adobe IMS (Adobe Identity Management Services) att användas för att ställa in rollerna för resurser i Experience Manager Admin-vyn för att säkra leverans- och sökupplevelsen?**

Användare som behöver åtkomst till Experience Manager Author-miljön hanteras som Adobe IMS-användare i Adobe Admin Console. Mer information om vad Adobe IMS-användare är och hur de nås och hanteras i Admin Console finns i [Adobe IMS-användare](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**Kan du godkänna flera resurser samtidigt i en mapp?**

Ja, du kan godkänna flera resurser i en mapp samtidigt.

Utför följande steg för att godkänna flera resurser samtidigt i [!DNL Experience Manager Assets]:

1. Markera resursen/resurserna och klicka på **[!UICONTROL Properties]**.
1. I **[!UICONTROL Basic]** flik, rulla ned till **[!UICONTROL Review Status]**.
1. Ändra granskningsstatus till **[!UICONTROL Approved]**.
1. Klicka på **[!UICONTROL Save & Close]**.

+++

+++**Hur säkrar jag materialleveransen och söker efter Dynamic Media OpenAPI:er?**

Med central resursstyrning i Experience Manager kan DAM-administratörer eller varumärkesansvariga hantera åtkomst till resurser. De kan begränsa åtkomsten genom att konfigurera roller för godkända resurser på redigeringssidan, särskilt på den AEM as a Cloud Service författarinstansen.

Slutanvändare som söker efter eller använder leverans-URL:er kan få åtkomst till begränsade resurser när auktoriseringsprocessen har slutförts.

Mer information finns i [Begränsa åtkomst till resurser i Experience Manager](restrict-assets-delivery.md#authoring).

+++

+++**Hur får du behörighet att redigera godkännandestatusen för en resurs?**

Som DAM-användare har du kanske inte behörighet att [godkänna tillgångar](approved-assets.md#approve-assets). För att få behörighet att redigera godkännandestatusen för en resurs kan administratörer redigera standardmetadataschemat eller andra metadatascheman som används i resursmappen och ge redigeringsbehörigheter till **[!UICONTROL Review Status]** fält. Mer information finns i [hur du inaktiverar redigering för granskningsstatus](approved-assets.md#configuration) fält.

+++

+++**Hur skiljer sig Dynamic Media med OpenAPI-funktioner från Dynamic Media?**

Dynamic Media med OpenAPI-funktioner och Dynamic Media representerar distinkta lösningar som alla har specialfunktioner för leverans. Det är av största vikt att du noggrant granskar dina specifika krav för att fastställa den lämpligaste lösningen som passar dina behov.

Nedan följer några av de viktigaste skillnaderna mellan Dynamic Media med OpenAPI-funktioner och Dynamic Media:

| Dynamic Media med OpenAPI-funktioner | Dynamic Media |
|---|---|
| [Endast tillgängligt med Assets as a Cloud Service](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | Finns även för Managed Services på plats eller Adobe med ytterligare konfigurations- och provisioneringsåtgärder. |
| [Begränsad uppsättning bildmodifierare som stöds, till exempel bredd, höjd, rotering, vändning, kvalitet och format](/help/assets/deliver-assets-apis.md) | En mängd tillgängliga bildmodifierare |
| [Begränsad leverans av resurser baserat på användare och roller](/help/assets/restrict-assets-delivery.md) | Resurser som publiceras på Dynamic Media är tillgängliga för alla användare |
| Stöd för smart beskärning av bilder | Stöd för smart beskärning av bilder och video |
| Stapla baserat på OpenAPI-specifikationer, som de flesta utvecklare känner igen. AEM Assets utbyggbarhet blir mycket enkelt genom att använda [Micro Frontend Asset Selector](/help/assets/asset-selector.md). | SOAP-baserade API:er, som blir ett hinder när man utvecklar integrationsanpassningar. |
| Ändringar som görs i godkända resurser i DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i leverans-URL:erna. Med ett kort TTL-värde (Time-to-Live) på 10 minuter konfigurerat för Dynamic Media med OpenAPI-funktioner via CDN blir uppdateringarna synliga i alla redigerings- och publiceringsgränssnitt på mindre än 10 minuter. | Rekommenderad CDN TTL på 10 timmar. Du kan åsidosätta TTL-värdet med åtgärden för cacheogiltigförklaring. |
| Endast godkända mediefiler finns tillgängliga för leverans av mediefiler till applikationer längre fram i kedjan, vilket möjliggör för varumärken som godkänner mediefiler i digitala upplevelser. Levererade mediefiler har samma förfallostatus som mediefiler på Författarinstansen AEM den as a Cloud Service databasen. | Alla uppdateringar av en Dynamic Media-publicerad mediefil publiceras automatiskt utan något arbetsflöde för godkännande, vilket inte säkerställer att det inte finns något varumärkesgodkänt material i digitala upplevelser. Inga interna tillgångar förfaller. En resurs förblir offentlig tills den tas bort från AEM as a Cloud Service databasen. |
| Användningsrapporter baserade på antalet levererade resurser. | Användningsrapporter är inte tillgängliga. |

+++

+++**Hur åtgärdar Dynamic Media med OpenAPI-funktioner begränsningarna i funktionen Connected Assets?**

Tabellen nedan visar de viktigaste skillnaderna mellan de två lösningarna:

| Dynamic Media med OpenAPI-funktioner | Anslutna resurser |
|---|---|
| Resurser för fjärdistributionen av DAM är tillgängliga på AEM as a Cloud Service. | Resurser för fjärdistributionen av DAM kan vara tillgängliga AEM as a Cloud Service eller Adobe Managed Services. |
| Resursbinärfiler kopieras inte när resurser på en fjärr-DAM-distribution är tillgängliga i en AEM Sites-instans. | Resursbinärfiler kopieras när resurser på en fjärr-DAM-distribution är tillgängliga på en AEM Sites-instans. |
| Stöd för alla format som stöds av AEM Assets. | Inget stöd för videor. |
| Stöder smart beskärning av bilder. | Stöd för Dynamic Media bildsmarta beskärningar och bildförinställningar. |
| Du kan använda Dynamic Media på den lokala platsdistributionen när du hämtar resurser från fjärr-DAM-distribution. | Dynamic Media på lokal platsdistribution är skrivskyddat. |
| Inga begränsningar för antalet AEM Sites-instanser som är anslutna till en fjärr-DAM-distribution. Du kan [begränsa åtkomsten till resurser på Sites-instansen genom att konfigurera roller](/help/assets/restrict-assets-delivery.md) för godkända resurser på fjärr-DAM. | Begränsning för att ansluta högst fyra AEM Sites-instanser till fjärr-DAM-distributionen. Ökat antal kräver ytterligare testning. |
| Både resursväljaren och Dynamic Media med OpenAPI-funktioner kan utökas för att tillåta anpassade integreringar. | API:er för anslutna resurser kan inte utökas för att tillåta anpassade integreringar. |
| Alla ändringar som görs i godkända resurser som är tillgängliga vid fjärdistributionen av DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i Sites-instansen inom ett kort TTL-värde på 10 minuter. | Resursuppdateringar för fjärrdistribution av DAM hanteras automatiskt via livscykelhändelser, men tar mycket längre tid jämfört med Dynamic Media med OpenAPI-funktioner. |
| Resursmetadata på fjärr-DAM är även tillgängliga på AEM Sites-instanser. | Resursmetadata på fjärr-DAM är inte tillgängliga på AEM Sites-instansen. |

+++



