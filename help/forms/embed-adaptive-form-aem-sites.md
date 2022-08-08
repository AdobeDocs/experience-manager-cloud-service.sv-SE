---
title: Bädda in ett anpassat formulär på AEM Sites-sidan
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: Du kan använda AEM Forms Container-komponenten för att lägga till eller bädda in adaptiv Forms på en AEM Sites-sida för att fylla i och skicka ett formulär utan att lämna AEM Sites-sidorna.
feature: Adaptive Forms
source-git-commit: dac38b2a90b2a1969e5332b8a658e8f1e0e5eccb
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---

# Bädda in ett anpassat formulär på en AEM webbplatssida {#embed-an-adaptive-form-to-aem-sites-page}

## Översikt {#overview}

Med AEM Forms kan formulärutvecklare smidigt bädda in anpassningsbara formulär på en AEM Sites-sida eller en webbsida som ligger på en annan plats än AEM. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret.

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

På AEM Sites-sidan kan du lägga till ett adaptivt formulär med:

* **[AEM Forms Container-komponent](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms innehåller en komponent som du kan lägga till på webbplatsens sidor. Med AEM Forms Container-komponenten kan du bädda in ett adaptivt formulär.

* **[Resursläsare](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Alla formulär är tillgängliga under Assets. Du kan dra och släppa formuläret som en resurs på sidan.

## Förutsättningar {#prerequisites}

Om du vill bädda in ett adaptivt formulär på en AEM Sites-sida som använder en redigerbar mall måste du se till att AEM Form-komponent är konfigurerad som en tillåten komponent i den associerade mallen. Mer information finns i **Princip och egenskaper (layoutbehållare)** avsnitt i [Skapa sidmallar](/help/sites-authoring/templates.md).

Om en platssida använder en statisk mall måste du konfigurera den i styckesystemet på webbplatssidan. Se [Konfigurera komponenter i designläge](/help/sites-authoring/default-components-designmode.md) för mer information.

## Bädda in ett anpassat formulär {#af-component}

Så här bäddar du in ett anpassat formulär med AEM Forms Container-komponenten:

1. Öppna sidan AEM webbplatser i redigeringsläge där du vill bädda in ett adaptivt formulär.
1. Dra AEM Forms Container-komponenten på sidan från panelen Komponentwebbläsaren. Du kan också söka efter ett anpassat formulär i Resurser-webbläsaren och dra och släppa det på sidan Platser. Formuläret bäddas in i en AEM Forms-behållare. Du kan skapa och lägga till ett nytt adaptivt formulär eller bädda in ett befintligt adaptivt formulär.

   >[!NOTE]
   >
   >Flera AEM Forms Container-komponenter på en sida stöds inte.

1. Om du vill skapa och bädda in ett nytt formulär trycker du på **Skapa formulär** ikon. Ett fönster där det nya formuläret skapas öppnas.

1. Tryck på den inbäddade AEM Forms Container-komponenten på webbplatssidan och tryck sedan på ![settings_icon](assets/settings_icon.png) i åtgärdsfältet. The **[!UICONTROL Edit AEM Forms Container]** öppnas.
1. Ange följande i dialogrutan Redigera AEM Forms-behållare.

   <!-- * **Asset Type:** Select the type of asset to embed. The options are Adaptive Form -->
   * **Resurssökväg**: Bläddra och välj det adaptiva formulär som ska bäddas in. Den fylls i automatiskt om du släppte den från Assets-webbläsaren.
   * **Efterbeställning** : Välj den åtgärd som ska utlösas när formulär skickas. Du kan välja att visa ett tackmeddelande eller en tacksida.

      * **Tack**: Skriv ett meddelande med RTF-redigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.
      * **Tack**: Bläddra och välj den sida som ska visas när formuläret skickas. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
         * **Omdirigering till dig som tackar dig**: Aktivera alternativet att ersätta sidan som innehåller det inbäddade adaptiva formuläret med tacksidan. I annat fall ersätter Tack-sidan det adaptiva formuläret i AEM Forms-behållaren, utan att de underliggande webbplatserna på sidan uppdateras. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Använd sidspråk**: Använd den lokala delen av AEM Sites-sidan i stället för den anpassade formulärens språkinställning.
   * **Sätt fokus på formulär**: Välj det här alternativet om du vill ange fokus på det första fältet i det adaptiva formuläret.

   * **Tema**: Välj ett tema som definierar format för komponenter i det adaptiva formuläret. Formateringen innehåller utseendeegenskaper som teckensnittsstil, bakgrundsfärg, dimensioner och justering.
   * **Höjd**: Ange behållarens höjd. Lämna det tomt om du vill ändra storlek på behållaren automatiskt.
   * **CSS-klientbibliotek**: Ange sökväg till ett CSS-klientbibliotek.

1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

## Publicera inbäddat adaptivt formulär {#publishing-embedded-adaptive-form}

Vi ska titta på följande scenarier för publicering av ett inbäddat adaptivt formulär på AEM webbplatssida:

* Om du publicerar sidan AEM webbplatser för första gången och den innehåller ett inbäddat adaptivt formulär publicerar du webbplatssidan och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret på en publicerad webbplatssida publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du har ändrat webbplatssidan och det inbäddade adaptiva formuläret publicerar du om webbplatssidan och den inbäddade resursen.

## Ändra inbäddat anpassat formulär  {#modifying-embedded-adaptive-form}

Sidan AEM webbplatser innehåller en referens till det adaptiva formuläret i AEM Forms Container. Därför behålls alla konfigurationer och egenskaper, t.ex. tema, format och skicka-åtgärd, som konfigurerats i den ursprungliga adaptiva formen i den inbäddade adaptiva formen.

Om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret gör du något av följande.

* Öppna originalformuläret i anpassningsbara formulär i respektive redigerare och ändra dem.
* Tryck på det adaptiva formuläret på webbplatssidan i redigeringsläge och tryck sedan på **[!UICONTROL Edit in a new window]**. Det ursprungliga formuläret öppnas i redigeringsläge som du kan ändra.

>[!NOTE]
>
>De ändringar som gjorts i det ursprungliga adaptiva formuläret återspeglas automatiskt i det inbäddade formuläret. Publicera dock om det adaptiva formuläret eller webbplatssidan så att ändringarna på den publicerade sidan återspeglas.

## Överväganden och bästa praxis {#considerations-and-best-practices}

Tänk på följande när du bäddar in anpassningsbara formulär på AEM sidor:

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickat Forms på formulärportalen.
* Den skicka-åtgärd som är konfigurerad i det ursprungliga formuläret behålls i det inbäddade formuläret.
* Upplevelsemål och A/B-tester som konfigurerats på det ursprungliga formuläret fungerar inte i det inbäddade formuläret. Du kan dock använda målinriktning för upplevelser på webbplatssidan för att presentera olika formulär baserat på användarprofiler.
* Om du har konfigurerat Adobe Analytics för det ursprungliga formuläret hämtas analysdata från det inbäddade formuläret i Adobe Analytics. Den är dock inte tillgänglig i rapporten för formuläranalys.
