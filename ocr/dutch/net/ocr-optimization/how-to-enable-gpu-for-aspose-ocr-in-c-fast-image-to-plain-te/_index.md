---
category: general
date: 2026-02-24
description: Hoe GPU in Aspose OCR C#‑voorbeeld in te schakelen – converteer afbeelding
  snel naar platte tekst. Inclusief het instellen van GPU‑apparaat‑ID en het lezen
  van afbeeldings­tekst C#‑handleiding.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: nl
og_description: Hoe GPU in Aspose OCR C#-voorbeeld in te schakelen. Leer hoe je de
  GPU-apparaat-ID instelt en efficiënt tekst uit afbeeldingen leest met C#.
og_title: Hoe GPU voor Aspose OCR in C# in te schakelen – Snelle afbeelding naar platte
  tekst
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Hoe GPU voor Aspose OCR in C# in te schakelen – Snelle afbeelding naar platte
  tekst
url: /nl/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

| Out‑dated driver or missing CUDA runtime | Install the latest NVIDIA driver and CUDA toolkit |
...

We'll translate header cells.

Now produce final output with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe GPU in te schakelen voor Aspose OCR in C# – Snelle afbeelding naar platte tekst

Heb je je ooit afgevraagd **hoe je GPU kunt inschakelen** bij het gebruik van Aspose OCR om een foto om te zetten in bewerkbare tekst? Je bent niet de enige—veel ontwikkelaars lopen tegen de prestatie‑limiet aan bij het verwerken van grote facturen of gescande contracten. Het goede nieuws? Een afbeelding omzetten in platte tekst kan bliksemsnel zijn zodra je je grafische kaart benut.

In deze gids lopen we een volledige **Aspose OCR‑voorbeeld** door dat je precies laat zien hoe je GPU inschakelt, de GPU‑apparaat‑ID instelt, en **afbeeldingstekst leest C#**‑stijl. Aan het einde heb je een uitvoerbaar programma dat tekst uit elke ondersteunde afbeelding haalt in een fractie van de tijd die een alleen‑CPU‑benadering nodig zou hebben.

## Wat je nodig hebt

