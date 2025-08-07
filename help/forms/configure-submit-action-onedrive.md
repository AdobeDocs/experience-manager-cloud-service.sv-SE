---
Title: How to submit data from an Adaptive Form to Microsoft&reg; OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft&reg; OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: AEM Forms OneDrive-integrering, Anslut till Microsoft OneDrive, Konfigurationsinställningar för OneDrive med AEM-formulär
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
role: User, Developer
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# Skicka ett anpassat formulär till Microsoft® OneDrive

Åtgärden **[!UICONTROL Submit to OneDrive]** kopplar ett anpassat formulär till en Microsoft® OneDrive. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till den anslutna Microsoft® OneDrive-lagringsplatsen.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/aem-forms-submit-action.md).

## Fördelar

Några av fördelarna med smidig integrering av AEM Forms och Microsoft® OneDrive är:

* Enhetsövergripande åtkomst till OneDrive säkerställer att lagrade formulärdata är tillgängliga på olika plattformar. Användarna kan komma åt inskickade data, bilagor och dokument från stationära datorer, bärbara datorer, surfplattor och mobila enheter, vilket förbättrar tillgängligheten och flexibiliteten.
* OneDrive-integrering med AEM-formulär är en tillförlitlig och skalbar lösning för effektiv datalagring. Alla inskickade anpassade formulär, som filer, bilagor och arkivdokument, kan enkelt sparas i OneDrive för att säkerställa att alla data är välorganiserade och tillgängliga.

## Anslut OneDrive till ett anpassat formulär

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

<span> Den här videon gäller endast för kärnkomponenter. Information om UE/Foundation Components finns i artikeln.</span>

Så här konfigurerar du OneDrive för AEM Forms-överföring:

1. [Skapa en OneDrive-konfiguration](#create-a-onedrive-configuration-create-onedrive-configuration): Den ansluter AEM Forms till din Microsoft® OneDrive-lagring.
2. [Använd åtgärden Skicka till OneDrive i ett adaptivt formulär](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® OneDrive.

### Skapa en OneDrive-konfiguration {#create-onedrice-configuration}

Så här ansluter du AEM Forms till din Microsoft® OneDrive-lagring:

1. Gå till din **AEM Forms Author**-instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® OneDrive]**.
1. När du har valt **[!UICONTROL Microsoft® OneDrive]** omdirigeras du till **[!UICONTROL OneDrive Browser]**.
1. Välj en **konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**. Konfigurationsguiden för OneDrive visas.

   ![Konfigurationsskärmen för OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth URL finns i [Microsoft®-dokumentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` för din app från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html` i Microsoft® Azure-portalen. Ersätt `[author-instance]` med URL:en för din Author-instans.
   * Lägg till API-behörigheterna `offline_access` och `Files.ReadWrite.All` för att ge läs-/skrivbehörigheter.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` för din app från Microsoft® Azure-portalen.

   >[!NOTE]
   >
   > Fältet **klienthemlighet** är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Om anslutningen lyckas visas meddelandet `Connection Successful`.

1. Välj nu **[!UICONTROL OneDrive Container]** > **[OneDrive-mapp]** för att spara data.

   >[!NOTE]
   >
   >* Som standard finns `forms-ootb-storage-adaptive-forms-submission` i OneDrive-behållaren.
   > * Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om den inte redan finns, genom att klicka på **Skapa mapp**.

Nu kan du använda den här lagringskonfigurationen för OneDrive för att skicka-åtgärden i ett adaptivt formulär.

### Använd OneDrive-konfiguration i ett adaptivt formulär {#use-onedrive-configuartion-in-af}

Du kan använda den skapade OneDrive-lagringskonfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en OneDrive-mapp.

>[!NOTE]
>
> * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär, där du har skapat ditt OneDrive-lagringsutrymme.
> * Om [!UICONTROL Configuration Container] inte är markerat visas de globala [!UICONTROL Storage Configuration]-mapparna i egenskapsfönstret för Skicka åtgärd.

>[!BEGINTABS]

>[!TAB Foundation Component]

Utför följande steg för att använda OneDrive-lagringskonfigurationen i ett adaptivt formulär baserat på Foundation-komponenten som:

1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/wubmit-to-onedrive-fc.png){width=50%,height=50%}
Du kan också spara DoR-dokument (Document of Record) i OneDrive.
1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Microsoft® OneDrive-lagringsplatsen.
Mappstrukturen som data ska sparas i är `/folder_name/form_name/year/month/date/submission_id/data`.

>[!TAB Kärnkomponent]

Utför följande steg för att använda OneDrive-lagringskonfigurationen i ett adaptivt formulär baserat på kärnkomponenten som:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
Du kan också spara DoR-dokument (Document of Record) i OneDrive.
1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

>[!TAB Universell redigerare]

Utför följande steg om du vill använda lagringskonfigurationen för OneDrive i ett adaptivt formulär som har skapats i Universal Editor:

1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.
Dialogrutan **Formuläregenskaper** visas.

   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.
1. Klicka på fliken **Skicka** och välj **[!UICONTROL Submit to OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/submit-to-onedrive-ue.png)
Om du väljer **Spara bifogade filer med ursprungligt namn** sparas de bifogade filerna i mappen med sina ursprungliga filnamn. Du kan också spara DoR-dokument (Document of Record) i Azure Blob Storage.
1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save&Close]**

>[!ENDTABS]

## Relaterade artiklar

{{af-submit-action}}
