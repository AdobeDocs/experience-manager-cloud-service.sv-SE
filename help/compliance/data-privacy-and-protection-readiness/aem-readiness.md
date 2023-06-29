---
title: Dataskydd och dataintegritet - Adobe Experience Manager as a Cloud Service beredskap
description: Läs mer om Adobe Experience Manager as a Cloud Service stöd för de olika dataskydds- och datasekretessreglerna och hur man gör när man implementerar ett nytt AEM as a Cloud Service projekt. Dessa förordningar omfattar EU:s allmänna dataskyddsförordning (GDPR), Kaliforniens konsumentsekretesslag.
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 1473c1ffccc87cb3a0033750ee26d53baf62872f
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service beredskap för dataskydd och dataintegritet {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Innehållet i detta dokument utgör inte juridisk rådgivning och är inte avsett som ersättning för juridisk rådgivning.
>
>Kontakta företagets juridiska avdelning för råd om dataskydd och dataintegritet.

>[!NOTE]
>
>Mer information om Adobe svar på sekretessfrågor och vad dessa svar innebär för dig som Adobe-kund finns i [Adobe Sekretesscenter](https://www.adobe.com/privacy.html).

För att hjälpa Adobe-kunder att följa dessa bestämmelser tillhandahåller Adobe dokumentation och procedurer (med API:er när sådana finns) för kundintegritetsadministratörer och AEM:

* Dokumentationen hjälper administratörer att hantera frågor om dataskydd och datasekretess.
* De dokumenterade procedurerna gör att kunderna kan köra förfrågningar manuellt eller göra API-anrop, om tillgängligt, från en extern portal eller tjänst.

>[!CAUTION]
>
>Informationen som beskrivs här är begränsad till Adobe Experience Manager as a Cloud Service.
>
>Data från en annan Adobe On-demand-tjänst, tillsammans med eventuella relaterade sekretessförfrågningar, kräver att åtgärder vidtas för den tjänsten.
>
>Mer information finns i [Adobe Sekretesscenter](https://www.adobe.com/privacy.html).

## Introduktion {#introduction}

Förekomster av Adobe Experience Manager as a Cloud Service, och de applikationer som körs på dem, ägs och drivs av Adobe.

Följaktligen är dataskyddsbestämmelser, som GDPR, CCPA med flera, i huvudsak kundernas ansvar.

Som en kort introduktion innehåller reglerna för datasekretess och skydd nya regler som ska följas av rollerna för:

* Affärsenheter (CCPA) och/eller datakontroller (GDPR)

* Tjänsteleverantörer (CCPA) och/eller dataprocessorer (GDPR)

De viktigaste bestämmelserna i sådana förordningar är

1. Utökad definition av personuppgifter som ska omfatta alla unika ID:n. som direkt och indirekt identifierbara data.

2. Förbättrade krav på samtycke.

3. Ökat fokus på raderingsrättigheter (dataradering).

4. Avanmäl dig från försäljning av data.

För Adobe Experience Manager as a Cloud Service:

* Förekomsterna och tillämpningarna som körs på dem ägs och hanteras av kunden.

   * Ägarskapet innebär att kunden effektivt hanterar de reglerande rollerna, bland annat affärsenheter och tjänsteleverantör, datakontroller och dataprocessor.

   * Adobe Experience Platform Privacy Service ingår inte i arbetsflödet för AEM, vilket visas i diagrammet nedan.

* AEM innehåller dokumentation och förfaranden för att kundens integritetsadministratör och/eller AEM ska kunna genomföra förfrågningar om integritetsreglering. antingen manuellt eller via API:er, om sådana finns.

* Ingen ny tjänst eller gränssnitt har lagts till.

   * Istället dokumenteras procedurer och API:er för användning av kundgränssnitt/portaler som hanterar förfrågningar om sekretessbestämmelser.

* AEM innehåller inga färdiga verktyg som stöder arbetsflödet för sekretessförfrågningar.

   * Adobe tillhandahåller dokumentation och procedurer för kundens sekretessadministratör, AEM administratör eller båda, så att de manuellt kan köra förfrågningar relaterade till sekretessreglerna.

Adobe tillhandahåller rutiner för hantering av sekretessförfrågningar som rör åtkomst, borttagning och avanmälan för Adobe Experience Manager as a Cloud Service. I vissa fall finns det API:er som kan anropas från en kundutvecklad portal eller skript som kan hjälpa till med automatisering.

Följande diagram visar hur ett arbetsflöde för sekretesspolicy kan se ut (illustreras med Adobe Experience Manager 6.5):

![Dataskydd och integritet](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service och beredskap för regelefterlevnad {#aem-as-a-cloud-service-and-regulatory-readiness}

Se avsnitten nedan för dokumentation om produktområden av AEM as a Cloud Service.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

Se [AEM Foundation Ready for Data Protection and Data Privacy Regulations](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

Se [AEM Sites beredskap för dataskydd och dataintegritet](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Cloud Service-integrering med Adobe Target och Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Integreringar av Adobe Experience Manager as a Cloud Service med Adobe Target och Adobe Analytics implementeras med tjänster som är klara för dataskydd och sekretess (till exempel GDPR). Inga personuppgifter från Adobe Target eller Adobe Analytics lagras i AEM för integreringarna.
Mer information finns i:

* [Adobe Target - sekretessöversikt](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html)

* [Adobe Analytics arbetsflöde för datasekretess](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)
