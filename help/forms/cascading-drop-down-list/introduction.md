---
title: Listruta för överlappande lista
description: Använd adaptiva Forms-uttryck för att lägga till automatisk validering, beräkning och aktivera eller inaktivera synlighet för ett avsnitt.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Använd fallbeskrivning

När du skapar formulär eller program är det ofta användbart att vägleda användarna genom platsval på ett strukturerat sätt. En listruta med överlappande alternativ gör detta enkelt och användarvänligt - användaren väljer först ett land, vilket filtrerar listan med tillgängliga delstater/provinser och sedan ett slutligt val av städer baserat på delstat. Den här metoden gör inte bara formulären renare utan förhindrar också ogiltiga kombinationer (som att välja en stad som inte finns i ett valt läge).

Följande steg krävs för att slutföra det här användningsfallet

- Skapa API-integrering
- Skapa formulär med fält för att fånga land/stat/stad
- Skapa regel för att fylla i listrutorna med API-integrering