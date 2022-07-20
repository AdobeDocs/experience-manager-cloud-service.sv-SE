---
title: Använda elektroniska signaturer i ett formulär med hjälp av klottersignaturer
seo-title: Apply electronic signatures to a form using scribble signatures
description: Signera formulär med klottrar
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: 73953a3d71f3328def3bd4c1f03516b4839695ea
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Använda elektroniska signaturer i ett formulär med hjälp av klottersignaturer{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

Du kan använda **Klottersignatur** komponenter och **Signatursteg** -komponent för att rita (Klottra) signatur i ett adaptivt formulär. Underskriftsstegkomponenten visar en PDF-version av det adaptiva formuläret. Du måste aktivera alternativet Dokument för post eller formulärmallsbaserad adaptiv Forms för att kunna använda signaturstegskomponenten.

Båda komponenterna har ett fönster som visas nedan för att signera ett formulär. Du kan också klicka på ikonen för geopositionering ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) för att lägga till geopositionering till signaturen.

![Dialogrutan Klottra signering](assets/scribble-signature.png)

## Konfigurera ett anpassat formulär för att använda skriptsignatur {#configure-an-adaptive-form-to-use-scribble-signature}

1. Alternativet Skapa ett postdokument aktiverat eller formulärmallsbaserat anpassat formulär. Stegvisa instruktioner finns i [Skapa ett adaptivt formulär](creating-adaptive-form.md).
1. Dra och släpp **Klottersignatur** från komponentwebbläsaren till det adaptiva formuläret.
1. Tryck på **Konfigurera** ![konfigurera](assets/configure.png) ikon. Egenskaper öppnas i webbläsaren och egenskaper för komponenten Skriptsignatur visas. Konfigurera egenskaper för komponenten Scribble Signature.
1. Dra och släpp signaturstegskomponenten från komponentwebbläsaren till det adaptiva formuläret.

   >[!NOTE]
   >
   >Komponenten Signatursteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Signatursteg.

1. Tryck på **Formulärbehållare** och trycker på **Konfigurera** ![](assets/configure.png) ikon. Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas. Navigera till **Adaptiv formulärbehållare** > **Elektronisk signatur** och avmarkera **Aktivera Adobe Sign** alternativ. Tryck på Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) om du vill spara ändringarna.

   >[!NOTE]
   >
   >När du lägger till en komponent för signatursteg i ett anpassat formulär markeras alternativet Aktivera Adobe Sign automatiskt.

1. Tryck på **Konfigurera** ![konfigurera](assets/configure.png) ikon. Egenskaper öppnas i webbläsaren och egenskaper för signatursteg visas. Konfigurera följande egenskaper:

   * **Elementnamn**: Ange komponentens namn.

   * **Titel:** Ange komponentens unika namn.
   * **Mallmeddelande:** Ange meddelandet som ska visas medan signaturen PDF läses in. Adobe Sign tjänster tar lite tid att förbereda och läsa in signaturen PDF.
   * **Underteckningstjänst:** Välj **Klottersignatur** alternativ.

   * **CSS-klass**: Ange CSS-klass för klientbiblioteket, om det finns någon. Det rekommenderas att använda [teman](themes.md) och [infogade format](inline-style-adaptive-forms.md) i stället för CSS-klassen.

   Tryck på Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) om du vill spara ändringarna. Signaturen har konfigurerats.

   När du fyller i ett formulär visas nu en PDF-version av det adaptiva formuläret och alternativ för att signera PDF-dokumentet finns. Mer information finns i [Signera ett anpassat formulär med klottrar signatur](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Signera ett anpassat formulär med klottrar signatur {#sign-an-adaptive-form-using-scribble-signature}

1. När du har fyllt i ett adaptivt formulär och kommit till sidan Signatursteg visas signaturskärmen.

   ![Signaturskärm för EchoSign-sida](assets/esignscribblesign.jpg)

1. Klicka på **[!UICONTROL Sign]**. Dialogrutan för klottersignering visas. Signera formuläret och klicka på Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) -ikonen för att spara signaturen.

   ![Dialogrutan Klottra signering](assets/scribblewidget.jpg)

1. Klicka på Slutför för att slutföra signeringsprocessen.

   ![Slutför signeringsprocessen](assets/scribblecomplete.jpg)

Signaturerna läggs till i formuläret och formulärkontrollen flyttas till nästa panel.

