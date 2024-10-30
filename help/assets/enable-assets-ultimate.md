---
title: Aktivera Assets Ultimate
description: Lär dig hur du aktiverar Assets Ultimate för nya och befintliga kunder.
feature: Asset Management
role: User, Admin
source-git-commit: 16ce83409044ad54140754112eb4d35b97883b44
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Aktivera [!DNL Assets] as a Cloud Service Ultimate {#enable-assets-cloud-service-ultimate}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Uppgradera till Asset Cloud Service Ultimate](/help/assets/assets/upgrade-assets-cs-ultimate-package-banner.png)

Med Assets as a Cloud Service Ultimate kan du utföra olika viktiga DAM-funktioner, t.ex. resurshantering och bibliotekstjänster, säkerhets- och rättighetshantering, anslutningar för Creative och Experience Cloud, UI-utbyggbarhet, API-driven automatisering, integrering med program från Adobe och utanför Adobe, anpassad koddriftsättning och mycket annat. En fullständig lista finns i [Assets as a Cloud Service Ultimate Overview](/help/assets/assets-ultimate-overview.md).

## Aktivera Assets Ultimate {#enable-assets-ultimate}

Nya Assets as a Cloud Service kunder måste först aktivera Assets Ultimate genom att skapa ett nytt program med Cloud Manager.

Utför följande steg:

1. Logga in på Cloud Manager som systemadministratör. Se till att du väljer rätt organisation när du loggar in.

   >[!NOTE]
   >
   >Se till att du har lagts till i rätt Cloud Manager-produktprofil för att lägga till ett nytt program. Mer information finns i [Rollbaserade behörigheter i Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

1. [Skapa ett nytt program](/help/journey-onboarding/create-program.md) och [lägg till miljöer](/help/journey-onboarding//create-environments.md) i det.

   Välj **[!UICONTROL Assets Ultimate]** på fliken **[!UICONTROL Solutions & Add-ons]** när du skapar det nya programmet. Du kan också expandera **[!UICONTROL Assets Ultimate]** och välja **[!UICONTROL Content Hub]** för att aktivera [Content Hub](/help/assets/product-overview.md) för resursdistribution.

   ![AEM Assets Ultimate](assets/aem-assets-ultimate-solutions.png)

1. Klicka på **[!UICONTROL Create]** för att skapa programmet. Assets Ultimate är nu aktiverat för Experience Manager Assets as a Cloud Service.

Systemadministratören är automatiskt berättigad som AEM på Assets Ultimate och får ett e-postmeddelande om att navigera till Admin Console för att hantera de tillgängliga produktprofilerna.

Din AEM as a Cloud Service-instans på Admin Console innehåller följande produktprofiler:

* AEM administratörer

* AEM

* [Användare av AEM Assets Collaborator](#onboard-collaborator-users)

* [AEM Assets Power Users](#onboard-power-users)

  ![AEM Assets produktprofiler](assets/aem-assets-product-profiles.png)

Om du har aktiverat Content Hub för Assets as a Cloud Service skapas en ny instans i AEM Assets as a Cloud Service Admin Console med `delivery` som suffix:

![Ny instans för Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Om du har etablerat Content Hub före 14 augusti 2024 skapas den nya instansen med `contenthub` som suffix.

Observera att det inte finns någon `author` eller `publish` i instansnamnet för Content Hub.

Klicka på instansnamnet för att visa Content Hub-produktprofilen för `AEM Assets Limited Users`.

![Content Hub produktprofil](assets/content-hub-product-profile.png)

Du kan börja lägga till användare eller användargrupper i den här produktprofilen för att ge dem tillgång till Content Hub.

>[!NOTE]
>
>Om du har etablerat Content Hub före den 14 augusti 2024 har Content Hub produktprofil `contenthub` omnämns efter `Limited Users` i stället för `delivery`.

## Aktivera Assets Ultimate för befintliga kunder {#enable-assets-ultimate-existing-customers}

Befintliga as a Cloud Service Assets-kunder kan uppgradera till Assets Ultimate genom att utföra två enkla steg. Du kan navigera till Assets as a Cloud Service program i Cloud Manager och se uppgraderingsstatus på programkortet baserat på tillgängligheten för Assets Ultimate-krediter. Om det finns tillräckligt med krediter för att uppgradera till Assets Ultimate kan du se statusen som `Assets license upgrade required`, vilket visas i följande bild:

![AEM Assets-uppgradering till Assets Ultimate](assets/aem-assets-upgrade-status-ultimate.png)

Om en befintlig kund köper en ny licens för Assets Ultimate visas uppgraderingsstatusen som `Assets license upgrade available`.

### Krav för uppgradering {#prerequisites-assets-upgrade}

Alla miljöer måste uppgraderas till den senaste versionen av AEM as a Cloud Service eller minst `2024.10.18175`-versionen. Om du inte uppfyller minimikraven kontaktar du Adobe för att gå över till AEM version.

### Uppgradera till Assets Ultimate {#upgrade-assets-ultimate}

Utför följande steg:

1. När du har växlat till minimikraven för den AEM versionen klickar du på programnamnet. Ett uppgraderingskort visas precis ovanför **[!UICONTROL Environments]**-avsnittet, vilket visas i följande bild:

   ![AEM Assets-uppgradering till Assets Ultimate](assets/aem-assets-upgrade-card.png)

1. Klicka på **[!UICONTROL Add Product Profiles]**. Cloud Manager visar alternativ för att lägga till nya produktprofiler i alla miljöer som är tillgängliga i programmet eller i enskilda miljöer.

   ![AEM Assets uppgraderingsalternativ](assets/aem-assets-upgrade-options.png)

1. Klicka på **[!UICONTROL All Environments]** om du vill lägga till de nya produktprofilerna i alla miljöer i programmet eller på **[!UICONTROL Individual Environments]** om du vill lägga till de nya produktprofilerna i de valda miljöerna.

   Om du klickar på **[!UICONTROL Individual Environments]** visas en lista med alla miljöer som är tillgängliga i programmet.

1. Klicka på ikonen Fler alternativ som motsvarar en miljö och välj **[!UICONTROL Add Product Profiles]** om du vill lägga till de nya produktprofilerna i den valda miljön.

   ![AEM Assets väljer enskilda miljöer](assets/aem-assets-individual-environments.png)

   Du kan också lägga till produktprofiler i valda miljöer genom att gå till avsnittet **[!UICONTROL Environments]**, klicka på ikonen Fler alternativ som motsvarar en miljö och välja **[!UICONTROL Add Product Profiles]**.

   Miljöns status visas `Adding Product Profiles` medan de nya produktprofilerna läggs till och sedan visas `Running` när processen är klar.

   Du måste lägga till produktprofiler i alla miljöer som är tillgängliga i programmet, enskilt eller i alla miljöer tillsammans, innan du utför nästa steg.

1. Klicka på **[!UICONTROL Upgrade]**. Alternativet **[!UICONTROL Upgrade]** visas bara när du lägger till produktprofiler i alla tillgängliga miljöer.

   ![Senaste steget i uppgraderingsprocessen](assets/aem-assets-upgrade-button.png)

   Uppgraderingsprocessen är klar och du har uppgraderat din Assets as a Cloud Service till Assets Ultimate. Status för programmet visar `Assets Ultimate`.

   ![Programstatus efter uppgradering](assets/program-status-post-upgrade.png)

Din AEM as a Cloud Service-instans på Admin Console innehåller nu följande produktprofiler:

* AEM administratörer

* AEM

* [Användare av AEM Assets Collaborator](#onboard-collaborator-users)

* [AEM Assets Power Users](#onboard-power-users)

![AEM Assets produktprofiler](assets/aem-assets-product-profiles.png)

Om du behöver aktivera Content Hub klickar du på ikonen Fler alternativ (..) på programnamnet i Cloud Manager och väljer **[!UICONTROL Edit Program]**. Expandera **[!UICONTROL Assets Ultimate]** och klicka på **[!UICONTROL Content Hub]**. Detta steg möjliggör Content Hub för Assets Ultimate. En ny instans har skapats i AEM Assets as a Cloud Service Admin Console med suffixet `delivery`:

![Ny instans för Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Om du har etablerat Content Hub före 14 augusti 2024 skapas den nya instansen med `contenthub` som suffix.

Observera att det inte finns någon `author` eller `publish` i instansnamnet för Content Hub.

Klicka på instansnamnet för att visa Content Hub-produktprofilen för `AEM Assets Limited Users`.

![Content Hub produktprofil](assets/content-hub-product-profile.png)

Du kan börja lägga till användare eller användargrupper i den här produktprofilen för att ge dem tillgång till Content Hub.

>[!NOTE]
>
>Om du har etablerat Content Hub före den 14 augusti 2024 har Content Hub produktprofil `contenthub` omnämns efter `Limited Users` i stället för `delivery`.

## Anlita användare av AEM Assets Collaborator {#onboard-collaborator-users}

AEM Assets Collaborator-användare kan arbeta med resurser från Experience Manager via integreringar av Assets som är tillgängliga för din organisation i andra Adobe-produkter och andra program än Adobe, skapa och redigera resurser med inbyggd Adobe Express och Firefly genom att utnyttja professionellt utformade mallar, märkeskit, Adobe Stock-resurser och så vidare, och få tillgång till och utnyttja godkända resurser från din organisation via AEM Assets Content Hub portal.

Anlita medarbetare:

1. Gå till Experience Manager Assets produktprofiler genom att klicka på AEM as a Cloud Service produktnamn i produktlistan på Admin Console.

1. Klicka på författarinstansen för AEM as a Cloud Service:
   ![Produktprofiler för AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Klicka på produktprofilen för medarbetare och klicka på **[!UICONTROL Add users]** för att lägga till användare eller användargrupper i produktprofilen.
   ![Användarproduktprofil](assets/aem-assets-collaborator-user-permissions.png)

1. Klicka på **[!UICONTROL Save]** om du vill spara ändringarna.

Du kan även komma åt och visa de tjänster som tilldelats till Collaborator-användare, vilket visas i följande bild:

![Tjänster för samarbetspartners](assets/aem-assets-collaborator-users.png)

`Adobe Express` och `AEM Assets Collaborator Users` tjänster är aktiverade som standard.

>[!NOTE]
>
>Du kan stänga av och aktivera för att aktivera eller inaktivera tillgängliga tjänster, enligt dina krav, men Adobe rekommenderar att du använder standardtjänsterna som är aktiverade för produktprofilerna.


## Införliva AEM Assets Power-användare {#onboard-power-users}

AEM Assets Power-användare har tillgång till alla AEM Assets-funktioner, inklusive hantering av resurser, behörigheter, metadata och övergripande styrning och automatisering av digitala resurser, kan arbeta med resurser från Experience Manager via integreringar av Assets som är tillgängliga för din organisation i andra Adobe- och icke-Adobe-program, skapa och redigera resurser med hjälp av inbyggd Adobe Express och Firefly, och utnyttja professionellt utformade mallar, varumärkeskit, Adobe Stock-resurser och så vidare, samt få tillgång till och utnyttja godkända resurser från din organisation via Content Hub portal.

Så här skaffar du Power-användare:

1. Gå till Experience Manager Assets produktprofiler genom att klicka på AEM as a Cloud Service produktnamn i produktlistan på Admin Console.

1. Klicka på författarinstansen för AEM as a Cloud Service:
   ![Produktprofiler för AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Klicka på Power users produktprofil och klicka på **[!UICONTROL Add users]** för att lägga till användare eller användargrupper i produktprofilen.
   ![Användarproduktprofil](assets/aem-assets-power-user-permissions.png)

1. Klicka på **[!UICONTROL Save]** om du vill spara ändringarna.

Du kan även få åtkomst till och visa de tjänster som tilldelats till Power-användare, enligt bilden nedan:

![Tjänster för avancerade användare](assets/aem-assets-power-users.png)

`Adobe Express` och `AEM Assets Power Users` tjänster är aktiverade som standard.

>[!NOTE]
>
>Du kan stänga av och aktivera för att aktivera eller inaktivera tillgängliga tjänster, enligt dina krav, men Adobe rekommenderar att du använder standardtjänsterna som är aktiverade för produktprofilerna.
