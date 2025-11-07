---
title: Assets Ultimate
description: Läs mer om viktiga aspekter av Assets Ultimate, t.ex. viktiga fördelar, användartyper och behörigheter.
feature: Asset Management
role: User, Admin
exl-id: 3ae96cd2-e0ac-43a5-a0bf-bebb1a028b10
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# [!DNL Assets] as a Cloud Service Ultimate {#assets-ultimate-user-types-privileges}

![Assets as a Cloud Service Ultimate](/help/assets/assets/aem-assets-ultimate-banner.png)

Assets as a Cloud Service Ultimate har avancerade DAM-funktioner. AEM Assets Ultimate har tagits fram för att hantera komplexa innehållsförsörjningskedjor och säkerställa att allt innehåll fungerar bra i alla kanaler.

## Varför Assets Ultimate? {#why-ultimate-existing-new-users}

Assets as a Cloud Service Ultimate har flera viktiga fördelar som hjälper er att effektivt hantera era behov av mediefiler, till exempel:

* Större flexibilitet med fler användartyper och behörigheter som är kopplade till dessa användartyper, som medarbetare, Power-användare och Limited-användare.

* Smidig mediedistribution med Content Hub.

* Skapa och mixa med AI-baserat material med Adobe Express och Firefly.

* Smidigare start- och uppgraderingsupplevelser för nya och befintliga användare.

## Viktiga funktioner i Assets Ultimate {#capabilities-assets-ultimate}

Med Assets as a Cloud Service Ultimate kan du utföra olika viktiga åtgärder för hantering av digitala resurser, som:

* **Resurshantering och bibliotekstjänster** &#x200B;: Verktyg som gör det möjligt för användare att importera, lagra, katalogisera, styra, hantera och styra ett varumärkes digitala resurser i ett centralt arkiv

* **Sök, identifiera och Collaboration**: Verktyg som gör att användare kan bläddra bland, upptäcka, dela och samarbeta med resurser som de behöver för att skapa avancerade kundupplevelser.

* **Säkerhet och Rights Management**: Verktyg för att hantera åtkomst, behörigheter, rättigheter och säkerhet för att säkerställa regelefterlevnad, konsekvens och varumärkesintegritet.

* **Creative Cloud Connections**: Verktyg som gör att marknadsförings- och kreativa team kan samarbeta med enklare åtkomst, kommentarer, granskningar och anteckningar för att uppdatera eller slutföra digitala resurser.

* **Experience Cloud Connections**: Verktyg som stöder inbyggd åtkomst till digitala resurser från andra Experience Cloud-program och -tjänster.

* **Distribution Portal Experience (Content Hub)**: Verktyg för att utöka åtkomsten till ett varumärkes godkända digitala resurser till externa intressenter för att säkerställa enhetlig användning och varumärkesexponering.

* **Integrationer**: integreringar med andra program från Adobe och andra program än Adobe.

* **Dynamiska media (tillägg)**: Verktyg för att omvandla och leverera bilder, videor och annat framväxande innehåll för interaktiva multimedieupplevelser för alla typer av enheter i stor skala.

* **Anpassning**: Verktyg för att anpassa DAM-användargränssnittets åtkomst till API:er för vidare utveckling.

* **Anpassad utbyggbarhet**: Omfattande flexibilitet genom den robusta API-först-plattformen, vilket möjliggör smidig integrering och anpassning för att uppfylla den kundkomplexa IT-infrastrukturen.

* **Automatisering av innehåll (tillägg)**: Verktyg för att kombinera arbetshantering och automatisera arbetsflöden för omvandling av digitala resurser för innehållsproduktion i stor skala.

