---
title: Skapa formulärfragment för WYSIWYG-baserad redigering
description: Lär dig hur du skapar formulärfragment i den universella redigeraren och lägger till dem i formulär.
feature: Edge Delivery Services
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 62c58ceb2d2d659bad591b3eba1bfd924f2a848b
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---


# Skapa och använda Edge Delivery Services-formulärfragment i Universal Editor

Forms innehåller ofta vanliga avsnitt som kontaktinformation, identifikationsinformation eller godkännandeavtal. Formulärutvecklarna skapar dessa avsnitt varje gång de skapar ett nytt formulär som är upprepande och tidskrävande.
För att slippa detta dubbelarbete erbjuder Universal Editor ett sätt att skapa återanvändbara formulärsegment, t.ex. paneler eller fältgrupper, bara en gång och återanvända dem i olika formulär. Dessa återanvändbara, modulära och fristående segment kallas för formulärfragment. Samma kontaktfragment för nödsituationer kan till exempel användas i olika avsnitt av ett formulär, till exempel för kontaktinformation för medarbetare och ansvarig.

I slutet av artikeln får du lära dig att skapa och använda fragment i formulär med den universella redigeraren.

## Funktioner för Edge Delivery Services-formulärfragment

* **Bevara konsekvens med formulärfragment**
Du kan integrera fragment i olika formulär, vilket gör att du kan upprätthålla enhetliga layouter och standardiserat innehåll. Med metoden&quot;ändra en gång, spegla överallt&quot; tillämpas automatiskt alla uppdateringar som görs i ett fragment på alla formulär.

* **Lägger till formulärfragment flera gånger i formuläret**
Du kan lägga till ett formulärfragment flera gånger i ett formulär och konfigurera dess databindningsegenskaper till datakällor eller scheman.

* **Använda fragment inom fragment**
Du kan skapa kapslade formulärfragment, vilket betyder att du kan lägga till ett fragment i ett annat fragment och ha en kapslad fragmentstruktur.

  >[!NOTE]
  >
  > Du kan inte kapsla in ett fragment i sig själv eftersom detta kan orsaka rekursiva referenser och oönskat beteende, vilket kan leda till fel eller återgivningsproblem.

## Att tänka på när du använder Edge Delivery Services-formulärfragment

* Du måste lägga till samma GitHub-URL i både fragmentet och formuläret där du tänker använda fragmentet.
* Du kan inte redigera ett formulärfragment som infogas med referens i ett formulär. Ändra det fristående formulärfragmentet om du vill redigera det.

## Krav för att skapa Edge Delivery Services-formulärfragment

