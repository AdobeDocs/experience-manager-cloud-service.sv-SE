---
title: Skapa sidor
description: Lär dig hur du skapar nya sidor för din webbplats med hjälp av webbplatskonsolen.
exl-id: 77264562-e76a-40c8-9878-847a8878fb8e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 6e13244d7ba7bb6e7a51525b66274427fe21d664
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Skapa sidor {#creating-pages}

Lär dig hur du skapar nya sidor för din webbplats med konsolen **Platser**.

>[!TIP]
>
>Innan du börjar skapa nya sidor bör du känna till [hur sidorna är ordnade i AEM.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## Åtkomstbehörigheter {#access-privileges}

Ditt konto behöver rätt behörighet för att skapa sidor.

Kontakta systemadministratören om du råkar ut för problem.

## Skapa en ny sida {#creating-a-new-page}

Om du inte har skapat alla sidor åt dig i förväg måste du skapa en sida innan du kan börja skapa innehåll:

1. Öppna [konsolen **Platser**.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navigera till den plats där du vill skapa den nya sidan.
1. Öppna den nedrullningsbara väljaren med **Skapa** i verktygsfältet och välj sedan **Sida** i listan:

   ![Skapa en sida](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. I det första steget i guiden kan du antingen:

   * Välj den mall som du vill använda för att skapa den nya sidan och välj sedan **Nästa** för att fortsätta eller **Avbryt** för att avbryta processen.
   * Mallar stöds både för [sidredigeraren](/help/sites-cloud/authoring/page-editor/introduction.md) och för [den universella redigeraren.](/help/edge/wysiwyg-authoring/templates.md)

   ![Välja en mall för en ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. Från det sista steget i guiden kan du antingen:

   * Använd de tre flikarna för att ange de [sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md) som du vill tilldela den nya sidan och välj sedan **Skapa** för att skapa sidan.

   * Använd **Bakåt** för att återgå till mallval.

   Nyckelfält är:

   * **Titel**:

      * Detta visas för användaren och är obligatoriskt.

   * **Namn**:

      * Detta används för att generera URI. Om inget anges hämtas namnet från titeln.
      * Om du anger en sida **Namn** när du skapar en sida, validerar AEM [namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR tillämpar.
      * Du **kan inte skicka ogiltiga tecken** i fältet **Namn**. När AEM upptäcker ogiltiga tecken markeras fältet och en förklaring visas som anger vilka tecken som behöver tas bort/ersättas.

   >[!TIP]
   >
   >Se [Konventioner för sidnamngivning](#page-naming-conventions).

   Den information som krävs för att skapa en sida är **Title**.

   ![Tillhandahåller sidtitel](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Tryck eller klicka på **Skapa** för att slutföra processen och skapa den nya sidan. Bekräftelsedialogrutan frågar om du vill **öppna** sidan direkt eller återgå till konsolen (**Klar**). Välj ett alternativ för att avsluta processen med att skapa sidan.

   ![Sidskapandet lyckades](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * Om du väljer **Öppna** öppnar konsolen **Platser** rätt redigerare baserat på den nya sidans mall, antingen:
      * [Sidredigeraren](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [Universell redigerare](/help/sites-cloud/authoring/universal-editor/authoring.md)

Om du återgår till konsolen kan du se din nya sida:

![Resulterande ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>Om du skapar en sida med ett namn som redan finns på samma plats, skapar AEM sidan med en variant av det namn som anges genom att lägga till en siffra. Om till exempel `beach` redan finns blir den nya sidan `beach1`.

>[!CAUTION]
>
>När en sida har skapats kan dess mall inte ändras såvida du inte [skapar en start med en ny mall](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), men befintligt innehåll går förlorat.
