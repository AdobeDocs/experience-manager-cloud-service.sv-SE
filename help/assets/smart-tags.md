---
title: Hur lägger jag till smarta taggar till resurser i AEM?
description: Lägg in smarta taggar i AEM med en artificiellt intelligent tjänst som lägger in kontextuella och beskrivande taggar.
contentOwner: AG
feature: Smart Tags
role: Admin, User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 4%

---


# Lägga till smarta taggar till resurser i AEM {#smart-tags-assets-aem}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/enhanced-smart-tags.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Organisationer som hanterar digitalt material använder i allt högre grad taxonomistyrd vokabulär i metadata. Det innehåller i själva verket en lista med nyckelord som anställda, partners och kunder vanligtvis använder för att referera till och söka efter sina digitala resurser. Genom att tagga resurser med taxonomistyrd vokabulär kan du se till att de är lätta att identifiera och hämta i sökningar.

Jämfört med naturliga språkordsuttryck hjälper taggning som baseras på företagstaxonomi till att anpassa tillgångarna till företagets verksamhet och säkerställer att de mest relevanta resurserna visas i sökningar. En biltillverkare kan t.ex. märka bilderna med modellnamn så att endast relevanta bilder visas när de genomsöks för att utforma en kampanj.

I bakgrunden använder funktionen det artificiellt intelligenta ramverket i [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) för att utbilda sin bildigenkänningsalgoritm i din taggstruktur och din företagsklonomi. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser. AEM använder automatiskt smarta taggar på överförda resurser som standard.

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## Resurstyper som stöds för smarta taggar i AEM {#smart-tags-supported-file-formats}

Du kan tagga följande typer av resurser:

