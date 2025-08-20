---
title: Användning av CIF produkt- och kategoriväljare
description: Lär dig hur du använder CIF produkt- och kategoriväljare i dina e-handelskomponenter för att hjälpa författare och marknadsförare att arbeta effektivt med e-handelsprodukter och katalogdata.
sub-product: Commerce
topics: Development
version: Experience Manager as a Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# AEM Content &amp; Commerce Authoring Pickers {#cif-pickers}

AEM Content &amp; Commerce Authoring innehåller en uppsättning redigeringsverktyg som hjälper AEM att effektivt arbeta med produktdata och kataloger för e-handel. Produktväljaren och kategoriväljaren ingår i CIF-tillägget och används av CIF Core Components. Projekt kan använda de här väljarna i alla komponentdialogrutor för att välja produkter eller kategorier.

## Produktväljare {#product-picker}

Om du vill använda produktväljaren i en projektkomponent måste utvecklaren lägga till `commerce/gui/components/common/cifproductfield` i en komponentdialogruta. Använd till exempel följande för `cq:dialog`:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

I produktfältet kan du navigera till den produkt som en användare vill välja genom de olika vyerna. Som standard returnerar produktfältet produktens ID, men det kan konfigureras med attributet `selectionId`.

Produktväljarfältet har stöd för följande valfria egenskaper:

- selectionId (id, uid, SKU, instruktionsmarginal, combinedSlug, combinedSku) - gör att du kan välja vilket produktattribut som ska returneras av väljaren (standard = id). Om du använder SKU returneras SKU:n för den valda produkten. Om du använder combinedSku returneras en sträng som base#variant med SKU:erna för basprodukten och den valda varianten, eller en SKU om en basprodukt väljs.
- filter (folderOrProduct, folderOrProductOrVariant) - filtrerar innehållet som ska återges av väljaren när du navigerar i produktträdet. folderOrProduct - återger mappar och produkter. folderOrProductOrVariant - återger mappar, produkter och produktvarianter. Om en produkt eller produktvariant återges blir den också valbar i väljaren. (default = folderOrProduct)
- multiple (true, false) - aktivera valet av en eller flera produkter (standard = false)
- emptyText - för att konfigurera det tomma textvärdet för väljarfältet

Standardegenskaper för dialogrutefält som `name`, `fieldLabel` eller `fieldDescription` stöds också.

>[!CAUTION]
>
>Komponenten `cifproductfield` kräver `cif.shell.picker` clientlib. Om du vill lägga till ett clientlib i en dialogruta kan du använda egenskapen extraClientlibs.

>[!CAUTION]
>
>Från och med CIF Core Components version 2.0.0 har stödet för `id` tagits bort och ersatts med `uid`. Adobe rekommenderar att du använder `sku` eller `slug` som produkt-ID. Adobe har fortsatt stöd för `id` endast för projekt som använder CIF Core Components version 1.x.

Ett fullt fungerande exempel på `cifproductfield` finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) -projektet. Se även [Anpassa dialogrutor](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=sv-SE#customizing-dialogs) i dokumentationen för AEM Core Components.

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

- selectionId(id, uid, instruktionsmarginal, urlPath, idAndUrlPath _(utgått)_, uidAndUrlPath _(utgått)_) - låter dig välja vilket kategoriattribut som ska returneras av väljaren (standard = id).
- multiple (true, false) - aktivera markering av en eller flera kategorier (standard = false)

Standardegenskaper för dialogrutefält som `name`, `fieldLabel` eller `fieldDescription` stöds också.

>[!CAUTION]
>
>Samma som komponenten `cifproductfield` i komponenten `cifcategoryfield` kräver även `cif.shell.picker` clientlib. Om du vill lägga till ett klientlib i en dialogruta kan du använda egenskapen `extraClientlibs`. Se [Anpassa dialogrutor](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=sv-SE#customizing-dialogs) i dokumentationen för AEM Core Components.

>[!CAUTION]
>
>Från och med CIF Core Components version 2.0.0 har stödet för `id` tagits bort och ersatts med `uid`. Adobe rekommenderar att du använder `uid` eller `urlPath` som kategoriidentifierare. Adobe har fortsatt stöd för `id` och `idAndUrlPath` endast för projekt som använder CIF Core Components version 1.x.

Ett fullt fungerande exempel på `cifcategoryfield` finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) -projektet.
