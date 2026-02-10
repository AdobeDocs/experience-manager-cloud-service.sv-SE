---
title: Hur integrerar man ett anpassat formulär med Microsoft&reg; Power Automate?
description: Integrera ett anpassat formulär med Microsoft&reg; Power Automate.
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
keywords: koppla samman AEM-blanketter med automatiserad strömhantering, automatiserad strömhantering AEM Forms, integrera automatiserad strömhantering till adaptiva Forms, skicka data från adaptiva Forms till Power Automate
feature: Adaptive Forms, Foundation Components, Core Components, Edge Delivery Services
role: Admin, User, Developer
source-git-commit: 64b6ce166baa892fcddd13c2e9c8b5e7e0053815
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 0%

---


# Ansluta ett adaptivt formulär med Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/forms-microsoft-power-automate-integration) |
| AEM as a Cloud Service | Den här artikeln |

<span class="preview"> Om du använder GovCloud och behöver ansluta till en GCC-klientorganisation (Government Cloud Computing) skickar du ett e-postmeddelande från din officiella adress till aem-forms-ea@adobe.com för att begära åtkomst via tidig Adobe-program. </span>

Du kan konfigurera ett adaptivt formulär så att det kör ett Microsoft® Power Automate Cloud-flöde när du skickar in det. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden.

Den adaptiva Forms-redigeraren tillhandahåller **Anropa ett Microsoft® Power Automate-flöde** för att skicka adaptiva formulärdata, bilagor och arkivdokument som skickas till Power Automate Cloud Flow.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/aem-forms-submit-action.md).


## Fördelar

Här är några exempel på vad du kan göra efter att ha integrerat ett adaptivt formulär med Microsoft® Power Automate:

* Använd adaptiva Forms-data i en Power Automate-affärsprocess
* Använd Power Automate för att skicka inhämtade data till fler än 500 datakällor eller till något offentligt tillgängligt API
* Utför komplexa beräkningar på inhämtade data
* Spara adaptiva Forms-data i lagringssystemen enligt ett fördefinierat schema

## Förutsättningar

Följande krävs för att ansluta ett adaptivt formulär med Microsoft® Power Automate:

* Microsoft® Power Automate Premium.
* Microsoft® [Power Automate-flöde](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) med `When an HTTP request is received`-utlösaren för att ta emot data för sändning av adaptiva formulär.
* En Experience Manager-användare med behörighet för [Forms Author](/help/forms/forms-groups-privileges-tasks.md) och [Forms Admin](/help/forms/forms-groups-privileges-tasks.md)
* Det konto som används för att ansluta till Microsoft® Power Automate är ägare av det Power Automate-flöde som konfigurerats för att ta emot data från adaptiv form

## Koppla samman en Forms as a Cloud Service-instans med Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Utför följande åtgärder för att ansluta din Forms as a Cloud Service-instans till Microsoft® Power Automate:

