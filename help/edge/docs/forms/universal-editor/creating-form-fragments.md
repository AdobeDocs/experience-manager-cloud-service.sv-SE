---
title: Skapa formulärfragment för WYSIWYG-baserad redigering
description: Lär dig hur du skapar formulärfragment i den universella redigeraren och lägger till dem i formulär.
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 0%

---

# Skapa formulärfragment i Universal Editor

<!--
<span class="preview"> This feature is available through the early access program. To request access, send an email with your GitHub organization name and repository name from your official address to <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . For example, if the repository URL is https://github.com/adobe/abc, the organization name is adobe and the repository name is abc.</span> 

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>
-->

Formulärfragment är återanvändbara komponenter som eliminerar repetitivt utvecklingsarbete och säkerställer konsekvens i alla era formulär. I stället för att återskapa vanliga avsnitt som kontaktinformation, adressinformation eller godkännandeavtal för varje formulär kan du skapa dessa element en gång som fragment och återanvända dem i flera formulär.

**Vad du ska göra i den här artikeln:**

- Förstå affärsvärdet och de tekniska funktionerna i formulärfragment
- Skapa återanvändbara formulärfragment med Universal Editor
- Integrera fragment i befintliga blanketter med rätt konfiguration
- Hantera fragmentets livscykel och bevara enhetlighet i alla formulär

**Affärsfördelar:**

- **Minskad utvecklingstid**: Bygg gemensamma formuläravsnitt en gång, återanvänd överallt
- **Förbättrad konsekvens**: Standardiserade layouter och innehåll i alla formulär
- **Förenklat underhåll**: Uppdatera ett fragment en gång för att återspegla ändringar i alla formulär som använder det
- **Förbättrad efterlevnad**: Se till att regelsektionerna är konsekventa och uppdaterade

Formulärfragment i Edge Delivery Services har stöd för avancerade funktioner som kapslade fragment, flera instanser i ett och samma formulär samt smidig integrering med datakällor.

## Förstå formulärfragment

Formulärfragment i Edge Delivery Services har kraftfulla funktioner för modulär formulärutveckling:

**Kärnfunktioner:**

- **Konsekvenshantering**: Fragment behåller identiska layouter och innehåll i flera formulär. Med metoden&quot;ändra en gång, spegla överallt&quot; tillämpas uppdateringar av ett fragment automatiskt på alla formulär i förhandsgranskningsläget.
- **Flera användningsområden**: Lägg till samma fragment flera gånger i ett enda formulär, var och en med oberoende databindning till olika datakällor eller schemaelement.
- **Kapslade strukturer**: Skapa komplexa hierarkier genom att bädda in fragment i andra fragment för avancerade formulärarkitekturer.

**Tekniska krav:**

- **GitHub URL-konsekvens**: Både fragmentet och alla formulär som använder det måste ange samma GitHub-databas-URL
- **Fristående redigering**: Fragment kan bara ändras i sin fristående form; ändringar kan inte göras i värdformuläret

**Publiceringsbeteende:**

>[!IMPORTANT]
>
>I förhandsgranskningsläget återspeglas fragmentändringarna omedelbart i alla formulär. I publiceringsläget måste du publicera om både fragmentet och alla formulär som använder det för att se uppdateringar.

>[!CAUTION]
>
>Undvik rekursiva fragmentreferenser (kapsling av ett fragment i sig) eftersom detta orsakar återgivningsfel och oväntat beteende.

## Förutsättningar

**Tekniska installationskrav:**

- [GitHub-databasen har konfigurerats](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) med en anslutning upprättad mellan din AEM-miljö och GitHub-databasen
- [Det senaste adaptiva Forms-blocket](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) har lagts till i GitHub-databasen (för befintliga Edge Delivery Services-projekt)
- Instans av AEM Forms Author med Edge Delivery Services-mall tillgänglig
- Åtkomst till URL:en för AEM Forms as a Cloud Service-författarinstansen och URL:en för GitHub-databasen

**Nödvändig kunskap och behörigheter:**

