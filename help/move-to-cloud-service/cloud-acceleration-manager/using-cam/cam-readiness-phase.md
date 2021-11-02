---
title: Beredningsfas i molnaccelerationshanteraren
description: Den här sidan innehåller en översikt över beredskapsfasen i Cloud Acceleration Manager.
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: ba405db754fd6335c76180c7520ab9c08e259f6e
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 4%

---

# Beredningsfas i molnaccelerationshanteraren {#readiness-phase-cam}

När du har skapat ett projekt i Cloud Acceleration Manager kan du nu starta utvärderingen av den aktuella AEM-implementeringen i beredskapsfasen.

Beredskapsfasen omfattar:

* [Best Practices Analysis](#best-practices-analysis)
* [Planering och installation](#planning-setup)

Följ stegen nedan för att gå till beredskapsfasen:

1. Klicka på projektkortet för att öppna projektstartsidan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. Navigera till **Beredskap** som visas i figuren nedan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Mer information finns i Skapa och hantera ett projekt i Cloud Acceleration Manager.

## Använda analyskort för metodtips {#best-practices-analysis}

Följ stegen nedan för att använda Best Practices Analysis-kortet:

1. Klicka på **Granska** från **Best Practices Analysis** kort.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. Följ de här stegen för att hämta BPA (Best Practices Analyzer).

   >[!NOTE]
   >För att undvika att affärskritiska instanser påverkas rekommenderar vi att du kör BPA i en redigeringsmiljö som är så nära produktionsmiljön som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Alternativt kan det köras på en klon av författarmiljön i produktion.

   1. Navigera till [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portalen och hämta Best Practices Analyzer som en zip-fil.

      >[!NOTE]
      >Granska [Använda Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) om du vill lära dig hur du kör BPA.

   1. Exportera rapporten i CSV-format

1. Klicka på **Överför ny rapport** för att överföra BPA-rapport i CAM.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >Rapporten kan inte överföras om du är i webbläsarens Incognito-läge.

1. När du har överfört en ny rapport visas rapporten Best Practices Analysis.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Granska och utforska kontrollpanelen Best Practices Analysis i CAM. Se avsnittet nedan [Analysrapport om metodtips för granskning](#analysis-report) för mer information.

   >[!NOTE]
   >När du överför en ny rapport återställs alla bedömningar.

### Använda Förhandsgranska {#print-preview-cam}

Du kan välja alternativet för förhandsgranskning i Cloud Acceleration Manager för att få en utskrivbar förhandsgranskning av rapporterna eller för att skriva ut rapporten till ett PDF-format för att göra den enkel att dela.

Följ stegen nedan:

1. Klicka på **Förhandsgranska utskrift** -ikonen enligt nedan.

   ![bild](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Klicka på **Förhandsgranska utskrift** öppnar en ny flik där rapporten visas i en förhandsgranskning som kan skrivas ut. Klicka på **Skriv ut** för att skriva ut rapporten i PDF-format.

   >[!IMPORTANT]
   >* Alternativet **Spara som PDF** rekommenderas och stöds för ovanstående funktioner.
   >* Om webbläsarens utskriftsknapp används skrivs bara en sida ut.


   ![bild](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview2.png)

### Använda Visa trendlinje {#trendline-view-cam}

När du överför mer än en BPA-rapport (Best Practices Analyzer) i ett projekt kan du välja **Visa trendlinje** möjlighet att visa och jämföra resultat från historiska BPA-rapporter.

Följ stegen nedan för att visa rapporter från trendlinjealternativet:

>[!NOTE]
>När du överför mer än en BPA-rapport i ett projekt visas **...** ikon.

1. Navigera till projektet och klicka på **Granska** från **Best Practices Analysis** i **Beredskap** fas.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Klicka på **...** för att visa listrutan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >Rapporten som visas är alltid den rapport som har det senaste rapportdatumet.

1. Klicka på **Visa trendlinje**, vilket visas i figuren nedan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. Klicka på **Visa trendlinje** öppnar trendlinjevyn för rapporten, så som visas i figuren nedan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view3.png)

   >[!NOTE]
   >Trendlinjerapporten visar resultaten från de historiska BPA-rapporterna i en grafisk representation.
   >
   >Du ser två diagram som visar trenden för:
   >1. **Trend för rapportresultat**
   >1. **Anpassade komponenter och malltrend**

   >
   >Du kan lägga till eller ändra den grafiska vyn via listrutan enligt bilden nedan:
   >![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view4.png)


### Analysrapport om metodtips för granskning {#analysis-report}

Utforska följande kort som finns på sidan Best Practices Analysis Report:

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Med varje kort kan du
>* klicka på varje kort för att öppna den tillhörande fliken
>* bokmärk alla rapportflikar (inklusive filtrering) för delning eller framtida hämtning
>* använda informationsikonen för att visa information om varje rapportsökning


#### Rapportegenskaper {#report-properties}

The **Rapportegenskaper** kort innehåller information om rapportegenskaper som rapportdatum, varaktighet, filter, överföringsdatum och information om Adobe Experience Manager (AEM).

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### Rapportöversikt {#report-overview}

Detta **Rapportöversikt** kortet innehåller rapportresultat och allvarlighetsgrader som gäller vid bedömning av om det är klart att gå över till AEM as a Cloud Service, vilket visas i figuren nedan.

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

Om du klickar på den här rapporten öppnas **Rapport** -fliken.

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

Du kan filtrera rapporten baserat på prioritet, undertyp eller antal.

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Se [Tolka rapporten Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) för att lära sig mer om resultatkategorier och prioritetsnivåer.

#### Utvärdering av bästa praxis {#best-practices-assessment}

Alternativet Best Practices Assessment (Utvärdering av bästa praxis) ger en bedömning av din aktuella AEM och ger vägledning om nästa steg för att anta AEM bästa praxis. Du kan granska följande information på den här fliken:

* Översikt över AEM
* Anpassade komponenter och mallar
* Ytterligare resultat
* Långsamma frågor
* Underhållsåtgärder

#### Utvärdering av migreringskomplexitet {#migration-complexity-assessment}

Med alternativet Utvärdering av migreringskomplexitet kan du bedöma hur komplicerat det är att migrera den befintliga AEM till AEM as a Cloud Service.

Du kan granska följande information på den här fliken:

* Översikt över AEM
* Bedömning
* Överväganden vid innehållsmigrering

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Använda Planera och konfigurera kort {#planning-setup}

Följ det här avsnittet för att utforska aktivitetskortet Planning and Setup.

1. Klicka på **Visa** från **Planering och installation** kort. Det här kortet innehåller allt relevant innehåll som hjälper dig att planera och konfigurera din AEM migrering.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. En innehållskarusell visar all relevant information för den här fasen av migreringsresan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Ta bort en analysrapport om bästa praxis {#delete-trendline}

Följ stegen nedan för att ta bort en rapport från trendlinjevyn:

>[!IMPORTANT]
>En rapport kan bara tas bort när mer än en rapport har överförts till ett projekt.

1. Navigera till projektet och klicka på **Granska** från **Best Practices Analysis** i **Beredskap** fas.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Klicka på **...** för att visa listrutan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

1. Klicka på **Visa trendlinje**, vilket visas i figuren nedan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. Klicka på borttagningsikonen i dialogrutan **Trendlinjerapport** skärm.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view5.png)

1. Klicka på **Ta bort** för att bekräfta borttagningen.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view6.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in i Cloud Acceleration Manager och hur du skapar ett projekt är du nu redo att gå vidare till nästa steg i [Implementeringsfas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
