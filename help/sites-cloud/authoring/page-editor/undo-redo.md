---
title: Ångra och Gör om begränsningar
description: Läs mer om begränsningarna för alternativen Ångra och Gör om i AEM.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Ångra och Gör om begränsningar {#undo-redo}

AEM lagrar en historik över åtgärder som du utför och den sekvens i vilken du utförde dem, så att du kan ångra flera åtgärder i den ordning som du utförde dem och göra om dem för att återanvända en eller flera av åtgärderna om det behövs.

Om ett element på innehållssidan är markerat (till exempel en textkomponent) gäller kommandot ångra och gör om det markerade objektet.

Funktionen för kommandona ångra och gör om liknar den i andra program. Använd kommandona för att återställa webbsidans senaste status när du fattar beslut om innehållet. Om du till exempel flyttar ett textstycke till en annan plats på sidan kan du använda kommandot Ångra för att flytta tillbaka stycket. Om du sedan bestämmer dig för att den föregående positionen var bättre använder du kommandot gör om för att ångra.

Du kan till exempel:

* Gör om åtgärder så länge du inte har gjort någon sidredigering sedan du använde Ångra.
* Ångra högst 20 redigeringsåtgärder (standardinställning).
* Använd även [Kortkommandon](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) för att ångra och göra om.

Du kan använda Ångra och Gör om för följande typer av sidändringar:

* Lägga till, redigera, ta bort och flytta stycken
* Redigera styckeinnehåll direkt
* Kopiera, klippa ut och klistra in objekt på en sida

>[!NOTE]
>
>* Särskilda behörigheter krävs för att ångra och göra om ändringar i filer och bilder.
>* Historiken för ändringar av filer och bilder varar i minst tio timmar. Efter den här gången kan du dock inte ångra ändringarna. Administratören kan ändra standardtiden på tio timmar.
>* Systemadministratören kan konfigurera olika aspekter av funktionerna Ångra/Gör om enligt kraven för din instans.
