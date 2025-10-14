---
title: Översätta innehåll för flerspråkiga webbplatser
description: Få en översikt över hur du översätter innehåll för flerspråkiga webbplatser.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Översätta innehåll för flerspråkiga webbplatser {#translating-content-for-multilingual-sites}

Automatisera översättningen av sidinnehåll och resurser för att skapa och underhålla flerspråkiga webbplatser. Om du vill automatisera arbetsflöden för översättning integrerar du översättare med AEM och skapar projekt för översättning av innehåll till flera språk. AEM har stöd för arbetsflöden för översättning mellan människor och datorer.

* **Personlig översättning:** Innehållet skickas till din översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.
* **Maskinöversättning:** Datoröversättningstjänsten översätter ditt innehåll omedelbart.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md), som är en guidad väg genom att översätta ditt AEM Sites-innehåll med hjälp av AEM kraftfulla översättningsverktyg, som är idealisk för dem som saknar AEM eller översättningsupplevelse.

Översättning av innehåll omfattar följande steg:

1. [Anslut AEM med översättningstjänstleverantören](integration-framework.md#connecting-to-a-translation-service-provider) och [skapa konfigurationer för översättningsintegreringsramverk](integration-framework.md).
1. [Koppla sidorna på din språkinställning](integration-framework.md#configuring-pages-for-translation) till översättningstjänsten och ramverkskonfigurationerna.
1. [Identifiera den typ av innehåll &#x200B;](rules.md) som ska översättas.
1. [Förbered innehållet för översättning](preparation.md) genom att skapa språkinställningen och skapa rotsidorna för språkkopior.
1. [Skapa översättningsprojekt](managing-projects.md) för att samla in innehållet som ska översättas och förbereda översättningsprocessen.
1. Använd översättningsprojekten för att [hantera innehållsöversättningsprocessen](managing-projects.md).

Om översättningstjänsten inte har någon koppling till AEM stöder AEM manuell extrahering och återinfogning av översättningsinnehåll i XML-format.

>[!NOTE]
>
>Användaren måste vara medlem i gruppen `project-administrators` för att kunna använda funktionerna för språkkopiering.

## Bästa praxis {#best-practices}

Sidan [Bästa praxis för översättning](best-practices.md) innehåller viktig information om din implementering.
