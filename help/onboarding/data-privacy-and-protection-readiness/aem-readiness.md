---
title: Dataskydd och dataintegritet - Adobe Experience Manager som Cloud Service-beredskap
description: Läs mer om Adobe Experience Manager som stöd för Cloud Service av de olika dataskydds- och dataintegritetsreglerna. bland annat EU:s allmänna dataskyddsförordning (GDPR), Kaliforniens konsumentintegritetslag och hur man ska följa detta när man genomför en ny AEM som ett Cloud Service-projekt.
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service Readiness for Data Protection and Data Privacy Regulations {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Innehållet i detta dokument utgör inte juridisk rådgivning och är inte avsett som ersättning för juridisk rådgivning.
>
>Kontakta företagets juridiska avdelning för råd angående dataskydd och dataintegritet.

>[!NOTE]
>
>Mer information om Adobe svar på sekretessfrågor och vad detta innebär för dig som Adobe-kund finns i [Adobe Privacy Center](https://www.adobe.com/privacy.html).

Adobe tillhandahåller dokumentation och procedurer (med API:er när sådana finns) för kundsekretessadministratören eller AEM administratör för att hantera förfrågningar om dataskydd och dataintegritet och hjälpa våra kunder att följa dessa regler. De dokumenterade procedurerna gör det möjligt för kunderna att utföra förfrågningar manuellt eller genom att anropa API:er, om sådana finns, från en extern portal eller tjänst.

>[!CAUTION]
>
>Informationen som beskrivs här är begränsad till Adobe Experience Manager som Cloud Service.
>
>Data från en annan Adobe On-demand-tjänst, tillsammans med eventuella relaterade sekretessförfrågningar, kommer att kräva åtgärder för den tjänsten.
>
>Mer information finns i [Adobe Privacy Center](https://www.adobe.com/privacy.html).

## Introduktion {#introduction}

Instanser av Adobe Experience Manager som Cloud Service, och de program som körs på dem, ägs och hanteras av våra kunder.

Följaktligen är dataskyddsbestämmelser, som GDPR, CCPA med flera, i huvudsak kundernas ansvar.

Som en mycket kort introduktion innehåller reglerna för datasekretess och skydd nya regler som ska följas av rollerna för:

* Affärsenheter (CCPA) och/eller datakontroller (GDPR)

* Tjänsteleverantörer (CCPA) och/eller dataprocessorer (GDPR)

De viktigaste bestämmelserna i sådana förordningar är

1. Utökad definition av personuppgifter som ska omfatta alla unika ID:n. som direkt och indirekt identifierbara data.

2. Förbättrade krav på samtycke.

3. Ökat fokus på raderingsrättigheter (dataradering).

4. Avanmäl dig från försäljning av data.

För Adobe Experience Manager som Cloud Service:

* Förekomsterna och tillämpningarna som körs på dem ägs och hanteras av kunden.

   * Detta innebär att kunden i praktiken hanterar de reglerande rollerna, bland annat affärsenheter och tjänsteleverantör, datakontroller och dataprocessor.

   * Adobe Experience Platform Privacy Service kommer inte att ingå i arbetsflödet för AEM, vilket visas i diagrammet nedan.

* AEM innehåller dokumentation och förfaranden för att kundens integritetsadministratör och/eller AEM ska kunna genomföra förfrågningar om integritetsreglering. antingen manuellt eller via API:er, om sådana finns.

* Ingen ny tjänst eller gränssnitt har lagts till.

   * Istället dokumenteras procedurer och API:er för användning av kundgränssnitt/portaler som hanterar förfrågningar om sekretessbestämmelser.

* AEM kommer inte att innehålla några färdiga verktyg som stöder arbetsflödet för sekretessförfrågningar.

   * Adobe ska tillhandahålla dokumentation och procedurer för kundens integritetsadministratör och/eller AEM, så att de manuellt kan utföra förfrågningar som rör sekretessbestämmelser.

Adobe tillhandahåller rutiner för att hantera sekretessförfrågningar som rör åtkomst, borttagning och avanmälan för Adobe Experience Manager som Cloud Service. I vissa fall finns det API:er som kan anropas från en kundutvecklad portal eller skript som kan hjälpa till med automatisering.

Följande diagram visar hur ett arbetsflöde för sekretesspolicy kan se ut (illustreras med Adobe Experience Manager 6.5):

![Dataskydd och integritet](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager som Cloud Service och regelberedskap {#aem-as-a-cloud-service-and-regulatory-readiness}

Se avsnitten nedan för dokumentation av AEM produktområden som en Cloud Service.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

Se [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

Se [AEM Sites beredskap för dataskydd och dataintegritet.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager som Cloud Service Integration med Adobe Target &amp; Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Dessa Adobe Experience Manager som Cloud Service-integreringar är med tjänster som är klara för dataskydd och sekretess (t.ex. GDPR). Inga personuppgifter från Adobe Target eller Adobe Analytics lagras i AEM för integreringarna.
Mer information finns i:

* [Adobe Target - sekretessöversikt](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics arbetsflöde för datasekretess](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)
