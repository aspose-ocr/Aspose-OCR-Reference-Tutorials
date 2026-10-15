---
category: general
date: 2026-03-07
description: Tekst extraheren uit PNG‑bestanden met C#. Leer hoe je een afbeelding
  naar tekst converteert in C# en lees snel tekst van gescande afbeeldingen.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: nl
og_description: Haal tekst uit PNG‑bestanden met C#. Deze gids laat zien hoe je een
  afbeelding naar tekst converteert met C# en tekst leest uit gescande afbeeldingen
  met Aspose OCR.
og_title: Tekst extraheren uit PNG in C# – Volledige OCR-gids
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Tekst extraheren uit PNG in C# – Volledige OCR-gids
url: /nl/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit PNG in C# – Volledige OCR-gids

Heb je ooit **tekst uit PNG**‑bestanden moeten halen, maar wist je niet waar te beginnen? Je bent niet de enige—de meeste ontwikkelaars komen tegen die muur wanneer ze voor het eerst gescande afbeeldingen of screenshots tegenkomen die doorzoekbare tekst moeten worden. Het goede nieuws? Met een paar regels C# en Aspose OCR kun je elke PNG in een handomdraai omzetten naar bewerkbare strings.

In deze tutorial lopen we het volledige proces door: van het vinden van PNG‑bestanden op schijf, het starten van OCR‑taken parallel, tot het tonen van een nette preview van elk resultaat. Aan het einde weet je hoe je **image to text C#** kunt uitvoeren, kun je **tekst lezen uit gescande afbeeldingen** efficiënt, en zie je de beste manier om **OCR op afbeeldingen uit te voeren** zonder je UI‑thread te belasten.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook op .NET Core en .NET Framework)  
- Aspose.OCR NuGet‑pakket (`Install-Package Aspose.OCR`)  
- Een map vol *.png*-bestanden die je wilt verwerken  
- Elke IDE die je wilt (Visual Studio, VS Code, Rider…)

Er is geen extra configuratie nodig; de bibliotheek wordt geleverd met alles wat nodig is om PNG’s, JPEG’s, TIFF’s, wat je maar wilt, te decoderen.

## Stap 1: Alle PNG‑bestanden vinden – “Extract Text from PNG” begint

Eerst moeten we elke PNG vinden waarop we OCR willen uitvoeren. `Directory.GetFiles` gebruiken is snel en betrouwbaar.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Waarom dit belangrijk is:* Het één keer scannen van de map houdt de rest van de pijplijn simpel, en de vroege controle voorkomt een stille “geen output”‑situatie die later moeilijk te debuggen is.

## Stap 2: Parallel OCR‑taken starten – Efficient **run OCR on images**

OCR sequentieel uitvoeren is prima voor een handvol bestanden, maar real‑world projecten hebben vaak te maken met tientallen of honderden. Door een `Task` per afbeelding te starten houden we de CPU bezig terwijl de bibliotheek het zware werk doet.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Pro tip:* `Task.Run` laadt het werk naar de thread‑pool, waardoor je UI (als je die hebt) responsief blijft. Op een server schaalt hetzelfde patroon netjes over de cores.

## Stap 3: Alle taken afwachten – Resultaten verzamelen

Nu wachten we tot elke OCR‑bewerking klaar is. `Task.WhenAll` retourneert een array die overeenkomt met de oorspronkelijke bestandsvolgorde, waardoor het eenvoudig is om resultaten aan bestandsnamen te koppelen.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Opmerking voor randgevallen:* Als één afbeelding een uitzondering gooit (beschadigd bestand, niet‑ondersteund formaat) zal de hele `WhenAll` de uitzondering doorgeven. Je kunt de interne `Task.Run` omhullen met een try/catch en een lege string of een diagnostisch bericht teruggeven als je fouttolerantie nodig hebt.

## Stap 4: Een preview tonen – Verifieer de **convert image to text C#** output

Een snelle preview helpt je bevestigen dat de OCR heeft gewerkt voordat je de data ergens anders opslaat.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Typische console‑output ziet er als volgt uit:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Als de preview onzin toont, controleer dan de beeldkwaliteit of overweeg pre‑processing (bijv. binarisatie) – maar voor de meeste schone PNG’s doet Aspose OCR het in één keer goed.

## Optioneel: Resultaten opslaan naar een CSV – Een real‑world use case

De meeste projecten hebben de geëxtraheerde tekst in een gestructureerd formaat nodig. Hieronder staat een kleine helper die de bestandsnaam en volledige OCR‑tekst naar een CSV‑bestand schrijft.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Nu kun je de CSV importeren in Excel, Power BI, of elk downstream‑systeem dat **read text from scanned images** verwacht.

## Veelgestelde vragen

**Wat als mijn PNG’s enorm zijn (meer dan 5 MB)?**  
Aspose OCR verkleint grote afbeeldingen automatisch om het geheugenverbruik beheersbaar te houden, maar je kunt handmatig de grootte aanpassen met `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` om de breedte te beperken tot 2000 px terwijl de beeldverhouding behouden blijft.

**Kan ik dit op Linux draaien?**  
Ja. Aspose OCR is cross‑platform; zorg er alleen voor dat de native afhankelijkheden (`libgdiplus` op sommige distributies) geïnstalleerd zijn.

**Staat de OCR‑taal standaard op Engels?**  
Klopt. Als je een andere taal nodig hebt, stel dan `engine.Language = OcrLanguage.French;` (of een andere ondersteunde enum) in vóór het aanroepen van `Recognize()`.

**Hoe ga ik om met met wachtwoord beveiligde PDF’s die PNG’s bevatten?**  
Converteer eerst de PDF‑pagina’s naar afbeeldingen (met Aspose PDF of een andere bibliotheek), en voer die PNG’s vervolgens door dezelfde pijplijn. Het principe van **how to run OCR on images** blijft ongewijzigd.

## Volledig werkend voorbeeld (Async Main)

Hieronder staat een zelf‑containend programma dat je kunt copy‑pasten in een console‑project. Het bevat alle bovenstaande onderdelen, plus een kleine helper om de invoermap te valideren.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Verwachte output** (voorbeeld voor twee PNG’s):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Afronding

We hebben zojuist alles behandeld wat je nodig hebt om **tekst uit PNG**‑bestanden te extraheren met C#. Van het vinden van de bestanden, het starten van parallelle OCR‑taken, het previewen van de strings, tot het opslaan in een CSV—deze gids biedt een productie‑klaar patroon voor **convert image to text C#** scenario’s.  

Als je klaar bent voor de volgende stap, probeer dan dezelfde pijplijn te gebruiken voor JPEG‑ of TIFF‑bestanden, experimenteer met verschillende OCR‑talen, of koppel de resultaten aan een zoekindex zodat je **tekst kunt lezen uit gescande afbeeldingen** in één oogopslag.  

Heb je vragen over randgevallen, prestatie‑optimalisatie, of licenties? Laat een reactie achter of ping de Aspose‑community—happy coding!  

![Voorbeeld van tekst extraheren uit PNG](extract-text-png.png "Tekst extraheren uit PNG met Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}