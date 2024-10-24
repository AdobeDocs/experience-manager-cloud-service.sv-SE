---
title: Hur lägger jag in e-signaturer i en blankett med hjälp av klottersignaturer?
description: Lär dig använda elektroniska signaturer i ett formulär med hjälp av klottersignaturer.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# E-signera ett formulär med hjälp av klottersignaturer{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [att lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Den här artikeln |


Du kan använda komponenten **Skriptsignatur** och komponenten **Signatursteg** för att rita (Klottra) signatur i ett anpassat formulär. Underskriftsstegkomponenten visar en PDF-version av det adaptiva formuläret. Du måste aktivera alternativet Dokument för post eller formulärmallsbaserad adaptiv Forms för att kunna använda signaturstegskomponenten.

![Dialogrutan Klottertecken](assets/scribble-signature.png)

## Olika alternativ finns i signaturfönstret

* **A:** Klicka på ikonen **Målarpensel** för att rita din signatur på arbetsytan.
* **B:** Klicka på ikonen **Rensa** för att rensa signaturen på arbetsytan.
* **C:** Klicka på ikonen **Geolocation** för att lägga till geopositionering tillsammans med signaturen.
* **D:** Klicka på ikonen **Tangentbord** för att skriva ditt namn på arbetsytan.

När du har valt ikonen Klar ![aem_forms_save](assets/aem_forms_save.png) i fönstret Klottsignatur kan du inte redigera signaturen. Om du vill redigera signaturen måste du bortse från den aktuella signaturen och signera igen med alternativet Målningspensel/Tangentbord ovan.

Du kan välja ikonen **Konfigurera** ![konfigurera ikon](assets/configure.png) för att ställa in proportionen för arbetsytan med klottersignaturer. Konfigurera ikon
* När proportionerna för arbetsytan Klottra signatur är mindre än 1 läggs platsinformationen till längst ned på arbetsytan Klottra signatur.


* När proportionerna för arbetsytan Klottra signatur är större än 1 läggs geopositioneringsinformationen till till höger på arbetsytan Klottra signatur.


![scribble signature-bottom](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>Signaturer sparas alltid i PNG-format.
>

## Konfigurera ett anpassat formulär för att använda skriptsignatur {#configure-an-adaptive-form-to-use-scribble-signature}

1. Alternativet Skapa ett postdokument aktiverat eller formulärmallsbaserat anpassat formulär. Stegvis information finns i [Skapa ett anpassat formulär](creating-adaptive-form.md).
1. Dra och släpp komponenten **Klottsignatur** från komponentwebbläsaren till det adaptiva formuläret.
1. Välj ikonen **Konfigurera** ![konfigurera](assets/configure.png) . Egenskaper öppnas i webbläsaren och egenskaper för komponenten Skriptsignatur visas. Konfigurera egenskaper för komponenten Scribble Signature.
1. Dra och släpp signaturstegskomponenten från komponentwebbläsaren till det adaptiva formuläret.

   >[!NOTE]
   >
   >Komponenten Signatursteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Signatursteg.

1. I innehållsläsaren väljer du **Formulärbehållare** och sedan ikonen **Konfigurera** ![konfigurera](assets/configure.png) . Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas. Navigera till **Adaptiv formulärbehållare** > **Elektronisk signatur** och avmarkera alternativet **Aktivera Adobe Sign** . Välj ikonen Klar ![aem_forms_save](assets/aem_forms_save.png) om du vill spara ändringarna.

   >[!NOTE]
   >
   >När du lägger till en komponent för signatursteg i ett anpassat formulär markeras alternativet Aktivera Adobe Sign automatiskt.

1. Välj ikonen **Konfigurera** ![konfigurera](assets/configure.png) . Egenskaper öppnas i webbläsaren och egenskaper för signatursteg visas. Konfigurera följande egenskaper:

   * **Elementnamn**: Ange komponentens namn.

   * **Titel:** Ange komponentens unika titel.
   * **Mallmeddelande:** Ange meddelandet som ska visas när signaturen PDF läses in. Adobe Sign tjänster tar lite tid att förbereda och läsa in signaturen PDF.
   * **Signeringstjänst:** Välj alternativet **Klottsignatur** .

   * **CSS-klass**: Ange CSS-klass för klientbiblioteket, om sådan finns. Adobe rekommenderar att du använder [teman](themes.md) och [ infogade format](inline-style-adaptive-forms.md) i stället för CSS-klassen.

   Välj ikonen Klar ![aem_forms_save](assets/aem_forms_save.png) om du vill spara ändringarna. Signaturen har konfigurerats.

   När du fyller i ett formulär visas nu en PDF-version av det adaptiva formuläret och alternativ för att signera PDF-dokumentet finns. Mer information finns i [Signera ett anpassat formulär med Klottsignatur](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Signera ett anpassat formulär med klottrar signatur {#sign-an-adaptive-form-using-scribble-signature}

1. När du har fyllt i ett adaptivt formulär och kommit till sidan Signatursteg visas signaturskärmen.

   ![Signaturskärm för EchoSign-sida](assets/esignscribblesign.jpg)

1. Klicka på **[!UICONTROL Sign]**. Dialogrutan för klottersignering visas. Signera formuläret och klicka på ikonen Klar ![aem_forms_save](assets/aem_forms_save.png) för att spara signaturen.

   ![Dialogrutan Klottertecken](assets/scribblewidget.png)

1. Klicka på Slutför för att slutföra signeringsprocessen.

   ![Slutför signeringsprocessen](assets/scribblecomplete.jpg)

Signaturerna läggs till i formuläret och formulärkontrollen flyttas till nästa panel.

## Se även {#see-also}

{{see-also}}