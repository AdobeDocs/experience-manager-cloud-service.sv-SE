---
title: Bygg engagerande Forms med kärnkomponenter och headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Bygg engagerande Forms med kärnkomponenter och headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: f65c5241e1e61e5a0bd9981778939caa313de76a
workflow-type: tm+mt
source-wordcount: '3412'
ht-degree: 3%

---


# Bygg engagerande Forms med kärnkomponenter och headless

## Lab-översikt

I detta praktiska labb lär du dig:

Hur man använder AEM Forms för att enkelt skapa anpassningsbara formulär med hjälp av de senaste kärnkomponenterna som är förenliga med AEM Sites, möjliggör datainhämtning i flera kanaler genom att leverera de adaptiva formulären som headless-formulär till webben, mobiler och chatt. Du får också lära dig de effektivaste strategierna när det gäller format, anpassningar och gränssnittsutveckling.

## Viktiga uppgifter

* **Affärsflexibilitet**: Som affärsanvändare kan jag enkelt skapa formulärupplevelser för flera kanaler.

* **Framåtutvecklare**: Som frontutvecklare kan jag styra användarupplevelsen med headless-formulär.

* **Utvecklarhastighet**: Som utvecklare kan jag enkelt och konsekvent anpassa webbplatser och Forms-komponenter.

## Förutsättningar


+++AEM Forms som Cloud Service, sandlåda



<table>
        <thead>
            <tr><th>Lab-ID</th><th>URL för författarinstans</th><th>Publiceringsinstans-URL</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## Lektion 1

### Syfte

Bekanta dig med AEM Forms as a Cloud Service miljö.

### Lektionssammanhang

I den här lektionen lär du dig att bekanta dig med AEM Forms as a Cloud Service miljö genom att navigera i användargränssnittet.

### Utövning

1. Öppna webbläsaren och ange webbadressen till Cloud Servicens författarmiljö. Till exempel:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Logga in i Cloud Servicens redigeringsmiljö. Inloggningsuppgifterna för din författarmiljö delas med dig under labbet.

1. När du är inloggad navigerar du till användargränssnittet för AEM Forms. Klicka **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Klicka **Forms och dokument**. Stäng alla popup-fönster som rör inställningar eller information.

   ![](/help/forms/assets/screenshot2028113929.png)

   Alla tillgängliga formulär visas.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lektion 2

### Syfte

Skapa ett adaptivt formulär med hjälp av de senaste centrala komponenterna, konfigurera och skicka in formuläret.

### Lektionssammanhang

I den här lektionen kommer du som företagsanvändare att skapa ett anpassningsbart formulär för flera kanaler, som webben, mobiler och chatt, med hjälp av anpassningsbar formulärredigering och standardiserade OOTB-kärnkomponenter för datainhämtning.

### Utövning

