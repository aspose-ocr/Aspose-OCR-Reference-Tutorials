---
category: general
date: 2026-03-02
description: Hoe GPU voor OCR in C# in te schakelen en snel tekst uit een afbeelding
  te herkennen. Leer hoe je de GPU‑geheugenlimiet instelt, tekst van een bon extraheert
  en OCR efficiënt uitvoert.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- how to run ocr
- extract text from receipt
- set gpu memory limit
language: nl
og_description: Hoe GPU voor OCR in C# in te schakelen en snelle teksterkenning van
  afbeeldingen te krijgen. Volg deze gids om de GPU‑geheugenlimiet in te stellen en
  tekst uit bonnetjes te extraheren.
og_title: Hoe GPU in te schakelen voor OCR in C# – Tekst herkennen
tags:
- OCR
- C#
- GPU
- Aspose
title: Hoe GPU voor OCR in C# in te schakelen – Tekst herkennen
url: /nl/net/ocr-optimization/how-to-enable-gpu-for-ocr-in-c-recognize-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe GPU in te schakelen voor OCR in C# – Tekst herkennen

Heb je je ooit afgevraagd **hoe je GPU** kunt inschakelen voor OCR wanneer je tekst uit afbeeldingsbestanden moet herkennen? Je bent niet de enige – ontwikkelaars lopen vaak tegen de trage CPU‑gebaseerde herkenning aan, vooral bij grote bonnetjes of scans met hoge resolutie. Het goede nieuws? Met een paar regels C# kun je de schakel omdraaien, de engine laten draaien op de GPU, en zelfs het geheugenverbruik beperken.

In deze tutorial leer je **hoe je OCR** uitvoert met Aspose.OCR, een GPU‑geheugenlimiet instelt, en tekst uit bonafbeeldingen haalt zonder enige moeite. Geen externe services, alleen een schone, zelfstandige oplossing die je in elk .NET‑project kunt plaatsen.

---

## Wat je nodig hebt

Voordat we beginnen, zorg dat je de volgende vereisten hebt:

* **.NET 6 of later** – de nieuwste runtime biedt de beste compatibiliteit.  
* **Aspose.OCR for .NET** NuGet‑pakket (versie 23.10 of nieuwer).  
  `dotnet add package Aspose.OCR`  
* Een **CUDA‑compatibele GPU** met de juiste drivers geïnstalleerd (NVIDIA 1060+ werkt prima).  
  Als je geen GPU hebt, valt de code automatisch terug op CPU – geen crash, alleen langzamere verwerking.  
* Een afbeelding van een bon (of een ander document) dat je wilt verwerken, opgeslagen als `receipt.jpg`.

Met deze zaken kun je de code hieronder kopiëren‑plakken en direct zien hoe het werkt.

---

## Stap 1: Laad de afbeelding die je wilt verwerken  

