---
title: Källkodslagringsplats - Cloud Services
description: Källkodslagringsplats - Cloud Services
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Databas för källkod {#source-code-repository}

Cloud Manager-programmet kommer att etableras automatiskt med sin egen Git-databas.

För att en användare ska få åtkomst till molnhanterarens Git-databas måste användaren använda en Git-klient med ett kommandoradsverktyg, en fristående visuell Git-klient eller användarens IDE som Eclipse, IntelliJ, NetBeans.

När en Git-klient har konfigurerats kan du hantera din Git-databas via användargränssnittet i Cloud Manager. Mer information om hur du hanterar Git med hjälp av användargränssnittet i Cloud Manager finns i [Åtkomst till Git](/help/implementing/cloud-manager/accessing-git.md).

För att börja utveckla AEM Cloud-programmet måste en lokal kopia av programkoden göras genom att checka ut den från Cloud Manager-databasen till en plats på den lokala datorn där de vill skapa sin databas.

```java
$ git clone {URL}
```

>[!NOTE]
>
>En användare kan checka ut en kopia av sin kod och göra ändringar i den lokala koddatabasen. När det är klart kan användaren spara sina kodändringar i fjärrkoddatabasen i Cloud Manager.
