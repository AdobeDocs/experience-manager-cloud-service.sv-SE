---
title: Komma igång med Forms på AEM Edge Delivery Services
description: Lär dig hur du skapar och levererar högpresterande formulär på Adobe Experience Manager Edge Delivery Services, med betoning på utvecklingsstrategin Universal Editor.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Komma igång med Forms på AEM Edge Delivery Services

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">pre-release channel</a>. </span>
-->

Med Adobe Experience Manager (AEM) Edge Delivery Services (EDS) kan du leverera blixtsnabba, skalbara webbupplevelser i toppklass. Den här guiden förklarar **hur du skapar och publicerar formulär för dessa upplevelser** - med en tydlig rekommendationshierarki:

1. **Universell redigerare (UE) - Bästa val för de flesta team**
2. **Dokumentbaserad redigering (dokument/ark) - Perfekt för snabba, enkla formulär**
3. **Dokumentredigering (DA) - Används för att bädda in formulär på DA-skapade sidor**

När allt är klart kan du välja rätt redigeringsmetod, förstå överföringsalternativen och följa nästa steg mot produktionsklara formulär.



## Välja en redigeringsmetod

| Team och krav | Rekommenderad metod | Varför |
|--------------------|--------------------|-----|
| Marknadsförare/formgivare behöver visuell kontroll, villkorsstyrd logik eller AEM-integreringar | **Universell redigerare** | Dra-och-släpp, avancerade regler, skicka till FSS eller AEM Publish |
| Innehållsförfattare som redan arbetar i Word/Google Docs/Sheets; enkel datainhämtning till kalkylblad/e-post | **Dokumentbaserad redigering** | Välbekanta verktyg, snabbaste vägen för grundläggande formulär |
| Webbplatssidor inbyggda i **Dokumentredigering (DA)** | **Bädda in** ett UE- eller dokumentbaserat formulär på DA-sidan | DA skapar inte formulär själva |


## Redigeringsmetoder i detalj

### Universal Editor

Universell redigerare är ett visuellt dra-och-släpp-verktyg för marknadsförare och designers som kombinerar snabbhet med kraftfulla verktyg i företagsklass:

- WYSIWYG redigering i realtid och förhandsgranskning av enheter.
- Avancerade regler och gränssnitt för validering - ingen kod behövs.
- Direkt integrering med AEM resurser, arbetsflöden och FDM (Form Data Model).
- Smidig leverans till utvecklare för anpassade komponenter i vanilj JS/CSS.
- Flexibla inskickningsmål: börja enkelt med **Forms Submission Service (FSS)** eller växla till **AEM Publish submit actions** när behoven växer.

> **Rekommendation**: Starta alla nya formulärprojekt med Universal Editor, såvida inte ditt team har dokumentcentrerat till 100 % och formuläret är mycket grundläggande.


### Dokumentbaserad redigering (dokument/ark)

Dokumentbaserad redigering passar bäst för att skapa enkla, komplexa formulär med välbekanta verktyg som Microsoft Word, Google Docs och Google Sheets. Den här metoden är idealisk för team som behöver ett snabbt och enkelt sätt att skapa formulär.

- Definiera formulärfält i en tabell (dokument) eller som rader (ark).
- Stöder grundläggande fältvalidering och Google reCAPTCHA för skräppostskydd.
- Blankettinlämning hanteras enbart via Forms inskickningstjänst.
- Direkt publicering - alla ändringar som görs i källdokumentet återspeglas direkt på webbplatsen utan att något driftsättningsflöde krävs.


### Bädda in Forms i Document Authoring (DA)

Document Authoring (DA) är utformat för att skapa strukturerat sidinnehåll och stöder inte skapande av egna formulär. Så här lägger du till ett formulär på en DA-skapad sida:

1. Skapa formuläret med **Universal Editor** (rekommenderas) eller dokumentbaserad redigering.
2. Publicera formuläret för att generera en unik URL (till exempel `/forms/contact-us`).
3. Infoga ett **Bädda in formulär**-block på din DA-sida och ange det publicerade formulärets URL.

<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## Nästa steg

1. **Börja med Universal Editor:** Se [Guiden Komma igång för Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) när du vill börja skapa formulär.
2. **Konfigurera formuläröverföring:** Välj och ange den metod du vill använda för att skicka formulär. Se [Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) eller AEM Publish submit actions för konfigurationsinstruktioner.
3. **Använd bästa praxis:** Granska [god praxis för formulärdesign](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md) för att säkerställa tillgänglighet och prestanda.
4. **Använd dokumentbaserad redigering:** Om du vill skapa formulär med Microsoft Excel eller Google Sheets följer du [dokumentbaserad redigering](/help/edge/docs/forms/tutorial.md).
5. **Bädda in Forms i dokumentredigering:** Om du skapar sidor i dokumentredigering kan du läsa [DA-självstudiekursen](https://www.aem.live/developer/da-tutorial) för instruktioner om hur du bäddar in publicerade formulär.

> **Du kan nu skapa ditt första högpresterande formulär med AEM Edge Delivery Services.**