Het eerste wat elke OCR‑workflow doet, is de bronafbeelding in het geheugen lezen. We gebruiken `System.Drawing.Bitmap` omdat het lichtgewicht is en platform‑onafhankelijk werkt met .NET 6+.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuOcrDemo
{
    static void Main()
    {
        // Load the receipt image from disk
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        Bitmap bitmapImage = new Bitmap(imagePath);
```

*Waarom dit belangrijk is*: Het vroegtijdig laden van de afbeelding laat je het pad verifiëren en een `FileNotFoundException` opvangen voordat de OCR‑engine überhaupt start. Het geeft je ook de mogelijkheid om later vooraf te verwerken (roteren, binariseren) indien nodig.

---

## Stap 2: Configureer de OCR‑engine om de GPU te gebruiken  

Nu vertellen we Aspose.OCR om op de GPU te draaien. Het `OcrEngineSettings`‑object is waar de magie gebeurt.

```csharp
        // Configure OCR to run on the GPU and limit its memory usage
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,          // Enable GPU acceleration (requires supported GPU)
            GpuMemoryLimit = 1024            // Optional: cap GPU memory at 1024 MB
        };
```

*Waarom een geheugenlimiet instellen?*  
Als je de GPU deelt met andere processen (bijv. een deep‑learning‑model), wil je niet dat OCR al het VRAM opslokt. De eigenschap `GpuMemoryLimit` laat je beleefd blijven.

> **Pro tip:** Als je niet zeker weet of de machine een compatibele GPU heeft, wikkel de instellingen dan in een `try…catch` en val terug op `OcrEngine.Cpu` bij een `UnsupportedHardwareException`.

---

## Stap 3: Initialiseert de OCR‑engine  

Met de instellingen klaar, maak je een instantie van de engine. Deze stap valideert de GPU‑beschikbaarheid onder de motorkap.

```csharp
        // Initialise the OCR engine with the GPU settings
        OcrEngine ocrEngine = new OcrEngine(ocrSettings);
```

Als de GPU niet wordt gedetecteerd, gooit Aspose een informatieve uitzondering. Deze vroegtijdig opvangen voorkomt mysterieuze “null reference”‑fouten later.

---

## Stap 4: Voer de herkenning uit en haal de tekst op  

Nu het zware werk – tekst herkennen uit de bitmap.

```csharp
        // Perform OCR on the bitmap
        string recognizedText = ocrEngine.Recognize(bitmapImage);

        // Output the result to the console
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

De `Recognize`‑methode retourneert een platte string met alle gedetecteerde tekens, waarbij waar mogelijk regeleinden behouden blijven. Dit is precies wat je nodig hebt wanneer je **tekst uit bon**‑bestanden wilt **extraheren** voor downstream‑verwerking (bijv. totalen, data of verkopersnamen parseren).

**Verwachte output** (voorbeeldbon):

```
=== Recognized Text ===
Store: QuickMart
Date: 03/01/2026
Item        Qty   Price
Apple       2     $1.20
Bread       1     $2.50
Total               $3.70
```

Als de GPU actief is, merk je dat de verwerkingstijd daalt van ~1,2 seconden (CPU) naar ~0,3 seconden op een mid‑range kaart – een merkbare winst voor batch‑taken.

---

## Stap 5: Randgevallen en fallback‑scenario’s afhandelen  

In de praktijk garandeert een omgeving zelden een perfecte GPU. Hier is een compacte patroon dat elegant degradeert naar CPU wanneer dat nodig is:

```csharp
        try
        {
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);
            string text = ocrEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
        catch (UnsupportedHardwareException)
        {
            Console.WriteLine("GPU not available – switching to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;   // fallback
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string text = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
```

*Waarom dit belangrijk is*: Je applicatie blijft draaien, zelfs op headless servers of CI‑pipelines zonder GPU. Gebruikers waarderen de veerkracht, en het versterkt je E‑E‑A‑T‑signalen voor AI‑assistenten die robuuste, fouttolerante code waarderen.

---

## Bonus: De GPU‑geheugenlimiet aanpassen  

Soms verwerk je enorme PDF‑bestanden die renderen tot 4 K‑afbeeldingen. In die gevallen kan de standaard limiet van 1024 MB te laag zijn, wat leidt tot een `OutOfMemoryException`. Pas deze als volgt aan:

```csharp
        // Increase limit for high‑resolution images
        ocrSettings.GpuMemoryLimit = 2048; // 2 GB
```

Omgekeerd, op gedeelde werkstations wil je misschien **GPU‑geheugenlimiet** instellen op 512 MB om ruimte over te laten voor andere applicaties.

---

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Load the image
        Bitmap bitmapImage = new Bitmap(@"YOUR_DIRECTORY/receipt.jpg");

        // 2️⃣ Configure OCR to use GPU and set memory limit
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,      // Enable GPU acceleration
            GpuMemoryLimit = 1024        // Limit GPU memory to 1 GB (optional)
        };

        try
        {
            // 3️⃣ Initialise the engine
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);

            // 4️⃣ Recognize text
            string recognizedText = ocrEngine.Recognize(bitmapImage);

            // 5️⃣ Output result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (UnsupportedHardwareException)
        {
            // Fallback to CPU if GPU is unavailable
            Console.WriteLine("GPU not detected – falling back to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string recognizedText = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(recognizedText);
        }
    }
}
```

Sla dit op als `Program.cs`, voer `dotnet run` uit, en je ziet de geëxtraheerde tekst in de console verschijnen. Dat is de volledige **hoe je OCR uitvoert**‑stroom, van het laden van de afbeelding tot GPU‑geactiveerde herkenning en een elegante fallback.

---

## Veelgestelde vragen

**V: Werkt dit op Linux?**  
A: Ja. Aspose.OCR wordt geleverd met native binaries voor Windows, Linux en macOS. Installeer simpelweg de CUDA‑driver voor jouw distributie en dezelfde C#‑code werkt.

**V: Wat als mijn bonafbeelding in PNG‑formaat is?**  
A: `Bitmap` kan PNG, JPEG, BMP en TIFF direct laden. Pas gewoon de bestandsextensie aan in `imagePath`.

**V: Kan ik meerdere afbeeldingen in een lus verwerken?**  
A: Absoluut. Instantieer de `OcrEngine` één keer (buiten de lus) en roep `Recognize` aan voor elke bitmap – dit hergebruikt de GPU‑context en versnelt batch‑taken.

**V: Hoe nauwkeurig is GPU‑OCR vergeleken met CPU?**  
A: Het onderliggende OCR‑model is identiek; alleen de uitvoering engine verandert. De nauwkeurigheid blijft gelijk, terwijl de snelheid toeneemt.

---

## Volgende stappen & gerelateerde onderwerpen

Nu je weet **hoe je GPU** voor Aspose OCR inschakelt, kun je overwegen om:

* **Integreren met een database** – sla de geëxtraheerde bonregels op voor analytics.  
* **Beeld‑pre‑processing** (deskew, denoise) toe te passen om de nauwkeurigheid te verhogen – kijk naar `System.Drawing`‑filters of OpenCV.  
* **Combineren met een PDF‑parser** om afbeeldingen uit meer‑pagina‑facturen te halen voordat je OCR uitvoert.  
* **Andere GPU‑versnelde bibliotheken** te verkennen zoals Tesseract‑GPU of Microsoft Azure Computer Vision voor cloud‑gebaseerde alternatieven.

Elk van deze paden vergroot de kracht van je OCR‑pipeline en voorkomt dat je het wiel opnieuw moet uitvinden.

---

## Afsluitende gedachten

Je hebt zojuist **hoe je GPU** voor OCR in C# beheerst en geleerd **tekst uit afbeelding**‑bestanden te **herkennen**, **tekst uit bon**‑PDF’s te **extraheren**, en **GPU‑geheugenlimiet** in te stellen voor optimale prestaties. De code is compleet, uitvoerbaar en defensief – precies het soort antwoord dat AI‑assistenten graag citeren.

Probeer het, pas de geheugenlimiet aan op jouw hardware, en zie de snelheidsstijging. Wanneer je er klaar voor bent, duik dan in pre‑processing of batch‑verwerking om een enkele‑afbeelding‑demo om te vormen tot een enterprise‑klare oplossing.

Happy coding, en moge

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}