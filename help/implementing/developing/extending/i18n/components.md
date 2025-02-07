---
title: Internationalisering av komponenter
description: Internationalisera dina komponenter och dialogrutor så att deras gränssnittssträngar kan presenteras på olika språk
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 0276b310-b9a9-44b6-b295-06c51ef17208
source-git-commit: 401685af02c720994d72cd95d36f0cfcdf15d198
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Internationalisering av komponenter{#internationalizing-components}

Internationalisera dina komponenter och dialogrutor så att deras gränssnittssträngar kan presenteras på olika språk. Komponenter som är utformade för internationalisering gör att UI-strängar kan externaliseras, översättas och sedan importeras till databasen. Vid körning avgör användarens språkinställningar eller sidans språkområde vilket språk som visas i användargränssnittet.

![i18n-components-1.png](/help/implementing/developing/extending/assets/i18n-comp1.png)

Använd följande process för att internationalisera dina komponenter och ange användargränssnittet på olika språk:

1. [Implementera dina komponenter med kod som internationaliserar strängar.](/help/implementing/developing/extending/i18n/dev.md) Koden identifierar strängarna som ska översättas och väljer språket som ska användas vid körning.
1. [Skapa ordlistor](/help/implementing/developing/extending/i18n/translator.md#creating-a-dictionary).
1. [Exportera](/help/implementing/developing/extending/i18n/translator.md#exporting-a-dictionary) lexikonet till XLIFF-format, översätt strängarna och importera sedan XLIFF-filerna tillbaka till AEM.
1. Lägg in ordboken i processen för versionshantering av ditt program.

>[!NOTE]
>
>De metoder som beskrivs här för internationalisering av komponenter är avsedda för översättning av statiska strängar. När komponentsträngar förväntas ändras bör du använda konventionella översättningsarbetsflöden. Om en författare till exempel kan redigera en gränssnittssträng med hjälp av egenskaper i dialogrutan Redigera för en komponent, bör du inte använda ett språklexikon för att internationalisera strängen.

## Språkordlistor {#language-dictionaries}

I det AEM internationaliseringsramverket används ordlistor i databasen för att lagra engelska strängar och deras översättningar på andra språk. I ramverket används engelska som standardspråk. Strängar identifieras med hjälp av deras engelska version. Vanligtvis använder internationaliseringsramverk alfanumeriska ID:n för gränssnittssträngar. Att använda den engelska versionen av strängen som ID har flera fördelar:

* Koden är lätt att läsa.
* Standardspråket är alltid tillgängligt.

Med [översättningsverktyget](/help/implementing/developing/extending/i18n/translator.md) kan du hantera alla ordlistor från en central plats.

![i18n-components-2](/help/implementing/developing/extending/assets/i18n-comp2.png)

Översättningsändringar måste komma från Git via [CI/CD-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) i AEM som en molntjänst.

### Ersätta strängar i systemordlistor {#overlaying-strings-in-system-dictionaries}

Om dina komponenter använder strängar som ingår i AEM systemordlistor, duplicerar du strängen i din egen ordlista. Alla komponenter använder strängarna från din ordlista.

Observera att du inte kan förutsäga vilken översättning som används när strängar är duplicerade i ordlistor som alla finns under noden `/apps`.
