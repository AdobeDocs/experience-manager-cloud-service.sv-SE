---
title: Pakethanteraren
description: Lär dig grunderna i AE; pakethantering med Package Manager.
feature: Administering, Developing
role: Admin
exl-id: b5fef273-912d-41f6-a698-0231eedb2b92
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3772'
ht-degree: 0%

---

# Pakethanteraren {#working-with-packages}

Med paket kan du importera och exportera databasinnehåll. Du kan använda paket för att installera nytt innehåll, överföra innehåll mellan instanser och säkerhetskopiera databasinnehåll.

Med Package Manager kan du överföra paket mellan AEM och det lokala filsystemet i utvecklingssyfte.

## Vad är paket? {#what-are-packages}

Ett paket är en ZIP-fil som innehåller databasinnehåll i ett filsystemsserialiseringsformat, som kallas vaultserialisering, och som ger en lättanvänd och lättredigerad representation av filer och mappar. Innehåll som ingår i paketet definieras med hjälp av filter.

Ett paket innehåller även vaultmetainformation, inklusive filterdefinitioner och importkonfigurationsinformation. Ytterligare innehållsegenskaper, som inte används för paketextrahering, kan inkluderas i paketet, till exempel en beskrivning, en visuell bild eller en ikon. Dessa extra innehållsegenskaper är endast avsedda för innehållspaketkonsumenten och för informationsändamål.

>[!NOTE]
>
>Paket representerar den aktuella versionen av innehållet när paketet skapas. De innehåller inga tidigare versioner av det innehåll som AEM sparar i databasen.

## Paket i AEM as a Cloud Service {#aemaacs-packages}

Innehållspaket som skapas för AEM as a Cloud Service-program måste ha en ren separation mellan oföränderligt och muterbart innehåll. Pakethanteraren kan därför bara användas för att hantera paket som innehåller innehåll. All kod måste distribueras via Cloud Manager.

>[!NOTE]
>
>Paket kan bara innehålla innehåll. Alla funktioner (till exempel innehåll som lagras under `/apps`) måste vara [distribuerade med CI/CD-pipeline i Cloud Manager](/help/implementing/cloud-manager/deploy-code.md).

>[!IMPORTANT]
>
>Pakethanterarens gränssnitt kan returnera ett **odefinierat**-felmeddelande om det tar längre tid än 10 minuter att installera ett paket.
>
>Detta beror inte på ett fel i installationen, utan på en timeout som Cloud Servicen har för alla begäranden.
>
>Försök inte installera igen om du ser ett sådant fel. Installationen fortsätter korrekt i bakgrunden. Om du startar om installationen kan vissa konflikter uppstå vid flera samtidiga importprocesser.

Mer information om hur du hanterar paket för AEMaaCS finns i [Distribuera till AEM as a Cloud Service](/help/implementing/deploying/overview.md) i användarhandboken för distribution.

## Paketstorlek {#package-size}

Adobe rekommenderar att du inte skapar stora paket. Detta för att undvika timeoutproblem vid överföring och hämtning av paket.

Som regel bör ett paket skickas i sin helhet inom 60 sekunder. Detta ger följande formel som vägledning.

```text
MaxPackageSize (in MB) = ConnectionSpeed (in MB/s) * 60 s
```

Eftersom nätverkstrafiken varierar och alltid är mindre än det annonserade maximala teoretiska värdet kan du testa med ett hastighetstest online.

Internet-hastigheter är nästan alltid olika för överföringar och nedladdningar. Om du måste både överföra och hämta paket bör du använda det lägre värdet (vanligen överföringshastigheten) i beräkningen.

### Exempel {#example}

Med ett testverktyg för Internet-hastighet ser jag att min nuvarande överföringshastighet är cirka 100 Mbit/s.

```text
100 Mbps = 12.5 MB/s
12.5 MB/s * 60 s = 750 MB
```

Alla paket jag skapar bör därför vara mindre än 750 MB.

>[!NOTE]
>
>Nätverkshastigheterna regleras av aktuella lokala villkor. Även om du nyligen har gjort ett hastighetstest kan det faktiska dataflödet variera.
>
>Formeln är därför bara en riktlinje och din maximala rekommenderade paketstorlek kan variera.

