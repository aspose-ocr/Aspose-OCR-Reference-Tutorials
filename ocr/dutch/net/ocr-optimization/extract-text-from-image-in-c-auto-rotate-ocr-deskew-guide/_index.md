---
category: general
date: 2026-03-29
description: Tekst extraheren uit een afbeelding met Aspose OCR in C#. Leer automatische
  rotatie‑OCR en hoe je een gescande afbeelding kunt rechtzetten voor perfecte resultaten.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: nl
og_description: Tekst extraheren uit afbeelding met Aspose OCR. Deze gids toont auto‑rotatie‑OCR
  en hoe je een gescande afbeelding kunt rechtzetten in C#.
og_title: Tekst uit afbeelding extraheren in C# – Automatisch roteren OCR en kantcorrectie
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Tekst uit afbeelding extraheren in C# – Automatisch roteren OCR‑ en Deskew‑gids
url: /nl/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding in C# – Auto‑Rotate OCR & Deskew gids

Heb je ooit **tekst uit afbeelding extraheren** nodig gehad, maar kwam het bestand in een vreemde hoek binnen? Het is een veelvoorkomende hoofdpijn—vooral wanneer je te maken hebt met gescande facturen, gefotografeerde bonnetjes of scheve PDF's. Het goede nieuws is dat je zelf geen aangepaste rotatie‑algoritme hoeft te schrijven. Door gebruik te maken van de ingebouwde *auto rotate OCR* functie van Aspose OCR kun je de engine de afbeelding laten rechtzetten en vervolgens **tekst uit afbeelding extraheren** in één soepele stap.  

In deze tutorial lopen we een compleet, kant‑klaar C#‑programma door dat:

* De OCR‑engine initialiseert met automatische oriëntatie en deskewing,
* Een geroteerde of scheve afbeelding herkent,
* Zowel de gedetecteerde rotatiehoek als de geëxtraheerde tekst retourneert.

Geen externe services, geen ingewikkelde wiskunde—slechts een paar regels code en een duidelijke uitleg van *how to deskew scanned image* wanneer nodig.

## Wat je nodig hebt

