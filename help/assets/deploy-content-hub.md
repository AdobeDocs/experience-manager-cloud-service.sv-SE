---
title: Distribuera [!DNL Content Hub]
description: Lär dig hur du distribuerar och aktiverar Content Hub och ger åtkomst till användare med olika typer av behörigheter (överföra resurser, Adobe Express-användare) och hur du ger administratörsbehörighet till användare.
role: Admin
source-git-commit: 56af07a198e1350282f5d3f771c1c29db318b90e
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---


# Distribuera Content Hub {#deploy-content-hub}

![Distribuera Content Hub](assets/deploy-content-hub.png)

Content Hub ingår som en del av Experience Manager Assets as a Cloud Service för att demokratisera tillgången till varumärkesinnehåll för organisationer och deras affärspartners.

Resurserna som är markerade Godkänd på Experience Manager Assets as a Cloud Service är tillgängliga för mediedistribution på Content Hub.

Den här artikeln innehåller ett komplett arbetsflöde för att ge Content Hub åtkomst till användare, inklusive variationer av behörigheter baserat på deras behov.

De olika behörigheterna för Content Hub omfattar:

* [Resurskunder](#onboard-content-hub-consumer-users): Få tillgång till varumärkesgodkända resurser på Content Hub-portalen.

* [Administratörer](#onboard-content-hub-administrator): Åtkomst till [Användargränssnitt för konfiguration](/help/assets/configure-content-hub-ui-options.md) på Content Hub, förutom Asset Consumer med inskickningsrättigheter.

* [Tillgångskunder med inlämningsrättigheter](#onboard-content-hub-consumer-users-submission-rights): Möjlighet att [överföra resurser till Content Hub](/help/assets/upload-brand-approved-assets.md) och [Integrering av Adobe Expresser](/help/assets/edit-images-content-hub.md) förutom tillgång till varumärkesgodkända mediefiler på Content Hub-portalen.

* [Resursdistributörer](#content-hub-asset-distributors): Möjlighet att godkänna mediefiler på Experience Manager Assets as a Cloud Service för att göra dessa mediefiler tillgängliga på Content Hub.

## Steg 1: Aktivera Content Hub för Experience Manager Assets med Cloud Manager {#enable-content-hub}

För att få tillgång till Content Hub-portalen måste administratörer först aktivera Content Hub för Experience Manager Assets as a Cloud Service med Cloud Manager. Utför följande steg:

1. Logga in på Cloud Manager. Se till att du väljer rätt organisation när du loggar in. Cloud Manager listar alla program.

1. Navigera till Experience Manager Assets as a Cloud Service program, klicka på ikonen Fler alternativ (..) och välj **[!UICONTROL Edit Program]**.

   ![Redigera program i Cloud Manager](assets/edit-program-cloud-manager.png)

1. På [!UICONTROL Edit Program] väljer du **[!UICONTROL Solutions & Add-ons]** -fliken.

1. Expandera **[!UICONTROL Assets]** och markera **[!UICONTROL Content Hub]**.
   ![Välj Content Hub i Cloud Manager](assets/edit-program-cloud-manager-content-hub.png)

1. Klicka på **[!UICONTROL Update]**.

Content Hub är nu aktiverat för Experience Manager Assets as a Cloud Service.

Om du inte har använt Experience Manager Assets tidigare klickar du på **[!UICONTROL Add Program]** och ange sedan programinformation (Programnamn, konfiguration för produktion) och klicka på **[!UICONTROL Continue]**. Du kan sedan välja **[!UICONTROL Assets]** och **[!UICONTROL Content Hub]** i **[!UICONTROL Solutions & Add-ons]** -fliken.

### Content Hub instans och produktprofil på Admin Console{#content-hub-instance-product-profile}

Efter [aktivera Content Hub för Assets as a Cloud Service med Cloud Manager](#enable-content-hub), finns det en ny instans som skapas i AEM Assets as a Cloud Service Admin Console med `contenthub` som suffix:

![Ny instans för Content Hub](assets/new-instance-content-hub.png)

Observera att det inte finns `author` eller `publish` i instansnamnet för Content Hub.

Klicka på instansnamnet för att visa Content Hub produktprofil.

![Content Hub produktprofil](assets/content-hub-product-profile.png)

## Steg 2: Integrera Content Hub-administratören {#onboard-content-hub-administrator}

Content Hub-administratörer kan lägga till resurser i Content Hub och kan även ställa in [Konfigurationsalternativ](/help/assets/configure-content-hub-ui-options.md) för andra användare i organisationen.

Så här skaffar du Content Hub-administratören:

1. [Öppna och klicka på Content Hub produktprofil](#content-hub-instance-product-profile).

1. Klicka **[!UICONTROL Add users]** om du vill lägga till användare eller användargrupper i produktprofilen.

1. Klicka **[!UICONTROL Save]** för att spara ändringarna.

1. När du har lagt till användaren i Content Hub produktprofil kan du få tillgång till Experience Manager Assets produktprofiler genom att klicka på AEM as a Cloud Service produktnamn i produktlistan på Admin Console.

1. Klicka på författarinstansen för AEM as a Cloud Service:
   ![Produktprofiler för AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console visar två produktprofiler för AEM as a Cloud Service: Administratörer och Användare.
1. Klicka på produktprofilen Administratörer och klicka på **[!UICONTROL Add users]** för att lägga till användaren i produktprofilen.
   ![Administratörsproduktprofil](assets/aem-cs-admin-product-profile.png)

1. Klicka **[!UICONTROL Save]** för att spara ändringarna.

## Steg 3: Införliva användare av Content Hub-mediefiler {#onboard-content-hub-consumer-users}

Content Hub konsumentanvändare har åtkomst till resurser som är tillgängliga på portalen, men kan inte lägga till nya resurser eller ändra befintliga resurser.

Så här tar du in användare på Content Hub:

1. [Öppna och klicka på Content Hub produktprofil](#content-hub-instance-product-profile).

1. Klicka **[!UICONTROL Add users]** om du vill lägga till användare eller användargrupper i produktprofilen.

1. Klicka **[!UICONTROL Save]** för att spara ändringarna.

Dessa användare har nu tillgång till de resurser som finns på Content Hub-portalen.

>[!NOTE]
>
>Du kan använda alla avancerade företagsfunktioner som synkronisering med externa identitetsleverantörer.

När du har lagt till lämpliga användare med Admin Console kan användarna få åtkomst till Content Hub via följande länk:

`https://experience.adobe.com/#/assets/contenthub`

### Inaktivera e-postmeddelanden för användare {#disable-email-notifications}

Om administratörer måste inaktivera e-postmeddelanden som skickas till användare när de läggs till i Content Hub produktprofil:

Klicka på sökikonen bredvid produktprofilens namn och inaktivera **[!UICONTROL Notify users by email]** växla.

![Inaktivera e-postmeddelanden](assets/disable-email-notifications.png)


## Steg 4: Införliva användare av Content Hub-mediefiler med inskickningsbehörighet (valfritt) {#onboard-content-hub-consumer-users-submission-rights}

Användare av Content Hub medieinnehåll med inskickningsbehörighet kan:

* [Ladda upp nytt varumärkesgodkänt material till Content Hub](/help/assets/upload-brand-approved-assets.md).

* [Ändra befintliga resurser med Adobe Express och spara resursen i databasen](/help/assets/edit-images-content-hub.md). Det går bara att redigera resurser med Adobe Express om användaren har Adobe Express.

Så här skaffar du Content Hub-användare rätt att lämna in tävlingsbidrag:

1. [När användaren har lagts till i Content Hub produktprofil](#onboard-content-hub-consumer-users)öppnar du Experience Manager Assets produktprofiler genom att klicka på AEM as a Cloud Service produktnamn i produktlistan på Admin Console.

1. Klicka på författarinstansen för AEM as a Cloud Service:
   ![Produktprofiler för AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console visar två produktprofiler för AEM as a Cloud Service: Administratörer och Användare.
1. Klicka på produktprofilen Användare och klicka på **[!UICONTROL Add users]** för att lägga till användaren i produktprofilen.
   ![Användarproduktprofil](assets/aem-cs-user-product-profile.png)

1. Klicka **[!UICONTROL Save]** för att spara ändringarna.

## Content Hub fildistributörer {#content-hub-asset-distributors}

Resursdistributörer kan godkänna mediefiler på AEM as a Cloud Service så att de är tillgängliga på Content Hub.

Så här konfigurerar du resursdistributionsrollen:

1. Gå till Experience Manager Assets produktprofiler genom att klicka på AEM as a Cloud Service produktnamn i produktlistan på Admin Console.

1. Klicka på författarinstansen för AEM as a Cloud Service:
   ![Produktprofiler för AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console visar två produktprofiler för AEM as a Cloud Service: Administratörer och Användare.
1. Klicka på produktprofilen Användare och klicka på **[!UICONTROL Add users]** för att lägga till användaren i produktprofilen.
   ![Användarproduktprofil](assets/aem-cs-user-product-profile.png)

1. Klicka **[!UICONTROL Save]** för att spara ändringarna.

   >[!NOTE]
   >
   > Du behöver inte läggas till i [Content Hub produktprofil](#onboard-content-hub-consumer-users) för resursdistributionsrollen.



