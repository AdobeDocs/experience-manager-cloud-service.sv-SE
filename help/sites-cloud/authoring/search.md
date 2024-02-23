---
title: Sök
description: Hitta materialet snabbare med omfattande sökfunktioner
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 89f23a590338561b4cfeb10b54a260a135ec2f08
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 6%

---

# Sök {#search-feature}

I författarmiljön i AEM finns olika sätt att söka efter innehåll, beroende på resurstypen.

## Grunderna i sökning {#search-basics}

Sökfunktionen finns i det övre verktygsfältet:

![Ikonen Sök](/help/sites-cloud/authoring/assets/search-icon.png)

Med sökfältet kan du:

* Sök efter ett specifikt nyckelord, en viss sökväg eller en viss tagg
* Filtrera enligt resursspecifika kriterier som ändrade datum, sidstatus, filstorlek osv.
* Definiera och använda en [sparad sökning](#saved-searches) - baserat på ovanstående kriterier

>[!NOTE]
>
>Sökningen kan även anropas med snabbtangenten `/` (snedstreck) när sökfältet visas.

## Sök och filtrera {#search-and-filter}

Så här söker och filtrerar du resurser:

1. Öppna **Sök** (med förstoringsglaset i verktygsfältet) och ange söktermen. Förslag görs och kan väljas:

   ![Sökterm](/help/sites-cloud/authoring/assets/search-term.png)

   Som standard är sökresultaten begränsade till din aktuella plats (d.v.s. konsol och relaterad resurstyp):

   ![Sökplats](/help/sites-cloud/authoring/assets/search-term-location.png)

1. Om det behövs kan du ta bort platsfiltret (markera **X** på filtret som du vill ta bort) för att söka i alla konsoler/resurstyper.
1. Resultaten visas, grupperade efter konsol och relaterad resurstyp.

   Du kan antingen välja en specifik resurs (för ytterligare åtgärd) eller gå ned på detaljnivå genom att välja önskad resurstyp, till exempel **Visa alla platser**:

   ![Sökresultat](/help/sites-cloud/authoring/assets/search-results.png)

1. Om du vill gå längre ned väljer du skensymbolen (längst upp till vänster) för att öppna sidopanelen **Filter och alternativ**.

   ![Rail, knapp](/help/sites-cloud/authoring/assets/rail-button.png)

   I enlighet med resurstypen Sök visas ett fördefinierat urval av söknings-/filtervillkor.

   På sidopanelen kan du välja:

   * Sparade sökningar
   * Sökkatalog
   * Taggar
   * Sökvillkor, till exempel Ändrade datum, Publiceringsstatus, LiveCopy-status

   >[!NOTE]
   >
   >Sökvillkoren kan variera:
   >
   >* Beroende på vilken resurstyp du har valt, är t.ex. kriterierna Resurser och Communities begripligt specialiserade.
   >* Instansen som sökningen i Forms kan anpassas (lämplig för platsen i AEM).

<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![Sidopanelen Sök](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Du kan också lägga till ytterligare söktermer.

1. Stäng **sökningen** med **X** (överst till höger).

>[!NOTE]
>
>Sökvillkoren sparas när du väljer ett objekt i sökresultatet.
>
>När du markerar ett objekt på sökresultatsidan och återgår till söksidan efter att du har använt knappen för att återställa webbläsaren, kvarstår sökvillkoren.

## Sparade sökningar {#saved-searches}

Förutom att söka efter en mängd olika aspekter kan du även spara en viss sökkonfiguration för hämtning och användning i ett senare skede:

1. Definiera sökvillkor och välj **Spara**.

   ![Spara en sökning](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Tilldela ett namn och använd sedan **Spara** bekräfta:

   ![Spara en sökning med ett namn](/help/sites-cloud/authoring/assets/search-save-name.png)

1. Din sparade sökning är tillgänglig från väljaren nästa gång du öppnar sökpanelen:

   ![Sparade sökningar](/help/sites-cloud/authoring/assets/saved-searches.png)

1. När du har sparat kan du:

   * Använd **x** (mot namnet på den sparade sökningen) för att starta en ny fråga (den sparade sökningen tas inte bort).
   * **Redigera sparad sökning**, ändra sökvillkoren och sedan **Spara** igen.

Du kan ändra sparade sökningar genom att markera den sparade sökningen och klicka på **Redigera sparad sökning** längst ned på sökpanelen.

![Ändra en sparad sökning](/help/sites-cloud/authoring/assets/saved-searches-modify.png)
