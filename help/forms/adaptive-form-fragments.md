---
title: Adaptiva formulärfragment
seo-title: Adaptive Form Fragments
description: Adaptiv Forms har en funktion för att skapa ett formulärsegment, t.ex. en panel eller en grupp med fält, som att använda det i ett adaptivt formulär. Du kan också spara en befintlig panel som fragment.
seo-description: Adaptive Forms provides a mechanism to create a form segment, such as a panel or a group of fields, as use it in any Adaptive Form. You can also save an existing panel as fragment.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 0%

---


# Adaptiva formulärfragment{#adaptive-form-fragments}

Alla formulär har utformats för ett specifikt ändamål, men det finns några vanliga segment i de flesta formulär, till exempel för att ge personliga uppgifter som namn och adress, familjeinformation, inkomstinformation och så vidare. Formulärutvecklare måste skapa dessa gemensamma segment varje gång ett nytt formulär skapas.

Adaptiv Forms är en praktisk mekanism för att skapa formulärsegment som en panel eller en grupp fält endast en gång och återanvända dem i adaptiv Forms. Dessa återanvändbara och fristående segment kallas adaptiva formulärfragment.

## Skapa ett fragment {#create-a-fragment}

Du kan skapa ett anpassat formulärfragment från grunden eller spara en panel i ett befintligt anpassat formulär som fragment.

### Skapa fragment från grunden {#create-fragment-from-scratch}

1. Logga in [!DNL AEM Forms] författarinstans på https://[*värdnamn*]:[*port*]/aem/forms.html.
1. Klicka **Skapa > Adaptivt formulärfragment**.
1. Ange rubrik, namn, beskrivning och taggar för fragmentet.

   >[!NOTE]
   >
   >Se till att du anger ett unikt namn för fragmentet. Om det redan finns ett annat fragment med samma namn kan fragmentet inte skapas.

1. Klicka för att öppna **Formulärmodell** och från **Välj från** väljer du en av följande modeller för fragmentet:

   * **Ingen**: Anger att fragmentet ska skapas från grunden utan att någon formulärmodell används.
   * **Formulärmall**: Anger att fragmentet ska skapas med en XDP-mall som överförts till [!DNL AEM Forms]. Välj lämplig XDP-mall som formulärmodell för fragmentet.

   ![Skapa ett adaptivt formulär med formulärmallen som modell](assets/form-template-model.png)

   Delformulären som är markerade som fragment i den valda formulärmallen visas också. Du kan välja ett delformulär för Adaptivt formulärfragment i listrutan.

   ![Välj delformulär från den angivna formulärmallen](assets/fragment-subform.png)

   Dessutom kan du skapa ett adaptivt formulärfragment med hjälp av delformulär som inte är markerade som fragment i formulärmallen genom att ange SOM-uttrycket för delformuläret i listrutan.

   * **XML-schema**: Anger att fragmentet ska skapas med ett XML-schema som har överförts till [!DNL AEM Forms]. Du kan överföra eller välja bland tillgängliga XML-scheman som formulärmodell för fragmentet.

   ![Skapa ett adaptivt formulärfragment baserat på ett XML-schema som modell](assets/xml-schema-model.png)

   Du kan också skapa ett adaptivt formulärfragment genom att välja en complexType som finns i det valda schemat i listrutan.

   ![Välj en komplex typ från den angivna XML-schemamodellen](assets/complex-type.png)

1. Klicka **Skapa** och sedan klicka **Öppna** om du vill öppna fragmentet, med en standardmall, i redigeringsläge.

I redigeringsläge kan du dra och släppa alla adaptiva formulärkomponenter från AEM-sidan till fragmentet. <!-- For information about Adaptive Form components, see Introduction to authoring Adaptive Forms. -->

Om du dessutom har valt ett XML-schema eller en XDP-formulärmall som formulärmodell för fragmentet visas en ny flik som visar formulärmodellhierarkin i innehållssökaren. Du kan dra och släppa formulärmodellelement till fragmentet. De tillagda elementen för formulärmodell konverteras till formulärkomponenter samtidigt som de ursprungliga egenskaperna från den associerade XDP- eller XSD-filen behålls.

### Spara panelen som ett fragment {#save-panel-as-a-fragment}

