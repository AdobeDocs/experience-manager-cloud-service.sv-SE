---
title: Hur publicerar eller avpublicerar man blanketter i förhandsgransknings- eller publiceringssammanhang?
description: Lär dig publicera och avpublicera formulär från AEM redigeringsmiljö för att förhandsgranska eller publicera instanser. Vare sig du testar formulären i en staging-miljö eller distribuerar dem live för slutanvändare har AEM smidiga verktyg för effektiv hantering.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, manage publication, , AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: 242dcbc5bb541dfac601454fb75dec3bdff1ea64
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---


# &#x200B; Hantera publikation i Experience Manager Forms

Som Adobe Experience Manager Forms-administratör kan du publicera formulär från författarinstansen till Experience Manager Forms. Du kan schemalägga att publicera ett formulär eller en mapp vid ett senare datum eller vid ett senare tillfälle. När de publicerats kan användarna öppna och fylla i formulären.

Du kan publicera eller avpublicera formulär med Publish eller alternativet Hantera publikation som finns i Experience Manager Forms gränssnitt. Om du gör senare ändringar i originalformulären eller -mappen i Experience Manager Forms återspeglas inte ändringarna i publiceringsinstansen förrän du publicerar om från Experience Manager Forms. Det ser till att ändringar som pågår inte är tillgängliga i publiceringsinstansen. Endast ändringar som publiceras av en administratör är tillgängliga i publiceringsinstansen.

## Publish-formulär med Publish

Med publiceringsalternativet kan du publicera ett formulär direkt. I Experience Manager Forms-konsolen går du till den överordnade mappen och väljer ett formulär som du vill publicera. Klicka på alternativet Publish i verktygsfältet, ta en titt på alla referensresurser som skulle publiceras med formuläret och klicka på Publish.

En skärmbild av en dator

Beskrivning genereras automatiskt

## Publish eller Unpublish forms using Manage Publication


Med Hantera publicering kan du publicera eller avpublicera innehåll till och från det valda målet, lägga till innehåll i publiceringslistan från alla formulär- och dokumentmappar, välja referenser att publicera och schemalägga publicering till ett senare datum eller en senare tidpunkt.


I Experience Manager Forms-konsolen går du till den överordnade mappen och väljer ett formulär som du vill publicera. Klicka på alternativet Hantera publikation i verktygsfältet.


En skärmbild av en dator

Beskrivning genereras automatiskt



Följande alternativ är tillgängliga i gränssnittet Hantera publikation:

* Åtgärder

   * Publish: Publish-formulär till det valda målet
   * Avpublicera: Avpublicera formulär från målet

* Mål

   * Publish: Publish-formulär till instansen Experience Manager Forms (AEM) Publish.
   * Förhandsgranska: Publish-formulär till förhandsgranskningsinstansen för Experience Manager Forms (AEM).

* Schemaläggning

   * Nu: Publish blanketter direkt
   * Senare: Publish-formulär baserade på aktiveringsdatum eller -tid



Klicka **Nästa** om du vill fortsätta. På fliken Omfång använder du alternativen Lägg till innehåll för att lägga till mer innehåll för publicering. Du kan t.ex. lägga till fler Forms- eller dokumentfiler.

### Lägg till innehåll

Genom att publicera i Experience Manager Forms kan du lägga till mer innehåll (formulär, resurser och mappar) i publiceringslistan. Du kan lägga till fler formulär, resurser eller mappar i listan från mappen för formulärsanddokument. Men du kan inte lägga till resurser från flera mappar samtidigt.

En skärmbild av en dator

Beskrivning genereras automatiskt

Klicka på knappen **Lägg till innehåll** om du vill lägga till mer innehåll. Du kan lägga till flera resurser från en mapp eller lägga till flera mappar samtidigt. Men du kan inte lägga till resurser från flera mappar samtidigt.

Om du vill konfigurera referenser för publicering eller inte publicering för ett formulär eller andra resurser, markerar du formuläret eller resursen och klickar på Publicerade referenser.

En skärmbild av en dator

Beskrivning genereras automatiskt

Avmarkera de resurser som du vill ska inte publiceras i dialogrutan Publicerade referenser och klicka sedan på Klart.


En skärmbild av en dator

Beskrivning genereras automatiskt


## Publish eller avpublicera ett formulär senare


Förutom att du kan publicera eller avpublicera formulär vid ett senare datum och vid ett senare tillfälle kan du även konfigurera ett arbetsflöde med alternativet Publicera eller avpublicera senare. Formulären publiceras eller publiceras när arbetsflödet är klart. Så här schemalägger du ett formulär för publicering eller avpublicering:

1. Gå till den överordnade mappen på Experience Manager Forms-konsolen och välj det formulär som du vill schemalägga för publicering.
1. Klicka på alternativet Hantera publikation i verktygsfältet.
1. Klicka på Publish eller Avpublicera från åtgärd och välj sedan det mål där du vill publicera eller avpublicera innehållet.

   * Förhandsgranska: Använd alternativet Förhandsgranska om du vill publicera eller avpublicera i en Experience Manager Forms-förhandsvisningsmiljö. Experience Manager Forms förhandsvisningsmiljöer används för att testa under utvecklingsformulär.
   * Publish: Använd alternativet Experience Manager Forms Publish för att skicka formuläret till Experience Manager Forms publiceringsmiljö när formuläret är klart att användas i en produktionsmiljö.


1. Välj Senare från Schemaläggning.

1. Välj ett aktiveringsdatum och ange datum och tid. Klicka på Nästa.

   En skärmbild av en dator

   Beskrivning genereras automatiskt

1. Lägg till innehåll (om det behövs) på fliken Omfång. Klicka på Nästa.

   En skärmbild av en dator

   Beskrivning genereras automatiskt

1, (Valfritt) Ange en arbetsflödestitel på fliken Arbetsflöden. Klicka på Publish Senare.

En skärmbild av en dator

Beskrivning genereras automatiskt

## Bestämmer publiceringsstatus

Det finns flera sätt att avgöra publiceringsstatus:

* Logga in på målinstansen för att verifiera publicerade formulär och andra resurser (beroende på schemalagt datum eller tid).

* Använd tidslinjevyn för att bestämma publiceringsstatus.

* Använd sidinformationsmenyn i Adaptiv Forms-redigerare.