---
category: general
date: 2026-03-07
description: Leer hoe je OCR in C# kunt gebruiken om tekst uit afbeeldingsbestanden
  te extraheren. Deze gids toont offline OCR, het converteren van een afbeelding naar
  tekst en het laden van een afbeelding voor OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: nl
og_description: Hoe OCR in C# te gebruiken om offline tekst uit afbeeldingen te extraheren.
  Stapsgewijze code, tips en volledige uitleg voor het omzetten van een afbeelding
  naar tekst.
og_title: Hoe OCR in C# te gebruiken – Complete offline gids
tags:
- OCR
- C#
- Aspose
title: Hoe OCR in C# te gebruiken – Tekst uit afbeeldingen offline extraheren
url: /nl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in C# – Tekst uit afbeeldingen offline extraheren

Heb je je ooit afgevraagd **hoe je OCR** kunt gebruiken in een .NET‑project zonder gegevens naar de cloud te sturen? Je bent niet de enige. Veel ontwikkelaars moeten *tekst uit afbeelding*‑bestanden halen op een beveiligde werkstation, en ze vrezen dat netwerkverkeer gevoelige informatie kan blootstellen.  

Het goede nieuws? Met Aspose.OCR kun je tekst herkennen uit PNG‑, JPEG‑ of PDF‑bestanden volledig offline. In deze tutorial lopen we door het laden van een afbeelding voor OCR, het configureren van de engine voor offline‑modus, en uiteindelijk **afbeelding naar tekst converteren** met slechts een paar regels C#.

By the end of this guide you’ll be able to:

* Installeer het Aspose.OCR NuGet‑pakket.  
* Stel de OCR‑engine in voor offline verwerking.  
* Laad een afbeelding voor OCR en haal de tekstuele inhoud eruit.  

Geen externe services, geen API‑sleutels—gewoon pure C#‑code die draait op elke Windows‑ of Linux‑machine.

---

## Vereisten

Before we dive in, make sure you have:

* .NET 6.0 SDK of later (de code werkt ook met .NET Framework 4.7+).  
* Visual Studio 2022, VS Code, of een willekeurige editor die C# ondersteunt.  
* Een kopie van de **Aspose.OCR**‑bibliotheek – je kunt deze ophalen via NuGet (`Aspose.OCR`).  
* Een OCR‑resources map (`Resources`) die bij de bibliotheek wordt geleverd (bevat taal‑databestanden).  
* Een voorbeeldafbeelding (bijv. `offline_test.png`) geplaatst in een bekende map.

> **Pro tip:** Houd de resources‑map naast je uitvoerbare bestand; dit vereenvoudigt de `ResourcesPath`‑configuratie.

## Stap 1: Installeer het Aspose.OCR NuGet‑pakket

Eerst voeg je de bibliotheek toe aan je project. Open een terminal in de projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Of, als je de Visual Studio‑UI verkiest, klik met de rechtermuisknop op **Dependencies → Manage NuGet Packages**, zoek naar *Aspose.OCR*, en klik op **Install**.

> Het installeren van het pakket haalt alle benodigde binaries op, zodat je geen extra DLL‑s nodig hebt.

## Stap 2: Maak en configureer de OCR‑engine (Hoe OCR te gebruiken – Offline‑modus)

Nu gaan we de OCR‑engine instantiëren en aangeven dat deze **offline** moet werken. Dit zorgt ervoor dat er geen netwerkverkeer plaatsvindt tijdens de herkenning.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**Waarom offline?**  
Wanneer `EngineMode` is ingesteld op `Online`, neemt de engine contact op met de cloud van Aspose om taal‑pakketten on‑the‑fly te downloaden. In gereguleerde omgevingen (financiën, gezondheidszorg) is dat verkeer vaak verboden. Door offline‑modus af te dwingen, garandeer je dat alles op de lokale machine blijft.

## Stap 3: Verwijs de engine naar de OCR‑resources map

De OCR‑engine heeft taaldata (getrainde modellen) nodig om tekens te herkennen. Geef aan waar die bestanden zich bevinden:

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

Als je niet zeker weet waar de map zich bevindt, zoek dan onder de NuGet‑pakketmap (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). Kopieer de volledige map naar je project voor eenvoudigere implementatie.

## Stap 4: Laad de afbeelding voor OCR (Afbeelding laden voor OCR)

