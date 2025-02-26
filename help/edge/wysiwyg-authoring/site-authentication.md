---
title: Konfigurera webbplatsautentisering för innehållsredigering
description: Läs om hur AEM Live har stöd för tokenbaserad autentisering och hur du kan konfigurera AEM att använda autentisering med WYSIWYG-redigering.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 6d28b831fb902173bb5fbadd4aa2a52ba58e0a3b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Konfigurera webbplatsautentisering för innehållsredigering {#site-authentication}

Läs om hur AEM Live har stöd för tokenbaserad autentisering och hur du kan konfigurera AEM att använda autentisering med WYSIWYG-redigering.

## Ökning {#overview}

AEM Live har stöd för tokenbaserad autentisering. Webbplatsautentisering används vanligtvis på både förhandsgransknings- och publiceringswebbplatser, men kan även konfigureras så att endast de enskilda webbplatserna skyddas.

>[!NOTE]
>
>Om du väljer att aktivera webbplatsautentisering måste du konfigurera den även i AEM redigeringsmiljöer

## Krav {#requirements}

Om du vill konfigurera webbplatsautentisering för användning med innehållsredigering måste du först utföra följande uppgifter:

* I det här dokumentet förutsätts att du redan har skapat en webbplats för ditt projekt baserat på [Utvecklarhandboken Komma igång för WYSIWYG Authoring med Edge Delivery Services-handboken.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* Du måste redan ha [aktiverat den svarslösa funktionen för ditt projekt.](/help/edge/wysiwyg-authoring/repoless.md)

## Konfigurera webbplatsautentisering {#configure-authentication}

Mer information om hur du konfigurerar webbplatsautentisering finns i dokumentet [Konfigurera webbplatsautentisering](https://www.aem.live/docs/authentication-setup-site).

Observera följande information när du konfigurerar autentisering:

* ID för det tekniska kontot
* Din webbplatsautentiseringstoken

Dessa objekt krävs för att slutföra konfigurationen av webbplatsautentisering för din AEM-redigeringsmiljö.

## Konfigurera redigeringsmiljö {#authoring-environment}

När webbplatsautentiseringen har konfigurerats kan du aktivera den i AEM redigeringsmiljö.

1. Logga in på AEM-författarinstansen och gå till **Verktyg** -> **Cloud-tjänster** -> **Edge Delivery Services-konfiguration** och välj den konfiguration som skapades automatiskt för platsen. Tryck eller klicka på **Egenskaper** i verktygsfältet.
1. I fönstret **Edge Delivery Services Configuration** väljer du fliken **Authentication** och anger följande värden, som du noterade när du konfigurerade platsautentisering.

   * **ID för det tekniska kontot**
   * **Webbplatsautentiseringstoken**

   ![Edge Delivery Services-konfiguration](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. Tryck eller klicka på **Spara och stäng**.
