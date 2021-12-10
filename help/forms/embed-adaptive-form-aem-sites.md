---
title: 'Hur bäddar jag in ett adaptivt formulär på en AEM webbplatssida? '
description: Du kan bädda in Adaptiv Forms på AEM webbplatssidor. Användarna kan fylla i och skicka formulär utan att lämna webbplatsens sidor.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# Bädda in ett anpassat formulär på AEM {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

[!DNL AEM Forms] gör det möjligt för formulärutvecklare att sömlöst bädda in Adaptiv Forms på en AEM Sites-sida eller en webbsida som ligger utanför AEM. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret.

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

På AEM Sites-sidan kan du lägga till ett adaptivt formulär med:

* **[[!DNL AEM Forms] Behållarkomponent](#af-component)**
   [!DNL AEM Forms] innehåller en komponent som du kan lägga till på dina webbplatssidor. The [!DNL AEM Forms] Med behållarkomponenten kan du bädda in ett anpassat formulär.

* **[Resursläsare](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Alla formulär du skapar finns tillgängliga under Resurser. Du kan dra och släppa formuläret som en resurs på sidan.

## Förutsättningar {#prerequisites}

Om du vill bädda in ett adaptivt formulär på en AEM webbplatssida som använder en redigerbar mall måste du se till att AEM Form-komponenten är konfigurerad som en tillåten komponent i den associerade mallen. Mer information finns i **Princip och egenskaper (layoutbehållare)** avsnitt i [Skapa sidmallar](/help/sites-authoring/templates.md).

Om en platssida använder en statisk mall måste du konfigurera den i styckesystemet på webbplatssidan. Se [Konfigurera komponenter i designläge](/help/sites-authoring/default-components-designmode.md) för mer information.

## Bädda in ett anpassat formulär  {#af-component}

Bädda in ett anpassat formulär med [!DNL AEM Forms] Behållarkomponent:

1. Öppna sidan AEM webbplatser, i redigeringsläge, där du vill bädda in ett adaptivt formulär.
1. Dra och släpp komponentens [!DNL AEM Forms] Behållarkomponent på sidan.

   Du kan också söka efter ett anpassat formulär i Resurser-webbläsaren och dra och släppa det på sidan Platser. Formuläret bäddas in i en [!DNL AEM Forms] Behållare.

   >[!NOTE]
   >
   >Flera [!DNL AEM Forms] Behållarkomponenter på en sida stöds inte.

1. Tryck på den inbäddade [!DNL AEM Forms] Containerkomponenten på webbplatssidan och tryck sedan på ![settings_icon](assets/settings_icon.png) i åtgärdsfältet. The **[!UICONTROL Edit AEM Forms Container]** öppnas.
1. I Redigera [!DNL AEM Forms] Dialogrutan Behållare anger följande.

   * **Resurstyp:** Välj vilken typ av resurs som ska bäddas in. Alternativen är Adaptiv form
   * **Resurssökväg**: Bläddra och välj det adaptiva formulär som ska bäddas in. Den fylls i automatiskt om du släppte den från Assets-webbläsaren.
   * (Endast adaptiv form) **Efterbeställning**: Välj den åtgärd som ska utlösas när formulär skickas. Du kan välja att visa ett tackmeddelande eller en tacksida.

      * **Tack**: Skriv ett meddelande med RTF-redigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.
      * **Tack**: Bläddra och välj den sida som ska visas när formuläret skickas. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
      * **Uppdatera sidan vid överföring**: Aktivera det här alternativet om du vill uppdatera sidan som innehåller det inbäddade adaptiva formuläret så att du kan se tack-sidan. I annat fall ersätter tack-sidan det adaptiva formuläret i dialogrutan [!DNL AEM Forms] behållare utan att sidan uppdateras. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Tema**: Välj ett tema som definierar format för komponenter i det adaptiva formuläret. Formateringen innehåller utseendeegenskaper som teckensnittsstil, bakgrundsfärg, dimensioner och justering.
   * **Höjd**: Ange behållarens höjd. Lämna det tomt om du vill ändra storlek på behållaren automatiskt.
   * **CSS-klientbibliotek**: Ange sökväg till ett CSS-klientbibliotek.


1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

## Publicera inbäddat adaptivt formulär {#publishing-embedded-adaptive-form}

Vi ska titta på följande scenarier för publicering av en inbäddad resurs (Adaptiv form) på AEM webbplatssida:

* Om du publicerar sidan AEM webbplatser för första gången och den innehåller ett inbäddat adaptivt formulär publicerar du sidan med webbplatser och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret på en publicerad webbplatssida publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du har ändrat webbplatssidan och det inbäddade adaptiva formuläret publicerar du om webbplatssidan och den inbäddade resursen.

## Ändra inbäddat anpassat formulär {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM på webbplatssidan upprätthåller en referens till det adaptiva formuläret i [!DNL AEM Forms] Behållare. Därför behålls alla konfigurationer och egenskaper, t.ex. tema, format och överföringsåtgärd, som konfigurerats i det ursprungliga adaptiva formuläret i det inbäddade adaptiva formuläret.

Om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret gör du något av följande.

* Öppna originalformuläret i Adaptive Forms i respektive redigerare och ändra dem.
* Tryck på det adaptiva formuläret på webbplatssidan i redigeringsläge och tryck sedan på **[!UICONTROL Edit in a new window]**. Det ursprungliga formuläret öppnas i redigeringsläge som du kan ändra.

>[!NOTE]
>
>De ändringar som gjorts i det ursprungliga adaptiva formuläret återspeglas automatiskt i det inbäddade formuläret. Publicera dock om det adaptiva formuläret eller webbplatssidan så att ändringarna på den publicerade sidan återspeglas.

## Överväganden och bästa praxis {#considerations-and-best-practices}

Tänk på följande när du bäddar in Adaptiv Forms på AEM webbplatser:

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickat Forms på formulärportalen.
* Den skicka-åtgärd som är konfigurerad i det ursprungliga formuläret behålls i det inbäddade formuläret.
* Upplevelsemål och A/B-tester som konfigurerats på det ursprungliga formuläret fungerar inte i det inbäddade formuläret. Du kan dock använda målinriktning för upplevelser på webbplatssidan för att presentera olika formulär baserat på användarprofiler.
* Om du har konfigurerat Adobe Analytics för det ursprungliga formuläret hämtas analysdata från det inbäddade formuläret i Adobe Analytics. Den är dock inte tillgänglig i rapporten för formuläranalys.

