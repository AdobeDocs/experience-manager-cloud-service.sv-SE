---
title: Funktioner för pågående webbplatser för Edge Delivery Services
description: Ta reda på vilka AEM Sites-funktioner och användningsexempel som är ett pågående arbete och upptäck alternativa lösningar när du använder Edge Delivery Services.
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: 92da26452438f2b56cdec1aecc76587d4982f00e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Funktioner för pågående webbplatser för Edge Delivery Services {#wip-sites-features}

Ta reda på vilka AEM Sites-funktioner och användningsexempel som är ett pågående arbete och upptäck alternativa lösningar när du använder Edge Delivery Services.

>[!TIP]
>
>Det pågående arbetet innebär inte slutet på vägen. Om du behöver en funktion eller ett användningsfall som anges som pågående arbete i det här dokumentet kan du kontakta din Adobe-representant. Ni och Adobe kan samarbeta för att förstå era särskilda behov och hitta alternativa lösningar.

## Funktioner för pågående arbete {#wip-features}

De flesta webbplatsfunktionerna är tillgängliga när du använder Edge Delivery Services med AEM Sites. Nästan alla åtgärder som är tillgängliga i [Platskonsolen](/help/sites-cloud/authoring/sites-console/introduction.md) gäller till exempel för Edge Delivery Services.

Vissa funktioner är dock under arbete. Pågående arbete-funktioner är funktioner i webbplatskonsolen som inte är tillgängliga för Edge Delivery Services med AEM Sites eller som bara är delvis tillgängliga. Av den anledningen kan PIA-funktioner presenteras på ett annat sätt än deras motsvarigheter på Sites eller så kan det finnas alternativa lösningar för användningsfallet.

I följande lista visas sådana PIA-funktioner och alternativa lösningar. Om ditt projekt kräver en PIA-funktion kan du titta närmare på alternativen nedan och kontakta Adobe för att få en förståelse för hur du använder dem.

| Webbplatsfunktion | Status för Edge | Anteckningar | Edge Documentation |
|---|---|---|---|
| [Sidarv](/help/sites-cloud/administering/msm-and-translation.md) | Tillgänglig |  | [Innehållsarv i den universella redigeraren](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Komponentarv](/help/sites-cloud/administering/msm-and-translation.md) | Delvis tillgänglig | Komponenter ärver innehåll, men arv kan bara återställas på sidnivå | [Innehållsarv i den universella redigeraren](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Språkkopia](/help/sites-cloud/administering/translation/overview.md) | Delvis tillgänglig | Komponenter ärver innehåll, men arv kan bara återställas på sidnivå | [Innehållsarv i den universella redigeraren](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Hantering av flera webbplatser](/help/sites-cloud/administering/msm/overview.md) | Delvis tillgänglig | Komponenter ärver innehåll, men arv kan bara återställas på sidnivå | [Innehållsarv i den universella redigeraren](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Startar](/help/sites-cloud/authoring/launches/overview.md) | Delvis tillgänglig | Komponenter ärver innehåll, men arv kan bara återställas på sidnivå | [Innehållsarv i den universella redigeraren](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Sidmallar](/help/sites-cloud/authoring/page-editor/templates.md) | Delvis tillgänglig | Sidor som skapas från mallar är oberoende kopior av den ursprungliga mallen. | [Använda sidmallar med den universella redigeraren](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Kontextnav och mål](/help/sites-cloud/authoring/personalization/overview.md) | Inte tillgängligt |  |  |
| [Timewarp](/help/sites-cloud/authoring/launches/preview.md) | Inte tillgängligt |  |  |
| [Associerat innehåll](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | Inte tillgängligt |  |  |
| [Experience Fragments](/help/sites-cloud/authoring/fragments/experience-fragments.md) | Alternativ | Skapa en sida och använda en fragmentkomponent |  |

## Användningsexempel - pågående arbete {#wip-use-cases}

Eftersom Edge Delivery Servicens bygger på en helt ny och modern teknologi är följande användningsområden i AEM Sites ännu inte helt täckta och håller på att utvecklas. Om ditt projekt kräver en PIA-lösning kan du kontakta Adobe för att få en förståelse för projektets behov.

| Användningsfall för webbplatser | Information |
|---|---|
| SSI (Server-side logic) för återgivning av sidor | Använda AEM runtime som programserver |
| Dynamiska sidor | SSI eller någon dynamisk inkluderingsteknik |
| Användarhantering | Använda AEM som IdP |
| Autentisering | Använda AEM för säkert innehåll |
| Innehållsbehörighet | AEM som säkert extranät |