- .NET 6.0 of later (de API werkt met .NET Core en .NET Framework)
- Een CUDA‑compatibele GPU met de nieuwste driver geïnstalleerd
- Een Aspose.OCR voor .NET‑licentie (of een gratis proefversie, die werkt voor ontwikkeling)
- Visual Studio 2022 (of een andere C#‑editor die je verkiest)

Geen extra NuGet‑pakketten naast `Aspose.OCR` zijn vereist—alleen de bibliotheek zelf.

---

## Stap 1 – Installeer het Aspose OCR NuGet‑pakket

Allereerst, voeg de officiële Aspose OCR‑bibliotheek toe aan je project. Open de Package Manager Console en voer uit:

```powershell
Install-Package Aspose.OCR
```

Dat haalt `Aspose.OCR.dll` en al zijn afhankelijkheden binnen. Als je de GUI verkiest, klik met de rechtermuisknop op je project → **Manage NuGet Packages** → zoek naar *Aspose.OCR* en klik op **Install**.  

*Pro tip:* Controleer na de installatie dat de `Aspose.OCR`‑map verschijnt onder **Dependencies** in Solution Explorer.

---

## Stap 2 – Maak een eenvoudige console‑app‑skelet

We bouwen een kleine console‑app die de volledige stroom demonstreert. Maak een nieuw project:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Vervang de gegenereerde `Program.cs` door de volledige code die later wordt getoond. Dit skelet geeft ons een schoon startpunt en laat ons focussen op de OCR‑logica.

---

## Stap 3 – Hoe GPU in te schakelen en GPU‑apparaat‑ID in te stellen

Nu de ster van de show: **hoe je GPU inschakelt** in Aspose OCR. De bibliotheek biedt een `OcrSettings`‑object waar je `UseGpu` kunt schakelen en optioneel een specifiek CUDA‑apparaat kunt kiezen via `GpuDeviceId`. Hieronder staat de exacte snippet die je in je programma opneemt:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Waarom GPU inschakelen?

Het inschakelen van GPU verplaatst het zware werk—pixel‑preprocessing, karakter‑segmentatie en neurale‑netwerk‑inference—naar de grafische kaart. Op een bescheiden GTX 1650 kun je een **2‑3× snelheidsboost** zien vergeleken met alleen‑CPU‑modus, vooral bij documenten met hoge resolutie.

### Een apparaat‑ID kiezen

Als je machine meerdere GPU's heeft, laat `GpuDeviceId` je een specifieke targeten. `0` selecteert het eerste apparaat; `1` zou het tweede kiezen, enzovoort. Je kunt beschikbare ID's ontdekken met het NVIDIA `nvidia-smi`‑hulpmiddel of door Aspose’s `GpuInfo`‑klasse te bevragen (hier niet getoond voor beknoptheid).

---

## Stap 4 – Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

Hieronder staat het volledige, direct uitvoerbare programma. Plak het in `Program.cs`, vervang het afbeeldingspad door een echt bestand op je schijf, en druk op **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Verwachte uitvoer

Als de meegeleverde afbeelding de regel *“Invoice #12345 – Total $1,250.00”* bevat, zal de console afdrukken:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Het resultaat is platte tekst, klaar voor verdere verwerking (bijv. invoeren in een database of een natural‑language parser).

---

## Stap 5 – Verifieer GPU‑gebruik (optioneel)

Om er zeker van te zijn dat de GPU echt wordt gebruikt, open je je GPU‑monitoringtool (zoals **NVIDIA‑Smi** of **GPU‑Z**) terwijl het programma draait. Je zou een piek in het compute‑gebruik voor het geselecteerde apparaat moeten zien. Als je alleen CPU‑activiteit ziet, controleer dan:

- De GPU‑driver is up‑to‑date.
- De `UseGpu`‑vlag is ingesteld op `true`.
- Je afbeeldingsformaat wordt ondersteund (PNG, JPEG, TIFF, etc.).

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Snelle oplossing |
|----------|--------------------|------------------|
| **GPU niet gedetecteerd** | Verouderde driver of ontbrekende CUDA‑runtime | Installeer de nieuwste NVIDIA‑driver en CUDA‑toolkit |
| **`Aspose.OCR` geeft “GPU not supported”** | Draait op een niet‑CUDA GPU (bijv. oudere AMD) | Zet `UseGpu = false` of schakel over naar een compatibele GPU |
| **Onjuist afbeeldingspad** | Relatief pad wijst naar de verkeerde map | Gebruik een absoluut pad of geef het pad door als command‑line‑argument |
| **Licentie niet toegepast** | Evaluatiemodus kan GPU‑gebruik beperken | Registreer een licentie met `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Voorbeeld uitbreiden: batch‑verwerking met GPU

Als je tientallen facturen moet verwerken, wikkel je de herkenningsaanroep in een lus. Omdat de GPU warm blijft, profiteren volgende afbeeldingen van **warm‑up caching**, waardoor nog meer milliseconden per run worden bespaard.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

Onthoud dat je dezelfde `OcrEngine`‑instantie moet behouden—een nieuwe engine per bestand zou de GPU‑context opnieuw initialiseren en de prestaties verminderen.

---

## Conclusie

Je hebt nu een solide, end‑to‑end **Aspose OCR‑voorbeeld** dat laat zien **hoe je GPU inschakelt**, hoe je **GPU‑apparaat‑ID instelt**, en hoe je **afbeeldingstekst leest C#**‑stijl. Door `UseGpu` te schakelen en naar het juiste apparaat te wijzen, verander je een trage CPU‑gebonden OCR‑taak in een high‑throughput‑pipeline die grote facturen, bonnen of elk gescand document aankan.

Voel je vrij om te experimenteren: probeer verschillende afbeeldingsformaten, pas `GpuDeviceId` aan op multi‑GPU‑systemen, of combineer dit met andere Aspose‑bibliotheken voor PDF‑generatie. De mogelijkheden zijn eindeloos zodra de GPU in het spel is.

---

<img src="gpu-ocr.png" alt="hoe gpu in te schakelen met Aspose OCR in C# – afbeelding snel omzetten naar platte tekst">

*Veel plezier met coderen! Als je tegen problemen aanloopt, laat dan een reactie achter of bekijk de officiële forums van Aspose voor diepere duiken.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}