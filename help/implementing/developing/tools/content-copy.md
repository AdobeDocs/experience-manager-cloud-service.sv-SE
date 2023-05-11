---
title: Verktyget Innehållskopia
description: Med innehållskopieringsverktyget kan man kopiera muterbart innehåll on demand från AEM as a Cloud Service produktionsmiljöer till lägre miljöer för teständamål.
source-git-commit: 4a5470ae8fe5a8e7f615009bf5f6b180aee4669b
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 0%

---


# Verktyget Innehållskopia {#content-copy}

Med innehållskopieringsverktyget kan man kopiera muterbart innehåll on demand från AEM as a Cloud Service produktionsmiljöer till lägre miljöer för teständamål.

## Introduktion {#introduction}

Aktuella, riktiga data är värdefulla för testning, validering och för att ge användaren erkännande. Med innehållskopieringsverktyget kan du kopiera innehåll från en AEM till en staging, utveckling eller [Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) miljö för sådan testning.

Innehållet som ska kopieras definieras av en innehållsuppsättning. En innehållsuppsättning består av en lista med JCR-sökvägar som innehåller det muterbara innehåll som ska kopieras från en källredigeringstjänstmiljö till en målredigeringstjänstmiljö i samma Cloud Manager-program. Följande sökvägar tillåts i en innehållsuppsättning.

```text
/content
/conf/**/settings/wcm
/conf/**/settings/dam/cfm/models
/conf/**/settings/graphql/persistentQueries
/etc/clientlibs/fd/themes
```

När du kopierar innehåll är källmiljön en källa till sanning.

* Om innehållet har ändrats i målmiljön skrivs det över av innehållet i källan, om sökvägarna är desamma.
* Om banorna inte är samma kommer innehåll från källan att sammanfogas med innehållet i målet.

## Behörigheter {#permissions}

För att du ska kunna använda verktyget för innehållskopiering krävs vissa behörigheter i både käll- och målmiljöer.

