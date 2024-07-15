---
title: Konfigurerar din kontomiljö
description: Adobe Experience Manager (AEM) ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön.
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 4%

---

# Konfigurerar din kontomiljö {#configuring-your-account-environment}

Adobe Experience Manager (AEM) ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön.

Med alternativet [Användare](#user-settings) i [sidhuvudet](/help/sites-cloud/authoring/basic-handling.md#the-header) och den tillhörande dialogrutan [Mina inställningar](#my-preferences) kan du ändra dina användaralternativ.

Börja med att gå till alternativet [Användare](#user-settings) i sidhuvudet.

## Användarinställningar {#user-settings}

Dialogrutan **Användare** ger dig åtkomst till:

* Personifiera som
   * Med funktionen Personifiera som kan en användare arbeta för en annan användares räkning. <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* Profil
   * Det erbjuder en praktisk länk till dina användarinställningar <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [Mina inställningar](#my-preferences)
   * Ange olika inställningar som är unika för användaren

![Användarinställningar](/help/sites-cloud/authoring/assets/user-settings.png)

### Mina inställningar {#my-preferences}

Dialogrutan **Mina inställningar** öppnas med alternativet [Användare](#user-settings) i sidhuvudet.

Varje användare kan ange sina egna önskade egenskaper.

![Mina inställningar](/help/sites-cloud/authoring/assets/user-preferences.png)

* **Språk**

  Detta definierar vilket språk som ska användas för redigeringsmiljöns användargränssnitt. Välj önskat språk i listan.

* **Fönsterhantering**

  Detta definierar beteendet för att öppna fönster. Välj antingen:

   * **Flera fönster** (standard)

      * Sidorna öppnas i ett nytt fönster.

   * **Ett fönster**

      * Sidorna öppnas i det aktuella fönstret.

* **Visa skrivbordsåtgärder för Assets**

  Det här alternativet kräver att AEM datorprogram används.

* **Anteckningsfärg**

  Detta definierar den standardfärg som används när anteckningar görs.

   * Klicka på färgblocket så att du kan öppna väljaren för färgruta och välja en färg.
   * Du kan också ange hexkoden för önskad färg i fältet.

* **Relativ datumpresentation**

  För att förbättra läsbarheten återges datum inom de senaste sju dagarna som relativa datum (till exempel för tre dagar sedan) och äldre datum som exakta datum (till exempel den 20 mars 2017).

  Det här alternativet definierar hur datum i systemet visas. Följande alternativ är tillgängliga:

   * **Visa alltid exakt datum**: Det exakta datumet visas alltid (aldrig ett relativt datum).
   * **1 Dag**: Det relativa datumet visas för datum inom en dag, annars visas ett exakt datum.
   * **7 dagar (standard)**: Det relativa datumet visas för datum inom sju dagar, annars visas ett exakt datum.
   * **1 Month**: Det relativa datumet visas för datum inom en månad, annars visas ett exakt datum.
   * **1 År**: Det relativa datumet visas för datum inom ett år, annars visas ett exakt datum.
   * **Visa alltid relativt datum**: Exakta datum visas aldrig och endast relativa datum visas.

* **Aktivera kortkommandon**

  AEM har stöd för olika kortkommandon som gör redigeringen effektivare.

   * [Kortkommandon för redigering av sidor](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)
   * [Kortkommandon för konsoler](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)

  Det här alternativet aktiverar kortkommandon. Som standard är de aktiverade, men kan inaktiveras, till exempel om en användare har vissa tillgänglighetskrav.

* **Aktivera Assets hemsida**

  Det här alternativet är endast tillgängligt om systemadministratören har aktiverat Assets hemsida för hela organisationen.

* **Stock-konfiguration**

  Med det här alternativet kan du ange den önskade Adobe Stock-konfigurationen och det är bara tillgängligt om systemadministratören har aktiverat [Adobe Stock-integrering](/help/assets/aem-assets-adobe-stock.md).