1. Öppna ett anpassat formulär som innehåller den panel som du vill spara som anpassat formulärfragment.
1. Klicka på **[!UICONTROL Save as Fragment]**. Dialogrutan Spara som fragment öppnas.

   >[!NOTE]
   >
   >Om panelen som du sparar som fragment innehåller en underordnad panel, kommer det resulterande fragmentet att inkludera dem.

1. Ange följande information i dialogrutan Skapa fragment:

   * **Namn**: Namnet på fragmentet. Standardvärdet är panelens elementnamn. Det är ett obligatoriskt fält.
      >[!NOTE]
      >
      >Se till att du anger ett unikt namn för fragmentet. Om det redan finns ett annat fragment med samma namn kan fragmentet inte skapas.

   * **Titel**: Fragmentets namn. Standardvärdet är panelens namn.

   * **Beskrivning**: Beskrivning av fragmentet.

   * **Taggar**: Taggar metadata för fragmentet.

   * **Målsökväg**: Databassökväg där fragmentet ska sparas. Om du inte anger en sökväg skapas en nod med samma namn som fragmentet bredvid noden som innehåller det adaptiva formuläret. Fragmentet sparas i den här noden.

   * **Formulärmodell**: Beroende på formulärmodellen för det adaptiva formuläret visas det här fältet **XML-schema**, **Formulärmall**, eller **Ingen**. Det är ett icke-redigerbart fält.

   * **Fragmentmodellrot**: Visas endast i XSD-baserad Adaptive Forms. Den anger fragmentmodellens rot. Du kan välja **/** eller den komplexa XSD-typen i listrutan. Observera att du bara kan återanvända fragmentet i ett annat adaptivt formulär om du väljer den komplexa typen som fragmentmodellrot.
Om du väljer **/** som fragmentmodellrot är det fullständiga XSD-trädet från roten synligt på fliken Adaptiv formulärdatamodell. För en fragmentmodellrot av en komplex typ visas bara de underordnade för den valda komplexa typen på fliken Adaptiv formulärdatamodell.

   * **XSD-referens**: Visas endast i XSD-baserad Adaptive Forms. Den visar platsen för XML-schemat.

   * **XDP-referens**: Visas endast i XDP-baserade Adaptive Forms. Här visas platsen för XDP-formulärmallen.

   ![save-fragment](assets/save-fragment.png)

   Dialogrutan Spara som fragment

1. Klicka **OK**.

   Panelen sparas på den angivna platsen eller standardplatsen i databasen. I det adaptiva formuläret ersätts panelen av en ögonblicksbild av fragmentet. Som visas nedan sparas den allmänna informationspanelen och dess underordnade paneler, Personlig information och Adress, som ett fragment.

   Om du vill redigera fragmentet klickar du på **[!UICONTROL Edit Asset]** i panelens verktygsfält. Fragmentet öppnas i en ny flik eller i ett nytt fönster i redigeringsläge.

   ![Redigera fragment](assets/edit-fragment.png)

## Arbeta med fragment {#working-with-fragments}

### Konfigurera fragmentutseende {#configure-fragment-appearance}

Alla fragment som du infogar i Adaptiv Forms visas som en platshållarbild. Platshållaren visar titlar på upp till högst tio underordnade paneler i fragmentet. Du kan konfigurera [!DNL AEM Forms] om du vill visa hela avsnittet i stället för platshållarbilden.

Utför följande steg för att visa fullständiga fragment i formulär:

1. Gå AEM webbkonsolens konfigurationssida på https:[*värd*]:[*port*]/system/console/configMgr.

1. Sök och klicka **[!UICONTROL Adaptive Form Configuration Service]** för att öppna den i redigeringsläge.
1. Inaktivera **[!UICONTROL Enable Placeholder in place of Fragment]** om du vill visa hela fragment i stället för platshållarbilden.

### Infoga ett fragment i ett anpassat formulär {#insert-a-fragment-in-an-adaptive-form}

De adaptiva formulärfragment du skapar visas på fliken Adaptiva formulärfragment i AEM innehållssökning. Så här infogar du ett adaptivt formulärfragment i ett adaptivt format:

