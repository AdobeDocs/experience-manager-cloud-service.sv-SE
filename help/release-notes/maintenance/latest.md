---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 67b9a5f73f1f8c599e902a0ac0d8efbc614c7f75
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva X {#X}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva X, som offentliggjordes den 1 april 2025. Den tidigare underhållsutgåvan släpptes 19823.

Funktionsaktiveringen i 2025.4.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-X}

FORMS-19068: Stöd har lagts till för AEP Connector-åtgärder i Forms Manager-API:er för att förbättra integreringsfunktionerna för formulärdata.

FORMS-18513: Implementerat stöd för dataträdsomvandling i AEP Connector för att förbättra guidefunktioner och datahanteringsfunktioner.

FORMS-18432: Implementerad formulärspecifik (regex-baserad) konfiguration av förifyllning på klientsidan för att möjliggöra selektiv förifyllning utan ändringar på OSGI-nivå.

FORMS-17551: Stöd för DoR (Document of Record) för SharePoint listintegreringar.

### Åtgärdade problem {#fixed-issues-X}

FORMS-19028: Förifyllningsfunktionen på klientsidan bryter hanteringen av formulärhändelser, vilket förhindrar Value commit- och DOMContentLoaded-händelser från att aktiveras korrekt vid formulärinläsning.

FORMS-18360: Förbättrad SharePoint listomfattningshantering för gruppwebbplatser i Forms Document Management för att förbättra dataorganisationen och åtkomstkontrollen.

FORMS-18325: Adobe Experience Platform (AEP) Cloud-konfiguration har lagts till för att förbättra integrationen av formulärdata och bearbetningskapaciteten.

FORMS-18213: Implementerad funktion för att dölja/exkludera inaktiverade fält från DoR (Document of Record) för att förbättra dokumentets tydlighet och användarupplevelsen.

FORMS-18189: Anpassad funktionshantering som förhindrar felloggning för tomma klientbibliotek och förbättrar felvisningen i användargränssnittet.

FORMS-18426: SharePoint listsökningsfunktion misslyckas när listnamn innehåller specialtecken (till exempel &#39;-&#39;), vilket påverkar formulärintegrationen med SharePoint-listor.

FORMS-18375: Formulär som baseras på Foundation-komponenter markerar felaktigt reaptcha-konfigurationer från mappen `conf/global` när ingen specifik konfigurationsbehållare har valts.

FORMS-18304: PDF/A-1b-dokument som godkänts i Acrobat och LiveCycle ES4 flaggas felaktigt som icke-kompatibla i AEM 6.5 Forms på grund av enhetsberoende färgfel.

FORMS-18271: Forms Theme Editor visar olokaliserade felmeddelanden som påverkar användarupplevelsen när det gäller formulärkonfiguration och temaanpassning.

FORMS-18068: Fet textåtergivningsproblem i DoR (Document of Record) för alternativknappar och kryssrutegrupper med hjälp av RTF-fält.

FORMS-7016: Tangentbordsfokusordningen i formulärredigeraren följer inte logisk navigering.

FORMS-6950: Nödvändiga ARIA-roller och attribut har lagts till i komponenter för filsystemets navigatortreeview för att förbättra skärmläsarens tillgänglighet och uppfylla WCAG 4.1.2-standarden Namn, roll, värde (nivå A).

### Kända fel {#known-issues-X}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-X}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-X}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar X-identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-X}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