- Grundläggande förståelse för formulärdesignkoncept och komponenthierarki
- Välbekant med gränssnittet i den universella redigeraren och arbetsflöden för att skapa formulär
- Behörigheter på författarnivå i AEM Forms för att skapa och hantera formulärresurser
- Förstå organisationens formulärstandarder och krav på återanvändbara komponenter

## Arbeta med Edge Delivery Services-formulärfragment

Du kan skapa Edge Delivery Services-formulärfragment i den universella redigeraren och lägga till de skapade fragmenten i Edge Delivery Services-formulär. Du kan utföra följande åtgärder med Edge Delivery Services-formulärfragment:

- [Skapa formulärfragment](#creating-form-fragments)
- [Lägga till formulärfragment i ett formulär](#adding-form-fragments-to-a-form)
- [Hantera formulärfragment](#managing-form-fragments)

+++ Skapa formulärfragment

Så här skapar du ett formulärfragment i den universella redigeraren:

1. Logga in på din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Klicka på **Skapa > Adaptivt formulärfragment**.

   ![Skapa fragment](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Guiden **Skapa adaptivt formulärfragment** visas.
1. Välj den Edge Delivery Services-baserade mallen på fliken **Välj mall** och klicka på **[!UICONTROL Next]**.
   ![Välj Edge Delivery Services-mall](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Ange rubrik, namn, beskrivning och taggar för fragmentet. Se till att du anger ett unikt namn för fragmentet. Om det finns ett annat fragment med samma namn kan fragmentet inte skapas.
1. Ange **GitHub-URL**. Om din GitHub-databas till exempel har namnet `edsforms`, finns den under kontot `wkndforms`, är URL:en `https://github.com/wkndforms/edsforms`.

   ![grundläggande egenskaper](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Valfritt) Klicka för att öppna fliken **Formulärmodell** och välj en av följande modeller för fragmentet på den nedrullningsbara menyn **Välj från**:

   ![Visar modelltyp på fliken Formulärmodell](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **Formulärdatamodell (FDM)**: Integrera datamodellsobjekt och datatjänster från datakällor i fragmentet. Välj FDM (Form Data Model) om formuläret kräver att du läser och skriver data från flera källor.

   - **JSON-schema**: Integrera formuläret med ett serverdelssystem genom att associera ett JSON-schema som definierar datastrukturen. Det gör att du kan lägga till dynamiskt innehåll med schemaelementen.
   - **Inget**: Anger att fragmentet ska skapas från grunden utan att någon formulärmodell används.

   >[!NOTE]
   >
   > Mer information om hur du integrerar formulär eller fragment med en formulärdatamodell (FDM) i den universella redigeraren för att använda olika backend-datakällor finns i [Integrera formulär med formulärdatamodellen i den universella redigeraren](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Valfritt) Ange **Publiceringsdatum** eller **Avpubliceringsdatum** för fragmentet på fliken **Avancerat**.

   ![Fliken Avancerat](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Klicka på **Skapa** för att generera fragmentet. En dialogruta med redigeringsalternativ visas.

   ![Redigera fragment](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Klicka på **Redigera** för att öppna fragmentet i Universal Editor med standardmallen använd.

   ![Fragment i Universal Editor för redigering](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **Designa fragmentinnehåll**: Lägg till formulärkomponenter (textfält, listrutor, kryssrutor) för att skapa det återanvändbara avsnittet. Detaljerad vägledning om komponenter finns i [Komma igång med Edge Delivery Services för AEM Forms med Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

1. **Konfigurera komponentegenskaper**: Ange fältnamn, verifieringsregler och standardvärden efter behov för ditt användningsfall.

1. **Spara och förhandsgranska**: Spara fragmentet och använd förhandsgranskningsläget för att verifiera layout och funktion.

   ![Skärmbild av ett ifyllt formulärfragment med kontaktinformation i Universell redigerare, med fält för namn, telefon, e-post och adress som kan återanvändas i flera formulär](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**Kontrollpunkt för validering:**

- Fragmentinläsningar utan fel i Universal Editor
- Alla formulärkomponenter återges korrekt
- Fältegenskaper och valideringsregler fungerar som förväntat
- Fragmentet sparas och är tillgängligt i Forms &amp; Documents Console

När fragmentet är klart kan du [integrera det i alla Edge Delivery Services-formulär](#adding-form-fragments-to-a-form).

+++


+++ Lägga till formulärfragment i ett formulär

I det här exemplet visas hur du skapar ett `Employee Details`-formulär som använder `Contact Details`-fragmentet för både den anställdes- och arbetsledarens informationsavsnitt. Detta tillvägagångssätt garanterar enhetlig datainsamling samtidigt som utvecklingsinsatsen minskas.

Så här integrerar du ett formulärfragment i formuläret:

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

   Formulärfragmentet läggs till med referens till formuläret och förblir synkroniserat med det fristående formulärfragmentet.

   ![Skärmbild som visar kontaktinformationsfragmentet som har integrerats i ett medarbetarformulär i den universella redigeraren och som visar hur fragment behåller sin struktur när de återanvänds](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   Du kan förhandsgranska formuläret för att se hur det ser ut i **förhandsgranskningsläget**.

   ![Förhandsgranska](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   På samma sätt kan du upprepa steg 3 till 7 för att infoga `Contact Details`-fragmentet för panelen `Supervisor Details`.

   ![Formulär för personalinformation](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ Hantera formulärfragment

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

+++

## Bästa praxis

**Fragmentdesign och namn:**

- **Använd beskrivande, unika namn**: Välj namn som tydligt anger fragmentets syfte (t.ex. &quot;contact-details-with-validation&quot; i stället för &quot;fragment1&quot;)
- **Planera för återanvändbarhet**: Designa fragment så att de blir sammanhangsberoende och fungerar på olika formulärtyper
- **Håll fragmenten fokuserade**: Skapa engångs-fragment i stället för komplexa flerfunktionskomponenter

**Utvecklingsarbetsflöde:**

- **Testa fragment oberoende**: Verifiera fragmentfunktioner innan du integrerar i formulär
- **Behåll konsekventa GitHub-URL:er**: Se till att samma databas-URL används för alla relaterade fragment och formulär
- **Syftet med dokumentfragment**: Inkludera tydliga beskrivningar och taggar som hjälper teammedlemmarna att förstå när de ska använda varje fragment

**Publikation och underhåll:**

- **Koordinera publikation**: När du uppdaterar fragment bör du planera att publicera om alla beroende formulär samtidigt
- **Versionskontroll**: Använd meningsfulla implementeringsmeddelanden när du uppdaterar fragment för att spåra ändringar över tid
- **Övervaka beroenden**: Håll reda på vilka formulär som använder varje fragment för att utvärdera uppdateringseffekten

>[!TIP]
>
>Fragmentformat, skript och uttryck bevaras när de bäddas in, så design med detta arv i åtanke.

## Sammanfattning

Du har nu lärt dig att utnyttja formulärfragment i Edge Delivery Services för att förbättra utvecklingseffektiviteten och upprätthålla enhetligheten i hela organisationens formulär.

**Viktiga resultat:**

- **Förstå**: Utnyttja affärsvärdet och de tekniska funktionerna i formulärfragment
- **Skapande**: Skapar återanvändbara formulärfragment med den universella redigeraren med rätt konfiguration
- **Integrering**: Fragment har lagts till i formulär med korrekt referenskonfiguration och egenskapskonfiguration
- **Hantering**: Utforskade livscykeloperationer och underhållsarbetsflöden för fragment

**Nästa steg:**

- Skapa ett bibliotek med ofta använda fragment för din organisation
- Upprätta namnkonventioner och styrningsprinciper för fragmentanvändning
- Utforska avancerad integrering med [Form Data Models](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) för dynamiska datadrivna fragment
- Implementera fragmentbaserade blankettmallar för enhetliga användarupplevelser

Era formulär har nu en modulär, underhållningsbar arkitektur som kan skalas effektivt mellan olika projekt samtidigt som de ger en enhetlig användarupplevelse.


