---
category: general
date: 2026-03-07
description: Leer hoe je tekst uit een PNG kunt lezen en Cyrillische tekst kunt extraheren
  met Aspose OCR, een afbeelding naar tekst kunt converteren en het Cyrillische taalpakket
  kunt downloaden.
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: nl
og_description: Leer hoe je tekst uit png kunt lezen, Cyrillische tekst kunt extraheren
  en een afbeelding naar tekst kunt converteren met Aspose OCR in C#.
og_title: tekst lezen uit png – Cyrillische tekst extraheren met Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: tekst lezen uit PNG – Cyrillische tekst extraheren met Aspose OCR
url: /nl/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst lezen uit png – Cyrillische tekst extraheren met Aspose OCR

Moet je **tekst lezen uit png** bestanden en Cyrillische tekens extraheren? In deze gids laten we je zien hoe je tekst uit png kunt lezen met Aspose OCR, Cyrillische tekst kunt extraheren, en **afbeelding naar tekst** kunt omzetten in slechts een paar regels C#.  

Als je ooit naar een screenshot van een Russische factuur hebt gekeken en je afvroeg hoe je de woorden in een doorzoekbare string kunt krijgen, dan ben je op de juiste plek. We zullen ook behandelen hoe je automatisch **download the Cyrillic language pack** kunt uitvoeren, zodat je niet naar extra bestanden hoeft te zoeken.

## Wat je zult bereiken

* **Load an image for OCR** direct vanaf schijf of een stream.  
* Stel de engine in op **Cyrillic language** zonder handmatige downloads.  
* Voer herkenning uit en **extract Cyrillic text** uit een PNG‑bestand.  
* Bekijk de herkende tekst die naar de console wordt afgedrukt – een schoon, platte‑tekst resultaat dat je kunt invoeren in databases, zoekindexen, of elke andere workflow.

Geen externe services, geen cloud‑sleutels, alleen het Aspose OCR NuGet‑pakket en een paar regels C#.

## Vereisten

* .NET 6.0 of later (de code werkt op .NET Core, .NET Framework, en .NET 5+).  
* Visual Studio 2022 of elke editor die je wilt.  
* Het Aspose.OCR NuGet‑pakket (`dotnet add package Aspose.OCR`).  
* Een PNG‑afbeelding die Cyrillische tekens bevat – bijvoorbeeld `cyrillic_sample.png` geplaatst in een map genaamd `YOUR_DIRECTORY`.

> **Pro tip:** Als je Visual Studio gebruikt, klik met de rechtermuisknop op het project → **Manage NuGet Packages** → zoek “Aspose.OCR” en installeer de nieuwste stabiele versie.

---

## Stap 1 – Installeer Aspose OCR en maak de engine

Eerst hebben we de OCR‑engine‑instantie nodig. De `OcrEngine`‑klasse is het toegangspunt voor alle bewerkingen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **Waarom dit belangrijk is:** De engine omvat taalpakketten, afbeeldingsdata en herkenningsopties. Eenmalig instantieren en hergebruiken over meerdere afbeeldingen kan de prestaties verbeteren.

---

## Stap 2 – **load image for ocr** en stel de taal in

Nu vertellen we de engine welke afbeelding verwerkt moet worden en welke taal gezocht moet worden. Het instellen van `Language.Cyrillic` downloadt automatisch het benodigde taalpakket de eerste keer dat het wordt uitgevoerd.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **Randgeval:** Als je PNG enorm is (meer dan 5 MB) wil je deze misschien eerst verkleinen om de herkenning te versnellen. De `Image`‑eigenschap accepteert ook een `Stream`, zodat je kunt laden vanuit geheugen, een web‑verzoek, of een Azure Blob zonder het bestandssysteem aan te raken.

---

## Stap 3 – **convert image to text** met één aanroep

