---
title: Vanliga frågor om att DHTML Viewer upphör
description: Från och med den 31 januari 2014 upphör Scene7 DHTML-visningsprogramplattform officiellt. I det här meddelandet får du svar på vanliga frågor så att du kan förbereda dig för den här övergången till vår nya HTML5-visningsprogramplattform.
translation-type: tm+mt
source-git-commit: 24d929702fd9eb31b95fdd6d97c7b9978d919804
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 0%

---


# Vanliga frågor om att DHTML Viewer upphör{#dhtml-viewer-end-of-life-faqs}

Från och med den 31 januari 2014 upphör Scene7 DHTML-visningsprogramplattform officiellt. I det här meddelandet får du svar på vanliga frågor så att du kan förbereda dig för den här övergången till vår nya HTML5-visningsprogramplattform.

**Vad är förändringen?**

Från och med den 31 januari 2014 kommer Scene7 officiellt att ha stöd för DHTML-visningsprogrammets plattform.

**Vad betyder&quot;slutet på livscykeln&quot;?**

Slutet av livscykeln innebär att Scene7 (1) inte längre lägger till några funktionsförbättringar i DHTML-visningsprogrammets plattform (2) inte längre åtgärdar eller släpper några felkorrigeringar på DHTML-visningsprogrammets plattform och (3) kundtjänst felsöker inte längre eller ger stöd för eventuella DHTML-relaterade visningsprogramproblem eller frågor.

**Varför gör Scene7 den här ändringen?**

Webbstandarderna utvecklas ständigt och DHTML är en äldre webbutvecklingsteknik som snabbt ersätts av HTML5. Den största begränsningen för DHTML som plattform är att den inte kan skapa den rikedom av upplevelser som HTML5 nu kan ha enhetligt och enklare stöd för i olika webbläsare. Exempel på sådana begränsningar är brist på stöd för olika webbläsare för:

* Anpassade markörer
* Rundade hörn
* Animeringar (som sidvändning, zoomövergångar)
* Effekter (som skuggor, glöd)
* Fullständigt teckensnittsstöd
* Plugin-lös videouppspelning

Specifikt för Scene7 DHTML-visningsprogramplattformen är både den JSP-baserade lösningen och Javascript-API:erna inte optimerade för mobila enheter för att utnyttja multitouch- och gestfunktionerna. Och även om DHTML-visningsprogram som släpptes 2011/början av 2012 är optimerade för mobilen var de svåra att anpassa och underhålla på grund av bristen på ett flexibelt komponentbaserat utvecklingsramverk för SDK.

Scene7 har beslutat sig för att investera i en HTML5-baserad visningsprogramplattform, som bygger på dessa begränsningar för DHTML och snabb branschanpassning med HTML5 som en ny standard för både datorer och mobiler. Investeringen kommer att ge våra kunder en stabil plattform som de kan använda för att skapa mer engagerande interaktiva visningsprogram som kan nå användare på flera olika skärmar, inklusive datorer, iOS och Android-enheter.

**Hur vet jag om mitt visningsprogram använder DHTML-plattformen?**

Kontrollera om:

1. Ditt företag använder ett användbart Scene7-visningsprogram som anges i den här tabellen, där&quot;Viewer Technology&quot; är&quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Ditt företag använder ett visningsprogram som har skapats som en ny förinställning baserad på ett användningsklart Scene7-visningsprogram i den här tabellen där&quot;Viewer Technology&quot; är&quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Ditt företag använder ett anpassat visningsprogram som har skapats från den JSP-baserade DHTML-lösningen:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. Ditt företag använder ett anpassat visningsprogram som har skapats från JavaScript API:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. Ditt företag använder ett anpassat visningsprogram som har skapats med det utfällbara DHTML-API:t för flera skärmar:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. Ditt företag använder ett anpassat visningsprogram som har skapats med det utfällbara DHTML-API:t för datorer:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. Företaget använder ett enhetsidentifieringsbibliotek som är en del av DHTML-visningspaketet:

   Leta efter JS-inkluderingar av &quot;sj_deviceDetect.js&quot; i koden.

   Detta har ersatts av den nya JS-enhetsidentifieringskoden här: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**Vad är den nya visningsprogramplattformen?**

Ersättningen för DHTML är Scene7 HTML5-visningsprogramplattformen som består av båda:

