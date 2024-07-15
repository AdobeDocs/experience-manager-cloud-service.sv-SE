---
title: Infrastruktur och serviceövervakning i AEM as a Cloud Service
description: Infrastruktur och serviceövervakning i AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
feature: Operations
role: Admin
source-git-commit: c7488b9a10704570c64eccb85b34f61664738b4e
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Infrastruktur och serviceövervakning i AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service ger möjlighet att observera och övervaka: infrastruktur, tjänster och användarupplevelse. Eftersom olika lösningar används och det finns flera övervakningsnivåer är den här sidan uppdelad i tre avsnitt:

* [Extern tillgänglighet](#external-availability)
* [Intern modulövervakning](#module-monitoring)
* [Kundobserverbarhet](#customer-observability)

AEM as a Cloud Service använder hundratals molnbaserade bildskärmar för att kontinuerligt rapportera varje miljös tillstånd (dygnet runt) i 365 dagar per år. Skärmdefinitionerna är inte statiska, de granskas kontinuerligt för att förbättra funktionen för tidig upptäckt. Dessutom har Adobe förfaranden för att ta emot samtal som är utformade för att svara på varningar.

Om du behöver information om andra typer av övervakning, som loggning eller övervakning via Cloud Manager, kan du läsa [Ytterligare resurser](#resources).

## Extern tillgänglighet {#external-availability}

Extern tillgänglighet består av två delar: Service Edge och Custom Monitoring.

### Service Edge {#service-edge}

Alla AEM as a Cloud Service miljöer övervakas med avseende på tillgänglighet. Service Edge Monitoring är dock bara konfigurerat för produktionsmiljöer och mätvärdena används för att beräkna kundens SLA. Miljömiljön och AEM as a Cloud Service CDN beaktas. Service Edge Monitoring har fem olika platser nära den region du valt och kontrollerar regelbundet om de finns tillgängliga. Om en webbplats inte är tillgänglig utlöses en varning och Adobe supportteam och processer engageras.

### Anpassad övervakning {#custom-monitoring}

Med anpassad övervakning kan kunderna välja att tillhandahålla upp till fem olika URL:er för webbegenskaper innan [publiceras](/help/journey-migration/go-live.md). Dessa URL:er ska vara giltiga och returnera en HTTP 200-svarskod. Dessa bildskärmar har stöd för kunder som [tar med sig ett eget CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) framför Adobe CDN och eventuell extern trafikroutning som används framför AEM as a Cloud Service som inte är under Adobe kontroll. Varningar från anpassade övervakningskontroller engagerar Adobe supportteam och processer.

>[!NOTE]
>
> Den här funktionen erbjuds endast för produktionsmiljöer och kunder med [avancerad molnsupport.](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html#support-add-ons) Kontakta ditt Adobe-kontoteam om du har några frågor.

## Intern modulövervakning {#module-monitoring}

Den externa tillgängligheten fokuseras på slutanvändarövervakning, medan intern modulövervakning observerar om delsystemen i arkitekturen fungerar nominellt utan någon funktion eller prestandaförsämring. Om ett problem uppstår utlöses varningar så att reparationer kan utföras antingen automatiskt eller genom att ledningsgruppen är inblandad, i syfte att förhindra kompromisslös tillgänglighet. Det finns olika kategorier av övervakare, som beskrivs nedan är några exempelkontroller:

* CPU-procentandelen för inaktivitet överstiger inte ett visst tröskelvärde.
* Instansomdistributioner överstiger inte en viss frekvens.
* Diskanvändningen är under ett visst tröskelvärde.
* Författarens databasstorlek är inom vissa gränser.
* Säkerhetskopieringen har slutförts.
* Databasens hälsa och prestanda övervakas.
* AEM Cloud-tjänster beter sig som förväntat, inklusive inga blockerade replikeringsköer, konsekventa data och prestandafrågor.

Ytterligare kontroller läggs till i miljöer som tillhandahålls för Forms. Kontrolldefinitionerna är inte statiska och kan komma att ändras och uppdateras.

## Kundobserverbarhet {#customer-observability}

Kunderna kan använda programprestandaövervakningen [New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) som innehåller prestandadata i realtid som samlats in och diagram för analys och felsökning. Genom att använda övervakningssviten kan kunderna direkt observera olika mätvärden som JVM-prestandamått, transaktionstid för Java™, externa bakgrundsanrop och databasanrop.

## Ytterligare resurser {#resources}

* [Prestandaövervakning för New Relic-program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [Loggar för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [Övervaka miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