1. Öppna det adaptiva formuläret, i redigeringsläge, där du vill infoga ett adaptivt formulärfragment.
1. Klicka **Resurser** ![assets-browser](assets/assets-browser.png) i sidlisten. Välj **Adaptiva formulärfragment** i listrutan.

   Du kan också välja att visa alla adaptiva formulärfragment eller filter baserat på formulärmodellen - Formulärmall, XML-schema eller Grundläggande.

1. Dra och släpp ett adaptivt formulärfragment på det adaptiva formuläret.

   >[!NOTE]
   >
   >Det adaptiva formulärfragmentet är inte aktiverat för redigering i det adaptiva formuläret. Dessutom kan du inte använda ett XSD-baserat fragment i en JSON-baserad adaptiv form och tvärtom.

Det adaptiva formulärfragmentet infogas som referens i det adaptiva formuläret och synkroniseras med det fristående adaptiva formulärfragmentet. Det innebär att när du uppdaterar det adaptiva formulärfragmentet återspeglas ändringarna i alla adaptiva Forms där fragmentet används.

### Bädda in ett fragment i adaptiv form {#embed-a-fragment-in-adaptive-form}

Du kan välja att bädda in ett adaptivt formulärfragment i ett adaptivt formulär genom att klicka på **Bädda in resurs: &lt;*fragmentName*>** på panelens verktygsfält för det tillagda fragmentet, vilket visas i följande exempelbild.

![Bädda in ett formulärfragment i anpassat formulär](assets/embed-fragment.png)

>[!NOTE]
>
>Det inbäddade fragmentet är inte längre länkat till det fristående fragmentet. Du kan redigera komponenterna i det inbäddade fragmentet i det adaptiva formuläret.

### Använda fragment inom fragment {#using-fragments-within-fragments}

Du kan skapa kapslade adaptiva formulärfragment, vilket betyder att du kan dra och släppa ett fragment i ett annat fragment och ha en kapslad fragmentstruktur.

### Ändra fragment {#change-fragments}

Du kan ersätta eller ändra ett adaptivt formulärfragment med ett annat fragment genom att använda **Välj fragmentresurs** i dialogrutan Redigera-komponent för en anpassad formulärfragmentpanel.

## Automatisk mappning av fragment för databindning {#auto-mapping-of-fragments-for-data-binding}

När du skapar ett adaptivt formulärfragment med en XFA-formulärmall eller en XSD-komplex typ och drar och släpper fragmentet till en adaptiv form, ersätts XFA-fragmentet eller XSD-komplex typ automatiskt med motsvarande adaptiv formulärfragment vars fragmentmodellrot är mappad till XFA-fragmentet eller XSD-komplex typ.

Du kan ändra fragmentresursen och dess bindningar i dialogrutan Redigera komponent.

>[!NOTE]
>
>Du kan också dra och släppa ett bundet adaptivt formulärfragment från biblioteket för adaptiva formulärfragment i AEM innehållssökaren och ange rätt bindningsreferens från dialogrutan Redigera komponent i panelen Adaptivt formulärfragment.

## Hantera fragment {#manage-fragments}

Du kan utföra flera åtgärder på adaptiva formulärfragment med [!DNL AEM Forms] Gränssnitt.

1. Gå till `https://[hostname]:'port'/aem/forms.html`.

1. Klicka **Välj** i [!DNL AEM Forms] Användargränssnittets verktygsfält och välj ett adaptivt formulärfragment. I verktygsfältet visas följande åtgärder som du kan utföra på det valda adaptiva formulärfragmentet.

