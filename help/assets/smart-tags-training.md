---
title: Tagga resurser automatiskt med  [!DNL Adobe AI] smart tjänst
description: Tagga tillgångar med en artificiellt intelligent tjänst som tillämpar kontextuella och beskrivande affärstaggar.
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 5%

---


# Utbildning om smarta taggar

Med hjälp av utbildningsmaterialet för smarta taggar kan du träna dina taggar så att du kan ange information om de relevanta taggarna inte finns där. Den använder ett artificiellt intelligent ramverk av [Adobe AI](https://business.adobe.com/ai/adobe-genai.html) för att utbilda sin bildigenkänningsalgoritm i din taggstruktur och din företagsklonomi. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser. [!DNL Experience Manager Assets] använder automatiskt smarta taggar på överförda resurser som standard.

## Fastställa kraven på smarta taggar-utbildning {#smart-tag-training-requirement}

Utbildning i smarta taggar krävs i följande scenarier:

* Om du vill lägga till en automatiserad etikett för att spara iterationer av att lägga till etiketter varje gång du överför samma resurs.
* För att förbättra möjligheten för resurser att använda relevanta taggar.
* Om du vill öka noggrannheten för de taggar som visas för en resurs.
* Om du vill lägga till etiketter som inte är tillgängliga eller saknas.


>[!NOTE]
>
>Smart-taggar tränas endast i en ***bildtyp*** av resursen.

## Steg som rör utbildning av smarta taggar

[!DNL Experience Manager] som [!DNL Cloud Service] genererar automatiskt smarta taggar till textbaserade resurser och till videoklipp som standard. Utför följande uppgifter för att utbilda smarta taggar till bilder:

* [Förstå taggmodeller och riktlinjer](#understand-tag-models-guidelines)
* [Tåg modellen](#train-model)
* [Tagga dina digitala resurser](#tag-assets)
* [Hantera taggar och sökningar](#manage-smart-tags-and-searches)

## Förstå taggmodeller och riktlinjer {#understand-tag-models-guidelines}

En taggmodell är en grupp relaterade taggar som är kopplade till olika visuella aspekter av bilder som taggas. Taggar relaterar till de olika visuella aspekterna av bilder så att taggarna när de används hjälper dig att söka efter särskilda typer av bilder. En skosamling kan till exempel ha olika taggar, men alla taggar är relaterade till skor och kan tillhöra samma taggmodell. När märkorden används kan de hjälpa dig att hitta olika typer av skor, till exempel efter design eller efter användning.

Innan du skapar en taggmodell och utbildar tjänsten bör du identifiera en uppsättning unika taggar som bäst beskriver objekten i bilderna i ditt företags sammanhang. Kontrollera att resurserna i din aktuella uppsättning bekräftar [riktlinjerna för utbildning](#training-guidelines).

### Utbildningsriktlinjer {#training-guidelines}

Kontrollera att bilderna i kursuppsättningen överensstämmer med följande riktlinjer:

<table>
   <tr>
      <th> Mått </th>
      <th> Beskrivning </th>
   </tr>
   <tr>
      <td> <b>Kvantitet och storlek </b></td>
      <td> Minst 10 och högst 50 bilder per tagg. </td>
   </tr>
   <tr>
      <td> <b>Samordning</b> </td>
      <td> Se till att bilderna för en tagg är visuellt lika. Det är bäst att lägga samman märkorden om samma visuella aspekter (till exempel samma typ av objekt i en bild) till en enda taggmodell. Det är till exempel ingen bra idé att tagga alla dessa bilder som <i>min-grupp</i> (för utbildning) eftersom de inte är visuellt lika. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/coherence.png"><br><i>Bild: Illustrativa bilder av Conherence som visar riktlinjerna för utbildning</i>
      </td>
   </tr>
   <tr>
      <td> <b>Täckning</b></td>
      <td> Det ska finnas tillräckligt med variation i bilderna i utbildningen. Tanken är att ge några men relativt olika exempel så att man kan fokusera på rätt saker. Om du använder samma tagg på bilder som ser olika ut bör du ta med minst fem exempel av varje typ. För taggen <i>model-down-pose</i> kan du t.ex. inkludera fler utbildningsbilder som liknar den markerade bilden nedan så att tjänsten kan identifiera liknande bilder mer exakt under taggningen.</td>
   </tr>
   <tr>
   <td colspan="2"> <img src="assets/do-not-localize/coverage_1.png"><br><i>Bild: Illustrativa bilder av täckningen som visar riktlinjerna för utbildning</i>
   </td>
   </tr>
   <tr>
      <td><b>Distraktion/obstruktion</b> </td>
      <td> Tjänsten tränar bättre på bilder som inte är så distraherande (framträdande bakgrunder, icke-relaterade komponenter, t.ex. objekt/personer med huvudmotivet). För taggen <i>casual-shoe</i> är till exempel den andra bilden inte en bra träningskandidat. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/distraction.png"><br><i>Bild: Illustrativa bilder av distraktion/obstruktion som kan användas som exempel på riktlinjerna för utbildning</i>
      </td>
   </tr>
   <tr>
      <td> <b>Fullständighet</b> </td>
      <td> Om en bild kvalificerar för mer än en tagg lägger du till alla tillämpliga taggar innan du inkluderar bilden för utbildning. För taggar som <i>regnrock</i> och <i>modellvy</i> lägger du till båda taggarna i den kvalificerade resursen innan du inkluderar den för träning. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/completeness.png"><br><i>Bild: Illustrativa bilder på fullständighet som visar riktlinjerna för utbildning</i>
      </td>
   </tr>
   <tr>
      <td> <b>Antal taggar</b> </td>
      <td> Adobe rekommenderar att du utbildar en modell med minst två distinkta taggar och minst tio olika bilder för varje tagg. Lägg inte till fler än 50 taggar i en enda taggmodell. </td>
   </tr>
   <tr>
      <td> <b>Antal exempel</b> </td>
      <td> Lägg till minst tio exempel för varje tagg. Adobe rekommenderar dock cirka 30 exempel. Högst 50 exempel per tagg stöds. </td>
   </tr>
   <tr>
      <td> <b>Förhindra falsk positiv och konflikt</b> </td>
      <td> Adobe rekommenderar att du skapar en enda taggmodell för en enda visuell aspekt. Strukturera taggmodellerna på ett sätt som undviker överlappande taggar mellan modellerna. Använd till exempel inte vanliga taggar som <i>sneakers</i> i två olika taggmodellnamn: <i>skor</i> och <i>skodon</i>. Utbildningsprocessen skriver över en tränad taggmodell med den andra för ett vanligt nyckelord. </td>
   </tr>
</table>

**Exempel**: Fler exempel på vägledning är:

* Skapa en taggmodell som endast innehåller

   * Taggar för bilmodeller.
   * Taggen för fodral för vuxna och barn.

* Skapa inte

   * En taggmodell som innehåller bilmodeller som släpptes 2019 och 2020.
   * Flera taggmodeller som innehåller samma få bilmodeller.

>[!NOTE]
>
>Du kan använda samma bilder för att utbilda olika taggmodeller. Koppla emellertid inte en bild till mer än en tagg i en taggmodell. Du kan lägga till märkord i samma bild med olika märkord som tillhör olika taggmodeller.
>Du kan inte ångra kursen. Riktlinjerna ovan bör hjälpa dig att välja bra bilder att utbilda.

## Ange modell för anpassade taggar {#train-model}

Följ de här stegen för att skapa och utbilda en modell för dina företagsspecifika taggar:

1. Skapa nödvändiga taggar och rätt taggstruktur. Överför relevanta bilder i DAM-databasen.
1. Gå till [!DNL Experience Manager Cloud Service] > **[!UICONTROL Assets]** i användargränssnittet för **[!UICONTROL Smart Tag Training]**.
1. Klicka på **[!UICONTROL Create]**. Ange **[!UICONTROL Title]**, **[!UICONTROL Description]**.
1. Klicka på mappikonen i fältet **[!UICONTROL Tags]**. Ett popup-fönster öppnas.
1. Sök efter eller välj lämpliga taggar från de befintliga taggarna i `cq-tags` som du vill lägga till i modellen. Klicka på **[!UICONTROL Next]**.

   >[!NOTE]
   >
   >Du kan sortera taggstrukturen i stigande eller fallande ordning baserat på **[!UICONTROL Name]** (i alfabetisk ordning), **[!UICONTROL Created]**-datum eller **[!UICONTROL Modified]**-datum.


1. Klicka **[!UICONTROL Select Assets]** mot varje tagg i dialogrutan **[!UICONTROL Add Assets]**. Sök i DAM-databasen eller bläddra i databasen för att välja minst 10 och högst 50 bilder. Välj resurser och inte mappen. När du har markerat bilderna klickar du på **[!UICONTROL Select]**.

   ![Visa utbildningsstatus](assets/smart-tags-training-status.png)

1. Om du vill förhandsvisa miniatyrbilderna för de markerade bilderna klickar du på dragspelet framför en tagg. Du kan ändra markeringen genom att klicka på **[!UICONTROL Add Assets]**. När du är nöjd med markeringen klickar du på **[!UICONTROL Submit]**. Användargränssnittet visar ett meddelande längst ned på sidan om att kursen har startats.
1. Kontrollera utbildningsstatusen i kolumnen **[!UICONTROL Status]** för varje taggmodell. Möjliga statusvärden är [!UICONTROL Pending], [!UICONTROL Trained] och [!UICONTROL Failed].

![Arbetsflöde för att träna taggningsmodellen för smarta taggar](assets/smart-tag-model-training-flow.png)

*Bild: Steg i utbildningsarbetsflödet för att träna taggningsmodellen.*

### Visa utbildningsstatus och rapport {#training-status}

Om du vill kontrollera om smarta taggar-tjänsten är utbildad i dina taggar i utbildningsuppsättningen med resurser kan du läsa rapporten om utbildningsarbetsflödet i rapportkonsolen.

1. I gränssnittet [!DNL Experience Manager Cloud Service] går du till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.
1. Klicka på **[!UICONTROL Asset Reports]** på sidan **[!UICONTROL Create]**.
1. Välj rapporten **[!UICONTROL Smart Tags Training]** och klicka sedan på **[!UICONTROL Next]** i verktygsfältet.
1. Ange en titel och beskrivning för rapporten. Under **[!UICONTROL Schedule Report]** låter du alternativet **[!UICONTROL Now]** vara markerat. Om du vill schemalägga rapporten till ett senare tillfälle väljer du **[!UICONTROL Later]** och anger ett datum och en tid. Klicka sedan på **[!UICONTROL Create]** i verktygsfältet.
1. På sidan **[!UICONTROL Asset Reports]** markerar du rapporten som du skapat. Om du vill visa rapporten klickar du på **[!UICONTROL View]** i verktygsfältet.
1. Granska informationen i rapporten. Rapporten visar träningsstatusen för de taggar du har tränat. Den gröna färgen i kolumnen **[!UICONTROL Training Status]** anger att smarta taggar har tränats för taggen. Gul färg anger att tjänsten är delvis tränad för en viss tagg. Om du vill utbilda tjänsten helt för en tagg lägger du till fler bilder med den särskilda taggen och genomför utbildningsarbetsflödet. Om du inte ser dina taggar i den här rapporten kör du utbildningsarbetsflödet igen för de här taggarna.Taggar
1. Om du vill hämta rapporten markerar du den i listan och klickar på **[!UICONTROL Download]** i verktygsfältet. Rapporten hämtas som ett kalkylblad.

>[!NOTE]
>
>Hur gör jag om jag vill överföra övergången från smarta taggar från en instans till en annan via en export?
>Du behöver inte exportera utbildning för smarta taggar om miljön tillhör samma IMS-organisation. Den delas automatiskt. Om miljön fungerar på olika IMS-organ finns det inget sätt att dela eller exportera utbildning för smarta taggar.

## Begränsningar och bästa metoder för smarta taggar {#limitations-smart-tags-training}

* Använd de bilder som passar bäst för att utbilda modellen. Utbildningen kan inte återupptas eller så kan utbildningsmodellen inte tas bort. Hur korrekt taggningen är beror på den aktuella kursen, så gör det med omsorg.
* Du kan inte utbilda tjänsten som tillämpar smarta taggar på videoklipp med hjälp av specifika videoklipp. Det fungerar med standardinställningarna för [!DNL Adobe AI].


>[!NOTE]
>
>Möjligheten att använda smarta taggar för att utbilda dig på dina taggar och använda dem på andra bilder beror på kvaliteten på de bilder du använder i utbildningen.
>För bästa resultat rekommenderar Adobe att du använder visuellt liknande bilder för att utbilda tjänsten för varje tagg.
