---
title: Hur lägger jag till platshållartext i formulärfält?
description: Platshållartext är avsedd att hjälpa användaren med datainmatning när kontrollen saknar värde. Det kan vara ett exempelvärde eller en kort beskrivning av det förväntade formatet.
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Platshållartext i [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

Platshållartexten representerar ett ord eller en kort fras. Avsikten är att hjälpa användaren att ange data när kontrollen inte har något värde. En platshållartext kan vara ett exempelvärde eller en kort beskrivning av det förväntade formatet. Platshållartexten visas innan användaren anger ett värde, den tas bort när användaren anger eller väljer ett värde.

>[!NOTE]
>
>Om platshållartexten har angetts måste den ha ett värde som inte innehåller några nya radtecken.

![Datumkomponent med och utan platshållartext](assets/dat-picker-place-holder-text.png)

**A.** Date-komponent med platshållartext **B.** Date-komponent utan platshållartext

[!DNL AEM Forms] har stöd för platshållartext för lösenordsrutor, datumväljare, numeriska rutor och textrutefält.\
Platshållartexter stöds inte för den inbyggda HTML5-datumwidgeten. Så här anger du en platshållartext:

1. Högerklicka på en komponent som stöder platshållartext och klicka på **Redigera**. Dialogrutan Redigera komponent visas.

1. Öppna fliken **Titel och text**.
1. Ange ett ord eller en kort fras i textrutan **Platshållare**. Klicka på **OK**.

>[!NOTE]
>
>Platshållartext stöds inte i [!DNL Microsoft Internet Explorer 9].