1. Skapa en slutpunkt för överföring av formuläret:

   1. Öppna <https://requestbin.com/> på en ny flik i webbläsaren.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Klicka **Skapa en offentlig behållare** och kopiera slutpunkts-URL:en.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Skapa ett anpassat formulär med hjälp av guidegränssnittet:

   1. Navigera till AEM Forms som Cloud Service och gå till Forms och Dokument på fliken Webbläsare som används i lektion 1.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Klicka **Skapa** och väljer Adaptiv form.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Välj **Tom med kärnkomponenter** mall från mallurvalsskärmen enligt nedan:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Klicka på **Stil** och väljer **wknd-tema** tema enligt nedan:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Klicka på **Inlämning** och väljer **Skicka till REST-slutpunkt** och ange det publika facket i
      **URL för begäran om POST** enligt nedan:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Klicka **Skapa**. Ange ett namn och en rubrik för formuläret. Till exempel: **konturer**. Klicka **Skapa**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Den adaptiva formulärredigeraren öppnas. Stäng alla popup-fönster eller dialogrutor för inställningar eller information. Klicka på komponentwebbläsaren till vänster och lägg till **Sidfot** -komponenten längst ned i det tomma formuläret.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. Rubriken är en del av den adaptiva formulärmallen. Det gör det enkelt att tillhandahålla ett konsekvent sidhuvud/sidfot i alla adaptiva formulär. Du kan också välja att göra den redigerbar i formuläret, vilket visas för sidfotskomponenten i nästa steg.

   1. Lägg till en **Titel** till formulärets mitt.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Lägg till en **Textindata** efter komponenten title.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Lägg till en **Nummerindata** -komponenten.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Lägg till en **Skicka-knapp** till formuläret.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Klicka på **Titel** så att **popup-meny** visas. Klicka på **Ikonen Redigera** på menyn för att redigera etiketten.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Retur `Contact Us` som rubriktext.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Klicka på **Textindata** så att snabbmenyn visas. Klicka på **Ikonen Redigera** på menyn för att redigera etiketten.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Retur **Fullständigt namn** som fältetikett.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Klicka på **Nummerindata** så att snabbmenyn visas. Klicka på **Ikonen Redigera** på menyn för att redigera etiketten.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Ange **Telefonnummer** som fältetikett.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Lägg till valideringar i formuläret:

   1. Klicka på **Telefonnummer** så att snabbmenyn visas. Klicka på **Ikon för skiftnyckel** på menyn för att konfigurera fältet.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Öppna **valideringsflik** markerar du fältet **Obligatoriskt** och klicka **Klar**. Meddelandet om att åtgärden lyckades visas.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Klicka **Förhandsgranska** för att förhandsgranska formuläret ur ett slutanvändarperspektiv.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Fyll i formuläret med provdata
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Skicka formuläret
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Kontrollera skickade data på fliken Begäranbehållare.
      ![](/help/forms/assets/screenshot2028125829.png)

Använd ett föriskapat registreringsformulär för den återstående övningen.

1. Öppna AEM Forms gränssnitt, till exempel `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`och väljer registreringsformuläret.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Klicka **Publicera**.

   ![](/help/forms/assets/screenshot2028115629.png)

   Meddelandet om att åtgärden lyckades visas.

   ![](/help/forms/assets/screenshot2028115729.png)

   Publicerings-URL:en för formuläret skulle likna `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Om du vill visa det publicerade formuläret ska du ersätta program-ID:t (pXXXXXX) och miljö-ID:t (eXXXXXX) i ovanstående URL med ID:n för din miljö.

## Lektion 3

### Syfte

Uppdatera format med hjälp av vedertagna metoder för utveckling av klientprogram.

### Lektionssammanhang

I den här lektionen lär du dig hur du enkelt kan uppdatera format för det tidigare skapade adaptiva formuläret.

### Utövning

Konfigurera lokal databas för temat:

1. Öppna kommandotolken eller kommandotolken med administratörsbehörighet:

   ![](/help/forms/assets/screenshot2028115829.png)

1. Använd följande kommando på kommandotolken för att navigera till **c:\git** mapp

   ```Shell
   cd c:\git
   ```

1. Använd följande kommando för att klona koden för temat Framtend:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Använd följande kommando i den listade ordningen för att navigera till **aem-forms-theme-canvas** och öppna Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Välj **Författarna av alla filer i den överordnade mappen är betrodda** och klicka **Ja, jag litar på författarna**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Om du vill återge formuläret som finns i molntjänstens publiceringsmiljö byter du namn på `env_template` -fil.  Om du vill byta namn på filen högerklickar du på **env_template** och väljer **Byt namn** alternativ.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Ange följande värden för variablerna i .env-filen och spara filen:

   * **AEM_URL**: Ange molntjänstens publiceringsmiljö. Till exempel, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: Ange formulärets sökväg. Om formulärsökvägen till exempel är `/content/forms/af/registration`, skulle värdet för den här variabeln vara `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. Kör följande kommando i kommandotolken:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Om du får ett meddelande där du ombeds att uppdatera npm via `npm notice Run npm nstall -g npm@9.6.0`ignorera meddelandet.
   > * Kör inte andra npm-kommandon om inte annat anges i arbetsboken.


