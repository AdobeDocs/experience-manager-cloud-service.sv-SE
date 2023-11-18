---
title: Integrera med Adobe Target
description: Lär dig hur du integrerar Adobe Target med AEM as a Cloud Service med Touch-gränssnittet och Adobe Launch.
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 1%

---

# Integrera med Adobe Target{#integrating-with-adobe-target}

Som en del av Adobe Experience Cloud kan Adobe Target öka innehållets relevans genom målinriktning och mätning i alla kanaler. Integrering av Adobe Target och AEM as a Cloud Service kräver:

* med Touch-gränssnittet för att skapa en målkonfiguration i AEM as a Cloud Service (IMS-konfiguration krävs).
* lägga till och konfigurera Adobe Target som ett tillägg i [Adobe Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html).

Adobe Launch krävs för att hantera egenskaper på klientsidan för både Analytics och Target på AEM (JS-bibliotek/taggar). Integreringen med Launch behövs dock för&quot;Experience Targeting&quot;.

Om du vill exportera Experience Fragments och/eller Content Fragments till Target behöver du bara [Adobe Target Configuration and IMS](/help/sites-cloud/integrating/integration-adobe-target-ims.md).

>[!NOTE]
>
>Kunder som inte har något befintligt Target-konto kan begära åtkomst till Target Foundation Pack för Experience Cloud. Foundation Pack ger begränsad volymanvändning av Target.

## Skapa Adobe Target-konfigurationen {#create-configuration}

1. Navigera till **verktyg** → **Cloud Service**.
   ![Navigering](assets/cloudservice1.png "Navigering")
2. Välj **Adobe Target**.
3. Välj **Skapa** -knappen.
   ![Skapa](assets/tenant1.png "Skapa")
4. Fyll i uppgifterna (se nedan) och välj **Anslut**.
   ![Anslut](assets/open_screen1.png "Anslut")

### IMS-konfiguration {#ims-configuration}

En IMS-konfiguration för både Launch och Target krävs för att Target ska kunna integreras korrekt med AEM och Launch. IMS-konfigurationen för Launch är förkonfigurerad i AEM as a Cloud Service, men mål-IMS-konfigurationen måste skapas (efter att Target har etablerats). Se [IMS-konfiguration som ska användas vid integrering med Adobe Target](/help/sites-cloud/integrating/integration-adobe-target-ims.md) och videon [Integrera Experience Platform Launch och AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html) om du vill lära dig hur du skapar mål-IMS-konfigurationen.

### Adobe Target klientorganisations-ID och Adobe Target klientkod {#tenant-client}

När du konfigurerar fälten för Adobe Target klient-ID och Adobe Target klientkod bör du tänka på följande:

1. För de flesta kunder är innehavar-ID och klientkod samma. Det innebär att båda fälten innehåller samma information och är identiska. Se till att du anger klient-ID i båda fälten.
2. För äldre syften kan du även ange olika värden i fälten Klient-ID och Klientkod.

I båda fallen:

* Som standard kopieras även klientkoden (om den läggs till först) automatiskt till fältet Klient-ID.
* Om det behövs kan du ändra standardinställningen för innehavar-ID.
* Backend-anrop till Target baseras på klientens ID och klientsidans anrop till Target baseras på klientkoden.

Som tidigare nämnts är det första fallet det vanligaste för AEM as a Cloud Service. Oavsett vilket, se till att **båda** fälten innehåller rätt information beroende på dina behov.

>[!NOTE]
>
> Om du vill ändra en befintlig målkonfiguration:
>
> 1. Ange klientorganisations-ID:t igen.
> 2. Återanslut till mål.
> 3. Spara konfigurationen.

### Redigera målkonfigurationen {#edit-target-configuration}

Så här redigerar du målkonfigurationen:

1. Välj en befintlig konfiguration och klicka på **Egenskaper**.
2. Redigera egenskaperna.
3. Välj **Återanslut till Adobe Target**.
4. Välj **Spara och stäng**.

### Lägga till en konfiguration till en plats {#add-configuration}

Om du vill använda en Touch UI-konfiguration på en webbplats går du till: **Webbplatser** > **Välj en webbplatssida** > **Egenskaper** > **Avancerat** > **Konfiguration** > Välj en konfigurationtenant.

## Integrera Adobe Target på AEM sajter med Adobe Launch {#integrate-target-launch}

