---
title: Hur konfigurerar jag en [!DNL AEM Forms]  som en molntjänstmiljö?
description: Lär dig att konfigurera och konfigurera en  [!DNL AEM Forms] as a Cloud Service miljö.
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 42f53662-fbcf-4676-9859-bf187ee9e4af
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 1%

---

# Inbyggt i [!DNL AEM Forms] as a Cloud Service {#overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |


## Bestäm profiler {#personas-aem-forms-project}

<!-- When you sign up for the service, Adobe creates an Organization identifier for your company in the Adobe Identity Management System (IMS), where your users and their permissions can be managed. So, --> Innan du går med i en as a Cloud Service miljö i Adobe Experience Manager (AEM) Forms måste du bestämma dig för vilka personer som ska delta och strukturera ett team för ditt projekt. Ett typiskt [!DNL AEM Forms]-projektteam har följande profiler:

* **Användarupplevelse (UX) Designer**: En användarupplevelse (UX) Designer definierar format, layout och varumärkning för [!DNL AEM Forms]-resurser.

* **Forms-behandlare**: En Forms-behandlare skapar adaptiva Forms, teman och mallar utifrån den stil, layout och profilering som finns i UX Designer. Användaren skapar också och integrerar adaptiva formulär med en formulärdatamodell (FDM) och AEM arbetsflöden. En Forms-deltagare utför vanligtvis kundrelaterade uppgifter.

* **Forms-utvecklare**: En Forms-utvecklare utvecklar en anpassad formulärlösning. En Forms-utvecklare utför vanligtvis backend-utveckling som utveckling av anpassade komponenter, AEM arbetsflöden, förifyllda tjänster med mera.

* **AEM administratör**: En AEM administratör hjälper till med den övergripande konfigurationen, som att konfigurera användare, göra miljön mer skarp, konfigurera datakällor, konfigurera e-post och tredjepartsprogram. AEM kan också hjälpa till med integreringar som integrering med Adobe Analytics, Adobe Target och Adobe Sign.

* **Slutanvändare**: En användare interagerar med och skickar det publicerade formuläret, signerar skickade formulär, spårar skickade ansökningar via en webbportal och får personliga meddelanden.

<!-- While onboarding to the service, assign the following AEM groups to [!DNL AEM Forms] as a Cloud Service based on their role:

| User type | AEM group |
|---|---|
| Form Practitioner | forms-users (AEM Forms Users), template-authors, workflow-user, workflow-editors, and fdm-author  |
| UX Designer| forms-users, template-authors|
| End-User| <ul> <li>When a user must login to view and submit an Adaptive Form, add such users to forms-users group. </li> <li>When no user authentication is required to access Adaptive Forms, do not assign any group to such users. </li> </ul>| -->

## Anlita tjänsten {#onboarding}

* [Anmäl dig](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=sv-SE) till as a Cloud Service [!DNL Adobe Experience Manager].

* (Endast för sandlådor) Efter introduktion av tjänsten kan du [skapa](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/pipelines/production-pipelines.html?lang=sv-SE) och [köra](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=sv-SE) både i pipelines för produktion och icke-produktion. Den aktiverar och tillför de senaste funktionerna i [!DNL AEM Forms] as a Cloud Service till din miljö.

Du kan använda Forms as a Cloud Service för att skapa ett anpassningsbart formulär (digital registrering) eller generera en kundkommunikation. När du har slutfört [Onboarding](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=sv-SE) till as a Cloud Service [!DNL Adobe Experience Manager] utför du följande åtgärder för att aktivera funktionerna Forms - Digital registrering eller Kundkommunikation. <!--You can also enable both the features-->:

1. Logga in på Cloud Manager och öppna AEM Forms as a Cloud Service Instance.
1. Öppna alternativet Redigera program, gå till fliken Lösningar och tillägg:

   * Om du har en produktionsmiljö väljer du alternativet **[!UICONTROL Forms - Communications]** för att aktivera tillägget Forms - Digital registrering och Forms - kommunikation.

     ![Kommunikation](assets/communications.png)

   <!-- If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option. ![Addon](assets/add-on.png) -->

   * Om du har en sandlådemiljö väljer du **[!UICONTROL Forms]** för att aktivera tillägget Forms - Digital registrering och Forms - Kommunikation.

     ![Val för digital registrering](assets/forms-digital-enrollment1.png)


