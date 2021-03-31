---
title: Användarroller och behörigheter
description: Den här sidan beskriver användarroller och behörigheter. Följ den här sidan om du vill lära dig hur du lägger till användare och tilldelar dem till roller i molnhanteraren.
translation-type: tm+mt
source-git-commit: 4b9476b094438acd08c945f0102b029b6792cb88
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 8%

---


# Användarroller och behörigheter {#user-roles-permissions}

## Användarroller {#user-roles}

Många funktioner i Cloud Manager kräver specifika behörigheter för att fungera och begränsar de åtgärder du vidtar i användargränssnittet utifrån de roller och behörigheter som tilldelats. I vissa fall, om du inte har behörighet att utföra en åtgärd, finns gränssnittskontrollen men är inaktiverad.

Om det finns en åtgärd som du vill utföra, men inte kan, markerar du avsnittet nedan, [Användarroller och behörigheter](#permissions). Beroende på vilket mål du har kan du kontakta systemadministratören och begära den roll du behöver.

I Cloud Manager definieras för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Business Owner
* Deployment Manager
* Program Manager
* Developer

>[!NOTE]
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

## Visa dina roller {#view-roles}

Om du vill visa din roll i Cloud Manager loggar du in på användargränssnittet i Cloud Manager, markerar din profilikon i det övre högra hörnet och väljer **Användarroller**, vilket visas i bilden nedan.

>[!NOTE]
>Mer information om hur du loggar in i Cloud Manager finns i [Navigera till Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md).

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### Integreringsproduktprofilen {#integration-product-profile}

Utöver ovanstående skapar Cloud Manager automatiskt en produktprofil med namnet&quot;Integrationer - Cloud Service&quot;. Den här produktprofilen används för integreringar mellan Adobe Experience Manager och andra Adobe-produkter. Den här produktprofilen **måste** inte tas bort. Om du tar bort den här profilen av misstag måste den återskapas manuellt. Visningsnamnet för den här profilen **måste** vara `CM_CS_DEFAULT`.


## Användarroller och behörigheter {#permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till **Git-databasen**. En företagsägare har också olika behörigheter för att lägga till och redigera program, lägga till miljöer och godkänna distributioner.

Var och en av rollerna har specifika behörigheter som är kopplade till varje roll. I följande tabell sammanfattas rollerna, de funktioner som är tillgängliga och de roller som kan utföra funktionen.

| Behörighet | Beskrivning | Företagsägare | Distributionshanteraren | Programhanteraren | Utvecklare |
|--- |--- |--- |--- |--- |--- |
| Lägg till program | Lägg till ett nytt program. | x |  |  |  |
| Skapa miljö | Skapa prod+stage, dev, environment. | x | x |  |  |
| Uppdateringsmiljö | Uppdatera Prod+Stage, Dev, Environmental. | x | x |  |  |
| Ta bort miljö | Ta bort miljöer som inte är produktiva, dev. | x | x |  |  |
| Inställningar för pipeline | Konfigurera eller redigera pipeline. |  | x |  |  |
| Körning av pipeline | Starta rörledningen. | x | x |  |  |
| Körning av pipeline | Avvisa/godkänn viktiga 3-nivåfel. | x | x | x |  |
| Körning av pipeline | Godkänn GoLive. | x | x | x |  |
| Körning av pipeline | Schemalägg produktionsdistribution. | x | x | x |  |
| Ta bort pipeline | Tillåter borttagning av en pipeline. |  | x |  |  |
| Avbryt körning | Avbryt aktuell körning. |  | x |  |  |
| Generera token för personlig åtkomst | Access Git. |  | x |  | x |