1. Kör nu följande kommando för att förhandsgranska formuläret.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   När ovanstående kommando har körts väntar du på `webpack compiled` meddelande. Formuläret visas på en webbläsarflik.

   >[!NOTE]
   >
   >Om du får en tom skärm i webbläsaren när du har kört `npm run live` i mer än 3-4 minuter, ändra `localhost` i webbläsarens URL till 127.0.0.1 och tryck **Retur**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. I Visual Studio Code öppnar du `PROJECT\src\site\_variables.scss` -fil. Lägg märke till `$error` färg är en skugga av RED.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Skicka formuläret i webbläsaren för att se den röda färgen i **Förnamn** fält.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Ange **$error** färg till **#5736Web** och spara filen.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Uppdatera webbläsaren och skicka formuläret. Observera att felfärgen i förnamnsfältet har ändrats i enlighet med detta.

   ![](/help/forms/assets/screenshot2028121129.png)

1. I kommandotolken trycker du på **CTRL+C**, ange **Y** och tryck **Retur** för att avsluta npm-processen. Det är viktigt att stoppa npm-servern så att den inte hamnar i konflikt med nästa uppsättning övningar.
1. Stäng fönster för Visual Studio-kod och kommandotolk.

## Lektion 4

### Syfte

Rendera formuläret till webb-/mobilgränssnitt och andra gränssnitt som en headless-form.

### Lektionssammanhang

I den här lektionen får du som frontutvecklare lära dig hur du kan återge den adaptiva formen som tidigare skapats som en headless-form med hjälp av ett ramverk för reaktionsspektrumdesign.

### Utövning

Konfigurera lokal databas med hjälp av ett reaktionsstartprojekt:

1. Öppna kommandotolken med administratörsbehörighet.

   ![](/help/forms/assets/screenshot2028115829.png)

1. Använd följande kommando på kommandotolken för att navigera till **c:\git** mapp

   ```Shell
   cd c:\git
   ```

1. Använd följande kommando för att klona startprojektet för adaptiv formulärreaktion:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Använd följande kommandon i den angivna ordningen för att navigera till **response-starter-kit-aem-headless-forms** och öppna Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Fönstret Visual Studio Code öppnas.

   ![](/help/forms/assets/screenshot2028117429.png)

Så här återger du formuläret som finns i molntjänstens publiceringsmiljö:

