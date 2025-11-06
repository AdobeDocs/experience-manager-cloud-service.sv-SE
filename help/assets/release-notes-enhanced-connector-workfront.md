---
title: Versionsinformation för  [!DNL Workfront for Experience Manager enhanced connector]
description: Versionsinformation för  [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 0%

---

# Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Workfront for Experience Manager enhanced connector].

Releasedatum för den senaste versionen, 1.9.21 av [!DNL Workfront for Experience Manager enhanced connector], är 25 juni 2025.

## Frigör högdagrar {#release-highlights}

Den senaste versionen av [!DNL Workfront for Experience Manager enhanced connector] innehåller följande förbättringar och felkorrigeringar:

* Förbättrad loggning av API-förfrågningar för att undvika falsk positiv loggning av autentiseringsfel.

* Anslutningsläckage för Workfront API-anrop har åtgärdats.

* Stöd för Workfront Enhanced Connector med 6.5 LTS för Java 17- och Java 21-versioner.

>[!NOTE]
>
>AEM 6.4 har fått utökat stöd. Se våra [tekniska supportperioder](https://helpx.adobe.com/support/programs/eol-matrix.html). Hitta de versioner som stöds [här](https://experienceleague.adobe.com/docs/?lang=en).

>[!IMPORTANT]
>
>Adobe rekommenderar att du [uppgraderar till den senaste 1.9.20-versionen](/help/assets/workfront-connector-install.md) av [!DNL Workfront for Experience Manager enhanced connector].

## Kända fel {#known-issues}

* När projektlänkade mappar konfigureras med AEM 6.4 sparar Experience Manager inte värdena för fälten **[!UICONTROL sub-folders]** och **[!UICONTROL Create linked folder in projects with portfolio]**. Värdet för fältet **[!UICONTROL sub-folders]** uppdateras till **[!UICONTROL undefined]** och värdet för fältet **[!UICONTROL Create linked folder in projects with portfolio]** uppdateras automatiskt till **[!UICONTROL Default Portfolio]** när konfigurationen har sparats.

* När du använder den klassiska Workfront-upplevelsen tillåter inte alternativet **[!UICONTROL Send to]** i listrutan **[!UICONTROL More]** att du väljer måldestinationen i Experience Manager. Alternativet **[!UICONTROL Send to]** fungerar korrekt med listrutan **[!UICONTROL Document Actions]**. Alternativet **[!UICONTROL Send to]** fungerar korrekt för listrutan **[!UICONTROL More]** och listrutan **[!UICONTROL Document Actions]** som är tillgänglig i den nya Workfront-upplevelsen.

## Tidigare versioner {#previous-releases}

### September 2024-utgåvan {#september-2024-release}

* MIME-typen förloras när en ny version av en befintlig resurs överförs och skapas.

### April 2024-utgåvan {#april-2024-release}

* Om HTTP-klienterna inte stängs uppstår minnesfel.


### Mars 2024-utgåvan {#march-2024-release}

* Problem uppstår vid bearbetning av överföringar av flera resurser från Workfront.
* Det går inte att lägga till avslutande citattecken när du använder Workfront för att söka efter mappar i Experience Manager resultat i `SERVER_ERROR`.

### Februari 2024-utgåvan {#february-2024-release}

* Aktivera växlingsfunktionen så att AEM Cloud-kunder kan konfigurera och konfigurera en anslutning.

* Om du stänger `resourceResolver` utan att uttryckligen stänga den underliggande sessionen orsakar det sessionsläckor i AEM-instanser. Det är viktigt att du uttryckligen stänger sessionen, eftersom det inte innebär att sessionen stängs implicit när Resurslösaren stängs automatiskt.

### Januariversion 2024 {#january-2024-release}

* [!DNL Workfront]-konfigurationen i [!DNL CRX DE] lagrar för närvarande inte `project ID`, vilket orsakar fel när skrivskyddad behörighet används. Läs mer om hur du [konfigurerar behörigheter](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#linked-folders).

* Det finns ingen offentlig dokumentation om hur du lägger till anpassade egenskaper i indexdefinitionen utanför rutan. Läs mer om att [lägga till anpassad egenskap](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#metadata-schema-mapping).

* Om du tar bort anslutningskonfigurationer på den utökade kopplingen påverkas händelsprenumerationer och andra sparade konfigurationer avsevärt, vilket gör att de pekar på en gammal URL.

* Om du installerar tilläggspaketet för formulär installeras inte **[!UICONTROL Toggle Router]**, vilket leder till att funktionen [!DNL WFEC AMS environment Toggle] inte fungerar.

* Om du aktiverar händelseprenumerationer på EWC-konfiguration uppstår upprepade API-anropsfel med felet `HTTP 400` när du konfigurerar [!DNL Workfront] förbättrad anslutning för första gången.

* Om du tar bort kommentarer om länkade mappresurser på Workfront går det inte att hitta den länkade mappsökvägen på AEM.

* Otillräckligt stöd för stora filresurser i AEM resulterar i ett problem med 4 byte-storlek.

* Ingen begärandetidsbearbetning för kritiska flöden i länkad mapp, dokumentuppdatering och anteckningsuppdatering.

### November 2023-utgåvan {#nov-2023-release}

* När du visar listan över AEM-mappar tar det mer än en minut att läsa in dialogrutan.
* Autentiserade [!DNL Workfront]-användare får upprepade gånger felloggar för autentiseringsfel.

### Oktober 2023-versionen {#october-2023-release}

* När händelseprenumerationer är inaktiverade under Avancerade inställningar kan du fortfarande välja alternativ för **Prenumerera på dokumentuppdateringshändelser för att uppdatera metadata för AEM-resurser**, **Publicera alla projektresurser till Brand Portal när projektet har slutförts** och **Aktivera kommentarsynkronisering**.

* Vissa av de mediefiler som lagras i Experience Manager återges inte korrekt när du förhandsgranskar dem i Workfront.

* När Experience Manager-anslutningen med Workfront konfigureras om skapas inte händelseprenumerationer som uppdatering av kommentarsynkronisering, borttagning och dokumentuppdatering.

* Större prestandaförbättringar i API för att skapa länkade mappar, uppdatera, aktivera länkade mappar, aktivera och inaktivera kommentarsynkronisering, spara avancerade inställningar på koppling.

### September 2023-utgåvan {#september-2023-release}

* Experience Manager förbättrade Connector hämtar alla händelseprenumerationer från Workfront samtidigt som en händelseprenumeration för ett projekt tas bort, vilket kan påverka programmets prestanda.

* När en resurs skickas från Workfront till Experience Manager är resursens MIME-typ inte inställd på attributet `dc:format` i Experience Manager.

* Workfront projekt-ID:n som lagras på Experience Manager utökade anslutning innehåller dubbletter.

### Augustiversionen 2023 {#august-2023-release}

* Det går inte att skapa länkade mappar i Experience Manager eftersom det inte finns något användarkonto kopplat till den länkade mappen.

* Ansiktsvillkor under metadatauppdateringar för en resurs i Experience Manager.

### Juniversion 2023 {#june-2023-release}

* När du har konfigurerat avancerade nätverk uppstår problem när innehåll skickas från Adobe Workfront till AEM as a Cloud Service.


### Version från maj 2023 {#may-2023-release}

* Workfront returnerar ett 409 HTTP-svar för dubblerade händelseprenumerationer baserat på ett REST-anrop från Experience Manager till Workfront, vilket leder till ett null-pekarundantag.

### April 2023-utgåvan {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.9, släppt 10 april 2023, innehåller följande uppdateringar:

* Experience Manager visar ett `DateTimeParseException`-undantag när det tar emot det senaste ändringsdatumet från Workfront när en länkad mapp skapas.

* Problem vid skapande av flera länkade projektmappar på kort tid.

* Det går inte att konfigurera en tröskelgräns för antalet nya uppsättningar av projektlänkade mappar.

### Mars 2023-utgåvan {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.8, släppt den 3 mars 2023, innehåller följande uppdateringar:

* Prestandaförbättringar i Experience Manager när länkade projektmappar skapas i Workfront.

* Kommentarsborttagningar i Workfront visas nu i Experience Manager.

* Möjlighet att hantera blockerande nya kunder på Experience Manager as a Cloud Service från att konfigurera anslutningsprogrammet.

### Januariversion 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.7, släppt 2 februari 2023, innehåller följande uppdateringar:

* Metadataredigeraren visar inte Workfront anpassade formuläregenskaper efter installationen av version 1.9.6.

* Dev Console visar `/content/dam/jcr:content/metadata/wfProjectURL not found`-felmeddelandet efter installation av den förbättrade Workfront-anslutningen och öppning av Assets hemsida.

### December 2022-utgåvan {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.6, släppt den 9 december 2009, innehåller följande uppdateringar:

**Förbättring**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront förbättrade anslutning stöder nu fulltextsökning av resurser och mappar.

**Felkorrigeringar**

* Metadata för dokumentversion synkroniseras inte korrekt mellan Workfront och Experience Manager.
* Problem vid skapande av en mapp som är länkad till Experience Manager i Workfront när mappen använder ett schema som saknar definition i den globala konfigurationen.
* Formuläret för metadataschemats svarar inte när du klickar på ett fält på grund av en inläsningstid som är längre än förväntat. Specifik OSGi-konfiguration för anpassade formulär har lagts till för att lösa problemet. Namnen på de anpassade formulär som du lägger till i metadataschemats är tillgängliga i loggarna.

### November 2022-utgåvan {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.5, släppt den 11 november, innehåller följande uppdateringar:

* När du bara definierar ett värde för ett flervärdesfält i Workfront mappas fältvärdet inte korrekt till Experience Manager.

* Experience Manager visar `SERVER_ERROR` på skärmen **[!UICONTROL Link External Files and Folders]** när resursmapparna öppnas på grund av ogiltig behörighet för `/content/dam/collections`.

* Om du aktiverar alternativet **[!UICONTROL Publish Assets to Brand Portal]** på konfigurationssidan för Workfront Enhanced Connector skapas en felaktig händelse. Händelsen tas inte bort även sedan alternativet inaktiverats.

  Så här löser du problemet:

   1. Uppgradera till version 1.9.5 av den förbättrade anslutningen.

   1. Inaktivera alternativet **[!UICONTROL Publish Assets to Brand Portal]** under avancerade inställningar.

   1. Aktivera alternativet **[!UICONTROL Publish Assets to Brand Portal]**.

   1. Ta bort fel händelseprenumerationer.

      1. Utför GET-anrop till `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Kör ett API-anrop för varje sidnummer.

      1. Sök efter följande text för att hitta händelseprenumerationer som matchar följande URL och som inte har någon `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Kontrollera att innehållet mellan `"objId": "",` och `"url"` matchar JSON-svaret. Den rekommenderade metoden är att kopiera från en händelseprenumeration som har en `objId` och sedan ta bort numret.

      1. Observera händelsens prenumerations-ID.
      1. Ta bort fel händelseprenumeration. Gör ett Delete API-anrop till `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` eftersom svarskoden innebär att felaktiga händelseprenumerationer har tagits bort.

         >[!NOTE]
         >
         >Om du redan har tagit bort fel händelseprenumerationer innan du utför de steg som beskrivs i den här proceduren kan du hoppa över det sista steget i den här proceduren.

### Oktober 2022-versionen {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.4, släppt i oktober 2007, innehåller följande uppdateringar:

* Det går inte att visa fliken Händelseprenumerationer på den utökade konfigurationssidan för anslutningsprogrammet på grund av många händelser.

* Workfront kan inte hämta listan över befintliga mappar i ett projekt, vilket resulterar i att dubblettmappar skapas.

### September 2022-utgåvan {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.3, släppt den 16 september, innehåller följande uppdateringar:

* Det går inte att överföra en fil som är större än 8 GB.
* Problem vid automatisk publicering av material som skickas från Workfront till AEM.
* Fältet Rotsökväg är inte tillgängligt för fältet Taggar när du redigerar ett standardformulär för metadataschema.
* Problem med att lägga till nya versioner i Workfront med AEM arbetsflöden.
* När du utför en sökning i AEM efter resurser som är tillgängliga i Workfront visas ett felmeddelande i AEM.
* När du skapar ett AEM-arbetsflöde för att skapa uppgifter från en resurs och inte definierar något överordnat uppgiftsnamn, skapas inte uppgiften i Workfront.

### Version från augusti 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.2, släppt den 3 augusti, innehåller följande uppdateringar:

* Arbetsflödessteget **[!UICONTROL Upload Document]** kan inte bifoga ett dokument till Workfront.

* Arbetsflödessteget **[!UICONTROL Upload Document]** kan inte bifoga ett dokument till aktiviteter och problem i Workfront. Arbetsflödessteget kopplar ett dokument till projekt.

### juliversion 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.1 innehåller följande uppdateringar:

* Stöd för autentisering mellan Experience Manager- och Workfront-program har lagts till med Workfront API-nyckel för instanser som migreras till Adobe IMS.

* När du länkar externa filer eller mappar visas felmeddelandet `SERVER_ERROR`. Felmeddelandet refererar till ett otillåtet undantag på grund av en felmatchning i API-nycklar.

* När du kör ett arbetsflöde för Skapa uppgift för en resurs visas undantaget Null-pekare i loggmeddelandena.

* När du aktiverar konfigurationsalternativet `Replace Spaces with DASH` under Avancerade inställningar i Experience Manager skapas en dubblett av mappen i Workfront.

### Juniversion 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] innehåller nu följande uppdateringar:

* När du överför via en länkad mapp eller använder åtgärden `Send To` som är tillgänglig i Workfront för att överföra resurser till Experience Manager as a Cloud Service, skadas resurserna och kan inte öppnas i Adobe Photoshop.

### Mars 2022-utgåvan {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] innehåller nu följande uppdateringar:

* Nu kan du skapa länkade mappar mellan Adobe Workfront och AEM Assets as a Cloud Service även om det finns flera projektlänkade mappkonfigurationer.

* Stöd för sidnumrering av händelseabonnemang har lagts till.

* Stöd för AEM 6.4.x har lagts till.

* Stöd för proxymiljöer har lagts till.

* Flera felkorrigeringar baseras på feedback från partner och kunder.

>[!MORELIKETHIS]
>
>* [Integrera [!DNL Workfront for Experience Manager enhanced connector] med Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
