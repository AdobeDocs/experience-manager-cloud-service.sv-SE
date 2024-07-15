---
title: Arbeta med uppgifter
description: Uppgifter representerar arbetsuppgifter som ska utföras på innehåll och används i projekt för att fastställa slutförandenivån för aktuella uppgifter
exl-id: 66f95a1f-34d0-4e2e-aa8c-addc2029a1d9
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 8%

---

# Arbeta med uppgifter {#working-with-tasks}

Uppgifter representerar arbetsuppgifter som ska utföras på innehåll. När du tilldelas en uppgift visas den i Inkorgen för arbetsflöde. Uppgiftsobjekt har värdet för uppgiften i kolumnen Typ.

Uppgifter används också i projekt för att avgöra hur fullständiga de aktuella uppgifterna är, inklusive arbetsflödesuppgifter.

## Spåra projektförlopp {#tracking-project-progress}

Du kan spåra projektförloppet genom att titta på de aktiva/slutförda aktiviteterna i ett projekt som representeras av **aktivitetspanelen**. Projektets förlopp kan avgöras av:

* **Uppgiftsruta:** Ett övergripande förlopp för projektet visas i uppgiftsrutan på sidan med projektinformation.

* **Uppgiftsruta:** När du klickar på uppgiftsrutan visas en lista med uppgifter. Den här listan innehåller detaljerad information om alla uppgifter som rör projektet.

Båda listar arbetsflödesuppgifter och uppgifter som du skapar direkt i **aktivitetspanelen**.

### Åtgärdsfönster {#task-tile}

Om ett projekt innehåller några relaterade uppgifter visas en åtgärdsruta i projektet. Åtgärdsrutan visar projektets aktuella status. Detta baseras på befintliga uppgifter i arbetsflödet och inkluderar inga uppgifter som kommer att genereras i framtiden allt eftersom arbetsflödet fortsätter. Följande information visas i åtgärdsrutan:

* Procent slutförda uppgifter
* Procent av aktiva uppgifter
* Procent av försenade uppgifter

![Åtgärdspanel](/help/sites-cloud/authoring/assets/projects-tasks-breakdown.png)

### Visa eller ändra uppgifter i ett projekt {#viewing-or-modifying-the-tasks-in-a-project}

Förutom att följa upp förloppet kanske du också vill visa mer information om projektet eller ändra det.

#### Uppgiftslista {#task-list}

Klicka på ellipsen (..) i aktivitetspanelen för att visa en lista med uppgifter som hör till projektet. Uppgifterna delas upp i överordnade arbetsflöden. Uppgiftsinformationen visas tillsammans med metadata som förfallodatum, tilldelad, prioritet och status.

![Uppgiftslista](/help/sites-cloud/authoring/assets/projects-task-list.png)

#### Uppgiftsinformation {#task-details}

Om du vill ha mer information om en viss uppgift väljer du uppgiften i uppgiftslistan och **Öppna**.

![Uppgiftsinformation](/help/sites-cloud/authoring/assets/projects-task-details.png)

### Visa och ändra aktivitetskommentarer {#viewing-and-modifying-task-comments}

I Uppgiftsinformation kan du redigera eller lägga till kommentarer. Alla kommentarer i ett projekt visas dessutom i kommentarsområdet.

![Kommentarer om aktiviteter](/help/sites-cloud/authoring/assets/projects-tasks-comments.png)

### Lägga till uppgifter {#adding-tasks}

Du kan lägga till nya uppgifter i projekt. Dessa uppgifter visas sedan på aktivitetspanelen och är tillgängliga i inkorgen Meddelanden för att utföra åtgärder.

Så här lägger du till en uppgift:

1. I projektet väljer du +-ikonen i rutan **Åtgärder** . Fönstret **Lägg till uppgift** öppnas.
1. Ange information om uppgiften. Titeln på uppgiften och vilken grupp den har tilldelats är obligatoriska. Ytterligare information som innehållssökväg, beskrivning, uppgiftsprioritet och förfallodatum är valfria. Du kan dessutom välja fliken **Avancerat** för att ange namnet på uppgiften, som används för att namnge URL:en.

   ![Lägg till en aktivitet](/help/sites-cloud/authoring/assets/projects-add-task.png)

1. Välj **Skapa**.

## Arbeta med uppgifter i Inkorgen {#working-with-tasks-in-the-inbox}

Ett annat sätt att komma åt uppgifter är via Inkorgen. I inkorgen kan du öppna innehållet för att implementera ändringarna. När du är klar anger du aktivitetsstatus till Slutförd. Uppgifter visas också i inkorgen när de tilldelas till en användargrupp som du tillhör. I det här fallet kan alla medlemmar i gruppen utföra arbetet och slutföra uppgiften.

![Uppgifter i inkorgen](/help/sites-cloud/authoring/assets/projects-task-inbox.png)

Om du vill slutföra en uppgift markerar du uppgiften och klickar på **Slutför**. Lägg till information för aktiviteten och klicka sedan på **Klar**. Mer information finns i [Inkorgen](/help/sites-cloud/authoring/inbox.md).

![Aktivitetsmeddelanden](/help/sites-cloud/authoring/assets/projects-task-notifications.png)
