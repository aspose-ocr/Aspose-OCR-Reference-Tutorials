---
category: general
date: 2026-01-15
description: c# ocr-handledning som visar hur du känner igen text från en bild, extraherar
  text från en faktura och konverterar bild till text med Aspose OCR på GPU:n.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: sv
og_description: c# OCR-handledning som lär dig att känna igen text från en bild, extrahera
  text från en faktura och konvertera en bild till text med Aspose OCR på GPU:n.
og_title: c# OCR‑handledning – Snabb GPU‑drivet textigenkänning
tags:
- OCR
- C#
- Aspose
- GPU
title: c# OCR-handledning – Känn igen text från bild med GPU-acceleration
url: /sv/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Känn igen text från bild med GPU-acceleration

Har du någonsin behövt en **c# ocr tutorial** som faktiskt får jobbet gjort utan oändliga försök‑och‑fel? Kanske stirrar du på en högupplöst faktura och undrar hur du **extract text from** på några sekunder. Den goda nyheten är att du inte behöver uppfinna hjulet på nytt—Aspose.OCR ger dig ett rent, GPU‑accelererat API som sköter det tunga lyftet åt dig.

I den här guiden går vi igenom ett komplett, körbart exempel som visar hur man **recognize text from image** filer, **convert image to text**, och hanterar de vanligaste fallgroparna. I slutet har du ett självständigt program som kan läsa vilken bild av ett dokument som helst, från kvitton till skannade kontrakt, och producera ren, sökbar text.

## Vad du kommer att lära dig

- Hur du installerar och refererar Aspose.OCR NuGet‑paketet.
- Hur du konfigurerar OCR‑motorn för att köra på GPU för blixtsnabb prestanda.
- Det korrekta sättet att **load image for ocr** med `OcrImage.FromFile`.
- Hur du anropar `Recognize` med önskat språk och hämtar resultatet.
- Tips för att hantera flersidiga PDF‑filer, lågkontrast‑skanningar och felhantering.

Ingen tidigare erfarenhet av Aspose krävs; bara en fungerande .NET‑utvecklingsmiljö (Visual Studio 2022 eller VS Code) och ett modest GPU (även ett integrerat Intel‑GPU räcker).

---

## Steg 1 – Installera Aspose.OCR och förbered ditt projekt

Först och främst: du behöver Aspose.OCR‑biblioteket. Det enklaste sättet är via NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Om du riktar dig mot .NET 6 eller senare kommer paketet automatiskt att hämta de inhemska GPU‑binärerna för Windows, Linux och macOS. Inga extra DLL‑filer att kopiera.

När paketet har lagts till, öppna din projektfil (`*.csproj`) och verifiera referensen:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Nu har du allt du behöver för att börja koda.

## Steg 2 – Skapa en GPU‑aktiverad OCR‑motor (c# ocr tutorial)

Kärnan i **c# ocr tutorial** är `OcrEngine`. Genom att sätta `Engine = Engine.Gpu` talar vi om för Aspose att använda grafikkortet istället för CPU:n.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Why GPU?** En GPU kan bearbeta tusentals pixlar parallellt, vilket minskar OCR‑tiden från sekunder till bråkdelar av en sekund på stora, hög‑DPI‑bilder.

## Steg 3 – Ladda bild för OCR (load image for ocr)

Att ladda bilden korrekt är viktigare än du kanske tror. `OcrImage.FromFile` stöder PNG, JPEG, BMP, TIFF och även PDF‑sidor. Den läser också bildens DPI, vilket påverkar noggrannheten.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Obs:** Om du arbetar med en PDF kan du extrahera varje sida som ett `OcrImage` och mata in dem en efter en.

## Steg 4 – Känn igen text från bild (recognize text from image)

Nu händer magin. Vi ber motorn att känna igen engelsk text, men du kan skicka vilket språk som helst som stöds av Aspose (Spanska, Tyska, Kinesiska, osv.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

`result.Text`‑egenskapen innehåller den rena strängen. Om du behöver förtroendescore för varje ord kan du inspektera `result.Regions`.

### Förväntad output

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Om bilden är suddig kan du se förvrängda tecken—det är här förbehandlingen från Steg 3 hjälper.

## Steg 5 – Extrahera text från faktura – verkligt exempel

Anta att du har en mapp full av skannade fakturor och vill plocka ut totalsumman. Nedan är en snabb utökning av föregående kod som använder ett enkelt reguljärt uttryck.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Du skulle anropa `ExtractTotalAmount(result.Text);` direkt efter att ha skrivit ut OCR‑resultatet. Detta visar hur enkelt det är att **extract text from invoice** filer när du har den råa strängen.

## Steg 6 – Konvertera bild till text i bulk (convert image to text)

Att bearbeta en enda fil är okej för en demo, men produktionskod måste ofta hantera dussintals eller hundratals bilder. Här är en kort loop som bearbetar en hel katalog:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Att köra `ProcessFolder(ocrEngine, @"C:\Invoices")` kommer att **convert image to text** för varje stödd fil i mappen, med GPU‑acceleration för hastighet.

## Edge Cases och vanliga fallgropar

| Situation | Varför det händer | Snabb lösning |
|-----------|-------------------|---------------|
| **Low‑contrast scan** | OCR har svårt att skilja förgrund från bakgrund. | Öka kontrasten (`ImagePreprocessor.AdjustContrast`) eller tillämpa adaptiv tröskelvärdesättning. |
| **Multi‑page PDF** | `OcrImage.FromFile` läser bara den första sidan. | Använd `PdfDocument` för att extrahera varje sida som ett `OcrImage` och loopa. |
| **Unsupported language** | Standardinställningen för språk är engelska. | Skicka `Language.Spanish` eller något annat stödjande enum‑värde. |
| **GPU not detected** | Saknade inhemska binärer eller föråldrad drivrutin. | Verifiera att GPU‑drivrutinen är uppdaterad; installera om NuGet‑paketet med flaggan `-runtime`. |
| **Out‑of‑memory on huge images** | GPU‑minnet är begränsat. | Skala ner bilden (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i en ny konsolapp. Det inkluderar alla hjälpfunktioner som diskuterats ovan.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}