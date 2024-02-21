---
title: Beredningsfas i molnaccelerationshanteraren
description: Den här sidan innehåller en översikt över beredskapsfasen i Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: f99395870d076d47ef53b01c9fc6579a9f8788a2
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 3%

---

# Beredningsfas i molnaccelerationshanteraren {#readiness-phase-cam}

När du har skapat ett projekt i Cloud Acceleration Manager kan du nu starta utvärderingen av din nuvarande Adobe Experience Manager-implementering (AEM) i beredskapsfasen.

Beredskapsfasen omfattar:

* [Best Practices Analysis](#best-practices-analysis)
* [Planering och installation](#planning-setup)

Följ stegen nedan för att navigera till beredskapsfasen:

1. Klicka på ditt projektkort.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Navigera till startsidan för projektet **Beredskap** som visas i figuren nedan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Mer information finns i Skapa och hantera ett projekt i Cloud Acceleration Manager.

## Använda analyskort för metodtips {#best-practices-analysis}

1. Klicka **Granska** från **Best Practices Analysis** kort.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Hämta BPA (Best Practices Analyzer).

   >[!NOTE]
   >För att undvika att affärskritiska instanser påverkas rekommenderar Adobe att du kör BPA i en redigeringsmiljö. Miljön bör vara så nära produktionsmiljön som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarapplikationer. Alternativt kan det köras på en klon av produktionsredigeringsmiljön.

   1. Navigera till [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portalen och hämta Best Practices Analyzer som en zip-fil.

      >[!NOTE]
      >Granska [Använda Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html#imp-considerations) om du vill lära dig hur du kör BPA.

   1. Exportera rapporten i CSV-format

1. Klicka **Överför ny rapport** så att du kan överföra BPA-rapport i CAM.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >Rapporten kan inte överföras om du är i webbläsarens Incognito-läge.

1. När du har överfört en ny rapport kan du se rapporten Best Practices Analysis.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >Om flera rapporter överförs är rapporten som visas i detalj alltid den som har det senaste skapandedatumet (inte överföringsdatumet).

1. Granska och utforska kontrollpanelen Best Practices Analysis i CAM. Se [Analysrapport om metodtips för granskning](#analysis-report) för mer information.

   >[!NOTE]
   >När du överför en ny rapport återställs alla bedömningar om den är nyare än den tidigare inlästa rapporten.

### Använda Förhandsgranska {#print-preview-cam}

Du kan välja alternativet för förhandsgranskning i Cloud Acceleration Manager för att få en utskrivbar förhandsgranskning av rapporterna eller för att skriva ut rapporten till ett PDF-format för att göra den enkel att dela.

Följ stegen nedan:

1. Klicka på **Förhandsgranska utskrift** -ikon.

   ![bild](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Klicka på den nya fliken med rapporten i en förhandsgranskning som kan skrivas ut **Skriv ut** för att skriva ut rapporten till PDF.

   >[!IMPORTANT]
   >
   >* Alternativet **Spara som PDF** rekommenderas och stöds för ovanstående funktioner.
   >* Om webbläsarens utskriftsknapp används skrivs bara en sida ut.

   ![bild](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Använda Visa trendlinje {#trendline-view-cam}

När du överför mer än en separat BPA-rapport (Best Practices Analyzer) i ett projekt kan du välja **Visa trendlinje** möjlighet att visa och jämföra resultat från historiska BPA-rapporter.

Följ stegen nedan för att visa rapporter från trendlinjealternativet:

>[!NOTE]
>När du överför mer än en distinkt BPA-rapport i ett projekt visas **...** -ikon. Rapporterna betraktas som samma (inte distinkta) om deras värdtid och skapandetid är desamma.

1. Navigera till projektet och klicka **Granska** från **Best Practices Analysis** i **Beredskap** fas.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Klicka **...**.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. I listrutan klickar du på **Visa trendlinje**, vilket visas i figuren nedan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Klicka **Visa trendlinje** öppnar rapportens trendlinjevy.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >Trendlinjerapporten visar resultaten från de historiska BPA-rapporterna i en grafisk representation.
   >
   >Du ser två diagram som visar trenden för:
   > 
   >1. **Trend för rapportresultat**
   >1. **Anpassade komponenter och malltrend**
   >
   >Du kan lägga till eller ändra den grafiska vyn med hjälp av listrutan, vilket visas i bilden nedan:
   >![bild](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Analysrapport om metodtips för granskning {#analysis-report}

Utforska följande kort som finns på sidan Best Practices Analysis Report:

![bild](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Med varje kort kan man
>
>* öppna tillhörande flik
>* bokmärk alla rapportflikar (inklusive filtrering) för delning eller framtida hämtning
>* använda informationsikonen för att visa information om varje rapportsökning

#### Rapportegenskaper {#report-properties}

The **Rapportegenskaper** kort innehåller information om rapportegenskaper som rapportdatum, varaktighet, filter, överföringsdatum och information om Adobe Experience Manager (AEM).

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Rapportöversikt {#report-overview}

Detta **Rapportöversikt** kortet innehåller rapportresultat och allvarlighetsgrader som gäller vid bedömning av om det är klart att gå över till AEM as a Cloud Service, vilket visas i figuren nedan.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Om du klickar på den här rapporten öppnas **Rapport** -fliken.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Du kan filtrera rapporten baserat på prioritet, undertyp eller antal.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Se [Tolka rapporten Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html) för att lära sig mer om forskningskategorier och prioritetsnivåer.

#### Utvärdering av bästa praxis {#best-practices-assessment}

Alternativet Best Practices Assessment (Utvärdering av bästa praxis) ger en bedömning av din aktuella AEM och ger vägledning om nästa steg för att anta AEM bästa praxis. Du kan granska följande information på den här fliken:

* AEM - översikt
* Anpassade komponenter och mallar
* Ytterligare resultat
* Långsamma frågor
* Underhållsaktiviteter

#### Utvärdering av migreringskomplexitet {#migration-complexity-assessment}

Med alternativet Utvärdering av migreringskomplexitet kan du bedöma hur komplicerat det är att migrera den befintliga AEM till AEM as a Cloud Service.

Du kan granska följande information på den här fliken:

* AEM - översikt
* Utvärdering
* Överväganden vid innehållsmigrering

  ![bild](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Använda Planera och konfigurera kort {#planning-setup}

1. Klicka **Visa** från **Planering och installation** kort. Det här kortet innehåller allt relevant innehåll som hjälper dig att planera och konfigurera AEM migrering.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. En innehållskarusell visar all relevant information för den här fasen av migreringsresan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Ta bort en analysrapport om bästa praxis från trendlinjevyn {#delete-trendline}

>[!IMPORTANT]
>En rapport kan bara tas bort när mer än en rapport har överförts till ett projekt.

1. Navigera till projektet och klicka **Granska** från **Best Practices Analysis** i **Beredskap** fas.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Klicka **...**.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Klicka på i listrutan **Visa trendlinje**, vilket visas i figuren nedan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Klicka på ikonen Ta bort på **Trendlinjerapport** skärm.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Klicka **Ta bort** för att bekräfta borttagningen.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in i Cloud Acceleration Manager och hur du skapar ett projekt är du nu redo att gå vidare till nästa steg i [Implementeringsfas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html).
