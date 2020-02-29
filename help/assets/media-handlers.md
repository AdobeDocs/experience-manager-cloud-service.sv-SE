---
title: Bearbeta resurser med mediehanterare och arbetsflöden
description: Lär dig mer om olika mediehanterare och hur du använder dem i arbetsflöden för att utföra åtgärder på resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# Bearbeta resurser med mediehanterare och arbetsflöden {#processing-assets-using-media-handlers-and-workflows}

Adobe Experience Manager Assets (AEM) innehåller en uppsättning standardarbetsflöden och mediehanterare för att bearbeta resurser. Arbetsflödet definierar de allmänna åtgärder som ska utföras på resurserna och delegerar sedan de specifika åtgärderna till mediehanterarna, till exempel generering av miniatyrbilder eller metadataextrahering.

Ett arbetsflöde kan definieras som körs automatiskt när en resurs av en viss typ överförs till servern. Bearbetningsstegen definieras som en serie mediehanterare för AEM Resurser. AEM innehåller vissa [inbyggda hanterare,](#default-media-handlers) och ytterligare kan antingen [anpassas](#creating-a-new-media-handler) eller definieras genom att delegera processen till ett [kommandoradsverktyg](#command-line-based-media-handler).

Mediehanterare är tjänster i AEM Resurser som utför specifika åtgärder på resurser. När till exempel en MP3-ljudfil överförs till AEM utlöses en MP3-hanterare som extraherar metadata och skapar en miniatyrbild. Mediehanterare används vanligtvis i kombination med arbetsflöden. De vanligaste MIME-typerna stöds i AEM. Specifika uppgifter kan utföras på resurser genom att antingen utöka/skapa arbetsflöden, utöka/skapa mediehanterare eller inaktivera/aktivera mediehanterare.

>[!NOTE]
>
>På sidan Format [som stöds av](file-format-support.md) Assets finns en beskrivning av alla format som stöds av AEM Assets samt funktioner som stöds för varje format.

## Standardmediehanterare {#default-media-handlers}

Följande mediehanterare är tillgängliga i AEM Resurser och hanterar de vanligaste MIME-typerna:

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

<table>
 <tbody>
  <tr>
   <td>Hanterarnamn</td>
   <td>Tjänstnamn (i systemkonsolen)</td>
   <td>MIME-typer som stöds</td>
  </tr>
  <tr>
   <td>TextHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.TextHandler</p> </td>
   <td>text/plain</td>
  </tr>
  <tr>
   <td>PdfHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pdf.PdfHandler</p> </td>
   <td><p>application/pdf<br /> application/illustrator</p> </td>
  </tr>
  <tr>
   <td>JpegHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.JpegHandler</p> </td>
   <td>image/jpeg</td>
  </tr>
  <tr>
   <td>Mp3Handler</td>
   <td><p>com.day.cq.dam.handler.standard.mp3.Mp3Handler</p> </td>
   <td><p>audio/mpeg</p> </td>
  </tr>
  <tr>
   <td>ZipHandler</td>
   <td><p>com.day.cq.dam.handler.standard.zip.ZipHandler</p> </td>
   <td><p>application/java-archive</p> <p>application/zip</p> </td>
  </tr>
  <tr>
   <td>PictHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pict.PictHandler</p> </td>
   <td><p>bild/pict</p> </td>
  </tr>
  <tr>
   <td>StandardImageHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.StandardImageHandler</p> </td>
   <td><p>image/gif</p> <p>bild/png</p> <p>application/photoshop</p> <p>image/jpeg</p> <p>bild/tiff</p> <p>image/x-ms-bmp</p> <p>image/bmp</p> </td>
  </tr>
  <tr>
   <td>MSOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler</td>
   <td>application/msword<br /> </td>
  </tr>
  <tr>
   <td>MSPowerPointHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler</td>
   <td>application/vnd.ms<br /> </td>
  </tr>
  <tr>
   <td>OpenOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler</td>
   <td>application/vnd.openxmlformats-officedocument.wordbehandlingml.document<br /> application/vnd.openxmlformats-officedocument.spreadsheet.sheet<br /> application/vnd.openxmlformats-officedocument.presentationml.presentation<br /><br /> </td>
  </tr>
  <tr>
   <td>EPubHandler</td>
   <td>com.day.cq.dam.handler.standard.epub.EPubHandler</td>
   <td>application/epub+zip</td>
  </tr>
  <tr>
   <td>GenericAssetHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.GenericAssetHandler</p> </td>
   <td>tillbaka om ingen annan hanterare hittades för att extrahera data från en resurs</td>
  </tr>
 </tbody>
</table>

Alla hanterare utför följande uppgifter:

* extrahera alla tillgängliga metadata från resursen.
* skapa en miniatyrbild av resursen.

Det går att visa de aktiva mediehanterarna:

1. Navigera till i webbläsaren `http://localhost:4502/system/console/components`.
1. Klicka på länken `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. En lista med alla aktiva mediehanterare visas.

## Använda mediehanterare i arbetsflöden för att utföra åtgärder på resurser {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

Mediehanterare är tjänster som vanligtvis används i kombination med arbetsflöden.

AEM har vissa standardarbetsflöden för att bearbeta resurser. Om du vill visa dem öppnar du arbetsflödeskonsolen och klickar på fliken **[!UICONTROL Modeller]** : de arbetsflödesrubriker som börjar med AEM Assets är de resursspecifika.

Befintliga arbetsflöden kan utökas och nya kan skapas för att bearbeta resurser enligt specifika krav.

I följande exempel visas hur du förbättrar arbetsflödet för synkronisering **[!UICONTROL av]** AEM-resurser så att delresurser genereras för alla resurser utom PDF-dokument.

### Inaktivera/aktivera en mediehanterare {#disabling-enabling-a-media-handler}

Mediehanterarna kan inaktiveras eller aktiveras via webbhanteringskonsolen för Apache Felix. När mediehanteraren är inaktiverad utförs inte dess uppgifter på resurserna.

Så här aktiverar/inaktiverar du en mediehanterare:

1. Navigera till i webbläsaren `https://<host>:<port>/system/console/components`.
1. Klicka på **[!UICONTROL Inaktivera]** bredvid namnet på mediehanteraren. Exempel: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Uppdatera sidan: en ikon visas bredvid mediehanteraren som anger att den är inaktiverad.
1. Om du vill aktivera mediehanteraren klickar du på **[!UICONTROL Aktivera]** bredvid namnet på mediehanteraren.

### Skapa en ny mediehanterare {#creating-a-new-media-handler}

Om du vill ha stöd för en ny medietyp eller utföra specifika åtgärder på en resurs måste du skapa en ny mediehanterare. I det här avsnittet beskrivs hur du fortsätter.

#### Viktiga klasser och gränssnitt {#important-classes-and-interfaces}

Det bästa sättet att starta en implementering är att ärva från en tillhandahållen abstrakt implementering som tar hand om de flesta saker och tillhandahåller ett rimligt standardbeteende: klassen `com.day.cq.dam.core.AbstractAssetHandler` .

Den här klassen tillhandahåller redan en abstrakt tjänstbeskrivning. Om du ärver från den här klassen och använder plugin-programmet maven-sling ska du se till att du anger ärvningsflaggan som `true`.

Implementera följande metoder:

* `extractMetadata()`: extraherar alla tillgängliga metadata.
* `getThumbnailImage()`: skapar en miniatyrbild av den överförda resursen.
* `getMimeTypes()`: returnerar resursens MIME-typer.

Här är en exempelmall:

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

Gränssnittet och klasserna omfattar:

* `com.day.cq.dam.api.handler.AssetHandler` gränssnitt: Det här gränssnittet beskriver tjänsten som lägger till stöd för specifika MIME-typer. Om du lägger till en ny MIME-typ måste det här gränssnittet implementeras. Gränssnittet innehåller metoder för import och export av specifika dokument, för att skapa miniatyrbilder och extrahera metadata.
* `com.day.cq.dam.core.AbstractAssetHandler` klass: Den här klassen fungerar som bas för alla andra tillgångshanterarimplementeringar och tillhandahåller vanliga funktioner.
* `com.day.cq.dam.core.AbstractSubAssetHandler` klass:
   *  Den här klassen fungerar som bas för alla andra implementeringar av tillgångshanterare och tillhandahåller vanliga funktioner plus vanliga funktioner för subresursextrahering.
   * Det bästa sättet att starta en implementering är att ärva från en tillhandahållen abstrakt implementering som tar hand om de flesta saker och tillhandahåller ett rimligt standardbeteende: klassen com.day.cq.dam.core.AbstractAssetHandler.
   * Den här klassen tillhandahåller redan en abstrakt tjänstbeskrivning. Om du ärver från den här klassen och använder maven-sling-plugin-programmet måste du ange att ärvningsflaggan ska vara true.

Följande metoder måste implementeras:

* `extractMetadata()`: den här metoden extraherar alla tillgängliga metadata.
* `getThumbnailImage()`: den här metoden skapar en miniatyrbild av den skickade resursen.
* `getMimeTypes()`: den här metoden returnerar resursens MIME-typ(er).

Här är en exempelmall:

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler utökar com.day.cq.dam.core.AbstractAssetHandler { // implementerar relevanta delar }

Gränssnittet och klasserna omfattar:

* `com.day.cq.dam.api.handler.AssetHandler` gränssnitt: Det här gränssnittet beskriver tjänsten som lägger till stöd för specifika MIME-typer. Om du lägger till en ny MIME-typ måste det här gränssnittet implementeras. Gränssnittet innehåller metoder för import och export av specifika dokument, för att skapa miniatyrbilder och extrahera metadata.
* `com.day.cq.dam.core.AbstractAssetHandler` klass: Den här klassen fungerar som bas för alla andra tillgångshanterarimplementeringar och tillhandahåller vanliga funktioner.
* `com.day.cq.dam.core.AbstractSubAssetHandler` klass: Den här klassen fungerar som bas för alla andra implementeringar av tillgångshanterare och tillhandahåller vanliga funktioner plus vanliga funktioner för subresursextrahering.

<!--
#### Example: create a specific Text Handler {#example-create-a-specific-text-handler}

In this section, you will create a specific Text Handler that generates thumbnails with a watermark.

Proceed as follows:

Refer to [Development Tools](../sites-developing/dev-tools.md) to install and set up Eclipse with a Maven plugin and for setting up the dependencies that are needed for the Maven project.

After you perform the following procedure, when you upload a txt file into AEM, the file's metadata are extracted and two thumbnails with a watermark are generated.

1. In Eclipse, create `myBundle` Maven project:

    1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
    1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
    1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
    1. Define the Maven project:

        * Group Id: com.day.cq5.myhandler
        * Artifact Id: myBundle
        * Name: My AEM bundle
        * Description: This is my AEM bundle

    1. Click **[!UICONTROL Finish]**.

1. Set the Java Compiler to version 1.5:

    1. Right-click the `myBundle` project, select Properties.
    1. Select Java Compiler and set following properties to 1.5:

        * Compiler compliance level
        * Generated .class files compatibility
        * Source compatibility

    1. Click **[!UICONTROL OK]**. In the dialog window, click Yes.

1. Replace the code in the pom.xml file with the following code:

1. Create the package `com.day.cq5.myhandler` that contains the Java classes under `myBundle/src/main/java`:

    1. Under myBundle, right-click `src/main/java`, select New, then Package.
    1. Name it `com.day.cq5.myhandler` and click Finish.

1. Create the Java class `MyHandler`:

    1. In Eclipse, under `myBundle/src/main/java`, right-click the `com.day.cq5.myhandler` package, select New, then Class.
    1. In the dialog window, name the Java Class MyHandler and click Finish. Eclipse creates and opens the file MyHandler.java.
    1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;

   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/

   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }

    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile the Java class and create the bundle:

    1. Right-click the myBundle project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
    1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). The new text handler is now active in AEM.
