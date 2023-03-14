---
title: Användning av CIF-produkt- och kategoriväljare
description: Lär dig hur du använder CIF-produkt- och kategoriväljare i dina kundhandelskomponenter för att hjälpa författare och marknadsförare att arbeta effektivt med e-handelsprodukter och katalogdata.
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
source-git-commit: d054f960f13b7308dbf42556ef60a971e880197e
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# AEM för innehåll och e-handel {#cif-pickers}

AEM Content &amp; Commerce Authoring innehåller en uppsättning redigeringsverktyg som hjälper AEM att effektivt arbeta med produktdata och kataloger för e-handel. Produktväljaren och kategoriväljaren är en del av CIF-tillägget och används av CIF-kärnkomponenterna. Projekt kan använda de här väljarna i alla komponentdialogrutor för att välja produkter eller kategorier.

## Produktväljare {#product-picker}

För att produktväljaren ska kunna användas i en projektkomponent måste utvecklaren lägga till `commerce/gui/components/common/cifproductfield` till en komponentdialogruta. Använd till exempel följande för cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

I produktfältet kan användaren navigera till den produkt som användaren vill välja via de olika vyerna. Som standard returnerar produktfältet produktens ID, men det kan konfigureras med `selectionId` -attribut.

Produktväljarfältet har stöd för följande valfria egenskaper:

- selectionId (id, uid, sku, instruktionsmarginal, combinedSlug, combinedSku) - gör att du kan välja vilket produktattribut som ska returneras av väljaren (standard = id). När du använder sku returneras sku för den valda produkten, när du använder combinedSku, och en sträng som base#variant returneras med skus för basprodukten och den valda varianten, eller en enda sku om en basprodukt väljs.
- filter (folderOrProduct, folderOrProductOrVariant) - filtrerar innehållet som ska återges av väljaren när du navigerar i produktträdet. folderOrProduct - återger mappar och produkter. folderOrProductOrVariant - återger mappar, produkt- och produktvarianter. Om en produkt eller produktvariant återges blir den också valbar i väljaren. (default = folderOrProduct)
- multiple (true, false) - aktivera valet av en eller flera produkter (standard = false)
- emptyText - för att konfigurera det tomma textvärdet för väljarfältet

Standardegenskaper för diaglogsfält som `name`, `fieldLabel`, eller `fieldDescription` stöds också.

>[!CAUTION]
>
>The `cifproductfield` -komponenten kräver `cif.shell.picker` clientlib. Om du vill lägga till ett clientlib i en dialogruta kan du använda egenskapen extraClientlibs.
>[!CAUTION]
>
>Från och med CIF Core Components version 2.0.0 finns stöd för `id` togs bort och ersattes med `uid`. Vi rekommenderar att du använder `sku` eller `slug` som produkt-ID. Vi fortsätter att stödja `id` endast för projekt som använder CIF Core Components version 1.x.

Ett fullt fungerande exempel på `cifproductfield` finns i [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) projekt. Se även [Anpassa dialogrutor](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) av dokumentationen AEM kärnkomponenter.

## Kategoriväljaren {#category-picker}

Kategoriväljaren kan användas i en komponentdialogruta på ett liknande sätt som produktväljaren.

Följande kodutdrag kan användas i en cq:dialog-konfiguration:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

Fältet för kategoriväljare har stöd för följande valfria egenskaper:

- selectionId(id, uid, instruktionsmarginal, urlPath, idAndUrlPath _(borttagen)_, uidAndUrlPath _(borttagen)_) - gör att du kan välja vilket kategoriattribut som ska returneras av väljaren (standard = id).
- multiple (true, false) - aktivera markering av en eller flera kategorier (standard = false)

Standardegenskaper för diaglogsfält som `name`, `fieldLabel`, eller `fieldDescription` stöds också.

>[!CAUTION]
>
>Samma som `cifproductfield` komponenten `cifcategoryfield` -komponenten kräver också `cif.shell.picker` clientlib. Om du vill lägga till ett clientlib i en dialogruta kan du använda `extraClientlibs` -egenskap. Se [Anpassa dialogrutor](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) av dokumentationen AEM kärnkomponenter.
>[!CAUTION]
>
>Från och med CIF Core Components version 2.0.0 finns stöd för `id` togs bort och ersattes med `uid`. Vi rekommenderar att du använder `uid` eller `urlPath` som kategoriidentifierare. Vi fortsätter att stödja `id` &amp; `idAndUrlPath` endast för projekt som använder CIF Core Components version 1.x.

Ett fullt fungerande exempel på `cifcategoryfield` finns i [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) projekt.