## Pakethanteraren {#package-manager}

Pakethanteraren hanterar paketen i AEM. När du har [tilldelat de nödvändiga behörigheterna](#permissions-needed-for-using-the-package-manager) kan du använda Package Manager för olika åtgärder, bland annat för att konfigurera, bygga, hämta och installera dina paket.

### Nödvändiga behörigheter {#required-permissions}

För att kunna skapa, ändra, överföra och installera paket måste användarna ha rätt behörighet på följande noder:

* Fullständiga rättigheter exklusive borttagning på `/etc/packages`
* Noden som innehåller paketinnehållet

>[!CAUTION]
>
>Om du beviljar behörigheter för paket kan det leda till att känslig information röjs och att data går förlorade.
>
>För att begränsa de här riskerna rekommenderar vi att du endast ger särskilda gruppbehörigheter för dedikerade underträd.

### Åtkomst till Package Manager {#accessing}

Du kommer åt Package Manager på tre sätt:

1. Från AEM huvudmeny > **Verktyg** > **Distribution** > **Paket**
1. Från [CRXDE Lite](crxde.md) med hjälp av det övre växlingsfältet
1. Direkt genom åtkomst till `http://<host>:<port>/crx/packmgr/`

### Pakethanterarens användargränssnitt {#ui}

Pakethanteraren är uppdelad i fyra huvudsakliga funktionsområden:

* **Vänster navigeringspanel** - Med den här panelen kan du filtrera och sortera paketlistan.
* **Paketlista** - Det här är listan över paket i din instans som filtrerats och sorterats efter val i den vänstra navigeringspanelen.
* **Aktivitetslogg** - Den här panelen minimeras först och utökas för att beskriva aktiviteten i Package Manager, till exempel när ett paket skapas eller installeras. Det finns ytterligare knappar på fliken Aktivitetslogg för att:
   * **Rensa logg**
   * **Visa/dölj**
* **Verktygsfält** - Verktygsfältet innehåller uppdateringsknappar för den vänstra navigeringspanelen och paketlistan samt knappar för sökning, skapande och överföring av paket.

![Pakethanterarens gränssnitt](assets/package-manager-ui.png)

Om du klickar på ett alternativ i den vänstra navigeringspanelen filtreras paketlistan omedelbart.

När du klickar på ett paketnamn expanderas posten i paketlistan så att du får mer information om paketet.

![Utökad paketinformation](assets/package-expand.png)

Det finns ett antal åtgärder som kan utföras på ett paket via de verktygsfältsknappar som är tillgängliga när paketdetaljen expanderas.

* [Redigera](#edit-package)
* [Bygge](#building-a-package)
* [Installera om](#reinstalling-packages)
* [Ladda ned](#downloading-packages-to-your-file-system)

Ytterligare åtgärder är tillgängliga under knappen **Mer**.

* [Ta bort](#deleting-packages)
* [Täckning](#package-coverage)
* [Innehåll](#viewing-package-contents-and-testing-installation)
* [Radbryt](#rewrapping-a-package)
* [Andra versioner](#other-versions)
* [Avinstallera](#uninstalling-packages)
* [Testa installationen](#viewing-package-contents-and-testing-installation)
* [Validera](#validating-packages)
* [Replikera](#replicating-packages)

### Paketstatus {#package-status}

Varje post i paketlistan har en statusindikator som gör att du snabbt kan se paketets status. När du hovrar över statusen visas verktygstipset med statusinformation.

![Paketstatus](assets/package-status.png)

Om paketet har ändrats eller aldrig byggts visas statusen som en länk för att vidta snabba åtgärder för att återskapa eller installera paketet.

## Paketinställningar {#package-settings}

Ett paket är i princip en uppsättning filter och databasdata som baseras på dessa filter. Med hjälp av pakethanterarens gränssnitt kan du klicka på ett paket och sedan på knappen **Redigera** för att visa information om ett paket, inklusive följande inställningar.

* [Allmänna inställningar](#general-settings)
* [Paketfilter](#package-filters)
* [Paketberoenden](#package-dependencies)
* [Avancerade inställningar](#advanced-settings)
* [Paketskärmbilder](#package-screenshots)

### Allmänna inställningar {#general-settings}

Du kan redigera olika paketinställningar för att definiera information som paketbeskrivning, beroenden och providerinformation.

Dialogrutan **Paketinställningar** är tillgänglig via knappen **Redigera** när du [skapar](#creating-a-new-package) eller [redigerar](#viewing-and-editing-package-information) ett paket. Klicka på **Spara** när ändringarna har gjorts.

![Dialogrutan Redigera paket, allmänna inställningar](assets/general-settings.png)

| Fält | Beskrivning |
|---|---|
| Namn | Paketets namn |
| Grupp | När du organiserar paket kan du ange namnet på en ny grupp eller välja en befintlig grupp |
| Version | Text som ska användas för versionen |
| Beskrivning | En kort beskrivning av paketet som tillåter formatering med HTML-kod |
| Miniatyrbild | Ikonen som visas med paketlistan |

### Paketfilter {#package-filters}

Filter identifierar databasnoderna som ska inkluderas i paketet. En **filterdefinition** anger följande information:

* **Rotsökvägen** för innehållet som ska inkluderas
* **Regler** som innehåller eller exkluderar specifika noder under rotsökvägen

Lägg till regler med knappen **+**. Ta bort regler med knappen **-**.

Regler tillämpas i den ordning de har, så att de kan placeras efter behov med pilknapparna **Upp** och **Ned** .

Filter kan innehålla noll eller flera regler. När inga regler har definierats innehåller paketet allt innehåll under rotsökvägen.

Du kan definiera en eller flera filterdefinitioner för ett paket. Använd mer än ett filter för att inkludera innehåll från flera rotsökvägar.

![Fliken Filter](assets/edit-filter.png)

När du skapar regler definierar du ett reguljärt uttryck (kallas även regex, regexp eller rationellt uttryck) för att ange alla noder som du vill ta med eller exkludera.

| Regeltyp | Beskrivning |
|---|---|
| include | Inkludera kommer att inkludera alla filer och mappar i den angivna katalogen som matchar det reguljära uttrycket. Inkludera **inkluderar inte** andra filer eller mappar från den angivna rotsökvägen. |
| exclude | Uteslut exkluderar alla filer och mappar som matchar det reguljära uttrycket. |

Paketfilter definieras oftast när du först [skapar paketet](#creating-a-new-package). De kan emellertid också redigeras senare, och därefter bör paketet byggas om för att uppdatera innehållet baserat på de nya filterdefinitionerna.

>[!TIP]
>
>Ett paket kan innehålla flera filterdefinitioner så att noder från olika platser enkelt kan kombineras till ett paket.

>[!TIP]
>
>Bakgrundsinformation finns i dokumentationen för [Apache Jackrabbit - Workspace Filter](https://jackrabbit.apache.org/filevault/filter.html).

### Beroenden {#dependencies}

![Fliken Beroenden](assets/dependencies.png)

| Fält | Beskrivning | Exempel/detaljer |
|---|---|---|
| Testat med | Det produktnamn och den version som det här paketet har eller är kompatibelt med. | `AEMaaCS` |
| Åtgärdade problem | Ett textfält som innehåller information om fel som har åtgärdats med det här paketet, en bugg per rad | - |
| Beroende på | Visar andra paket som är nödvändiga så att det aktuella paketet körs som förväntat vid installationen | `groupId:name:version` |
| Ersätter | En lista över borttagna paket som det här paketet ersätter | `groupId:name:version` |

### Avancerade inställningar {#advanced-settings}

![Fliken Avancerade inställningar](assets/advanced-settings.png)

| Fält | Beskrivning | Exempel/detaljer |
|---|---|---|
| Namn | Namnet på paketets leverantör | `WKND Media Group` |
| URL | URL för providern | `https://wknd.site` |
| Länk | Paketspecifik länk till en providersida | `https://wknd.site/package/` |
| Kräver | Definierar om det finns några begränsningar när paketet installeras | **Admin** - Paketet får bara installeras med administratörsbehörighet <br>**Starta om** - AEM måste startas om efter att paketet har installerats |
| AC-hantering | Anger hur åtkomstkontrollsinformationen som definieras i paketet hanteras när paketet importeras | **Ignorera** - Bevara ACL:er i databasen <br>**Skriv över** - Skriv över ACL:er i databasen <br>**Merge** - Sammanfoga båda uppsättningarna ACL:er <br>**MergePreserve** - Lägg samman åtkomstkontroll i innehållet med den som följer med paketet genom att lägga till åtkomstkontrollposter för objekt som inte finns i innehållet <br>**Rensa**} - Rensa åtkomstkontrollistor |

### Paketskärmbilder {#package-screenshots}

Du kan bifoga flera skärmbilder till ditt paket för att få en visuell representation av hur innehållet ser ut.

![Fliken Skärmbilder](assets/screenshots.png)

## Paketåtgärder {#package-actions}

Det finns många åtgärder som kan utföras på ett paket.

### Skapa ett paket {#creating-a-new-package}

1. [Åtkomst till pakethanteraren](#accessing).

1. Klicka på **Skapa paket**.

   >[!TIP]
   >
   >Om din instans har många paket kan det finnas en mappstruktur på plats. I sådana fall är det enklare att navigera till den önskade målmappen innan du skapar det nya paketet.

1. Ange följande fält i dialogrutan **Nytt paket**:

   ![Dialogrutan Nytt paket](assets/new-package-dialog.png)

   * **Paketnamn** - Välj ett beskrivande namn som hjälper dig (och andra) att enkelt identifiera innehållet i paketet.

   * **Version** - Det här är ett textfält där du kan ange en version. Detta läggs till paketnamnet för att bilda zip-filens namn.

   * **Grupp** - Det här är målgruppens (eller mappens) namn. Med grupper kan du ordna dina paket. En mapp skapas för gruppen om den inte redan finns. Om du lämnar gruppnamnet tomt skapas paketet i huvudpaketlistan.

1. Klicka på **OK** för att skapa paketet.

1. AEM listar det nya paketet högst upp i paketlistan.

   ![Nytt paket](assets/new-package.png)

1. Klicka på **Redigera** för att definiera innehållet i [paketet](#package-contents). Klicka på **Spara** när du har redigerat inställningarna.

1. Du kan nu [bygga](#building-a-package) ditt paket.

Det är inte obligatoriskt att omedelbart skapa paketet efter att det har skapats. Ett obyggt paket innehåller inget innehåll och består endast av filterdata och andra metadata för paketet.

>[!TIP]
>
>Adobe rekommenderar att [inte skapar stora paket](#package-size) för att undvika timeout.

### Skapa ett paket {#building-a-package}

Ett paket byggs ofta samtidigt som du [skapar paketet](#creating-a-new-package), men du kan gå tillbaka vid ett senare tillfälle för att antingen skapa eller återskapa paketet. Detta kan vara användbart om innehållet i databasen har ändrats eller om paketfiltren har ändrats.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Klicka på **Skapa**. En dialogruta innehåller en fråga om du vill bekräfta att du vill skapa paketet eftersom allt befintligt paketinnehåll skrivs över.

1. Klicka på **OK**. AEM skapar paketet och visar allt innehåll som lagts till i paketet på samma sätt som i aktivitetslistan. När AEM är klar visas en bekräftelse på att paketet har skapats och (när du stänger dialogrutan) information om paketlistan uppdateras.

>[!TIP]
>
>Adobe rekommenderar att [inte skapar stora paket](#package-size) för att undvika timeout.

### Redigera ett paket {#edit-package}

När ett paket har överförts till AEM kan du ändra dess inställningar.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Klicka på **Redigera** och uppdatera **[paketinställningarna](#package-settings)** efter behov.

1. Klicka på **Spara** för att spara.

Du kan behöva [återskapa paketet](#building-a-package) för att uppdatera innehållet baserat på dina ändringar.

### Rewrapping a Package {#rewrapping-a-package}

När ett paket har byggts kan det paketeras om. När du gör om en paketering ändras paketinformationen utan miniatyrbild, beskrivning och så vidare, utan att paketinnehållet ändras.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Klicka på **Redigera** och uppdatera **[paketinställningarna](#package-settings)** efter behov.

1. Klicka på **Spara** för att spara.

1. Klicka på **Mer** > **Radbrytning** så uppmanas du bekräfta åtgärden i en dialogruta.

### Visa andra paketversioner {#other-versions}

Eftersom alla versioner av ett paket visas i listan som alla andra paket, kan pakethanteraren hitta andra versioner av ett valt paket.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Klicka på **Mer** > **Andra versioner** så öppnas en dialogruta med en lista över andra versioner av samma paket med statusinformation.

### Innehåll och testinstallation för visning av paket {#viewing-package-contents-and-testing-installation}

När du har skapat ett paket kan du visa innehållet.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Om du vill visa innehållet klickar du på **Mer** > **Innehåll** och Pakethanteraren visar hela innehållet i paketet i aktivitetsloggen.

   ![Paketet innehåller](assets/package-contents.png)

1. Om du vill utföra en torr installation klickar du på **Mer** > **Testa installationen** och Pakethanteraren rapporterar resultaten i aktivitetsloggen som om installationen utfördes.

   ![Testa installationen](assets/test-install.png)

### Hämtar paket till filsystemet {#downloading-packages-to-your-file-system}

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Klicka på knappen **Hämta** eller på paketets länkade filnamn i paketinformationsområdet.

1. AEM hämtar paketet till datorn.

>[!TIP]
>
>Adobe rekommenderar att [inte skapar stora paket](#package-size) för att undvika timeout.

### Överför paket från filsystemet {#uploading-packages-from-your-file-system}

1. [Åtkomst till pakethanteraren](#accessing).

1. Välj den gruppmapp som du vill att paketet ska överföras till.

1. Klicka på knappen **Överför paket**.

1. Ange nödvändig information om det överförda paketet.

   ![Dialogrutan Paketöverföring.](assets/package-upload-dialog.png)

   * **Paket** - Använd knappen **Bläddra..** för att välja det paket som krävs från det lokala filsystemet.
   * **Tvinga överföring** - Om det redan finns ett paket med det här namnet framtvingar det här alternativet överföringen och skriver över det befintliga paketet.

1. Klicka på **OK** och det valda paketet överförs och paketlistan uppdateras därefter.

Paketinnehållet finns nu på AEM, men för att göra innehållet tillgängligt måste du [installera paketet](#installing-packages).

>[!TIP]
>
>Adobe rekommenderar att [inte skapar stora paket](#package-size) för att undvika timeout.

### Verifierar paket {#validating-packages}

Eftersom paket kan ändra befintligt innehåll är det ofta användbart att validera dessa ändringar innan du installerar.

#### Valideringsalternativ {#validation-options}

Pakethanteraren kan utföra följande valideringar:

* [OSGi-paketimporter](#osgi-package-imports)
* [Övertäckningar](#overlays)
* [ACL:er](#acls)

##### Validera OSGi-paketimporter {#osgi-package-imports}

>[!NOTE]
>
>Eftersom paket inte kan användas för att distribuera kod i AEMaaCS är **OSGi-paketimporter**-valideringen onödig.

**Vad är markerat**

Den här valideringen undersöker paketet för alla JAR-filer (OSGi-paket), extraherar deras `manifest.xml` (som innehåller de versionshanteringsberoenden som OSGi-paketet är beroende av) och verifierar den AEM instansen exporterar dessa beroenden med rätt versioner.

**Så här rapporteras det**

Alla versionshanteringsberoenden som inte kan uppfyllas av den AEM instansen visas i aktivitetsloggen för Package Manager.

**Fellägen**

Om beroenden inte uppfylls startar inte OSGi-paketen med dessa beroenden. Detta resulterar i en trasig programdistribution eftersom allt som förlitar sig på det ostartade OSGi-paketet i sin tur inte fungerar som det ska.

**Fellösning**

För att åtgärda fel på grund av att OSGi-paket inte är nöjda måste beroendeversionen i paketet med otillfredsställande importer justeras.

##### Validera övertäckningar {#overlays}

>[!NOTE]
>
>Eftersom paket inte kan användas för att distribuera kod i AEMaaCS behövs inte validering av **Overlays**.

**Vad är markerat**

Valideringen avgör om det paket som installeras innehåller en fil som redan finns i AEM.

Med en befintlig övertäckning på `/apps/sling/servlet/errorhandler/404.jsp`, till exempel, ett paket som innehåller `/libs/sling/servlet/errorhandler/404.jsp`, så att den ändrar den befintliga filen på `/libs/sling/servlet/errorhandler/404.jsp`.

**Så här rapporteras det**

Alla sådana övertäckningar beskrivs i aktivitetsloggen för Package Manager.

**Fellägen**

Ett feltillstånd innebär att paketet försöker distribuera en fil som redan är överlagrad, vilket innebär att ändringarna i paketet åsidosätts (och därmed&quot;döljs&quot;) av övertäckningen och inte börjar gälla.

**Fellösning**

För att lösa det här problemet måste den som ansvarar för övertäckningsfilen i `/apps` granska ändringarna i den överliggande filen i `/libs` och införliva ändringarna efter behov i övertäckningen ( `/apps`) och distribuera den överliggande filen på nytt.

>[!NOTE]
>
>Valideringsfunktionen kan inte stämma av om det överlagda innehållet har integrerats korrekt i överläggsfilen. Valideringen fortsätter därför att rapportera om konflikter även efter att nödvändiga ändringar har gjorts.

##### Validera åtkomstkontrollistor {#acls}

**Vad är markerat**

Valideringen kontrollerar vilka behörigheter som läggs till, hur de hanteras (sammanfoga/ersätt) och om de aktuella behörigheterna påverkas.

**Så här rapporteras det**

Behörigheterna beskrivs i aktivitetsloggen för Package Manager.

**Fellägen**

Inga explicita fel kan anges. Valideringen anger helt enkelt om nya ACL-behörigheter läggs till eller påverkas av att paketet installeras.

**Fellösning**

Med hjälp av den information som valideringen ger kan de påverkade noderna granskas i CRXDE och åtkomstkontrollistorna kan justeras i paketet efter behov.

>[!CAUTION]
>
>Som god praxis rekommenderas att paket inte påverkar AEM-tillhandahållna åtkomstkontrollistor eftersom detta kan leda till oväntat beteende.

#### Utför validering {#performing-validation}

Paketvalidering kan göras på två olika sätt:

* [Via pakethanterarens gränssnitt](#via-package-manager).
* [Via HTTP-POST-begäran, till exempel med cURL](#via-post-request).

Validering ska alltid ske efter att paketet har överförts, men innan det installeras.

##### Paketvalidering via Package Manager {#via-package-manager}

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Validera paketet genom att klicka på **Mer** > **Validera**

1. I den modala dialogrutan som sedan visas använder du kryssrutorna för att välja valideringstyp(er) och påbörjar valideringen genom att klicka på **Validera**.

1. De valda valideringarna körs sedan och resultaten visas i aktivitetsloggen för Package Manager.

##### Paketvalidering via HTTP-POST-begäran {#via-post-request}

Begäran om POST har följande format.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

Parametern `type` kan vara en kommaavgränsad, osorterad lista som består av:

* `osgiPackageImports`
* `overlays`
* `acls`

Värdet för `type` är som standard `osgiPackageImports` om det inte skickas explicit.

När du använder cURL kör du en programsats som liknar följande:

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

Vid validering via POST skickas svaret tillbaka som ett JSON-objekt.

### Täckning för visningspaket {#package-coverage}

Paket definieras av sina filter. Du kan låta Pakethanteraren tillämpa filter från ett paket på det befintliga databasinnehållet för att visa vilket innehåll i databasen som omfattas av paketets filterdefinition.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen från paketlistan genom att klicka på paketnamnet.

1. Klicka på **Mer** > **Disponering**.

1. Täckningsinformationen visas i aktivitetsloggen.

### Installerar paket {#installing-packages}

När du överför ett paket läggs bara paketinnehållet till i databasen, men det är inte tillgängligt. Du måste installera det överförda paketet för att kunna använda paketets innehåll.

>[!CAUTION]
>
>Om du installerar ett paket kan befintligt innehåll skrivas över eller tas bort. Överför bara ett paket om du är säker på att det inte tar bort eller skriver över innehåll som du behöver.

Innan du installerar paketet skapas ett ögonblicksbildspaket som innehåller det överskrivna innehållet automatiskt i Package Manager. Den här ögonblicksbilden installeras om du avinstallerar paketet.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen för det paket som du vill installera från paketlistan genom att klicka på paketnamnet.

1. Klicka antingen på knappen **Installera** i objektinformationen eller på länken **Installera** i paketstatusen.

1. En dialogruta begär bekräftelse och tillåter att ytterligare alternativ anges.

   * **Endast extrahera** - Extrahera endast paketet så att ingen ögonblicksbild skapas och därför inte kan avinstalleras
   * **Spara tröskelvärde** - Antal tillfälliga noder tills automatiskt sparande aktiveras (öka om du stöter på undantag för samtidig ändring)
   * **Extrahera delpaket** - Aktivera automatisk extrahering av delpaket
   * **Åtkomstkontrollhantering** - Anger hur åtkomstkontrollsinformationen som definieras i paketet hanteras när paketet installeras (alternativen är desamma som de [avancerade paketinställningarna](#advanced-settings))
   * **Beroendehantering** - Ange hur beroenden ska hanteras under installationen

1. Klicka på **Installera**.

1. Aktivitetsloggen visar installationsförloppet.

När installationen är klar och slutförd uppdateras paketlistan och ordet **Installed** visas i paketstatusen.

### Paket installeras om {#reinstalling-packages}

När du installerar om paket utförs samma steg på ett redan installerat paket som bearbetas när [paketet](#installing-packages) först installeras.

### Filsystembaserad överföring och installation {#file-system-based-upload-and-installation}

Du kan helt och hållet avstå från Package Manager när du installerar paket. AEM kan identifiera paket som har placerats på en viss plats i värddatorns lokala filsystem och överföra och installera dem automatiskt.

1. Under AEM installationsmapp finns det en `crx-quicksart`-mapp tillsammans med jar- och `license.properties`-filen. Skapa en mapp med namnet `install` under `crx-quickstart` som resulterar i sökvägen `<aem-home>/crx-quickstart/install`.

1. Lägg till dina paket i den här mappen. De laddas automatiskt upp och installeras på din instans.

1. När överföringen och installationen är klar kan du se paketen i Package Manager som om du hade använt gränssnittet i Package Manager för att installera dem.

Om instansen körs börjar överföringen och installationen omedelbart när du lägger till den i paketet i mappen `install`

Om instansen inte körs installeras paket som placeras i mappen `install` vid start i alfabetisk ordning.

### Avinstallerar paket {#uninstalling-packages}

När du avinstallerar paketet återställs innehållet i databasen till ögonblicksbilden som gjorts automatiskt av Package Manager före installationen.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen för det paket som du vill avinstallera från paketlistan genom att klicka på paketnamnet.

1. Klicka på **Mer** > **Avinstallera** om du vill ta bort innehållet i det här paketet från databasen.

1. En dialogruta begär bekräftelse och visar alla ändringar som görs.

1. Paketet tas bort och ögonblicksbilden tillämpas. Processens förlopp visas i aktivitetsloggen.

### Tar bort paket {#deleting-packages}

Om du tar bort ett paket tas endast dess information bort från Pakethanteraren. Om det här paketet redan har installerats tas det installerade innehållet inte bort.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen för det paket som du vill ta bort från paketlistan genom att klicka på paketnamnet.

1. AEM ber om en bekräftelse på att du vill ta bort paketet. Bekräfta borttagningen genom att klicka på **OK**.

1. Paketinformationen tas bort och information rapporteras i aktivitetsloggen.

### Replikerar paket {#replicating-packages}

Replikera innehållet i ett paket för att installera det på publiceringsinstansen.

1. [Åtkomst till pakethanteraren](#accessing).

1. Öppna paketinformationen för det paket som du vill replikera från paketlistan genom att klicka på paketnamnet.

1. Klicka på **Mer** > **Replikera**.

1. Paketet replikeras och information rapporteras i aktivitetsloggen.

## Programvarudistribution {#software-distribution}

AEM kan användas för att skapa och dela innehåll i AEMaaCS-miljöer.

[Programvarudistribution](https://downloads.experiencecloud.adobe.com) innehåller AEM paket för den lokala utvecklingen AEM SDK. AEM som tillhandahålls vid programvarudistribution får inte installeras i AEMaaCS-molnmiljöer om inte Adobe Support uttryckligen har godkänt detta.

Mer information finns i [dokumentationen för programvarudistribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html).