* [Konfigurera din GitHub-databas](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) för att upprätta en anslutning mellan din AEM-miljö och GitHub-databasen.
* Om du redan använder Edge Delivery Services lägger du till den senaste versionen av [Adaptive Forms-blocket](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) i din GitHub-databas.
* Instansen AEM Forms Author innehåller en mall baserad på Edge Delivery Services. Kontrollera att den [senaste versionen av Core Components](https://github.com/adobe/aem-core-forms-components) är installerad i din miljö.
* Ha URL:en till din AEM Forms as a Cloud Service-författarinstans och din GitHub-databas till hands.

## Arbeta med Edge Delivery Services-formulärfragment

Du kan skapa Edge Delivery Services-formulärfragment i den universella redigeraren och lägga till de skapade fragmenten i Edge Delivery Services-formulär. Du kan utföra följande åtgärder med Edge Delivery Services-formulärfragment:

* [Skapa formulärfragment](#creating-form-fragments)
* [Lägga till formulärfragment i ett formulär](#adding-form-fragments-to-a-form)
* [Hantera formulärfragment](#managing-form-fragments)

### Skapa formulärfragment

Så här skapar du ett formulärfragment i den universella redigeraren:

1. Logga in på din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Klicka på **Skapa > Adaptivt formulärfragment**.

   ![Skapa fragment](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Guiden **Skapa adaptivt formulärfragment** visas.
1. Välj den gruppbaserade mallen för leveranstjänster på fliken **Välj mall** och klicka på **[!UICONTROL Next]**.
   ![Välj Edge Delivery Services-mall](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Ange rubrik, namn, beskrivning och taggar för fragmentet. Se till att du anger ett unikt namn för fragmentet. Om det finns ett annat fragment med samma namn kan fragmentet inte skapas.
1. Ange **GitHub-URL**. Om din GitHub-databas till exempel har namnet `edsforms`, finns den under kontot `wkndforms`, är URL:en `https://github.com/wkndforms/edsforms`.

   ![grundläggande egenskaper](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Valfritt) Klicka för att öppna fliken **Formulärmodell** och välj en av följande modeller för fragmentet på den nedrullningsbara menyn **Välj från**:

   ![Visar modelltyp på fliken Formulärmodell](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **Formulärdatamodell (FDM)**: Integrera datamodellsobjekt och datatjänster från datakällor i fragmentet. Välj FDM (Form Data Model) om formuläret kräver att du läser och skriver data från flera källor.

   * **JSON-schema**: Integrera formuläret med ett serverdelssystem genom att associera ett JSON-schema som definierar datastrukturen. Det gör att du kan lägga till dynamiskt innehåll med schemaelementen.
   * **Inget**: Anger att fragmentet ska skapas från grunden utan att någon formulärmodell används.

   >[!NOTE]
   >
   > [Klicka här](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) om du vill lära dig hur du integrerar formulär eller fragment med en formulärdatamodell (FDM) i den universella redigeraren för att använda olika backend-datakällor.

1. (Valfritt) Ange **Publiceringsdatum** eller **Avpubliceringsdatum** för fragmentet på fliken **Avancerat**.

   ![Avancerad flik](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Klicka på **Skapa** så visas en guide.

   ![Redigera fragment](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Klicka på **Redigera** så öppnas det skapade fragmentet med en standardmall i Universal Editor för redigering.

   ![Fragment i Univerasal Editor för redigering](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   I redigeringsläget kan du lägga till alla formulärkomponenter i fragmentet. Mer information om hur du skapar ett fragment i den universella redigeraren finns i artikeln [Komma igång med Edge Delivery Services för AEM Forms med den universella redigeraren](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) .

   Skärmbilden nedan visar `contact fragment` som har skapats i Universell redigerare.

   ![Kontaktfragment](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   När du har skapat fragmentet kan du [lägga till det skapade fragmentet i Edge Delivery Services Forms](#adding-form-fragments-in-forms).

### Lägga till formulärfragment i ett formulär

Låt oss skapa ett enkelt `Employee Details`-formulär som innehåller information om både medarbetare och ansvarig. Du kan använda fragmentet `Contact Details` på både den anställdes- och övervakarpanelerna. Så här använder du formulärfragmentet i formuläret:

1. Öppna formuläret i redigeringsläge.
1. Lägg till komponenten Formulärfragment i formuläret.
1. Öppna innehållsläsaren och navigera till komponenten **[!UICONTROL Adaptive Form]** i **innehållsträdet**.
1. Navigera till avsnittet där du vill lägga till ett fragment. Navigera till exempel till panelen **Information om medarbetare**.

   ![Navigera till avsnittet](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Klicka på ikonen **[!UICONTROL Add]** och lägg till komponenten **[!UICONTROL Form Fragment]** från listan **Adaptiva formulärkomponenter**.
   ![Lägg till formulärfragment](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   När du väljer komponenten **[!UICONTROL Form Fragment]** läggs fragmentet till i formuläret. Du kan konfigurera egenskaperna för det tillagda fragmentet genom att öppna dess **Egenskaper**. Dölj till exempel fragmentets namn från dess **egenskaper**.

   ![Konfigurerar fragmentets egenskaper](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Markera **fragmentreferensen** på fliken **Grundläggande**. Alla fragment som är tillgängliga för formuläret, beroende på formulärmodellen, visas.

   Navigera till exempel till `/content/forms/af` och markera fragmentet `Contact Details`.

   ![Välj fragment](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Klicka på **[!UICONTROL Select]**.

   Formulärfragmentet läggs till med referens till formuläret och förblir synkroniserat med det fristående formulärfragmentet. Det innebär att alla ändringar som görs i fragmentet speglas i alla instanser där fragmentet är inbyggt i formulären.

   ![Fragment i formulär](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   Du kan förhandsgranska formuläret för att se hur det ser ut i **förhandsgranskningsläget**.

   ![Förhandsgranska](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   På samma sätt kan du upprepa steg 3 till 7 för att infoga `Contact Details`-fragmentet för panelen `Supervisor Details`.

   ![Formulär för personalinformation](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### Hantera formulärfragment

Du kan utföra flera åtgärder på formulärfragment med AEM Forms användargränssnitt.

1. Logga in på din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

1. Markera ett formulärfragment och i verktygsfältet visas följande åtgärder som du kan utföra på det markerade fragmentet.

   ![Hantera fragment](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>Åtgärd</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
    </tr>
    <tr>
   <td><p>Redigera</p> </td>
   <td><p>Öppnar formulärfragmentet i redigeringsläge.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Egenskaper</p> </td>
   <td><p>Tillhandahåller alternativ för att ändra egenskaperna för formulärfragmentet.<br /> <br /> </p> </td>
    </tr>
    <td><p>Kopiera</p> </td>
   <td><p> Innehåller alternativ för att kopiera formulärfragmentet och klistra in det på önskad plats. <br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>Förhandsgranska</p> </td>
   <td><p>Tillhandahåller alternativ för att förhandsgranska fragmentet som HTML eller utföra en anpassad förhandsgranskning genom att sammanfoga data från en XML-fil med fragmentet. <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Ladda ned</p> </td>
   <td><p>Hämtar det markerade fragmentet.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Starta granskning/hantera granskning</p> </td>
   <td><p>Tillåter initiering och hantering av en granskning av det valda fragmentet.<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>Publicera/avpublicera</p> </td>
   <td><p>Publicerar/återpublicerar det valda fragmentet.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Ta bort</p> </td>
   <td><p>Tar bort det markerade fragmentet.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Jämför</p> </td>
   <td><p>Jämför två olika formulärfragment för förhandsgranskning.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## Bästa praxis

* Kontrollera att fragmentnamnet är unikt. Fragmentet kan inte skapas om det finns ett befintligt fragment med samma namn.
* Alla uttryck, skript och format i ett fristående formulärfragment behålls när de infogas som referens eller bäddas in i ett formulär.
* När du publicerar ett formulär publiceras de formulärfragment som infogats med referens i formuläret automatiskt.

## Se även

{{universal-editor-see-also}}