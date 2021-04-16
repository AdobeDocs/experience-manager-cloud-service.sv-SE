---
title: Användning av CIF-produkt- och kategoriväljare
description: Lär dig hur du använder CIF-produkt- och kategoriväljare i dina kundhandelskomponenter för att hjälpa författare och marknadsförare att arbeta effektivt med e-handelsprodukter och katalogdata.
sub-product: Handel
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 0f2747190523613d2fa1f4710dee1c28d4a5148f
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# Redigeringsväljare för AEM och e-handel {#cif-pickers}

AEM Content &amp; Commerce Authoring innehåller en uppsättning redigeringsverktyg som hjälper AEM att effektivt arbeta med produktdata och kataloger för e-handel. Produktväljaren och kategoriväljaren är en del av CIF-tillägget och används av CIF-kärnkomponenterna. Projekt kan använda de här väljarna i alla komponentdialogrutor för att välja produkter eller kategorier.

## Produktväljaren {#product-picker}

Om du vill använda produktväljaren i en projektkomponent måste utvecklaren lägga till `commerce/gui/components/common/cifproductfield` i en komponentdialogruta. Använd till exempel följande för cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

I produktfältet kan användaren navigera till den produkt som användaren vill välja via de olika vyerna. Som standard returnerar produktfältet produktens ID, men det kan konfigureras med attributet `selectionId`.

Produktväljarfältet har stöd för följande valfria egenskaper:

- selectionId (id, uid, sku, instruktionsmarginal, combinedSlug, combinedSku) - gör att du kan välja vilket produktattribut som ska returneras av väljaren (standard = id). När du använder sku returneras sku för den valda produkten, när du använder combinedSku, och en sträng som base#variant returneras med skus för basprodukten och den valda varianten, eller en enda sku om en basprodukt väljs.
- filter (folderOrProduct, folderOrProductOrVariant) - filtrerar innehållet som ska återges av väljaren när du navigerar i produktträdet. folderOrProduct - återger mappar och produkter. folderOrProductOrVariant - återger mappar, produkt- och produktvarianter. Om en produkt eller produktvariant återges blir den också valbar i väljaren. (default = folderOrProduct)
- multiple (true, false) - aktivera valet av en eller flera produkter (standard = false)
- emptyText - för att konfigurera det tomma textvärdet för väljarfältet

Standardegenskaper för diagloger som `name`, `fieldLabel` eller `fieldDescription` stöds också.

Komponenten `cifproductfield` kräver clientlib-objektet cif.shell.picker. Om du vill lägga till ett clientlib i en dialogruta kan du använda egenskapen extraClientlibs.

Ett fullt fungerande exempel på `cifproductfield` finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)-projektet. Se även [Anpassa dialogrutor](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) i dokumentationen för AEM Core Components.

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

- selectionId(id, uid, instruktionsmarginal, idAndUrlPath, uidAndUrlPath) - gör att du kan välja vilket kategoriattribut som ska returneras av väljaren (standard = id). idAndUrlPath och uidAndUrlPath är specialalternativ som lagrar kategorinamnet id/uid och url_path avgränsade med en | tecken som t.ex. 1|men/högst.
- multiple (true, false) - aktivera markering av en eller flera kategorier (standard = false)

Standardegenskaper för diagloger som `name`, `fieldLabel` eller `fieldDescription` stöds också.

Samma som `cifproductfield`-komponenten för `cifcategoryfield`-komponenten kräver även clientlib för cif.shell.picker. Om du vill lägga till ett klientlib i en dialogruta kan du använda egenskapen `extraClientlibs`. Se [Anpassa dialogrutor](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) i dokumentationen för AEM Core Components.

Ett fullt fungerande exempel på `cifcategoryfield` finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)-projektet.