1. Byt namn på filen env_template till .env. Om du vill byta namn högerklickar du på **env_template** och väljer **Byt namn** alternativ.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Ange följande värden för variablerna i .env-filen. Spara filen när du har uppdaterat variablerna.

   * **AEM_URL**: Ange URL:en för molntjänstens publiceringsmiljö. Till exempel, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: Ange sökvägen till det anpassade formulär som skapades i föregående lektion. Till exempel, `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Öppna kommandofönstret, kontrollera att du befinner dig i katalogen response-starter-kit-aem-headless-forms och kör följande kommando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Kör följande kommando i kommandotolken:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   Ovanstående kommando startar en lokal utvecklingsserver som skulle återge formulärdefinitionen som hämtats från AEM på ett headless sätt med hjälp av frontend-biblioteket för reaktionsspektrum.

   >[!NOTE]
   >
   > 
   > Om du får en tom skärm i webbläsaren när du har kört `npm start` i mer än 3-4 minuter, ändra `localhost` i webbläsarens URL till 127.0.0.1 och tryck **Retur**.

   ![](/help/forms/assets/screenshot2028118229.png)

Låt oss kontrollera hur reglerna verkställs i den här rubrikfria formen:

1. Välj **Markera kryssrutan för att få 5 % rabatt** alternativ. Det efterföljande alternativet för att använda kreditkort är inaktiverat.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Avmarkera **Markera kryssrutan för att få 5 % rabatt** för att aktivera kreditkortsalternativet.

   ![](/help/forms/assets/screenshot2028126329.png)

Låt oss göra ändringar i formuläret på servern som företagsanvändare och automatiskt se ändringarna som återspeglas i det headless-formuläret.

1. Öppna AEM Forms gränssnitt i webbläsaren. Till exempel: [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Välj **registrering** formulär och klicka **Redigera.** Formuläret öppnas i redigeraren för anpassade formulär.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Välj **Telefonnummer** och klicka på **Ikonen Redigera (pennikonen)** i verktygsfältet. Om du inte kan se popup-verktygsfältet växlar du till redigeringsläget genom att klicka på **Redigera** överst till höger, vänster till **Förhandsgranska** -knappen.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Ändra etiketten till Mobilnummer. Klicka på ett tomt utrymme i formuläret så sparas ändringarna i formuläret.

   ![](/help/forms/assets/screenshot2028119729.png)

Låt oss publicera det uppdaterade formuläret för att sprida ändringarna till publiceringsmiljön.

1. Markera registreringsformuläret på fliken för AEM Forms-hanteringsgränssnittet och klicka på **Avpublicera**. Om du inte ser **Avpublicera** går du vidare till steg 3 för att publicera ändringarna direkt.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Klicka **Avpublicera**. Klicka **Stäng** i respektive dialogruta.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. När webbläsaren har uppdaterats markerar du registreringsformuläret och klickar på **Publicera**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Klicka **Publicera**. Klicka **Stäng** i respektive dialogruta.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Uppdatera webbläsarfliken med det headfria formuläret synligt. Observera att telefonnummeretiketten har ändrats till Mobilnummer.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Öppna kommandotolkfönstret som används för att starta **response-starter-kit-aem-headless-forms** projekt, tryck **CTRL+C** och sedan ange **Y** och tryck på Retur för att avsluta npm-processen. Det är viktigt att stoppa npm-servern så att den inte hamnar i konflikt med nästa uppsättning övningar.

1. Stäng fönster för Visual Studio-kod och kommandotolk.


## Lektion 5

### Syfte

Rendera formuläret som ett headless-formulär med Google Material UI

### Lektionssammanhang

I den här lektionen lär du dig att återge den adaptiva formen som tidigare skapats som ett headless-formulär med Google Material UI.

### Utövning

Konfigurera lokal databas med hjälp av huvudanvändargränssnittets startprojekt:

1. Öppna kommandotolken med administratörsbehörighet.

   ![](/help/forms/assets/screenshot2028115829.png)


1. Använd följande kommando på kommandotolken för att navigera till **c:\git** mapp:

   ```Shell
   cd c:\git
   ```

1. Kör följande kommandon i den angivna ordningen för att skapa en mapp med namnet mui och navigera till multimappen med följande kommandon:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Använd följande kommando för att klona startprojektet för adaptiv formulärreaktion:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Använd följande kommando i den listade ordningen för att navigera till **response-starter-kit-aem-headless-forms** och öppna koden i Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Så här återger du formuläret som finns i molntjänstens publiceringsmiljö:

1. Byt namn på **env_template** fil till **.env** -fil. Om du vill byta namn högerklickar du på **env_template** och markera **Byt namn**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Ange följande värden för variablerna i .env-filen. Spara filen när du har uppdaterat variablerna. Använd **CTRL + S** växla kombination för att spara filen.

   * **AEM_URL**: Ange URL:en för molntjänstens publiceringsmiljö. Till exempel: [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: Ange sökvägen till det anpassade formulär som skapades i föregående lektion. Till exempel /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Öppna kommandofönstret och kontrollera att du är vid **response-starter-kit-aem-headless-forms** och kör följande kommando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Kör följande kommando i kommandotolken:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   Kommandot startar en lokal utvecklingsserver och återger formulärdefinitionen som hämtats från AEM utan rubrik med hjälp av Google materialgränssnittets bibliotek i förgrunden.

   >[!NOTE]
   >
   >Om du får en tom skärm i webbläsaren när du har kört `npm start` i mer än 3-4 minuter, ändra `localhost` i webbläsarens URL till 127.0.0.1 och tryck **Retur**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Så här utvärderar du körningen av samma affärslogik i den här formuläråtergivningen:

   Välj **Markera kryssrutan för att få 5 % rabatt**. Det följande alternativet **Vill du ansöka om ett kreditkortsformulär för Web.Finance Corporate?** inaktiveras.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lektion 6

### Syfte

Skapa ett alternativt utseende och känsla för den headless-formen med materialvariationer för UI-komponenter

### Lektionssammanhang

I den här lektionen lär du dig som gränssnittsutvecklare hur du skapar en alternativ representation av olika komponenter med hjälp av materialgränssnittet för det adaptiva formulär som tidigare skapats av företagsanvändaren.

### Utövning

Uppdatera variationen av komponenterna i det headless-projektet. Ändra varianten på textindatakomponenten i användargränssnittet till `OutlinedInput`:

1. I Visual Code navigerar du till textindatakomponenten genom att öppna `index.tsx` fil på `src/components/textinput/index.tsx`.

1. Lägg till `//` i början av kodraden 103. Raden konverteras till en kommentar.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Lägg till följande på rad 104 om du vill använda en annan variant av komponenten och spara filen. Använd **CTRL + S** växla kombination för att spara filen.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   Det är viktigt att använda korrekt skiftläge för &#39;OutlinedInput&#39;-varianten, annars misslyckas kompileringen. Kompileringen av den lokala utvecklingsmiljön startar automatiskt i kommandotolken. Vänta tills följande meddelande visas

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Uppdatera webbläsaren, om den inte uppdateras automatiskt, för att se hur textinmatningskomponenten använder en annan variant.

   ![](/help/forms/assets/screenshot2028127729.png)


   Den här ändringen sker för slutanvändare utan att formulärdefinitionen på AEM Forms Server ändras och gäller specifikt för den aktuella huvudlösa kanalen. Till exempel webbkanalen i det här labbet.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Stäng Visual Studio-kod och kommandotolken i Windows.