Herkenning is zo simpel als het aanroepen van `Recognize()`. Na deze aanroep bevat de `Text`‑eigenschap de geëxtraheerde string.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **Wat er onder de motorkap gebeurt:** Aspose draait een op neurale netwerken gebaseerde classifier getraind op miljoenen Cyrillische glyphs. De bibliotheek abstraheert al die complexiteit, zodat je gewoon schone Unicode krijgt.

---

## Stap 4 – Output het resultaat (of stuur het elders naartoe)

Voor demonstratiedoeleinden zullen we de tekst naar de console afdrukken, maar je kunt het gemakkelijk naar een bestand, een database, of een zoekindex sturen.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**Verwachte output** (ervan uitgaande dat `cyrillic_sample.png` de zin “Привет мир” bevat):

```
=== Recognized Cyrillic Text ===
Привет мир
```

Als de output er rommelig uitziet, controleer dan of de afbeelding duidelijk is en dat je `Language.Cyrillic` hebt ingesteld. De engine gebruikt standaard Engels, waardoor Cyrillische tekens als onbekende symbolen worden behandeld.

---

## Stap 5 – Volledig, uitvoerbaar voorbeeld

Alles bij elkaar, hier is een zelfstandige programma dat je kunt kopiëren‑plakken in een nieuw console‑project.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Sla het bestand op als `Program.cs`, voer `dotnet run` uit, en je zou de Cyrillische tekst moeten zien afgedrukt.

---

## Veelgestelde vragen & probleemoplossing

| Vraag | Antwoord |
|----------|--------|
| **Wat als het taalpakket niet downloadt?** | Zorg ervoor dat de machine internettoegang heeft. Het pakket wordt gecached in `%USERPROFILE%\.Aspose\OCR\Languages`. Het verwijderen van die map dwingt een nieuwe download af. |
| **Kan ik andere talen lezen naast Cyrillisch?** | Zeker – vervang `Language.Cyrillic` door `Language.English`, `Language.Arabic`, enz. Dezelfde auto‑downloadlogica geldt. |
| **Mijn PNG is ruisachtig – resultaten zijn slecht. Wat kan ik doen?** | Pre‑process de afbeelding: verhoog het contrast, converteer naar grijstinten, of pas een median filter toe. Aspose OCR biedt ook `Settings.ImagePreprocess` opties. |
| **Is er een manier om begrenzingskaders voor elk woord te krijgen?** | Ja, na `Recognize()` kun je `ocrEngine.Regions` inspecteren, die rechthoeken teruggeeft voor elk gedetecteerd woord. |
| **Heb ik een licentie nodig voor productiegebruik?** | De gratis evaluatie werkt tot 100 pagina's. Voor commerciële projecten koop een licentie – deze verwijdert het evaluatiewatermerk en ontgrendelt high‑speed batchverwerking. |

---

## Volgende stappen – de oplossing uitbreiden

* **Batch processing:** Loop over een map met PNG's, verzamel alle teksten in een CSV‑bestand.  
* **Integratie met Azure Cognitive Search:** Indexeer de geëxtraheerde Cyrillische strings voor snelle opzoeking.  
* **Combineer met PDF-conversie:** Gebruik Aspose.PDF om gescande PDF's eerst naar PNG's te converteren, en voer daarna dezelfde OCR‑stroom uit.  

Al deze scenario's hergebruiken het kernpatroon dat we net hebben behandeld: **load image for OCR → set language → recognize → use the text**.

---

## Conclusie

Je weet nu hoe je **tekst uit png** kunt **lezen**, **Cyrillische tekst** kunt **extraheren**, en **afbeelding naar tekst** kunt **omzetten** met Aspose OCR in C#. De belangrijkste stappen zijn het creëren van de engine, het laden van de afbeelding, het selecteren van de juiste taal (die automatisch **download the Cyrillic language pack**), en tenslotte het aanroepen van `Recognize()`.

Probeer het met verschillende afbeeldingen, experimenteer met de `Settings`‑opties, en zie hoe je applicaties doorzoekbaar, meertalig en veel intelligenter worden.  

Veel plezier met coderen, en voel je vrij om een reactie achter te laten als je ergens tegenaan loopt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}