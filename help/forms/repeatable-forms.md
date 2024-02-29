---
description: Den här självstudiekursen innehåller anvisningar om hur du gör ett avsnitt i ett formulär upprepningsbart
title: Upprepningsbara avsnitt i Edge Delivery Services
feature: Edge Delivery Services
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Upprepningsbara avsnitt i Edge Delivery

Ett upprepningsbart avsnitt är en komponent i ett formulär som dupliceras eller replikeras flera gånger för att samla in information för flera förekomster av samma data.

Ta till exempel ett formulär som används för att samla in information från användare som ansöker om ett lån. Formuläret gör det möjligt för användarna att lämna personuppgifter, inklusive uppgifter om medlånarna. Användare kan ange information för medsökande, med det här avsnittet upprepningsbart.

![Upprepningsbara avsnitt i formulär](/help/forms/assets/eds-repeatable.png)

## Förutsättningar

Konfigurera Edge Delivery Service (EDS) Github-projekt med hjälp AEM boilerplate och klona motsvarande Github-databas på den lokala datorn. Se [självstudiekurs för utvecklare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/build/tutorial.html) för mer information.

## Upprepningsbara avsnitt i Edge Delivery

Låt oss ta ett exempel på en låneblankett. Formuläret gör det möjligt att skicka personuppgifter. Du kan inkludera information om andra sökande med repeterbara avsnitt, med möjlighet att lägga till minst tre avsnitt med samansökande.

>[!NOTE]
>
> * Du kan skapa en Microsoft Excel på din SharePoint-webbplats eller Google Drive för att göra fälten repeterbara i ett formulär.
> * I det här fallet tar vi ett exempel på en Microsoft SharePoint. Om du vill göra din SharePoint-mapp till innehållskälla följer du de steg som beskrivs i [Så här använder du Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).


Så här lägger du till repeterbara avsnitt i Edge Delivery:

1. [Skapa ett formulär med Microsoft Excel](#author-form)
2. [Förhandsgranska och publicera formuläret](#preview-form)

### Skapa ett formulär med Microsoft Excel {#author-form}

1. Gå till ditt Microsoft SharePoint-konto och öppna eller skapa AEM Edge Delivery-projektkatalog.
2. Öppna en befintlig Microsoft Excel-fil eller skapa ny.
I det här exemplet använder vi ett Excel-blad med namnet `loan-application.xlsx` som skapats i Microsoft SharePoint Site.
3. Lägg till nya kolumner med etiketten som `Repeatable`, `Min`och `Max` i din Microsoft Excel-fil.
4. Ange värdet för `Repeatable` kolumn som `True` för den fältuppsättning som du vill göra upprepningsbar.
5. Ange värden för `Min` och `Max` kolumner. The `Min` värdet är det minsta antal förekomster som panelen upprepas för, medan `Max` är det maximala antalet förekomster som panelen upprepas för.
6. Spara din Microsoft Excel-fil.

>[!NOTE]
>
> Här är [Låneansökan](/help/forms/assets/loan-application.xlsx) Excel-blad som referens.

### Förhandsgranska/publicera formuläret med Edge Delivery Service

1. Öppna eller skapa en ny dokumentfil i en Microsoft SharePoint-webbplats om du vill bädda in Excel-bladet i den med en `Form Block`. Öppna till exempel `index` och lägga till en `Form Block`.
2. Öppna kommandotolken, navigera till AEM Edge Delivery-projektkatalog på den lokala datorn och kör kommandot som `aem up`.

Formuläret är tillgängligt på `https://localhost:3000`, där du klickar på `Add` knappen lägger till ett nytt upprepningsbart avsnitt där information om medsökande kan anges. Du kan också ta bort det repeterbara avsnittet genom att klicka på `Delete` -knappen.

>[!NOTE]
>
> Om du får ett &quot;Sidan hittades inte&quot;-fel när du öppnar formuläret på localhost lägger du till katalognamnet för Microsoft SharePoint-webbplatsen framför den URL där formuläret finns. Exempel: `http://localhost:3000/<dir-name>/`




