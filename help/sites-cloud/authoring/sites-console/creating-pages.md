---
title: Skapa sidor
description: Lär dig hur du skapar nya sidor för din webbplats med hjälp av webbplatskonsolen.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Skapa sidor {#creating-pages}

Lär dig hur du skapar nya sidor för din webbplats med **Webbplatser** konsol.

>[!TIP]
>
>Innan du börjar skapa nya sidor bör du känna till [hur sidorna är ordnade i AEM.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## Åtkomstbehörigheter {#access-privileges}

Ditt konto behöver rätt behörighet för att skapa sidor.

Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

## Skapa en ny sida {#creating-a-new-page}

Om du inte har skapat alla sidor åt dig i förväg måste du skapa en sida innan du kan börja skapa innehåll:

1. Öppna [den **Webbplatser** konsol.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navigera till den plats där du vill skapa den nya sidan.
1. Öppna den nedrullningsbara väljaren med **Skapa** i verktygsfältet väljer du **Sida** från listan:

   ![Skapa en sida](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. Från det första steget i guiden kan du antingen:

   * Välj den mall som du vill använda för att skapa den nya sidan och välj sedan **Nästa** för att fortsätta.

   * **Avbryt** om du vill avbryta processen.

   ![Välja en mall för en ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. Från det sista steget i guiden kan du antingen:

   * Använd de tre flikarna för att ange [sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md) du vill tilldela till den nya sidan väljer du **Skapa** för att skapa sidan.

   * Använd **Bakåt** för att återgå till mallval.

   Nyckelfält är:

   * **Titel**:

      * Detta visas för användaren och är obligatoriskt.

   * **Namn**:

      * Detta används för att generera URI. Om inget anges hämtas namnet från titeln.
      * Om du anger en sida **Namn** när du skapar en sida, AEM [validerar namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som ålagts av AEM och JCR.
      * Du **kan inte skicka ogiltiga tecken** i **Namn** fält. När AEM upptäcker ogiltiga tecken markeras fältet och en förklaring visas som anger vilka tecken som behöver tas bort/ersättas.

   >[!TIP]
   >
   >Se [Konventioner för sidnamngivning](#page-naming-conventions).

   Minimiinformationen som krävs för att skapa en sida är **Titel**.

   ![Ange sidrubrik](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Använd **Skapa** för att slutföra processen och skapa en ny sida. Bekräftelsedialogrutan frågar om du vill **Öppna** sidan omedelbart eller återgå till konsolen (**Klar**):

   ![Sidskapandet lyckades](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Om du skapar en sida med ett namn som redan finns på den platsen, genereras automatiskt en variant av namnet genom att en siffra läggs till. Om `beach` finns redan, en ny sida blir `beach1`.

1. Om du återgår till konsolen kan du se din nya sida:

   ![Resultat av ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>När en sida har skapats kan dess mall inte ändras - såvida du inte [skapa en startsida med en ny mall](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)men befintligt innehåll går förlorat.