Je kunt de engine elke ondersteunde bitmap geven. Hier laden we een PNG van de schijf:

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**Tip:** Als je afbeeldingen uit een stream moet verwerken (bijv. geüpload via een API), gebruik dan `ImageStream.FromStream(yourStream)`.

## Stap 5: Voer het herkenningsproces uit en converteer afbeelding naar tekst

Met alles klaar, start je de OCR. De `Recognize()`‑methode doet het zware werk, en de geëxtraheerde tekst is beschikbaar via de `Text`‑eigenschap.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

## Stap 6: Geef de geëxtraheerde tekst weer

Tot slot, toon het resultaat. In een console‑app kun je eenvoudig naar de console schrijven, maar in een web‑API zou je de string als JSON retourneren.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Het uitvoeren van het programma moet de tekstinhoud van `offline_test.png` afdrukken. Bijvoorbeeld, als de afbeelding de zin *“Hello, World!”* bevat, zie je:

```
=== OCR Result ===
Hello, World!
```

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma. Kopieer‑en‑plak het in een nieuw console‑project (`dotnet new console`) en pas de paden aan zodat ze bij jouw omgeving passen.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Verwachte output:** De console drukt de exacte tekst af die in het PNG‑bestand staat. Als de afbeelding onscherp is, kan het resultaat foutherkende tekens bevatten—zie de probleemoplossingssectie hieronder.

## Veelvoorkomende valkuilen & tips (Tekst uit PNG efficiënt herkennen)

| Probleem | Waarom het gebeurt | Hoe op te lossen |
|----------|--------------------|------------------|
| **Lege output** | ResourcesPath wijst naar de verkeerde map of er ontbreken taalbestanden. | Controleer of de map `eng.traineddata` bevat (of andere taalbestanden) en controleer de pad‑string nogmaals. |
| **Onzin‑tekens** | Beeldresolutie is te laag of de afbeelding is niet gebinariseerd. | Pre‑process de afbeelding (verhoog DPI, pas `ImageProcessor` toe om te verscherpen). |
| **Prestatie‑vertraging** | Grote afbeeldingen worden verwerkt op volledige resolutie. | Verklein de afbeelding tot maximaal 2000 px breedte voordat je deze aan OCR geeft. |
| **Niet‑ondersteund formaat** | Een BMP gebruiken met een ongewoon pixel‑formaat. | Converteer de afbeelding eerst naar PNG of JPEG (`System.Drawing.Image.Save`). |

**Pro tip:** Als je meerdere talen moet herkennen, stel `ocrEngine.Settings.Language = Language.English | Language.French;` in vóór het aanroepen van `Recognize()`.

## Veelgestelde vragen

**Q: Kan ik deze code op Linux gebruiken?**  
Zeker. Aspose.OCR is cross‑platform; zorg er alleen voor dat de native libraries aanwezig zijn (ze worden meegeleverd met het NuGet‑pakket).

**Q: Wat als ik geen Resources‑map heb?**  
Je kunt de gratis taal‑pakketten downloaden van de website van Aspose of ze uit het NuGet‑pakket halen (`.../aspose.ocr/<version>/resources`).

**Q: Is er een manier om vertrouwensscores te krijgen?**  
Ja. Na `Recognize()` kun je `ocrEngine.RecognizedWords` inspecteren – elk woord bevat een `Confidence`‑eigenschap.

## Conclusie

We hebben behandeld **hoe je OCR** in C# kunt gebruiken om *tekst uit afbeelding*‑bestanden volledig offline te extraheren. Door Aspose.OCR te installeren, `EngineMode.Offline` te configureren, naar de resources te wijzen, een afbeelding te laden en `Recognize()` aan te roepen, kun je betrouwbaar **afbeelding naar tekst converteren** zonder ooit het internet aan te raken.

Neem de bovenstaande code, vervang de paden naar je eigen afbeeldingen, en begin met het bouwen van functies zoals doorzoekbare PDF‑s, automatisering van gegevensinvoer, of toegankelijkheidstools. Vervolgens kun je **tekst uit PNG** in bulk verkennen, of de engine integreren in een ASP.NET Core‑API om OCR‑resultaten aan front‑end applicaties te leveren.

Veel plezier met coderen, en voel je vrij om te experimenteren—OCR is verrassend vergevingsgezind zodra de engine correct is ingesteld!

--- 

![Diagram die offline OCR‑workflow toont – hoe OCR te gebruiken in een beveiligde omgeving](https://example.com/ocr-workflow.png "hoe OCR te gebruiken diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}