AEM erbjuder en färdig integrering med Experience Platform Launch. Genom att lägga till Adobe Target-tillägget i Experience Platform Launch kan du använda Adobe Target funktioner på AEM webbsidor. Målbibliotek återges endast med Launch.

>[!NOTE]
>
>Befintliga (äldre) ramverk fungerar fortfarande, men de kan inte konfigureras i Touch-gränssnittet. Adobe rekommenderar att du återskapar variabelmappningskonfigurationerna i Launch.

Som en allmän översikt är integrationsstegen:

1. Skapa en startegenskap
2. Lägg till de tillägg som krävs
3. Skapa ett dataelement (för att hämta hubbparametrar)
4. Skapa en sidregel
5. Bygg och publicera

### Skapa en startegenskap {#create-property}

En egenskap är en behållare som är fylld med tillägg, regler och dataelement.

1. Välj **Ny egenskap** -knappen.
2. Ange ett namn för egenskapen.
3. Som domän anger du den IP/värddator som du vill läsa in startbiblioteket för.
4. Välj **Spara** -knappen.
   ![Launchproperty](assets/properties_newproperty1.png "Launchproperty")

### Lägga till de tillägg som krävs {#add-extension}

**Tillägg** är den behållare som hanterar huvudbiblioteksinställningarna. Adobe Target-tillägget stöder implementeringar på klientsidan genom att använda Target JavaScript SDK för den moderna webben, at.js. Lägg till båda **Adobe Target** och **Adobe ContextHub** tillägg.

1. Välj alternativet Tilläggskatalog och sök efter mål i filtret.
2. Välj **Adobe Target** at.js och klicka på alternativet Install.
   ![Målsökning](assets/search_ext1.png "Målsökning")
3. Välj **Konfigurera** -knappen. Observera konfigurationsfönstret med Target-kontots autentiseringsuppgifter importerade och at.js-versionen för det här tillägget.
4. Välj **Spara** om du vill lägga till måltillägget i Launch-egenskapen. Du bör kunna se måltillägget under **Installerade tillägg** lista.
   ![Spara tillägg](assets/configure_extension1.png "Spara tillägg")
5. Upprepa stegen ovan om du vill söka efter **Adobe ContextHub** tillägg och installation (det här tillägget krävs för integrering med kontexthub-parametrar, baserat på vilken målanpassning som görs).

### Skapa ett dataelement {#data-element}

**Dataelement** är platshållare som du kan mappa kontextnavparametrar till.

1. Välj **Dataelement**.
2. Välj **Lägg till dataelement**.
3. Ange namnet på dataelementet och mappa det till en kontextnavparameter.
4. Välj **Spara**.
   ![Dataelement](assets/data_elem1.png "Dataelement")

### Skapa en sidregel {#page-rule}

I **Regel** definierar och ordnar den en sekvens av åtgärder, som körs på webbplatsen, för att uppnå målgruppsanpassning.

1. Lägg till en uppsättning åtgärder som visas i skärmbilden.
   ![Åtgärder](assets/rules1.png "Åtgärder")
2. I Lägg till parametrar i alla Mboxes lägger du till dataelementet som konfigurerats tidigare (se dataelementet ovan) i den parameter som skickas i mbox-anropet.
   ![Mbox](assets/map_data1.png "Åtgärder")

### Bygg och publicera {#build-publish}

Mer information om hur du skapar och publicerar finns i [page](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html).

## Förändringar i innehållsstrukturen mellan Classic- och Touch UI-konfigurationer {#changes-content-structure}

<table style="table-layout:auto">
  <tr>
    <th>Ändra</th>
    <th>Konfiguration av klassiskt användargränssnitt</th>
    <th>Konfiguration av pekskärmsgränssnitt</th>
    <th>Konsekvenser</th>
  </tr>
  <tr>
    <td>Sökväg till målkonfigurationen.</td>
    <td>/etc/cloudservices/testandtarget/</td>
    <td>/conf/tenant/settings/cloudconfigs/target/</td>
    <td> Tidigare fanns det flera konfigurationer under /etc/cloudservices/testandtarget, men nu finns det en enda konfiguration under en klientorganisation.</td>
  </tr>
</table>

>[!NOTE]
>
>Äldre konfigurationer stöds fortfarande för befintliga kunder (utan möjlighet att redigera eller skapa). Äldre konfigurationer är en del av innehållspaket som överförs av kunder med VSTS.
