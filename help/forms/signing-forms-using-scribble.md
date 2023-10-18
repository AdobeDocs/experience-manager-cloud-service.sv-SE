---
title: Hur lägger jag in e-signaturer i en blankett med hjälp av klottersignaturer?
description: Lär dig använda elektroniska signaturer i ett formulär med hjälp av klottersignaturer.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# E-signera ett formulär med hjälp av klottersignaturer{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Den här artikeln |


Du kan använda **Klottersignatur** komponenter och **Signatursteg** -komponent för att rita (Klottra) signatur i ett adaptivt formulär. Underskriftsstegkomponenten visar en PDF-version av det adaptiva formuläret. Du måste aktivera alternativet Dokument för post eller formulärmallsbaserad adaptiv Forms för att kunna använda signaturstegskomponenten.

![Dialogrutan Klottra signering](assets/scribble-signature.png)

## Olika alternativ finns i signaturfönstret

* **S:** Klicka på **Målarpensel** för att rita din signatur på arbetsytan.
* **B:** Klicka på **Rensa** -ikonen för att rensa signaturen på arbetsytan.
* **C:** Klicka på **Geolokalisering** -ikon för att lägga till geopositionering tillsammans med signaturen.
* **D:** Klicka på **Tangentbord** om du vill skriva ditt namn på arbetsytan.

När du trycker på Klart ![aem_forms_save](assets/aem_forms_save.png) -ikonen i fönstret Klottsignatur kan du inte redigera signaturen. Om du vill redigera signaturen måste du bortse från den aktuella signaturen och signera igen med alternativet Målningspensel/Tangentbord ovan.

Du kan trycka på **Konfigurera** ![konfigurera ikon](assets/configure.png) -ikonen för att ange proportioner för arbetsytan Skrivbar signatur.
* När proportionerna för arbetsytan Klottra signatur är mindre än 1 läggs platsinformationen till längst ned på arbetsytan Klottra signatur.


* När proportionerna för arbetsytan Klottra signatur är större än 1 läggs geopositioneringsinformationen till till höger på arbetsytan Klottra signatur.


![klottra signature-bottom](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>Signaturer sparas alltid i PNG-format.
>

## Konfigurera ett anpassat formulär för att använda skriptsignatur {#configure-an-adaptive-form-to-use-scribble-signature}

1. Alternativet Skapa ett postdokument aktiverat eller formulärmallsbaserat anpassat formulär. Stegvisa instruktioner finns i [Skapa ett adaptivt formulär](creating-adaptive-form.md).
1. Dra och släpp **Klottersignatur** från komponentwebbläsaren till det adaptiva formuläret.
1. Tryck på **Konfigurera** ![konfigurera](assets/configure.png) -ikon. Egenskaper öppnas i webbläsaren och egenskaper för komponenten Skriptsignatur visas. Konfigurera egenskaper för komponenten Scribble Signature.
1. Dra och släpp signaturstegskomponenten från komponentwebbläsaren till det adaptiva formuläret.

   >[!NOTE]
   >
   >Komponenten Signatursteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Signatursteg.

1. Tryck på **Formulärbehållare** och trycker på **Konfigurera** ![konfigurera ikon](assets/configure.png) -ikon. Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas. Navigera till **Adaptiv formulärbehållare** > **Elektronisk signatur** och avmarkera **Aktivera Adobe Sign** alternativ. Tryck på Klar ![aem_forms_save](assets/aem_forms_save.png) om du vill spara ändringarna.

   >[!NOTE]
   >
   >När du lägger till en komponent för signatursteg i ett anpassat formulär markeras alternativet Aktivera Adobe Sign automatiskt.

1. Tryck på **Konfigurera** ![konfigurera](assets/configure.png) -ikon. Egenskaper öppnas i webbläsaren och egenskaper för signatursteg visas. Konfigurera följande egenskaper:

   * **Elementnamn**: Ange komponentens namn.

   * **Titel:** Ange komponentens unika namn.
   * **Mallmeddelande:** Ange meddelandet som ska visas medan signaturen PDF läses in. Adobe Sign tjänster tar lite tid att förbereda och läsa in signaturen PDF.
   * **Underteckningstjänst:** Välj **Klottersignatur** alternativ.

   * **CSS-klass**: Ange CSS-klass för klientbiblioteket, om sådan finns. Det rekommenderas att använda [teman](themes.md) och [infogade format](inline-style-adaptive-forms.md) i stället för CSS-klassen.

   Tryck på Klar ![aem_forms_save](assets/aem_forms_save.png) om du vill spara ändringarna. Signaturen har konfigurerats.

   När du fyller i ett formulär visas nu en PDF-version av det adaptiva formuläret och alternativ för att signera PDF-dokumentet finns. Mer information finns i [Signera ett anpassat formulär med klottrar signatur](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Signera ett anpassat formulär med klottrar signatur {#sign-an-adaptive-form-using-scribble-signature}

1. När du har fyllt i ett adaptivt formulär och kommit till sidan Signatursteg visas signaturskärmen.

   ![Signaturskärm för EchoSign-sida](assets/esignscribblesign.jpg)

1. Klicka på **[!UICONTROL Sign]**. Dialogrutan för klottersignering visas. Signera formuläret och klicka på Klar ![aem_forms_save](assets/aem_forms_save.png) -ikonen för att spara signaturen.

   ![Dialogrutan Klottra signering](assets/scribblewidget.png)

1. Klicka på Slutför för att slutföra signeringsprocessen.

   ![Slutför signeringsprocessen](assets/scribblecomplete.jpg)

Signaturerna läggs till i formuläret och formulärkontrollen flyttas till nästa panel.

## Se även {#see-also}

{{see-also}}