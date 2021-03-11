---
title: Beviljade åtkomsträttigheter - vad som krävs
description: Beviljade åtkomsträttigheter - vad som krävs
translation-type: tm+mt
source-git-commit: 4904d7728befd3562940b35c7d44dbf9cae87fee
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 10%

---


# Åtkomstbehörigheter har beviljats {#access-rights-granted}

Adobe skapar en **Organization**-identifierare för ditt företag i Adobe Identity Management System (IMS), där alla användare och deras behörigheter kan hanteras. Varje användare, som måste vara medlem i den här organisationen och ska få åtkomst till någon av [!UICONTROL Experience Cloud]-tjänsterna, måste ha sin egen **Adobe ID**.

## Användaridentitetstyper {#user-identity-types}

Om du vill komma igång med en Adobe ID går du till [Hantera identitetstyper för Adobe](https://helpx.adobe.com/enterprise/using/identity.html) och får detaljerade instruktioner om hur du hämtar en Adobe ID med någon av de tillgängliga identitetstyperna.

## Användare och roller {#users-and-roles}

När Adobe har skapat en organisation för företaget läggs administratören till som den första medlemmen i den här organisationen. Administratören får som standard administratörsbehörighet och tilldelas [!UICONTROL AEM Managed Services]produkten **** och en eller flera [!UICONTROL Cloud Manager]produktfiler **för**. 

1. När din systemadministratör har gett dig åtkomst till Cloud Manager får du ett e-postmeddelande som tar dig till inloggningssidan för Cloud Manager som också är tillgänglig via [Adobe Experience Cloud](https://my.cloudmanager.adobe.com/).

1. Klicka på **Hantera åtkomst** på startsidan för Cloud Manager.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

1. När du klickar på **Hantera åtkomst** navigeras du till **Admin Console** där du kan hantera användarroller och behörigheter för Cloud Manager.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin1.png)

   Från Admin Console kan du utföra SysAdmin-uppgifter som:
   * [Hantera roller](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-roles)
   * [Hantera åtkomst till författarinstans](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-access-aem)

>[!NOTE]
>Gå till avsnittet [Användare och roller](#users-roles) om du vill veta mer om användare och rolldefinitioner i Cloud Manager.

Med de här behörigheterna tilldelade är administratören nu konfigurerad med en enda inloggning (med Adobe ID) för att få åtkomst till [!UICONTROL Experience Cloud]-tjänsterna, logga in i dina AEM molnmiljöer och använda [!UICONTROL Cloud Manager].

## Användare och roller {#users-roles}

Många funktioner i [!UICONTROL Cloud Manager] kräver specifika behörigheter för att kunna användas.

[!UICONTROL Cloud Manager] definierar för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

>[!CAUTION]
>
>Om du vill använda [!UICONTROL Cloud Manager] måste du ha en Adobe ID och Adobe Experience Manager som produktkontext för Cloud Service.

### Rolldefinitioner {#role-definitions}

>[!NOTE]
>
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

I följande tabell sammanfattas rollerna:

| [!UICONTROL Cloud Manager] Roller | Beskrivning |
|--- |--- |
| Företagsägare | Ansvarig för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-skiktsfel. |
| Programhanteraren | Använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status och visa KPI:er. Kan godkänna viktiga fel i tre nivåer. |
| Distributionshanteraren | Hanterar distributionsåtgärder. Använder [!UICONTROL Cloud Manager] för att köra scen-/produktionsdistributioner. Kan redigera CI/CD-rör. Kan godkänna viktiga fel i tre nivåer. Kan få åtkomst till Git-databasen. |
| Utvecklare | Utvecklar och testar anpassad programkod. I används främst [!UICONTROL Cloud Manager] för att visa status. Kan få åtkomst till Git-databasen för kodimplementering. |
| Innehållsförfattare | I allmänhet interagerar inte med [!UICONTROL Cloud Manager]. Använd [!UICONTROL Cloud Manager] Programväljaren (när du har navigerat från [!UICONTROL Experience Cloud]) för att få åtkomst till AEM. |

### Integreringsproduktprofilen {#integration-product-profile}

Utöver ovanstående skapar Cloud Manager automatiskt en produktprofil med namnet&quot;Integrationer - Cloud Service&quot;. Den här produktprofilen används för integreringar mellan Adobe Experience Manager och andra Adobe-produkter. Den här produktprofilen **måste** inte tas bort. Om du tar bort den här profilen av misstag måste den återskapas manuellt. Visningsnamnet för den här profilen **måste** vara `CM_CS_DEFAULT`.

