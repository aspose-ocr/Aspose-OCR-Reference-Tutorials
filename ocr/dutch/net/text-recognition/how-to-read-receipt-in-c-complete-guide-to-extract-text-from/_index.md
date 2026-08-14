---
category: general
date: 2026-02-20
description: Leer hoe je een bon kunt lezen in C# door tekst uit een afbeelding te
  extraheren en deze naar JSON te converteren. Stapsgewijze code met Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: nl
og_description: Ontdek hoe je een bon kunt lezen in C# door een afbeeldingsbestand
  te laden, tekst te extraheren met Aspose OCR en het resultaat naar JSON te converteren.
  Volledig codevoorbeeld.
og_title: Hoe een ontvangstbewijs te lezen in C# – Tekst extraheren, converteren naar
  JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Hoe een bon te lezen in C# – Complete gids voor het extraheren van tekst uit
  een afbeelding
url: /nl/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

to "Oplossing / Aanbeveling". Keep bold text maybe.

Also keep code snippets unchanged.

Now produce final content with all translations.

Be careful not to translate shortcodes at end.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Kassabon te Lezen in C# – Complete Gids

Heb je je ooit afgevraagd **hoe je een kassabon** afbeeldingen programmatisch kunt lezen? Misschien bouw je een uitgaven‑tracking app en moet je regel‑items halen uit een foto van een supermarktbon. Naar mijn ervaring is het grootste pijnpunt het omzetten van die wazige JPEG naar gestructureerde data die je daadwerkelijk kunt gebruiken. Het goede nieuws? Met een paar regels C# en Aspose OCR kun je **tekst uit afbeelding extraheren**, vervolgens **afbeelding naar JSON converteren** op een manier die bijna magisch aanvoelt.

In deze tutorial loop je weg met een kant‑klaar werkende oplossing die **een afbeelding bestand laadt C#**, OCR uitvoert, en een gedetailleerde JSON‑payload teruggeeft. Geen externe services, geen ingewikkelde REST‑calls — gewoon pure .NET‑code die je in elk console‑ of ASP.NET‑project kunt stoppen. Aan het einde begrijp je waarom elke stap belangrijk is, hoe je veelvoorkomende randgevallen afhandelt (zoals niet‑standaard kassabonformaten), en hoe de JSON‑output er precies uitziet.

## Wat je nodig hebt

- **.NET 6.0 of later** – de code gebruikt `System.Drawing.Common` dat ondersteund wordt op Windows, Linux en macOS.
- **Aspose.OCR for .NET** – je kunt een gratis proef‑NuGet‑pakket (`Aspose.OCR`) pakken of een gelicentieerde kopie gebruiken als je die hebt.
- Een **voorbeeld kassabon afbeelding** (`receipt.jpg`) geplaatst op een locatie die je app kan lezen.
- Elke IDE die je wilt (Visual Studio, Rider, VS Code).  

Dat is alles. Geen extra configuratie, geen API‑sleutels.

---

## Stap 1 – Laad het Afbeeldingsbestand C# (Primaire Trefwoord in Actie)

Voordat de OCR‑engine zijn magie kan doen, moet je de foto in het geheugen krijgen. Dit is de klassieke “load image file C#” stap die veel ontwikkelaars over het hoofd zien.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Waarom dit belangrijk is:**  
`Image.FromFile` leest het bestand *eenmalig* en houdt een handle open, wat perfect is voor een snelle OCR‑run. Als je veel bonnetjes in een lus verwerkt, overweeg dan `Image.FromStream` te gebruiken om het bestand niet te vergrendelen.

> **Pro tip:** Als je een *FileNotFoundException* krijgt, controleer dan het pad en zorg dat de afbeelding daadwerkelijk bestaat. Relatieve paden werken ook (`"./receipt.jpg"`), maar absolute paden zijn veiliger voor productie‑jobs.

## Stap 2 – Maak en Configureer de OCR‑Engine

Aspose OCR wordt geleverd met een kant‑klare `OcrEngine`. Je hoeft geen model te trainen; de bibliotheek weet al hoe hij gedrukte tekst moet lezen, wat precies is wat de meeste kassabonnen gebruiken.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Waarom we deze opties instellen:**  
`DetectOrientation` vertelt de engine om de afbeelding automatisch te draaien als de kassabon ondersteboven is gescand. Het instellen van de taal beperkt de tekenset, wat de nauwkeurigheid kan verbeteren — vooral wanneer je alleen Engelstalige alfanumerieke data nodig hebt.