1. [Skapa en Microsoft](#ms-power-automate-application)
1. [Skapa Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Skapa Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Publicera Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Skapa Microsoft® Azure Active Directory-program {#ms-power-automate-application}

1. Logga in på [Azure Portal](https://portal.azure.com/).
1. Välj [!UICONTROL Azure Active Directory] i den vänstra navigeringen.
1. Välj [!UICONTROL App registrations] på den vänstra panelen på sidan Standardkatalog.
1. Klicka på Nya registreringar på sidan Appregistreringar.
1. Ange namn, kontotyper som stöds och omdirigerings-URI på sidan. Ange följande i omdirigerings-URI och klicka på Spara.
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registrera ett Azure Active Directory-program](assets/power-automate-application.png)

   >[!NOTE]
   >Du kan även ange ytterligare omdirigerings-URI om det behövs från autentiseringssidan.
   > För kontotyper som stöds väljer du en innehavare, flera innehavare eller ett personligt Microsoft®-konto beroende på ditt användningssätt


1. Aktivera följande alternativ på autentiseringssidan och klicka på Spara.


   * Åtkomsttoken (används för implicita flöden)
   * ID-tokens (används för implicita och hybridflöden)

1. Klicka på `Add a permission` på API-behörighetssidan.

1. Markera `Power Automate` under Microsoft® API:er och välj följande behörigheter.
   * Flows.Manage.All
   * Flows.Read.All
   * GCC-behörighet (valfritt om du vill ansluta till en GCC-klient (Government Cloud Computing))
Klicka på `Add permissions` om du vill spara behörigheterna.
1. Klicka på `Add a permission` på API-behörighetssidan. Välj API:er som min organisation använder och sök efter `DataVerse` och aktivera `user_impersonation` Klicka `Add`-behörigheter.
1. (Valfritt) Klicka på Ny klienthemlighet på sidan Certifikat och hemligheter. På skärmen Lägg till en klienthemlighet anger du en beskrivning och en tidsperiod för när hemligheten ska upphöra och klickar på Lägg till. En hemlig sträng genereras.
1. Anteckna din organisationsspecifika [Dynamics-miljö-URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### Skapa Microsoft® Power Automate Dataverse Cloud-konfiguration {#microsoft-power-automate-dataverse-cloud-configuration}

1. I AEM Forms-författarinstans går du till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. Välj **[!UICONTROL Configuration Browser]** på sidan **[!UICONTROL Create]**.
1. I dialogrutan **[!UICONTROL Create Configuration]** anger du **[!UICONTROL Title]** för konfigurationen, aktiverar **[!UICONTROL Cloud Configurations]** och väljer **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för lagring av molntjänster. Kontrollera att mappnamnet inte innehåller något utrymme.
1. Navigera till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** och öppna konfigurationsbehållaren som du skapade i föregående steg.


   >[!NOTE]
   >
   >När du skapar ett adaptivt formulär anger du behållarnamnet i fältet **[!UICONTROL Configuration Container]**.

1. På konfigurationssidan väljer du **[!UICONTROL Create]** för att skapa [!DNL Microsoft® Power Automate Flow Service]-konfigurationen i AEM Forms.
1. På sidan **[!UICONTROL Configure Dataverse Service for Microsoft® Power Automate]** anger du **[!UICONTROL Client ID]** (kallas även program-ID), **[!UICONTROL Client Secret]**, **[!UICONTROL OAuth URL]** och **[!UICONTROL Dynamic Environment URL]**. Använd klient-ID, klienthemlighet, OAuth URL och URL för dynamisk miljö för [Microsoft® Azure Active Directory Application](#ms-power-automate-application) som du skapade i föregående avsnitt. Använd alternativet Endpoints i användargränssnittet i Microsoft® Azure Active Directory för att hitta OAuth-URL

   ![Använd alternativet Slutpunkter i Microsoft Power Automate-programmets användargränssnitt för att hitta OAuth-URL:en](assets/endpoints.png)

1. Välj **[!UICONTROL Connect]**. Logga in på ditt Microsoft® Azure-konto om du blir tillfrågad. Välj **[!UICONTROL Save]**.

### Skapa Microsoft® Power Automate Flow Service Cloud-konfiguration {#create-microsoft-power-automate-flow-cloud-configuration}

1. Navigera till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Flow Service]** och öppna konfigurationsbehållaren som du skapade i föregående avsnitt.


   >[!NOTE]
   >
   >När du skapar ett adaptivt formulär anger du behållarnamnet i fältet **[!UICONTROL Configuration Container]**.

1. På konfigurationssidan väljer du **[!UICONTROL Create]** för att skapa [!DNL Microsoft® Power Automate Flow Service]-konfigurationen i AEM Forms.

1. (Valfritt) Markera kryssrutan `Connect to Microsoft GCC` för att ansluta till GCC-klienten.

   >[!NOTE]
   >
   > Om du vill ansluta till en GCC-klient (Government Cloud Computing) väljer du GCC-behörighet i Microsoft Azure Portal.


   ![Power Automate Cloud-konfiguration](/help/forms/assets/power-automate.png)

1. På sidan **[!UICONTROL Configure Dataverse for Microsoft® Power Automate]** anger du **[!UICONTROL Client ID]** (kallas även program-ID), **[!UICONTROL Client Secret]**, **[!UICONTROL OAuth URL]** och **[!UICONTROL Dynamic Environment URL]**. Använd klient-ID, Klienthemlighet, OAuth URL och Dynamics Environment-ID. Använd alternativet Endpoints i användargränssnittet i Microsoft® Azure Active Directory för att hitta OAuth-URL:en. Öppna länken [Mina flöden](https://us.flow.microsoft.com) och välj Mina flöden använder det ID som anges i URL:en som Dynamics Environment ID.

1. Välj **[!UICONTROL Connect]**. Logga in på ditt Microsoft® Azure-konto om du blir tillfrågad. Välj **[!UICONTROL Save]**.

### Publicera både Microsoft® Power Automate Dataverse och Microsoft® Power Automate Flow Service Cloud-konfigurationer {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Navigera till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** och öppna konfigurationsbehållaren som du skapade i det tidigare avsnittet [Skapa Microsoft® Power Automate Dataverse Cloud Configuration](#microsoft-power-automate-dataverse-cloud-configuration).
1. Välj `dataverse`-konfigurationen och välj **[!UICONTROL Publish]**.
1. På sidan Publicera väljer du **[!UICONTROL All Configurations]** och sedan **[!UICONTROL Publish]**. Publicera både Power Automate Dataverse och Power Automate Flow Service Cloud-konfigurationer.

Din instans av Forms as a Cloud Service är nu ansluten till Microsoft® Power Automate. Nu kan du skicka adaptiva Forms-data till ett Power Automate-flöde.

>[!IMPORTANT]
>
>Token som används för Microsoft® Power Automate-anslutningen upphör att gälla efter 90 dagar.
>
> Om du vill att integreringen ska fungera, autentiseras och publiceras på nytt, både Microsoft® Power Automate Dataverse och Microsoft® Power Automate Flow Service, innan eller när token upphör att gälla, ska du följa de steg som beskrivs i [Publicera både Microsoft® Power Automate Dataverse och Microsoft® Power Automate Flow Service Cloud-konfigurationer](#publish-microsoft-power-automate-dataverse-cloud-configuration).
>
> Mer information om principer för token-livstid finns i [Microsoft Entra-dokumentationen om konfigurerbara token-livstider](https://learn.microsoft.com/en-us/entra/identity-platform/configurable-token-lifetimes#token-lifetime-policies-for-refresh-tokens-and-session-tokens). Om token inte förnyas kan det hända att formulärinskickning till Power Automate misslyckas.

## Skicka data till ett Power Automate-flöde med Anropa en Microsoft® Power Automate-åtgärd {#use-the-invoke-microsoft-power-automate-flow-submit-action}

När du har [anslutit din Forms as a Cloud Service-instans till Microsoft® Power Automate](#connect-forms-server-with-power-automate) utför du följande åtgärd för att konfigurera ditt adaptiva formulär så att inhämtade data skickas till ett Microsoft®-flöde när formulär skickas.

>[!BEGINTABS]

>[!TAB Foundation Component]

1. Logga in på din författarinstans, markera ditt adaptiva formulär och klicka på **[!UICONTROL Properties]**.
1. I konfigurationsbehållaren bläddrar du till och markerar den behållare som har skapats i avsnittet [Skapa Microsoft® Power Automate Dataverse Cloud Configuration](#microsoft-power-automate-dataverse-cloud-configuration) och väljer **[!UICONTROL Save and Close]**.
1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren.
1. I egenskapsbehållaren för **[!UICONTROL Submit Actions]** markerar du alternativet **[!UICONTROL Invoke a Power Automate flow]** och väljer **[!UICONTROL Power Automate flow]**. Välj önskat flöde och adaptiva Forms-data skickas till det när de skickas.

   ![Konfigurera Skicka-åtgärd](assets/submission.png)
1. Klicka på **[!UICONTROL Done]**.

>[!NOTE]
>
> Innan du skickar det adaptiva formuläret måste du se till att `When an HTTP Request is received`-utlösaren med JSON-schema under läggs till i Power Automate-flödet.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

>[!TAB Kärnkomponent]

1. Logga in på din författarinstans, markera ditt adaptiva formulär och klicka på **[!UICONTROL Properties]**.
1. I konfigurationsbehållaren bläddrar du till och markerar den behållare som har skapats i avsnittet [Skapa Microsoft® Power Automate Dataverse Cloud Configuration](#microsoft-power-automate-dataverse-cloud-configuration) och väljer **[!UICONTROL Save and Close]**.
1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. Välj alternativet **[!UICONTROL Invoke a Power Automate flow]** i listrutan Skicka-åtgärd och välj en **[!UICONTROL Power Automate flow]**. Välj önskat flöde och adaptiva Forms-data skickas till det när de skickas.

   ![Konfigurera Skicka-åtgärd](/help/forms/assets/power-automate-cc.png)
1. Klicka på **[!UICONTROL Done]**.

>[!NOTE]
>
> Innan du skickar det adaptiva formuläret måste du se till att `When an HTTP Request is received`-utlösaren med JSON-schema under läggs till i Power Automate-flödet.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

>[!TAB Universell redigerare]

1. Logga in på din Author-instans och välj ditt adaptiva formulär.
1. I konfigurationsbehållaren bläddrar du till och markerar den behållare som har skapats i avsnittet [Skapa Microsoft® Power Automate Dataverse Cloud Configuration](#microsoft-power-automate-dataverse-cloud-configuration) och väljer **[!UICONTROL Save and Close]**.
1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.
Dialogrutan **Formuläregenskaper** visas.

   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.


1. Klicka på fliken **Skicka** och välj åtgärden **[!UICONTROL Invoke a Power Automate flow]** Skicka. Välj önskat flöde och adaptiva Forms-data skickas till det när de skickas.

   ![Konfigurera Skicka-åtgärd](/help/forms/assets/power-automate-ue.png)
1. Klicka på **[!UICONTROL Save&Close]**.

>[!NOTE]
>
> Innan du skickar det adaptiva formuläret måste du se till att `When an HTTP Request is received`-utlösaren med JSON-schema under läggs till i Power Automate-flödet.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

>[!ENDTABS]

<!--
## See also

* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
* [Configure a Submit Action](configure-submit-actions-core-components.md)
* [Adobe Experience Manager Connector for Microsoft&reg; Power Automate](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)
* [Connect Adaptive Form to Microsoft&reg; Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)
-->


## Relaterade artiklar

{{af-submit-action}}

<!--

>[!MORELIKETHIS]
>
>* [Connect Adaptive Form to Microsoft Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)

-->