* HTML5 färdiga visningsprogram med mobiloptimerad interaktion för olika typer av visningsprogram, inklusive grundläggande zoom, utfällbar zoom, bilduppsättningar, färgruteuppsättningar, flerdimensionell rotation och blandade media. Fullständiga aktuella exempel på dessa visningsprogram finns i: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* HTML5 viewer SDK som möjliggör omfattande anpassning av Adobe Scene7-visningsprogram för webbplatser och enheter som stöds av HTML5 (som iOS och Android), vilket ger maximal flexibilitet och kreativitet för att ge tittaren ett varumärke som både ser ut och interaktivt ut. Fördelen med återanvändbara prestandaoptimerade komponenter minskar den totala kostnaden för visningsprogramutveckling och snabbar upp den anpassade utvecklingen.

**När har HTML5-visningsprogramplattformen de funktioner jag behöver för att gå över från DHTML-visningsprogramplattformen?**

Scene7 släppte den första SDK:n för HTML5-visningsprogrammet hösten 2011 när version 5.5 startades. Sedan dess har vi lagt till många funktioner till plattformen och utökat stöd för fler och fler typer av tittare. För de vanligaste kraven för visningsprogram har HTML5-visningsprogramplattformen förmodligen redan de funktioner som du behöver migrera nu. Och vi fortsätter att satsa stort på denna visningsprogramplattform med releaser varje kvartal.

För att avgöra om dina krav på visningsprogram kan uppfyllas idag med HTML5-visningsprogramplattformen, se följande dokumentation:

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (för visningsfunktioner och anpassningsfunktioner som är färdiga)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (för att komma åt SDK API-dokumentationen)

Om du fortfarande är osäker på om HTML5 Viewer SDK kan uppfylla dina krav eller inte kan du kontakta vårt professionella tjänstteam.

**Hur övergår jag mina tittare till HTML5-plattformen?**

Scene7 erbjuder följande alternativ för att övergå till HTML5-plattformen:

1. Använd en av Scene7 färdiga HTML5-visningsprogram som du hittar exempel på här: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. Konfigurera en av Scene7 färdiga HTML5-visningsprogram under SPS-programkonfigurationen. På så sätt kan du anpassa vissa beteenden, t.ex. visningsprogrammets storlek, övergångar, zoombeteende: [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. Anpassa utseendet på och känslan i Scene7 färdiga HTML5-visningsprogram genom att ändra CSS för att ändra visuell design som knappbilder, placering, genomskinlighet, bakgrundsfärger osv.: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. Skapa ett anpassat HTML5-visningsprogram från grunden med SDK, som du kan hämta här: [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). Du kan använda professionella tjänster för att bygga ett anpassat visningsprogram eller låta ett eget webbutvecklingsteam bygga det.

**Vad gäller för webbläsare som inte stöder HTML5?**

HTML5 stöds på många mobila enheter och webbläsare och fortsätter att dra fördel av det. Trots att HTML5 inte stöds i Internet Explorer 8 eller tidigare har Scene7 utvecklat vår HTML5-visningsprogramplattform för att utöka stödet till och med IE 7 och IE 8. Med Scene7 HTML5-visningsprogram kan du nå en överväldigande majoritet av både dator- och mobilanvändare med en enda utvecklingsplattform.

Aktuella systemkrav från och med HTML5 SDK version 2.2.1 är:

* Microsoft® Windows® XP eller senare, Macintosh® OS X 10.6 eller senare
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 eller senare
* iOS 3.2.2 eller senare
* Certifierad på iPhone3 eller senare och iPad1 eller senare (inbyggda webbläsare)
* Android OS 2.2 eller senare

Om du vill kontrollera om webbläsaren är kompatibel med vår HTML5-visningsprogramplattform startar du följande exempelvisningsprogram:

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

Om du ser den inzoomade bilden genom att hålla musen över huvudbilden eller dra fingret över den, så är det en webbläsare/enhet som stöds.

**Vilka alternativ har jag om jag vill vara aktiv i produktionen med mitt befintliga DHTML-visningsprogram?**

Även om du fortfarande kan vara aktiv i produktion med DHTML-baserade visningsprogram är det viktigt att notera att det inte kommer att finnas några förbättringar, felkorrigeringar eller kundvård efter den 31 januari 2014. Därför rekommenderar vi starkt alla kunder att gå över till vår mer robusta HTML5-visningsprogramplattform. . Om din företagssituation förhindrar en sådan övergång före EOL-datumet kan du dock välja att kontraktera med professionella tjänster för att förlänga den underhållsperiod som stöds. Kontakta din kontoansvarige om du vill ha mer information.

**Vem kontaktar jag för mer information?**

Om dessa frågor och svar inte besvarar alla dina frågor, [använd Admin Console för att skapa ett supportärende](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) eller kontakta din kontoansvarige på Adobe.