## Stap 3 – Herken de Afbeelding en Converteer naar JSON

Nu komt het leuke deel: **tekst uit afbeelding extraheren** en **afbeelding naar JSON converteren** in één enkele aanroep.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

De `RecognizeToJson`‑methode retourneert een rijke JSON‑structuur die bevat:

- `Text`: de platte samengevoegde tekst.
- `Lines`: een array van lijnobjecten met coördinaten.
- `Words`: elk woord met een vertrouwensscore.
- `Regions`: begrenzende vakken voor gedetecteerde tekstblokken.

Je kunt deze JSON deserialiseren naar een C#‑object als je getypeerde toegang nodig hebt, maar voor veel scenario’s is het afdrukken van de ruwe JSON voldoende.

## Stap 4 – Output de JSON (of Sla Het Op)

Laten we de output bekijken en bespreken wat je ermee kunt doen.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Voorbeeldoutput

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Wat nu?**  
Parse de `Lines`‑array om het `Total`‑bedrag eruit te halen, of stuur de JSON door naar een downstream‑service die onkostennotities opslaat. Omdat het resultaat al JSON is, kun je het direct in elke NoSQL‑database, Azure Function, of Power Automate‑flow injecteren.

## Stap 5 – Veelvoorkomende Randgevallen Afhandelen

Zelfs de beste OCR‑engines struikelen over een paar dingen. Hieronder staan scenario’s die je kunt tegenkomen tijdens het leren **hoe je een kassabon** afbeeldingen leest.

| Situatie | Oplossing / Aanbeveling |
|-----------|------------------------|
| **Low‑resolution kassabon (≤ 150 dpi)** | Schaal de afbeelding eerst op met `Bitmap` en `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Gedraaide of scheve kassabon** | Houd `DetectOrientation = true`. Bij ernstige scheefstand, pre‑process met `Image.RotateFlip` of een derde‑partij bibliotheek zoals OpenCV. |
| **Gekleurde achtergrond (bijv. kassabon op een tafel)** | Converteer naar grijstinten en verhoog het contrast vóór OCR (`ImageAttributes`). |
| **Meerdere kassabonnen op één foto** | Snijd elk kassabon‑gebied handmatig bij of gebruik `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Grote bestanden die OutOfMemory veroorzaken** | Gebruik `using`‑blokken om `Image`‑objecten direct te disposen, of verwerk in delen. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

## Stap 6 – Volledig Werkend Voorbeeld (Kopieer‑Plak Klaar)

Hieronder staat het *complete* programma dat je nu meteen kunt compileren. Het bevat alle stappen, de juiste `using`‑directives, en nette foutafhandeling.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Run het:**  
`dotnet run` vanuit de projectmap. Als alles correct is ingesteld zie je de JSON in de console en wordt deze naast je kassabon‑afbeelding opgeslagen.

## Conclusie

We hebben zojuist **hoe je een kassabon** afbeeldingen in C# van begin tot eind behandeld. Door de afbeelding te laden, Aspose OCR te configureren, en `RecognizeToJson` aan te roepen, kun je **tekst uit afbeelding extraheren** en **afbeelding naar JSON converteren** met praktisch geen boilerplate. De aanpak schaalt — van een enkele demo‑bon tot een batch‑processor die ’s nachts honderden bonnen afhandelt.

Volgende stappen die je kunt verkennen:

- **Parse de JSON** om data zoals datums, totalen en regelitems te halen (gebruik `System.Text.Json` of `Newtonsoft.Json`).
- **Integreer met een database** (SQL, Cosmos DB) om onkosten automatisch op te slaan.
- **Voeg een UI toe** (WinForms, WPF, of Blazor) zodat gebruikers kassabonnen kunnen slepen‑en‑neerzetten.
- **Vervang Aspose OCR** door een andere engine (Tesseract, Microsoft Azure OCR) als licenties een zorg zijn — houd gewoon het “load image file C#” patroon aan.

Voel je vrij om te experimenteren, dingen kapot te maken, en daarna hier terug te komen voor een opfrisser. Als je vastloopt, zijn de community (en de Aspose‑forums) uitstekende plekken om vragen te stellen. Veel programmeerplezier, en geniet van het omzetten van papieren kassabonnen naar schone, doorzoekbare data!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}