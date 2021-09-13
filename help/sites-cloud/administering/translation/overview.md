---
title: Översätta innehåll för flerspråkiga webbplatser
description: Få en översikt över hur du översätter innehåll för flerspråkiga webbplatser.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Översätta innehåll för flerspråkiga webbplatser {#translating-content-for-multilingual-sites}

Automatisera översättningen av sidinnehåll och resurser för att skapa och underhålla flerspråkiga webbplatser. Om du vill automatisera arbetsflöden för översättning integrerar du översättare med AEM och skapar projekt för översättning av innehåll till flera språk. AEM har stöd för arbetsflöden för översättning mellan människor och datorer.

* **Personlig översättning:** Innehållet skickas till din översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.
* **Maskinöversättning:** Maskinöversättningstjänsten översätter ditt innehåll omedelbart.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll kan du läsa vår [Site Translation Journey,](/help/journey-sites/translation/overview.md), där du vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

Översättning av innehåll omfattar följande steg:

1. [Koppla AEM med översättningstjänsten ](integration-framework.md#connecting-to-a-translation-service-provider) och  [skapa konfigurationer](integration-framework.md) för översättningsintegrering.
1. [Koppla sidorna i ditt språk till ](integration-framework.md#configuring-pages-for-translation) översättningstjänsten och ramverkskonfigurationerna.
1. [Identifiera vilken typ av ](rules.md) innehåll som ska översättas.
1. [Förbered innehållet för ](preparation.md) översättning genom att skapa språket överordnad och skapa rotsidorna för språkkopior.
1. [Skapa översättningsprojekt ](managing-projects.md) för att samla in det innehåll som ska översättas och förbereda översättningsprocessen.
1. Använd översättningsprojekten för att [hantera innehållsöversättningsprocessen](managing-projects.md).

Om översättningstjänsten inte har någon koppling till AEM stöder AEM manuell extrahering och återinfogning av översättningsinnehåll i XML-format.

>[!NOTE]
>
>Användaren måste vara medlem i `project-administrators`-gruppen för att kunna använda språkkopieringsfunktionerna.

## Bästa praxis {#best-practices}

Sidan [Bästa praxis för översättning](best-practices.md) innehåller viktig information om implementeringen.
