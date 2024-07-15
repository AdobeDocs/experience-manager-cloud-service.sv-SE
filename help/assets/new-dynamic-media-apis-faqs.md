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

+++**Är alla resurser i Experience Manager Assets as a Cloud Service-databasen tillgängliga för sökning och leverans med Dynamic Media med OpenAPI-funktioner?**

Nej, endast [godkända och senaste versionen av resurserna](/help/assets/approved-assets.md) är tillgängliga för sökning och leverans med Dynamic Media med OpenAPI-funktioner, vilket säkerställer att alla kanaler och program har ett enhetligt varumärke.

+++

+++**Hur kan administratörer markera nya och befintliga resurser som lagts till i en mapp som godkända?**

Status för en resurs i Experience Manager Assets styrs av egenskapen `jcr:content/metadata/dam:status`. Den här egenskapens värden kan vara:

* Godkänd

* Avvisad

* Begärda ändringar

Experience Manager Assets anger statusen Godkänd med hjälp av ![Godkänn Assets](assets/thumbs-up-icon.svg) som finns på resurskortet, vilket visas i följande bild:

![Ikon för Godkända resurser](/help/assets/assets/approved-assets-thumbs-up.png)

Information om hur du godkänner alla resurser i en mapp finns i instruktionerna för [att massgodkänna resurser i en mapp](/help/assets/approved-assets.md#bulk-approve-assets). Det finns också en video som visar hela processen.

När du har konfigurerat en mapp för gruppgodkännande godkänns alla nya resurser som läggs till i mappen automatiskt. Alla befintliga resurser godkänns efter att de har bearbetats om. Mer information om hur du bearbetar resurser finns i [Återbearbetar digitala resurser](/help/assets/reprocessing.md). Om du kopierar eller flyttar ej godkända resurser från någon annan mapp måste du [bearbeta om resurserna](/help/assets/reprocessing.md).

Resursen markeras som `Rejected` om administratören anger `Rejected`- eller `Changes requested`-värden. Experience Manager Assets anger statusen Avvisat med ![Avvisa Assets](/help/assets/assets/do-not-localize/reject-assets.svg) som finns på resurskortet.

+++

+++**Hur kan du få användar- eller grupp-ID:t för Adobe IMS (Adobe Identity Management Services) att användas för att ställa in rollerna för resurser i Experience Manager Admin-vyn, för att säkra leverans- och sökupplevelsen?**

Användare som behöver åtkomst till Experience Manager Author-miljön hanteras som Adobe IMS-användare i Adobe Admin Console. Mer information om vad Adobe IMS-användare är och hur de nås och hanteras i Admin Console finns i [Adobe IMS-användare](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**Kan du godkänna flera resurser samtidigt i en mapp?**

Ja, du kan godkänna flera resurser i en mapp samtidigt.

Utför följande steg för att godkänna flera resurser samtidigt i [!DNL Experience Manager Assets]:

1. Markera resurserna och klicka på **[!UICONTROL Properties]**.
1. Bläddra nedåt till **[!UICONTROL Review Status]** på fliken **[!UICONTROL Basic]**.
1. Ändra granskningsstatusen till **[!UICONTROL Approved]**.
1. Klicka på **[!UICONTROL Save & Close]**.

+++

+++**Hur kan jag skydda resursleveransen och söka efter Dynamic Media OpenAPI:er?**

Med central resursstyrning i Experience Manager kan DAM-administratörer eller varumärkesansvariga hantera åtkomst till resurser. De kan begränsa åtkomsten genom att konfigurera roller för godkända resurser på redigeringssidan, särskilt på AEM as a Cloud Service författarinstans.

Slutanvändare som söker efter eller använder leverans-URL:er kan få åtkomst till begränsade resurser när auktoriseringsprocessen har slutförts.

Mer information finns i [Begränsa åtkomst till resurser i Experience Manager](restrict-assets-delivery.md#authoring).

+++

+++**Hur får du behörighet att redigera godkännandestatusen för en resurs?**

Som DAM-användare kanske du inte har behörighet att [godkänna resurser](approved-assets.md#approve-assets). Om du vill ha behörighet att redigera godkännandestatusen för en resurs kan administratören redigera standardmetadataschemat eller något annat metadataschema som används i resursmappen och ge redigeringsbehörighet till fältet **[!UICONTROL Review Status]**. Mer information finns i [Så här inaktiverar du redigering för fältet Granskningsstatus](approved-assets.md#configuration).

+++

+++**Hur skiljer sig Dynamic Media med OpenAPI-funktioner från Dynamic Media?**

Dynamic Media med OpenAPI-funktioner och Dynamic Media representerar distinkta lösningar som alla har specialfunktioner för leverans. Det är av största vikt att du noggrant granskar dina specifika krav för att fastställa den lämpligaste lösningen som passar dina behov.

Nedan följer några av de viktigaste skillnaderna mellan Dynamic Media med OpenAPI-funktioner och Dynamic Media:

| Dynamic Media med OpenAPI-funktioner | Dynamic Media |
|---|---|
| [Endast tillgängligt med Assets as a Cloud Service](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | Finns även för Managed Services på plats eller Adobe med ytterligare konfigurations- och provisioneringsåtgärder. |
| [Begränsad uppsättning bildmodifierare som stöds, till exempel bredd, höjd, rotering, vänd, kvalitet och format](/help/assets/deliver-assets-apis.md) | En mängd tillgängliga bildmodifierare |
| [Begränsad leverans av resurser baserat på användare och roller](/help/assets/restrict-assets-delivery.md) | Assets som publiceras på Dynamic Media är tillgängliga för alla användare |
| Stöd för smart beskärning av bilder | Stöd för smart beskärning av bilder och video |
| Stapla baserat på OpenAPI-specifikationer, som de flesta utvecklare känner igen. AEM Assets utbyggbarhet blir mycket enkelt genom att använda [väljaren för mikrofonresurs](/help/assets/asset-selector.md). | SOAP-baserade API:er, som blir ett hinder när man utvecklar integrationsanpassningar. |
| Ändringar som görs i godkända resurser i DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i leverans-URL:erna. Med ett kort TTL-värde (Time-to-Live) på 10 minuter konfigurerat för Dynamic Media med OpenAPI-funktioner via CDN blir uppdateringarna synliga i alla redigerings- och publiceringsgränssnitt på mindre än 10 minuter. | Rekommenderad CDN TTL på 10 timmar. Du kan åsidosätta TTL-värdet med åtgärden för cacheogiltigförklaring. |
| Endast godkända mediefiler finns tillgängliga för leverans av mediefiler till applikationer längre fram i kedjan, vilket möjliggör för varumärken som godkänner mediefiler i digitala upplevelser. Levererade mediefiler har samma förfallostatus som mediefiler på Författarinstansen av AEM as a Cloud Service-databasen. | Alla uppdateringar av en Dynamic Media-publicerad mediefil publiceras automatiskt utan något arbetsflöde för godkännande, vilket inte säkerställer att det inte finns något varumärkesgodkänt material i digitala upplevelser. Inga interna tillgångar förfaller. En resurs förblir offentlig tills den tas bort från AEM as a Cloud Service-databasen. |
| Användningsrapporter baserade på antalet levererade resurser. | Användningsrapporter är inte tillgängliga. |

+++

+++**Hur åtgärdar Dynamic Media med OpenAPI-funktioner begränsningarna i funktionen för anslutna Assets?**

Tabellen nedan visar de viktigaste skillnaderna mellan de två lösningarna:

| Dynamic Media med OpenAPI-funktioner | Uppkopplad Assets |
|---|---|
| Assets på fjärrdistributionen av DAM är tillgängligt på AEM as a Cloud Service. | Assets på fjärrdistributionen av DAM är tillgängligt på AEM as a Cloud Service eller Adobe Managed Services. |
| Resursbinärfiler kopieras inte när resurser på en fjärr-DAM-distribution är tillgängliga i en AEM Sites-instans. | Resursbinärfiler kopieras när resurser på en fjärr-DAM-distribution är tillgängliga på en AEM Sites-instans. |
| Stöd för alla format som stöds av AEM Assets. | Inget stöd för videor. |
| Stöder smart beskärning av bilder. | Stöd för Dynamic Media bildsmarta beskärningar och bildförinställningar. |
| Du kan använda Dynamic Media på den lokala platsdistributionen när du hämtar resurser från fjärr-DAM-distribution. | Dynamic Media på lokal platsdistribution är skrivskyddat. |
| Inga begränsningar för antalet AEM Sites-instanser som är anslutna till en fjärr-DAM-distribution. Du kan [begränsa åtkomsten till resurser på platsinstansen genom att konfigurera roller](/help/assets/restrict-assets-delivery.md) för godkända resurser på fjärr-DAM. | Begränsning för att ansluta högst fyra AEM Sites-instanser till fjärr-DAM-distributionen. Ökat antal kräver ytterligare testning. |
| Både resursväljaren och Dynamic Media med OpenAPI-funktioner kan utökas för att tillåta anpassade integreringar. | Anslutna Assets-API:er kan inte utökas för att tillåta anpassade integreringar. |
| Alla ändringar som görs i godkända resurser som är tillgängliga vid fjärdistributionen av DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i Sites-instansen inom ett kort TTL-värde på 10 minuter. | Resursuppdateringar för fjärrdistribution av DAM hanteras automatiskt via livscykelhändelser, men tar mycket längre tid jämfört med Dynamic Media med OpenAPI-funktioner. |
| Resursmetadata på fjärr-DAM är även tillgängliga på AEM Sites-instanser. | Resursmetadata på fjärr-DAM är inte tillgängliga på AEM Sites-instansen. |

+++



