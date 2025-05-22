---
title: Huvudvy för behörighetshantering
description: Lär dig mer om det nya Touch-gränssnittet som underlättar behörighetshantering.
feature: Security
role: Admin
source-git-commit: 66ec051a2412fdbfb18dec5b79c6d5d5ca496216
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---


# Huvudvy för behörighetshantering {#principal-view-for-permissions-management}

## Ökning {#overview}

AEM introducerar behörighetshantering för användare och grupper. Huvudfunktionaliteten är densamma som det klassiska användargränssnittet, men är mer användarvänlig och effektiv.

## Åtkomst till användargränssnittet {#accessing-the-ui}

Den nya UI-baserade behörighetshanteringen nås via behörighetskortet under Säkerhet enligt nedan:

![Gränssnitt för behörighetshantering](assets/screen_shot_2019-03-17at63333pm.png)

Den nya vyn gör det enklare att se på hela uppsättningen behörigheter och begränsningar för ett givet huvudobjekt på alla sökvägar där behörigheter uttryckligen har beviljats. Detta eliminerar behovet av att gå till

CRXDE för att hantera avancerade behörigheter och begränsningar. Den har konsoliderats i samma vy.

![Behörighetsvy](assets/permissionView.png)

Det finns ett filter som gör att användaren kan välja vilken typ av huvudobjekt som ska användas för att kontrollera **Användare**, **Grupper** eller **Alla** och söka efter ett huvudkonto **.**

![Sök efter typer av huvudkonton](assets/image2019-3-20_23-52-51.png)

## Visa behörigheter för ett huvudkonto {#viewing-permissions-for-a-principal}

Med ramen till vänster kan användare rulla nedåt för att hitta ett huvudnamn eller söka efter en grupp eller en användare baserat på det valda filtret, vilket visas nedan:

![Visa behörigheter för ett huvudkonto](assets/doi-1.png)

Om du klickar på namnet visas de tilldelade behörigheterna till höger. I behörighetsrutan visas en lista med åtkomstkontrollposter på specifika sökvägar tillsammans med konfigurerade begränsningar.

![Visa ACL-lista](assets/permissionsList.png)

## Lägga till ny åtkomstkontrollpost för ett huvudkonto {#adding-new-access-control-entry-for-a-principal}

Du kan lägga till nya behörigheter genom att lägga till en åtkomstkontrollpost. Klicka bara på knappen Lägg till ACE.

![Lägg till ny åtkomstkontrollista för ett huvudkonto](assets/patru.png)

Då öppnas fönstret som visas nedan. Nästa steg är att välja en sökväg där behörigheten måste konfigureras.

![Konfigurera behörighetssökväg](assets/cinci-1.png)

Här har en sökväg valts där du kan konfigurera behörighet för **dam-users**:

![Exempelkonfiguration för dam-users](assets/sase-1.png)

När sökvägen har valts går arbetsflödet tillbaka till den här skärmen, där användaren kan välja en eller flera av de tillgängliga namnutrymmena (som `jcr`, `rep` eller `crx`) enligt nedan.

Du kan lägga till behörigheter genom att söka i textfältet och sedan välja från listan.

