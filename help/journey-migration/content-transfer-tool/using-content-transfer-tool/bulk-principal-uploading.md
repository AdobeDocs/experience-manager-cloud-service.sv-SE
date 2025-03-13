---
title: Massöverföring av huvudkonton till IMS efter användning av CTT
description: Översikt över Överför filer gruppvis för grupper och användare och hur du använder dem på Admin Console för att skapa grupper och användare i IMS.
exl-id: 43ebd6f1-1492-461a-8d9b-2b55dcde9052
source-git-commit: b9c739a03b358de7c011e50ddbdd609c90f86b6f
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 0%

---

# Massöverföring av huvudkonton till IMS efter användning av CTT {#bulk-principal-uploading}

>[!CONTEXTUALHELP]
>id="bulk-principal-uploading"
>title="Massöverföring av huvudkonton"
>abstract="Översikt över Överför filer gruppvis för grupper och användare och hur du använder dem på Admin Console för att skapa grupper och användare i IMS."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Dokumentation för AEM Admin Console"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

## Introduktion {#introduction}

När du migrerar innehåll till molnet med CTT och CAM skapas grupper på AEM molninstans, men det går inte att placera grupper eller användare i IMS. De måste finnas i IMS för att kunna hanteras på rätt sätt av kunderna. Lyckligtvis finns det funktioner i Admin Console som gör att man kan skapa IMS-grupper och användare i grupp. CAM-importen underlättar processen genom att indatafiler sparas för att skapa massfiler. Detta gör att kunderna kan slutföra Admin Console-åtgärden som en del av den övergripande migreringsprocessen. Två typer av massöverföringsfiler skapas: en för grupper och en för användare.