<table>
 <tbody>
  <tr>
   <td><p><strong>Åtgärd</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p>Öppna</p> </td>
   <td><p>Öppnar det markerade adaptiva formulärfragmentet i redigeringsläge.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Visa egenskaper</p> </td>
   <td><p>Öppnar egenskapspanelen. På panelen Egenskaper kan du visa och redigera egenskaper, generera en förhandsvisning och överföra en miniatyrbild för det valda fragmentet. Mer information finns i <a href="manage-form-metadata.md" target="_blank">Hantera metadata</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Kopiera</p> </td>
   <td><p>Kopierar det markerade fragmentet. Knappen Klistra in visas i verktygsfältet.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Hämta</p> </td>
   <td><p>Hämtar det markerade fragmentet.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Förhandsgranska</p> </td>
   <td><p>Tillhandahåller alternativ för att förhandsgranska fragmentet som HTML eller som en anpassad förhandsgranskning genom att sammanfoga data från en XML-fil med fragmentet. <!-- For more information, see <a href="previewing-forms.md" target="_blank">Previewing a form</a>.<br /> <br /> --></p> </td>
  </tr>
  <tr>
   <td><p>Starta granskning/hantera granskning</p> </td>
   <td><p>Gör att du kan initiera och hantera en granskning av det valda fragmentet. <!-- For more information, see <a href="create-reviews-forms.md" target="_blank">Creating and managing reviews</a>.<br /> <br /> </p> --> </td>
  </tr>
  <tr>
   <td><p>Skapa ordlista</p> </td>
   <td><p>Skapar en ordlista för lokalisering av det valda fragmentet. <!-- For more information, see <a href="lazy-loading-adaptive-forms.md" target="_blank">Localizing Adaptive Forms</a>.<br /> <br /> --> </p> </td>
  </tr>
  <tr>
   <td><p>Publicera/avpublicera</p> </td>
   <td><p>Publicerar/avpublicerar det markerade fragmentet.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Ta bort</p> </td>
   <td><p>Tar bort det markerade fragmentet.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Lokalisera anpassat formulär som innehåller fragment {#localizing-adaptive-form-containing-fragments}

Om du vill lokalisera ett adaptivt formulär som innehåller adaptiva formulärfragment måste du lokalisera fragmentet och formuläret separat. Tanken är att lokalisera ett fragment en gång och återanvända det i flera adaptiva Forms.

>[!NOTE]
>
>Lokaliseringstangenterna i fragmentet visas inte i XLIFF-filen för ett adaptivt formulär.

## Viktiga punkter att komma ihåg när du arbetar med fragment {#key-points-to-remember-when-working-with-fragments}

* Kontrollera att fragmentnamnet är unikt. Fragmentet kan inte skapas om det finns ett befintligt fragment med samma namn.
* Om du sparar en panel som ett fragment som innehåller ett annat XDP-fragment i ett XDP-baserat adaptivt formulär, binds det resulterande fragmentet automatiskt till det underordnade XDP-fragmentet. Om det finns ett XSD-baserat anpassat formulär binds det resulterande fragmentet till schemaroten.
* När du skapar ett adaptivt formulärfragment skapas en fragmentnod, som liknar noden guideContainer för ett adaptivt formulär i CRXDe Lite.
* Ett fragment i ett adaptivt formulär som använder en annan formulärdatamodell stöds inte. Ett XDP-baserat fragment stöds till exempel inte i en XSD-baserad Adaptiv form och vice versa.
* Anpassade formulärfragment kan användas via fliken Adaptiva formulärfragment i AEM innehållssökaren.
* Alla uttryck, skript och format i ett fristående adaptivt formulärfragment behålls när de infogas som referens eller bäddas in i ett adaptivt formulär.
* Du kan inte redigera ett adaptivt formulärfragment som infogas med referens i ett adaptivt formulär. Om du vill redigera kan du antingen redigera det fristående adaptiva formulärfragmentet eller bädda in fragmentet i det adaptiva formuläret.
* När du publicerar ett adaptivt formulär måste du publicera de fristående adaptiva formulärfragment som infogats med referens i det adaptiva formuläret.
* När du publicerar om ett uppdaterat adaptivt formulärfragment återspeglas ändringarna i de publicerade instanserna av det adaptiva formulär som fragmentet används i.
* Adaptiv form som innehåller Verifiera-komponenten stöder inte anonyma användare. Du bör inte heller använda komponenten Verify i ett adaptivt formulärfragment.
* (**Endast Mac**) För att säkerställa att funktionen för formulärfragment fungerar perfekt i alla scenarier lägger du till följande post i filen /private/etc/hosts:
   `127.0.0.1 <Host machine>` **Värddator**: Apple Mac-maskinen som [!DNL AEM Forms] distribueras.

## Referensfragment {#reference-fragments}

Referensadaptiva formulärfragment som du kan använda för att skapa formuläret finns tillgängliga. Mer information finns i [Referensfragment](reference-adaptive-form-fragments.md).