>[!NOTE]
>
>En fullständig lista över behörigheter och beskrivningar finns i [Administrering av användar-, grupp- och åtkomsträttigheter](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/security/user-group-ac-admin#access-right-management).

![Sökbehörighet för en angiven sökväg.](assets/image2019-3-21_0-5-47.png) ![Lägg till ny post för &quot;dam-users&quot;, vilket visas av en sökväg som är markerad i lodräta kolumner.](assets/image2019-3-21_0-6-53.png)

När listan över behörigheter har valts kan användaren välja behörighetstyp: Neka eller Tillåt, enligt nedan.

![Välj behörighet](assets/screen_shot_2019-03-17at63938pm.png) ![Välj behörighet](assets/screen_shot_2019-03-17at63947pm.png)

## Använda begränsningar {#using-restrictions}

Förutom listan över behörigheter och behörighetstypen för en viss sökväg kan du på den här skärmen även lägga till begränsningar för den detaljerade åtkomstkontrollen enligt nedan:

![Lägg till begränsningar](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Mer information om vad varje begränsning innebär finns i [Jackrabbit Oak-dokumentationen](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

Du kan lägga till begränsningar enligt nedan genom att välja begränsningstyp, ange värdet och klicka på ikonen **+** .

![Lägg till begränsningstypen](assets/sapte-1.png) ![Lägg till begränsningstypen](assets/opt-1.png)

Den nya åtkomstkontrollistan visas i åtkomstkontrollistan enligt nedan. Observera att `jcr:write` är ett aggregeringsprivilegium som inkluderar `jcr:removeNode` som lades till ovan, men som inte visas nedan som det beskrivs under `jcr:write`.

## Redigera ACE {#editing-aces}

Du kan redigera åtkomstkontrollposter genom att markera ett huvudnamn och välja det ACE som du vill redigera.

Här kan du till exempel redigera posten nedan för **dam-users** genom att klicka på pennikonen till höger:

![Lägg till begränsning](assets/image2019-3-21_0-35-39.png)

Redigeringsskärmen visas med konfigurerade ACE-adresser förmarkerade. Du kan ta bort dem genom att klicka på kryssikonen bredvid dem eller genom att lägga till nya behörigheter för den angivna sökvägen enligt nedan.

![Redigera post](assets/noua-1.png)

Här läggs privilegiet `addChildNodes` till för **dam-users** på den angivna sökvägen.

![Lägg till privilegium](assets/image2019-3-21_0-45-35.png)

Du kan spara ändringarna genom att klicka på knappen **Spara** överst till höger och ändringarna återspeglas i de nya behörigheterna för **dam-users** enligt nedan:

![Spara ändringar](assets/zece-1.png)

## Ta bort ACE {#deleting-aces}

Åtkomstkontrollposter kan tas bort om du vill ta bort alla behörigheter som tilldelats ett huvudkonto på en viss sökväg. X-ikonen bredvid ACE kan användas för att ta bort den så som visas nedan:

![Ta bort ACE:n](assets/image2019-3-21_0-53-19.png) ![Ta bort ACE:n](assets/unspe.png)

## Behörighetsvy {#permissions-view}

### Behörighetsvy för Touch UI {#touch-ui-permisions-view}

Administratörer behöver mer detaljerad kontroll och synlighet i behörighetstilldelningar på nodnivå för bättre säkerhet och hantering inom AEM. Tidigare fanns det bara en huvudbaserad vy med behörigheter som begränsar möjligheten att se hur åtkomstkontrollistor tillämpas på specifika noder eller filtrerade vyer. Den nya noden och filtrerade vyn ger ett detaljerat och kontextualiserat perspektiv för behörighetstilldelningar, vilket ger bättre hantering och granskning av säkerhetskonfigurationer. Den här funktionen förbättrar den administrativa tillsynen och förenklar behörighetshantering, förbättrar säkerheten, minskar antalet felkonfigurationer och effektiviserar åtkomstkontrollen i AEM.


Du kommer åt Permissions Touch UI-vyn genom att klicka på **Tools - Security - Permissions** enligt nedan:

![Permissions Touch UI card](assets/image-2025-2-5_15-37-59.png)

När du har startat behörighetsvyn kan du klicka på **Nodvy** eller **Filtrerad vy** i skärmens övre högra hörn beroende på visningsinställningar.

#### Nodvy

I den här vyn visas åtkomstkontrollistor för varje enskild nod(sökväg). Här finns information om:

Lokala åtkomstkontrollistor för den valda noden.
Effektiva ACL:er, som innehåller ACL:er som tillämpas på varje överordnad nod upp till roten (&quot;/&quot;).
Användarna kan lägga till, ta bort eller uppdatera åtkomstkontrollistor. När användaren klickar på en bana visas dess underordnade i den vänstra rutan, medan den högra sidan visar en tabellvy över alla åtkomstkontrollistor som är kopplade till den sökvägen.

![Nodvy](assets/image-2025-2-5_15-26-2.png)

#### Filtrerad vy

I den här vyn kan användare effektivt söka efter behörigheter på en angiven sökväg och ett visst objekt. I den här vyn kan användare enkelt avgöra vilken typ av behörigheter som tilldelats en grupp med huvudkonton för den valda sökvägen.
Dessutom ger den filtrerade vyn insikter om effektiva åtkomstkontrollistor. Den visar de åtkomstkontrollistor som är associerade med den överordnade noden för den valda sökvägen, med hänsyn tagen till det valda huvudkontot och eventuella vanliga huvudprinciper.

![Filtervy](assets/FilteredView.png)

### Behörighetsvyn i databaswebbläsaren {#the-repository-browser-permissions-view}

Behörighetsvyn kan också nås via [Databasläsaren](/help/implementing/developing/tools/repository-browser.md).

Du kan komma åt den genom att:

1. Öppna utvecklarkonsolen, klicka på fliken **Databasläsare** och sedan på **Öppna Databasläsaren**

   ![Starta Databasläsaren](assets/image-2025-2-5_15-38-47.png)

1. Klicka på fliken **Behörigheter** i databasläsaren

   ![Fliken Behörigheter](assets/image-2025-2-5_15-29-33.png)

**Obs!** Administratörsrättigheter krävs för att visa behörigheterna. Följ stegen som anges [här](/help/implementing/developing/tools/repository-browser.md#navigate-the-hierarchy-navigate-the-hierarchy) för att komma åt behörigheterna.

## Klassiska kombinationer av användargränssnittsbehörigheter {#classic-ui-privilege-combinations}

Det nya behörighetsgränssnittet använder uttryckligen den grundläggande uppsättningen behörigheter i stället för fördefinierade kombinationer som inte riktigt återspeglar de exakta underliggande behörigheter som beviljats.

Det orsakade förvirring om exakt vad som konfigureras. I följande tabell visas mappningen mellan privilegiakombinationerna från det klassiska användargränssnittet och de behörigheter som de består av:

<table>
 <tbody>
  <tr>
   <th>Klassiska kombinationer av användargränssnittsbehörigheter</th>
   <th>Behörighetsgränssnittsbehörighet</th>
  </tr>
  <tr>
   <td>Läs</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>Ändra</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>Skapa</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>Ta bort</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>Läs ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>Redigera ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>Replikera</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
