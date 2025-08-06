---
title: Dynamic Media med OpenAPI-funktioner - frågor och svar
description: Dynamic Media med OpenAPI-funktioner - frågor och svar
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: 4c346ea4bd3ddea7f5f9f14af56a0b3ec779f9f9
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Dynamic Media med OpenAPI-funktioner - frågor och svar {#new-dynaminc-media-apis-frequently-asked-questions}

## Finns alla resurser i Experience Manager Assets as a Cloud Service-databasen tillgängliga för sökning och leverans med Dynamic Media med OpenAPI-funktioner? {#assets-available-for-search}

Nej, endast [godkända och senaste versionen av resurserna](/help/assets/approve-assets.md) är tillgängliga för sökning och leverans med Dynamic Media med OpenAPI-funktioner, vilket säkerställer att alla kanaler och program har ett enhetligt varumärke.


## Hur kan administratörer markera nya och befintliga resurser som lagts till i en mapp som godkända? {#add-assets-to-folder-as-approved}

Status för en resurs i Experience Manager Assets styrs av egenskapen `jcr:content/metadata/dam:status`. Den här egenskapens värden kan vara:

* Godkänd

* Avvisad

* Begärda ändringar

Experience Manager Assets anger statusen Godkänd med hjälp av en godkänd ikon som finns på tillgångskortet, vilket visas i följande bilder för Admin- och Resursvyer:

**Administratörsvy**

![Godkända resurser i administrationsvyn](/help/assets/assets/approved-assets-thumbs-up.png)

**Assets-vy**

![Godkända resurser i Assets-vyn](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


Information om hur du godkänner alla resurser i en mapp finns i instruktionerna för [att massgodkänna resurser i en mapp](/help/assets/approve-assets.md#bulk-approve-assets). Det finns också en video som visar hela processen.

När du har konfigurerat en mapp för gruppgodkännande godkänns alla nya resurser som läggs till i mappen automatiskt. Alla befintliga resurser godkänns efter att de har bearbetats om. Mer information om hur du bearbetar resurser finns i [Återbearbetar digitala resurser](/help/assets/reprocessing.md). Om du kopierar eller flyttar ej godkända resurser från någon annan mapp måste du [bearbeta om resurserna](/help/assets/reprocessing.md).

Resursen markeras som `Rejected` om administratören anger `Rejected`- eller `Changes requested`-värden. Experience Manager Assets anger statusen Avvisat med ![Avvisa Assets](/help/assets/assets/do-not-localize/reject-assets.svg) som finns på resurskortet i administratörsvyn.

På samma sätt anger Experience Manager Assets statusen Avvisat i Assets-vyn med följande status Avvisat på resurskortet:

![Avvisade resurser i Assets-vyn](/help/assets/assets/rejected-assets-admin-view.png)


## Hur kan du få användar- eller grupp-ID:n för Adobe IMS (Adobe Identity Management Services) att användas för att ange rollerna för resurser i Experience Manager Admin-vyn, för att säkra leverans- och sökupplevelsen? {#set-roles-secure-delivery-search}

Användare som behöver åtkomst till Experience Manager Author-miljön hanteras som Adobe IMS-användare i Adobe Admin Console. Mer information om vad Adobe IMS-användare är och hur de nås och hanteras i Admin Console finns i [Adobe IMS-användare](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=sv-SE).


## Kan du godkänna flera resurser samtidigt i en mapp? {#approve-multiple-assets-in-folder}

Ja, du kan godkänna flera resurser i en mapp samtidigt.

Utför följande steg för att godkänna flera resurser samtidigt i [!DNL Experience Manager Assets Admin view]:

1. Markera resurserna och klicka på **[!UICONTROL Properties]**.
1. Bläddra nedåt till **[!UICONTROL Basic]** på fliken **[!UICONTROL Review Status]**.
1. Ändra granskningsstatusen till **[!UICONTROL Approved]**.
1. Klicka på **[!UICONTROL Save & Close]**.

På samma sätt kan du godkänna flera resurser samtidigt i en mapp i Assets-vyn:

1. Markera resurserna och klicka på **[!UICONTROL Bulk Metadata Edit]**.

1. Välj **[!UICONTROL Approved]** i fältet **[!UICONTROL Status]** som är tillgängligt i avsnittet [!UICONTROL Properties] i den högra rutan.

1. Klicka på **[!UICONTROL Save]**.


## Hur säkrar jag materialleveransen och söker efter Dynamic Media OpenAPI:er? {#secure-asset-delivery}

Med central resursstyrning i Experience Manager kan DAM-administratörer och varumärkesansvariga hantera åtkomst till resurser. De kan begränsa åtkomsten genom att konfigurera roller eller genom att ställa in aktiverings- och inaktiveringstid för godkända mediefiler på redigeringssidan, särskilt på AEM as a Cloud Service författarinstans.

Slutanvändare som söker efter eller använder leverans-URL:er kan få åtkomst till begränsade resurser när auktoriseringsprocessen har slutförts.

Mer information finns i [Begränsa åtkomst till resurser i Experience Manager](restrict-assets-delivery.md#authoring).


## Hur får du behörighet att redigera godkännandestatusen för en resurs? {#permissions-edit-approval-status}

Som DAM-användare kanske du inte har behörighet att [godkänna resurser](approve-assets.md#approve-assets). Om du vill ha behörighet att redigera godkännandestatusen för en resurs kan administratören redigera standardmetadataschemat eller något annat metadataschema som används i resursmappen och ge redigeringsbehörighet till fältet **[!UICONTROL Review Status]**. Mer information finns i [Så här inaktiverar du redigering för fältet Granskningsstatus](approve-assets.md#configuration).


## Vilken filstorlek stöds för videoklipp? {#supported-file-formats-videos}

Dynamic Media med OpenAPI-funktioner har stöd för videor med lång form. Videorna har stöd för upp till 50 GB och 2 timmar.


## Hur skiljer sig Dynamic Media med OpenAPI-funktioner från Dynamic Media? {#dynamic-media-and-dynamic-media-with-openapi-differences}

Dynamic Media med OpenAPI-funktioner och Dynamic Media representerar distinkta lösningar som alla har specialfunktioner för leverans. Det är av största vikt att du noggrant granskar dina specifika krav för att fastställa den lämpligaste lösningen som passar dina behov.

Allmän vägledning från Adobe är att utnyttja Dynamic Media med OpenAPI-stacken för alla integreringsanvändningsfall (program från första eller tredje part). Om det redan finns en integrering med Dynamic Media-stacken bör du inte ändra den eftersom URL:er för OpenAPI-stacken är olika i strukturen. Använd OpenAPI-stacken endast för nya integreringsfall. Om ditt användningsfall kräver avancerade modifieringar som inte är tillgängliga med OpenAPI-stacken bör du undvika OpenAPI-stacken tills Adobe överbryggar luckan. Även för grundläggande inbyggd leverans från AEM Assets Cloud Services kan OpenAPI-stacken utvärderas så länge ditt användningsfall täcks av modifieringarna som finns i OpenAPI-stacken. Sammanfattningsvis kan Dynamic Media och Dynamic Media med OpenAPI-stacken finnas samtidigt, beroende på vilken typ av användning du har.

Nedan följer några av de viktigaste skillnaderna mellan Dynamic Media med OpenAPI-funktioner och Dynamic Media:

| Dynamic Media med OpenAPI-funktioner | Dynamiska medier |
|---|---|
| [Endast tillgängligt med Assets as a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | Finns även i On-Local eller Adobe Managed Services med ytterligare konfigurations- och provisioneringsåtgärder. |
| [Begränsad uppsättning bildmodifierare som stöds, till exempel bredd, höjd, rotering, vänd, kvalitet och format](/help/assets/deliver-assets-apis.md) | En mängd tillgängliga bildmodifierare |
| [Begränsad leverans av resurser baserat på användare, roller, datum och tid](/help/assets/restrict-assets-delivery.md) | Assets som publiceras på Dynamic Media är tillgängliga för alla användare |
| De flesta utvecklare är bekanta med OpenAPI-specifikationer. AEM Assets utbyggbarhet blir mycket enkelt genom att använda [Micro-Front Asset Selector](/help/assets/overview-asset-selector.md). | SOAP-baserade API:er, som blir ett hinder när man utvecklar integrationsanpassningar. |
| Ändringar som görs i godkända resurser i DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i leverans-URL:erna. Med ett kort TTL-värde (Time-to-Live) på 10 minuter konfigurerat för Dynamic Media med OpenAPI-funktioner via CDN blir uppdateringarna synliga i alla redigerings- och publiceringsgränssnitt på mindre än 10 minuter. | Rekommenderad CDN TTL på 10 timmar. Du kan åsidosätta TTL-värdet med åtgärden för cacheogiltigförklaring. |
| Endast godkända mediefiler finns tillgängliga för leverans av mediefiler till applikationer längre fram i kedjan, vilket möjliggör för varumärken som godkänner mediefiler i digitala upplevelser. | Alla uppdateringar av en publicerad resurs i Dynamic Media publiceras automatiskt utan något arbetsflöde för godkännande, vilket inte säkerställer att det finns varumärkesgodkända resurser i digitala upplevelser. |
| Användningsrapporter baserade på antalet levererade resurser. Den här funktionen kommer snart att vara tillgänglig. | Användningsrapporter är inte tillgängliga. Den här funktionen kommer snart att vara tillgänglig. |
| Assets som har markerats som Förfallen på Assets as a Cloud Service-databasen är inte längre tillgängliga för program längre fram i kedjan. | Inga interna tillgångar förfaller. En resurs förblir offentlig tills den tas bort från AEM as a Cloud Service-databasen. |
| Stöder inte förinställningar för bilder och videomaterial för smart beskärning. | Stöder bildförinställningar och videofunktioner för smart beskärning. |
| Dynamiska videokodar som säkerställer att bästa kodning hanteras baserat på indatavideon. Ingen inställning krävs för inbyggd videoleverans. | Standard 3 kodar oberoende av videoingång (kan påverka videoleveransprestanda). Du måste ställa in olika kodningar manuellt för olika videobithastigheter. |
| Det är svårt att gissa vilken resurs-UID-baserade URL:er är (gör att URL-adresser kan döljas), men SEO-optimering används. | URL-döljning är bara tillgänglig för URL-frågeparametrar. Assets-id:n (resursnamn) i URL:er är identifierbara. |


## Hur tillgodoser Dynamic Media med OpenAPI-funktioner begränsningarna i funktionen Connected Assets? {#dynamic-media-openapi-addresses-connected-assets-limitations}

Tabellen nedan visar de viktigaste skillnaderna mellan de två lösningarna:

| Dynamic Media med OpenAPI-funktioner | Uppkopplad Assets |
|---|---|
| Assets på fjärrdistributionen av DAM är tillgängligt på AEM as a Cloud Service. | Assets på fjärrdistributionen av DAM kan vara tillgängligt på AEM as a Cloud Service eller Adobe Managed Services. |
| Resursbinärfiler kopieras inte när resurser på en fjärr-DAM-distribution är tillgängliga i en AEM Sites-instans. | Resursbinärfiler kopieras när resurser på en fjärr-DAM-distribution är tillgängliga på en AEM Sites-instans. |
| Stöd för alla format som stöds av AEM Assets. | Inget stöd för videor. |
| Du kan använda Dynamic Media på den lokala platsdistributionen när du hämtar resurser från fjärr-DAM-distribution. | Dynamiska medier på lokala platser är skrivskyddade. |
| Inga begränsningar för antalet AEM Sites-instanser som är anslutna till en fjärr-DAM-distribution. Du kan [begränsa åtkomsten till resurser på platsinstansen genom att konfigurera roller](/help/assets/restrict-assets-delivery.md) för godkända resurser på fjärr-DAM. | Begränsning för att ansluta högst fyra AEM Sites-instanser till fjärr-DAM-distributionen. Ökat antal kräver ytterligare testning. |
| Både resursväljaren och Dynamic Media med OpenAPI-funktioner kan utökas för att tillåta anpassade integreringar. | Anslutna Assets-API:er kan inte utökas för att tillåta anpassade integreringar. |
| Alla ändringar som görs i godkända resurser som är tillgängliga vid fjärdistributionen av DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i Sites-instansen inom ett kort TTL-värde på 10 minuter. | Resursuppdateringar för fjärrdistribution av DAM hanteras automatiskt via livscykelhändelser, men tar mycket mer tid jämfört med Dynamic Media med OpenAPI-funktioner. |
| Resursmetadata på fjärr-DAM är även tillgängliga på AEM Sites-instanser. | Resursmetadata på fjärr-DAM är inte tillgängliga på AEM Sites-instansen. |

## Vissa modifierare är markerade som begränsad tillgänglighet. Hur kan jag börja använda dem? {#use-limited-availability-modifiers}

Så här aktiverar du produktionsanvändning av modifierare i begränsad tillgänglighet för ditt konto:

1. [Skapa ett Adobe-supportärende med Admin Console](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html).

1. Ange följande i Adobe Support-ärendet:

   * IMS-organisation

   * Lista över modifierare som ska aktiveras
