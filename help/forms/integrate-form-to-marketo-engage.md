---
Title: How to Integrate Marketo Engage with AEM Forms?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 74cd25f9-1ee1-4f3f-8e02-8714071e7c86
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Integrera Marketo Engage med AEM Forms

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

Genom att integrera AEM Forms med [Adobe Marketo Engage](https://experienceleague.adobe.com/sv/docs/marketo/using/home) kan användare utnyttja möjligheterna i Marketo Engage för att skapa affärslogik från insamlade data och automatisera arbetsflöden, inklusive smarta kampanjer och automatiserad e-postmarknadsföring. Det konfigurerade formuläret kan skicka inhämtade data till Marketo Engage för bearbetning.

## Fördelar med att integrera Marketo Engage med blanketter

Nedan följer några fördelar med att ansluta ett AEM-formulär till Adobe Marketo Engage:

* **Förenklad integrering**: Om du kopplar formulär till Marketo Engage behöver du inte skapa en separat formulärdatamodell. Integreringsprocessen är enkel och användarvänlig.
* **Automatisk datainhämtning**: Det hjälper till att automatiskt hämta in formulärinskickat material och lagra det i Marketo, vilket eliminerar manuell datainmatning och minskar antalet fel.

* **Leadhantering**: Effektiviserar leadhanteringsprocesserna genom att integrera formulärinlämningar direkt i marknadsföringsdatabasen, vilket ger bättre spårning och näring av leads.

* **Förbättrade kampanjprestanda**: Den använder formulärdata för att analysera och optimera marknadsföringskampanjer, vilket förbättrar det övergripande resultatet och avkastningen på investeringen.

* **Analys och rapportering**: Det hjälper till att få tillgång till stabila analys- och rapporteringsverktyg, som Munchkin, inom Marketo för att mäta effektiviteten i formulär och kampanjer.

* **Uppföljningsautomatisering**: Det hjälper till att automatisera uppföljning av e-postmeddelanden och arbetsflöden som triggas av formulärskickning, vilket garanterar snabb kommunikation med leads.

## Fördelar med att använda AEM Forms framför alternativa blankettlösningar

Tabellen nedan visar några skäl att välja AEM Forms framför andra alternativa formulärlösningar:

| **Funktion** | **AEM Forms** | **Andra formulärlösningar** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **Anpassningar** | Gör att du kan lägga till specifika anpassade funktioner, justera formuläråtgärder och ändra fältbeteenden för att förbättra formulärinteraktioner och komplexa arbetsflöden | Inget anpassningsstöd |
| **Regelredigeraren** | Stöder en inbyggd regelredigerare för att lägga till logik och villkor. | Inget stöd för regelredigeraren |
| **Layoutalternativ** | Stöder flera layoutalternativ | Begränsade layoutalternativ |
| **Förifyll tjänst** | Erbjuder en förifyllningstjänst för att automatiskt fylla i formulärdata. | Ingen förifyllningstjänst är tillgänglig |
| **Inbäddning på platser** | Kan bäddas in på platser med iFrame | Det går inte att bädda in webbplatser med iFrame |
| **Enkel integrering med platser** | Ingen ytterligare utbildning krävs; AEM Forms använder samma kunskaper som Sites | Ytterligare utbildning kan behövas |
| **Skicka data** | Kan skicka data till olika plattformar och erbjuder flera olika anslutningar, som Connect to SharePoint, Connect to OneDrive, Connect to Salesforce med flera. | Kan skicka data till ett begränsat antal anslutningar, till exempel till Salesforce |

## Att tänka på när du integrerar Marketo Engage med formulär

Tänk på följande när du integrerar Marketo Engage med AEM Forms:

* AEM stöder bara People(Leads)-databasen bland de olika Marketo-databaserna.
* Marketo tillåter att [10 anpassade objekt](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) skapas som användardefinierade objekt för att lagra specialiserade data utöver standardfälten i Leads, vilket stöder unika affärsbehov.
* AEM har bara åtkomst till anpassade objekt om de är kopplade till lead-databasen

## Förutsättningar för att integrera Marketo Engage med formulär

Nedan beskrivs förutsättningarna för att ansluta Marketo Engage till AEM Forms:

* En giltig Adobe Marketo Engage-licens
* En fungerande instans av Marketo Engage som [hämtar klient-ID och klienthemlighet](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) för att skapa en molnkonfiguration.

## Skapa molntjänstkonfiguration för att ansluta AEM Forms (Adaptiv Forms) till Marketo Engage

![Arbetsflöde](/help/forms/assets/workflow-marketo-1.png)

>[!VIDEO](https://video.tv.adobe.com/v/3442865/engage-marketo-aem-forms-aem)

<span> Den här videon gäller endast för kärnkomponenter. Information om UE/Foundation Components finns i artikeln.</span>

Molnkonfigurationen kopplar din Experience Manager-instans till Adobe Marketo Engage-instansen. Så här skapar du en molnkonfiguration för Marketo Engage:

1. Gå till **Verktyg** > **Molntjänster** > **Marketo Engage**.

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

2. Öppna en mapp som ska vara värd för konfigurationen och klicka på **Skapa**. Fönstret **Skapa Marketo Engage-konfiguration** visas.

   >[!NOTE]
   >
   > Du kan också [konfigurera mappen för molntjänstkonfigurationer](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations).

3. Ange **Rubrik** för konfigurationen och autentiseringsuppgifterna för att ansluta till tjänsten. Du kan hämta autentiseringsuppgifterna från Adobe Marketo Engage kontrollpanel:
   * **Klient-ID** och **Klienthemlighet** finns i **Admin** > **Integration** > **LaunchPoint** genom att markera den anpassade tjänsten och klicka på **Visa information**.
   * **Identitets-URL** är tillgänglig i **Admin** > **Integration** > **Webbtjänster** som **Identitet** i avsnittet **REST API** .

4. Klicka på **Anslut**.  Om anslutningen lyckas visas meddelandet `Authentication Successful`.
5. Klicka på **[!UICONTROL Create]** om du vill spara molnkonfigurationsinställningarna.

![Marketo Engage Cloud-konfiguration](/help/forms/assets/marketo-engage-cloud-configuration.png)

Nu kan du använda den molntjänstkonfiguration du har skapat för att ansluta Marketo Engage-datakällan till ett adaptivt formulär.

## Nästa steg

Du har skapat molntjänstkonfigurationen för att integrera Adobe Marketo Engage med AEM Forms. Nu kan du integrera:
* [Nytt anpassat formulär med Marketo Engage](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Befintlig anpassningsbar form med Marketo Engage](/help/forms/use-marketo-engage-data-source-in-form.md)

## Relaterade artiklar

{{af-submit-action}}

## Se även

{{marketo-engage-see-also}}