* **Bilder**: Bilder i många format taggas med Adobe Sensei smarta innehållstjänster. Du [skapar en utbildningsmodell](#train-model) och sedan taggas de överförda bilderna automatiskt. Smarta taggar används för de filtyper som stöds och som genererar återgivningar i JPG- och PNG-format.
* **Textbaserade resurser**: [!DNL Experience Manager Assets] taggar automatiskt de textbaserade resurser som stöds när de överförs.
* **Videoresurser**: Videotaggning är aktiverat som standard i [!DNL Adobe Experience Manager] som [!DNL Cloud Service]. [Videoklipp taggas automatiskt](/help/assets/smart-tags-video-assets.md) när du överför nya videoklipp eller bearbetar om befintliga.

| Bilder (MIME-typer) | Textbaserade resurser (filformat) | Videomaterial (filformat och kodekar) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| bild/tiff | DOC | MKV (H264/AVC) |
| bild/png | DOCX | MOV (H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | PDF | FLV (H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap | |  |
| image/x-xpixmap | |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

AEM lägger automatiskt till smarta taggar i textbaserade resurser och i videoklipp som standard. Om du vill lägga till smarta taggar automatiskt till bilder utför du följande åtgärder.

* [Förstå taggmodeller och riktlinjer](#understand-tag-models-guidelines).
* [Utbilda modellen](#train-model).
* [Tagga dina digitala resurser](#tag-assets).
* [Hantera taggar och sökningar](#manage-smart-tags-and-searches).

## Förstå taggmodeller och riktlinjer {#understand-tag-models-guidelines}

En taggmodell är en grupp relaterade taggar som är kopplade till olika visuella aspekter av bilder som taggas. Taggar relaterar till de olika visuella aspekterna av bilder så att taggarna när de används hjälper dig att söka efter särskilda typer av bilder. En skosamling kan till exempel ha olika taggar, men alla taggar är relaterade till skor och kan tillhöra samma taggmodell. När märkorden används kan de hjälpa dig att hitta olika typer av skor, till exempel efter design eller efter användning. Om du vill förstå innehållsrepresentationen för en utbildningsmodell i [!DNL Experience Manager] ska du visualisera en utbildningsmodell som en entitet på den översta nivån som består av en grupp med manuellt tillagda taggar och exempelbilder för varje tagg. Varje tagg kan användas exklusivt på en bild.

Innan du skapar en taggmodell och utbildar tjänsten bör du identifiera en uppsättning unika taggar som bäst beskriver objekten i bilderna i ditt företags sammanhang. Kontrollera att resurserna i din aktuella uppsättning uppfyller [riktlinjerna för utbildning](#training-guidelines).

### Utbildningsriktlinjer {#training-guidelines}

Kontrollera att bilderna i kursuppsättningen överensstämmer med följande riktlinjer:

**Kvantitet och storlek:** Minst 10 bilder och högst 50 bilder per tagg.

**Samordning**: Kontrollera att bilderna för en tagg är visuellt lika. Det är bäst att lägga samman märkorden om samma visuella aspekter (till exempel samma typ av objekt i en bild) till en enda taggmodell. Det är till exempel ingen bra idé att tagga de här bilderna som `my-party` (för utbildning) eftersom de inte är visuellt lika.

![Illustrativa bilder som exempel på riktlinjer för utbildning](assets/do-not-localize/coherence.png)

**Täckning**: Det ska finnas tillräckligt med variation i bilderna i kursen. Tanken är att ge några exempel som är ganska olika, men som ändå är ganska olika, så att [!DNL Experience Manager] lär sig att fokusera på rätt saker. Om du använder samma tagg på bilder som ser olika ut bör du ta med minst fem exempel av varje typ. För taggen *model-down-pose* kan du t.ex. inkludera fler utbildningsbilder som liknar den markerade bilden nedan så att tjänsten kan identifiera liknande bilder mer exakt under taggningen.

![Illustrativa bilder som exempel på riktlinjer för utbildning](assets/do-not-localize/coverage_1.png)

**Distraktion/obstruktion**: Tjänsten tränar bättre på bilder som har mindre störning (framträdande bakgrunder, icke-relaterade komponenter, t.ex. objekt/personer med huvudmotivet). För taggen *casual-shoe* är till exempel den andra bilden inte en bra träningskandidat.

![Illustrativa bilder som exempel på riktlinjer för utbildning](assets/do-not-localize/distraction.png)

**Fullständighet:** Om en bild kvalificerar sig för mer än en tagg lägger du till alla tillämpliga taggar innan du inkluderar bilden för träning. För taggar som *regnrock* och *modellvy* lägger du till båda taggarna i den kvalificerade resursen innan du inkluderar den för träning.

![Illustrativa bilder som exempel på riktlinjer för utbildning](assets/do-not-localize/completeness.png)

**Antal taggar**: Adobe rekommenderar att du utbildar en modell med minst två distinkta taggar och minst tio olika bilder för varje tagg. Lägg inte till fler än 50 taggar i en enda taggmodell.

**Antal exempel**: Lägg till minst tio exempel för varje tagg. Adobe rekommenderar dock cirka 30 exempel. Högst 50 exempel per tagg stöds.

**Förhindra felaktiga positiva och konflikter**: Adobe rekommenderar att du skapar en enda taggmodell för en enskild visuell aspekt. Strukturera taggmodellerna på ett sätt som undviker överlappande taggar mellan modellerna. Använd till exempel inte vanliga taggar som `sneakers` i två olika taggmodellnamn `shoes` och `footwear`. Utbildningsprocessen skriver över en tränad taggmodell med den andra för ett vanligt nyckelord.

**Exempel**: Fler exempel på vägledning är:

* Skapa en taggmodell som endast innehåller

   * Taggar för bilmodeller.
   * Taggen för fodral för vuxna och barn.

* Skapa inte

   * En taggmodell som innehåller bilmodeller som släpptes 2019 och 2020.
   * Flera taggmodeller som innehåller samma få bilmodeller.

**Bilder som används för att utbilda**: Du kan använda samma bilder för att utbilda olika taggmodeller. Koppla emellertid inte en bild till mer än en tagg i en taggmodell. Du kan lägga till märkord i samma bild med olika märkord som tillhör olika taggmodeller.

Du kan inte ångra kursen. Riktlinjerna ovan bör hjälpa dig att välja bra bilder att utbilda.

## Ange modell för anpassade taggar {#train-model}

Följ de här stegen för att skapa och utbilda en modell för dina företagsspecifika taggar:

1. Skapa nödvändiga taggar och rätt taggstruktur. Överför relevanta bilder i DAM-databasen.
1. Gå till **[!UICONTROL Assets]** > **[!UICONTROL Smart Tag Training]** i användargränssnittet för [!DNL Experience Manager].
1. Klicka på **[!UICONTROL Create]**. Ange **[!UICONTROL Title]**, **[!UICONTROL Description]**.
1. Klicka på mappikonen i fältet **[!UICONTROL Tags]**. Ett popup-fönster öppnas.
1. Sök efter eller välj lämpliga taggar från de befintliga taggarna i `cq-tags` som du vill lägga till i modellen. Klicka på **[!UICONTROL Next]**.

   >[!NOTE]
   >
   >Du kan sortera taggstrukturen i stigande eller fallande ordning baserat på **[!UICONTROL Name]** (i alfabetisk ordning), **[!UICONTROL Created]**-datum eller **[!UICONTROL Modified]**-datum.


1. Klicka **[!UICONTROL Add Assets]** mot varje tagg i dialogrutan **[!UICONTROL Select Assets]**. Sök i DAM-databasen eller bläddra i databasen för att välja minst 10 och högst 50 bilder. Välj resurser och inte mappen. När du har markerat bilderna klickar du på **[!UICONTROL Select]**.

   ![Visa utbildningsstatus](assets/smart-tags-training-status.png)

1. Om du vill förhandsvisa miniatyrbilderna för de markerade bilderna klickar du på dragspelet framför en tagg. Du kan ändra markeringen genom att klicka på **[!UICONTROL Add Assets]**. När du är nöjd med markeringen klickar du på **[!UICONTROL Submit]**. Användargränssnittet visar ett meddelande längst ned på sidan om att kursen har startats.
1. Kontrollera utbildningsstatusen i kolumnen **[!UICONTROL Status]** för varje taggmodell. Möjliga statusvärden är [!UICONTROL Pending], [!UICONTROL Trained] och [!UICONTROL Failed].

![Arbetsflöde för att träna taggningsmodellen för smarta taggar](assets/smart-tag-model-training-flow.png)

*Bild: Steg i utbildningsarbetsflödet för att träna taggningsmodellen.*

### Visa utbildningsstatus och rapport {#training-status}

Om du vill kontrollera om smarta taggar-tjänsten är utbildad i dina taggar i utbildningsuppsättningen med resurser kan du läsa rapporten om utbildningsarbetsflödet i rapportkonsolen.

1. I gränssnittet [!DNL Experience Manager] går du till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.
1. Klicka på **[!UICONTROL Create]** på sidan **[!UICONTROL Asset Reports]**.
1. Välj rapporten **[!UICONTROL Smart Tags Training]** och klicka sedan på **[!UICONTROL Next]** i verktygsfältet.
1. Ange en titel och beskrivning för rapporten. Under **[!UICONTROL Schedule Report]** låter du alternativet **[!UICONTROL Now]** vara markerat. Om du vill schemalägga rapporten till ett senare tillfälle väljer du **[!UICONTROL Later]** och anger ett datum och en tid. Klicka sedan på **[!UICONTROL Create]** i verktygsfältet.
1. På sidan **[!UICONTROL Asset Reports]** markerar du rapporten som du skapat. Om du vill visa rapporten klickar du på **[!UICONTROL View]** i verktygsfältet.
1. Granska informationen i rapporten. Rapporten visar träningsstatusen för de taggar du har tränat. Den gröna färgen i kolumnen **[!UICONTROL Training Status]** anger att smarta taggar har tränats för taggen. Gul färg anger att tjänsten är delvis tränad för en viss tagg. Om du vill utbilda tjänsten helt för en tagg lägger du till fler bilder med den särskilda taggen och genomför utbildningsarbetsflödet. Om du inte ser dina taggar i den här rapporten kör du utbildningsarbetsflödet igen för de här taggarna.Taggar
1. Om du vill hämta rapporten markerar du den i listan och klickar på **[!UICONTROL Download]** i verktygsfältet. Rapporten hämtas som ett kalkylblad.

<!--
### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Click **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figure: Navigate to the asset folder and review the tags to verify whether your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).*

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. From upper-left corner, open the **[!UICONTROL Timeline]**.
1. Open actions from the bottom of the left sidebar and click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify that your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly trained tags. However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours. For periodic tagging workflows, unaltered assets are tagged when the time gap exceeds six months.

### Tag uploaded assets {#tag-uploaded-assets}

[!DNL Experience Manager] can automatically tag the assets that users upload to DAM. To do so, administrators configure a workflow to add an available step that tags assets. See [how to enable Smart Tags for uploaded assets](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).
-->

## Tagga resurser med smarta taggar i AEM {#tag-assets}

Alla typer av resurser som stöds taggas automatiskt av [!DNL Experience Manager Assets] när de överförs. Taggning är aktiverat och fungerar som standard. AEM använder rätt smarta taggar i nära realtid. <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* För bilder och videoklipp baseras smarta taggar på vissa visuella aspekter.

* För textbaserade resurser beror effekten av smarta taggar inte på mängden text i resursen utan på relevanta nyckelord eller enheter som finns i resursens text. För textbaserade resurser är de smarta taggarna de nyckelord som visas i texten men de som bäst beskriver resursen. För resurser som stöds extraherar [!DNL Experience Manager] redan texten, som sedan indexeras och används för att söka efter resurserna. Smarta taggar baserade på nyckelord i texten ger dock en dedikerad, strukturerad och prioriterad sökfaktor. Den senare hjälper till att förbättra tillgångsidentifiering jämfört med ett sökindex.

## Hantera smarta taggar och resurssökningar {#manage-smart-tags-and-searches}

Du kan strukturera smarta taggar om du vill ta bort felaktiga taggar som kan ha tilldelats ert varumärkesobjekt, så att endast de mest relevanta taggarna visas.

Genom att moderera smarta taggar kan du också förbättra taggbaserade sökningar efter resurser genom att se till att dina resurser visas i sökresultaten för de mest relevanta taggarna. I grund och botten hjälper det till att eliminera riskerna för att orelaterade resurser visas i sökresultaten.

Du kan också tilldela en högre rankning till en tagg för att öka taggens relevans för resursen. Om du befordrar en tagg för en resurs ökar risken för att resursen visas i sökresultaten när en sökning utförs baserat på den aktuella taggen.

Så här modererar du smarta taggar för dina digitala resurser:

1. I sökfältet söker du efter digitala resurser baserat på en tagg.

1. Om du vill identifiera de digitala resurser som du inte tycker är relevanta för sökningen kontrollerar du sökresultaten.

1. Markera en resurs och välj sedan ![Hantera taggar-ikonen](assets/do-not-localize/manage-tags-icon.png) i verktygsfältet.

1. Granska taggarna från sidan **[!UICONTROL Manage Tags]**. Om du inte vill att resursen ska genomsökas baserat på en viss tagg markerar du taggen och väljer ![Ta bort ikon](assets/do-not-localize/delete-icon.png) i verktygsfältet. Du kan också välja symbolen `X` bredvid etiketten.

1. Om du vill tilldela en högre rankning till en tagg markerar du taggen och väljer ![Befordra ikon](assets/do-not-localize/promote-icon.png) i verktygsfältet. Taggen som du höjer upp flyttas till avsnittet **[!UICONTROL Tags]**.

1. Välj **[!UICONTROL Save]** och sedan **[!UICONTROL OK]** för att stänga dialogrutan [!UICONTROL Success].

1. Navigera till sidan [!UICONTROL Properties] för resursen. Observera att taggen som du befordrade har hög relevans och därför visas högre i sökresultaten.

### Förstå [!DNL Experience Manager]-sökresultat med smarta taggar {#understand-search}

Som standard kombineras söktermerna i [!DNL Experience Manager] med en `AND` -sats. Om du använder smarta taggar ändras inte standardbeteendet. Om du använder smarta taggar läggs en `OR`-sats till för att hitta någon av söktermerna i de använda smarta taggarna. Du kan till exempel söka efter `woman running`. Assets med bara `woman` eller bara `running` nyckelord i metadata visas inte som standard i sökresultaten. En resurs som taggats med antingen `woman` eller `running` med smarta taggar visas i en sådan sökfråga. Sökresultaten är en kombination av

* Assets med nyckelorden `woman` och `running` i metadata.

* Assets smart taggad med något av nyckelorden.

Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. I ovanstående exempel är den ungefärliga visningsordningen för sökresultat:

1. matchar `woman running` i de olika metadatafälten.
1. matchar `woman running` i smarta taggar.
1. matchar `woman` eller `running` i smarta taggar.

## Taggningsrelaterade begränsningar och bästa praxis {#limitations}

Förbättrad smart taggning bygger på inlärningsmodeller för bilder och taggar för dessa. Dessa modeller är inte alltid perfekta när det gäller att identifiera taggar. Den aktuella versionen av smarta taggar har följande begränsningar:

* Oförmåga att identifiera små skillnader i bilder. Exempel: skjortor som inte passar lika bra som skjortor med normal passning.
* Oförmåga att identifiera taggar baserat på små mönster eller delar av en bild. Till exempel logotyper på skjortor.
* Taggning stöds på de språk som [!DNL Experience Manager] stöder.
* De taggar som inte hanteras gäller:

   * Ej visuella, abstrakta aspekter. Exempel: år eller säsong då en produkt släpps, stämning eller känslor som en bild ger upphov till samt en subjektiv nyans av en video.
   * Fina visuella skillnader mellan produkter som skjortor med och utan färg eller små logotyper som är inbäddade i produkter.

Använd de bilder som passar bäst för att utbilda modellen. Utbildningen kan inte återupptas eller så kan utbildningsmodellen inte tas bort. Hur korrekt taggningen är beror på den aktuella kursen, så gör det med omsorg.

<!-- TBD: Add limitations related to text files. -->

Om du vill söka efter filer med smarta taggar (vanliga eller förbättrade) använder du sökningen [!DNL Assets] (fulltextsökning). Det finns inget separat sökpredikat för smarta taggar.

>[!NOTE]
>
>Möjligheten att använda smarta taggar för att utbilda dig på dina taggar och använda dem på andra bilder beror på kvaliteten på de bilder du använder i utbildningen.
>För bästa resultat rekommenderar Adobe att du använder visuellt liknande bilder för att utbilda tjänsten för varje tagg.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Förstå hur smarta taggar hjälper dig att hantera dina digitala filer](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Använd smarta taggar för videofilmer](smart-tags-video-assets.md)