1. Klicka på **[!UICONTROL Update]**.
1. Kör byggprocessen. När byggprocessen är klar aktiveras den valda lösningen för din miljö.

>[!NOTE]
>
> Om du vill aktivera och konfigurera API:er för dokumentbearbetning lägger du till följande regel i [Dispatcher-konfigurationen](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Konfigurera användare {#config-users}

När du är klar med introduktionen till tjänsten loggar du in på din [!DNL AEM Forms]-as a Cloud Service miljö, öppnar författare och Publish-instanser och lägger till användare i Forms-specifika [AEM-grupper](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=sv-SE#accessing), baserat på deras personliga profil. I följande tabell visas Forms-specifika AEM, som är tillgängliga direkt i kartongen, och motsvarande användartyper. Tabellen innehåller även AEM instanstyp för varje användartyp:

| Användartyper (personas) | Användargrupper | AEM |
|---|---|---|
| Formgivare/Forms-utvecklare | <ul> <li> [!DNL forms-users] </li><li> [!DNL template-author] </li><li> [!DNL workflow-users] </li><li> [!DNL workflow-editors] </li><li> [!DNL fdm-authors] </li></ul> | Författarinstans |
| Användarupplevelse (UX) Designer | <ul> <li> [!DNL forms-users]</li><li> [!DNL template-author] </li></ul> | Författarinstans |
| AEM-administratör | <ul> <li>[!DNL aem-administrators],</li> <li>[!DNL fd-administrators] </li> </ul> | Författare och Publish-instans |
| Slutanvändare | <ul> <li>När en användare måste logga in för att visa och skicka ett adaptivt formulär lägger du till sådana användare i gruppen [!DNL forms-users]. </li> <li>När ingen användarautentisering krävs för att få tillgång till Adaptiv Forms ska du inte tilldela någon grupp till sådana användare. </li> </ul> | Författare och Publish-instans |

Mer information om Forms-specifika AEM och motsvarande behörigheter finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).

<!-- You can also create  [user groups](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=sv-SE#accessing) specific  to your organization, assign policies, and [users](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=sv-SE#accessing) to the groups. The policies help control permissions of the users that are part of the group. For information a -->

## Nästa steg {#next-steps}

[Konfigurera en lokal utvecklingsmiljö](setup-local-development-environment.md). Du kan använda en lokal utvecklingsmiljö för att skapa ett adaptivt formulär och relaterade resurser (teman, mallar, anpassade skickaåtgärder, förifyllningstjänst med mera). Och [konvertera PDF forms till anpassad Forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=sv-SE) utan att logga in i en molnutvecklingsmiljö.

<!-- ### Business unit and end-users {#business-unit-and-end-users}

| Role| Organization| Description|
|-----|-------|-----|
| UX Designer                  | Customer/System Integrator/Partner | Defines user experience design (style, layout, branding) as per organizational requirements for Adaptive Forms to allow AEM Forms practitioners to design the corresponding themes and templates.                                     |
| Forms Practitioner           | Customer                           | Authors Adaptive Forms, creates Form Data Model integrations, and creates business workflows using the Experience Manager Workflows. Typically undertakes the front-end work.                                                         |
| Business Executive - Digital | Customer                           | Responsible for business unit's product marketing strategy and revenues, main business stakeholders for digital use cases, solutions, and service offerings for the end-users, signs off on the use case implementation and delivery. |
| Customer Experience Lead     | Customer                           | Business user persona. Authors, personalizes and updates Adaptive Forms fields/rules/styling, identifies, and prioritizes business needs. Validates business use-case with SI/Partner developers/practitioners during UAT.            |
| Forms Back-Office User       | Customer                           | End-user internal to organization filling forms, participating in back-office Forms workflows such as review/approval of applications and so on.                                                                                            |
| Forms End-User               | External to customer               | Interacts with and submits the published form as end customer or citizen, signs submitted forms, tracks her applications through web portal, receives personalized interactive communications.                                        |

### Project team {#project-team}

| Role | Org | Description|
|-----|-----|-----|
| Experience Manager Administrator | System Integrator /Partner/Customer | Helps with overall installation, configures SSL certificates, configures data sources, email, and other third-party software, integrations like Adobe Analytics, Adobe Target, Automated Forms Conversion Services with Experience Manager instance. |
| Project Manager                  | System Integrator /Partner/Customer | Converts customer use-case into technical requirements, manages schedule/cost/scope for overall project.                                                                                                                                             |
| Product Owner                    | System Integrator /Partner/Customer | Prioritizes and evaluates scrum team's work for high-quality delivery on time.                                                                                                                                                                       |
| Scrum Master                     | System Integrator /Partner/Customer | Ensures agile values and processes in place to deliver on defined requirements as per prioritization by PO.                                                                                                                                          |
| Infrastructure / security expert | System Integrator /Partner/Customer | Provisions and configures best possible infrastructure, security controls and infra processes to address current and projected RASP requirements.                                                                                                    |
| Technical Architect              | System Integrator /Partner/Customer | Provides best high-level architecture and infrastructure guidance for use-case implementation and address RASP (Reliability, Availability, Scalability, and Performance) and security challenges.                                                    | -->

<!-- ## Onboard to the service {#onboarding}

[Onboard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=sv-SE) to the [!DNL Adobe Experience Manager] as a Cloud Service. 

After you onboard the service, configure a [local development environment](setup-local-development-environment.md). 

Administrators are responsible for managing Adobe software and services for their organization. Administrators grant access to developers in their organization to connect and use your [!DNL AEM Forms] as a Cloud Service program. When an administrator is provisioned for an organization, the administrator receives an email with title 'You now have administrator rights to manage Adobe software and services for your organization'. If you are an administrator, check your mailbox for email with previously mentioned title and proceed to [add users](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=sv-SE#onboarding-users-in-admin-console) by way of IMS and assign [form-specific groups](forms-groups-privileges-tasks.md) to users based on their role.

## Next step {#next-steps} -->

<!-- ## Prerequisites {#prerequisites}

If you are new to AEM as a cloud service, contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS). Once Adobe has created an organization for your company, your designated administrator is added as the first member of the organization. The administrator can setup an [!DNL AEM Forms] as a Cloud Service instance. 

## Onboard and set up a new environment {#onboard-and-setup-a-new-environment}

Log in to Cloud Manager and create a program. After the program is ready, create environments, add developers or users to environments, and run the pipeline to get the latest version of [!DNL AEM Forms] as a Cloud Service and start developing for your environment. The detailed steps are:

1. Contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS) and provide access to an administrator in your organization.
1. Configure [Automated Forms Conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=sv-SE). After a configuration is complete, a profile for Automated Forms Conversion Service is available in [Admin Console](https://adminconsole.adobe.com/).

    If the service is not available, log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not use any other ID or Federated ID to login.
    1. Click **[!UICONTROL Automated Forms Conversion Service]** option.
    1. Click **[!UICONTROL New Profile]** in the Products tab.
    1. Specify **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, and **[!UICONTROL Description]** for the profile. Click **[!UICONTROL Done]**. A profile is created. 
1. Log in to [Cloud Manager](https://experience.adobe.com/#/@marketinghub/experiencemanager) and [create a program](https://docs.adobe.com/content/help/sv-SE/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) for your organization.
1. [Create environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=sv-SE#adding-environments) within your program.
1. Log in to [Admin console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html) and add developers or users to your organization.
1. Run the [build pipeline](https://docs.adobe.com/content/help/sv-SE/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). It brings latest [!DNL Experience Manager Forms] as a Cloud Service features to your environment.
1. [Start developing](https://docs.adobe.com/content/help/sv-SE/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) and creating Adaptive Forms on [!DNL Experience Manager Forms] as a Cloud Service environment.
1. Configure the [local development environment](setup-local-development-environment.md) for rapid development

## Configure dispatcher caching {#caching}

You can make dispatcher caching related configuration changes to code on your local development instance and deploy the changes to your [!DNL AEM Forms] as a Cloud Service instance. For details, see [update dispatcher configuration](setup-local-development-environment.md).
 -->
