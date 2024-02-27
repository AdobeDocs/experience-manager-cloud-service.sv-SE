---
title: Konfigurera tidslinjevy för AEM Screens
description: På den här sidan beskrivs hur du konfigurerar en tidslinjevy på as a Cloud Service Skärmar.
source-git-commit: 30317d006142b3fbfc1b62fab5b4e28cb1b7dbb7
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# Konfigurera tidslinjevy för AEM Screens {#configuring-timelineview-screens}

## Introduktion {#introduction}

I det här avsnittet beskrivs hur du skapar en tidslinjevy för AEM Screens.

AEM innehåller en serie funktioner som gör att flera personer i en organisation kan samarbeta när det gäller att skapa, hantera och använda kanaler.
Tidslinjen, som finns i det vänstra fältet, beskriver kanalerna, placeringen eller någon skärmmapps livscykel i tid för att visa vad som har hänt med den under dess livstid. Detta kan filtreras ned efter typ.
På tidslinjen finns följande funktioner förutom loggarna för livscykeln.

![Använd profil i mapp](/help/screens-cloud/assets/configure/Screens-timeline1.jpg)

![Använd profil i mapp](/help/screens-cloud/assets/configure/screens-timeline2.jpg)

Så här skapar du en tidslinjevy för AEM Screens:

1. Lägga till en kommentar
1. Spara en version
1. Starta ett arbetsflöde

I följande avsnitt beskrivs dessa steg i detalj.

### Lägg till en kommentar {#addcomment}

Kommentarer som är tillgängliga via tidslinjen gör det möjligt för användare att skapa en centraliserad och historisk post för diskussioner som äger rum om kanalen, platsen eller valfri mapp på skärmen.
Kommentarerna är ett bra, konsoliderat sätt för AEM att diskutera ett sätt som kan bevaras, vilket gör att andra kan förstå viktiga beslut.

1. Navigera till kanalen som du vill lägga till en kommentar för
1. Välj kanalen
1. Öppna kolumnen Tidslinje
1. Lägg till önskad kommentar och tryck på Retur

![Lägg till en kommentar](/help/screens-cloud/assets/configure/screen-timeline3.jpg)

Informationen i tidslinjen uppdateras för att ange att kommentaren lades till.

![Lägg till en kommentar](/help/screens-cloud/assets/configure/screens-timeline4.jpg)

### Spara en version {#saveversion}

Versionshantering skapar en ögonblicksbild av en kanal vid en viss tidpunkt. Med versionshantering kan du utföra följande åtgärder:
* Skapa en kanalversion.
* Återställ en kanal till en tidigare version, till exempel:
   * om du vill ångra en ändring som du har gjort på sidan.
* Jämför den aktuella versionen av en kanal med en tidigare version:
   * för att framhäva skillnader i kanalinnehållet.


#### Skapa en ny version {#createnewversion}

1. Navigera till kanalen som du vill lägga till en kommentar för
1. Välj kanalen
1. Öppna kolumnen Tidslinje
1. Klicka på knappen (tre punkter) i kommentarsfältet längst ned.

   ![Lägg till en kommentar](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. Välj Spara som version
1. Ange en etikett och en kommentar om det behövs

   ![Lägg till en kommentar](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. Bekräfta den nya versionen med Skapa. Informationen i tidslinjen uppdateras för att ange den nya versionen.

#### Återgå till en version {#revertversion}

Så här återställer du den markerade sidan till en tidigare version:
1. Navigera till kanalen som du vill lägga till en kommentar för
1. Välj kanalen
1. Öppna kolumnen Tidslinje
1. Välj antingen Visa alla eller Versioner i listrutan Filter. Kanalversionerna för den valda kanalen visas
1. Välj den version som du vill återställa till. Möjliga alternativ visas:

   ![Lägg till en kommentar](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. Välj Återställ till den här versionen. Den valda versionen återställs och informationen på tidslinjen uppdateras

#### Förhandsgranska en version {#previewversion}

Du kan förhandsgranska en viss version:
1. Navigera till kanalen som du vill lägga till en kommentar för
1. Välj kanalen
1. Öppna kolumnen Tidslinje
1. Välj antingen Visa alla eller Versioner i listrutan Filter. Kanalversionerna för den valda kanalen visas
1. Markera den version som du vill förhandsgranska. Möjliga alternativ visas:

   ![Förhandsgranska version](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. Välj Förhandsgranska. Kanalen visas på en ny flik.

#### Jämföra en version med den aktuella versionen {#compareversion}

Du kan jämföra en specifik version med den aktuella versionen:
1. Navigera till kanalen som du vill lägga till en kommentar för
1. Välj kanalen
1. Öppna kolumnen Tidslinje
1. Välj antingen Visa alla eller Versioner i listrutan Filter. Kanalversionerna för den valda kanalen visas
1. Välj den version som du vill jämföra. Möjliga alternativ visas:

   ![Jämför version](/help/screens-cloud/assets/configure/screens-timeline9.jpg)

1. Välj Jämför med aktuell. Popup-fönstret öppnas och skillnaderna visas

### Starta ett arbetsflöde {#workflowstart}

När du redigerar kan du anropa arbetsflöden för att agera i dina kanaler. Det går också att använda mer än ett arbetsflöde.
När du använder arbetsflödet anger du följande information:
* Arbetsflödet som ska användas
* Alternativt kan du använda en titel som hjälper till att identifiera arbetsflödesinstansen i en användares inkorg
* Arbetsflödets nyttolast

#### Starta arbetsflödet

1. Navigera till kanalen som du vill lägga till en kommentar för
1. Välj kanalen
1. Öppna kolumnen Tidslinje
1. Klicka på knappen (tre punkter) med kommentarfältet längst ned

   ![Starta arbetsflöde](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. Välj Starta arbetsflöde
1. Guiden Skapa arbetsflöde öppnas och du kan ange arbetsflödesinformation
1. Välj Arbetsflödesmodell i listrutan och ange arbetsflödets titel

   ![Starta arbetsflöde](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. Fortsätt genom att klicka på Nästa
1. I omfångssteget kan du
* Lägg till innehåll om du vill lägga till ytterligare resurser i arbetsflödet
* Inkludera underordnade objekt för att ange att underordnade resurser ska inkluderas i arbetsflödet
* Ta bort markering för att ta bort resursen från arbetsflödet

  ![Starta arbetsflöde](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. Använd Skapa för att stänga guiden och skapa arbetsflödesinstansen
1. Du kan behöva utföra ytterligare åtgärder för att slutföra arbetsflödet beroende på vald arbetsflödesmodell

![Starta arbetsflöde](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
