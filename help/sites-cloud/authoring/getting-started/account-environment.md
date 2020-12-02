---
title: Konfigurerar din kontomiljö
description: AEM ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 4%

---


# Konfigurerar din kontomiljö {#configuring-your-account-environment}

AEM ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön.

Med alternativet [Användare](#user-settings) i [sidhuvudet](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header) och den tillhörande dialogrutan [Mina inställningar](#my-preferences) kan du ändra dina användaralternativ.

Börja med att gå till alternativet [Användare](#user-settings) i rubriken.

## Användarinställningar {#user-settings}

Dialogrutan **Användare**-inställningar ger dig tillgång till:

* Personifiera som
   * Med funktionen Personifiera som kan en användare arbeta för en annan användares räkning. <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* Profil
   * Ger en praktisk länk till dina användarinställningar <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [Mina inställningar](#my-preferences)
   * Ange olika inställningar som är unika för din användare

![Användarinställningar](/help/sites-cloud/authoring/assets/user-settings.png)

### Mina inställningar {#my-preferences}

Dialogrutan **Mina inställningar** är tillgänglig via alternativet [Användare](#user-settings) i sidhuvudet.

Varje användare kan ange vissa egenskaper för sig själv.

![Mina inställningar](/help/sites-cloud/authoring/assets/user-preferences.png)

* **Språk:**

   Detta definierar vilket språk som ska användas för redigeringsmiljöns användargränssnitt. Välj önskat språk i listan.

* **Fönsterhantering**

   Detta definierar beteendet för att öppna fönster. Välj något av följande:

   * **Flera fönster**  (standard)

      * Sidorna öppnas i ett nytt fönster.
   * **Ett fönster**

      * Sidorna öppnas i det aktuella fönstret.


* **Visa skrivbordsåtgärder för Assets**

   Det här alternativet kräver AEM datorprogram.

* **Anteckningsfärg**

   Detta definierar den standardfärg som används när anteckningar görs.

   * Klicka på färgblocket för att öppna väljaren för färgrutor och markera en färg.
   * Du kan också ange hexkoden för önskad färg i fältet.

* **Relativ datumpresentation**

   För att förbättra läsbarheten kommer AEM att återge datum inom de senaste sju dagarna som relativa datum (t.ex. för tre dagar sedan) och äldre datum som exakta datum (t.ex. den 20 mars 2017).

   Det här alternativet definierar hur datum i systemet visas. Följande alternativ är tillgängliga:

   * **Visa alltid exakt datum**: Det exakta datumet visas alltid (aldrig ett relativt datum).
   * **1 dag**: Det relativa datumet visas för datum inom en dag, annars visas ett exakt datum.
   * **7 dagar (standard)**: Det relativa datumet visas för datum inom sju dagar, i annat fall visas ett exakt datum.
   * **1 månad**: Det relativa datumet visas för datum inom en månad, annars visas ett exakt datum.
   * **1 år**: Det relativa datumet visas för datum inom ett år, annars visas ett exakt datum.
   * **Visa alltid relativt datum**: Exakta datum visas aldrig och endast relativa datum visas.

* **Aktivera kortkommandon**

   AEM stöder ett antal kortkommandon som gör redigeringen effektivare.

   * [Kortkommandon för att redigera sidor](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [Kortkommandon för konsoler](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

   Det här alternativet aktiverar kortkommandon. Som standard är de aktiverade, men kan inaktiveras om en användare har vissa tillgänglighetskrav.

* **Aktivera startsidan för resurser**

   Det här alternativet är endast tillgängligt om systemadministratören har aktiverat Assets Home Page Experience för hela organisationen.

* **Stock-konfiguration**

   Med det här alternativet kan du ange den önskade Adobe Stock-konfigurationen och det är bara tillgängligt om systemadministratören har aktiverat [Adobe Stock-integrering](/help/assets/aem-assets-adobe-stock.md).