Vilka åtgärder du kan utföra i Assets as a Cloud Service beror på vilken användartyp du har. Mer information finns i [Tillgängliga användartyper](#available-user-types).


## Vilka är tillgängliga användartyper och behörigheter? {#available-user-types}

Assets as a Cloud Service har fyra typer av användare. Varje användartyp har olika behörighetsgrupper. Användartyperna är:

* **Administratör**: Standardadministratörsanvändaren som konfigurerar de andra tre användartyperna i organisationen.

* **Begränsade användare**: Begränsade användare kan komma åt och utnyttja godkända resurser från din organisation via AEM Assets Content Hub-portalen.

* **Medarbetare-användare**: Som medarbetare kan du:

   * Arbeta med material från Experience Manager via integreringar av Assets som är tillgängliga för er organisation i andra Adobe-produkter och program från andra företag än Adobe.

   * Skapa och redigera material med inbyggda Adobe Express och Firefly och använd professionellt designade mallar, märkespaket, Adobe Stock-material med mera.

   * Få åtkomst till och utnyttja godkänt material från er organisation via AEM Assets Content Hub portal.

* **Kraftfulla användare**: Som Power-användare kan du:

   * Få tillgång till alla AEM Assets-funktioner, inklusive hantering av resurser, metadata och övergripande styrning och automatisering av digitala resurser.

   * Arbeta med resurser från Experience Manager via integreringar med Assets som är tillgängliga för din organisation i andra Adobe- och icke-Adobe-program.

   * Skapa och redigera material med inbyggda Adobe Express och Firefly och använd professionellt designade mallar, märkespaket, Adobe Stock-material med mera.

   * Få åtkomst till och utnyttja godkänt material från er organisation via AEM Assets Content Hub portal.

  ![Assets as a Cloud Service Power user](/help/assets/assets/assets-cs-power-users.png)

I följande tabell sammanfattas tillgängliga AEM Assets-användartyper, vilka behörigheter de har och vilka produktprofiler som krävs för att få dessa behörigheter:


| Användarroll | Begränsade användare | Medarbetare | Kraftfulla användare | Administratörer |
|---------------|----------|----------|-------------------------|---|
| **Funktioner** |  |  |  |  |
| Få tillgång till varumärkesgodkända resurser på Content Hub-portalen | ✓ | ✓ | ✓ | ✓ |
| Skapa och redigera material med inbyggda Adobe Express och Firefly | - | ✓ | ✓ | ✓ |
| Integrering av resurser inom organisationen med Adobe och andra program än Adobe | - | ✓ | ✓ | ✓ |
| Få tillgång till alla AEM Assets-funktioner, som hantering av resurser, metadata och övergripande styrning och automatisering | - | - | ✓ | ✓ |
| Hantera behörigheter för innehåll i AEM Assets redigeringsmiljö | - | - | - | ✓ |
| **Användaren måste finnas i dessa produktprofiler (Admin Console)** |  |  |  |  |
| AEM > Delivery instance > AEM Assets Limited Users | ✓ | ✓ | ✓ | ✓ |
| AEM > Production Author instance > AEM Assets Collaborator Users | - | ✓ | - | - |
| AEM > Production Author instance > AEM Assets Power Users | - | - | ✓ | - |
| AEM > Production Author instance > AEM Administrators | - | - | - | ✓ |
| **Mer information** | Se [Aktivera Content Hub](/help/assets/enable-assets-ultimate.md##enable-assets-ultimate-new-users) | Se [Användare som samarbetar internt](/help/assets/enable-assets-ultimate.md#onboard-collaborator-users) | Se [Onboard Power Users](/help/assets/enable-assets-ultimate.md#onboard-power-users) | - |

Information om hur du kommer igång med Assets Ultimate finns i [Aktivera AEM Assets Ultimate](/help/assets/enable-assets-ultimate.md). Om AEM Assets-användare har frågor om när du kan uppgradera till Assets Ultimate kontaktar du din kontorepresentant för Adobe. Du kan även se [Aktivera Assets Ultimate för befintliga kunder](/help/assets/enable-assets-ultimate.md#enable-assets-ultimate-existing-customers) om du vill ha mer information.

AEM Assets erbjuder också en enklare DAM för kunder som inte har avancerade krav som UI-utökningsmöjligheter, API-driven automatisering och anpassad koddriftsättning. Mer information finns i [AEM Assets Prime](/help/assets/assets-prime.md).