Se även [Hantera användare](https://helpx.adobe.com/enterprise/using/users.html) för mer information om hur du hanterar AEM as a Cloud Service-användare.

## Allmänna regler för överföring av filer {#rules}

Det finns några allmänna riktlinjer för redigering och användning av båda typerna av överföringsfiler:

* Administratörsåtkomst till Admin Console måste först beviljas innan instruktionerna kan följas.
* Observera att det finns flera olika sätt att skapa användare och gruppera i IMS.  Se [IMS-stöd för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support) om du vill veta mer om alla tillgängliga alternativ.  Här beskrivs endast Admin Console massöverföringsmetoder.
* Det finns tre identitetstyper i IMS: Adobe ID, Enterprise ID och Federated ID.  Instruktionerna på den här sidan finns endast för **Adobe ID**.  Om du behöver använda Enterprise ID eller Federated ID, se den fullständiga [Admin Console-dokumentationen](https://helpx.adobe.com/ca/enterprise/using/admin-console.html) och även den specifika dokumentationen för [Admin Console Bulk Group-överföring](https://helpx.adobe.com/ca/enterprise/using/user-groups.html) och [Admin Console Bulk User Upload](https://helpx.adobe.com/ca/enterprise/using/bulk-upload-users.html).  Specifikationerna för överföringsfilerna skiljer sig något åt för de två identitetstyperna.
* Om ett CSV-fält tillåter flera poster (till exempel flera produktprofiler, flera grupper eller flera administratörer) måste posterna stå inom dubbla citattecken och avgränsas med kommatecken, dvs. `"profile 1,profile 2"`.

   * Enkla citattecken kan användas för det här fallet i stället för dubbla citattecken, men om du redigerar filen i Microsoft Excel kan det uppstå tolkningsproblem. Om du använder Excel för att redigera dessa filer måste du använda dubbla citattecken i stället för enkla citattecken.

## Överföring av gruppgrupp {#group-upload}

#### Användningsfall: Grupper har migrerats till AEM as a Cloud Service, men de här grupperna finns inte i IMS/Admin Console, så de måste överföras till IMS via Admin Console.

Så här använder du Admin Console funktion för gruppöverföring när du har kört en CTT/CAM-migrering:
1. Hämta gruppgruppfilen från CAM

   1. I CAM går du till **Innehållsöverföring** och väljer **Inmatningsjobb**.
   1. Klicka på ellipsen (..) på raden för det aktuella intrycket och välj **Visa huvudsammanfattning**.
   1. I den dialogruta som visas väljer du **Gruppfil** i listrutan under **Hämta en fil..** och klickar på knappen **Hämta**.
   1. Spara den resulterande CSV-filen.

1. Redigera gruppgruppfilen

   * Varje rad representerar en grupp som ska överföras och har fyra fält (fältnamnen utgör filens första rad):

      * _Användargruppnamn_ - Gruppnamnet är obligatoriskt och får innehålla högst 255 tecken.  Gruppnamnet måste vara detsamma i IMS och AEM
      * _Beskrivning_ - Det här fältet är valfritt och får innehålla högst 255 tecken
      * _Administratörer för användargrupp_ - minst en gruppadministratör måste inkluderas i det här fältet. Du kan tilldela flera administratörer genom att separera varje administratör med ett kommatecken och omsluta listan inom citattecken. Posten för varje administratör måste innehålla användarens identitetstyp, följt av ett bindestreck och sedan e-postadressen.  Till exempel
        `"Adobe ID-myAdmin@example.com,Adobe ID-myOtherAdmin@example.com"`. Ta inte med ett blanksteg efter kommatecknet som avgränsar administratörer. Du kan inte inkludera användare (som administratörer) som för närvarande inte ingår i organisationen i Admin Console
      * _Tilldelade produktprofiler_ - Det här fältet är valfritt. Du kan tilldela flera produktprofiler genom att separera varje profil med kommatecken och omsluta listan inom citattecken. Produktprofilerna som du inkluderar måste dock redan vara konfigurerade för organisationen. Se till att du anger produktprofilens namn och inte produktnamnet.  Medlemskap i produktprofiler som tilldelats en grupp ärvs av alla användare som placerats i gruppen.  Så här hittar du en produktprofil:

         1. Gå till Admin Console
         1. Hitta din produkt (t.ex. Adobe Experience Manager as a Cloud Service) och klicka på den
         1. Hitta din miljö (instans) och klicka på den
         1. Visa en lista över produktprofiler och klicka på den för din AEM-miljö. Produktprofilen är överst, dvs. _AEM Users - author - Program 12345 - Environment 012345_.

   * När CSV-filen redigeras kan vissa program lägga till ytterligare citattecken när de sparas, vilket gör att bearbetningen misslyckas. Det är en god vana att inspektera CSV-filen med Raw-format i en enkel textredigerare för att se till att varje fält bara har ett inledande och ett avslutande citattecken (och de ska inte vara&quot;typografiska citattecken&quot;).

1. Ladda upp gruppfilen i Admin Console

   1. Gå till **Användare** och sedan till **Användargrupper** i Admin Console
   1. Klicka på knappen &quot;..&quot; till höger. Välj **Lägg till användargrupper via CSV** på menyn och välj den CSV-fil som ska överföras. Klicka på **Överför**
   1. Du får ett svar på att CSV-filen har överförts (till Admin Console), men att den inte har importerats till IMS än
   1. Gå till samma&quot;..&quot;-meny och välj **Resultat av gruppåtgärd**. Den visar en lista över massöverföringsförsök och talar om för dig (under **Status**) om massöverföringen har bearbetats, slutförts eller misslyckats

      * Först visas Bearbetning, vilket anger att det inte är färdigt
      * Klicka på länken **Lägg till användargrupper** för att visa ett enkelt statusmeddelande för varje rad.
      * Om det i stället har misslyckats klickar du på den lilla ikonen under **Arkiv** och ger lite mer information om varför det misslyckades.  Gruppradnumren refereras från rad 1.
1. Använd Admin Console för att verifiera dina ändringar.

## Massöverföring och redigering av användare {#bulk-user}

Admin Console innehåller två olika åtgärder för att överföra och redigera användarinformation. Instruktioner för att lägga till nya användare i IMS-program direkt nedan. Instruktioner för redigering av befintliga IMS-användare finns i följande avsnitt: [Redigera flera användare](#user-edit).

### Överföring av flera användare {#user-upload}

#### Användningsexempel: Grupper har migrerats till AEM as a Cloud Service och överförts via massöverföring eller någon annan metod.  Användare kanske inte finns i IMS/Admin Console, så de måste överföras och länkas till sina grupper i IMS via Admin Console.

>[!NOTE]
>
>En användare visas i filen **Massöverföring av användare** om den finns i en grupp som har inhämtats under samma förtäring som filen skapades från. Det kan också visas om användaren är direkt i en ACL eller CUG för migrerat innehåll, eller är medlem i en inbyggd grupp eller lokal grupp som finns i en ACL eller CUG för det migrerade innehållet. Mer information om de här fallen finns i [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Så här använder du Admin Console massöverföring av användare:

1. Hämta massanvändarfilen från CAM
   1. I CAM går du till **Innehållsöverföring** och väljer **Inmatningsjobb**.
   1. Klicka på ellipsen (..) på raden för det aktuella intrycket och välj **Visa huvudsammanfattning**.
   1. I den dialogruta som visas väljer du **Massanvändarfil** i listrutan under **Hämta en fil..** och klickar på knappen **Hämta**.
   1. Spara den resulterande CSV-filen
1. Redigera massanvändarfilen
   * Varje rad representerar en användare som ska överföras och har femton fält (fältnamnen utgör filens första rad). Vissa fält är valfria och beskrivs inte här. Se [CSV-format för massanvändare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format).  Fälten är:

      * _Identitetstyp_ - valfritt.  Om inget anges skapas den som en Adobe ID
      * _Användarnamn_ - valfritt och inte använt för Adobe ID-överföringar
      * _Domän_ - valfritt och inte använt för Adobe ID-överföringar
      * _E-post_ - krävs.  E-postadressen används för verifiering första gången användaren loggar in
      * _Förnamn_ - valfritt.  Ska användas eftersom det visas, med efternamn, på flera ställen
      * _Efternamn_ - valfritt.  Ska användas eftersom den visas på flera ställen
      * _Landskod_ - Valfri och används inte för Adobe ID-överföringar
      * _ID_ - Valfritt och inte använt för Adobe ID-överföringar
      * _Produktkonfigurationer_ - valfritt. Det här fältet ärvs också från alla grupper som användaren är medlem i
      * _Administratörsroller_ - valfritt. Använd det här fältet om användaren är administratör. Mer information finns i [CSV-format för flera användare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
      * _Produktkonfigurationer som administreras_ - valfritt.  Mer information finns i [CSV-format för flera användare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format). Det här fältet ärvs också från alla grupper som användaren är medlem i
      * _Användargrupper_ - valfritt. En lista över grupper som användaren ska tilldelas som medlem. Varje grupp måste vara en befintlig IMS-grupp. När massanvändarfilen hämtas från CAM fylls fältet i automatiskt med namnen på den IMS-aktiverade gruppen som användaren var medlem i (direkt eller indirekt) före migreringen
      * _Användargrupper som administreras_ - valfritt.  Mer information finns i [CSV-format för flera användare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format). Det här fältet ärvs också från alla grupper som användaren är medlem i
      * _Produkter som administreras_ - valfritt.  Mer information finns i [CSV-format för flera användare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format). Det här fältet ärvs också från alla grupper som användaren är medlem i
      * _Kontrakt administrerade_ - valfritt.  Mer information finns i [CSV-format för flera användare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
      * _Developer Access_ - valfritt.  Mer information finns i [CSV-format för flera användare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
      * _Automatiskt tilldelade produkter_ - valfritt.  Mer information finns i [CSV-format för flera användare](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)

   * När CSV-filen redigeras kan vissa program lägga till ytterligare citattecken när de sparas, vilket gör att bearbetningen misslyckas. Det är god praxis att inspektera CSV-filen för Raw-format i en enkel textredigerare för att se till att varje fält bara har ett inledande och ett avslutande citattecken (och de ska inte vara&quot;typografiska citattecken&quot;)

1. Använd Admin Console för att importera massanvändarfilen

   1. Gå till Användare i Admin Console
   1. Klicka på knappen **Lägg till användare via CSV**
   1. Dra och släpp eller välj en CSV-fil för en större användare som hämtats från CAM
   1. Klicka på knappen **Överför**
   1. Du får ett svar på att CSV-filen har överförts (till Admin Console), men att den inte har importerats till IMS än.
   1. Gå till menyn &quot;..&quot; till höger och välj **Resultat av gruppåtgärd**.  Den visar en lista över massöverföringsförsök och visar (under **Status**) om massöverföringen har bearbetats, slutförts eller misslyckats.

      * Först visas Bearbetning, vilket anger att det inte är färdigt
      * Klicka på länken **Lägg till användare** för att visa ett enkelt statusmeddelande för varje rad
      * Om det i stället har misslyckats klickar du på den lilla ikonen under **Arkiv** så får du lite mer information om varför det misslyckades. Användarradnumren refereras från rad 1.

1. Använd Admin Console för att verifiera dina ändringar.

>[!NOTE]
>
>Efter ett icke-rensat intag är det möjligt att användare som tidigare har migrerats och sedan skapats i IMS kommer att visas i filen för massöverföring av användare. Det här kan vara av många skäl. I så fall går det inte att överföra användaren igen. Prova i stället att ta bort användaren från filen för massöverföring av användare. Om användaren måste läggas till i olika grupper använder du filen Redigera gruppanvändare enligt nedan.

### Redigera flera användare {#user-edit}

#### Användningsexempel: Grupper och användare har migrerats till AEM as a Cloud Service och överförts via massöverföring eller någon annan metod. Nu behöver du göra några ändringar för flera användare samtidigt, till exempel lägga till dem i en befintlig IMS-grupp.

Så här använder du Admin Console gruppredigeringsfunktion:

1. Hämta massanvändarfilen från Admin Console

   1. Gå till Användare i Admin Console
   1. Klicka på knappen &quot;..&quot; till höger.  Välj **Redigera användarinformation via CSV** på menyn
   1. Klicka på **Hämta CSV-mall** och välj **Aktuella användare**.  En CSV-fil ska visas i din lokala mapp för hämtningar.

1. Redigera massanvändarfilen

   1. Gå till Användare i Admin Console
   1. Redigera CSV-filen med en textredigerare (rekommenderas) eller ett kalkylbladsprogram som Excel. Om du använder ett program kan data ändras oförutsägbart, så vi rekommenderar att du använder en textredigerare för att verifiera filens formatering när du har redigerat.
   1. Beskrivningarna av fälten i den här filen är desamma som ovan under Överför flera användare
   1. Ta bort alla användare som inte redigeras
   1. Om du ändrar fältet Användargrupper lämnar du de aktuella grupperna och lägger till nya efter behov. Om du tar bort en befintlig grupp tas användaren bort från den gruppen i IMS
   1. När CSV-filen redigeras kan vissa program lägga till ytterligare citattecken när de sparas, vilket gör att bearbetningen misslyckas. Det är god praxis att inspektera CSV-råfilen i en enkel textredigerare för att se till att varje fält bara har ett inledande och ett avslutande citattecken (och de ska inte vara&quot;typografiska citattecken&quot;)

1. Överför massanvändarfilen i Admin Console

   1. Gå till Användare i Admin Console
   1. Klicka på knappen &quot;..&quot; till höger. Välj **Redigera användarinformation via CSV** på menyn
   1. Dra och släpp eller välj den redigerade CSV-filen för massanvändare
   1. Klicka på knappen Överför
   1. Du får ett svar på att CSV-filen har överförts (till Admin Console), men att den inte har importerats till IMS än
   1. Gå till menyn &quot;..&quot; till höger och välj **Resultat av gruppåtgärd**. Här visas en lista över massöverföringsförsök och om massöverföringen har bearbetats, slutförts eller misslyckats visas (under Status).

      * Först visas Bearbetning, vilket anger att det inte är färdigt
      * Klicka på länken **Redigera användarinformation** för att visa ett enkelt statusmeddelande för varje rad
      * Om det i stället har misslyckats klickar du på den lilla ikonen under **Arkiv** så visas lite mer information om varför det misslyckades. Användarradnumren refereras från rad 1.

1. Använd Admin Console för att verifiera dina ändringar.
