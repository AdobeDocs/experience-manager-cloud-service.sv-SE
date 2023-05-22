---
title: Infrastruktur- och serviceövervakning på AEM as a Cloud Service
description: Infrastruktur- och serviceövervakning på AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: f55439552e253b8b71b40525454130c6f163e6d4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Infrastruktur- och serviceövervakning på AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service ger möjlighet att observera och övervaka: infrastruktur, tjänster och användarupplevelse. Eftersom olika lösningar används och det finns flera övervakningsnivåer är den här sidan uppdelad i tre avsnitt:

* [Extern tillgänglighet](#external-availability)
* [Intern modulövervakning](#module-monitoring)
* [Kundobserverbarhet](#customer-observability)

AEM as a Cloud Service använder hundratals molnbaserade bildskärmar för att kontinuerligt rapportera varje miljös tillstånd (dygnet runt) i 365 dagar per år. Skärmdefinitionerna är inte statiska, de granskas kontinuerligt för att förbättra funktionen för tidig upptäckt. Dessutom har Adobe utformat förfaranden för att ringa in meddelanden.

Om du behöver information om andra typer av övervakning, som loggning eller övervakning via Cloud Manager, kan du läsa [Ytterligare resurser](#resources) -avsnitt.

## Extern tillgänglighet {#external-availability}

Extern tillgänglighet består av två delar: Service Edge och anpassad övervakning.

### Service Edge {#service-edge}

Alla dina AEM as a Cloud Service miljöer övervakas med avseende på tillgänglighet. Men Service Edge Monitoring är bara konfigurerat för produktionsmiljöer och mätvärdena används för att beräkna kundens SLA. Miljömiljön och AEM as a Cloud Service CDN beaktas. Service Edge Monitoring har fem olika platser nära den valda regionen och kontrollerar regelbundet om den är tillgänglig. Om en webbplats inte är tillgänglig kommer det att utlösa en varning och engagera stödgrupper och processer på Adobe-nivå.

### Anpassad övervakning {#custom-monitoring}

Med anpassad övervakning har kunderna möjlighet att ange upp till fem olika URL:er för webbegenskaper före [live](/help/journey-migration/go-live.md). Dessa URL:er ska vara giltiga och returnera en HTTP 200-svarskod. Dessa skärmar ger stöd åt kunder som [egen CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) framför CDN i Adobe och eventuell extern trafikledning som är anställd framför AEM as a Cloud Service och som inte står under Adobe:s kontroll. Varningar från anpassade övervakningskontroller kommer att engagera Adobe stödgrupper och processer.

>[!NOTE]
>
> Den här funktionaliteten erbjuds endast kunder med [Avancerad molnsupport.](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html#support-add-ons) Om du har några frågor kontaktar du supportärendet via Admin Console.

## Intern modulövervakning {#module-monitoring}

Den externa tillgängligheten fokuseras på slutanvändarövervakning, men den interna modulövervakningen observerar om delsystemen för arkitektur fungerar perfekt utan någon funktion eller prestandaförsämring. Om ett problem uppstår utlöses varningar så att reparationer kan utföras antingen automatiskt eller genom att ledningsgruppen är inblandad, i syfte att förhindra kompromisslös tillgänglighet. Det finns olika kategorier av övervakare, som beskrivs nedan är några exempelkontroller:

* CPU-procentandelen för inaktivitet överstiger inte ett visst tröskelvärde.
* Instansomdistributioner överstiger inte en viss frekvens.
* Diskanvändningen är under ett visst tröskelvärde.
* Författarens databasstorlek är inom vissa gränser.
* Säkerhetskopieringen har slutförts.
* Databasens hälsa och prestanda övervakas.
* AEM Cloud-tjänsterna beter sig som förväntat, inklusive inga blockerade replikeringsköer, konsekventa data- och prestandafrågor.

Ytterligare kontroller läggs till i miljöer som tillhandahålls för Forms. Tänk på att kontrolldefinitionerna inte är statiska och kan ändras och uppdateras.

## Kundobserverbarhet {#customer-observability}

Kunderna kan använda [Prestandaövervakning för New Relic-program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) en programsvit som innehåller realtidsprestandadata som samlats in och diagram för analys och felsökning. Genom att använda övervakningssviten kan kunderna direkt observera olika mätvärden som: Prestandamätningar för JVM, transaktionstid för Java, externa bakgrundsanrop och databasanrop.

## Ytterligare resurser {#resources}

* [Prestandaövervakning för New Relic-program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [Loggning för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [Övervakningsmiljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