| Innehållskopia | AEM | Distributionshanterarroll |
|---|---|---|
| Skapa och ändra [innehållsuppsättningar](#create-content-set) | Obligatoriskt | Krävs inte |
| Starta eller avbryta [innehållskopia](#copy-content) | Obligatoriskt | Obligatoriskt |

## Skapa en innehållsuppsättning {#create-content-set}

Innan något innehåll kan kopieras måste en innehållsuppsättning definieras. När innehållet har definierats kan det återanvändas för att kopiera innehållet. Följ de här stegen för att skapa en innehållsuppsättning.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Navigera till **Innehållsuppsättningar** sidan från **Miljö** skärm.

1. Tryck eller klicka på **Lägg till innehållsuppsättning** längst upp till höger på skärmen.

   ![Innehållsuppsättningar](assets/content-sets.png)

1. På **Detaljer** Ange ett namn och en beskrivning för innehållsuppsättningen och tryck eller klicka på **Fortsätt**.

   ![Information om innehållsuppsättning](assets/add-content-set-details.png)

1. På **Innehållsbanor** -fliken i guiden anger du sökvägarna till det ändringsbara innehåll som ska inkluderas i innehållsuppsättningen.

   1. Ange banan i dialogrutan **Lägg till inkluderingssökväg** fält.
   1. Tryck eller klicka på **Lägg till bana** om du vill lägga till sökvägen till innehållsuppsättningen.
   1. Tryck eller klicka på **Lägg till bana** igen om det behövs.
      * Upp till femtio banor tillåts.

   ![Lägg till banor i innehållsuppsättningen](assets/add-content-set-paths.png)

1. Om du behöver förfina eller begränsa din innehållsuppsättning kan undersökvägar uteslutas.

   1. I listan med inkluderade sökvägar trycker eller klickar du på **Lägg till exkludera delsökvägar** -ikonen bredvid banan som du vill begränsa.
   1. Ange den delbana som ska uteslutas under den valda banan.
   1. Tryck eller klicka **Uteslut bana**.
   1. Tryck eller klicka **Lägg till exkludera delsökvägar** igen om du vill lägga till ytterligare sökvägar som ska uteslutas efter behov.
      * Undantagna sökvägar måste vara relativa till den inkluderade sökvägen.
      * Det finns ingen gräns för antalet uteslutna banor.

   ![Exkludera banor](assets/add-content-set-paths-excluded.png)

1. Du kan ändra de angivna sökvägarna om det behövs.

   1. Tryck eller klicka på X bredvid de uteslutna delbanorna för att ta bort dem.
   1. Tryck eller klicka på ellipsknappen bredvid banorna för att visa **Redigera** och **Ta bort** alternativ.

   ![Redigera sökvägslista](assets/add-content-set-excluded-paths.png)

1. Tryck eller klicka **Skapa** för att skapa innehållsuppsättningen.

Innehållsuppsättningen kan nu användas för att kopiera innehåll mellan miljöer.

## Redigera en innehållsuppsättning {#edit-content-set}

Följ liknande steg som när du skapar ett innehållssteg. Istället för att trycka eller klicka **Lägg till innehållsuppsättning** väljer du en befintlig uppsättning från konsolen och väljer **Redigera** på ellipsmenyn.

![Redigera innehållsuppsättning](assets/edit-content-set.png)

Observera att när du redigerar din innehållsuppsättning kan du behöva utöka de konfigurerade sökvägarna för att visa de uteslutna delsökvägarna.

## Kopierar innehåll {#copy-content}

När en innehållsuppsättning har skapats kan du använda den för att kopiera innehåll. Följ de här stegen för att kopiera innehåll.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Navigera till **Innehållsuppsättningar** sidan från **Miljö** skärm.

1. Välj en innehållsuppsättning från konsolen och välj **Kopiera innehåll** på ellipsmenyn.

   ![Innehållskopia](assets/copy-content.png)

   >[!NOTE]
   >
   >En miljö kan inte markeras om:
   >
   >* Användaren har inte rätt behörighet.
   >* Miljön har en pågående pipeline eller en åtgärd för att kopiera innehåll.
   >* Miljön försätts i viloläge eller startar.


1. I **Kopiera innehåll** anger du källa och mål för kopieringsåtgärden.

   ![Kopierar innehåll](assets/copying-content.png)

   * Innehåll kan bara kopieras från en högre miljö till en lägre miljö eller mellan utvecklings-/RDE-miljöer där miljöhierarkin är som följer (från högst upp till lägst):
      * Produktion
      * Mellanlagring
      * Utveckling/RDE

1. Om det behövs kan du även välja att **Inkludera åtkomstkontrollistor** i kopieringsprocessen.

1. Tryck eller klicka **Kopiera**.

Kopieringsprocessen startar. Kopieringsprocessens status visas i konsolen för den valda innehållsuppsättningen.

## Innehållskopia - aktivitet {#copy-activity}

Du kan övervaka statusen för dina kopieringsprocesser i **Kopiera innehållsaktivitet** sida.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Navigera till **Kopiera innehållsaktivitet** sidan från **Miljö** skärm.

![Innehållskopia - aktivitet](assets/copy-content-activity.png)

### Status för innehållskopia {#statuses}

När du börjar kopiera innehåll kan processen ha någon av följande statusar.

| Status | Beskrivning |
|---|---|
| Pågår | Innehållskopieringen pågår |
| Misslyckades | Åtgärden Kopiera innehåll misslyckades |
| Slutförd | Innehållskopieringen har slutförts |
| Avbruten | Användaren avbryter en innehållskopia när den har startats |

### Avbryta en kopieringsprocess {#cancelling}

Om du behöver avbryta en innehållskopia efter att du har startat den kan du avbryta den.

Om du vill göra det går du till **Kopiera innehållsaktivitet** väljer du **Avbryt** på ellipsmenyn i kopieringsprocessen som du påbörjade tidigare.

![Avbryt innehållskopia](assets/content-copy-cancel.png)

>[!NOTE]
>
>När du avbryter en innehållskopia kan det resultera i en partiell kopia av innehållet i målmiljön. Detta kan göra att målmiljön inte kan användas.
>
>Om din miljö är i ett sådant läge på grund av att du har ställt in tjänsten ber vi dig kontakta Adobe kundtjänst för att få hjälp.

## Begränsningar {#limitations}

Verktyget för innehållskopiering har följande begränsningar.

* Innehåll kan inte kopieras från en lägre miljö till en högre miljö.
* Innehåll kan bara kopieras från och till redigeringstjänster.
* Det går inte att kopiera innehåll mellan program.
* Det går inte att köra samtidiga kopieringsåtgärder för innehåll i samma miljö.
* Upp till femtio sökvägar kan anges per innehållsuppsättning. Det finns ingen begränsning för uteslutna banor.
* Verktyget för innehållskopia bör inte användas som kloning eller spegling eftersom det inte kan spåra flyttat eller borttaget innehåll i källan.
* Verktyget för innehållskopiering har ingen versionshantering och kan inte automatiskt identifiera ändrat innehåll eller nyligen skapat innehåll i källmiljön i en innehållsuppsättning sedan den senaste kopieringsåtgärden.
   * Om du bara vill uppdatera målmiljön med innehållsändringar sedan den senaste kopieringsåtgärden, måste du skapa en innehållsuppsättning och ange sökvägarna i källinstansen där ändringar har gjorts sedan den senaste kopieringsåtgärden.
* Versionsinformation ingår inte i en innehållskopia.