| Voorwaarde | Waarom het belangrijk is |
|------------|--------------------------|
| .NET 6.0 or later (or .NET Framework 4.6+) | Aspose OCR wordt geleverd als een NuGet‑pakket dat zich richt op deze runtimes. |
| Visual Studio 2022 (or any C# editor) | Maakt het eenvoudig om NuGet‑pakketten toe te voegen en de console‑app uit te voeren. |
| A sample image (`rotated_document.jpg`) | Het bestand moet een JPEG, PNG, BMP of TIFF zijn die niet perfect rechtop staat. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | Biedt de `OcrEngine`, `PreprocessingFilters` en gerelateerde types. |

Als je die punten hebt afgevinkt, ben je klaar om te gaan. Anders haal je de nieuwste Aspose OCR van NuGet—het is een installatie met één klik.

---

## Stap 1 – Initialise de OCR Engine (Primary Keyword in Action)

Het eerste wat we doen is een `OcrEngine`‑instantie maken en deze vertellen om **auto rotate OCR** en **deskew** toe te passen op elke binnenkomende afbeelding. Die twee vlaggen worden gecombineerd met een bitwise OR (`|`) omdat `PreprocessingFilters` een enum is met het `[Flags]`‑attribuut.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Waarom dit belangrijk is:**  
> *Auto‑rotate OCR* inspecteert de tekstbasislijn van de afbeelding, raadt de juiste oriëntatie en roteert deze intern vóór herkenning. *Auto‑deskew* doet hetzelfde voor lichte hellingen die vaak voorkomen in gescande documenten. Door beide in te schakelen, garandeer je de best mogelijke **extract text from image** resultaten zonder handmatige beeldbewerking.

---

## Stap 2 – Herken de afbeelding en haal het resultaat op

Nu geven we de engine een bestandspad. De `RecognizeImage`‑methode retourneert een `OcrResult`‑object dat de gedetecteerde rotatiehoek, vertrouwensscores en de platte‑tekst uitvoer bevat.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** Als je werkt met een stream (bijv. een geüpload bestand), gebruik dan `ocrEngine.RecognizeImage(Stream)` in plaats daarvan. Dezelfde preprocessing‑vlaggen gelden, dus je krijgt nog steeds de voordelen van **auto rotate OCR**.

---

## Stap 3 – Toon de rotatiehoek en de geëxtraheerde tekst

Tot slot printen we twee stukken informatie naar de console: de hoek die de engine denkt dat de afbeelding moest worden gedraaid, en de daadwerkelijke tekst die eruit is gehaald.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Verwachte output** (jouw cijfers zullen verschillen afhankelijk van de invoerafbeelding):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Als de afbeelding al rechtop stond, zal de rotatiehoek `0°` zijn, en krijg je nog steeds schone tekst dankzij het *auto‑deskew* algoritme.

---

## Stap 4 – Begrijpen hoe je gescande afbeelding deskewt (Secondary Keyword Deep‑Dive)

Je vraagt je misschien af *how to deskew scanned image* wanneer de OCR‑engine een niet‑nul rotatie rapporteert. Onder de motorkap past Aspose OCR een **Hough‑transformatie** toe om de dominante tekstlijnoriëntatie te detecteren. Vervolgens roteert het de bitmap met de inverse van die hoek, waardoor de tekst effectief wordt rechtgezet.

**Wanneer is dit van belang?**  
* Scanners die papier onder een lichte hoek invoeren (veelvoorkomend in kantooromgevingen).  
* Smartphone‑foto's die met de hand worden genomen—de horizon is zelden perfect.  

**Afhandeling van randgevallen:**  
Als de `RotationAngle` van het resultaat ongewoon groot is (bijv. > 45°), kan de engine de afbeelding verkeerd hebben geïnterpreteerd (misschien is het een logo of een niet‑tekstgrafiek). In dat geval kun je:

1. De afbeelding handmatig roteren met `System.Drawing` voordat je deze aan de engine geeft, of  
2. `AutoRotate` uitschakelen en alleen `AutoDeskew` behouden als je weet dat het document al rechtop staat.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Stap 5 – Veelvoorkomende valkuilen & Pro‑tips (E‑E‑A‑T in Action)

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|--------------------|-----------|
| **Vage of lage‑resolutie afbeeldingen** | OCR‑nauwkeurigheid daalt drastisch; rotatiedetectie kan falen. | Gebruik scans van minimaal 300 dpi; pas een verscherpingsfilter toe vóór OCR. |
| **Gemengde talen** | De engine standaard naar Engels; vreemde tekens worden onleesbaar. | Stel `Language = Language.English | Language.Spanish` in (of de juiste combinatie). |
| **Grote bestanden (> 10 MB)** | Geheugendruk kan een `OutOfMemoryException` veroorzaken. | Schaald de afbeelding eerst verkleinen, of verwerk in tegels met `OcrEngine.RecognizeRegion`. |
| **Onjuist bestandspad** | `FileNotFoundException` stopt het programma. | Gebruik `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` voor robuustheid. |

> **Pro tip:** Log altijd `ocrResult.RotationAngle` en `ocrResult.Confidence` (indien beschikbaar). Deze metrics helpen je beslissen of een herpoging met andere preprocessing‑instellingen de moeite waard is.

---

## Stap 6 – Voorbeeld uitbreiden (Wat is het vervolg?)

Nu je **tekst uit afbeelding kunt extraheren** met auto‑rotatie en deskewing, overweeg deze volgende stappen:

* **Batch processing** – Loop over een map met afbeeldingen, sla elk resultaat op in een database, en markeer alle met `RotationAngle > 5°` voor handmatige controle.  
* **PDF-conversie** – Combineer de geëxtraheerde tekst met de originele afbeelding tot een doorzoekbare PDF met behulp van Aspose.PDF.  
* **Taaldetectie** – Gebruik Aspose.OCR’s `AutoDetectLanguage`‑vlag om de engine automatisch de beste taal te laten kiezen.  

Elk van deze bouwt voort op hetzelfde kernprincipe: laat de bibliotheek de oriëntatie afhandelen, en jij richt je op de bedrijfslogica.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Sla het bestand op als `Program.cs`, voer `dotnet add package Aspose.OCR` uit, en daarna `dotnet run`. Je zou de hoek en de schone tekst in de console moeten zien.

---

## Conclusie

We hebben zojuist laten zien hoe je **tekst uit afbeelding** kunt extraheren in C# terwijl je Aspose OCR de zorg laat nemen voor *auto rotate OCR* en het lastige *how to deskew scanned image* probleem. Door de twee preprocessing‑vlaggen in te schakelen, rechtzet de engine automatisch scheve afbeeldingen, detecteert de juiste oriëntatie, en levert nauwkeurige tekst—geen handmatige beeldbewerking nodig.

Voel je vrij om te experimenteren met grotere batches, verschillende talen, of zelfs de output te integreren in een doorzoekbare PDF. De mogelijkheden zijn eindeloos zodra de OCR‑engine het zware werk voor je doet.

**Klaar om je document‑pipeline naar een hoger niveau te tillen?** Pak de code, richt deze op je eigen scans, en zie de rotatiehoeken verdwijnen. Als je ergens tegenaan loopt, laat dan een reactie achter—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}