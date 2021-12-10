---
title: Hur lägger jag till variabler i AEM?
description: Lär dig skapa en variabel, ange ett värde för variabeln och använda den i [!DNL AEM Forms] Arbetsflödessteg.
exl-id: d9139ea9-2f86-476c-8767-b36766790f2c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---

# Variabler i Forms-centrerade AEM {#variables-in-aem-forms-workflows}

En variabel i en arbetsflödesmodell är ett sätt att lagra ett värde baserat på dess datatyp. Du kan använda namnet på variabeln i vilket arbetsflödessteg som helst för att hämta värdet som lagras i variabeln. Du kan också använda variabelnamn för att definiera uttryck för att fatta beslut om routning.

I AEM arbetsflödesmodeller kan du:

* [Skapa en variabel](variable-in-aem-workflows.md#create-a-variable) av en datatyp som baseras på den informationstyp som du vill lagra i den.
* [Ange ett värde för variabeln](variable-in-aem-workflows.md#set-a-variable) med hjälp av arbetsflödessteget Ange variabel.
* [Använd variabeln](variable-in-aem-workflows.md#use-a-variable) i alla [!DNL AEM Forms] Arbetsflödessteg för att hämta det lagrade värdet och i stegen ELLER Dela och Gå till för att definiera ett routningsuttryck.

I följande video visas hur du kan skapa, ange och använda variabler i AEM arbetsflödesmodeller:

>[!VIDEO](assets/variables_introduction_1_1.mp4)

Variabler är ett tillägg till befintliga [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) gränssnitt. Du kan använda [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) i ECMAScript för att komma åt metadata som sparats med variabler.

## Skapa en variabel {#create-a-variable}

Du skapar variabler med hjälp av avsnittet Variabler som är tillgängliga i arbetsflödesmodellens sidospak. AEM arbetsflödesvariabler har stöd för följande datatyper:

* **Primitiva datatyper**: Long, Double, Boolean, Date och String
* **Komplexa datatyper**: [Dokument](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html), [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html), [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)och instansen Form Data Model.

>[!NOTE]
>
>Arbetsflöden har endast stöd för ISO8601-format för datatypsvariabler.

Använd datatypen ArrayList för att skapa variabelsamlingar. Du kan skapa en ArrayList-variabel för alla primitiva och komplexa datatyper. Skapa till exempel en ArrayList-variabel och välj String som undertyp för att lagra flera strängvärden med variabeln.

Så här skapar du en variabel:

1. Navigera AEM till Verktyg ![](assets/hammer-icon.svg) > Arbetsflöde > Modeller.
1. Tryck **[!UICONTROL Create]** och ange arbetsflödesmodellens titel och valfria namn. Markera modellen och tryck på **[!UICONTROL Edit]**.
1. Tryck på variabelikonen som är tillgänglig i sidokanten av arbetsflödesmodellen och tryck på **[!UICONTROL Add Variable]**.

   ![Lägg till variabel](assets/variables_add_variable_new.png)

1. I dialogrutan Lägg till variabel anger du namnet och väljer variabeltyp.
1. Välj datatyp från **[!UICONTROL Type]** och ange följande värden:

   * Primitiv datatyp - Ange ett valfritt standardvärde för variabeln.
   * JSON eller XML - Ange en JSON- eller XML-schemasökväg (tillval). Systemet validerar schemasökvägen när egenskaper som är tillgängliga i schemat mappas och lagras till en annan variabel.
   * Formulärdatamodell - Ange en formulärdatamodell.
   * ArrayList - Ange en undertyp för samlingen.

1. Ange en valfri beskrivning för variabeln och tryck på ![ready_icon](assets/Smock_Checkmark_18_N.svg) för att spara ändringarna. Variabeln visas i listan som är tillgänglig i den vänstra rutan.

Tänk på följande när du skapar variabler:

* Skapa så många variabler som ett arbetsflöde kräver. Om du vill spara databasresurser bör du dock använda det minsta antalet variabler som krävs och återanvända variabler när det är möjligt.
* Variabler är skiftlägeskänsliga. Se till att du refererar till variabler med samma skiftläge i arbetsflödet.
* Undvik att använda specialtecken i namnet på variabeln

## Ange en variabel {#set-a-variable}

Du kan använda steget Ange variabel för att ange värdet för en variabel och definiera i vilken ordning värdena ska anges. Variabeln ställs in i den ordning som variabelmappningarna visas i steget för att ange variabel.

Ändringar av variabelvärden påverkar bara instansen av den process i vilken ändringen sker. När ett arbetsflöde initieras och variabeldata ändras påverkar ändringarna bara den instansen av arbetsflödet. Ändringarna påverkar inte andra instanser av arbetsflödet som har initierats tidigare eller som har initierats senare.

Beroende på variabelns datatyp kan du använda följande alternativ för att ange värdet för en variabel:

* **Literal:** Använd alternativet när du vet exakt vilket värde du ska ange. Du kan också använda alternativet för att ange en JSON i form av en sträng.

* **Uttryck:** Använd alternativet när värdet som ska användas beräknas baserat på ett uttryck. Uttrycket skapas i den angivna uttrycksredigeraren.

* **JSON-punktnotation:** Använd alternativet för att hämta ett värde från en JSON- eller FDM-typvariabel.
* **XPATH:** Använd alternativet för att hämta ett värde från en XML-typvariabel.

* **I förhållande till nyttolast:** Använd alternativet när värdet som ska sparas till variabeln är tillgängligt på en sökväg som är relativ till nyttolasten.

* **Absolut sökväg:** Använd alternativet när värdet som ska sparas i variabeln är tillgängligt på en absolut sökväg.

Du kan också uppdatera specifika element i en JSON- eller XML-typvariabel med JSON DOT Notation eller XPATH.

### Lägg till mappning mellan variabler {#add-mapping-between-variables}

Så här lägger du till mappning mellan variabler:

1. Tryck på ikonen Steg i arbetsflödesmodellens sidokicka på arbetsflödets redigeringssida.
1. Dra och släpp **[!UICONTROL Set Variable]** steg till arbetsflödesredigeraren, tryck på steget och välj ![configure_icon](assets/Smock_Wrench_18_N.svg) (Konfigurera).
1. I dialogrutan Ange variabel väljer du **[!UICONTROL Mapping]** > **[!UICONTROL Add Mapping]**.
1. I **Kartvariabel** markerar du variabeln där data ska lagras, väljer mappningsläge och anger ett värde som ska lagras i variabeln. Mappningslägena varierar beroende på variabeltypen.
1. Mappa fler variabler för att skapa ett meningsfullt uttryck. Tryck ![ready_icon](assets/Smock_Checkmark_18_N.svg) för att spara ändringarna.

### Exempel 1: Fråga en XML-variabel för att ange ett värde för en strängvariabel {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Välj en variabel av XML-typ för att lagra en XML-fil. Fråga XML-variabeln för att ange värdet för en strängvariabel för egenskapen som är tillgänglig i XML-filen. Använd **Ange XPATH för XML-variabeln** fält för att definiera egenskapen som ska lagras i strängvariabeln.

I det här exemplet väljer du **formdata** XML-variabel som lagrar **cc-app.xml** -fil. Fråga **formdata** variabel som anger värdet för **e-postadress** strängvariabel som lagrar värdet för **emailAddress** egenskapen finns i **cc-app.xml** -fil.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Ange värdet för en variabel")

### Exempel 2: Använd ett uttryck för att lagra värden baserat på andra variabler {#example2}

Använd ett uttryck för att beräkna summan av variablerna och lagra resultatet i en variabel.

I det här exemplet använder du uttrycksredigeraren för att definiera ett uttryck för att beräkna summan av **tillgångskostnad** och **saldobelopp** variabler och lagra resultatet i **totalvärde** variabel.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Använda uttrycksredigeraren {#use-expression-editor}

Du använder också uttryck för att beräkna värdet för en variabel i körningsmiljön. Variabler tillhandahåller en uttrycksredigerare för att definiera uttryck.

Använd uttrycksredigeraren för att:

* Ange värdet för variabler med andra arbetsflödesvariabler, siffror eller matematiska uttryck.
* Använd arbetsflödesvariabler, sträng, tal eller ett uttryck i ett matematiskt uttryck
* Lägg till villkor för att ange värden för variabler.
* Lägg till operatorer mellan villkor.

![Uttrycksredigeraren](assets/variables_expression_editor_new.png)

Det bygger på den adaptiva regelredigeraren Forms med följande ändringar. Regelredigerare i variabler:

* Har inte stöd för funktioner.
* Inget användargränssnitt för att visa en sammanfattning av regler
* Har ingen kodredigerare.
* Stöder inte aktivering och inaktivering av ett objekts värde.
* Stöder inte inställning av ett objekts egenskap.
* Stöder inte anrop till en webbtjänst.

Mer information finns i [Anpassad regelredigerare för Forms](rule-editor.md).

## Använda en variabel {#use-a-variable}

Du kan använda variabler för att hämta indata och utdata eller spara resultatet av ett steg. Arbetsflödesredigeraren innehåller två typer av arbetsflödessteg:

* Arbetsflödessteg med stöd för variabler
* Arbetsflödessteg utan stöd för variabler

### Arbetsflödessteg med stöd för variabler {#workflow-steps-with-support-for-variables}

Steget Gå till, eller Dela, och alla [!DNL AEM Forms] Arbetsflödessteg stöder variabler.

#### ELLER Dela upp steg {#or-split-step}

Med ELLER-delning skapas en delning i arbetsflödet, varefter endast en gren är aktiv. I det här steget kan du lägga in sökvägar för villkorlig bearbetning i arbetsflödet. Du kan lägga till arbetsflödessteg i varje gren efter behov.

Du kan definiera routningsuttryck för en gren med hjälp av en regeldefinition, ett ECMA-skript eller ett externt skript.

Du kan använda variabler för att definiera routningsuttrycket med hjälp av uttrycksredigeraren. Mer information om hur du använder routningsuttryck för steget ELLER Dela finns i [ELLER Dela upp steg](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#or-split).

I det här exemplet ska du använda [exempel 2](variable-in-aem-workflows.md#example2) för att ange värdet för **totalvärde** variabel. Gren 1 är aktiv om värdet för **totalvärde** variabeln är större än 50000. På samma sätt kan du definiera en regel som gör grenen 2 aktiv om värdet för **totalvärde** variabeln är mindre än 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Välj på liknande sätt en extern skriptsökväg eller ange ECMA-skriptet för routningsuttryck för att utvärdera den aktiva grenen. Tryck **[!UICONTROL Rename Branch]** om du vill ange ett alternativt namn för grenen.

<!-- For more examples, see [Create a workflow model](aem-forms-workflow.md#create-a-workflow-model). -->

#### Gå till steg {#go-to-step}

The **Gå till steg** I kan du ange nästa steg i arbetsflödesmodellen som ska köras, beroende på resultatet av ett routningsuttryck.

Ungefär som i steget ELLER Dela kan du definiera routningsuttryck för Gå till med hjälp av en regeldefinition, ett ECMA-skript eller ett externt skript.

Du kan använda variabler för att definiera routningsuttrycket med hjälp av uttrycksredigeraren. Mer information om hur du använder routningsuttryck för steget Gå till finns i [Gå till steg](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#goto-step).

![Gå till regel](assets/variables_goto_rule1_new.png)

I det här exemplet anger steget Gå till att visa kreditkortsansökan som nästa steg om värdet för **actiontaken** variabeln är lika med **Behöver mer information**.

Fler exempel på hur du använder regeldefinition i steget Gå till finns i [Simulera en for-slinga](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#simulateforloop).

#### Forms-centrerade arbetsflödessteg {#forms-workflow-centric-workflow-steps}

Alla [!DNL AEM Forms] Arbetsflödessteg stöder variabler. Mer information finns i [Forms-centrerat arbetsflöde i OSGi](aem-forms-workflow-step-reference.md).

### Arbetsflödessteg utan stöd för variabler {#workflow-steps-without-support-for-variables}

Du kan använda [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) gränssnitt för att komma åt variabler i arbetsflödessteg som inte stöder variabler.

#### Hämta variabelvärdet {#retrieve-the-variable-value}

Använd följande API:er i ECMA-skriptet för att hämta värden för befintliga variabler baserat på datatypen:

| Variabeldatatyp | API |
|---|---|
| Primitiv (long, Double, Boolean, Date och String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| Dokument | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData().getMetaDataMap(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| Formulärdatamodell | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |


**Exempel**

Hämta värdet för strängdatatypen med följande API:

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Uppdatera variabelvärdet {#update-the-variable-value}

Använd följande API i ECMA-skriptet för att uppdatera värdet för en variabel:

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Exempel**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

Uppdaterar värdet för **lön** variabel till 50000.

### Ange variabler för att starta arbetsflöden {#apiinvokeworkflow}

Du kan använda ett API för att ange variabler och skicka dem för att anropa arbetsflödesinstanser.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) I används model, wfData och metaData som argument. Använd MetaDataMap för att ange värdet för variabeln.

I det här API:t **variableName** variabeln är inställd på **value** med metaData.put(variableName, value);

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**Exempel**

Initiera **doc** dokumentobjekt till en bana (&quot;a/b/c&quot;) och ange värdet för **docVar** variabel till den sökväg som lagras i dokumentobjektet.

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## Redigera en variabel {#edit-a-variable}

1. Tryck på ikonen Variabler i sidledaren i arbetsflödesmodellen på sidan Redigera arbetsflöde. I avsnittet Variabler i den vänstra rutan visas alla befintliga variabler.
1. Tryck på ![redigera](assets/edit.svg) (Redigera) bredvid variabelnamnet som du vill redigera.
1. Redigera variabelinformationen och tryck på ![ready_icon](assets/Smock_Checkmark_18_N.svg) för att spara ändringarna. Du kan inte redigera **[!UICONTROL Name]** och **[!UICONTROL Type]** fält för en variabel.

## Ta bort en variabel {#delete-a-variable}

Ta bort alla referenser till variabeln från arbetsflödet innan du tar bort variabeln. Kontrollera att variabeln inte används i arbetsflödet.

Så här tar du bort en variabel:

1. Tryck på ikonen Variabler i sidledaren i arbetsflödesmodellen på sidan Redigera arbetsflöde. I avsnittet Variabler i den vänstra rutan visas alla befintliga variabler.
1. Tryck på ikonen Ta bort bredvid variabelnamnet som du vill ta bort.
1. Tryck ![ready_icon](assets/Smock_Checkmark_18_N.svg) för att bekräfta och ta bort variabeln.

## Referenser {#references}

Fler exempel på hur du använder variabler i [!DNL AEM Forms] Arbetsflödessteg, se [Variabler i AEM arbetsflöden](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html).
