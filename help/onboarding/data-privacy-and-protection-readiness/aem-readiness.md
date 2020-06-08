---
title: Dataskydd och dataintegritet - Adobe Experience Manager som en molntjänst
description: 'Lär dig mer om Adobe Experience Manager som molntjänst för de olika dataskydds- och datasekretessreglerna. inklusive EU:s allmänna dataskyddsförordning (GDPR), Kaliforniens konsumentsekretesslag och hur man ska följa detta när man implementerar en ny AEM som ett molntjänstprojekt. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Adobe Experience Manager som molntjänst för beredskap för dataskydd och sekretess {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Innehållet i detta dokument utgör inte juridisk rådgivning och är inte avsett som ersättning för juridisk rådgivning.
>
>Kontakta företagets juridiska avdelning för råd angående dataskydd och dataintegritet.

>[!NOTE]
>
>Mer information om Adobes svar på sekretessfrågor och vad detta innebär för dig som Adobe-kund finns i [Adobes Sekretesscenter](https://www.adobe.com/privacy.html).

Adobe tillhandahåller dokumentation och procedurer (med API:er när sådana finns) för kundsekretessadministratören eller AEM-administratören för att hantera förfrågningar om dataskydd och datasekretess och hjälpa våra kunder att följa dessa regler. De dokumenterade procedurerna gör det möjligt för kunderna att utföra förfrågningar manuellt eller genom att anropa API:er, om sådana finns, från en extern portal eller tjänst.

>[!CAUTION]
>
>Informationen som beskrivs här är begränsad till Adobe Experience Manager som en molntjänst.
>
>Data från en annan Adobe On-demand-tjänst, tillsammans med eventuella relaterade sekretessförfrågningar, kräver åtgärder för den tjänsten.
>
>Mer information finns i [Adobes Sekretesscenter](https://www.adobe.com/privacy.html).

## Introduktion {#introduction}

Instanser av Adobe Experience Manager som en molntjänst, och de program som körs på dem, ägs och hanteras av våra kunder.

Följaktligen är dataskyddsbestämmelser, som GDPR, CCPA med flera, i huvudsak kundernas ansvar.

Som en mycket kort introduktion innehåller reglerna för datasekretess och skydd nya regler som ska följas av rollerna för:

* Affärsenheter (CCPA) och/eller datakontroller (GDPR)

* Tjänsteleverantörer (CCPA) och/eller dataprocessorer (GDPR)

De viktigaste bestämmelserna i sådana förordningar är

1. Utökad definition av personuppgifter som ska omfatta alla unika ID:n. som direkt och indirekt identifierbara data.

2. Förbättrade krav på samtycke.

3. Ökat fokus på raderingsrättigheter (dataradering).

4. Avanmäl dig från försäljning av data.

För Adobe Experience Manager som molntjänst:

* Förekomsterna och tillämpningarna som körs på dem ägs och hanteras av kunden.

   * Detta innebär att kunden i praktiken hanterar de reglerande rollerna, bland annat affärsenheter och tjänsteleverantör, datakontroller och dataprocessor.

   * Integritetstjänsten för Adobe Experience Platform kommer inte att ingå i arbetsflödet för AEM, vilket visas i bilden nedan.

* AEM innehåller dokumentation och förfaranden för kundens integritetsadministratör och/eller AEM-administratör för att verkställa förfrågningar om sekretessbestämmelser. antingen manuellt eller via API:er, om sådana finns.

* Ingen ny tjänst eller gränssnitt har lagts till.

   * Istället dokumenteras procedurer och API:er för användning av kundgränssnitt/portaler som hanterar förfrågningar om sekretessbestämmelser.

* AEM kommer inte att innehålla några färdiga verktyg som stöder arbetsflödet för sekretessförfrågningar.

   * Adobe kommer att tillhandahålla dokumentation och procedurer för kundens sekretessadministratör och/eller AEM-administratör, vilket gör att de manuellt kan utföra förfrågningar relaterade till sekretessreglerna.

Adobe tillhandahåller procedurer för hantering av sekretessförfrågningar relaterade till åtkomst, borttagning och avanmälan för Adobe Experience Manager som en molntjänst. I vissa fall finns det API:er som kan anropas från en kundutvecklad portal eller skript som kan hjälpa till med automatisering.

Följande diagram visar hur ett arbetsflöde för sekretesspolicy kan se ut (illustreras med Adobe Experience Manager 6.5):

![Dataskydd och integritet](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager som molntjänst och regelberedskap {#aem-as-a-cloud-service-and-regulatory-readiness}

Se avsnitten nedan för dokumentation av gällande bestämmelser om produktområden för AEM som en molntjänst.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager som en molntjänstintegrering med Adobe Target och Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Dessa integreringar med Adobe Experience Manager som molntjänst är anpassade för dataskydd och sekretess (t.ex. GDPR). Inga personuppgifter från Adobe Target eller Adobe Analytics lagras i AEM i relation till integreringarna.
Mer information finns i:

* [Adobe Target - Integritetsöversikt](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Arbetsflöde för dataintegritet i Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