1. In your browser, open the Apache Felix Web Management Console. Select the Components tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

-->

## Kommandoradsbaserad mediehanterare {#command-line-based-media-handler}

Med AEM kan du köra valfritt kommandoradsverktyg i ett arbetsflöde för att konvertera resurser (till exempel ImageMagick) och lägga till den nya återgivningen i resursen. Du behöver bara installera kommandoradsverktyget på den disk där AEM-servern finns och lägga till och konfigurera ett processsteg i arbetsflödet. Den anropade processen, som kallas `CommandLineProcess`, gör det även möjligt att filtrera efter specifika MIME-typer och skapa flera miniatyrbilder baserat på den nya återgivningen.

Följande konverteringar kan automatiskt köras och lagras i AEM Resurser:

* EPS- och AI-omvandling med [ImageMagick](https://www.imagemagick.org/script/index.php) och [Ghostscript](https://www.ghostscript.com/)
* FLV-videotranskodning med [FFmpeg](https://ffmpeg.org/)
* MP3-kodning med [LAME](http://lame.sourceforge.net/)
* Ljudbearbetning med [SOX](http://sox.sourceforge.net/)

>[!NOTE]
>
>I andra system än Windows returnerar verktyget FFMpeg ett fel när återgivningar genereras för en videoresurs som har ett enkelt citattecken (&#39;) i filnamnet. Om namnet på videofilen innehåller ett enkelt citattecken tar du bort det innan du överför det till AEM.

Processen `CommandLineProcess` utför följande åtgärder i den ordning de anges:

* Filtrerar filen enligt specifika MIME-typer, om det anges.
* Skapar en tillfällig katalog på den disk som är värd för AEM-servern.
* Direktuppspelar originalfilen till den tillfälliga katalogen.
* Kör det kommando som definieras av argumenten i steget. Kommandot körs i den tillfälliga katalogen med behörigheten för den användare som kör AEM.
* Flyttar tillbaka resultatet till AEM-serverns återgivningsmapp.
* Tar bort den tillfälliga katalogen.
* Skapar miniatyrbilder baserade på dessa återgivningar, om de anges. Miniatyrbildernas antal och mått definieras av stegets argument.

### Ett exempel med ImageMagick {#an-example-using-imagemagick}

I följande exempel visas hur du ställer in kommandoradsprocessteget så att varje gång en resurs med mime-type gif eller tiff läggs till i /content/dam på AEM-servern skapas en vänd bild av originalet tillsammans med tre ytterligare miniatyrbilder (140x100, 48x48 och 10x250).

För att göra detta använder du ImageMagick. ImageMagick är en kostnadsfri programsvit för att skapa, redigera och komponera bitmappsbilder och används vanligtvis från kommandoraden.

Installera först ImageMagick på disken som är värd för AEM-servern:

1. Installera ImageMagick: finns i dokumentationen [till](https://www.imagemagick.org/script/download.php)ImageMagick.
1. Konfigurera verktyget så att du kan köra konverteringen på kommandoraden.
1. Om du vill se om verktyget är korrekt installerat kör du följande kommando `convert -h` på kommandoraden.

   En hjälpskärm med alla möjliga alternativ för konverteringsverktyget visas.

   >[!NOTE]
   >
   >I vissa versioner av Windows (till exempel Windows SE) kanske inte kommandot convert körs eftersom det står i konflikt med det inbyggda konverteringsverktyget som ingår i Windows-installationen. I det här fallet anger du den fullständiga sökvägen för verktyget ImageMagick som används för att konvertera bildfiler till miniatyrer. Exempel, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Om du vill se om verktyget fungerar som det ska lägger du till en JPG-bild i arbetskatalogen och kör kommandot convert `<image-name>.jpg -flip <image-name>-flipped.jpg` på kommandoraden.

   En speglad bild läggs till i katalogen.

Lägg sedan till kommandoradsprocessteget i arbetsflödet för **[!UICONTROL DAM-uppdatering av resurser]** :

1. Gå till **[!UICONTROL arbetsflödeskonsolen]** .
1. Redigera **[!UICONTROL DAM Update Asset]** -modellen på fliken **[!UICONTROL Modeller]** .
1. Ändra inställningarna för det **[!UICONTROL webbaktiverade återgivningssteget]** enligt följande:

   **Argument**:

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. Spara arbetsflödet.

Om du vill testa det ändrade arbetsflödet lägger du till en resurs i `/content/dam`.

1. Hämta en tiff-bild i filsystemet. Byt namn på filen till `myImage.tiff` och kopiera den till, `/content/dam`till exempel med hjälp av WebDAV.
1. Gå till **[!UICONTROL CQ5 DAM]** -konsolen, till exempel `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Öppna resursen **[!UICONTROL myImage.tiff]** och kontrollera att den vända bilden och de tre miniatyrbilderna har skapats.

#### Konfigurera processteget CommandLineProcess {#configuring-the-commandlineprocess-process-step}

I det här avsnittet beskrivs hur du anger **processargument** för **CommandLineProcess**.

Värdena för **processargument** måste avgränsas med kommatecken och får inte börja med ett blanksteg.

<table>
 <tbody>
  <tr>
   <td> Argument-Format</td>
   <td>Beskrivning</td>
  </tr>
  <tr>
   <td> mime:&lt;mime-type&gt;</td>
   <td><p>Valfritt argument. Processen används om resursen har samma MIME-typ som argumentet.</p> <p>Flera MIME-typer kan definieras.</p> </td>
  </tr>
  <tr>
   <td> tn:&lt;width&gt;:&lt;height&gt;</td>
   <td><p>Valfritt argument. Processen skapar en miniatyrbild med de dimensioner som definieras i argumentet.</p> <p>Flera miniatyrbilder kan definieras.<br /> </p> </td>
  </tr>
  <tr>
   <td> cmd: &lt;kommando&gt;</td>
   <td><p>Definierar det kommando som ska köras. Syntaxen beror på kommandoradsverktyget.</p> <p>Endast ett kommando kan definieras.</p> <p>Följande variabler kan användas för att skapa kommandot:<br/></p> <p><code>${filename}</code>: indatafilens namn, t.ex. "original.jpg"<br/><code>${file}</code>: indatafilens fullständiga sökvägsnamn, till exempel "/tmp/cqdam0816.tmp/original.jpg"<br/><code>${directory}</code>: indatafilens katalog, till exempel "/tmp/cqdam0816.tmp".<br/> <code>${basename}</code>: namnet på indatafilen utan filnamnstillägg, t.ex. original<br/> <code>${extension}</code>: tillägg för indatafilen, till exempel JPG<br/></p></td>
  </tr>
 </tbody>
</table>

Om till exempel ImageMagick är installerat på den disk som är värd för AEM-servern och du skapar ett processsteg med **CommandLineProcess** som implementering och följande värden som **Processargument**:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

När arbetsflödet körs gäller steget endast resurser som har bild/gif eller mime:image/tiff som mime-types, skapar det en vänd bild av originalet, konverterar den till .jpg och skapar tre miniatyrbilder med måtten: 140x100, 48x48 och 10x250.

Använd följande **processargument** för att skapa de tre standardminiatyrbilderna med ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Använd följande **processargument** för att skapa den webbaktiverade återgivningen med ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>Steget **CommandLineProcess** gäller bara för Resurser (noder av typen `dam:Asset`) eller underordnade objekt till en resurs.
