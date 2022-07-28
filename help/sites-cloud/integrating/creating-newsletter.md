---
title: Skapa ett Adobe Experience Manager Newsletter
description: 'Skapa ett Adobe Experience Manager Newsletter '
feature: Administering
role: Admin
source-git-commit: f68f5a457bbbcd76681cccabe5a3f4c92b6f8770
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Skapa ett Adobe Experience Manager Newsletter {#creating-newsletter}

Innan du kan utföra stegen nedan måste du först [integrera](/help/sites-cloud/integrating/integrating-campaign-classic.md) Adobe Campaign Classic och AEM as a Cloud Service. När du har konfigurerat både Adobe Campaign Classic och AEM as a Cloud Service får du lära dig hur du skapar ett Adobe Experience Manager Newsletter.

1. Klicka på Adobe Experience Manager logotyp i den övre vänstra delen av AEM författare och välj **Webbplatser**.
1. Välj Campaign, klicka **Skapa→Sida**.
   ![skapa](assets/create.png)
1. Välj Varumärke och klicka på **Nästa**.
1. Ange en titel och klicka på **Skapa** och **Klar**.
1. Om du vill skapa en Campaign-sida går du till **Campaigns→AdobeDemo→Överordnad** och klicka **Skapa→Sida**.
   ![kampanjsida](assets/campaignpage.png)
1. Välj Campaign-mallen och klicka sedan på **Nästa** och **Klar**.
1. Ange en titel och klicka på **Skapa** och **Klar**.
1. Gå till **Campaign→AdobeDemo→Överordnad** och markera kryssrutan CampaignPage. Klicka **Egenskaper** överst till vänster.
   ![kampanjegenskaper](assets/propertiesedit.png)
1. Gå till **Cloud Service** tab:
   * Välj Adobe Campaign i listrutan Cloud Service.
   * Välj önskat namn för Adobe Campaign-konfigurationen.
   * **Spara** och **Stäng**.
1. Om du vill skapa en e-postsida från Adobe Campaign Classic går du till **Campaign→AdobeDemo→Överordnad→CampaignPage** och klicka **Skapa→Sida**.
1. Markera Adobe Campaign-mallen för e-post (till exempel AC 6.1) och klicka på **Nästa**.
1. Ange nyhetsbrevets titel på sidan Skapa och klicka på **Skapa** och **Klar**.
1. Gå till **Campaign→AdobeDemo→Överordnad→CampaignPage** markerar du kryssrutan Campaign Classic och klickar på **Redigera** överst till vänster för att öppna e-postsidan.
1. Redigera nyhetsbrevet från Adobe Campaign Classic efter dina behov.
1. Klicka på **Sidinformation** överst till vänster och klicka på **Publicera sida**.
1. Välj konfigurationen som sidan ska publiceras på. Klicka **Publicera**.
   ![publiceringssida](assets/publish.png)
1. Nyhetsbrevet har publicerats på publiceringsinstansen och även på AEM Adobe Campaign Classic-konfiguration.
   * Nu visas nyhetsbrevet i Adobe Campaign Classic
1. Klicka på knappen Sidinformation och klicka på **Starta arbetsflöde**.
1. Välj **Godkänn för Adobe Campaign** som arbetsflödesmodell och klicka på **Starta arbetsflöde** -knappen.
1. En ansvarsfriskrivning visas högst upp på sidan. Klicka **Slutförd** för att bekräfta granskningen och klicka igen **OK**.
1. Klicka **Slutförd** och markera **Godkännande av nyhetsbrev** i listrutan Nästa steg och klicka på **OK** -knappen.

## Skapa en mottagare {#creating-recipient}

1. Öppna Adobe Campaign Classic-servern med Adobe Campaign Classic klientkonsol.
1. Gå till Utforskaren.
1. Gå till Profiler och mål i trädvyn till vänster och välj **Mottagare**.
   ![mottagare](assets/recipients.png)
1. Fyll i information om mottagaren.
   * Ange förnamnet.
   * Ange efternamn.
   * Ange e-postadressen.
   * Klicka **Spara**.

## Skapa en e-postleverans i Adobe Campaign Classic {#create-delivery}

1. Öppna Adobe Campaign Classic-servern med Adobe Campaign Classic klientkonsol.
1. Gå till Utforskaren.
1. I trädvyn till vänster väljer du **Campaign Management** och markera **Leveranser**.
1. Klicka på längst upp till höger **Nytt**.
1. Välj **E-postleverans med AEM** i listrutan Leveransmall och klicka på **Fortsätt**.
1. Klicka på länken Från under E-postparametrar.
   * Ange avsändaradressen.
   * Ange fältet Från.
   * Klicka **OK**.
1. Klicka **Till** klicka sedan på **Lägg till** på den valda målskärmen.
1. Välj **En mottagare** och klicka **Nästa**.
   ![måltyp](assets/publish.png)
1. Välj den skapade mottagaren [tidigare](#creating-recipient) och klicka **Slutför**.
1. Mottagaren har valts. Klicka **OK**.
1. Klicka **Synkronisera**.
1. Markera e-postsidan i listan och klicka på **OK**.
1. E-postmallen synkroniseras. Klicka **Uppdatera innehåll** om den inte har lästs in.
1. Klicka **Skicka** för att skicka e-postmeddelandet.
1. På nästa skärm väljer du **Leverera så snart som möjligt** och sedan klicka **Analysera**.
   ![leveransmål](assets/deliverytarget.png)
1. När leveransen är klar klickar du **Bekräfta leverans** för att börja skicka e-postmeddelandet. Klicka **Ja** för att bekräfta.
   ![bekräfta leverans](assets/confirmdelivery.png)
1. Leveransen har startat. Klicka **Stäng**.
1. Klicka **Spara** för att spara på leveransen.