## Vanliga frågor och svar

+++ Är guiden Adaptiv blankett tillgänglig offentligt?

Ja, det finns med AEM Forms som Cloud Service.

+++


+++ Är kärnkomponenterna tillgängliga för allmänheten?

Ja, de adaptiva kärnkomponenterna i Forms finns tillgängliga med AEM Forms som Cloud Service.

+++

+++ Är headless-formulär tillgängliga för allmänheten?

Ja, formulär utan rubrik finns med AEM Forms som Cloud Service.

+++

+++ Kräver Headless-formulär en separat licens?

Nej, Headless-formulär använder samma licensvärde, antal formulärinskickade formulär.

+++

+++ Finns kärnkomponenter och headless-formulär med AEM 6.5 Forms?

Ja, både adaptiva formulär och headless-komponenter finns tillgängliga med AEM Forms 6.5 Service Pack 16 och senare.

+++


## Nästa steg

Nu när ni har lärt er att skapa anpassningsbara formulär och leverera dem till flera kanaler med hjälp av headless-formulär, bör ni försöka att använda era nya kunskaper i praktiken. Ha kul och gör det bara genom att skapa och leverera enastående datainhämtningsupplevelser till slutanvändarna, var de än är, i stor skala!

## Resurser

* [Introduktion av komponenter i adaptiva Form Core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Skapa anpassningsbara formulär med hjälp av kärnkomponenter](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Uppdatera format för grundkomponentbaserad AF](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Headless adaptive forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Använda startkit för Headless React](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


