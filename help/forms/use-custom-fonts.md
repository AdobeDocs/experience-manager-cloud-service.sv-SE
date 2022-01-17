---
title: 'Använda anpassade teckensnitt '
description: 'Använda anpassade teckensnitt '
source-git-commit: 10fe582edc8ffc93ea3f8564a64259882bba1d6f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Använda anpassade teckensnitt

**Cloud Service Communications-dokumentationen finns i betaversionen**

Du kan använda Forms as a Cloud Service Communications för att kombinera en XDP-mall, ett XDP-baserat PDF-dokument eller ett Acrobat-formulär (AcroForm) med XML-data för att generera PDF-dokument. Du kan använda teckensnitt som ingår i Cloud Service eller anpassade teckensnitt (typsnitt som godkänts av organisationen) för att återge de genererade PDF-dokumenten. Du kan använda utvecklingsprojektet för Cloud Service för att lägga till anpassade teckensnitt i din Cloud Service.

## PDF-dokument

Du kan [bädda in ett teckensnitt](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) till ett PDF-dokument. När ett teckensnitt är inbäddat visas PDF-dokumentet (Looks) identiskt på alla plattformar. Det har använt inbäddade teckensnitt för att få ett konsekvent utseende och känsla. När ett teckensnitt inte är inbäddat beror teckensnittsåtergivningen på återgivningsinställningarna för PDF-visningsprogrammet. Om teckensnittet är tillgängligt på klientdatorn använder PDF det angivna teckensnittet, annars återges PDF med ett reservteckensnitt.

## Lägga till anpassade teckensnitt i din as a Cloud Service Forms-miljö

Så här lägger du till anpassade teckensnitt i Cloud Servicen:

1. Konfigurera och öppna det lokala utvecklingsprojektet. Du kan använda vilken IDE som helst.
1. I mappstrukturen på den översta nivån i projektet skapar du en mapp där du kan spara anpassade teckensnitt och lägga till anpassade teckensnitt i mappen. Till exempel typsnitt/src/main/resources
   ![Mappen Teckensnitt](assets/fonts.png)

1. Öppna filen pom.xml på den översta nivån i utvecklingsprojektet.
1. Lägg till `<Font-Archive-Version>` manifest entry to the .pom file and set value of version to 1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   </addDefaultEntries>
                   </addDefaultImplementationEntries>
               </manifest>
               <manifestEntries>
                   <Font-Archive-Version>1</Font-Archive-Version>
                   <Font-Archive-Contents>/</Font-Archive-Contents>
               </manifestEntries> 
           </archive>
       </configuration>
   </plugin>
   ```

1. Lägg till teckensnittsmappen i `<modules>` som visas i pom-filen. Till exempel:

   ```xml
   <modules>
       <module>all</module>
       <module>core</module>
       <module>ui.frontend</module>
       <module>ui.apps</module>
       <module>ui.apps.structure</module>
       <module>ui.config</module>
       <module>ui.content</module>
       <module>it.tests</module>
       <module>dispatcher</module>
       <module>dispatcher.ams</module>
       <module>dispatcher.cloud</module>
       <module>ui.tests</module>
       <module>fonts</module>
   </modules>
   ```

1. Checka in den uppdaterade koden och [köra pipeline](/help/implementing/cloud-manager/deploy-code.md) för att distribuera teckensnitten i Cloud Servicen.
